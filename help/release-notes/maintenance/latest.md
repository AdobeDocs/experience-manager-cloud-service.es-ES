---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 13124956fcce105ad42767f67b700284c8250012
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 34%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 21644 {#21644}

A continuación se resumen las mejoras continuas para la versión de mantenimiento 21644, que se publicó el miércoles, 22 de julio de 2025. La versión de mantenimiento anterior fue la 21570.

La activación de funcionalidades 2025.7.0 proporciona el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-21644}

* ASSETS-39377: Mejore la administración de los 429 desde el almacenamiento remoto en el importador por lotes de Assets.
* ASSETS-46026: profundidad máxima configurable para el exportador de metadatos.
* ASSETS-49172: los recursos de plantilla de Dynamic Media deben heredar los metadatos de la carpeta.
* ASSETS-50209: Compatibilidad con subcadenas en plantillas DM.
* ASSETS-52326: página de configuración de AEM Assets para establecer las preferencias de visualización del título para Assets.
* ASSETS-52805: Añada la salida CSV/compatibilidad de descarga para el trabajo Operación por lotes.
* ASSETS-52873: agregue una nueva configuración en las propiedades de la carpeta para deshabilitar el procesamiento de IA para esa carpeta.
* ASSETS-53535: rendimiento mejorado de carga de vídeo de YouTube.
* ASSETS-53612: Control de la búsqueda híbrida en Assets Omnisearch.
* GRANITE-60183: actualice la dependencia commons-fileupload a 1.6.0.
* GRANITE-60287: Actualice QS a Jackrabbit 2.22.1.
* SITES-30452: API de contenido con ASO - Sugerencias de título y descripción.
* SITES-31677: el espacio de trabajo personalizado admite la exportación de fragmentos de contenido de AEM a destino.
* SKYOPS-112741: elimine el paquete `com.adobe.granite.product.support` de AEM-CS SDK.

### Problemas solucionados {#fixed-issues-21644}

* ASSETS-12882: Problemas de alineación de la interfaz de usuario después de abrir los ajustes preestablecidos del visor.
* ASSETS-48958: Problema con la sincronización de recursos que cambia el estado de publicación en el AEM local de Sites.
* ASSETS-50856: `dam:processingAttempts` no se restablece en completeUpload.
* ASSETS-51604: Faltan datos del tipo &quot;Compartido con&quot; en el CSV del informe de uso compartido de vínculos.
* ASSETS-51783: Volver a la configuración de DM en `/conf/global` si no se encuentra ninguna configuración mediante la consulta de búsqueda.
* ASSETS-51857: Los elementos de la tabla de recursos no se pueden reordenar.
* ASSETS-52169: Nueva representación automática de BAT incluida erróneamente en las descargas de recursos.
* ASSETS-52229: Faltan notificaciones en la bandeja de entrada para los informes de recursos en AEM as a Cloud Service.
* ASSETS-52399: El error de versión en com.day.cq.dam.api puede romper el código del cliente.
* ASSETS-52780: el recurso se puede marcar para la vista previa incluso sin activarlo o desactivarlo.
* ASSETS-52866: Los vídeos DM migrados permanecen en estado de procesamiento en la carpeta con la sincronización de DM deshabilitada.
* ASSETS-53237: la lista desplegable Perfil de color está en blanco en el editor de ajustes preestablecidos de imagen.
* ASSETS-53240: Informe de recursos: Uso del disco falla al obtener el tamaño de representación de recursos de Dynamic Media.
* ASSETS-53446: errores intermitentes de actualización del token de autenticación de YouTube debido a NPE.
* ASSETS-53827: Los bloques de validación de ACL guardan conjuntos de medios mixtos.
* ASSETS-5403: Los clientlibs de Dynamic Media utilizados en la instancia de publicación deben tener `allowProxy=true`.
* ASSETS-54261: la importación de metadatos filtra conexiones y se bloquea si el archivo no se puede descargar.
* CQ-4359863: búsqueda de etiquetas interrumpida para palabras clave desordenadas en el editor de fragmentos de contenido/editor de recursos.
* CQ-4359958: Hacer compatible openapi-support con AEM 6.5.22.0 y versiones posteriores.
* CQ-4360256: incluya la ruta de contexto del servlet en la ruta de solicitud para las solicitudes HTTP administradas mediante el contexto del servlet `/adobe`.
* CQ-4360317: método Add para establecer el encabezado de fecha de ocaso al crear respuestas.
* GRANITE-60311: Quickstart de AEM SDK: NPE en &quot;Impresora de configuración del instalador OSGi&quot;.
* GS-15285: los usuarios se muestran como desactivados.

### Problemas conocidos {#known-issues-21644}

Ninguna.

### Características y API obsoletas {#deprecated-21644}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-21644}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 4 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-21644}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.80.0 | [API Oak 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Servidor HTTP Apache | 2.4.63 | [Apache Httpd 2.4.63](https://github.com/apache/httpd/blob/2.4.63/CHANGES) |
| Componentes principales de AEM | 2.29.0 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
