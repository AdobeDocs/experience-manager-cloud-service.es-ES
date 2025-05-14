---
title: Uso de Edge Delivery Services con AEM
description: Descubra cómo se puede utilizar AEM as a Cloud Service con Edge Delivery Services.
feature: Edge Delivery Services
exl-id: 41999302-b4c9-4f5a-b659-6e7398a3c4f4
role: Admin, Architect, Developer
index: false
hide: true
hidefromtoc: true
source-git-commit: e57610e4c5e498ddfdbaa0ba39c9197ecfb5d177
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 100%

---


# Uso de Edge Delivery Services con AEM {#using-edge}

Edge Delivery Services está disociado del origen de contenido y puede ingerir contenido de diferentes orígenes de contenido. Esto significa que puede trabajar con varios orígenes de contenido en el mismo sitio web con publicación optimizada y sin problemas, independientemente del origen elegido.

Con Edge Delivery Services, puede crear entornos de desarrollo rápidos en los que los autores pueden actualizar y publicar contenido rápidamente y en los que se pueden iniciar nuevos sitios rápidamente. Tan solo se tarda un par de segundos en pasar de la edición a ver el contenido en directo en Internet.

![Fuentes de contenido para Edge Delivery](assets/content-sources.png)

La ingesta desde múltiples fuentes de contenido ofrece la máxima flexibilidad al usuario.  Adobe ofrece directrices para ayudarle a elegir las fuentes de contenido que mejor se adaptan a su proyecto.

Hay casos en los que el origen de contenido está predefinido o no es flexible (por ejemplo, el proyecto no puede utilizar Sharepoint o Google Drive). Pero en muchos casos, la herramienta no está predeterminada y la elección de la herramienta no es evidente.

El principio rector del Adobe es la simplicidad.  Empiece por la creación basada en documentos y añada complejidad cuando sea necesario.  Si se necesita un cambio de herramienta, la integración de Edge Delivery Services de AEM cubre la migración de contenido.

![Flexibilidad de fuente de contenido](assets/content-source-flexiblity.png)

## Creación {#authoring-edge}

Con Edge Delivery Services, la creación es fácil, rápida y flexible.  Puede optar por crear utilizando la creación basada en documentos o la creación WYSIWYG con el editor universal.

Consulte el documento [Creación de contenido para Edge Delivery Services](/help/edge/wysiwyg-authoring/authoring.md) para obtener más información.

## Publicación {#publishing-edge}

Con Edge Delivery Services, la publicación de contenido se realiza sin problemas independientemente de la fuente de contenido. 

Consulte el documento [Publicación de contenido para Edge Delivery Services](/help/edge/wysiwyg-authoring/publishing.md) para obtener más información.

## El desarrollo de {#developing-edge}

Edge Delivery Services se basa en el concepto de bloques. AEM incluye una completa biblioteca de bloques predefinidos, que se puede ampliar para satisfacer las necesidades de cada proyecto.  El código de los proyectos de Edge Delivery Services se administra en GitHub.

Consulte el documento [Guía de introducción del desarrollador para la creación WYSIWYG con Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) para obtener más información.
