---
title: 'Cloud Manager: preguntas más frecuentes sobre los Cloud Services'
seo-title: Cloud Manager FAQs
description: Consulte las preguntas frecuentes de Cloud Manager para Cloud Services para obtener algunas sugerencias para la resolución de problemas
seo-description: Follow this page to get answers on Cloud Manager - Cloud Services FAQs
exl-id: eed148a3-4a40-4dce-bc72-c7210e8fd550
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 1%

---

# Preguntas frecuentes sobre Cloud Manager {#cloud-manager-faqs}

La siguiente sección proporciona respuestas a las preguntas más frecuentes relacionadas con Cloud Manager para Cloud Services.

## ¿Es posible utilizar Java 11 con compilaciones de Cloud Manager? {#java-11-cloud-manager}

AEM compilación de Cloud Manager falla al intentar cambiar la compilación de Java 8 a 11. El problema puede tener muchas causas y las más comunes se documentan a continuación:

* Añada el complemento toolchain con la configuración correcta para Java 11 como está documentado [here](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/create-application-project/using-the-wizard.html?lang=en#getting-started).  Por ejemplo, consulte la [código de proyecto de ejemplo wknd](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75).

* Si encuentra el siguiente error, debe eliminar el uso de `maven-scr-plugin` y convertir todas las anotaciones OSGi en anotaciones OSGi R6. Para obtener instrucciones, consulte [here](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/).

   `[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]`

* Para las compilaciones de Cloud Manager, el complemento maven enforcer falla con error `"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion"`. Este es un problema conocido debido a que Cloud Manager utiliza una versión diferente de Java para ejecutar el comando maven en comparación con el código de compilación. Por ahora, omita `requireJavaVersion` desde las configuraciones de maven-enforcer-plugin.

## Nuestra implementación está atascada porque la comprobación de calidad del código falló. ¿Hay alguna manera de evitar este cheque? {#deployment-stuck}

Todos los errores de calidad de código excepto *Clasificación de seguridad* son métricas no críticas, por lo que se pueden evitar expandiendo los elementos en la interfaz de usuario de los resultados.

Un usuario con [Administrador de implementación, Administrador de proyectos o Propietario empresarial](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html?lang=en#requirements) puede anular los problemas, en cuyo caso la canalización continúa o pueden aceptar los problemas, en cuyo caso la canalización se detiene con un error.  Consulte [Puerta de tres niveles mientras se ejecuta una canalización](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#how-to-use) para obtener más información.


## ¿Se nos permite utilizar SNAPSHOT en la versión del proyecto Maven? ¿Cómo funciona el control de versiones de los paquetes y los archivos jar del paquete para las implementaciones de fase y producción? {#snapshot-version}

Consulte los siguientes escenarios para obtener más información sobre el control de versiones de los paquetes y los archivos jar de paquetes para las implementaciones de fase y producción:

1. Para implementaciones de desarrolladores, la rama Git `pom.xml` Los archivos deben contener `-SNAPSHOT` al final del `<version>` valor. Esto permite una implementación posterior en la que la versión no cambia para instalarse. En implementaciones de desarrolladores, no se agrega ni genera ninguna versión automática para la compilación de maven.

1. En la implementación de fase y producción, se genera una versión automática como se documenta [here](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/activating-maven-project.html?lang=en#managing-code).

1. Para las versiones personalizadas en las implementaciones de fase y producción, establezca una versión maven adecuada para 3 partes como `1.0.0`. Actualice la versión cada vez que tenga que realizar otra implementación en producción.

1. Cloud Manager añade automáticamente su versión a las compilaciones de Fase y Producción e incluso crea una rama Git. No se requiere ninguna configuración especial. Si se omite el paso 3 anterior, la implementación seguiría funcionando correctamente y se establecería una versión automáticamente.

1. No hay problemas, si deja la versión con `-SNAPSHOT` para compilaciones o implementaciones de fase y producción. Cloud Manager establece automáticamente un número de versión adecuado y crea una etiqueta para usted en Git. Se puede hacer referencia a esta etiqueta más adelante, si es necesario.

1. Si desea probar algún código experimental en el entorno de desarrollo, puede crear una nueva rama de Git y establecer la canalización para utilizar esa rama diferente. Esto resulta útil cuando las implementaciones comienzan a fallar y le gustaría probarlo con versiones anteriores del código para ver cuándo se interrumpió.

   El comando Git de abajo crea una rama remota denominada *testbranch1* contra una confirmación preexistente específica `485548e4fbafbc83b11c3cb12b035c9d26b6532b`.  Esta rama especial se puede usar en Cloud Manager sin afectar a otras ramas:

   `git push origin 485548e4fbafbc83b11c3cb12b035c9d26b6532b:refs/heads/testbranch1`

   Consulte la [Documentación de Git](https://git-scm.com/book/en/v2/Git-Internals-Git-References) para obtener más información.

   Si desea eliminar la rama de prueba más adelante, utilice el comando eliminar:

   `git push origin --delete testbranch1`

## La compilación de Maven falla en las implementaciones de Cloud Manager, pero se genera localmente sin errores. ¿Cómo se depura? {#maven-build-fail}

Consulte [Recurso de Git](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md) para obtener más información.

## ¿Qué hacer si la implementación de Cloud Manager falla en el paso de implementación en AEM entorno as a Cloud Service? {#cloud-manager-deployment-cloud-service}

El motivo más común para que las implementaciones fallen es que los permisos para la variable *sling-distribution-importer* usuario.
Consulte el ejemplo siguiente para comprender un problema, una causa y una solución:

**Problema**
Durante una implementación de Cloud Manager en entornos as a Cloud Service AEM, el paso de implementación falla y se observan errores como los que se muestran a continuación.

`[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.jackrabbit.vault.fs.io.Importer Error while committing changes. Retrying import from checkpoint at /. Retries 4/10`
`[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.sling.distribution.journal.impl.subscriber DistributionSubscriber Error processing queue item`
`org.apache.sling.distribution.common.DistributionException: Error processing distribution package`
`dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 162/infinite.`
`Caused by: org.apache.sling.api.resource.PersistenceException: Unable to commit changes to session.`
`Caused by: javax.jcr.AccessDeniedException: OakAccess0000: Access denied [EventAdminAsyncThread #7] org.apache.sling.distribution.journal.impl.publisher.DistributionPublisher [null] Error processing distribution package` `dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 344/infinite. Message: Error trying to extract package at path /etc/packages/com.myapp/myapp-base.ui.content-5.1.0-SNAPSHOT.`

**Causa**

El usuario sling-distribution-importer necesita permisos adicionales para las rutas de contenido definidas en el paquete ui.content.  Esto generalmente significa que necesitamos agregar permisos para /conf y /var.

**Solución**
La solución a esto es agregar una [Configuración de RepositoryInitializer OSGi](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=es) script a su paquete de implementación de aplicaciones para agregar ACL para el usuario sling-distribution-importer.
En el error de ejemplo anterior, el paquete myapp-base.ui.content-*.zip incluye contenido en `/conf` y `/var/workflow`. Para que la implementación no falle, necesitaríamos añadir permisos para sling-distribution-importer en esas rutas.
Este es un ejemplo [org.apache.sling.jcr.repository.RepositoryInitializer-DistributionService.config](https://github.com/cqsupport/cloud-manager/blob/main/org.apache.sling.jcr.repoinit.RepositoryInitializer-distribution.config) de una de estas configuraciones de OSGi que agrega permisos adicionales para el usuario sling-distribution-importer.  Esta configuración agrega permisos en /var.  Este archivo xml a continuación [1] debe añadirse al paquete de aplicación en `/apps/myapp/config` (donde myapp es la carpeta donde se almacena el código de la aplicación).
org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config

1. Si la variable *sling-distribution-importer* no es la causa, entonces la implementación podría estar fallando debido a una configuración OSGi incorrecta que rompe un servicio predeterminado. Compruebe los registros durante la implementación para ver si hay algún error obvio.

1. Es posible que la implementación falle debido a configuraciones incorrectas de Dispatcher o Apache. Asegúrese de probar las configuraciones de Apache y Dispatcher localmente mediante la imagen Docker incluida en el SDK. Consulte [Dispatcher en la nube](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#content-delivery) sobre cómo configurar el contenedor de Docker de Dispatcher para facilitar las pruebas locales.

1. Es posible que la implementación falle debido a algún otro error durante la replicación de los paquetes de contenido (distribución de sling) de las instancias de autor a publicación.

   Consulte los pasos a continuación para simular esto en una configuración local:

   * Instalación de una instancia de Autor y Publicación (con los últimos AEM SDK jars)
   * Inicie sesión en la instancia de autor.
   * Vaya a **Herramientas** -> **Implementación** -> **Distribución**
   * Distribuya los paquetes de contenido que forman parte de la base de código y vea si la cola se bloquea con un error

## No se puede establecer una variable a través de las variables de canalización establecidas de aio cloud manager. ¿Cómo depurar estos problemas? {#set-variable}

Si está recibiendo un `403` al intentar listar o establecer variables de canalización a través de comandos similares a los que se muestran a continuación, debe agregarse como *Administrador de implementación* Función del producto de Cloud Manager en el Admin Console.\
Consulte [Permisos de API](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md) para obtener más información.

Comandos y errores relacionados:

`$ aio cloudmanager:list-pipeline-variables 222`

*Error*: `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1`

*Error*: `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1`

`setting variables... !`

*Error*: `Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)`
