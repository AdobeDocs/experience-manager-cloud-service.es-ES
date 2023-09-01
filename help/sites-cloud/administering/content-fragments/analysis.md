---
title: Análisis de fragmentos de contenido
description: Comprenda la estructura y la entrega de contenido de los fragmentos de contenido. Esto proporciona información sobre la entrega sin encabezado y la creación de páginas.
feature: Content Fragments
role: User, Developer, Architect
source-git-commit: 3d20f4bca566edcdb5f13eab581c33b7f3cf286d
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 2%

---


# Análisis de la estructura de fragmentos de contenido {#analyzing-content-fragments-structure}

Los fragmentos de contenido están diseñados para [Envío sin encabezado mediante GraphQL](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md). Esto significa que pueden tener una estructura de varias capas.

Experience Manager AEM () proporciona varios métodos para ver y analizar la estructura de los fragmentos.

## Referencias {#references}

La estructura se crea mediante Referencias:

* [Los tipos de datos para Referencias se definen en el Modelo de fragmento de contenido](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#using-references-to-form-nested-content)
* Durante la creación, puede:
   * [Administrar estas referencias](/help/sites-cloud/administering/content-fragments/authoring.md##manage-references)
   * [Buscar referencias principales del fragmento](/help/sites-cloud/administering/content-fragments/managing.md#parent-references-fragment)

## Árbol de estructura {#structure-tree}

Abra el **Árbol de estructura** de la barra de herramientas del editor para mostrar la estructura jerárquica del fragmento de contenido y sus referencias. Utilice el icono de vínculo para abrir las referencias.

Por ejemplo:

![Editor de fragmentos de contenido: árbol de estructura](assets/cf-authoring-structure-tree.png)