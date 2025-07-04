---
title: Integración del Selector de recursos con la API abierta de Dynamic Media
description: Integre el selector de recursos con varias aplicaciones de Adobe, que no sean de Adobe y de terceros.
role: Admin, User
exl-id: b01097f3-982f-4b2d-85e5-92efabe7094d
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 3%

---

# Integración de Dynamic Media con funciones de OpenAPI {#integrate-asset-selector-dynamic-media-open-apis}

El Selector de recursos le permite integrarse utilizando varias aplicaciones de Adobe para permitir que funcionen juntas sin problemas.

## Requisitos previos {#prereqs-polaris}

Utilice los siguientes requisitos previos si integra el Selector de recursos con Dynamic Media con las capacidades de OpenAPI:

* [Métodos de comunicación](/help/assets/overview-asset-selector.md#prereqs)
* Para acceder a Dynamic Media con las funciones de OpenAPI, debe tener licencias para:
   * Repositorio de Assets (por ejemplo, Experience Manager Assets as a Cloud Service).
   * AEM Dynamic Media.
* Solo hay [recursos aprobados](/help/assets/approve-assets.md) disponibles para usar, lo que garantiza la coherencia de la marca.

## Integración de Dynamic Media con funciones de OpenAPI {#adobe-app-integration-polaris}

La integración del Selector de recursos con el proceso OpenAPI de Dynamic Media implica varios pasos, entre los que se incluye la creación de una URL de Dynamic Media personalizada o una URL de Dynamic Media lista para elegir, etc.

### Integre el Selector de recursos para Dynamic Media con las funciones de OpenAPI {#integrate-dynamic-media}

Las propiedades `rootPath` y `path` no deben formar parte de Dynamic Media con capacidades de OpenAPI. En su lugar, puede configurar la propiedad `aemTierType`. A continuación se muestra la sintaxis de la configuración:

```
aemTierType:[1: "delivery"]
```

Esta configuración le permite ver todos los recursos aprobados sin carpetas o como una estructura plana. Para obtener más información, vaya a la propiedad `aemTierType` en [Propiedades del selector de recursos](/help/assets/asset-selector-properties.md).


### Creación de una URL de envío dinámico a partir de recursos aprobados {#create-dynamic-media-url}

Una vez configurado el Selector de recursos, se utiliza un esquema de objetos para crear una URL de envío dinámico a partir de los recursos seleccionados.
Por ejemplo, un esquema de un objeto de una matriz de objetos que se recibe al seleccionar un recurso:

```
{
"dc:format": "image/jpeg",
"repo:assetId": "urn:aaid:aem:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
"repo:name": "image-7.jpg",
"repo:repositoryId": "delivery-pxxxx-exxxxxx.adobe.com",
...
}
```

La función `handleSelection` que actúa como objeto JSON lleva todos los recursos seleccionados. Por ejemplo, `JsonObj`. La URL de envío dinámico se crea combinando los siguientes operadores:

| Objeto | JSON |
|---|---|
| Host | `assetJsonObj["repo:repositoryId"]` |
| Raíz API | `/adobe/assets` |
| asset-id | `assetJsonObj["repo:assetId"]` |
| seo-name | `assetJsonObj["repo:name"].split(".").slice(0,-1).join(".")` |
| formato | `.jpg` |

#### Especificación de API de entrega de recursos aprobados {#approved-assets-delivery-api-specification}

Formato de URL:
`https://<delivery-api-host>/adobe/assets/<asset-id>/as/<seo-name>.<format>?<image-modification-query-parameters>`

Donde,

* El host es `https://delivery-pxxxxx-exxxxxx.adobe.com`
* La raíz de API es `"/adobe/assets"`
* `<asset-id>` es el identificador del recurso
* `as` es la parte constante de la especificación de API abierta que indica a qué se puede hacer referencia el recurso
* `<seo-name>` es el nombre de un recurso
* `<format>` es el formato de salida
* `<image modification query parameters>` como compatible con la especificación de API de entrega de recursos aprobados

#### Recursos aprobados API de entrega de representación original {#approved-assets-delivery-api}

La dirección URL de envío dinámico tiene la siguiente sintaxis:
`https://<delivery-api-host>/adobe/assets/<asset-id>/original/as/<seo-name>`, donde,

* El host es `https://delivery-pxxxxx-exxxxxx.adobe.com`
* La raíz de la API para la entrega de la representación original es `"/adobe/assets"`
* `<asset-id>` es el identificador de recurso
* `/original/as` es la parte constante de la especificación de API abierta que indica a qué se puede hacer referencia en la representación original
* `<seo-name>` es el nombre del recurso que puede tener o no una extensión

### Listo para elegir la URL de envío dinámico {#ready-to-pick-dynamic-delivery-url}

La función `handleSelection` que actúa como objeto JSON lleva todos los recursos seleccionados. Por ejemplo, `JsonObj`. La URL de envío dinámico se crea combinando los siguientes operadores:

| Objeto | JSON |
|---|---|
| Host | `assetJsonObj["repo:repositoryId"]` |
| Raíz API | `/adobe/assets` |
| asset-id | `assetJsonObj["repo:assetId"]` |
| seo-name | `assetJsonObj["repo:name"]` |

A continuación se muestran las dos formas de atravesar el objeto JSON:

![URL de envío dinámico](assets/dynamic-delivery-url.png)

* **Miniatura:** Las miniaturas pueden ser imágenes y recursos como PDF, vídeo, imágenes, etc. Sin embargo, puede utilizar los atributos de altura y anchura de la miniatura de un recurso como representación de envío dinámico.
Se puede utilizar el siguiente conjunto de representaciones para los recursos de tipo PDF:
Una vez que se selecciona un pdf en la barra de tareas, el contexto de selección ofrece la siguiente información. A continuación se muestra la forma de atravesar el objeto JSON:

  <!--![Thumbnail dynamic delivery url](image-1.png)-->

  Puede hacer referencia a `selection[0].....selection[4]` para la matriz de vínculos de representación desde la captura de pantalla anterior. Por ejemplo, las propiedades clave de una de las representaciones de miniaturas incluyen:

  ```
  { 
      "height": 319, 
      "width": 319, 
      "href": "https://delivery-pxxxxx-exxxxx.adobeaemcloud.com/adobe/assets/urn:aaid:aem:8560f3a1-d9cf-429d-a8b8-d81084a42d41/as/algorithm design.jpg?width=319&height=319", 
      "type": "image/webp" 
  } 
  ```

En la captura de pantalla anterior, la dirección URL de envío de la representación original de PDF debe incorporarse en la experiencia de destino si se requiere PDF y no su miniatura. Por ejemplo, `https://delivery-pxxxxx-exxxxx.adobeaemcloud.com/adobe/assets/urn:aaid:aem:8560f3a1-d9cf-429d-a8b8-d81084a42d41/original/as/algorithm design.pdf`

* **Vídeo:** Puede usar la URL del reproductor de vídeo para los recursos de tipo de vídeo que usan un iFrame incrustado. Puede utilizar las siguientes representaciones de matrices en la experiencia de Target:
  <!--![Video dynamic delivery url](image.png)-->

  ```
  { 
      "height": 319, 
      "width": 319, 
      "href": "https://delivery-pxxxxx-exxxxx.adobeaemcloud.com/adobe/assets/urn:aaid:aem:2fdef732-a452-45a8-b58b-09df1a5173cd/as/DragDrop.2.jpg?width=319&height=319", 
      "type": "image/webp" 
  } 
  ```

  Puede hacer referencia a `selection[0].....selection[4]` para la matriz de vínculos de representación desde la captura de pantalla anterior. Por ejemplo, las propiedades clave de una de las representaciones de miniaturas incluyen:

  El fragmento de código de la captura de pantalla anterior es un ejemplo de un recurso de vídeo. Incluye la matriz de vínculos de representaciones. El `selection[5]` del extracto es el ejemplo de una miniatura de imagen que puede utilizarse como marcador de posición de una miniatura de vídeo en la experiencia de destino. `selection[5]` en la matriz de representaciones es para el reproductor de vídeo. Esto sirve un HTML y se puede establecer como `src` del iframe. Admite flujo de velocidad de bits adaptable, que es una entrega del vídeo optimizada para la web.

  En el ejemplo anterior, la dirección URL del reproductor de vídeo es `https://delivery-pxxxxx-exxxxx.adobeaemcloud.com/adobe/assets/urn:aaid:aem:2fdef732-a452-45a8-b58b-09df1a5173cd/play`

### Configuración de filtros personalizados {#configure-custom-filters-dynamic-media-open-api}

El Selector de recursos para Dynamic Media con funciones de OpenAPI le permite configurar propiedades personalizadas y los filtros basados en ellas. La propiedad `filterSchema` se usa para configurar dichas propiedades. La personalización puede exponerse como `metadata.<metadata bucket>.<property name>.`, en función de la cual se pueden configurar los filtros, donde,

* `metadata` es la información de un recurso
* `embedded` es el parámetro estático utilizado para la configuración, y
* `<propertyname>` es el nombre de filtro que está configurando

Para la configuración, las propiedades definidas en el nivel `jcr:content/metadata/` se exponen como `metadata.<metadata bucket>.<property name>.` para los filtros que desea configurar.

Por ejemplo, en el Selector de recursos para Dynamic Media con capacidades OpenAPI, una propiedad de `asset jcr:content/metadata/client_name:market` se convierte en `metadata.embedded.client_name:market` para la configuración de filtros.

Para obtener el nombre, se debe realizar una actividad única. Realice una llamada a la API de búsqueda para el recurso y obtenga el nombre de la propiedad (el contenedor, en esencia).

### Interfaz de usuario del Selector de recursos para Dynamic Media con funciones de OpenAPI {#interface-dynamic-media-open-api}

Después de la integración con el Selector de recursos de Micro-FrontEnd de Adobe, puede ver la estructura de recursos solamente de todos los recursos aprobados disponibles en el repositorio de recursos de Experience Manager.

![Dynamic Media con la IU de capacidades de OpenAPI](assets/polaris-ui.png)

* **A**: ocultar/mostrar panel
* **B**: Assets
* **C**: Ordenando
* **D**: Filtros
* **E**: Barra de búsqueda
* **F**: orden ascendente o descendente
* **G**: Cancelar Selección
* **H**: seleccione uno o varios recursos

>[!NOTE]
>
>Las carpetas solo se admiten cuando se conecta al repositorio de creación y no a Dynamic Media con el repositorio de OpenAPI.

>[!MORELIKETHIS]
>
>* [Integrar el Selector de recursos con varias aplicaciones](/help/assets/integrate-asset-selector.md)
>* [Propiedades del Selector de recursos](/help/assets/asset-selector-properties.md)
>* [Personalizaciones del Selector de recursos](/help/assets/asset-selector-customization.md)
