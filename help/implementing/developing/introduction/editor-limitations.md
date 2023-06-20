---
title: Limitaciones del editor
description: El editor de la IU táctil utiliza las superposiciones para interactuar con el contenido limitado en un iframe. Esta interacción crea algunas limitaciones en el uso del editor y también para los desarrolladores.
exl-id: 6a4f0e43-1076-4da9-95dc-9c5bf83e30d0
source-git-commit: bceec9ea6858b1c4c042ecd96f13ae5cac1bbee5
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 10%

---

# Limitaciones del editor {#editor-limitations}

El editor de la IU táctil utiliza las superposiciones para interactuar con el contenido limitado en un iframe. Esta interacción crea algunas limitaciones en el uso del editor y también para los desarrolladores. Esta página resume estas limitaciones y proporciona soluciones o soluciones alternativas siempre que sea posible.

## Limitaciones funcionales {#functional-limitations}

Un autor puede encontrar las siguientes limitaciones funcionales al utilizar el editor para crear páginas.

### Vínculos no activos {#links-not-active}

Cuándo [edición de una página](/help/sites-cloud/authoring/fundamentals/editing-content.md), los vínculos no están activos.

* [Cambiar a **Previsualizar** modo](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode) para navegar mediante los vínculos del contenido.

### Páginas de estructura {#structure-pages}

Las páginas no pueden tener nombre `structure`. Páginas con nombre `structure` no se podrán editar en el editor de páginas.

## Limitaciones de CSS {#css-limitations}

Un desarrollador puede encontrar las siguientes limitaciones con las interacciones del editor con CSS.

### Elementos en posición absoluta {#absolutely-positioned-elements}

Los elementos con una posición absoluta pueden causar problemas en la posición de su superposición.

* Si esto sucede, asegúrese de que las dimensiones del elemento con una posición absoluta son correctas, ya que el editor creará una superposición con las mismas dimensiones.

### Unidades vh {#vh-units}

`vh` AEM las unidades no son compatibles porque la altura del iframe debe ajustarse automáticamente mediante la opción de configuración de la posición de la unidad de control de.

### Imágenes de fondo fijas {#fixed-background-images}

Es posible que las imágenes de fondo fijas no se muestren como fijas al desplazarse debido al hecho de que están incrustadas en un iframe.

* Seleccionar **Ver página publicada** en las acciones de la barra de encabezado muestra la página correctamente.

### Altura al 100% {#height}

El 100 % de altura no es compatible con el elemento de cuerpo de una página.

* Una solución alternativa es implementar un cuerpo de pantalla completa &quot;estirando&quot; el elemento de cuerpo de la siguiente manera:

```xml
body {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
}
```

### Contraer margen {#margin-collapsing}

Los problemas de contracción del margen se pueden ver si el primer elemento secundario del elemento body tiene un margen.

* La solución consiste en añadir una corrección clara en el nivel de elemento de cuerpo como se indica a continuación:

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```
