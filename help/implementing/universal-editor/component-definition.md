---
title: Definición de componente
description: Comprenda en detalle el contrato JSON entre la definición del componente y el editor universal.
feature: Developing
role: Admin, Architect, Developer
exl-id: e1bb1a54-50c0-412a-a8fd-8167c6f47d2b
source-git-commit: b4e61ec6abcaf73119f8963d72317759b2bd7c76
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 96%

---

# Definición de componente {#component-definition}

Comprenda en detalle el contrato JSON entre la definición del componente y el editor universal.

## Información general {#overview}

El archivo `component-definition.json` define los componentes disponibles para los autores de contenido del proyecto. Este documento explica en detalle el propósito de este archivo y cómo lo utiliza el editor universal para presentar a los autores los componentes de creación de páginas.

>[!TIP]
>
>Para obtener información general del proceso de modelado de contenido, consulte el documento [Modelado de contenido para la creación WYSIWYG con proyectos de Edge Delivery Services.](https://www.aem.live/developer/component-model-definitions)

>[!TIP]
>
>No necesita crear su propio archivo de `component-definition.json` desde cero. La plantilla de proyecto que usa para [arrancar su proyecto](https://www.aem.live/developer/ue-tutorial) contiene un [archivo `component-definition.json` que funciona por completo](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-definition.json) y que puede adaptar a sus necesidades.

## Definición de componente de ejemplo {#example}

El siguiente es un `component-definition.json` de ejemplo completo pero simple.

```json
{
  "groups":[
    {
      "title":"General Components",
      "id":"general",
      "components":[
        {
          "title":"Text",
          "id":"text",
          "model": "text",
          "filter": "texts",
          "plugins":{
            "aem":{
              "page":{
                "resourceType":"wknd/components/text",
                "template":{
                  "text":"Default Text",
                  "name":"Text"
                }
              }
            },
            "aem65":{
              "page":{
                "resourceType":"wknd/components/text",
                "template":{
                  "text":"Default Text",
                  "name":"Text"
                }
              }
            }
          }
        }
      ]
    }
  ]
}
```

## `groups` {#groups}

`groups` define los grupos de componentes que el autor ve en el editor universal al hacer clic en el icono **Añadir** en el panel de propiedades del editor para [agregar un nuevo componente a una página](/help/sites-cloud/authoring/universal-editor/authoring.md#adding-components). Los grupos ayudan a organizar los componentes. Los grupos comunes pueden ser **Componentes generales** y **Componentes avanzados**.

* `title` define la descripción textual del grupo que se muestra en la IU del editor.
* `id` identifica de forma exclusiva el grupo.

## `components` {#components}

`components` define qué componentes pertenecen a un grupo.

* `title` define la descripción textual del componente que se muestra en la IU.
* `id` identifica de forma exclusiva el componente.
   * El [modelo de componente](/help/implementing/universal-editor/field-types.md#model-structure) del mismo `id` define los campos del componente.
   * Como es único, se puede usar, por ejemplo, en una [definición de filtro](/help/implementing/universal-editor/filtering.md) para determinar qué componentes se pueden añadir a un contenedor.
* `model` define qué [modelo](/help/implementing/universal-editor/field-types.md#model-structure) se usa con el componente.
   * De este modo, el modelo se mantiene de forma centralizada en la definición del componente y no necesita [especificarse en la instrumentación.](/help/implementing/universal-editor/field-types.md#instrumentation)
   * Esto le permite mover componentes entre contenedores.
* `filter` define qué [filtro](/help/implementing/universal-editor/filtering.md) debe usarse con el componente.

## `plugins` {#plugins}

`plugins` define qué complemento es responsable de mantener el componente. Los complementos comunes incluyen los siguientes:

* `aem` para [AEM as a Cloud Service.](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service)
* `aem65` para [AEM 6.5.](https://experienceleague.adobe.com/es/docs/experience-manager-65) y [AEM 6.5 LTS](https://experienceleague.adobe.com/es/docs/experience-manager-65-lts)
* `xwalk` para [crear con AEM Sites para Edge Delivery Services.](https://www.aem.live/developer/ue-tutorial)

## `page` o `cf` {#page-cf}

Una vez definido `plugin`, debe indicar si está relacionado con la página o con el fragmento.

* `page` indica que el componente es contenido en la página actual.
* `cf` indica que el componente está relacionado con contenido de un [fragmento de contenido](/help/assets/content-fragments/content-fragments.md).

### `page` {#page}

Si el componente es contenido en la página, puede proporcionar la siguiente información.

* `resourceType` define el [Sling](/help/implementing/developing/introduction/sling-cheatsheet.md) `resourceType` utilizado para procesar el componente.
* `template` define los valores o claves opcionales que se escribirán de manera automática en el componente recién creado y define qué filtro o modelo se debe aplicar al componente.
   * Es útil para texto explicativo, de muestra o de marcador de posición.

#### `template` {#template}

Si se proporcionan pares de clave/valor opcionales, `template` puede escribirlos de manera automática en el nuevo componente. Además, también se pueden especificar los siguientes valores opcionales.

### `cf` {#cf}

Si el componente está relacionado con el contenido de un fragmento de contenido, puede proveer la siguiente información.

* `name` define un nombre opcional guardado en el JCR para el componente recién creado.
   * Solo es informativo y, por lo general, no se muestra en la IU como `title`.
* `cfModel` define el modelo de [fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md) para el componente recién creado.
* `cfFolder` define en qué carpeta se creará el fragmento de contenido.
* `title` define el título del nuevo fragmento de contenido.
* `description` define una descripción del nuevo fragmento de contenido.
* `template` define los valores o claves opcionales que se escribirán de forma automática en el fragmento de contenido recién creado.
   * Es útil para texto explicativo, de muestra o de marcador de posición.

### `cf` puede estar implícito {#cf-implied}

Si la página está [instrumentada](/help/implementing/universal-editor/getting-started.md#instrument-page) para que apunte a un campo de referencia, `cf` se supondrá.

```html
<div data-aue-resource="urn:aem:/content" data-aue-type="container" data-aue-prop="field"></div>
```

En tal caso, se supone `cf`, ya que `data-aue-prop` señala a un campo de referencia. Sin `data-aue-prop`, el editor universal supondrá `page`, porque en tal caso los componentes no están vinculados a través de un campo de referencia.

```html
<div data-aue-resource="urn:aem:/content" data-aue-type="container"></div>
```

Los componentes son simples subnodos debajo del recurso.
