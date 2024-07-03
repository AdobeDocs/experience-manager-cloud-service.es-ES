---
title: CIF Atributos personalizados para crear un carrusel de productos de
description: AEM CIF Obtenga información sobre cómo ampliar el componente Carrusel de productos de la actualizando el modelo Sling y personalizando el marcado.
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 594f0e6ec88851c86134be8d5d7f1719f74ddf4f
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# CIF Atributos personalizados para crear un carrusel de productos de {#product-carousel}

## Introducción {#intro}

El componente Carrusel de productos se amplía a través de este tutorial. Como primer paso, añada una instancia del carrusel de productos a la página de inicio para comprender la funcionalidad de línea de base:

1. Navegue hasta la página de inicio del sitio, por ejemplo [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)
1. Inserte un nuevo componente Carrusel de productos en el contenedor de diseño principal de la página.
   ![Componente de carrusel de productos](/help/commerce-cloud/assets/product-carousel-component.png)
1. Expanda el panel lateral (si no está activado) y cambie la lista desplegable del buscador de recursos a **Productos**.
     ![Productos de carrusel](/help/commerce-cloud/assets/carousel-products.png)    
1. Esto debería mostrar una lista de los productos disponibles de una instancia de Adobe Commerce conectada.
   ![Instancia conectada](/help/commerce-cloud/assets/connected-instance.png)
1. Los productos se mostrarán como se muestra a continuación con las propiedades predeterminadas:
   ![Producto mostrado con propiedades](/help/commerce-cloud/assets/discount.png)

## Actualización del modelo de Sling {#update-sling-model}

Puede ampliar la lógica empresarial del carrusel de productos implementando un modelo Sling:

1. En el IDE, vaya al módulo principal a `core/src/main/java/com/venia/core/models/commerce` CIF y cree una interfaz de carrusel personalizada que amplíe la interfaz de carrusel de productos de la interfaz de la interfaz de Carrusel de productos:

   ```
   package com.venia.core.models.commerce;
   import com.adobe.cq.commerce.core.components.models.productcarousel.ProductCarousel;
   public interface CustomCarousel extends ProductCarousel {
   }
   ```
1. A continuación, cree una clase de implementación `CustomCarouselImpl.java` en `core/src/main/java/com/venia/core/models/commerce/CustomCarouselImpl.java`.
El patrón de delegación para modelos Sling permite `CustomCarouselImpl` para referencia `ProductCarousel` modelo a través de `sling:resourceSuperType` propiedad:

   ```
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductCarousel productCarousel;
   ```

1. La anotación @PostConstruct garantiza que se llame a este método cuando se inicialice el modelo Sling. La consulta de GraphQL del producto ya se ha ampliado utilizando el método extendProductQueryWith para recuperar atributos. Actualice la consulta de GraphQL para incluir el atributo en la consulta parcial:

   ```
   @PostConstruct
   private void initModel() {
   productsRetriever = productCarousel.getProductsRetriever();
   
   if(productCarousel.getProductsRetriever() != null)
   productCarousel.getProductsRetriever().extendProductQueryWith(p -> p
   .createdAt()
   .addCustomSimpleField("accessory_gemstone_addon")
   );
   }
   ```

   En el código anterior, la variable `addCustomSimpleField` se utiliza para recuperar la variable `accessory_gemstone_addon` atributo.

## Personalización del marcado {#customize-markup}

Para personalizar aún más el marcado:

1. Crear una copia de `productcard.html` de `/apps/core/cif/components/commerce/productcarousel/v1/productcarousel` (la ruta crxde del componente principal) al módulo ui.apps `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productcarousel/productcard.html`.

1. Editar `productcard.html` para llamar al atributo personalizado, que se menciona en la clase de implementación:

   ```xml
   ..
   <div
       data-product-sku="${product.commerceIdentifier.value}"
       data-product-base-sku="${product.combinedSku.baseSku}"
       id="${product.id}"
       data-cmp-data-layer="${product.data.json}"
       class="card product__card">
       <span>${product.product.responseData['accessory_gemstone_addon']}</span>
       <a href="${product.URL}"
           target="${productCarousel.linkTarget}"
   ..
   ```

1. AEM Guarde los cambios e implemente las actualizaciones para que se implementen mediante el comando de Maven, desde un terminal de línea de comandos. Podrá ver el atributo personalizado `accessory_gemstone_addon` para los productos seleccionados en la página.
