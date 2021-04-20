---
title: Markdown
description: Comprender cómo el editor de fragmentos de contenido utiliza la sintaxis Markdown para permitirle crear fácilmente contenido sin encabezado.
feature: Content Fragments
role: Business Practitioner
translation-type: tm+mt
source-git-commit: 6fa911f39d707687e453de270bc0f3ece208d380
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 5%

---


# Markdown {#markdown}

Cuando esté [creando](/help/assets/content-fragments/content-fragments-variations.md#authoring-your-content), el editor de fragmentos de contenido utiliza la sintaxis *markdown* para permitirle escribir fácilmente contenido sin encabezado:

![editor de markdown](/help/assets/content-fragments/assets/cfm-markdown-01.png)

Puede definir:

* [Anotación de encabezado](/help/assets/content-fragments/content-fragments-markdown.md#heading-notation)
* [Párrafos y saltos de línea](/help/assets/content-fragments/content-fragments-markdown.md#paragraphs-and-line-breaks)
* [Vínculos](/help/assets/content-fragments/content-fragments-markdown.md#links)
* [Imágenes](/help/assets/content-fragments/content-fragments-markdown.md#images)
* [Comillas de bloque](/help/assets/content-fragments/content-fragments-markdown.md#block-quotes)
* [Listas](/help/assets/content-fragments/content-fragments-markdown.md#lists)
* [Énfasis](/help/assets/content-fragments/content-fragments-markdown.md#emphasis)
* [Bloques de código](/help/assets/content-fragments/content-fragments-markdown.md#code-blocks)
* [Fuentes de barra invertida](/help/assets/content-fragments/content-fragments-markdown.md#backslash-escapes)

## Notación de encabezado {#heading-notation}

Para crear un encabezado, coloque una etiqueta (#) delante del encabezado. Se utiliza una etiqueta (#) para H1, dos etiquetas hash (##) para H2, etc. Se pueden usar hasta 6 etiquetas hash. Por ejemplo:

    `## This is an H2`

    `### This is an H3`

    `###### This is a H6`

De forma opcional, puede crear una H1 subrayando el texto en signos iguales y creando una H2 subrayando el texto en signos menos. Por ejemplo:

    `This is an H1`

    `=============`

    `This is an H2`

    `-------------`

## Párrafos y saltos de línea {#paragraphs-and-line-breaks}

Un párrafo es simplemente una o más líneas consecutivas de texto, separadas por una o más líneas en blanco. Una línea en blanco es una línea que contiene únicamente espacios o tabulaciones. Los párrafos normales no deben tener sangría con espacios o tabulaciones.

Un salto de línea se crea terminando una línea con dos o más espacios que un retorno.

## Vínculos {#links}

Puede crear vínculos en línea y de referencia.

En ambos estilos, el texto del vínculo está delimitado por corchetes `[]`.

Estos son ejemplos de vínculos en línea:

    `This is [an example](https://example.com/ "Title") inline link.`

    `This is [an example of an email link](emailto:myaddress@mydomain.info)`

    `[This link](https://example.net/) has no title attribute.`

Un vínculo de referencia tiene la siguiente sintaxis:

    `Hey you should [checkout][0] this [cool thing][wiki] that I [made][].`

    `[0]: https://www.google.ca`

    `[wiki]: https://www.wikipedia.org`

    `[made]: https://www.stackoverflow.com`

## Imágenes {#images}

La sintaxis de las imágenes es similar a los vínculos. Puede crear imágenes en línea y referenciadas.

Por ejemplo, una imagen en línea tiene la siguiente sintaxis:

    `![Alt text](/path/to/img.jpg)`

    `![Alt text](/path/to/img.jpg "Optional title")`

La sintaxis incluye:

* Un signo de exclamación: !;
* seguido de un conjunto de corchetes, que contienen el texto del atributo alternativo de la imagen;
* seguido de un conjunto de paréntesis, que contiene la dirección URL o la ruta a la imagen, y de un atributo de título opcional entre comillas dobles o simples.

Una imagen de estilo de referencia tiene la siguiente sintaxis:

    `![Alt text][id]`

Donde &quot;id&quot; es el nombre de una referencia de imagen definida. Las referencias de imagen se definen con una sintaxis idéntica a las referencias de vínculo:

    `[id]: url/to/image "Optional title attribute"`

## Comillas de bloque {#block-quotes}

Puede citar texto añadiendo el símbolo > antes del texto. Por ejemplo:

    `>This is block quotes`

    `>asdhfjlkasdhlf`

    `>asdfahsdlfasdfj`

Puede tener comillas de bloque anidadas. Por ejemplo:

    `> This is the first level of quoting.`

    `>`

        `>> This is nested blockquote.`

    `>`

    `> Back to the first level.`

## Listas {#lists}

Puede crear listas ordenadas y sin ordenar.

Para crear una lista desordenada, utilice &amp;ast; antes de los elementos de la lista. Por ejemplo:

    `* item in list`

    `* item in list`

    `* item in list`

Para crear una lista ordenada, añada los números, seguidos de un punto, antes de cada elemento de la lista. Por ejemplo:

    `1. First item in list.`

    `2. Second item in list.`

    `3. Third item in list.`

## Énfasis {#emphasis}

Puede agregar estilo en cursiva o negrita al texto.

Para agregar cursiva de la siguiente manera:

    `*single asterisks*`

    `_single underscores_`

    `Keyboard shortcut: Ctrl-I (Cmd-I)`

Puede aplicar negrita al texto de la siguiente manera:

    `**double asterisks**`

    `__double underscores__`

    `Keyboard shortcut: Ctrl-B (Cmd-B)`

Para indicar un intervalo de código, encapsúltelo con comillas de rebote (`). A diferencia de los bloques de código preformateados, un intervalo de código indica el código dentro de un párrafo normal.

Por ejemplo:

    ``Use the `printf()` function.``

## Bloques de código {#code-blocks}

Los bloques de código generalmente se utilizan para ilustrar el código fuente. Puede crear bloques de código aplicando sangría al código utilizando una pestaña o un mínimo de 4 espacios. Por ejemplo:

    `This is a normal paragraph.`

        `This is a code block.`

## Fuentes de barra invertida {#backslash-escapes}

Puede utilizar las secuencias de escape de barra invertida para generar caracteres literales que tengan un significado especial en la sintaxis del formato. Por ejemplo, si desea rodear una palabra con asteriscos literales (en lugar de una etiqueta HTML &lt;em> ), puede utilizar barras invertidas antes de los asteriscos, de esta manera:

    `\\*literal asterisks\\*`

Las secuencias de escape de barra invertida están disponibles para los siguientes caracteres:

    ` \ backslash`

    `` ` backtick``

    ` * asterisk`

    ` _ underscore`

    ` {} curly braces`

    ` [] square brackets`

    ` () parentheses`

    ` # hash mark`

    ` + plus sign`

    ` - minus sign (hyphen)`

    ` . dot`
