---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 6e82bbcc1b83fa9216831f6f746665507a46eec7
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 23%

---

# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 14029 {#release-14029}

A continuación se resumen las mejoras continuas para la 14029 de la versión de mantenimiento, que se publicó el 25 de octubre de 2023. Esta versión de mantenimiento es una actualización de la versión de mantenimiento 13804 anterior.

La activación de funciones 2023.11.0 proporcionará el conjunto completo de funciones para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información.

### Mejoras {#enhancements-14029}

* ASSETS-28551: mejorar la escalabilidad de la interfaz de usuario de Mi vínculo compartido
* ASSETS-28566: Añadir dam:metadataForm: índice Lucene
* ASSETS-29281: actualizar RAPI para enviar eventos de descarga de la versión 2

### Problemas corregidos {#fixed-issues-14029}

* ASSETS-25199: el componente principal de la imagen no muestra los cultivos inteligentes adecuados
* ASSETS-26142: unified-shell.js customEnvLabel no se establece ni se vuelve a intentar si la solicitud de detección falla o se interrumpe
* ASSETS-26416: el predicado de fecha relativa siempre se define como &quot;hace 1 día(s)&quot; en el formulario de búsqueda
* ASSETS-27321: borrar la caché de grupo en los cambios de miembro del equipo
* ASSETS-27591: Corrija la dependencia en el org.json antiguo
* ASSETS-28439: Lista de bloqueados de etiquetas inteligentes NPE cuando la lista de bloqueados global no está configurada
* ASSETS-28612: corrección de BlockedTagResolver en &quot;repository-api&quot;
* ASSETS-28634: el campo Omnisearch de las existencias de Adobe no obtiene datos de recursos añadidos automáticamente
* ASSETS-28727: la lista de configuración del perfil de procesamiento no muestra los valores de altura y anchura personalizados especificados
* AEM ASSETS-29056: añadir representaciones de transcodificación perfil de procesamiento estándar
* ASSETS-29105: el proveedor de restricciones no se encuentra en SecurityProviderRegistration requiredServicePids en el modelo de características de RDE
* ASSETS-29106: la vista de las existencias de Adobe AEM genera un error en el shell unificado habilitado para la creación de informes de
* ASSETS-29115: Quitar la propiedad de configuración para las rutas del proveedor de restricción
* ASSETS-29208: Errores en la carga de recursos causados por solicitudes enviadas a un pod de creación antes de que se registre el servicio CompleteUploadAssetServlet
* ASSETS-29297: Problema al crear la opción de filtro Guardar búsqueda con desprotegido
* ASSETS-29363: El perfil de metadatos no aplica los valores predeterminados para IPTC
* ASSETS-29404: el informe de vínculos compartidos alcanza el límite de consultas
* ASSETS-29431: quitar indicadores de funciones antiguas
* ASSETS-29443: el Héroe de Unified Shell permanece visible y se puede hacer clic cuando el modo de encabezado de Granite Shell cambia a &quot;selección&quot;
* ASSETS-29476: la llamada a la API scene7DAMService.getS7FileReference(asset) no devuelve el valor esperado.
* ASSETS-29515: Assets/Nodes con &quot;jcr:lastModifiedBy&quot;: &quot;workflow-process-service&quot; se muestra como &quot;usuario externo&quot; en la vista de lista
* ASSETS-29579: Los usuarios no administradores no pueden crear un conjunto de imágenes
* ASSETS-29631: Utilice dam:roles para una entrega/búsqueda segura
* AEM ASSETS-29689: dc:roles (y la nueva propiedad dam:roles) debe filtrarse de lado de la
* ASSETS-29738: la restricción de carga de recursos falla con NullPointerException
* ASSETS-29779: los recursos pequeños no se pueden procesar en webp porque no están en el almacenamiento de blob
* ASSETS-29892: Se produce un error en la exportación de metadatos en una carpeta con un gran número de recursos
* ASSETS-29996: &quot;Usuario externo&quot; como modificador al cargar recursos de forma intermitente solo en instancias de PROD
* ASSETS-30167: HTML para adobe_dam: se producen restricciones después de cargar un recurso
* ASSETS-30276: Compartir vínculo de la interfaz de usuario: no se puede compartir desde los detalles del recurso
* ASSETS-30434: el evento de procesamiento de recursos completado no se envía a la canalización
* ASSETS-30519: Agregar RAPI a REDMetricsServletFilter
* CQ-4354413: QueryBuilder: las consultas con corchetes se traducen incorrectamente a xpath
* CQ-4354834: no se puede agregar un comentario en la tarea de bandeja de entrada
* CQ-4354836: no se puede iniciar el flujo de trabajo o crear una tarea desde la consola Proyectos
* CQ-4354867: La referencia ToggleCondition hace referencia a un campo inexistente en InstanceActionServlet
* AEM CQ-4354895: Kit de traducción de: 12 de octubre
* GRANITE-45560: representación de esquema común en la envolvente de evento
* GRANITE-47267: Actualización a Apache Felix Http Jetty 4.2.18
* GRANITE-47599: Las importaciones de contenido fallan desde 13323 actualización (JCRVLT-721)
* GRANITE-47873: Actualización a Apache Felix Webconsole 4.9.6

### Problemas conocidos {#known-issues-14029}

Ninguna.

### Tecnologías integradas {#embedded-tech-14029}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM OAK | 1,56-T20230927085643-189caed | [API Oak 1.56.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.56.0/index.html) |
| API AEM SLING | Versión 2.27.2 | [API de Apache Sling 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versión 1.4.20-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | Versión 2.23.4 | [Componentes principales de WCM de AEM](https://github.com/adobe/aem-core-wcm-components) |
