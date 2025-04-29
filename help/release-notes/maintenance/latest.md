---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 437125b6819edf70539ebacb4a8beddb755fcb7a
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 39%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 20626 {#20626}

A continuación, se resumen las mejoras continuas para la versión de mantenimiento 20626, que se publicó el miércoles, 29 de abril de 2025. La versión de mantenimiento anterior fue la 20476.

La activación de funcionalidades 2025.5.0 proporciona el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-20626}

* ASSETS-46413, ASSETS-46580: Se ha agregado un nuevo estado de revisión &quot;Vista previa&quot;.
* ASSETS-49542: Ampliación de los idiomas admitidos para la transcripción y traducción de vídeo y audio.
* ASSETS-48264: Ampliación del soporte de calidad PNG para representaciones.

### Problemas solucionados {#fixed-issues-20626}

* ASSETS-50387: Corrija la miniatura predeterminada del fragmento de contenido para su uso en GenStudio.
* ASSETS-49006: muestra las propiedades de vídeo cuando el usuario no tiene permisos de escritura.
* ASSETS-46757, ASSETS-46997: Mejore la accesibilidad en el editor de recortes inteligente.
* ASSETS-48018: mejore el seguimiento de referencia de recursos en el informe de publicación de Assets.
* ASSETS-35846: mejorar la coherencia del acceso entre el nivel de creación y el de entrega.
* ASSETS-48171: Mejore la coherencia de la plantilla de Dynamic Media con lienzo.
* ASSETS-49813: mejore la notificación de caducidad.
* ASSETS-47768, ASSETS-49825, ASSETS-49008, ASSETS-48287: Mejore la administración y la visibilidad de las operaciones por lotes.
* ASSETS-50003, ASSETS-50004: mejore la nomenclatura y el control sobre las representaciones incluidas en una descarga de recursos.
* ASSETS-47939: Mejore la organización de las respuestas para Content Hub.
* ASSETS-46738: mejore el rendimiento para colecciones muy grandes.
* ASSETS-50121: Mejore la fiabilidad de los eventos publicados de recursos.
* ASSETS-48490: Mejore la resistencia del procesamiento automatizado durante la ingesta de imágenes.
* ASSETS-28106, ASSETS-49404: Mejore la solidez de la búsqueda de texto completo.
* ASSETS-50006, ASSETS-50423: Mejore el rendimiento de búsqueda y recorrido dentro de una carpeta grande.
* ASSETS-46021: Mejore la visualización de vídeo para Safari y los navegadores móviles.
* ASSETS-49002: Mejore el control de la edición de plantillas de Dynamic Media.
* ASSETS-48376: Varias mejoras en la IU de Content Hub.
* ASSETS-48504, ASSETS-49378: Varias mejoras en el comportamiento de la interfaz de usuario.
* ASSETS-49540: Saque Asset Relations OpenAPI de la fase experimental.
* ASSETS-40284: Actualice la documentación sobre la integración de Adobe Stock.
* ASSETS-49739: Trabaje para integrar Figma desde el Selector de recursos.

#### Guías de AEM {#guides}

* GUIDES-21734: No se pueden generar nuevos ID para elementos cuando estos se añaden mediante fragmentos o se crean mediante plantillas, incluso cuando la opción de ID de generación automática está activada en XMLEditorConfig.
* GUIDES-25969: Si falta el atributo `scope=external` en los vínculos externos de un tema DITA, la publicación de HTML5 falla sin indicar los archivos en los que falta este atributo en los registros de errores, especialmente cuando el microservicio está habilitado.
* GUIDES-27288: no se pueden pasar las propiedades de metadatos para asignar páginas de aterrizaje generadas con la nueva publicación de AEM Sites.

Para obtener más información sobre las funciones nuevas y mejoradas y los problemas corregidos en la versión, consulte la [hoja de ruta de la versión de Experience Manager Guides](https://experienceleague.adobe.com/es/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemas conocidos {#known-issues-20626}

Ninguna.

### Características y API obsoletas {#deprecated-20626}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-20626}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 11 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-20626}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.78.0 | [API Oak 1.78.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.78.0/index.html?lang=es) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.29.0 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
