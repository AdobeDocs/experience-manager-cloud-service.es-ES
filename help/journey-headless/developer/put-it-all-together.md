---
title: 'Cómo ponerlo todo junto: su aplicación y su contenido en AEM sin encabezado'
description: En esta parte del recorrido para desarrolladores de contenido de AEM sin encabezado, aprenda a lanzar su proyecto de AEM, incluidos los fragmentos de contenido, las llamadas de GraphQL, las llamadas de la API REST y la aplicación, para prepararlo para su puesta en marcha.
exl-id: bece84ad-4c8c-410c-847e-9ef3f79970cb
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 100%

---

# Cómo ponerlo todo junto: su aplicación y su contenido en AEM sin encabezado {#put-it-all-together}

En esta parte del [recorrido para desarrolladores de contenido de AEM sin encabezado](overview.md), se familiarizará con cómo utilizar las herramientas de desarrollo de AEM y el SDK sin encabezado para montar la aplicación.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido de AEM sin encabezado, [Cómo actualizar su contenido a través de las API de AEM Assets](update-your-content.md) ha aprendido a actualizar el contenido sin encabezado existente en AEM mediante la API y ahora debería:

* Comprender la API HTTP de AEM Assets.

## Objetivo {#objective}

El objetivo de este artículo es ayudarle a comprender cómo montar su aplicación sin encabezado de AEM mediante lo siguiente:

* Información sobre el SDK de AEM sin encabezado y las herramientas de desarrollo necesarias
* Configuración de un tiempo de ejecución de desarrollo local para simular el contenido antes de su puesta en marcha
* Conceptos básicos de la replicación de contenido de AEM

## El SDK de AEM {#the-aem-sdk}

El SDK de AEM se utiliza para crear e implementar código personalizado. Es la principal herramienta que necesita para que pueda desarrollar y probar su aplicación sin encabezado antes de ponerla en marcha. Contiene los siguientes artefactos:

* Jar de inicio rápido: un archivo Jar ejecutable que se puede utilizar para configurar una instancia de autor y de publicación
* Herramientas de Dispatcher: el módulo de Dispatcher y sus dependencias para los sistemas basados en Windows y UNIX®
* Jar de API de Java™: la dependencia Jar/Maven de Java™ que expone todas las API de Java™ permitidas que se pueden usar para desarrollarse con AEM
* Javadoc jar: los javadocs para el Jar de la API de Java™

## El SDK de AEM sin encabezado {#the-aem-headless-sdk}

A diferencia del SDK de AEM, el **SDK sin encabezado** de AEM es un conjunto de bibliotecas que los clientes pueden utilizar para interactuar rápida y fácilmente con las API de AEM sin encabezado través de HTTP.

Para obtener más información, consulte [SDK de AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/aem-headless-sdk.html?lang=es).

## Herramientas de desarrollo adicionales {#additional-development-tools}

Además del SDK de AEM, necesita herramientas adicionales que faciliten el desarrollo y las pruebas del código y el contenido de forma local:

* Java™
* Git
* Apache Maven
* La biblioteca Node.js
* El IDE de su elección

Como AEM es una aplicación Java™, debe instalar Java™ y el SDK de Java™ para que permitir el desarrollo de AEM as a Cloud Service.

Git es lo que se utiliza para administrar el control de origen y para registrar los cambios en Cloud Manager y luego implementarlos en una instancia de producción.

AEM utiliza Apache Maven para crear proyectos generados a partir del arquetipo del proyecto Maven de AEM. Todos los IDE principales proporcionan compatibilidad con la integración de Maven.

Node.js es un entorno de tiempo de ejecución de JavaScript que se utiliza para trabajar con los recursos front-end de un subproyecto `ui.frontend` del proyecto de AEM. Node.js se distribuye con npm, es el administrador de paquetes de Node.js de facto, que se utiliza para administrar las dependencias de JavaScript.

## Generalidades de los componentes del sistema AEM {#components-of-an-aem-system-at-a-glance}

A continuación, veremos las partes que constituyen el entorno de AEM.

Un entorno de AEM completo está formado por un Autor, una Publicación y un Dispatcher. Estos mismos componentes están disponibles durante la ejecución del desarrollo local para que le resulte más fácil previsualizar el código y el contenido antes de ponerlo en marcha.

* **El servicio de creación** es donde los usuarios internos crean, administran y previsualizan contenido.

* **El servicio de publicación** se considera el entorno “activo” y suele ser con el que interactúan los usuarios finales. El contenido, después de editarse y aprobarse en el servicio de creación, se distribuye al de publicación. El patrón de implementación más común con las aplicaciones sin encabezado de AEM es tener la versión de producción de la aplicación conectada a un servicio de publicación de AEM.

* **Dispatcher** es un servidor web estático ampliado con el módulo Dispatcher de AEM. Almacena en la caché las páginas web producidas por la instancia de publicación para mejorar el rendimiento.

## Flujo de trabajo de desarrollo local {#the-local-development-workflow}

El proyecto de desarrollo local se basa en Apache Maven y utiliza Git para el control de código fuente. Para actualizar el proyecto, los desarrolladores pueden utilizar su entorno de desarrollo integrado preferido, como Eclipse, Visual Studio Code o IntelliJ, entre otros.

Para probar las actualizaciones de código o contenido introducidas por la aplicación sin encabezado, debe implementar las actualizaciones en el tiempo de ejecución de AEM local, que incluye las instancias locales de los servicios de creación y publicación de AEM.

Asegúrese de tomar nota de las distinciones entre cada componente en el tiempo de ejecución de AEM local, ya que es vital probar las actualizaciones allí donde sean más importantes. Por ejemplo, pruebe las actualizaciones de contenido en la instancia de autor o pruebe el nuevo código en la instancia de publicación.

En un sistema de producción, Dispatcher y el servidor de HTTP, Apache, siempre estarán frente a una instancia de publicación de AEM. Proporcionan almacenamiento en caché y servicios de seguridad para el sistema AEM, por lo que es fundamental probar el código y las actualizaciones de contenido para Dispatcher también.

## Vista previa del código y el contenido localmente con el entorno de desarrollo local {#previewing-your-code-and-content-locally-with-the-local-development-environment}

Para preparar el proyecto AEM sin encabezado para su lanzamiento, debe asegurarse de que todas las partes constitutivas del proyecto funcionen correctamente.

Para ello, hay que juntar todo: código, contenido y configuración, y probarlo en un entorno de desarrollo local para estar preparado para la puesta en marcha.

El entorno de desarrollo local consta de tres esferas principales:

1. El proyecto de AEM: este proyecto contiene todo el código, la configuración y el contenido personalizados en los que los desarrolladores de AEM van a trabajar.
1. El tiempo de ejecución local de AEM: versiones locales de los servicios de publicación y autor de AEM que se utilizan para implementar código del proyecto de AEM.
1. Tiempo de ejecución de Dispatcher local: una versión local del HTTPD del servidor web Apache que incluye el módulo de Dispatcher.

Una vez configurado el entorno de desarrollo local, puede simular el contenido que sirve en la aplicación React mediante la implementación local de un servidor de nodo estático.

<!-- THIS TOPIC IS 404. IT DOES NOT APPEAR IN THE TOC OR ANYWHERE ELSE To get a more in-depth look at setting up a local development environment and all dependencies needed for content preview, see [Production Deployment documentation](https://experienceleague.adobe.com/docs/experience-manager-learn/headless-tutorial/graphql/multi-step/production-deployment.html). -->

## Siguientes pasos {#whats-next}

Ahora que ha completado esta parte del recorrido para desarrolladores de AEM sin encabezado, debería poder hacer lo siguiente:

* Familiarizarse con las herramientas de desarrollo de AEM.
* Comprender el flujo de trabajo de desarrollo local.

Continúe con su recorrido de AEM sin encabezado revisando a continuación el documento [Cómo poner en marcha su aplicación Headless](/help/journey-headless/developer/go-live.md) donde realmente pone en marcha su proyecto de AEM sin encabezado.

## Recursos adicionales {#additional-resources}

* [SDK de AEM as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
* [Configuración de un entorno de AEM local](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html?lang=es)
* [SDK de AEM sin encabezado para exploradores del lado del cliente (JavaScript)](https://github.com/adobe/aem-headless-client-js)
* [SDK de AEM sin encabezado del lado del servidor/Nodo.js (JavaScript)](https://github.com/adobe/aem-headless-client-nodejs)
* [SDK de AEM sin encabezado para Java™](https://github.com/adobe/aem-headless-client-java)
* [Introducción a AEM como CMS sin encabezado](/help/headless/introduction.md)
* [Portal para desarrolladores de AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=es)
* [Tutoriales de AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=es)
