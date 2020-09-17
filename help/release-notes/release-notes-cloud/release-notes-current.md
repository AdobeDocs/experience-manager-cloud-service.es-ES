---
title: Notas de la versión 2020.9.0 de la versión  [!DNL Adobe Experience Manager] as a Cloud Service.
description: '[!DNL Adobe Experience Manager] as a Cloud Service Notas de la versión 2020.9.0.'
translation-type: tm+mt
source-git-commit: 529a538948f537fde8b2c50fb1f3acc942a7cb64
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 22%

---


# Notas de la versión [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 {#release-notes}

En la siguiente sección se describen las notas de la versión generales de Experience Manager as a Cloud Service 2020.9.0.

## [!DNL Adobe Experience Manager Sites] como Cloud Service {#sites}

### What is new in [!DNL Sites] {#what-is-new-sites}

* El SDK de Javascript del Editor de aplicaciones de una sola página (SPA) [ahora es de código abierto.](/help/implementing/developing/spa/reference-materials.md)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

* Componentes principales de CIF v1.3.0. Consulte Componentes [principales de](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.3.0) CIF para obtener más detalles.

* Ya está disponible la capacidad de previsualización con plantillas de producto/categoría para productos y categorías. Esto permite a los usuarios/especialistas en marketing de AEM negocios realizar vistas de las plantillas de producto/categoría con datos reales.

* Se agregó la página de propiedades a productos y categorías para permitir que los usuarios comerciales puedan obtener detalles de vista asociados con el SKU o ID de categoría del producto.

* Función de ordenación agregada a la consola de producto para permitir la clasificación de productos/categorías por nombre o atributos de precio.

* Funcionalidad de búsqueda de productos agregada a la consola de producto.

### Corrección de errores {#bug-fixes-commerce}

* Las configuraciones de Commerce Cloud no respetaban la herencia. Esto se ha solucionado para garantizar que la configuración hereda valores.

## Cloud Manager {#cloud-manager}

### Fecha de la versión {#release-date-cm}

The Release Date for [!UICONTROL Cloud Manager] Version 2020.9.0 is September 03, 2020.

### Novedades {#what-is-new-cloud-manager}

* La auditoría de contenido se ha vuelto a etiquetar como auditoría de experiencias.
* El proceso de compilación se ha separado en tres comandos Maven independientes.
* Si el repositorio Git no se clona, se volverá a crear hasta tres veces.

### Corrección de errores {#bug-fixes-cm}

* La ficha Auditoría de contenido mostraba incorrectamente la dirección URL base utilizando el dominio de autor en lugar del dominio de publicación.

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

Consulte esta sección para conocer las novedades y las actualizaciones de Cloud Manager versión 1.1.0.

### Novedades {#what-is-new-cra}

* El analizador de preparación para la nube (CRA) tiene una consola de estado de inicio que muestra un botón explícito &quot;Generar informe&quot; en el que el usuario puede hacer clic para ejecutar el CRA.

* La interfaz de usuario de CRA muestra el progreso mientras se está ejecutando. Muestra los elementos que se analizan y los resultados encontrados durante la ejecución.

* El informe CRA muestra un resumen y el número de conclusiones en un formato de tabla organizado por el tipo de búsqueda y el nivel de importancia. Al hacer clic en el número de esa búsqueda, se desplazará automáticamente a la ubicación de esa búsqueda en el informe.

### Corrección de errores {#cra-bug-fixes}

* En algunos casos, el informe CRA no se actualizaba después de forzar una actualización. Esto se ha corregido en esta versión.

