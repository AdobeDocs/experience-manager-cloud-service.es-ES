---
title: AEM Métodos para crear contenido en el
description: AEM Conozca las diferentes formas en que puede crear contenido en las listas de contenido y en qué se diferencian.
feature: Authoring
exl-id: ef482843-451b-474e-a8d0-d0bfcc17221b
solution: Experience Manager Sites
role: User
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# AEM Métodos para crear contenido en el {#authoring-methods}

AEM Conozca las diferentes formas en que puede crear contenido en las listas, en qué se diferencian y cuándo puede utilizar una sobre la otra.

## AEM Flexibilidad de creación de {#authoring-flexibility}

AEM as a Cloud Service ofrece varios editores diferentes para editar diferentes tipos de contenido y admitir diferentes casos de uso de creación.

* [Creación de WYSIWYG AEM con el editor de páginas](#page-editor): El editor de páginas es el editor clásico para crear contenido en el mundo, probado y confiable en miles y miles de sitios web.
* [Creación de WYSIWYG AEM AEM con el editor universal](#universal-editor): el editor universal es una interfaz de usuario moderna que le permite crear contenido de manera independiente del contenido y está disponible para proyectos de la comunidad que aprovechan a los Edge Delivery Services de la aplicación de la.
* [Creación basada en documentos](#document-based): si utiliza los servicios de Edge Delivery, puede optar por crear su contenido como documentos convencionales, como Microsoft Word o Google Docs AEM, completamente fuera de las consolas de.
* AEM [Editor de fragmentos de contenido de](#cf-editor): este es el editor que se elige para crear contenido sin encabezado.

AEM Debido a la naturaleza integrada y escalable de los métodos, estos se pueden utilizar de forma exclusiva o en combinación entre sí según las necesidades del proyecto.

Consulte con el administrador del sistema o el administrador del proyecto si no está seguro de qué opciones de creación están disponibles para usted o si desea explorar nuevas opciones para crear contenido.

## Creación de WYSIWYG con el editor de páginas {#page-editor}

AEM Este es el editor clásico para la creación de contenido en el que se ha intentado y en el que se confía desde hace miles y miles de sitios web.

AEM ![Editor de páginas de la página de la](assets/authoring-methods-page-editor.png)

AEM El editor de páginas de presenta un entorno integrado para crear contenido mediante una interfaz de lo que se ve es lo que se obtiene (WYSIWYG). Arrastre y suelte los componentes predefinidos para crear su página y editar el contenido in situ.

AEM AEM Para obtener más información acerca del editor de páginas de la página de la, consulte el documento [Editor de páginas de la](/help/sites-cloud/authoring/page-editor/introduction.md).

## Creación de WYSIWYG con el editor universal {#universal-editor}

AEM AEM El editor universal es una interfaz de usuario moderna que le permite crear contenido de manera independiente del contenido, y es la primera opción para crear proyectos que aprovechen los Edge Delivery Services de la aplicación de manera independiente del contenido.

![Editor universal](assets/authoring-methods-ue.png)

AEM AEM Se accede al editor universal a través de la consola Sites dentro de la interfaz de usuario de, pero ofrece la potencia y la flexibilidad independiente del contenido para crear no solo el contenido de la, sino también el contenido externo correctamente instrumentado.

Para obtener más información acerca del editor universal, consulte el documento [Creación de contenido con el editor universal](/help/sites-cloud/authoring/universal-editor/authoring.md).

## Creación basada en documentos  {#document-based}

Si usa los servicios de Edge Delivery, puede optar por crear su contenido como documentos convencionales, como Microsoft Word o Google Docs AEM, completamente fuera de la consola [**Sites**](/help/sites-cloud/authoring/sites-console/introduction.md).

![Edición de contenido basado en documentos](assets/authoring-methods-document.jpg)

AEM Con la creación basada en documentos, los creadores pueden utilizar las herramientas que ya conocen y seguir beneficiándose de la velocidad y el rendimiento de los Edge Delivery Services de la publicación de contenido de los documentos de los que se dispone en el sitio de trabajo de los autores de manera que puedan publicar su contenido. AEM La creación basada en documentos no requiere el uso de la consola de.

Para obtener más información acerca de la creación basada en documentos, consulte [Creación y publicación de contenido](/help/edge/docs/authoring.md).

## AEM Editor de fragmentos de contenido {#cf-editor}

AEM El editor de fragmentos de contenido es el editor de elección para crear contenido sin encabezado.

AEM ![Editor de fragmentos de contenido de la aplicación](assets/authoring-methods-cf-editor.png)

AEM El editor de fragmentos de contenido de la aplicación presenta una interfaz clara para crear y administrar contenido estructurado, ideal para la entrega sin encabezado.

AEM Para obtener más información acerca del editor de fragmentos de contenido de la, consulte los documentos [Administración de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/managing.md) y [Creación de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/managing.md).

>[!NOTE]
>
>El editor *new* que se resalta en esta sección no está disponible cuando se desarrolla localmente para AEM as a Cloud Service.
>
>El [*editor de fragmentos de contenido original*](/help/assets/content-fragments/content-fragments-variations.md) también está disponible.
