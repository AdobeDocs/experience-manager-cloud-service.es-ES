---
title: Notas de la versión 2020.9.0 de la versión  [!DNL Adobe Experience Manager] as a Cloud Service.
description: '[!DNL Adobe Experience Manager] as a Cloud Service Notas de la versión 2020.9.0.'
translation-type: tm+mt
source-git-commit: cca8aff3ada327252bfabd2207e7aa86fdf00033
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 24%

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
