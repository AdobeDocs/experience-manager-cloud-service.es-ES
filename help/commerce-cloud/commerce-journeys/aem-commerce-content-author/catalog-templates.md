---
title: Administrar páginas y plantillas de catálogo de productos
description: Obtenga información sobre cómo administrar las plantillas y páginas del catálogo de productos
exl-id: 0d795d85-c865-40d5-941e-e02ee96fdd11
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 2%

---

# Administrar páginas y plantillas de catálogo de productos {#product-catalog}

Obtenga información sobre cómo administrar las plantillas y páginas del catálogo de productos.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido de creación de contenido y comercio de AEM, [Introducción a AEM conceptos básicos de creación del CIF](getting-started.md), ha aprendido lo básico de la creación del CIF.

Este artículo se basa en estos fundamentos.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo administrar las plantillas y páginas del catálogo de productos. Después de leer, debería haber logrado lo siguiente:

* comprender los conceptos de las plantillas de catálogo
* cómo funcionan las plantillas genéricas
* han creado una plantilla individual

## El concepto básico {#basic-concept}

La tienda Venia viene con una experiencia típica del catálogo de productos con navegación, y aterrizaje, categoría (PLP) y páginas de detalles de productos (PDP).

Las páginas del catálogo se crean dinámicamente mediante una plantilla de catálogo del CIF de AEM y datos de producto en tiempo real que se recuperan del extremo de comercio cuando es necesario. Cada catálogo tiene una plantilla genérica para páginas de productos y categorías.
![estructura del catálogo](assets/catalog-structure.png)

El componente de navegación muestra contenido y páginas de catálogo. Es posible mostrar la página de aterrizaje del catálogo o las categorías de primer nivel en la navegación. Al pasar el ratón por encima de una categoría, se mostrarán las categorías de segundo nivel como una segunda línea.
![navegación por el catálogo](assets/catalog-navigation.png)

Al hacer clic en una categoría se abrirá la página de categoría (o página de lista de productos).

![PLP](assets/catalog-plp.png)

Al hacer clic en un producto, se abrirá la página de detalles del producto.

![PLP](assets/catalog-pdp.png)

## Las plantillas {#templates}

### Plantillas genéricas {#generic}

La plantilla de catálogo genérica de Venia utiliza el componente principal de lista de productos. Este componente muestra la imagen de categoría si está disponible y los productos de la categoría.
![plantilla de categoría](assets/category-template.png)

La plantilla de producto genérica Venia utiliza el componente principal de detalles del producto. Este componente muestra la información del producto para varios tipos de producto y la acción de complemento al carro de compras.
![plantilla de producto](assets/product-template.png)

### Editar plantillas {#edit-templates}

Las plantillas se pueden editar abriendo directamente la página de plantillas o cambiando al modo de edición mientras se explora una página de catálogo de productos. Tenga en cuenta que al cambiar la página se cambiará la plantilla y no solo la página específica del producto/categoría.

### Plantillas de categoría o específicas de producto {#specific}

CIF admite varias plantillas en tan solo unos pocos clics. Para crear otra plantilla, seleccione la plantilla genérica de la categoría correspondiente y cree una nueva página utilizando la variable **Crear** acción.

![crear página de plantilla](assets/create-template-page.png)

Seleccione la plantilla de producto o categoría correspondiente.

![crear plantilla seleccionar](assets/create-template-select.png)

Introduzca el título y cree la página.

![crear plantilla entrar](assets/create-template-enter.png)

Observe que ahora tiene una plantilla específica en la genérica .

![crear jerarquía de plantillas](assets/create-template-hierachry.png)

Abra la plantilla . Se parece exactamente a la plantilla de categoría genérica.

![crear plantilla nueva](assets/create-template-new.png)

Agregue cualquier imagen sobre la página.

![crear actualización de plantilla](assets/create-template-update.png)

La plantilla se puede previsualizar con cualquier categoría o producto. Apertura **Información de la página** y, a continuación, seleccione **Ver con categoría/producto**. Seleccione el producto/categoría del selector para obtener una vista previa de este producto/categoría. Select **Compre El Aspecto** para obtener una vista previa de la plantilla actualizada.

![crear plantilla ](assets/create-template-picker.png)

Ahora tenemos que asignar esta plantilla a la categoría específica. Abra las propiedades en la **Información de la página** y cambie a la pestaña comercio . Haga clic en el icono de la carpeta para seleccionar la **Compre El Aspecto** del selector de categorías. Es posible asignar varias categorías a una plantilla y también incluir subcategorías habilitando la casilla de verificación.

![crear plantilla asociada](assets/create-template-associate.png)

Vuelva a la página principal y haga clic en **Compre El Aspecto** para ver la plantilla específica. Todas las demás categorías siguen utilizando la plantilla genérica .

![crear resultado de plantilla](assets/create-template-result.png)

Se puede aplicar el mismo flujo de trabajo para crear plantillas de producto individuales.

## Siguientes pasos {#what-is-next}

Ahora que ha completado esta parte del recorrido, debe:

* comprender los conceptos de las plantillas de catálogo
* cómo funcionan las plantillas genéricas
* han creado una plantilla individual

Aproveche este conocimiento y continúe con su recorrido revisando el documento [Administrar experiencias de catálogo de productos por etapas](staged-catalog.md), donde aprenderá a trabajar con datos de productos clasificados y AEM lanzamientos.

## Recursos adicionales {#additional-resources}

Aunque se recomienda pasar a la siguiente parte del recorrido revisando el documento [Administrar experiencias de catálogo de productos por etapas](staged-catalog.md), los siguientes son algunos recursos opcionales adicionales que profundizan en algunos conceptos mencionados en este documento, pero no son necesarios para continuar con el recorrido sin encabezado:

* [Creación de páginas de múltiples productos y categorías](/help/commerce-cloud/authoring/multi-template-usage.md)
* [Guía de migración para el Experience Manager Cloud Service](/help/commerce-cloud/migration.md) - Cómo migrar al complemento AEM Commerce Integration Framework (CIF) desde una versión antigua
