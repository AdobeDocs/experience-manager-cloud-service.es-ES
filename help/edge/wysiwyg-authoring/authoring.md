---
title: Creación de contenido de WYSIWYG para Edge Delivery Services
description: Descubra cómo funciona la creación de contenido con los Edge Delivery Services y cómo crear contenido de AEM con los Edge Delivery Services.
feature: Edge Delivery Services
exl-id: 963ff71a-8176-4d9d-8240-dc429405d139
role: User
source-git-commit: a7b48559e5bf60c86fecd73a8bcef6c9aaa03b80
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 61%

---


# Creación de contenido de WYSIWYG para Edge Delivery Services {#authoring-edge}

Con Edge Delivery Services, la creación es fácil, rápida y flexible.  Tiene dos opciones para crear contenido para Edge Delivery Services:

* [Editor universal](#universal-editor): una interfaz de usuario moderna de lo que se ve es lo que se obtiene (WYSIWYG AEM) para crear contenido dentro de la interfaz de usuario de la creación de contenido de la interfaz de usuario de la interfaz de usuario de
* [Creación basada en documentos](#document-based), como Microsoft Word o Google Docs

## Creación del Editor universal {#universal-editor}

Cuando se utilizan Edge Delivery Services con AEM as a Cloud Service, el hecho más fundamental para comprender es que el contenido que crea persiste en AEM as a Cloud Service.

![Funcionamiento de la creación de WYSIWYG con Edge Delivery Services](assets/how-aem-edge-works.png)

1. [El entorno de AEM Sites](/help/sites-cloud/authoring/quick-start.md) se usa para administrar contenido, por ejemplo, para crear páginas nuevas, fragmentos de experiencias, fragmentos de contenido, etc.
   * Todas las funciones de AEM están disponibles, como flujos de trabajo, MSM, traducción, lanzamientos, etc.
1. [El editor universal](/help/sites-cloud/authoring/universal-editor/authoring.md) se utiliza para crear el contenido gestionado en AEM.
   * El editor universal ofrece una interfaz de usuario nueva y moderna para la creación de contenido.
   * Para la creación, AEM procesa el HTML, pero incluye los scripts, estilos, iconos y otros recursos de los Edge Delivery Services.
   * Aunque se utiliza el Editor universal, todos los cambios se mantienen en AEM.
   * El editor universal aún no tiene paridad de características con el editor de páginas de AEM y es posible que algunas características de AEM no estén disponibles en el editor universal.
1. El contenido que crea con el editor universal y persiste en AEM se publica en los Edge Delivery Services.
   * El contenido permanece almacenado en AEM.
   * AEM renderiza el HTML semántico necesario para la ingesta.
   * El contenido se publica en Edge Delivery Services.
1. [Edge Delivery Services](/help/edge/developer/keeping-it-100.md) garantizan una puntuación del 100 % en Lighthouse.

Los bloques son componentes fundamentales de una página que envían los Edge Delivery Services. Los autores pueden elegir entre bloques predeterminados proporcionados como estándar por Adobe o entre bloques personalizados para su proyecto por los desarrolladores.

El editor universal proporciona una interfaz gráfica de usuario moderna e intuitiva para crear su contenido mediante la adición y organización de bloques.

![Agregar y organizar bloques en el editor universal](assets/blocks.png)

Los detalles de los bloques se pueden configurar en el panel Propiedades.

![Configuración de propiedades de bloque](assets/block-properties.png)

Para obtener más información sobre cómo crear contenido con el editor universal, consulte el documento [Creación de contenido con el editor universal.](/help/sites-cloud/authoring/universal-editor/authoring.md)

Consulte la [Guía de introducción para desarrolladores para la creación de WYSIWYG con Edge Delivery Services AEM](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) para aprender a iniciar su propio proyecto de creación con Edge Delivery Services de y con los que crear su propio proyecto de manera que se pueda crear con los desarrolladores de y con los que se pueda crear un proyecto de manera más sencilla.

## Métodos de creación adicionales  {#authoring-methods}

La creación de WYSIWYG es una herramienta potente e intuitiva para autores de contenido. AEM Sin embargo, hay muchos casos de uso de creación diferentes, por lo que ofrece soluciones de creación adicionales, por lo que los trabajos de creación de documentos se ofrecen de manera más sencilla.

AEM Consulte el documento [Elección de un método de creación](/help/edge/authoring-methods.md) para obtener más información acerca de las soluciones de creación que ofrece, incluidas las ofertas de creación basada en documentos y sin encabezado.
