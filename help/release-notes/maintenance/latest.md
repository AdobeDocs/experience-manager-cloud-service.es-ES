---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: e771913562b3770e5a504432d40c770804aadc4b
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 34%

---

# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 13804 {#release-13804}

A continuación se resumen las mejoras continuas para la 13804 de la versión de mantenimiento, que se publicó el 10 de octubre de 2023. Esta versión de mantenimiento es una actualización de la versión de mantenimiento 13665 anterior.

La activación de funciones 2023.10.0 proporcionará el conjunto completo de funciones para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información.

### Mejoras {#enhancements-13804}

* GRANITE-47238: Mantenimiento del registro de auditoría: depure los cronjob para utilizar la configuración del cliente.
* GRANITE-47123: Publish (Sling): mejore el tiempo de inicio inicializando la caché de la ruta de vanidad de forma asincrónica de forma predeterminada.
* GRANITE-46618: Publish (Replication): mejore la velocidad de inicio de la publicación mediante el agrupamiento de mensajes de estado de replicación.
* GRANITE-47136: Indexación (Descarga): mejore la velocidad de descarga del nuevo descargador de índices paralelo (desactivando la validación de suma de comprobación).
* GRANITE-47211: Publish (Infra): mejore la desvinculación de las implementaciones de nivel de Publish (almacenando y recuperando el nombre de revisión del almacén de segmentos).
* GRANITE-47267: Actualización a Apache Felix Http Jetty 4.2.18 (incluye corrección de errores para la administración de parámetros de solicitud ([FELIX-6625](https://issues.apache.org/jira/browse/FELIX-6625)) con mejoras de rendimiento para desarrollos locales y RDE).
* GRANITE-47247: Actualización a Sling Servlets Resolver 2.9.14 con mejoras de rendimiento en la resolución de servlets.

### Problemas corregidos {#fixed-issues-13804}

* GRANITE-47376: Author (Infra): Corrección de errores de DiscoveryTopologyUndefined después de reiniciar con desplazamiento.
* AEM AEM CQ-4353436: Consola web de (Sling): configuraciones vacías en los validadores de ServiceUserMapperImpl (principal/usuario) que rompen la instancia de la ([SLING-11912](https://issues.apache.org/jira/browse/SLING-11912)).
* SKYOPS-63925: Trabajo de transformación: evitar errores de TransformJob con JDK 11 - ZipException: errores de encabezado CEN no válidos (con el indicador JVM disableZip64ExtraFieldValidation).
* SKYOPS-63361: Trabajo de transformación (registro) Registro mejorado con trabajos de transformación (subpaso CUSTOMER_EXTRACT).
* SKYOPS-64103: herramienta FACT (registro): reduce o trunca los mensajes de error y advertencia de la compilación de Clientlib.
* SKYOPS-65109: herramienta FACT (gestión de errores): los paquetes de contenido con dependencias sin resolver dan como resultado un error informado correctamente.
* SKYOPS-65368: herramienta FACT (Gestión de errores): la herramienta se ejecuta en un ciclo de inclusión interminable y, finalmente, se agota el tiempo de espera en incrustaciones circulares de Clientlibs.
* SKYOPS-64031: RDE: ComponentCacheImpl puede entrar en un estado incoherente debido al registro duplicado de ResourceResolverFactory ([SLING-12019](https://issues.apache.org/jira/browse/SLING-12019)).
* ASSETS-29105: RDE: el proveedor de restricción no se encuentra en SecurityProviderRegistration requiredServicePids en el modelo de funciones RDE.
* GRANITE-44674: CoralUI: la funcionalidad de campo obligatorio del selector de fecha es incorrecta.

### Problemas conocidos {#known-issues-13804}

* CQ-4354836: no se puede iniciar el flujo de trabajo o crear una tarea desde la consola Proyectos.
* CQ-4354834 : los usuarios no pueden agregar comentarios en una tarea de la bandeja de entrada.

### Tecnologías integradas {#embedded-tech-13804}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM OAK | 1,56-T20230927085643-189caed | [API Oak 1.56.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.56.0/index.html) |
| API AEM SLING | Versión 2.27.2 | [API de Apache Sling 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versión 1.4.20-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | Versión 2.23.4 | [Componentes principales de WCM de AEM](https://github.com/adobe/aem-core-wcm-components) |
