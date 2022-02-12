---
title: Arquitectura de AEM sin cabeza
description: Obtenga información sobre la arquitectura de alto nivel para Adobe Experience Manager en relación con una implementación sin periféricos. Comprenda la función de los servicios de AEM Author, Preview y Publish y el patrón de implementación recomendado para aplicaciones sin periféricos.
feature: Content Fragments,GraphQL API
source-git-commit: 64b2beb4af2297e19e39ad534856bce33ffcfcf8
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---


# Arquitectura de AEM sin cabeza

Un entorno de AEM típico está formado por un servicio de creación, un servicio de publicación y un servicio de vista previa opcional.

* **El servicio Autor** es donde los usuarios internos crean, administran y previsualizan contenido.

* **El servicio Publicar** se considera el entorno &quot;Activo&quot; y es lo que los usuarios finales interactúan con él. El contenido, después de editarse y aprobarse en el servicio Autor, se distribuye al servicio Publicar . El patrón de implementación más común con AEM aplicaciones sin periféricos es tener la versión de producción de la aplicación conectada a un servicio de AEM Publish.

* **El servicio Vista previa** funcionalmente es igual que la variable **Servicio de publicación**. Sin embargo, solo está disponible para usuarios internos. Esto lo convierte en un sistema ideal para que los aprobadores revisen los próximos cambios de contenido antes de que se realicen en directo para los usuarios finales.

* **Dispatcher** es un servidor web estático ampliado con el módulo AEM dispatcher. Proporciona capacidades de almacenamiento en caché y otra capa de seguridad. La variable **Dispatcher** se encuentra delante de **Publicación** y **Vista previa** servicios.

Dentro de un Programa as a Cloud Service AEM puede tener varios entornos, Dev, Stage y Prod. Cada entorno tendría su propio **Autor**, **Publicación** y **Vista previa** servicios. Puede obtener más información sobre la administración [entornos aquí](/help/implementing/cloud-manager/manage-environments.md)

## Modelo de publicación de autor

El patrón de implementación más común con AEM aplicaciones sin periféricos es tener la versión de producción de la aplicación conectada a un servicio de AEM Publish.

![Arquitectura de publicación de autor](assets/autho-publish-architecture-diagram.png)

El diagrama anterior muestra este patrón de implementación común.

1. A **Autor de contenido** utiliza el servicio AEM Author para crear, editar y administrar contenido.
1. La variable **Autor de contenido** y otros usuarios internos pueden obtener una vista previa del contenido directamente en el servicio Autor. Se puede configurar una versión de Vista previa de la aplicación que se conecte al servicio Autor.
1. Una vez aprobado el contenido, puede publicarse en el servicio de AEM Publish.
1. La variable **Dispatcher** es una capa delante de **Publicación** que puede almacenar en caché determinadas solicitudes y proporcionar una capa de seguridad.
1. Los usuarios finales interactúan con la versión de producción de la aplicación. La aplicación Producción se conecta al servicio Publicar a través de Dispatcher y utiliza las API de GraphQL para solicitar y consumir contenido.

## Creación Vista previa de la implementación de publicación

Otra opción para implementaciones sin encabezado es incorporar un **Vista previa de AEM** servicio. Con este enfoque, el contenido se puede publicar primero en la variable **Vista previa** y una versión de vista previa de la aplicación sin encabezado pueden conectarse a ella. La ventaja de este enfoque es que la variable **Vista previa** se puede configurar con los mismos requisitos y permisos de autenticación que el **Publicación** , lo que facilita la simulación de la experiencia de producción.

![Arquitectura de vista previa y publicación del autor](assets/author-preview-publish-architecture-diagram.png)

1. A **Autor de contenido** utiliza el servicio AEM Author para crear, editar y administrar contenido.
1. El contenido se publica primero en el servicio de vista previa de AEM.
1. Se puede configurar una versión de Vista previa de la aplicación que se conecte al servicio de Vista previa.
1. Una vez revisado y aprobado el contenido, puede publicarse en el servicio de AEM Publish.
1. Los usuarios finales interactúan con la versión de producción de la aplicación. La aplicación Producción se conecta al servicio Publicar a través de Dispatcher y utiliza las API de GraphQL para solicitar y consumir contenido.

