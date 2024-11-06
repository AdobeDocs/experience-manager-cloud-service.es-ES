---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 90e1ca38bd517215a631573987462a716bfed160
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 32%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 18459 {#18459}

A continuación se resumen las mejoras continuas de la versión de mantenimiento 18459, que se publicó el miércoles, 05 de noviembre de 2024. La versión de mantenimiento anterior fue la 18311.

La activación de funcionalidades 2024.11.0 proporcionará el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-18459}

* CQ-4357471: Añada compatibilidad con la traducción de diccionarios i18n en AEMaaCS.
* SITES-23591: Fragmentos de contenido: Actualización de fragmentos de contenido para admitir UUID.
* SITES-25440: Fragmentos de contenido: la API de búsqueda de CFM para mostrar el estado de replicación.
* SITES-24369: Fragmentos de contenido: mejoras en la documentación de OpenAPI.
* SITES-25478: Fragmentos de contenido: Agregue compatibilidad back-end para referencias de recursos externos.
* SITES-26119: Fragmentos de contenido: Agregue compatibilidad con referencias de recursos externos en el tipo de referencia.
* SITES-21199: Edge Delivery con editor universal: agregue compatibilidad con las plantillas creadas a partir de páginas.
* SITES-20311: Edge Delivery con editor universal: agregue compatibilidad para importar CSV en hojas de cálculo.
* SITES-24821: Edge Delivery con el editor universal: convierta aem.page/aem.live en el predeterminado para integrar con Edge Delivery.

### Problemas solucionados {#fixed-issues-18459}

* CQ-4358730: CQPagePreviewGenerator falla cuando hay más de 10 claves por traducir.
* FORMS-14978: Habilitando la carga de página para un formulario basado en componentes principales para el editor de temáticas.
* FORMS-16596: Problema de accesibilidad: Botones desactivados no reconocidos por el Reader de pantalla.
* SITES-10575: MSM: Blueprint Bloomfilter Loader intenta cargar >100 000 filas.
* SITES-20755: Fragmentos de contenido: la referencia de recurso con actualización UUID no muestra la miniatura.
* SITES-26253: Fragmentos de contenido: migración UUID: cambie el tema del trabajo de Sling para que sea genérico.
* SITES-21338: Fragmentos de contenido: el extremo referencedBy no devuelve la referencia de página correcta.
* SITES-24421: Fragmentos de contenido: Editar extremo CF no funciona para CF recuperado a través de GET CF.
* SITES-25461: Fragmentos de contenido: el filtro por modelo en la búsqueda de CF debe distinguir entre mayúsculas y minúsculas.
* SITES-25471: Fragmentos de contenido: corrige la validación de modelos globales en ModelValidatorServlet.
* SITES-25795: Fragmentos de contenido: La API del modelo CF falla cuando no hay ninguna fecha cq establecida.
* SITES-25817: Fragmentos de contenido: Mejorar promoteLaunch: actualizar la última promoción de lanzamientos CF.
* SITES-26030: Fragmentos de contenido: El extremo /referencesTree no devuelve el encabezado necesario.
* SITES-26031: Fragmentos de contenido: El estado de replicación no se devuelve en el extremo de búsqueda CFM.
* SITES-26213: Fragmentos de contenido: los fragmentos de contenido para cancelar la publicación solo deben validar las referencias publicadas.
* SITES-26226: Fragmentos de contenido: inicia un problema del flujo de trabajo cuando ninguna de las rutas dadas es utilizable.
* SITES-26238: Fragmentos de contenido: Las referencias de recurso devueltas por la API tienen un orden diferente al orden de JCR.
* SITES-25456: Events: Al mover una página, se genera un evento eliminado por la página además del evento movido por la página.
* SITES-25658: Events: el nivel y sourceUrl no se rellenan en los eventos de estado de contenido de la página.
* SITES-6497: Lanzamientos: la página de creación del lanzamiento no funciona.
* SITES-25938: Lanzamientos: eliminación inesperada después de traducir el proyecto.
* SITES-25393: Edge Delivery con editor universal: nodos de texto que se pierden al procesar texto enriquecido con formato de párrafo único.
* SITES-24643: Edge Delivery con el editor universal: los atributos de metadatos OpenGraph y twitter no funcionan en el modelo de metadatos de página.
* SITES-25401: Fragmentos de experiencia: actualización de referencia de XF lenta


### Problemas conocidos {#known-issues-18459}

Ninguna.

### Características y API obsoletas {#deprecated-18459}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-18459}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 21 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-18459}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.70.0 | [API Oak 1.70.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.27.0 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
