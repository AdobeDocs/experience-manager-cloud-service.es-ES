---
title: 'Administrador de nube: Preguntas más frecuentes sobre los Cloud Services'
seo-title: Preguntas más frecuentes sobre Cloud Manager
description: Consulte las preguntas más frecuentes sobre Cloud Manager para Cloud Services para obtener algunos consejos sobre la solución de problemas
seo-description: 'Siga esta página para obtener respuestas sobre Cloud Manager: Preguntas más frecuentes sobre los Cloud Services'
translation-type: tm+mt
source-git-commit: 75a5ff02e5f7c0e0e3ba42c8559851d3c98c3c8d
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 0%

---


# Preguntas más frecuentes sobre Cloud Manager {#cloud-manager-faqs}

La siguiente sección proporciona respuestas a las preguntas más frecuentes relacionadas con Cloud Manager para Cloud Services.

## ¿Es posible utilizar Java 11 con las compilaciones de Cloud Manager? {#java-11-cloud-manager}

La compilación de AEM Cloud Manager falla al intentar cambiar la compilación de Java 8 a 11. El problema puede tener muchas causas y las más comunes se documentan a continuación:

* Añada el complemento maven-toolchain-plugin con la configuración correcta para Java 11 como se documenta [aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/create-application-project/using-the-wizard.html?lang=en#getting-started).  Por ejemplo, consulte el [código de proyecto de muestra de wknd](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75).

* Si encuentra el error siguiente, debe eliminar el uso de `maven-scr-plugin` y convertir todas las anotaciones OSGi en anotaciones OSGi R6. Para obtener instrucciones, consulte [aquí](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/).

   `[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]`

* Para las compilaciones de Cloud Manager, el complemento maven enforcer falla con el error `"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion"`. Se trata de un problema conocido debido a que Cloud Manager utiliza una versión diferente de Java para ejecutar el comando maestro en lugar de compilar código. Por ahora, omita `requireJavaVersion` de las configuraciones de maven-enforcer-plugin.

## Nuestra implementación está bloqueada porque la comprobación de calidad del código falló. ¿Hay alguna manera de evitar este cheque? {#deployment-stuck}

Todos los errores de calidad del código, excepto *Clasificación de seguridad*, son métricas no críticas, por lo que se pueden evitar expandiendo los elementos en la interfaz de usuario de los resultados.

Un usuario con la función [Deployment Manager, Project Manager o Business Owner](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html?lang=en#requirements) puede anular los problemas, en cuyo caso la canalización continúa o puede aceptar los problemas, en cuyo caso la canalización se detiene con un error.  Consulte [Puerta de tres niveles mientras se ejecuta una canalización](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#how-to-use) para obtener más detalles.


## ¿Se nos permite utilizar SNAPSHOT en la versión del proyecto Maven? ¿Cómo funciona el control de versiones de los paquetes y los archivos jares del paquete para las implementaciones de fase y producción? {#snapshot-version}

Consulte los siguientes escenarios para obtener información sobre la versión de los paquetes y los archivos jar del paquete para implementaciones de fase y producción:

1. Para implementaciones de desarrolladores, los archivos de rama de Git `pom.xml` deben contener `-SNAPSHOT` al final del valor `<version>`. Esto permite la implementación posterior cuando la versión no cambia para instalarse. En las implementaciones para desarrolladores, no se agrega ni se genera ninguna versión automática para la compilación mecanizada.

1. En la implementación de Etapa y Producción, se genera una versión automática como documentada [aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/activating-maven-project.html?lang=en#managing-code).

1. Para las versiones personalizadas en las implementaciones de fase y producción, establezca una versión maquetada de 3 partes como `1.0.0`. Actualice la versión cada vez que tenga que realizar otra implementación en producción.

1. Cloud Manager agrega automáticamente su versión a las compilaciones de Stage y Production, e incluso crea una rama Git. No se requiere una configuración especial. Si se omite el paso 3 anterior, la implementación seguiría funcionando correctamente y se establecería una versión automáticamente.

1. No hay problemas, si deja la versión con `-SNAPSHOT` para compilaciones o implementaciones de fase y producción. Cloud Manager establece automáticamente un número de versión correcto y crea una etiqueta para usted en Git. Esta etiqueta se puede consultar más adelante, si es necesario.

1. Si desea probar algún código experimental en entorno de desarrollo, puede crear una nueva rama Git y configurar la canalización para utilizar esa rama diferente. Esto resulta útil cuando el inicio de implementaciones falla y le gustaría probarlo con versiones anteriores del código para ver cuándo se interrumpe.

   El comando Git de abajo crea una rama remota denominada *testbranch1* con respecto a una confirmación específica `485548e4fbafbc83b11c3cb12b035c9d26b6532b` preexistente.  Esta rama especial se puede usar en Cloud Manager sin afectar a otras ramas:

   `git push origin 485548e4fbafbc83b11c3cb12b035c9d26b6532b:refs/heads/testbranch1`

   Consulte la [documentación de Git](https://git-scm.com/book/en/v2/Git-Internals-Git-References) para obtener más detalles.

   Si desea eliminar la rama de prueba más adelante, utilice el comando delete:

   `git push origin --delete testbranch1`

## La compilación de Maven falla en las implementaciones de Cloud Manager pero se genera localmente sin errores. ¿Cómo depurar? {#maven-build-fail}

Consulte [Recurso de Git](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md) para obtener más detalles.

## ¿Qué hacer si la implementación de Cloud Manager falla en el paso de implementación de AEM como Entorno de Cloud Service? {#cloud-manager-deployment-cloud-service}

El motivo más común de error de las implementaciones es que el usuario *sling-distribution-importer* no tiene permisos suficientes.
Consulte el ejemplo siguiente para comprender un problema, una causa y una solución:

****
ProblemaDurante la implementación de Cloud Manager en AEM como entorno de Cloud Service, el paso de implementación falla y se observan errores como los que se muestran a continuación.

`[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.jackrabbit.vault.fs.io.Importer Error while committing changes. Retrying import from checkpoint at /. Retries 4/10`
`[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.sling.distribution.journal.impl.subscriber DistributionSubscriber Error processing queue item`
`org.apache.sling.distribution.common.DistributionException: Error processing distribution package`
`dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 162/infinite.`
`Caused by: org.apache.sling.api.resource.PersistenceException: Unable to commit changes to session.`
`Caused by: javax.jcr.AccessDeniedException: OakAccess0000: Access denied [EventAdminAsyncThread #7] org.apache.sling.distribution.journal.impl.publisher.DistributionPublisher [null] Error processing distribution package` `dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 344/infinite. Message: Error trying to extract package at path /etc/packages/com.myapp/myapp-base.ui.content-5.1.0-SNAPSHOT.`

**Causa**

El usuario de sling-distribution-importer necesita permisos adicionales para las rutas de contenido definidas en el paquete ui.content.  Esto generalmente significa que necesitamos agregar permisos para /conf y /var.

****
SoluciónLa solución a esto es agregar un script de  [configuración OSGi de ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#deploying) RepositoryInitializer al paquete de implementación de aplicaciones para agregar ACL para el usuario de sling-distribution-importer.
En el error de ejemplo anterior, el paquete myapp-base.ui.content-*.zip incluye contenido en `/conf` y `/var/workflow`. Para que la implementación no falle, necesitaríamos agregar permisos para sling-distribution-importer en esas rutas.
Este es un ejemplo [org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config](https://github.com/cqsupport/cloud-manager/blob/main/org.apache.sling.jcr.repoinit.RepositoryInitializer-distribution.config) de una configuración OSGi de este tipo que agrega permisos adicionales para el usuario sling-distribution-importer.  Esta configuración agrega permisos en /var.  Este archivo xml que aparece debajo de [1] debe agregarse al paquete de la aplicación en `/apps/myapp/config` (donde myapp es la carpeta donde se almacena el código de la aplicación).
org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config

1. Si la *sling-distribution-importer* no es la causa, la implementación podría estar fallando debido a una configuración OSGi incorrecta que rompe un servicio de fuera del equipo. Compruebe los registros durante la implementación para ver si hay errores obvios.

1. Es posible que la implementación falle debido a que las configuraciones del despachante o apache son erróneas. Asegúrese de probar las configuraciones de Apache y Dispatcher localmente mediante la imagen de Docker incluida en el SDK. Consulte [Dispatcher en la nube](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#content-delivery) sobre cómo configurar el contenedor de Dispatcher Docker para facilitar las pruebas locales.

1. Es posible que la implementación falle debido a algún otro error durante la replicación de los paquetes de contenido (distribución sling) de instancias de creación a publicación.

   Consulte los pasos a continuación para simular esto en una configuración local:

   * Instalación de una instancia de Autor y Publicación (con los últimos tarros AEM SDK)
   * Inicie sesión en la instancia de autor
   * Vaya a **Herramientas** -> **Implementación** -> **Distribución**
   * Distribuya los paquetes de contenido que forman parte de la base de código y vea si la cola se bloquea con un error

## No se puede establecer una variable mediante el administrador de nube de AIO establecer variables de canalización. ¿Cómo depurar estos problemas? {#set-variable}

Si está obteniendo un error `403` al intentar realizar la lista o establecer variables de canalización a través de comandos similares a los que se muestran a continuación, debe agregarlo como una función de producto *Administrador de implementación* Administrador de nube en el Admin Console.\
Consulte [Permisos de API](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md) para obtener más información.

Comandos y errores relacionados:

`$ aio cloudmanager:list-pipeline-variables 222`

*Error*:  `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1`

*Error*:  `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1`

`setting variables... !`

*Error*:  `Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)`
