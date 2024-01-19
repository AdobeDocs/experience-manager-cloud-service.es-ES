---
title: Personalización de la IU
description: Obtenga información acerca de los diferentes puntos de extensión que le permiten personalizar la interfaz de usuario del editor universal para satisfacer las necesidades de los autores de contenido.
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
source-git-commit: 7ef3efa6e074778b7b3e3a8159056200b2663b30
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 0%

---


# Personalización de la IU {#customizing-ui}

Obtenga información acerca de los diferentes puntos de extensión que le permiten personalizar la interfaz de usuario del editor universal para satisfacer las necesidades de los autores de contenido.

## Desactivación de publicación {#disable-publish}

Algunos flujos de trabajo de creación requieren que el contenido se revise antes de publicarse. En estos casos, la opción para publicar no debe estar disponible para ningún autor.

El **Publish** por lo tanto, el botón se puede suprimir por completo en una aplicación añadiendo los siguientes metadatos.

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```
