---
title: Preguntas frecuentes sobre Cloud Manager
description: Encuentre respuestas a las preguntas más frecuentes sobre Cloud Manager en AEM as a Cloud Service.
exl-id: eed148a3-4a40-4dce-bc72-c7210e8fd550
source-git-commit: 65632de3fbf81ef44d30994365e6365a6148b836
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Preguntas frecuentes sobre Cloud Manager {#cloud-manager-faqs}

Este documento proporciona respuestas a las preguntas más frecuentes sobre Cloud Manager en AEM as a Cloud Service.

## ¿Es posible utilizar Java 11 con compilaciones de Cloud Manager? {#java-11-cloud-manager}

Sí. Deberá agregar la variable `maven-toolchains-plugin` con la configuración adecuada para Java 11.

El proceso está documentado [here](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/using-the-wizard.md#getting-started).

Por ejemplo, consulte la [código de proyecto de ejemplo de proyecto wknd](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75).

## Mi compilación falla con un error sobre maven-scr-plugin después de cambiar de Java 8 a Java 11. ¿Qué puedo hacer? {#build-fails-maven-scr-plugin}

Es posible que la compilación de AEM Cloud Manager falle al intentar cambiar la compilación de Java 8 a 11. Si encuentra el siguiente error, debe eliminar `maven-scr-plugin` y convertir todas las anotaciones OSGi en anotaciones OSGi R6.

```text
[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]
```

Para obtener instrucciones sobre cómo eliminar este complemento, consulte [aquí.](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/)

## Mi compilación falla con un error sobre RequireJavaVersion después de cambiar de Java 8 a Java 11. ¿Qué puedo hacer? {#build-fails-requirejavaversion}

Para las compilaciones de Cloud Manager, la variable `maven-enforcer-plugin` puede fallar con este error.

```text
"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion".
```

Este es un problema conocido debido a que Cloud Manager utiliza una versión diferente de Java para ejecutar el comando maven en comparación con el código de compilación. Simplemente omita `requireJavaVersion` de su `maven-enforcer-plugin` configuraciones.

## La comprobación de calidad del código falló y nuestra implementación se atascó. ¿Hay alguna manera de evitar este cheque? {#deployment-stuck}

Sí. Todos los errores de comprobación de calidad del código, excepto la clasificación de seguridad, son métricas no críticas, por lo que se pueden evitar ampliando los elementos en la interfaz de usuario de los resultados.

Consulte el documento [Prueba de calidad de código](/help/implementing/cloud-manager/code-quality-testing.md) para obtener más información.

## ¿Puedo utilizar SNAPSHOT para la versión del proyecto Maven? {#use-snapshot}

Sí. Para implementaciones de desarrolladores, la rama de Git `pom.xml` Los archivos deben contener `-SNAPSHOT` al final del `<version>` valor.

Esto permite que la implementación posterior se siga instalando cuando la versión no ha cambiado. En implementaciones de desarrolladores, no se agrega ni genera ninguna versión automática para la compilación de maven.

También puede establecer la versión en `-SNAPSHOT` para compilaciones o implementaciones de fase y producción. Cloud Manager establece automáticamente un número de versión adecuado y crea una etiqueta para usted en Git. Se puede hacer referencia a esta etiqueta más adelante, si es necesario.

Para obtener más información sobre la gestión de versiones, consulte [documentado aquí.](/help/implementing/cloud-manager/managing-code/project-version-handling.md)

## ¿Cómo funcionan las versiones de paquetes y paquetes para las implementaciones de fase y producción? {#snapshot-version}

En las implementaciones de fase y producción, se genera una versión automática como [documentado aquí.](/help/implementing/cloud-manager/managing-code/project-version-handling.md)

Para las versiones personalizadas en las implementaciones de fase y producción, establezca una versión maven adecuada en tres partes como `1.0.0`. Actualice la versión cada vez que implemente en producción.

Cloud Manager añade automáticamente su versión a las compilaciones de fase y producción y crea una rama de Git. No se requiere ninguna configuración especial. Si no establece una versión maven como se describió anteriormente, la implementación se realizará correctamente y se establecerá una versión automáticamente.

## Mi compilación de maven falla en las implementaciones de Cloud Manager, pero se genera localmente sin errores. ¿Qué está mal? {#maven-build-fail}

Consulte [este recurso git](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md) para obtener más información.

## ¿Qué puedo hacer si una implementación de Cloud Manager falla en el paso de implementación en AEM as a Cloud Service? {#cloud-manager-deployment-cloud-service}

El motivo más común para que una implementación falle es que no hay permisos suficientes para `sling-distribution-importer` usuario. En este caso, el paso de implementación falla durante una implementación de Cloud Manager y se generan errores como los siguientes.

```text
[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.jackrabbit.vault.fs.io.Importer Error while committing changes. Retrying import from checkpoint at /. Retries 4/10
[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.sling.distribution.journal.impl.subscriber DistributionSubscriber Error processing queue item
org.apache.sling.distribution.common.DistributionException: Error processing distribution package
dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 162/infinite.
Caused by: org.apache.sling.api.resource.PersistenceException: Unable to commit changes to session.
Caused by: javax.jcr.AccessDeniedException: OakAccess0000: Access denied [EventAdminAsyncThread #7] org.apache.sling.distribution.journal.impl.publisher.DistributionPublisher [null] Error processing distribution package` `dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 344/infinite. Message: Error trying to extract package at path /etc/packages/com.myapp/myapp-base.ui.content-5.1.0-SNAPSHOT.
```

La variable `sling-distribution-importer` el usuario necesita permisos adicionales para las rutas de contenido definidas en la variable `ui.content package`.  Esto suele significar que debe agregar permisos para ambos `/conf` y `/var`.

La solución es agregar un [Configuración de RepositoryInitializer OSGi](/help/implementing/deploying/overview.md#repoint) script a su paquete de implementación de aplicaciones para agregar ACL para el `sling-distribution-importer` usuario.

En el ejemplo de error anterior, el paquete `myapp-base.ui.content-*.zip` incluye contenido en `/conf` y `/var/workflow`. Para que la implementación se realice correctamente, los permisos de la variable `sling-distribution-importer` en esas rutas es necesario.

Este es un ejemplo de [`org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config`](https://github.com/cqsupport/cloud-manager/blob/main/org.apache.sling.jcr.repoinit.RepositoryInitializer-distribution.config) Configuración de OSGi que agrega permisos adicionales para `sling-distribution-importer` usuario.  La configuración agrega permisos en `/var`.  Esta configuración debe añadirse al paquete de aplicaciones en `/apps/myapp/config` (donde myapp es la carpeta donde se almacena el código de la aplicación).

## Mi implementación de Cloud Manager falla en el paso de implementación en AEM as a Cloud Service y ya he agregado una configuración OSGi de RepositoryInitializer. ¿Qué más puedo hacer? {#build-failures}

If [adición de una configuración OSGi de RepositoryInitializer](#cloud-manager-deployment-cloud-service) no resolvió el error, puede deberse a uno de estos problemas adicionales.

* Es posible que la implementación esté fallando debido a una configuración OSGi incorrecta que rompe un servicio predeterminado.
   * Compruebe los registros durante la implementación para ver si hay algún error obvio.

* Es posible que la implementación falle debido a configuraciones incorrectas de Dispatcher o Apache.
   * Asegúrese de probar las configuraciones de Apache y Dispatcher localmente mediante la imagen Docker incluida en el SDK.
   * Consulte [Dispatcher en la nube](/help/implementing/dispatcher/disp-overview.md#content-delivery) sobre cómo configurar el contenedor de Docker de Dispatcher para facilitar las pruebas locales.

* Es posible que la implementación falle debido a algún otro error durante la replicación de los paquetes de contenido (distribución Sling) de las instancias de autor a publicación.
   * Siga estos pasos para simular el problema en una configuración local.
      1. Instale una instancia de autor y publicación localmente mediante los últimos AEM SDK jars.
      1. Inicie sesión en la instancia de autor.
      1. Vaya a **Herramientas** -> **Implementación** -> **Distribución**.
      1. Distribuya los paquetes de contenido que forman parte de la base de código y vea si la cola se bloquea con un error.

## No puedo establecer una variable mediante un comando aio. ¿Qué puedo hacer? {#set-variable}

Puede recibir una `403` error como el siguiente al intentar enumerar o establecer variables de canalización mediante `aio` comandos.

```shell
$ aio cloudmanager:list-pipeline-variables 222

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1

setting variables... !

Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)
```

En este caso, el usuario que ejecuta estos comandos debe agregarse al **Administrador de implementación** en el Admin Console.

Consulte [Permisos de API](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md) para obtener más información.
