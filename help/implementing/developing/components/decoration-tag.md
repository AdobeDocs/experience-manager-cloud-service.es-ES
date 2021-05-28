---
title: Etiqueta decorativa
description: Cuando se procesa un componente de una página web, se puede generar un elemento HTML que ajuste el componente procesado en sí mismo. Para los desarrolladores, AEM tiene una lógica clara y sencilla para controlar las etiquetas de decoración que envuelven los componentes incluidos.
exl-id: a90fd619-eff6-466f-9178-90374f988b5d
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 10%

---

# Etiqueta decorativa {#decoration-tag}

Cuando se procesa un componente de una página web, se puede generar un elemento HTML que ajuste el componente procesado en sí mismo. Esto tiene dos propósitos principales:

* Un componente solo se puede editar cuando se ajusta con un elemento HTML.
* El elemento envolvente se utiliza para aplicar clases HTML que proporcionan:
   * Información de diseño
   * Información de estilo

Para los desarrolladores, AEM tiene una lógica clara y sencilla para controlar las etiquetas de decoración que envuelven los componentes incluidos. La combinación de dos factores define si se representa la etiqueta de decoración y cómo se hace, y en qué se sumergirá esta página:

* El propio componente puede configurar su etiqueta de decoración con un conjunto de propiedades.
* Las secuencias de comandos que incluyen componentes pueden definir los aspectos de la etiqueta de decoración con parámetros de inclusión.

## Recomendaciones {#recommendations}

Estas son algunas recomendaciones generales sobre cuándo incluir el elemento envolvente que debería ayudar a evitar tener problemas inesperados:

* La presencia del elemento envolvente no debe diferir entre los WCMModes (modo de edición o previsualización), instancias (autor o publicación) o entorno (ensayo o producción), de modo que la CSS y los JavaScript de la página funcionen de forma idéntica en todos los casos.
* El elemento wrapper debe agregarse a todos los componentes que sean editables, de modo que el editor de páginas pueda inicializarlos y actualizarlos correctamente.
* Para los componentes no editables, se puede evitar el elemento envolvente si no cumple ninguna función en particular, de modo que el marcado resultante no se infle innecesariamente.

## Controles de componentes {#component-controls}

Se pueden aplicar las siguientes propiedades y nodos a los componentes para controlar el comportamiento de su etiqueta decorativa:

* **`cq:noDecoration {boolean}`:** Esta propiedad se puede añadir a un componente y un valor verdadero fuerza AEM no generar ningún elemento envolvente sobre el componente.
* **`cq:htmlTag`node :** Este nodo se puede agregar bajo un componente y puede tener las siguientes propiedades:
   * **`cq:tagName {String}`:** Esto se puede utilizar para especificar una etiqueta HTML personalizada que se utilizará para ajustar los componentes en lugar del elemento DIV predeterminado.
   * **`class {String}`:** Esto se puede usar para especificar nombres de clase css que se agregarán al envoltorio.
   * Otros nombres de propiedad se agregarán como atributos HTML con el mismo valor de cadena que se proporciona.

## Controles de script {#script-controls}

En general, el comportamiento del envoltorio en HTL se puede resumir de la siguiente manera:

* No se procesa ningún DIV envolvente de forma predeterminada (cuando se hace `data-sly-resource="foo"`).
* Todos los modos wcm (deshabilitado, vista previa, edición tanto en autor como en publicación) se representan de forma idéntica.

El comportamiento del envoltorio también se puede controlar completamente.

* El script HTL tiene control total sobre el comportamiento resultante de la etiqueta wrapper.
* Las propiedades de componente (como `cq:noDecoration` y `cq:tagName`) también pueden definir la etiqueta de envoltura.

Es posible controlar completamente el comportamiento de las etiquetas wrapper de los scripts HTL y su lógica asociada.

Para obtener más información sobre el desarrollo en HTL, consulte la [documentación de HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=es).

### Árbol de decisiones {#decision-tree}

Este árbol de decisión resume la lógica que determina el comportamiento de las etiquetas envolventes.

![Árbol de decisiones](assets/decoration-tag-decision-tree.png)

### Casos de uso {#use-cases}

En los tres casos de uso siguientes se proporcionan ejemplos de cómo se gestionan las etiquetas envolventes y también se ilustra cuán sencillo es controlar el comportamiento deseado de las etiquetas envolventes.

En todos los ejemplos siguientes se asume la siguiente estructura de contenido y componentes:

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

El caso de uso más típico es cuando un componente incluye otro componente por motivos de reutilización del código. En ese caso, el componente incluido no desea ser editable con su propia barra de herramientas y cuadro de diálogo, por lo que no se necesita un envoltorio y se ignorará el `cq:htmlTag` del componente. Esto puede considerarse el comportamiento predeterminado.

`one.html: <sly data-sly-resource="child"></sly>`

`two.html: Hello World!`

Resultado en `/content/test.html`:

**`Hello World!`**

Un ejemplo sería un componente que incluye un componente de imagen principal para mostrar una imagen, normalmente en ese caso utilizando un recurso sintético, que consiste en incluir un componente secundario virtual pasando a un recurso de datos sly-resource un objeto Map que represente todas las propiedades que tendría el componente.

#### Caso de uso 2: Incluir un componente editable {#use-case-include-an-editable-component}

Otro caso de uso común es cuando los componentes de contenedor incluyen componentes secundarios editables, como un contenedor de diseño. En este caso, cada elemento secundario incluido necesita imperativamente un envoltorio para que funcione el editor (a menos que se deshabilite explícitamente con la propiedad `cq:noDecoration` ).

Dado que el componente incluido es en este caso un componente independiente, necesita un elemento envolvente para que funcione el editor y para definir su diseño y estilo para aplicar. Para déclencheur de este comportamiento, está la opción `decoration=true`.

`one.html: <sly data-sly-resource="${'child' @ decoration=true}"></sly>`

`two.html: Hello World!`

Resultado en `/content/test.html`:

**`<article class="component-two">Hello World!</article>`**

#### Caso de uso 3: Comportamiento personalizado {#use-case-custom-behavior}

Puede haber muchos casos complejos, que se pueden lograr fácilmente con la posibilidad de que HTL proporcione explícitamente:

* **`decorationTagName='ELEMENT_NAME'`** Para definir el nombre del elemento del envoltorio.
* **`cssClassName='CLASS_NAME'`** Para definir los nombres de clase CSS que desea establecer en él.

`one.html: <sly data-sly-resource="${'child' @ decorationTagName='aside', cssClassName='child'}"></sly>`

`two.html: Hello World!`

Resultado `/content/test.html`:

**`<aside class="child">Hello World!</aside>`**
