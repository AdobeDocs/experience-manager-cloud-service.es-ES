---
title: Llamadas al editor universal
description: Obtenga información sobre los distintos tipos de llamadas que el Editor universal realiza a su aplicación para ayudarle en la depuración.
source-git-commit: 16f2922a3745f9eb72f7070c30134e5149eb78ce
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 1%

---


# Llamadas al editor universal {#calls}

Obtenga información sobre los distintos tipos de llamadas que el Editor universal realiza a su aplicación para ayudarle en la depuración.

{{universal-editor-status}}

## Información general {#overview}

El editor universal se comunica con la aplicación instrumentada a través de una serie de llamadas definidas. Esto es transparente para y no afecta a la experiencia del usuario final.

Sin embargo, para el desarrollador, comprender estas llamadas y lo que hacen puede ser útil al depurar la aplicación cuando se utiliza el Editor universal. Si ha instrumentado la aplicación y no se comporta como se esperaba, puede resultar útil abrir **Red** de las herramientas para desarrolladores del navegador e inspeccione las llamadas a medida que edita el contenido de la aplicación.

![Ejemplo de una llamada de detalles en la pestaña Red de las herramientas para desarrolladores del explorador](assets/calls-network-tab.png)

* El **Carga útil** de la llamada contiene detalles de lo que el editor está actualizando, incluida la identificación de qué actualizar y cómo actualizarlo.
* El **Respuesta** incluye detalles de qué ha actualizado exactamente el servicio de edición. Esto sirve para facilitar la actualización del contenido en el editor. En algunos casos, como un `move` Llamada de, se debe actualizar la página completa.

A continuación se muestra una lista de los tipos de llamadas que el editor universal realiza a su aplicación, así como cargas útiles y respuestas de ejemplo.

## Actualizar {#update}

Un `update` Esta llamada se produce cuando edita contenido en la aplicación mediante el Editor universal. El `update` persistirá en los cambios.

Su carga útil incluye detalles de lo que se debe escribir en el JCR.

* `itemid`: La ruta JCR que se va a actualizar
* `itemprop`: la propiedad JCR que se está actualizando
* `itemtype`: el tipo de valor JCR de la propiedad que se actualiza
* `value`: los datos actualizados

### Carga útil de muestra {#update-payload}

```json
{
  "op": "patch",
  "connections": {
    "aem": "aem:https://author-pXXXX-eYYYYY.adobeaemcloud.com"
  },
  "path": {
    "itemid": "urn:aem:/content/wknd/language-masters/en/jcr:content/root/container/carousel/item_1571954853062",
    "itemtype": "text",
    "itemprop": "jcr:title"
  },
  "value": "Tiny Toon Adventures"
}
```

### Respuesta de ejemplo {#update-response}

```json
{
  "updates": [
    {
      "itemid": "urn:aem:/content/wknd/language-masters/en/jcr:content/root/container/carousel/item_1571954853062",
      "itemprop": "jcr:title",
      "itemtype": "text"
    }
  ]
}
```

## Detalles {#details}

A `details` Esta llamada se produce al cargar la aplicación en el editor universal para recuperar el contenido de la aplicación.

Su carga útil incluye los datos que se van a procesar, así como detalles de lo que representan los datos (el esquema) para que se puedan procesar en el Editor universal.

* Para un componente, el editor universal solo recupera un componente `data` , ya que el esquema de los datos se define en la aplicación.
* Para los fragmentos de contenido, el editor universal también recupera un `schema` ya que el modelo de fragmento de contenido se define en el JCR.

### Carga útil de muestra {#details-payload}

```json
{
  "op": "patch",
  "connections": {
    "aem": "aem:https://author-pXXXX-eYYYYY.adobeaemcloud.com"
  },
  "path": {
    "itemid": "urn:aem:/content/wknd/language-masters/en/jcr:content/root/container/carousel/item_1571954853062",
    "itemtype": "component",
    "itemprop": ""
  }
}
```

### Respuesta de ejemplo {#details-response}

```json
{
  "data": {
    "jcr:primaryType": "nt:unstructured",
    "jcr:title": "Tiny Toon Adventures!",
    "fileReference": "/content/dam/wknd-shared/en/adventures/riverside-camping-australia/adobestock-216674449.jpeg",
    "cq:panelTitle": "WKND Adventures",
    "actionsEnabled": "true",
    "jcr:lastModifiedBy": "admin",
    "titleFromPage": "false",
    "jcr:description": "<p>With WKND Adventures, you don't just see the world you experinece it.</p>",
    "jcr:lastModified": "Wed Jan 03 2024 09:06:05 GMT+0100",
    "descriptionFromPage": "true",
    "sling:resourceType": "wknd/components/teaser",
    "textIsRich": "true",
    "cq:styleIds": [
      "1555543212672"
    ],
    "actions": {
      "jcr:primaryType": "nt:unstructured",
      "item0": {
        "jcr:primaryType": "nt:unstructured",
        "link": "/content/wknd/language-masters/en/adventures",
        "text": "View Trips"
      }
    }
  }
}
```

## Añadir {#add}

Un `add` Esta llamada se produce cuando se coloca un componente nuevo en la aplicación mediante el Editor universal.

Su carga útil incluye un `path` objeto que contiene dónde se debe añadir el contenido.

También incluye una `content` con objetos adicionales para detalles específicos del extremo del contenido que se va a almacenar [para cada complemento.](/help/implementing/universal-editor/architecture.md) AEM Por ejemplo, si la aplicación se basa en el contenido de los Magento y de la aplicación, la carga útil contendría un objeto de datos para cada sistema.

### Carga útil de muestra {#add-payload}

```json
{
  "op": "patch",
  "connections": {
    "aemconnection": "aem:https://author-pXXXX-eYYYYY.adobeaemcloud.com"
  },
  "path": {
    "container": {
      "itemid": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "itemtype": "container",
      "itemprop": ""
    }
  },
  "content": {
    "name": "text",
    "aem": {
      "page": {
        "resourceType": "wknd/components/text",
        "template": {
          "text": "Default Text"
        }
      }
    }
  }
}
```

### Respuesta de ejemplo {#add-response}

```json
{
  "updates": [
    {
      "itemid": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "itemtype": "container"
    }
  ]
}
```

## Mover {#move}

A `move` Esta llamada se produce cuando se mueve un componente dentro de la aplicación mediante el Editor universal.

Su carga útil incluye un `from` que define dónde estaba el componente y un `to` que define dónde se movió.

### Carga útil de muestra {#move-payload}

```json
{
  "op": "patch",
  "connections": {
    "aemconnection": "aem:https://author-pXXXX-eYYYYY.adobeaemcloud.com"
  },
  "from": {
    "container": {
      "itemid": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "itemtype": "container",
      "itemprop": ""
    },
    "component": {
      "itemid": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text_1068508321",
      "itemtype": "text",
      "itemprop": "text"
    }
  },
  "to": {
    "container": {
      "itemid": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "itemtype": "container",
      "itemprop": ""
    },
    "before": {
      "itemid": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text_2063168902",
      "itemtype": "text",
      "itemprop": "text"
    }
  }
}
```

### Respuesta de ejemplo {#move-response}

```json
{
  "updates": [
    {
      "itemid": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "itemtype": "container"
    }
  ]
}
```

## Quitar {#remove}

A `remove` Esta llamada se produce cuando se elimina un componente de la aplicación mediante el Editor universal.

Su carga útil incluye la ruta del objeto que se elimina.

### Carga útil de muestra {#remove-payload}

```json
{
  "op": "patch",
  "connections": {
    "aemconnection": "aem:https://author-pXXXX-eYYYYY.adobeaemcloud.com"
  },
  "path": {
    "component": {
      "itemid": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text_1068508321",
      "itemtype": "text",
      "itemprop": "text"
    },
    "container": {
      "itemid": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "itemtype": "container",
      "itemprop": ""
    }
  }
}
```

### Respuesta de ejemplo {#remove-response}

```json
{
  "updates": [
    {
      "itemid": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "itemprop": "",
      "itemtype": "container"
    }
  ]
}
```

## Parche {#patch}

A `patch` esta llamada se produce al actualizar contenido en un cuadro de diálogo dentro de la aplicación. Esto actualiza el contenido dentro de la página de la aplicación como un parche JSON al contenido existente.

Su carga útil incluye la ruta del contenido de la página, así como el parche JSON del cambio que se va a realizar.

### Carga útil de muestra {#patch-payload}

```json
{
  "op": "patch",
  "connections": {
    "aemconnection": "aem:https://author-pXXXX-eYYYYY.adobeaemcloud.com"
  },
  "path": {
    "itemid": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text_1540979193",
    "itemtype": "text",
    "itemprop": "text"
  },
  "patch": [
    {
      "op": "replace",
      "path": "/text",
      "value": "Still More WKND Adventures"
    }
  ]
}
```

### Respuesta de ejemplo {#patch-response}

```json
{
  "updates": [
    {
      "itemid": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text_1540979193"
    }
  ]
}
```

## Publicación {#publish}

A `publish` La llamada de se produce al hacer clic en **Publish** en el Editor universal para publicar el contenido que ha editado.

El editor universal repite el contenido y genera una lista de referencias que también deben publicarse.

### Carga útil de muestra {#publish-payload}

```json
{
  "op": "patch",
  "connections": {
    "aemconnection": "aem:https://author-pXXXX-eYYYYY.adobeaemcloud.com"
  },
  "references": [
    "urn:aemconnection:/content/dam/wknd-shared/en/magazine/arctic-surfing/aloha-spirits-in-northern-norway/jcr:content/data/master",
    "urn:aemconnection:/content/wknd/us/en/adventures/jcr:content/root/container/container/title",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/bali-surf-camp/bali-surf-camp/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/climbing-new-zealand/climbing-new-zealand/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/cycling-southern-utah/cycling-southern-utah/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/cycling-tuscany/cycling-tuscany/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/downhill-skiing-wyoming/downhill-skiing-wyoming/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/napa-wine-tasting/napa-wine-tasting/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/riverside-camping-australia/riverside-camping-australia/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/ski-touring-mont-blanc/ski-touring-mont-blanc/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/surf-camp-in-costa-rica/surf-camp-costa-rica/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/tahoe-skiing/tahoe-skiing/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/west-coast-cycling/west-coast-cycling/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/yosemite-backpacking/yosemite-backpacking/jcr:content/data/master",
    "urn:aemconnection:/content/wknd/us/en/newsletter/jcr:content/root/container/title",
    "urn:aemconnection:/content/wknd/us/en/newsletter/jcr:content/root/container/text",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/title",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/image",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/image_2123678383",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text_1668104604",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/image_229050934",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/image_275525847",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text_358189229",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text_2063168902",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text_1540979193"
  ]
}
```

### Respuesta de ejemplo {#publish-response}

```json
{
  "publishes": [
    "/content/dam/wknd-shared/en/magazine/arctic-surfing/aloha-spirits-in-northern-norway",
    "/content/wknd/us/en/adventures",
    "/content/dam/wknd-shared/en/adventures/bali-surf-camp/bali-surf-camp",
    "/content/dam/wknd-shared/en/adventures/climbing-new-zealand/climbing-new-zealand",
    "/content/dam/wknd-shared/en/adventures/cycling-southern-utah/cycling-southern-utah",
    "/content/dam/wknd-shared/en/adventures/cycling-tuscany/cycling-tuscany",
    "/content/dam/wknd-shared/en/adventures/downhill-skiing-wyoming/downhill-skiing-wyoming",
    "/content/dam/wknd-shared/en/adventures/napa-wine-tasting/napa-wine-tasting",
    "/content/dam/wknd-shared/en/adventures/riverside-camping-australia/riverside-camping-australia",
    "/content/dam/wknd-shared/en/adventures/ski-touring-mont-blanc/ski-touring-mont-blanc",
    "/content/dam/wknd-shared/en/adventures/surf-camp-in-costa-rica/surf-camp-costa-rica",
    "/content/dam/wknd-shared/en/adventures/tahoe-skiing/tahoe-skiing",
    "/content/dam/wknd-shared/en/adventures/west-coast-cycling/west-coast-cycling",
    "/content/dam/wknd-shared/en/adventures/yosemite-backpacking/yosemite-backpacking",
    "/content/wknd/us/en/newsletter",
    "/content/wknd/language-masters/en/universal-editor-container"
  ]
}
```
