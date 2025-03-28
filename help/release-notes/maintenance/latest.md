---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 23ebeb259e5955bd51431844fd67db9b363034ea
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 100%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 19823 {#19823}

A continuación, se resumen las mejoras continuas para la versión de mantenimiento 19823, publicada el 4 de marzo de 2025. La versión de mantenimiento anterior fue la 19687.

La activación de funcionalidades 2025.3.0 proporciona el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-19823}

* ASSETS-46491: cambio de estado del controlador de eventos OSGI para el procesamiento de recursos.
* ASSETS-45613: envío de eventos de cancelación de publicación cuando se eliminan o mueven los recursos.
* ASSETS-45131: compatibilidad con propiedades de etiquetas personalizadas en el centro de contenido.

### Problemas solucionados {#fixed-issues-19823}

* ASSETS-20433: problemas de ingesta de Dynamic Media con los PDF protegidos por contraseña.
* ASSETS-24675: las opciones de procesamiento de imágenes no se muestran para el perfil de imagen solo de muestra.
* ASSETS-41257: la comparación de versiones de recursos procesa los recursos con una relación de aspecto incorrecta. Las versiones de los recursos se muestran en el orden incorrecto en la línea de tiempo.
* ASSETS-44894: es posible que no se pueda hacer clic en los marcadores de la vista de recursos.
* ASSETS-45015: la anchura y altura del recorte inteligente se establecen en cero si no se encuentra el controlador del recurso de recorte inteligente.
* ASSETS-45192: reduzca la frecuencia de las solicitudes de pulso.
* ASSETS-45724: asegúrese de que se vuelva a intentar la carga de DM si no se ha asignado el trabajo de carga.
* ASSETS-46425: problemas de búsqueda de integración de Adobe Stock.
* ASSETS-27400: es posible que el generador de previsualización de carpetas intente abrir la original.
* CQ-4358722: gestione diferentes códigos de configuración regional en Java 11 y Java 17.
* SITES-29369: eventos publicados o sin publicar de página activados tras la activación o desactivación de recursos.
* SITES-24074: corrija la accesibilidad del teclado en el contenedor unificado.
* SITES-28058: el título de la carpeta de recursos no se ha transferido a Live Copy.

### Problemas conocidos {#known-issues-19823}

Ninguna.

### Características y API obsoletas {#deprecated-19823}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-19823}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda seis vulnerabilidades identificadas, lo que refuerza nuestro compromiso de una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-19823}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.76.0 | [API Oak 1.76.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.76.0/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.27.0 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
