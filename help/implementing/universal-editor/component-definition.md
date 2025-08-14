---
title: Definición de componente
description: Comprenda en detalle el contrato JSON entre la definición del componente y el Editor universal.
feature: Developing
role: Admin, Architect, Developer
exl-id: e1bb1a54-50c0-412a-a8fd-8167c6f47d2b
source-git-commit: bb149cd43158bfd1ceb43b04cc536c8c8291f968
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 2%

---

# Definición de componente {#component-definition}

Comprenda en detalle el contrato JSON entre la definición del componente y el Editor universal.

## Información general {#overview}

El archivo `component-definition.json` define los componentes disponibles para los autores de contenido del proyecto. Este documento explica en detalle el propósito de este archivo y cómo lo utiliza el Editor universal para presentar a los autores los componentes de creación de páginas.

>[!TIP]
>
>Para obtener una descripción general del proceso de modelado de contenido, consulte el documento [Modelado de contenido para la creación de WYSIWYG con proyectos de Edge Delivery Services.](https://www.aem.live/developer/component-model-definitions)

>[!TIP]
>
>No necesita crear su propio archivo de `component-definition.json` desde cero. La plantilla de proyecto que usas para [arrancar tu proyecto](https://www.aem.live/developer/ue-tutorial) contiene un [archivo `component-definition.json` que funciona por completo](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-definition.json) y que puedes adaptar a tus necesidades.

## Ejemplo de definición de componente {#example}

El siguiente es un ejemplo completo, pero simple `component-definition.json`.

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

`groups` define los grupos de componentes que el autor ve en el editor universal al hacer clic en el icono **Agregar** en el panel de propiedades del editor para [agregar un nuevo componente a una página](/help/sites-cloud/authoring/universal-editor/authoring.md#adding-components). Los grupos ayudan a organizar los componentes. Los grupos comunes pueden ser **Componentes generales** y **Componentes avanzados**.

* `title` define la descripción textual del grupo que se muestra en la interfaz de usuario del editor.
* `id` identifica de forma exclusiva el grupo.

## `components` {#components}

`components` define qué componentes pertenecen a un grupo.

* `title` define la descripción textual del componente que se muestra en la interfaz de usuario.
* `id` identifica de forma exclusiva el componente.
   * El [modelo de componente](/help/implementing/universal-editor/field-types.md#model-structure) del mismo `id` define los campos del componente.
   * Como es único, se puede usar, por ejemplo, en una [definición de filtro](/help/implementing/universal-editor/filtering.md) para determinar qué componentes se pueden agregar a un contenedor.
* `model` define qué [modelo](/help/implementing/universal-editor/field-types.md#model-structure) se usa con el componente.
   * Por lo tanto, el modelo se mantiene de forma centralizada en la definición del componente y no es necesario [especificar la instrumentación.](/help/implementing/universal-editor/field-types.md#instrumentation)
   * Esto le permite mover componentes entre contenedores.
* `filter` define qué [filtro](/help/implementing/universal-editor/filtering.md) debe usarse con el componente.

## `plugins` {#plugins}

`plugins` define qué complemento es responsable de mantener el componente. Los complementos comunes incluyen:

* `aem` para AEM as a Cloud Service.
* `aem5` para AEM 6.5.
* `xwalk` para la creación de AEM as a Cloud Service WYSIWYG.

## `page` o `cf` {#page-cf}

Una vez definido `plugin`, debe indicar si está relacionado con la página o con el fragmento.

* `page` indica que el componente es contenido en la página actual.
* `cf` indica que el componente está relacionado con contenido de un [fragmento de contenido](/help/assets/content-fragments/content-fragments.md).

### `page` {#page}

Si el componente tiene contenido en la página, puede proporcionar la siguiente información.

* `resourceType` define [Sling](/help/implementing/developing/introduction/sling-cheatsheet.md) `resourceType` utilizado para procesar el componente.
* `template` define los valores o claves opcionales que se escribirán automáticamente en el componente recién creado y define qué filtro o modelo se debe aplicar al componente.
   * Útil para texto explicativo, de muestra o de marcador de posición.

#### `template` {#template}

Si se proporcionan pares clave/valor opcionales, `template` puede escribirlos automáticamente en el nuevo componente. Además, también se pueden especificar los siguientes valores opcionales.

### `cf` {#cf}

Si el componente está relacionado con el contenido de un fragmento de contenido, puede proporcionar la siguiente información.

* `name` define un nombre opcional guardado en el JCR para el componente recién creado.
   * Solo informativo y, por lo general, no se muestra en la interfaz de usuario como lo es `title`.
* `cfModel` define el modelo [Fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md) para el componente recién creado.
* `cfFolder` define en qué carpeta se creará el fragmento de contenido.
* `title` define el título del nuevo fragmento de contenido.
* `description` define una descripción del nuevo fragmento de contenido.
* `template` define los valores o claves opcionales que se escribirán automáticamente en el fragmento de contenido recién creado.
   * Útil para texto explicativo, de muestra o de marcador de posición.

### `cf` puede ser implícito {#cf-implied}

Si la página está [instrumentada](/help/implementing/universal-editor/getting-started.md#instrument-page) para que apunte a un campo de referencia, se tomará el valor `cf`.

```html
<div data-aue-resource="urn:aem:/content" data-aue-type="container" data-aue-prop="field"></div>
```

En tal caso, se supone `cf`, ya que `data-aue-prop` señala a un campo de referencia. Sin `data-aue-prop`, el editor universal supondrá `page`, porque en tal caso los componentes no están vinculados a través de un campo de referencia.

```html
<div data-aue-resource="urn:aem:/content" data-aue-type="container"></div>
```

Los componentes son simplemente subnodos debajo del recurso.
