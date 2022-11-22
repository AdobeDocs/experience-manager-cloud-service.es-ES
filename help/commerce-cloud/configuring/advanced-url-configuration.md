---
title: Configuraciones de URL avanzadas
description: Obtenga información sobre cómo personalizar las direcciones URL para páginas de productos y categorías. Esto permite que las implementaciones optimicen las direcciones URL de los motores de búsqueda y promuevan la detección.
sub-product: Commerce
version: Cloud Service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
exl-id: 314494c4-21a9-4494-9ecb-498c766cfde7,363cb465-c50a-422f-b149-b3f41c2ebc0f
source-git-commit: fbd2fdcb61bcbae49f07c3da26b14d56d50b1cab
workflow-type: tm+mt
source-wordcount: '2214'
ht-degree: 16%

---

# Configuraciones de URL avanzadas {#url}

>[!NOTE]
>
> La optimización de los motores de búsqueda (SEO) se ha convertido en una preocupación clave para muchos expertos en marketing. En consecuencia, es necesario abordar las preocupaciones de SEO en muchos proyectos de Adobe Experience Manager (AEM) as a Cloud Service. Lea [Prácticas recomendadas para la administración de direcciones URL y SEO](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/seo-and-url-management.html) para obtener más información.

Los [componentes principales del CIF de AEM](https://github.com/adobe/aem-core-cif-components) proporcionan configuraciones avanzadas para personalizar las direcciones URL de las páginas de productos y categorías. Muchas implementaciones personalizan estas direcciones URL con fines de optimización de los motores de búsqueda (SEO). En el siguiente vídeo se explica cómo configurar el `UrlProvider` servicio y las funciones de las [Asignaciones de Mapping](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) para personalizar las direcciones URL de las páginas de productos y categorías.

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## Configuración {#configuration}

Para configurar la variable `UrlProvider` según los requisitos de SEO y las necesidades, un proyecto debe proporcionar una configuración OSGI para el _Configuración del proveedor de URL del CIF_.

>[!NOTE]
>
> Desde la versión 2.0.0 de los componentes principales del CIF de AEM, la configuración del proveedor de URL solo proporciona formatos de URL predefinidos, en lugar de los formatos configurables de texto libre conocidos en las versiones 1.x. Además, el uso de selectores para pasar datos en direcciones URL se ha sustituido por sufijos.

### Formato de la dirección URL de la página del producto {#product}

Esto configura las direcciones URL de las páginas de producto y admite las siguientes opciones:

* `{{page}}.html/{{sku}}.html#{{variant_sku}}` (predeterminada)
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`

En el caso del [Tienda de referencia de Venia](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` se sustituye por `/content/venia/us/en/products/product-page`
* `{{sku}}` será reemplazado por el sku del producto, por ejemplo, `VP09`
* `{{url_key}}` será reemplazado por el `url_key` propiedad, por ejemplo, `lenora-crochet-shorts`
* `{{url_path}}` será reemplazado por el `url_path`, por ejemplo, `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` se reemplazará por la variante seleccionada actualmente, por ejemplo, `VP09-KH-S`

Dado que la variable `url_path` En desuso, los formatos de URL de producto predefinidos utilizan la variable `url_rewrites` y elija el que tenga la mayor cantidad de segmentos de ruta como alternativa si la variable `url_path` no está disponible.

Con los datos del ejemplo anterior, la dirección URL de una variante de producto con formato de URL predeterminado tendrá el mismo aspecto `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`.

### Formato de dirección URL de la página de categoría {#product-list}

Esto configura las direcciones URL de las páginas de categorías o listas de productos y admite las siguientes opciones:

* `{{page}}.html/{{url_path}}.html` (predeterminada)
* `{{page}}.html/{{url_key}}.html`

En el caso del [Tienda de referencia de Venia](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` se sustituye por `/content/venia/us/en/products/category-page`
* `{{url_key}}` se reemplazará por el `url_key` property
* `{{url_path}}` se reemplazará por el `url_path`

Con los datos del ejemplo anterior, la dirección URL de una página de categoría con formato de dirección URL predeterminado será como `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`.

>[!NOTE]
> 
> La variable `url_path` es una concatenación del `url_keys` de los antepasados de un producto o categoría y del producto o categoría `url_key` separado por `/` barra diagonal. Cada `url_key` se considera único dentro de un almacén determinado.

### Configuración específica del almacén {#store-specific-urlformats}

Los formatos de URL de categoría y página de producto de todo el sistema establecidos por la variable _Configuración del proveedor de URL del CIF_ se puede cambiar para cada tienda.

En la configuración del CIF, un editor puede seleccionar un formato de URL de página de producto o categoría alternativo. Si no hay nada seleccionado, la implementación se volverá a utilizar en la configuración de todo el sistema.

Cambiar el formato de la URL de un sitio web activo puede tener un impacto negativo en el tráfico orgánico del sitio. Consulte la [Prácticas recomendadas](#best-practices) a continuación y planifique cuidadosamente el cambio del formato de la URL con antelación.

![Formatos de URL en la configuración del CIF](assets/store-specific-url-formats.png)

>[!NOTE]
>
> La configuración específica del almacén de los formatos URL requiere [Componentes principales de CIF 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) y la última versión del complemento Contenido y comercio de Adobe Experience Manager.

## Direcciones URL de página de producto según la categoría {#context-aware-pdps}

Dado que es posible codificar la información de categoría en una URL de producto, los productos que se encuentran en varias categorías también pueden abordarse con varias URL de producto.

Los formatos de URL predeterminados seleccionarán una de las posibles alternativas utilizando el siguiente esquema:

* si la variable `url_path` está definido por el backend de comercio electrónico que lo utiliza (obsoleto)
* de la variable `url_rewrites` use las direcciones URL que terminen con el `url_key` como alternativas
* para estas alternativas use el que tenga la mayor cantidad de segmentos de ruta
* si hay varios, tome el primero en el orden dado por el servidor de comercio electrónico

Este esquema seleccionará `url_path` con la mayoría de los antecesores, basándose en el supuesto de que una categoría secundaria es más específica que su categoría principal. El `url_path` se considera _canónico_ y siempre se utilizarán como vínculo canónico en páginas de productos o en el mapa del sitio del producto.

Sin embargo, cuando un comprador navega de una página de categoría a una página de producto, o de una página de producto a otra página de producto relacionada en la misma categoría, vale la pena mantener el contexto de categoría actual. En este caso, la variable `url_path` La selección debería preferir alternativas, que estén dentro del contexto de categoría actual sobre el _canónico_ selección descrita anteriormente.

Esta función debe habilitarse en la variable _Configuración del proveedor de URL del CIF_. Si se habilita, la selección obtendrá una puntuación mayor en las alternativas, cuando

* coinciden con partes de una categoría determinada `url_path` desde el principio (coincidencia de prefijos confusos)
* o coinciden con el de una categoría determinada `url_key` en cualquier parte (coincidencia parcial exacta)

Por ejemplo, considere la respuesta para un [consulta de productos](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) más abajo. Dado que el usuario se encuentra en la página de categoría &quot;Nuevos productos / Novedades en verano de 2022&quot; y la tienda utiliza el formato de URL de página de categoría predeterminado, la alternativa &quot;new-products/new-in-summer-2022/gold-cirque-earrings.html&quot; coincidiría con dos segmentos de ruta del contexto desde el principio: &quot;nuevos productos&quot; y &quot;nuevos en verano de 2022&quot;. Si la tienda utiliza un formato de URL de página de categoría que solo contenga la categoría `url_key`, la misma alternativa se seguiría seleccionando ya que coincide con el de `url_key` en cualquier parte. En ambos casos, la dirección URL de la página del producto se crearía para &quot;new-products/new-in-summer-2022/gold-cirque-earrings.html&quot; `url_path`.

```
{
  "data": {
    "products": {
      "items": [
        {
          "sku": "VA18-GO-NA",
          "url_key": "gold-cirque-earrings",
          "url_rewrites": [
            {
              "url": "gold-cirque-earrings.html"
            },
            {
              "url": "venia-accessories/gold-cirque-earrings.html"
            },
            {
              "url": "venia-accessories/venia-jewelry/gold-cirque-earrings.html"
            },
            {
              "url": "new-products/gold-cirque-earrings.html"
            },
            {
              "url": "new-products/new-in-summer-2022/gold-cirque-earrings.html"
            }
          ]
        }
      ]
    }
  }
}
```

>[!NOTE]
>
> Se requieren direcciones URL de producto según la categoría [Componentes principales de CIF 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) o posterior.

## Categoría específica y páginas de producto {#specific-pages}

Es posible crear [varias páginas de productos y categorías](../authoring/multi-template-usage.md) solo para un subconjunto específico de categorías o productos de un catálogo.

### Criterios de selección {#specific-pages-selection}

La selección de una página de categoría específica es directa, en función del `url_path` o `url_key`. Las subcategorías coincidentes solo se admiten en formatos de URL que contengan la categoría completa `url_path`. De lo contrario, solo una coincidencia exacta de la variable `url_key` es posible.

Las páginas de producto específicas se seleccionan según el SKU o la categoría del producto. El posterior requiere que parte de la información de la categoría se codifique en la dirección URL del producto. Esto solo está disponible para algunos de los formatos de URL predeterminados. Consulte la siguiente tabla para ver una comparación del formato URL que admite la selección de páginas específica por sku o categoría.


| Formato de URL | por sku | por categoría |
| ----------------------------------------------------- | ------ | ---------------- |
| `{{page}}.html/{{url_key}}.html` | nº | nº |
| `{{page}}.html/{{category}}/{{url_key}}.html` | nº | coincidencia exacta solamente |
| `{{page}}.html/{{url_path}}.html` | nº | yes |
| `{{page}}.html/{{sku}}.html` | yes | nº |
| `{{page}}.html/{{sku}}/{{url_key}}.html` | yes | nº |
| `{{page}}.html/{{sku}}/{{category}}/{{url_key}}.html` | yes | coincidencia exacta solamente |
| `{{page}}.html/{{sku}}/{{url_path}}.html` | yes | yes |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
> La selección de páginas de productos específicas por categoría requiere [Componentes principales de CIF 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) o posterior.

### Vinculación profunda {#specific-pages-deep-linking}

La variable `UrlProvider` está preconfigurado para generar vínculos profundos a páginas de productos y categorías específicas en instancias de nivel de autor. Esto resulta útil para los editores que exploran un sitio con el modo de vista previa, navegan a una página de producto o categoría específica y vuelven al modo de edición para editar la página.

Por otro lado, en las instancias de nivel de publicación, las URL de las páginas de catálogo deben mantenerse estables para no perder ganancias en las clasificaciones de los motores de búsqueda, por ejemplo. Debido a que las instancias de nivel de publicación no procesarán vínculos profundos a páginas de catálogo específicas de forma predeterminada. Para cambiar este comportamiento, la variable _Estrategia de página específica del proveedor de URL del CIF_ se puede configurar para que siempre genere direcciones URL de página específicas.

### Varias páginas del catálogo {#multiple-product-pages}

Cuando los editores deseen tener control total de la navegación de nivel superior de un sitio, puede que no se desee utilizar una sola página de catálogo para representar las categorías de nivel superior de un catálogo. En su lugar, los editores pueden crear varias páginas de catálogo, una para cada categoría del catálogo que desean incluir en la navegación de nivel superior.

Para ese caso de uso, cada una de las páginas del catálogo puede tener una referencia a una página de producto y categoría específica para la categoría configurada para la página del catálogo. La variable `UrlProvider` se utilizarán para crear vínculos para las páginas y categorías de la categoría configurada. Sin embargo, por motivos de rendimiento solo se tienen en cuenta los elementos secundarios de página de catálogo directo de la raíz de navegación/página de aterrizaje de un sitio.

Se recomienda que las páginas de producto y categoría de una página de catálogo descendientes de esa página de catálogo; de lo contrario, es posible que componentes como Navegación o Ruta de navegación no funcionen correctamente.

>[!NOTE]
>
> La compatibilidad completa con varias páginas de catálogo requiere [Componentes principales de CIF 2.10.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.10.0) o posterior.

## Personalizaciones {#customization}

### Formatos de URL personalizados {#custom-url-format}

Para proporcionar un formato de URL personalizado, un proyecto puede implementar o bien la variable [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) o [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) y registre la implementación como servicio OSGI. Estas implementaciones, si están disponibles, reemplazarán el formato configurado y predefinido. Si hay varias implementaciones registradas, el que tenga la clasificación de servicio más alta reemplaza a las que tengan la clasificación de servicio más baja.

Las implementaciones de formato de URL personalizado deben implementar un par de métodos para generar una URL a partir de parámetros determinados y para analizar una URL y devolver los mismos parámetros respectivamente.

### Combinación con asignaciones de Sling {#sling-mapping}

Además del `UrlProvider`, también es posible configurar las [asignaciones de Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) para reescribir y procesar direcciones URL. El tipo de archivo del proyecto AEM también proporciona [una configuración de ejemplo](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) para configurar algunas asignaciones de Sling para el puerto 4503 (publicación) y 80 (Dispatcher).

### Combinación con AEM Dispatcher {#dispatcher}

Las reescrituras de URL también se pueden lograr usando AEM servidor HTTP de Dispatcher con `mod_rewrite` módulo. El [tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype) proporciona una referencia a la configuración de AEM Dispatcher que ya incluye las [reglas de reescritura](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) básicas para el tamaño generado.

## Prácticas recomendadas {#best-practices}

### Elija el mejor formato de URL {#choose-url-format}

Como se mencionó antes de seleccionar uno de los formatos predeterminados disponibles, o incluso implementar un formato personalizado, depende en gran medida de las necesidades y requisitos de una tienda. Las siguientes sugerencias pueden ayudar a tomar una decisión educada.

_**Utilice un formato de URL de página de producto que contenga el SKU.**_

Los componentes principales del CIF utilizan el sku como identificador principal en todos los componentes. Si el formato de la dirección URL de la página del producto no contiene el sku, se necesita una consulta de GraphQL para resolverlo. Esto puede afectar al tiempo hasta el primer byte. Además, puede ser deseable que los compradores puedan encontrar productos en sku usando motores de búsqueda.

_**Utilice un formato de URL de página de producto que contenga el contexto de categoría.**_

Algunas funciones del proveedor de URL del CIF solo están disponibles cuando se utilizan formatos de URL de producto, que codifican el contexto de la categoría, como la categoría `url_key` o la categoría `url_path`. Aunque estas funciones no sean necesarias para una nueva tienda, el uso de uno de estos formatos de URL al principio ayuda a reducir los esfuerzos de migración en el futuro.

_**Equilibrio entre la longitud de la dirección URL y la información codificada.**_

Según el tamaño del catálogo, en particular el tamaño y la profundidad del árbol de categorías, puede que no sea razonable codificar la totalidad de `url_path` de categorías en la dirección URL. En ese caso, la longitud de la dirección URL se podría reducir incluyendo solo el `url_key` en su lugar. Esto admitirá la mayoría de las funciones disponibles al utilizar la categoría `url_path`.

Además, utilice [Asignaciones de Sling](#sling-mapping) para combinar el sku con el producto `url_key`. En la mayoría de los sistemas de comercio electrónico, el sku sigue un formato particular y separa el sku del `url_key` para las solicitudes entrantes debería ser fácilmente posible. Con esto en mente, debería ser posible reescribir la dirección URL de una página de producto a `/p/{{category}}/{{sku}}-{{url_key}}.html`y una dirección URL de categoría a `/c/{{url_key}}.html` respectivamente. La variable `/p` y `/c` siguen siendo necesarios para distinguir las páginas de productos y categorías de otras páginas de contenido.

### Migración a un nuevo formato de URL {#migrate-url-formats}

Muchos de los formatos de URL predeterminados son de alguna manera compatibles entre sí, lo que significa que las URL formateadas por uno pueden ser analizadas por otro. Esto ayuda a migrar entre formatos de URL.

Por otro lado, los motores de búsqueda necesitarán algún tiempo para volver a rastrear todas las páginas del catálogo con el nuevo formato de URL. Para admitir este proceso y también para mejorar la experiencia del usuario final, se recomienda proporcionar redirecciones que reenvíen al usuario de las direcciones URL antiguas a las nuevas.

Un enfoque podría ser conectar un entorno de ensayo al back-end de comercio electrónico de producción y configurarlo para que utilice el nuevo formato de URL. Después, obtenga la variable [mapa del sitio del producto generado por el generador del mapa del sitio de los productos CIF](../../overview/seo-and-url-management.md) para el entorno de ensayo y producción, y utilícelos para crear un [Mapa de reescritura httpd de Apache](https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html). Este mapa de reescritura se puede implementar en el despachante junto con el despliegue del nuevo formato de URL.

## Ejemplo {#example}

El proyecto [Tienda de referencia de Venia](https://github.com/adobe/aem-cif-guides-venia) incluye configuraciones de muestra para demostrar el uso de direcciones URL personalizadas para páginas de productos y categorías. Esto permite que cada proyecto configure patrones de URL individuales para páginas de productos y categorías según sus necesidades de SEO. Se utiliza una combinación de asignaciones de CIF `UrlProvider` y de Sling como se describe anteriormente.

>[!NOTE]
>
>Esta configuración debe ajustarse con el dominio externo utilizado por el proyecto. Las asignaciones de Sling funcionan según el nombre de host y el dominio. Por lo tanto, esta configuración está deshabilitada de forma predeterminada y debe habilitarse antes de la implementación. Para ello, cambie el nombre de la `hostname.adobeaemcloud.com` carpeta Asignaciones de Sling en `ui.content/src/main/content/jcr_root/etc/map.publish/https` función del nombre de dominio utilizado y habilite esta configuración añadiendo `resource.resolver.map.location="/etc/map.publish"` a la `JcrResourceResolver` configuración del proyecto.

## Recursos adicionales {#additional}

* [Tienda de referencia de Venia](https://github.com/adobe/aem-cif-guides-venia)
* [Asignación de recursos de AEM](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Asignaciones de Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
