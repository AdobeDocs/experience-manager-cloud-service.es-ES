---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 3686697c85273ccc13e80b8d7f4ad1ff3c79845d
workflow-type: ht
source-wordcount: '632'
ht-degree: 100%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 21706 {#21706}

A continuación se resumen las mejoras continuas para la versión de mantenimiento 21706, que se publicó el 24 de julio de 2025. La versión de mantenimiento anterior fue la 21570.

>[!NOTE]
>
>La versión 21644 pasó a ser privada y se ha reemplazado por la versión 21706.

La activación de funcionalidades 2025.7.0 proporciona el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-21706}

* ASSETS-39377: mejorar la gestión de 429s desde el almacenamiento remoto en el importador masivo de recursos.
* ASSETS-46026: profundidad máxima configurable para el exportador de metadatos.
* ASSETS-49172: los recursos de plantilla de Dynamic Media deben heredar los metadatos de la carpeta.
* ASSETS-50209: compatibilidad con subcadenas en plantillas DM.
* ASSETS-52326: página de configuración de AEM Assets para establecer las preferencias de visualización del título para Assets.
* ASSETS-52805: añadir soporte de salida/descarga CSV para el trabajo de operación masiva.
* ASSETS-52873: añadir una nueva configuración en las propiedades de la carpeta para deshabilitar el procesamiento de IA para esa carpeta.
* ASSETS-53535: rendimiento mejorado de carga de vídeo de YouTube.
* ASSETS-53612:control de la búsqueda híbrida en Assets Omnisearch.
* GRANITE-60183: actualizar la dependencia de commons-filepload io a 1.6.0.
* GRANITE-60287: actualizar QS a Jackrabbit 2.22.1.
* SITES-30452: API de contenido con ASO - Sugerencias de título y descripción.
* SITES-31677: el espacio de trabajo personalizado admite la exportación de fragmentos de contenido de AEM a destino.
* SKYOPS-112741: quitar el paquete `com.adobe.granite.product.support` del SDK de AEM-CS.

### Problemas solucionados {#fixed-issues-21706}

* ASSETS-12882: problemas de alineación de la interfaz de usuario después de abrir los ajustes preestablecidos del visor.
* ASSETS-48958: problema con la sincronización de recursos que cambia el estado Publicado en el AEM local de Sites.
* ASSETS-50856: `dam:processingAttempts` no se restablece en completeUpload.
* ASSETS-51604: faltan datos del tipo &quot;Compartido con&quot; en el CSV del informe de uso compartido de vínculos.
* ASSETS-51783: volver a DM en `/conf/global` si no se encuentra ninguna configuración mediante la consulta de búsqueda.
* ASSETS-51857: los elementos de la tabla de recursos no se pueden reordenar.
* ASSETS-52169: nueva representación de la máquina BAT incluida erróneamente en las descargas de recursos.
* ASSETS-52229: faltan notificaciones en la bandeja de entrada para los informes de recursos en AEM as a Cloud Service.
* ASSETS-52399: el error de versión en com.day.cq.dam.api puede romper el código del cliente.
* ASSETS-52780: el recurso se puede marcar para la vista previa incluso sin el conmutador activado.
* ASSETS-52866: los vídeos de DM migrados permanecen en estado de procesamiento en la carpeta con la sincronización de DM deshabilitada.
* ASSETS-53237: la lista desplegable Perfil de color está en blanco en el editor de ajustes preestablecidos de imagen.
* ASSETS-53240: informe de recursos: el uso del disco falla al obtener el tamaño de representación de recursos de Dynamic Media.
* ASSETS-53446: errores intermitentes de actualización del token de autenticación de YouTube debido a NPE.
* ASSETS-53827: los bloques de validación de ACL guardan conjuntos de medios mixtos.
* ASSETS-5403: Los clientlibs de Dynamic Media utilizados en la instancia de publicación deben tener `allowProxy=true`.
* ASSETS-54261: la importación de metadatos pierde conexiones y se bloquea si el archivo no se puede descargar.
* CQ-4359863: búsqueda de etiquetas interrumpida para palabras clave desordenadas en el editor de fragmentos de contenido/editor de recursos.
* CQ-4359958: hacer compatible openapi-support con AEM 6.5.22.0 y versiones posteriores.
* CQ-4360256: incluir la ruta de contexto del servlet en la ruta de solicitud para las solicitudes HTTP gestionadas mediante el contexto del servlet `/adobe`.
* CQ-4360317: método de adición para establecer el encabezado de fecha Sunset al crear respuestas.
* GRANITE-60311: inicio rápido del SDK de AEM: NPE en &quot;Impresora de configuración del programa de instalación OSGi&quot;.
* GS-15285: los usuarios se muestran como desactivados.

### Problemas conocidos {#known-issues-21706}

Ninguna.

### Características y API obsoletas {#deprecated-21706}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-21706}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 4 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-21706}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.80.0 | [API Oak 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80/index.html?lang=es) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.63 | [Apache Httpd 2.4.63](https://github.com/apache/httpd/blob/2.4.63/CHANGES) |
| Componentes principales de AEM | 2.29.0 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
