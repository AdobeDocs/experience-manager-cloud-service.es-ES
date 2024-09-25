---
title: Bloques para WYSIWYG y la creación basada en documentos
description: Descubra cómo puede crear bloques que se puedan utilizar tanto para la creación de WYSIWYG como para la creación basada en documentos.
feature: Edge Delivery Services
role: User
source-git-commit: 3419fa943eb865d87467443527ea97fcd64909c2
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# Bloques para WYSIWYG y la creación basada en documentos {#wysiwyg-and-doc-blocks}

Descubra cómo puede crear bloques que se puedan utilizar tanto para la creación de WYSIWYG como para la creación basada en documentos.

## Información general {#overview}

En ciertos proyectos, es posible que desee admitir la creación de [WYSIWYG con el editor universal](/help/edge/wysiwyg-authoring/authoring.md), así como la creación basada en documentos [de.](/help/edge/docs/authoring.md) Para minimizar el tiempo de desarrollo y garantizar la misma experiencia en el sitio, puede crear un conjunto de bloques para admitir ambos casos de uso.

Para ello, debe utilizar el mismo método de modelado de contenido tanto para la configuración de creación de WYSIWYG como para la configuración de creación basada en documentos.

## Aproximación {#approach}

En WYSIWYG AEM authoring de, usted [declara un modelo](/help/edge/wysiwyg-authoring/content-modeling.md) y proporciona convenciones de nomenclatura. A continuación, los datos se representan en estructuras de bloque similares a la tabla mediante Edge Delivery del mismo modo que si la tabla se hubiera creado manualmente mediante la creación basada en documentos.

Para conseguirlo, se realizan ciertas suposiciones como, por ejemplo, para un bloque simple como un teaser que todas las propiedades y grupos de propiedades se representan en 1.n filas con una sola columna cada una. Para bloques que tienen 1..En los elementos (como carrusel y tarjetas), los elementos se anexan después de estas filas con una fila cada uno y una columna para cada propiedad o grupo de propiedades.

Si sigue el mismo enfoque para la creación basada en documentos, puede reutilizar los bloques de WYSIWYG.
