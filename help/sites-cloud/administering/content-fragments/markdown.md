---
title: Markdown
description: Entender cómo el editor de fragmentos de contenido utiliza la sintaxis de markdown para permitirle crear fácilmente contenido, tanto para la creación de páginas como para la entrega sin encabezado.
feature: Content Fragments
role: User
exl-id: 6fbf8128-3b7f-4eda-bbbd-3336578d2586
solution: Experience Manager Sites
source-git-commit: 278242e0be1da5c64abfa5d9ac174013688ff422
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 79%

---

# Markdown {#markdown}

Cuando esté [creando](/help/sites-cloud/administering/content-fragments/authoring.md#edit-multi-line-text-fields-plaintext-markdown) fragmentos de contenido, es posible que tenga [campos de texto de varias líneas](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types) definidos con el **tipo predeterminado** de **Markdown**. El editor de fragmentos de contenido usa la sintaxis *markdown* para permitirle escribir fácilmente contenido, tanto para la creación de páginas como para la entrega sin encabezado:

![Campo Markdown de texto multilínea en el editor](/help/sites-cloud/administering/content-fragments/assets/cf-markdown-field-edit.png)

Puede definir lo siguiente:

* [Anotación de encabezado](/help/sites-cloud/administering/content-fragments/markdown.md#heading-notation)
* [Párrafos y saltos de línea](/help/sites-cloud/administering/content-fragments/markdown.md#paragraphs-and-line-breaks)
* [Vínculos](/help/sites-cloud/administering/content-fragments/markdown.md#links)
* [Imágenes](/help/sites-cloud/administering/content-fragments/markdown.md#images)
* [Comillas de bloque](/help/sites-cloud/administering/content-fragments/markdown.md#block-quotes)
* [Listas](/help/sites-cloud/administering/content-fragments/markdown.md#lists)
* [Énfasis](/help/sites-cloud/administering/content-fragments/markdown.md#emphasis)
* [Bloques de código](/help/sites-cloud/administering/content-fragments/markdown.md#code-blocks)
* [Escapes de barra invertida](/help/sites-cloud/administering/content-fragments/markdown.md#backslash-escapes)

## Anotación de encabezado {#heading-notation}

Para crear un encabezado, coloque una almohadilla (#) delante del encabezado. Una almohadilla (#) indica un H1, dos (##) indica un H2, etc. Se pueden usar hasta seis almohadillas. Por ejemplo:

    `## This is an H2`

    `### This is an H3`

    `###### This is a H6`

De forma opcional, puede crear un H1 subrayando el texto en signos iguales y un H2 subrayando el texto en signos menos. Por ejemplo:

    `This is an H1`

    `=============`

    `This is an H2`

    `-------------`

## Párrafos y saltos de línea {#paragraphs-and-line-breaks}

Un párrafo es simplemente una o más líneas consecutivas de texto, separadas por una o más líneas en blanco. Una línea en blanco es una que contiene únicamente espacios o tabulaciones. Los párrafos normales no deben tener sangría con espacios o tabulaciones.

Un salto de línea se crea terminando una línea con dos o más espacios y un retorno.

## Vínculos {#links}

Puede crear vínculos en línea y de referencia.

En ambos estilos, el texto del vínculo está delimitado por corchetes `[]`.

Estos son ejemplos de vínculos en línea:

    `This is [an example](https://example.com/ "Title") inline link.`

    `This is [an example (non-standard) of an email link](emailto:myaddress@mydomain.info)`

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

La sintaxis incluye lo siguiente:

* Un signo de exclamación: !;
* seguido de un conjunto de corchetes, que contienen el texto del atributo alternativo de la imagen;
* seguido de un conjunto de paréntesis, que contiene la dirección URL o la ruta a la imagen, y de un atributo de título opcional entre comillas dobles o simples.

Una imagen de estilo de referencia tiene la siguiente sintaxis:

    `![Alt text][id]`

Donde “id” es el nombre de una referencia de imagen definida. Las referencias de imagen se definen con una sintaxis idéntica a las referencias de vínculo:

    `[id]: url/to/image "Optional title attribute"`

## Comillas de bloque {#block-quotes}

Puede citar texto añadiendo el símbolo > antes del texto. Por ejemplo:

    `>This is block quotes`

    `>asdhfjlkasdhlf`

    `>asdfahsdlfasdfj`

Puede tener citas de bloque anidadas. Por ejemplo:

    `> This is the first level of quoting.`

    `>`

        `>> This is nested blockquote.`

    `>`

    `> Back to the first level.`

## Listas {#lists}

Puede crear listas ordenadas y desordenadas.

Para crear una lista desordenada, utilice el símbolo &ast; antes de los elementos de la lista. Por ejemplo:

    `* item in list`

    `* item in list`

    `* item in list`

Para crear una lista ordenada, añada los números, seguidos de un punto, antes de cada elemento de la lista. Por ejemplo:

    `1. First item in list.`

    `2. Second item in list.`

    `3. Third item in list.`

## Énfasis {#emphasis}

Puede añadir estilos de cursiva o negrita a su texto.

Puede añadir cursiva de la siguiente manera:

    `*single asterisks*`

    `_single underscores_`

    `Keyboard shortcut: Ctrl-I (Cmd-I)`

Puede aplicar negrita al texto de la siguiente manera:

    `**double asterisks**`

    `__double underscores__`

    `Keyboard shortcut: Ctrl-B (Cmd-B)`

Para indicar un intervalo de código, encapsúlelo con acentos graves (&grave;). A diferencia de los bloques de código con formato previo, un intervalo de código indica el código dentro de un párrafo normal.

Por ejemplo:

    ``Use the `printf()` function.``

## Bloques de código {#code-blocks}

Los bloques de código suelen emplearse para ilustrar el código fuente. Puede crear bloques de código sangrándolos con una tabulación o con un mínimo de cuatro espacios. Por ejemplo:

    `This is a normal paragraph.`

        `This is a code block.`

## Escapes de barra invertida {#backslash-escapes}

Puede utilizar secuencias de escape de barra invertida para generar caracteres literales que también tengan un significado especial en la sintaxis de formato. Por ejemplo, si desea rodear una palabra con asteriscos literales (en lugar de una etiqueta &lt;em> de HTML), puede utilizar barras invertidas antes de los asteriscos, de esta manera:

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
