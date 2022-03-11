---
title: Introducción a la creación de CIF
description: Introducción a la creación de CIF
exl-id: 0bef4d8c-0ad3-4ec8-ab08-8c83203b3b68
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 2%

---

# Introducción a la creación AEM CIF {#getting-started}

Obtenga información sobre AEM creación del CIF.

## La historia hasta ahora {#story-so-far}

En el documento anterior de este recorrido de Contenido y Comercio AEM, [Obtenga información sobre AEM contenido y comercio](/help/commerce-cloud/introduction.md), aprendió la teoría básica de lo que es un CMS sin objetivos y ahora debería entender los conceptos básicos de Contenido y Comercio AEM.

Este artículo se basa en estos fundamentos.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo utilizar CIF para la creación específica de contenido y comercio. Después de leer, debe:

* Comprender los conceptos de creación del CIF con el Editor universal
* Cómo acceder a los datos del catálogo de productos en AEM usando selectores de productos y categorías
* Acceso a los datos de contenido y comercio mediante la cabina de productos y AEM Omnisearch

## Creación de CIF en el Editor universal {#cif-authoring}

CIF amplía el Editor universal con capacidades para acceder a los datos del producto en tiempo real sin abandonar el contexto:

Abra el panel lateral y seleccione &quot;Productos&quot; en la lista desplegable.
![Seleccionar tipo de producto](assets/asset-finder-overview.png)

Puede examinar el catálogo de productos o utilizar el campo de búsqueda de texto completo para buscar productos.
![tipo de producto](assets/asset-finder-search.png)

Los productos se pueden soltar en componentes compatibles con las caídas de productos (por ejemplo, teaser de productos, carrusel de productos) directamente en la página que crea automáticamente un componente teaser de productos.

## seleccionadores de productos y categorías {#pickers}

Si se requieren datos de producto y categoría en componentes de comercio o AEM cuadros de diálogo de back-office, AEM autores pueden utilizar selectores que son elementos de interfaz de usuario para buscar cómodamente y seleccionar datos del catálogo de productos.

### Selector de productos

Al hacer clic en el icono de la carpeta, se abrirá la interfaz de usuario modal del selector (por ejemplo, teaser de productos)
![selector de productos](assets/product-picker-open.png)

Los productos se pueden encontrar navegando por la estructura del catálogo a la izquierda o buscando. La búsqueda de texto completo respetará la categoría seleccionada y limitará los resultados de búsqueda a esta categoría.
![carpeta del selector de productos](assets/product-picker-folders.png)

Los productos con variaciones se marcan con un icono de carpeta en el que se puede hacer clic para mostrar todas las variaciones.
![variantes del selector de productos](assets/product-picker-variants.png)
![variantes del selector de productos abiertas](assets/product-picker-variants-open.png)

### Selector de categoría

Funciona como un selector de productos. Al hacer clic en el icono de la carpeta, se abrirá la interfaz de usuario modal del selector (por ejemplo, carrusel de categorías)
![selector de categorías](assets/category-picker-open.png)

Examine la estructura del catálogo a la izquierda y seleccione la categoría .
![selector de categorías](assets/category-picker-folders.png)

## Product Cockpit {#cockpit}

La cabina de productos es un lugar central para acceder rápidamente al catálogo de productos con todo su contenido enriquecido. En uno de los siguientes módulos aprenderá a enriquecer los datos del producto con contenido. Por ahora, centrémonos en acceder a los datos de los productos.

En el menú principal, haga clic en comercio para ver una lista de todos los catálogos de productos adjuntos.
![elemento de menú de comercio](assets/commerce-menu-item.png)

Muestra una lista de todos los catálogos de productos de conexión.
![catálogos integrados de cabina](assets/cockpit-Integrated-catalogs.png)

El catálogo de productos muestra de forma predeterminada todas las categorías de primer nivel con todos los productos. Al hacer clic en una categoría se abrirá esa categoría con todos los productos y subcategorías relacionados, incluidos sus productos.
![catálogo de productos de cocpit](assets/cockpit-product-catalog.png)

Puede abrir las propiedades del producto haciendo clic en el icono de propiedad. El icono aparece al pasar el ratón sobre el mosaico de un producto.
![propiedades de producto de la cabina](assets/cockpit-properties.png)

Todas las propiedades del producto son de solo lectura porque los datos se cargan en tiempo real desde el servidor conectado. El cambio de las propiedades del producto debe realizarse en el sistema back-end que es el sistema de registro. La pestaña **Variantes** solo aparecerá si el producto tiene variaciones. Al hacer clic en la pestaña , se mostrarán todas las variaciones con sus atributos.
![variantes de producto de cabina](assets/cockpit-properties-variants.png)

Las fichas restantes muestran todo AEM contenido asociado al producto. Discutiremos estas pestañas en uno de los siguientes módulos.

## AEM Omnisearch {#omnisearch}

El uso de Omnisearch es una forma sencilla de encontrar AEM contenido mediante la búsqueda de texto completo. CIF amplía Omnisearch con búsqueda de texto completo de catálogos de productos con su contenido AEM asociado.
![elemento de menú de comercio](assets/omnisearch.png)

Omnisearch realizará una búsqueda de texto completo en el backend de comercio para encontrar todos los productos relacionados. El resultado aparece en **Ver todos los productos**. Omnisearch también buscará AEM contenido asociado al producto buscado. Los resultados se incluirán en las categorías AEM respectivas. En este ejemplo, un fragmento de contenido está relacionado con el producto.

## Siguientes pasos {#what-is-next}

Ahora que ha completado esta parte del recorrido, debe:

* Comprender los conceptos de creación del CIF con el Editor universal
* Cómo acceder al catálogo de productos en AEM usando selectores de productos y categorías
* Acceso a los datos de contenido y comercio mediante la cabina de productos y AEM Omnisearch

Aproveche este conocimiento y continúe con su recorrido revisando el documento [Administrar plantillas y páginas del catálogo de productos](catalog-templates.md), donde aprenderá a crear y personalizar su primera experiencia de catálogo de productos.

## Recursos adicionales {#additional-resources}

Aunque se recomienda pasar a la siguiente parte del recorrido revisando el documento [Administrar plantillas y páginas del catálogo de productos](catalog-templates.md), los siguientes son algunos recursos opcionales adicionales que profundizan en algunos conceptos mencionados en este documento, pero no son necesarios para continuar en el recorrido.

* [Configuración de tiendas y catálogos](/help/commerce-cloud/getting-started.md#catalog)
