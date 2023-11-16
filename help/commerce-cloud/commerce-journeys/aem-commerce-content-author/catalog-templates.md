---
title: Administrar páginas y plantillas del catálogo de productos
description: Obtenga información sobre cómo administrar páginas y plantillas de catálogo de productos
exl-id: 0d795d85-c865-40d5-941e-e02ee96fdd11
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 2%

---

# Administrar páginas y plantillas del catálogo de productos {#product-catalog}

Obtenga información sobre cómo administrar páginas y plantillas de catálogo de productos.

## La historia hasta ahora {#story-so-far}

AEM En el documento anterior del recorrido de creación de Contenido y comercio de la, [AEM CIF Introducción a los conceptos básicos de creación de la](getting-started.md)CIF , ha aprendido los conceptos básicos de la creación de la.

Este artículo se basa en estos aspectos básicos.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo administrar las páginas y plantillas del catálogo de productos. Después de leer, debería haber logrado lo siguiente:

* comprender los conceptos de las plantillas de catálogo
* cómo funcionan las plantillas genéricas
* ha creado una plantilla individual

## El concepto básico {#basic-concept}

La tienda Venia incluye una experiencia típica de catálogo de productos con navegación y aterrizaje, categoría (PLP) y páginas de detalles de producto (PDP).

AEM CIF Las páginas de catálogo se crean dinámicamente mediante una plantilla de catálogo de de datos y datos de producto en tiempo real que se recuperan del extremo de comercio cuando es necesario. Cada catálogo tiene una plantilla genérica para páginas de productos y categorías.
![estructura del catálogo](assets/catalog-structure.png)

El componente de navegación muestra el contenido y las páginas del catálogo. Es posible mostrar la página de aterrizaje del catálogo o las categorías de primer nivel en la navegación. Al pasar el ratón por encima de una categoría, se mostrarán las categorías de segundo nivel como una segunda línea.
![navegación por catálogo](assets/catalog-navigation.png)

Al hacer clic en una categoría, se abre la página de categoría (o la página de lista de productos).

![PLP](assets/catalog-plp.png)

Al hacer clic en un producto, se abre la página de detalles del producto.

![PLP](assets/catalog-pdp.png)

## Las plantillas {#templates}

### Plantillas genéricas {#generic}

La plantilla de catálogo de Venia genérica utiliza el componente principal de la lista de productos. Este componente muestra la imagen de la categoría si está disponible y los productos de la categoría.
![plantilla de categoría](assets/category-template.png)

La plantilla de producto genérica Venia utiliza el componente principal Detalles del producto. Este componente muestra información del producto para varios tipos de productos y acciones de complemento al carro de compras.
![plantilla de producto](assets/product-template.png)

### Editar plantillas {#edit-templates}

Las plantillas se pueden editar abriendo directamente la página de la plantilla o cambiando al modo de edición mientras navega por una página del catálogo de productos. Tenga en cuenta que al cambiar la página se cambiará la plantilla y no solo la página específica del producto/categoría.

### Plantillas específicas de categoría o producto {#specific}

CIF La aplicación admite varias plantillas en solo unos clics. Para crear otra plantilla, seleccione la plantilla genérica de la categoría correspondiente y cree una nueva página utilizando **Crear** acción.

![crear página de plantilla](assets/create-template-page.png)

Seleccione la plantilla de producto o categoría correspondiente.

![crear selección de plantilla](assets/create-template-select.png)

Introduzca el título y cree la página.

![crear entrada de plantilla](assets/create-template-enter.png)

Observe que ahora tiene una plantilla específica debajo de la genérica.

![crear jerarquía de plantillas](assets/create-template-hierachry.png)

Abra la plantilla. Se parece exactamente a la plantilla de categoría genérica.

![crear plantilla nueva](assets/create-template-new.png)

Añada cualquier imagen en la parte superior de la página.

![crear actualización de plantilla](assets/create-template-update.png)

La plantilla se puede previsualizar con cualquier categoría o producto. Abrir **Información de página** y luego seleccione **Ver con categoría / producto**. Seleccione el producto/categoría del selector para obtener una vista previa de este producto/categoría. Seleccionar **Compra El Look** para obtener una vista previa de la plantilla actualizada.

![crear plantilla ](assets/create-template-picker.png)

Ahora tenemos que asignar esta plantilla a la categoría específica. Abra las propiedades en **Información de página** y cambie a la pestaña commerce. Haga clic en el icono de la carpeta para seleccionar **Compra El Look** del selector de categorías. Es posible asignar varias categorías a una plantilla e incluir también subcategorías activando la casilla de verificación.

![crear plantilla asociada](assets/create-template-associate.png)

Vuelva a la página principal y haga clic en **Compra El Look** para ver la plantilla específica. Todas las demás categorías seguirán utilizando la plantilla genérica.

![crear resultado de plantilla](assets/create-template-result.png)

Se puede aplicar el mismo flujo de trabajo para crear plantillas de producto individuales.

## Siguientes pasos {#what-is-next}

Ahora que ha completado esta parte del recorrido, debe:

* comprender los conceptos de las plantillas de catálogo
* cómo funcionan las plantillas genéricas
* ha creado una plantilla individual

Aproveche este conocimiento y continúe con su recorrido revisando el documento a continuación [Administrar experiencias del catálogo de productos clasificados](staged-catalog.md)AEM , donde aprenderá a trabajar con los datos de los productos clasificados y los lanzamientos de la.

## Recursos adicionales {#additional-resources}

Aunque se recomienda pasar a la siguiente parte del recorrido revisando el documento [Administrar experiencias del catálogo de productos clasificados](staged-catalog.md)Sin embargo, los siguientes son algunos recursos opcionales extra. Profundizan en varios conceptos mencionados en este documento, pero no son necesarios para continuar con el recorrido sin encabezado:

* [Creación de páginas de múltiples productos y categorías](/help/commerce-cloud/authoring/multi-template-usage.md)
* [Guía de migración para el Experience Manager Cloud Service](/help/commerce-cloud/migration.md) AEM - Cómo migrar al complemento de Commerce integration framework CIF de () desde una versión antigua
