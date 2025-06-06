---
title: Metadatos JSON-LD
description: Obtenga información sobre cómo habilitar y comprobar la función JSON+LD en AEM CIF.
feature: Commerce Integration Framework
role: Admin, Developer
exl-id: 547d3721-e094-4a42-8a7c-27e4ef97ea9c
source-git-commit: 6ee09ab274e26f6972a81e662b78030a71b3fc9b
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 3%

---

# Metadatos JSON-LD {#json-ld}

En esta guía se explica cómo habilitar y comprobar la función JSON+LD en AEM CIF.

>[!NOTE]
>
> Esta característica es experimental.

## Habilitar JSON+LD en la configuración de CIF {#enabling}

De manera predeterminada, la casilla de verificación **Habilitar JSON+LD** no está visible en la configuración de CIF. Para habilitar esta función, el proyecto debe incluir la configuración OSGi necesaria, que permite mostrar la casilla de verificación. Esta configuración permite a los usuarios alternar la compatibilidad con scripts JSON+LD en las páginas de producto.
Para que la casilla de verificación **Habilitar JSON+LD** esté disponible en la configuración de CIF, agregue la siguiente configuración OSGi al proyecto: &grave;
com.adobe.cq.cif.components.models.JsonLdFeatureEnable&grave;.
Para obtener más información sobre cómo agregar esta configuración, consulte [Agrega la configuración para Json-Ld](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.cif.components.models.JsonLdFeatureEnable.cfg.json) en el repositorio público aem-cif-guides-venia.

Una vez que se agrega e implementa esta configuración, la casilla de verificación se vuelve visible en los ajustes de configuración de CIF y estos son los pasos para habilitar **JSON+LD**:

1. Vaya a la configuración de CIF en AEM.
1. Cancelar herencia.
1. Marque la casilla de verificación **Habilitar JSON+LD**.
1. Guarde la configuración.

## Verificación de JSON+LD en una página de detalles del producto (PDP) {#verify}

Para ilustrar los pasos para verificar JSON+LD, se utiliza el proyecto Venia como ejemplo, donde ya se ha añadido la configuración JSON+LD necesaria para habilitar la función. Estos son los pasos a seguir:

1. Vaya a la instancia local de AEM y abra la Página de detalles del producto (PDP): http://localhost:4502/editor.html/content/venia/us/en/products/product-page.html
1. Cree un producto en la página de detalles del producto (PDP).
1. Cambiar al modo **Ver como Publicar**.
1. Abra **Ver página Source** en su explorador.
1. Busque JSON+LD en el origen de la página.

Si se configura correctamente, encontrará el script JSON+LD asociado con el producto insertado en la página.

## Estructura JSON+LD de muestra para un producto {#sample}

A continuación se muestra un ejemplo de la estructura **JSON+LD** para la falda Agatha, creada en la página PDP del proyecto Venia:

```
<script type="application/ld+json">
{
  "@context": "http://schema.org",
  "@type": "Product",
  "sku": "VSK05",
  "name": "Agatha Skirt",
  "image": "https://mcstaging.catalogservice4commerce.fun/media/catalog/product/cache/926ea6fc2ad48a7202ff4587b6c2768e/v/s/vsk05-pe_main_2.jpg",
  "description": "The Agatha Skirt has a large circumference that lends itself to all sorts of drama...",
  "@id": "product-ef4fa1dc72",
  "offers": [
    {
      "@type": "Offer",
      "sku": "VSK05-KH-S",
      "url": "/content/venia/us/en/products/product-page.html/agatha-skirt.html",
      "priceCurrency": "USD",
      "price": 78.0
    },
    {
      "@type": "Offer",
      "sku": "VSK05-RN-XS",
      "availability": "InStock",
      "priceSpecification": {
        "@type": "UnitPriceSpecification",
        "priceType": "https://schema.org/ListPrice",
        "price": 18.0,
        "priceCurrency": "USD"
      },
      "price": 46.0
    }
  ]
}
</script>
```

## Asignación de atributos JSON+LD a GraphQL {#mapping}

Los atributos JSON+LD se pueden asignar a consultas de GraphQL en AEM CIF, lo que garantiza que los datos estructurados reflejen dinámicamente la información del producto recuperada mediante GraphQL.

### Asignación de productos de ejemplo {#example}

| Atributo JSON+LD | Atributo GraphQL de Magento | Obligatorio (S/N) |
|---------------------------------|-------------------|---|
| sku | sku | N |
| offers.url | Lógica personalizada | N |
| offers.SpecialPricedate | special_to_date | N |
| offers.sku | sku | N |
| offers.priceSpecification.priceCurrency | moneda | Y |
| offers.priceSpecification.price | regular_price | N |
| offers.priceCurrency | moneda | Y |
| offers.price | special_price | Y |
| offers.image | media_gallery.url | N |
| offers.availability | stock_status | N |
| name | name | Y |
| image | media_gallery.url | Y |
| descripción | descripción | N |
| aggregateRating.reviewCount | review_count | N |
| aggregateRating.ratingValue | rating_summary | N |
| @id | id | N |

Esta asignación garantiza que el script JSON+LD se rellene dinámicamente en función de los datos del producto recuperados mediante consultas de GraphQL.

Para probar la estructura JSON+LD, puede usar la Prueba de [resultados enriquecidos - Consola de búsqueda de Google](https://search.google.com/test/rich-results/result?id=wtU3LVIEM8H7Aaf5qqK9qw). Esta herramienta proporciona comentarios detallados, incluido si los atributos necesarios están presentes o no, y ayuda a garantizar que los datos estructurados se implementen correctamente.
