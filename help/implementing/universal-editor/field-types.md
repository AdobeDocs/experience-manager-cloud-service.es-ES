---
title: Tipos de campos
description: Obtenga información sobre los distintos tipos de campos que el editor universal puede editar en el carril de componentes con ejemplos de cómo instrumentar su propia aplicación.
exl-id: cb4567b8-ebec-477c-b7b9-53f25b533192
source-git-commit: 7ef3efa6e074778b7b3e3a8159056200b2663b30
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 7%

---


# Tipos de campos {#field-types}

Obtenga información sobre los distintos tipos de campos que el editor universal puede editar en el carril de componentes con ejemplos de cómo instrumentar su propia aplicación.

{{universal-editor-status}}

## Información general {#overview}

Al adaptar sus propias aplicaciones para utilizarlas con el editor universal, debe instrumentar los componentes y definir qué tipos de datos pueden manipular en el carril de componentes del editor.

Este documento proporciona información general sobre los tipos de campo disponibles junto con ejemplos de configuración.

>[!TIP]
>
>Si no conoce cómo instrumentar la aplicación para el editor universal, consulte el documento [AEM Información general del editor universal para desarrolladores de.](/help/implementing/universal-editor/developer-overview.md)

## Booleano {#boolean}

Un campo booleano almacena un valor true/false simple representado como una casilla de verificación.

### Muestra {#sample-boolean}

```json
{
  "fields": [   
   {
      "component": "boolean",
      "valueType": "boolean",
      "name": "field1",
      "label": "Boolean Field",
      "description": "This is a boolean field.",
      "required": true,
      "placeholder": null,
      "validation": {
        "customErrorMsg": "This is an error."
      }
    }
  ]
}
```

## Grupo de casillas de verificación {#checkbox-group}

Al igual que un booleano, un grupo de casillas de verificación permite seleccionar varios elementos verdaderos/falsos.

### Muestra {#sample-checkbox-group}

```json
{
  "fields": [   
   {
      "component": "checkbox-group",
      "valueType": "string-array",
      "name": "field1",
      "label": "Checkbox Group",
      "description": "This is a checkbox group.",
      "required": true,
      "placeholder": null,
      "options": [
        { "name": "First option", "value": "one" },
        { "name": "Second option", "value": "two" },
        { "name": "Third option", "value": "three" }
      ]
    }
  ]
}
```

## Fecha y hora {#date-time}

Un campo de fecha y hora permite especificar una fecha, una hora o una combinación de ambas.

### Muestra {#sample-date-time}

```json
{
  "fields": [   
      {
      "component": "date-time",
      "valueType": "date-time",
      "name": "field1",
      "label": "Date Time",
      "description": "This is a date time field that stores both date and time.",
      "required": true,
      "placeholder": "YYYY-MM-DD HH:mm:ss",
      "displayFormat": null,
      "valueFormat": null,
      "validation": {
        "customErrorMsg": "Marty! You have to come back with me!"
      }
    },
    {
      "component": "date-time",
      "valueType": "date",
      "name": "field2",
      "label": "Another Date Time",
      "description": "This is another date time field that only stores the date.",
      "required": true,
      "placeholder": "YYYY-MM-DD",
      "displayFormat": null,
      "valueFormat": null,
      "validation": {
        "customErrorMsg": "Back to the future!"
      }
    },
    {
      "component": "date-time",
      "valueType": "time",
      "name": "field3",
      "label": "Yet Another Date Time",
      "description": "This is another date time field that only stores the time.",
      "required": true,
      "placeholder": "HH:mm:ss",
      "displayFormat": null,
      "valueFormat": null,
      "validation": {
        "customErrorMsg": "Great Scott!"
      }
    }
  ]
}
```

## Número {#number}

Un campo numérico permite introducir un número.

### Muestra {#sample-number}

```json
{
  "fields": [   
   {
      "component": "number",
      "valueType": "number",
      "name": "field1",
      "label": "Number Field",
      "description": "This is a number field.",
      "required": true,
      "placeholder": null,
      "validation": {
        "numberMin": null,
        "numberMax": null,
        "customErrorMsg": "Please don't do that."
      }
    }
  ]
}
```

## Grupo de radio {#radio-group}

Un grupo de opciones permite realizar una selección mutuamente excluyente de varias opciones representadas como un grupo similar a un grupo de casillas de verificación.

### Muestra {#sample-radio-group}

```json
{
  "fields": [   
   {
      "component": "radio-group",
      "valueType": "string",
      "name": "field1",
      "label": "Radio Group",
      "description": "This is a radio group.",
      "required": true,
      "placeholder": null,
      "options": [
        { "name": "Option One", "value": "one" },
        { "name": "Option Two", "value": "two" },
        { "name": "Option Three", "value": "three" }
      ]
    }
  ]
}
```

## Referencia {#reference}

Una referencia permite especificar otro objeto de datos como referencia desde el objeto actual.

## Seleccionar {#select}

Una selección permite seleccionar una o más opciones predefinidas en un menú desplegable.

### Muestra {#sample-select}

```json
{
  "fields": [   
   {
      "component": "select",
      "valueType": "string",
      "name": "field1",
      "label": "Select",
      "description": "This is a select.",
      "required": true,
      "placeholder": null,
      "options": [
        { "name": "Option One", "value": "one" },
        { "name": "Option Two", "value": "two" },
        { "name": "Option Three", "value": "three" }
      ],
      "emptyOption": true
    }
  ]
}
```

## Área de texto {#text-area}

Un área de texto permite la entrada de texto multilínea.

### Muestra {#sample-text-area}

```json
{
  "fields": [   
   {
      "component": "text-area",
      "valueType": "string",
      "name": "field1",
      "label": "Text Area",
      "description": "This is a text area.",
      "required": true,
      "multi": true,
      "placeholder": null,
      "mimeType": "text/x-markdown"
    }
  ]
}
```

## Entrada de texto {#text-input}

Una entrada de texto permite una sola línea de entrada de texto.

### Muestra {#sample-text-input}

```json
{
  "fields": [   
   {
      "component": "text-input",
      "valueType": "string",
      "name": "field1",
      "label": "Text Input",
      "description": "This is a text input.",
      "required": true,
      "multi": true,
      "placeholder": null
    },
    {
      "component": "text-input",
      "valueType": "string",
      "name": "field2",
      "label": "Another Text Input",
      "description": "This is a text input with validation.",
      "required": true,
      "multi": true,
      "placeholder": null,
      "validation": {
        "minLength": 5,
        "maxLength": 10,
        "regExp": "^foo:.*",
        "customErrorMsg": "I'm sorry, Dave. I can't do that."
      }
    }
  ]
}
```

## Pestaña {#tab}

Una pestaña permite agrupar otros campos de entrada en varias pestañas para mejorar la organización del diseño para los autores.

A `tab` definición se puede considerar como un separador en la matriz de `fields`. Todo lo que viene después de un `tab` se colocará en esa pestaña hasta que se cree un nuevo `tab` se encuentra, después de lo cual los siguientes elementos se colocarán en la nueva pestaña.

Si desea que los elementos aparezcan encima de todas las pestañas, deben definirse antes que las pestañas.

### Muestra {#sample-tab}

```json
{
  "id": "title",
  "fields": [
    {
      "component": "tab",
      "label": "Tab",
      "name": "tab1"
    },
    {
      "component": "text-input",
      "name": "tab-response",
      "value": "",
      "placeholder": "Tab? I can't give you a tab unless you order something.",
      "label": "Lou",
      "valueType": "string"
    },
    {
      "component": "tab",
      "label": "Pepsi Free",
      "name": "tab2"
    },
    {
      "component": "text-input",
      "name": "pepsi-free-response",
      "value": "",
      "placeholder": "You want a Pepsi, pal, you're gonna pay for it.",
      "label": "Mr. Carruthers",
      "valueType": "string"
    },
    {
      "component": "select",
      "name": "without-sugar",
      "value": "coffee",
      "label": "Something without sugar",
      "valueType": "string",
      "options": [
        { "name": "Coffee", "value": "coffee" },
        { "name": "Hot Coffee", "value": "hot-coffee" },
        { "name": "Hotter Coffee", "value": "hotter-coffee" }
      ]
    }
  ]
}
```
