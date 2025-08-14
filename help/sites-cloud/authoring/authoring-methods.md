---
title: Métodos para crear contenido en AEM
description: Conozca las diferentes formas de crear contenido en AEM y en qué se diferencian.
feature: Authoring
exl-id: ef482843-451b-474e-a8d0-d0bfcc17221b
solution: Experience Manager Sites
role: User
source-git-commit: bb149cd43158bfd1ceb43b04cc536c8c8291f968
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 1%

---

# Métodos para crear contenido en AEM {#authoring-methods}

Conozca las diferentes formas de crear contenido en AEM, en qué se diferencian y cuándo puede utilizar una sobre la otra.

## Flexibilidad de creación de AEM {#authoring-flexibility}

AEM as a Cloud Service ofrece varios editores diferentes para editar diferentes tipos de contenido y admitir diferentes casos de uso de creación.

* [Creación de WYSIWYG con el editor universal](#universal-editor): el editor universal es una interfaz de usuario moderna que le permite crear contenido de AEM de forma independiente del contenido y está disponible para proyectos de AEM que usen Edge Delivery Services.
* [Creación de WYSIWYG con el editor de páginas](#page-editor): El editor de páginas es el editor clásico para crear contenido en AEM, probado y confiable para miles y miles de sitios web.
* [Creación basada en documentos](#document-based): si utiliza los servicios de Edge Delivery, puede optar por crear su contenido como documentos convencionales, como Microsoft Word o Google Docs, completamente fuera de las consolas de AEM.
* [Editor de fragmentos de contenido de AEM](#cf-editor): este es el editor de elección para crear contenido sin encabezado.

Debido al carácter integrado y escalable de AEM, estos métodos se pueden utilizar de forma exclusiva o en combinación según las necesidades del proyecto.

Consulte con el administrador del sistema o el administrador del proyecto si no está seguro de qué opciones de creación están disponibles para usted o si desea explorar nuevas opciones para crear contenido.

## Creación de WYSIWYG con el editor universal {#universal-editor}

El editor universal es una interfaz de usuario moderna que le permite crear contenido de AEM de forma independiente del contenido y es la primera opción para proyectos de AEM que aprovechan Edge Delivery Services.

![Editor universal](assets/authoring-methods-ue.png)

Se accede al editor universal a través de la consola Sitios en AEM, pero ofrece la potencia y la flexibilidad no solo independiente del contenido para crear contenido de AEM, sino también contenido externo correctamente instrumentado.

Para obtener más información acerca del editor universal, consulte el documento [Creación de contenido con el editor universal](/help/sites-cloud/authoring/universal-editor/authoring.md).

## Creación de WYSIWYG con el editor de páginas {#page-editor}

Este es el editor clásico para crear contenido en proyectos tradicionales de AEM, probados y en los que se confía para miles y miles de sitios web.

![Editor de páginas de AEM](assets/authoring-methods-page-editor.png)

El editor de páginas de AEM presenta un entorno integrado para crear contenido mediante una interfaz de lo que se ve es lo que se obtiene (WYSIWYG). Arrastre y suelte los componentes predefinidos para crear su página y editar el contenido in situ.

Para obtener más información acerca del editor de páginas de AEM, consulte el documento [Editor de páginas de AEM](/help/sites-cloud/authoring/page-editor/introduction.md).

## Creación basada en documentos  {#document-based}

Si utiliza los servicios de Edge Delivery, puede optar por crear su contenido como documentos convencionales, como Microsoft Word o Google Docs, completamente fuera de la consola [AEM **Sites**](/help/sites-cloud/authoring/sites-console/introduction.md).

![Edición de contenido basado en documentos](assets/authoring-methods-document.jpg)

Con la creación basada en documentos, los autores pueden utilizar las herramientas que ya conocen y seguir beneficiándose de la velocidad y el rendimiento del Edge Delivery Services de AEM para publicar su contenido. La creación basada en documentos no requiere el uso de la consola de AEM.

Para obtener más información acerca de la creación basada en documentos, consulte [Creación y publicación de contenido](https://www.aem.live/docs/aem-authoring).

## Editor de fragmentos de contenido de AEM {#cf-editor}

El editor de fragmentos de contenido de AEM es el editor de elección para crear contenido sin encabezado.

![Editor de fragmentos de contenido de AEM](assets/authoring-methods-cf-editor.png)

El editor de fragmentos de contenido de AEM presenta una interfaz clara para crear y administrar contenido estructurado, ideal para la entrega sin encabezado.

Para obtener más información acerca del editor de fragmentos de contenido de AEM, consulte los documentos [Administración de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/managing.md) y [Creación de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/managing.md).

>[!NOTE]
>
>El editor *new* que se resalta en esta sección no está disponible cuando se desarrolla localmente para AEM as a Cloud Service.
>
>El [*editor de fragmentos de contenido original*](/help/assets/content-fragments/content-fragments-variations.md) también está disponible.
