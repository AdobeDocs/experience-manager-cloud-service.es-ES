---
title: Etiqueta decorativa
description: Cuando se procesa un componente de una página web, se puede generar un elemento HTML que ajuste el componente procesado en sí mismo. Para los desarrolladores, AEM tiene una lógica clara y sencilla para controlar las etiquetas de decoración que envuelven los componentes incluidos.
exl-id: a90fd619-eff6-466f-9178-90374f988b5d
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 10%

---

# Etiqueta decorativa {#decoration-tag}

Cuando se procesa un componente de una página web, se puede generar un elemento HTML que ajuste el componente procesado en sí mismo. Esto tiene dos propósitos principales:

* Un componente solo se puede editar cuando se envuelve con un elemento HTML.
* El elemento envolvente se utiliza para aplicar clases de HTML que proporcionan:
   * Información de diseño
   * Información de estilo

Para los desarrolladores, AEM tiene una lógica clara y sencilla para controlar las etiquetas de decoración que envuelven los componentes incluidos. El procesamiento de la etiqueta de decoración y cómo se realiza se define mediante la combinación de dos factores, en los que se sumergirá esta página:

* Los propios componentes pueden configurar su etiqueta de decoración con un conjunto de propiedades.
* Los scripts que incluyen componentes pueden definir los aspectos de la etiqueta de decoración con parámetros include.

## Recomendaciones {#recommendations}

Estas son algunas recomendaciones generales sobre cuándo incluir el elemento envolvente que deben ayudar a evitar tener problemas inesperados:

* La presencia del elemento envolvente no debe diferir entre WCModes (modo de edición o vista previa), instancias (autor o publicación) o entorno (ensayo o producción), de modo que CSS y JavaScript de la página funcionen de forma idéntica en todos los casos.
* El elemento envolvente debe añadirse a todos los componentes editables, de modo que el editor de páginas pueda inicializarlos y actualizarlos correctamente.
* En el caso de los componentes no editables, el elemento envolvente se puede evitar si no cumple ninguna función en particular, de modo que el marcado resultante no se hinche innecesariamente.

## Controles de componentes {#component-controls}

Se pueden aplicar las siguientes propiedades y nodos a los componentes para controlar el comportamiento de su etiqueta de decoración:

* **`cq:noDecoration {boolean}`:** AEM Esta propiedad se puede añadir a un componente y un valor true obliga a los usuarios a no generar ningún elemento contenedor sobre el componente.
* **`cq:htmlTag`nodo :** Este nodo se puede añadir bajo un componente y puede tener las siguientes propiedades:
   * **`cq:tagName {String}`:** Se puede utilizar para especificar una etiqueta de HTML personalizada que se utilizará para ajustar los componentes en lugar del elemento DIV predeterminado.
   * **`class {String}`:** Se puede utilizar para especificar los nombres de clase css que se agregarán al contenedor.
   * Otros nombres de propiedades se agregan como atributos de HTML con el mismo valor de cadena proporcionado.

## Controles de script {#script-controls}

En general, el comportamiento del envoltorio en HTL se puede resumir de la siguiente manera:

* No se procesa ningún DIV de contenedor de forma predeterminada (al hacer lo siguiente `data-sly-resource="foo"`).
* Todos los modos wcm (desactivados, de vista previa, de edición tanto en autor como en publicación) se representan de forma idéntica.

El comportamiento del envoltorio también puede controlarse completamente.

* La secuencia de comandos HTL tiene control total sobre el comportamiento resultante de la etiqueta envolvente.
* Propiedades del componente (como `cq:noDecoration` y `cq:tagName`) también puede definir la etiqueta envolvente.

Es posible controlar completamente el comportamiento de las etiquetas envolventes desde los scripts HTL y su lógica asociada.

Para obtener más información sobre el desarrollo en HTL, consulte la [Documentación de HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=es).

### Árbol de decisión {#decision-tree}

Este árbol de decisión resume la lógica que determina el comportamiento de las etiquetas envolventes.

![Árbol de decisión](assets/decoration-tag-decision-tree.png)

### Casos de uso {#use-cases}

Los tres casos de uso siguientes proporcionan ejemplos de cómo se gestionan las etiquetas de envoltorio, y también ilustran lo sencillo que es controlar el comportamiento deseado de las etiquetas de envoltorio.

Todos los ejemplos siguientes suponen la siguiente estructura de contenido y componentes:

```
/content/test/
  @resourceType = "test/components/one"
  child/
    @resourceType = "test/components/two"
```

```
/apps/test/components/
  one/
    one.html
  two/
    two.html
    cq:htmlTag/
      @cq:tagName = "article"
      @class = "component-two"
```

#### Caso de uso 1: Incluir un componente para la reutilización de código {#use-case-include-a-component-for-code-reuse}

El caso de uso más típico es cuando un componente incluye otro componente por motivos de reutilización del código. En ese caso, no se desea que el componente incluido pueda editarse con su propia barra de herramientas y cuadro de diálogo, por lo que no se necesita ningún contenedor, y el componente `cq:htmlTag` se ignora. Este puede considerarse el comportamiento predeterminado.

`one.html: <sly data-sly-resource="child"></sly>`

`two.html: Hello World!`

Resultado en `/content/test.html`:

**`Hello World!`**

Un ejemplo sería un componente que incluye un componente de imagen principal para mostrar una imagen, normalmente en ese caso utilizando un recurso sintético, que consiste en incluir un componente secundario virtual pasando a data-sly-resource un objeto Map que representa todas las propiedades que tendría el componente.

#### Caso de uso 2: Incluir un componente editable {#use-case-include-an-editable-component}

Otro caso de uso común es cuando los componentes de contenedor incluyen componentes secundarios editables, como un contenedor de diseño. En este caso, cada elemento secundario incluido necesita imperativamente un contenedor para que funcione el editor (a menos que esté explícitamente deshabilitado con la variable `cq:noDecoration` property).

Dado que el componente incluido es, en este caso, un componente independiente, necesita un elemento envolvente para que funcione el editor y defina su diseño y estilo para aplicar. Para poner en déclencheur este comportamiento, está el `decoration=true` opción.

`one.html: <sly data-sly-resource="${'child' @ decoration=true}"></sly>`

`two.html: Hello World!`

Resultado en `/content/test.html`:

**`<article class="component-two">Hello World!</article>`**

#### Caso de uso 3: Comportamiento personalizado {#use-case-custom-behavior}

Puede haber cualquier número de casos complejos, que se pueden lograr fácilmente con la posibilidad de que HTL proporcione explícitamente:

* **`decorationTagName='ELEMENT_NAME'`** Para definir el nombre del elemento del envoltorio.
* **`cssClassName='CLASS_NAME'`** Para definir los nombres de clase CSS que se establecerán en ella.

`one.html: <sly data-sly-resource="${'child' @ decorationTagName='aside', cssClassName='child'}"></sly>`

`two.html: Hello World!`

Resultado resultante `/content/test.html`:

**`<aside class="child">Hello World!</aside>`**
