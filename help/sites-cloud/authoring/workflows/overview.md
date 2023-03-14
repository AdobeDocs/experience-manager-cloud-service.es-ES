---
title: Uso de flujos de trabajo
description: Los flujos de trabajo en AEM le permiten automatizar una serie de pasos que se llevan a cabo en una página o un recurso.
exl-id: ed157646-abb3-45c6-bafd-7889bd93fdf3
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 100%

---

# Uso de flujos de trabajo {#working-with-workflows}

Los flujos de trabajo de AEM le permiten automatizar una serie de pasos que se llevan a cabo en páginas (una o más) o recursos.

Por ejemplo, al publicar, un editor debe revisar el contenido antes de que un administrador del sitio active la página. Un flujo de trabajo que automatiza este ejemplo notifica a cada participante cuándo es el momento de realizar el trabajo necesario:

1. El autor aplica el flujo de trabajo a la página.
1. El editor recibe un elemento de trabajo que indica que es necesario para revisar el contenido de la página. Al terminar, indica que el elemento de trabajo se ha completado.
1. El administrador del sitio recibe un elemento de trabajo que solicita la activación de la página. Al terminar, indica que el elemento de trabajo se ha completado.

Normalmente:

* Los autores de contenido aplican los flujos de trabajo a las páginas y también participan en los flujos de trabajo.
* Los flujos de trabajo que utiliza son específicos de los procesos empresariales de su organización.

En las páginas que se incluyen a continuación, se tratan los temas siguientes:

* [Aplicación de flujos de trabajo a páginas](/help/sites-cloud/authoring/workflows/applying.md)
* [Participación en flujos de trabajo](/help/sites-cloud/authoring/workflows/participating.md)
