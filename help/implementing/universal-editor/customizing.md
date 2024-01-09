---
title: Personalización de la IU
description: Obtenga información acerca de los diferentes puntos de extensión que le permiten personalizar la interfaz de usuario del editor universal para satisfacer las necesidades de los autores de contenido.
source-git-commit: 65893c0c0dee37bed8ecfbb06a12e7c093c4397c
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
