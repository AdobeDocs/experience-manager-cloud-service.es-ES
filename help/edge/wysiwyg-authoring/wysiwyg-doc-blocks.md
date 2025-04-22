---
title: Bloques para la creación WYSIWYG y basada en documentos
description: Descubra cómo puede crear bloques que se puedan utilizar tanto para la creación WYSIWYG como para la creación basada en documentos.
feature: Edge Delivery Services
role: User
exl-id: f039c70a-e1a0-4fcc-8f42-dfa0f8bb3764
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 100%

---

# Bloques para la creación WYSIWYG y basada en documentos {#wysiwyg-and-doc-blocks}

Descubra cómo puede crear bloques que se puedan utilizar tanto para la creación WYSIWYG como para la creación basada en documentos.

## Información general {#overview}

En determinados proyectos, puede admitir tanto la [creación WYSIWYG mediante el editor universal](/help/edge/wysiwyg-authoring/authoring.md) como la [creación basada en documentos](/help/edge/docs/authoring.md).  Para minimizar el tiempo de desarrollo y garantizar la misma experiencia en el sitio, puede crear un conjunto de bloques para admitir ambos casos de uso.

Para ello, debe utilizar el mismo enfoque de modelado de contenido tanto para su configuración de creación WYSIWYG como para su configuración de creación basada en documentos.

## Enfoque {#approach}

En la creación WYSIWYG en AEM, se [declara un modelo](/help/edge/wysiwyg-authoring/content-modeling.md) y se proporcionan convenciones de nomenclatura. A continuación, los datos se presentan en estructuras de bloques similares a tablas mediante Edge Delivery, del mismo modo que si la tabla se hubiera creado manualmente mediante la creación basada en documentos.

Para lograrlo, se hacen ciertas suposiciones como, por ejemplo, para un bloque sencillo como un teaser, todas las propiedades y grupos de propiedades se representan en 1..n filas con una sola columna cada una. Para bloques que tienen 1..n elementos (como carrusel y tarjetas), los elementos se añaden después de estas filas con una fila cada una y una columna para cada propiedad/grupo de propiedades.

Si sigue el mismo método para la creación basada en documentos, podrá reutilizar los bloques WYSIWYG.
