---
title: 'Cómo ponerlo todo juntos: su aplicación y su contenido en AEM sin cabeza'
description: En esta parte del Recorrido para desarrolladores sin encabezado de AEM, aprenda a tomar su proyecto de AEM, incluidos los fragmentos de contenido, las llamadas de GraphQL, las llamadas a la API de REST y la aplicación, y prepárelo para su lanzamiento.
exl-id: bece84ad-4c8c-410c-847e-9ef3f79970cb
source-git-commit: 270eb35023e34eed2cd17674372794c6c2cc7757
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 7%

---

# Cómo ponerlo todo juntos: su aplicación y su contenido en AEM sin cabeza {#put-it-all-together}

En esta parte del [recorrido para desarrolladores AEM sin encabezado](overview.md), se familiariza con cómo utilizar las herramientas de desarrollo de AEM y el SDK sin encabezado para agrupar la aplicación.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido sin AEM, [Cómo actualizar su contenido a través de las API de AEM Assets](update-your-content.md) ha aprendido a actualizar el contenido sin encabezado existente en AEM mediante API y ahora debería:

* Comprender la API HTTP de AEM Assets.

## Objetivo {#objective}

El objetivo de este artículo es ayudarle a comprender cómo agrupar su aplicación sin encabezado de AEM mediante:

* Información sobre el SDK sin AEM y la herramienta de desarrollo necesaria
* Configuración de un tiempo de ejecución de desarrollo local para simular el contenido antes de lanzarse
* Aspectos básicos de la replicación AEM contenido

## El SDK AEM {#the-aem-sdk}

El SDK de AEM se utiliza para crear e implementar código personalizado. Es la principal herramienta que necesita para desarrollar y probar su aplicación sin encabezado antes de lanzarse. Contiene los siguientes artefactos:

* El Jar de inicio rápido: un archivo jar ejecutable que puede utilizarse para configurar una instancia de autor y de publicación
* Herramientas de Dispatcher: el módulo de Dispatcher y sus dependencias para los sistemas basados en Windows y UNIX®
* Jar de la API de Java™: la dependencia Java™ Jar/Maven que expone todas las API de Java™ permitidas que se pueden usar para desarrollar con AEM
* Javadoc jar: los javadocs para el jar de la API de Java™

## El SDK sin AEM {#the-aem-headless-sdk}

A diferencia del SDK de AEM, la AEM **SDK sin encabezado** es un conjunto de bibliotecas que los clientes pueden utilizar para interactuar rápida y fácilmente con las API sin encabezado AEM a través de HTTP.

Para obtener más información sobre el SDK AEM sin encabezado, consulte la [documentación aquí](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/how-to/aem-headless-sdk.html?lang=en).

## Herramientas de desarrollo adicionales {#additional-development-tools}

Además del SDK de AEM, necesitará herramientas adicionales que faciliten el desarrollo y la prueba del código y el contenido localmente:

* Java™
* Git
* Maven Apache
* La biblioteca Node.js
* El IDE de su elección

Como AEM es una aplicación Java™, debe instalar Java™ y el SDK de Java™ para admitir el desarrollo de AEM as a Cloud Service.

Git es lo que utilizará para administrar el control de código fuente y para registrar los cambios en Cloud Manager y luego implementarlos en una instancia de producción.

AEM utiliza Apache Maven para crear proyectos generados a partir del tipo de archivo del proyecto Maven de AEM. Todos los IDE principales proporcionan compatibilidad con la integración de Maven.

Node.js es un entorno de tiempo de ejecución de JavaScript que se utiliza para trabajar con los recursos del front-end de un proyecto de AEM `ui.frontend` subproyecto. Node.js se distribuye con npm, es el administrador de paquetes Node.js de facto, que se utiliza para administrar las dependencias de JavaScript.

## Componentes de un sistema AEM de un vistazo {#components-of-an-aem-system-at-a-glance}

A continuación, echemos un vistazo a las partes constitutivas de un entorno AEM.

Un entorno de AEM completo está formado por un Autor, una Publicación y un Dispatcher. Estos mismos componentes están disponibles en el tiempo de ejecución del desarrollo local para que le resulte más fácil previsualizar el código y el contenido antes de lanzarse.

* **El servicio de creación** es donde los usuarios internos crean, administran y previsualizan contenido.

* **El servicio de publicación** se considera el entorno “activo” y suele ser con el que interactúan los usuarios finales. El contenido, después de editarse y aprobarse en el servicio de creación, se distribuye al de publicación. El patrón de implementación más común con las aplicaciones sin encabezado de AEM es tener la versión de producción de la aplicación conectada a un servicio de publicación de AEM.

* **Dispatcher** es un servidor web estático ampliado con el módulo AEM de Dispatcher. Almacena en caché las páginas web producidas por la instancia de publicación para mejorar el rendimiento.

## Flujo de trabajo de desarrollo local {#the-local-development-workflow}

El proyecto de desarrollo local se basa en Apache Maven y utiliza Git para el control de código fuente. Para actualizar el proyecto, los desarrolladores pueden utilizar su entorno de desarrollo integrado preferido, como Eclipse, Visual Studio Code o IntelliJ, entre otros.

Para probar las actualizaciones de código o contenido que ingerirá la aplicación sin encabezado, debe implementar las actualizaciones en el tiempo de ejecución de AEM local, que incluye instancias locales del autor de AEM y los servicios de publicación.

Asegúrese de tomar nota de las distinciones entre cada componente en el tiempo de ejecución de AEM local, ya que es importante probar las actualizaciones donde más importen. Por ejemplo, pruebe las actualizaciones de contenido en la instancia de autor o pruebe el nuevo código en la instancia de publicación.

En un sistema de producción, un Dispatcher y un servidor http Apache siempre se sentarán frente a una instancia de publicación AEM. Proporcionan almacenamiento en caché y servicios de seguridad para el sistema AEM, por lo que es fundamental probar el código y las actualizaciones de contenido para Dispatcher también.

## Vista previa del código y el contenido localmente con el entorno de desarrollo local {#previewing-your-code-and-content-locally-with-the-local-development-environment}

Para preparar el proyecto sin AEM para su lanzamiento, debe asegurarse de que todas las partes constitutivas del proyecto funcionen correctamente.

Para ello, hay que juntar todo: código, contenido y configuración, y pruébelo en un entorno de desarrollo local para estar preparado para la puesta en marcha.

El entorno de desarrollo local consta de tres esferas principales:

1. El proyecto AEM: esto contendrá todo el código personalizado, la configuración y el contenido en el que los desarrolladores de AEM estarán trabajando
1. Local AEM Runtime: versiones locales de los servicios de publicación y autor de AEM que se utilizarán para implementar código del proyecto de AEM
1. Tiempo de ejecución de Dispatcher local: versión local del servidor web Apache htttpd que incluye el módulo de Dispatcher.

Una vez configurado el entorno de desarrollo local, puede simular el contenido que sirve en la aplicación React mediante la implementación local de un servidor Nodo estático.

Para obtener una vista más detallada sobre la configuración de un entorno de desarrollo local y todas las dependencias necesarias para la vista previa del contenido, consulte [Documentación de implementación de producción](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/production-deployment.html?lang=en#prerequisites).

## Siguientes pasos {#whats-next}

Ahora que ha completado esta parte del Recorrido para desarrolladores sin encabezado de AEM, debe:

* Familiarícese con las herramientas de desarrollo de AEM
* Comprender el flujo de trabajo de desarrollo local

Debe continuar con su recorrido sin AEM para la próxima revisión del documento [Cómo vivir con tu aplicación sin encabezado](/help/journey-headless/developer/go-live.md) ¡donde realmente tomas tu proyecto sin AEM en vivo!

## Recursos adicionales {#additional-resources}

* [El SDK as a Cloud Service AEM](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
* [Configuración De Un Entorno AEM Local](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html?lang=es)
* [AEM SDK sin encabezado para exploradores del lado del cliente (JavaScript)](https://github.com/adobe/aem-headless-client-js)
* [AEM SDK sin encabezado para server-side/Node.js (JavaScript)](https://github.com/adobe/aem-headless-client-nodejs)
* [AEM SDK sin encabezado para Java™](https://github.com/adobe/aem-headless-client-java)

