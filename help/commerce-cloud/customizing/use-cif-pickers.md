---
title: CIF Uso del selector de productos y categorías de la
description: CIF Aprenda a utilizar el selector de productos y categorías en los componentes de comercio de clientes para ayudar a los autores y especialistas en marketing a trabajar de forma eficaz con los datos de catálogos y de productos de comercio.
sub-product: Commerce
topics: Development
version: Cloud Service
activity: develop
audience: developer
feature: Commerce Integration Framework
exl-id: 30f1f263-1b78-46ae-99ed-61861c488b2a
source-git-commit: ecf4c06fd290d250c14386b3135250633b26c910
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# AEM Seleccionadores de creación de contenido y comercio de {#cif-pickers}

AEM AEM La creación de contenido y comercio proporciona un conjunto de herramientas de creación para ayudar a los autores y especialistas en marketing a trabajar de forma eficaz con los datos y catálogos de productos de comercio. CIF CIF El Selector de productos y el Selector de categorías forman parte de los complementos de productos y son utilizados por los componentes principales de la. Los proyectos pueden utilizar estos selectores en cualquier cuadro de diálogo de componente para seleccionar productos o categorías.

## Selector de productos {#product-picker}

Para utilizar el selector de productos en un componente de proyecto, un desarrollador debe agregar `commerce/gui/components/common/cifproductfield` al cuadro de diálogo de componente. Por ejemplo, use lo siguiente para cq:dialog:

```xml
<product jcr:primaryType="nt:unstructured"
    sling:resourceType="commerce/gui/components/common/cifproductfield"
    fieldDescription="The product or product variant displayed by the teaser"
    fieldLabel="Select Product"
    filter="folderOrProductOrVariant"
    name="./selection"
    selectionId="sku"/>
```

El campo de producto permite desplazarse al producto que un usuario desea seleccionar mediante las diferentes vistas. De forma predeterminada, el campo product devuelve el ID del producto, pero se puede configurar con la variable `selectionId` atributo.

El campo selector de productos admite las siguientes propiedades opcionales:

- selectionId (id, uid, SKU, slug, mergedSlug, mergedSku): permite elegir el atributo de producto que devolverá el selector (predeterminado = id). El uso del SKU devuelve el SKU del producto seleccionado. Usar el SKU combinado devuelve una cadena como base#variant con los SKU del producto base y la variante seleccionada, o un SKU único si se selecciona un producto base.
- filter (folderOrProduct, folderOrProductOrVariant): filtra el contenido que el selector procesará al navegar por el árbol de productos. folderOrProduct: procesa carpetas y productos. folderOrProductOrVariant: procesa carpetas, productos y variantes de productos. Si se procesa un producto o una variante de producto, también se puede seleccionar en el selector. (predeterminado = folderOrProduct)
- multiple (true, false): habilita la selección de uno o varios productos (default = false)
- emptyText: para configurar el valor de texto vacío del campo selector

Además, las propiedades de campo de cuadro de diálogo estándar como `name`, `fieldLabel`, o `fieldDescription`, son compatibles.

>[!CAUTION]
>
>El `cifproductfield` el componente requiere el `cif.shell.picker` clientlib. Para agregar clientlib a un cuadro de diálogo, puede utilizar la propiedad extraClientlibs.
>[!CAUTION]
>
>CIF A partir de la versión 2.0.0 de los componentes principales de, la compatibilidad con `id` se ha eliminado y reemplazado por `uid`. Adobe recomienda utilizar `sku` o `slug` como identificador de producto. El Adobe sigue siendo compatible `id` CIF solo para proyectos que utilizan la versión 1.x de los componentes principales de la.

Un ejemplo práctico completo de la `cifproductfield` se puede encontrar en la [CIF Componentes principales](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/_cq_dialog/.content.xml) proyecto. Consulte también [Personalización de cuadros de diálogo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html#customizing-dialogs) AEM de la documentación de componentes principales de la.

## Selector de categoría {#category-picker}

El selector de categorías se puede utilizar en un cuadro de diálogo de componentes de forma similar al selector de productos.

El siguiente fragmento se puede utilizar en una configuración cq:dialog:

```xml
<category jcr:primaryType="nt:unstructured" 
    sling:resourceType="commerce/gui/components/common/cifcategoryfield" 
    fieldLabel="Category" 
    name="./categoryId" 
    selectionId="uid" />
```

El campo selector de categorías admite las siguientes propiedades opcionales:

- selectionId(id, uid, slug, urlPath, idAndUrlPath) _(obsoleto)_, uidAndUrlPath _(obsoleto)_): permite elegir el atributo de categoría que el selector devolverá (predeterminado = id).
- multiple (true, false): habilita la selección de una o varias categorías (default = false)

Además, las propiedades de campo de cuadro de diálogo estándar como `name`, `fieldLabel`, o `fieldDescription`, son compatibles.

>[!CAUTION]
>
>Igual que el `cifproductfield` Componente el `cifcategoryfield` Este componente también requiere el `cif.shell.picker` clientlib. Para agregar una clientlib a un cuadro de diálogo, puede utilizar la variable `extraClientlibs` propiedad. Consulte [Personalización de cuadros de diálogo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html#customizing-dialogs) AEM de la documentación de componentes principales de la.
>[!CAUTION]
>
>CIF A partir de la versión 2.0.0 de los componentes principales de, la compatibilidad con `id` se ha eliminado y reemplazado por `uid`. Adobe recomienda utilizar `uid` o `urlPath` como identificador de categoría. El Adobe sigue siendo compatible `id` &amp; `idAndUrlPath` CIF solo para proyectos que utilizan la versión 1.x de los componentes principales de la.

Un ejemplo práctico completo de la `cifcategoryfield` se puede encontrar en la [CIF Componentes principales](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/featuredcategorylist/v1/featuredcategorylist/_cq_dialog/.content.xml) proyecto.
