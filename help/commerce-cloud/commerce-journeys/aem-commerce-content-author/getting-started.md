---
title: Introducción a la creación de CIF
description: Introducción a la creación de CIF
exl-id: 0bef4d8c-0ad3-4ec8-ab08-8c83203b3b68
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 2%

---

# AEM Introducción a la creación de CIF de {#getting-started}

AEM Obtenga información acerca de la creación de CIF de.

## La historia hasta ahora {#story-so-far}

AEM En el documento anterior de este recorrido de contenido y comercio de la, [AEM Obtenga información sobre Contenido y comercio de la](/help/commerce-cloud/introduction.md)AEM , ha aprendido la teoría básica de lo que es un CMS sin encabezado y ahora debe comprender los conceptos básicos de Contenido y comercio de la.

Este artículo se basa en estos aspectos básicos.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo utilizar CIF para la creación específica de contenido y comercio. Después de leer, debería:

* Comprender los conceptos de creación del CIF con el editor universal
* AEM Cómo acceder a los datos del catálogo de productos en el uso de selectores de productos y categorías en el
* AEM Cómo acceder a los datos de contenido y comercio mediante la cabina de productos y el acceso a la plataforma de datos de Omnisearch y el acceso a la plataforma de datos de Omnisearch

## Creación del CIF en el editor universal {#cif-authoring}

CIF amplía el editor universal con funciones para acceder a los datos de productos en tiempo real sin salir del contexto:

Abra el panel lateral y seleccione &quot;Productos&quot; en la lista desplegable.
![Seleccionar tipo de producto](assets/asset-finder-overview.png)

Puede examinar el catálogo de productos o utilizar el campo de búsqueda de texto completo para encontrar productos.
![tipo de producto](assets/asset-finder-search.png)

Los productos se pueden soltar en componentes compatibles con lanzamientos de productos (por ejemplo, teaser de productos, carrusel de productos) directamente en la página que crea automáticamente un componente teaser de productos.

## Seleccionadores de productos y categorías {#pickers}

AEM AEM Si se requieren datos de producto y categoría en los componentes de comercio o en los cuadros de diálogo de administración de la aplicación, los autores de la aplicación pueden utilizar selectores, que son elementos de la interfaz de usuario, para buscar y seleccionar cómodamente los datos del catálogo de productos.

### Selector de productos

Al hacer clic en el icono de la carpeta se abrirá la interfaz de usuario modal del selector (por ejemplo, teaser de productos)
![selector de productos](assets/product-picker-open.png)

Los productos se pueden encontrar navegando a través de la estructura del catálogo a la izquierda o buscando. La búsqueda de texto completo respetará la categoría seleccionada y limitará los resultados de búsqueda a esta categoría.
![carpeta del selector de productos](assets/product-picker-folders.png)

Los productos con variaciones están marcados con un icono en forma de carpeta en el que se puede hacer clic para mostrar todas las variaciones.
![variantes del selector de productos](assets/product-picker-variants.png)
![variantes del selector de productos abiertas](assets/product-picker-variants-open.png)

### Selector de categoría

Funciona como un selector de productos. Al hacer clic en el icono de la carpeta se abrirá la interfaz de usuario modal del selector (por ejemplo, carrusel de categorías)
![selector de categoría](assets/category-picker-open.png)

Examine la estructura del catálogo a la izquierda y seleccione la categoría.
![selector de categoría](assets/category-picker-folders.png)

## Product Cockpit {#cockpit}

La cabina de productos es un lugar central para acceder rápidamente al catálogo de productos con todo su contenido enriquecido. En uno de los siguientes módulos aprenderá a enriquecer datos de productos con contenido. Por ahora, vamos a centrarnos en acceder a los datos del producto.

En el menú principal, haga clic en comercio para ver una lista de todos los catálogos de productos adjuntos.
![elemento del menú de comercio](assets/commerce-menu-item.png)

Esto muestra una lista de todos los catálogos de productos de Connect.
![catálogos integrados en cabina](assets/cockpit-Integrated-catalogs.png)

El catálogo de productos muestra de forma predeterminada todas las categorías de primer nivel con todos los productos. Al hacer clic en una categoría, se abrirá esa categoría con todos los productos y subcategorías relacionados, incluidos sus productos.
![catálogo de productos cockpit](assets/cockpit-product-catalog.png)

Puede abrir las propiedades del producto haciendo clic en el icono de propiedad. El icono aparece al pasar el ratón por encima de un mosaico de producto.
![propiedades de producto de cabina](assets/cockpit-properties.png)

Todas las propiedades del producto son de solo lectura porque los datos se cargan en tiempo real desde el servidor conectado. El cambio de las propiedades del producto debe realizarse en el sistema back-end, que es el sistema de registro. La pestaña **Variantes** solo aparecerá si el producto tiene variaciones. Al hacer clic en la pestaña, se muestran todas las variaciones con sus atributos.
![variantes de producto de cabina](assets/cockpit-properties-variants.png)

AEM Las pestañas restantes muestran todo el contenido de la asociado con el producto. Analizaremos estas fichas en uno de los siguientes módulos.

## AEM Búsqueda de Omnisearch {#omnisearch}

AEM El uso de Omnisearch es una manera fácil de encontrar contenido de la mediante la búsqueda de texto completo. AEM El CIF amplía Omnisearch con la búsqueda de texto completo de catálogos de productos con su contenido asociado de la.
![elemento del menú de comercio](assets/omnisearch.png)

Omnisearch ejecutará una búsqueda de texto completo en el backend del comercio para encontrar todos los productos relacionados. El resultado se enumera en **Ver todos los productos**. AEM Omnisearch también buscará el contenido que esté asociado con el producto buscado. AEM Los resultados se enumeran en las respectivas categorías de. En este ejemplo, un fragmento de contenido está relacionado con el producto.

## Siguientes pasos {#what-is-next}

Ahora que ha completado esta parte del recorrido, debe:

* Comprender los conceptos de creación del CIF con el editor universal
* AEM Cómo acceder al catálogo de productos en el uso de selectores de productos y categorías en el
* AEM Cómo acceder a los datos de contenido y comercio mediante la cabina de productos y el acceso a la plataforma de datos de Omnisearch y el acceso a la plataforma de datos de Omnisearch

Aproveche este conocimiento y continúe con su recorrido revisando el documento a continuación [Administrar páginas y plantillas del catálogo de productos](catalog-templates.md), donde aprenderá a crear y personalizar su primera experiencia con el catálogo de productos.

## Recursos adicionales {#additional-resources}

Aunque se recomienda pasar a la siguiente parte del recorrido revisando el documento [Administrar páginas y plantillas del catálogo de productos](catalog-templates.md)Sin embargo, los siguientes son algunos recursos opcionales extra. Profundizan en varios conceptos mencionados en este documento, pero no son necesarios para continuar el recorrido.

* [Configuración de tiendas y catálogos](/help/commerce-cloud/getting-started.md#catalog)
