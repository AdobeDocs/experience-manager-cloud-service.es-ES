---
title: Análisis de fragmentos de contenido
description: Comprenda la estructura de los fragmentos de contenido. Esto proporciona información relevante para la entrega sin encabezado y la creación de páginas.
feature: Content Fragments
role: User, Developer
exl-id: d9268c1a-bfe6-4df7-bad9-6007dd79e0aa
solution: Experience Manager Sites
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 3%

---

# Análisis de la estructura de fragmentos de contenido {#analyzing-content-fragments-structure}

Los fragmentos de contenido están diseñados para [entrega sin encabezado mediante GraphQL](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md). Esto significa que pueden tener una estructura de varias capas.

Experience Manager (AEM) proporciona varios métodos para ver y analizar la estructura de los fragmentos.

## Referencias {#references}

La estructura de varias capas se crea mediante Referencias:

* [Los tipos de datos para Referencias se definen en el Modelo de fragmento de contenido](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#using-references-to-form-nested-content)
* Durante la creación, puede:
   * [Administrar estas referencias](/help/sites-cloud/administering/content-fragments/authoring.md##manage-references)
   * [Buscar referencias principales del fragmento](/help/sites-cloud/administering/content-fragments/managing.md#parent-references-fragment)

## Árbol de estructura {#structure-tree}

Abra la pestaña **Árbol de estructura** de la barra de herramientas del editor para mostrar la estructura jerárquica del fragmento de contenido y sus referencias. Utilice el icono de vínculo para abrir las referencias.

Por ejemplo:

![Editor de fragmentos de contenido: árbol de estructura](assets/cf-authoring-structure-tree.png)
