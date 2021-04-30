---
title: 'Cómo ponerlo todo juntos: su aplicación y su contenido en AEM sin cabeza'
description: En esta parte del Recorrido para desarrolladores sin encabezado de AEM, aprenda a tomar su proyecto de AEM, incluidos los fragmentos de contenido, las llamadas de GraphQL, las llamadas a la API de REST y la aplicación, y prepárelo para su lanzamiento.
hide: true
hidefromtoc: true
index: false
exl-id: 254fb9dd-36c8-43ce-aaea-ceb4d079503d
translation-type: tm+mt
source-git-commit: e8eb9d2c96d24601e50c48f6846a8c8bac8b0252
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 0%

---

# Cómo ponerlo todo juntos: su aplicación y su contenido en AEM sin encabezado {#put-it-all-together}

>[!CAUTION]
>
>TRABAJO EN CURSO - La creación de este documento está en curso y no debe entenderse como completo o definitivo ni debe utilizarse con fines de producción.

En esta parte del [AEM Recorrido para desarrolladores sin encabezado,](overview.md) aprenda a utilizar su proyecto de AEM, incluidos los fragmentos de contenido, las llamadas de GraphQL, las llamadas a la API de REST y la aplicación, y a prepararlo para su lanzamiento.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido sin AEM encabezado, [How to Update Your Content via AEM Assets APIs](update-your-content.md), ha aprendido a actualizar el contenido sin encabezado existente en AEM mediante API y ahora debería:

* Comprender la API HTTP de AEM Assets.

Este artículo se basa en estos fundamentos para que entienda cómo preparar su propio proyecto sin objetivos AEM para su lanzamiento.

## Objetivo {#objective}

* Comprender qué es el flujo de trabajo de desarrollo local para AEM
* Instale el SDK de AEM para obtener un tiempo de ejecución de desarrollo local que pueda utilizar para probar el contenido en
* Obtenga información sobre las herramientas de desarrollo que debe tener para trabajar junto al tiempo de ejecución del desarrollo local

## Flujo de trabajo de desarrollo local {#the-local-development-workflow}

El proyecto de desarrollo local se basa en Apache Maven y utiliza Git para el control de código fuente. Para actualizar el proyecto, los desarrolladores pueden utilizar su entorno de desarrollo integrado preferido, como Eclipse, Visual Studio Code o IntelliJ, entre otros.

Para probar las actualizaciones de código o contenido que ingerirá la aplicación sin encabezado, debe implementar las actualizaciones en un tiempo de ejecución de AEM local, que incluye instancias locales de las instancias de autor y publicación de AEM.

Asegúrese de tener en cuenta las distinciones entre cada componente en el tiempo de ejecución de AEM local, ya que es importante probar las actualizaciones donde más importen, por ejemplo, probar las actualizaciones de contenido en el autor o probar el nuevo código en la instancia de publicación.

En un sistema de producción, un Dispatcher y un servidor http Apache siempre se sentarán frente a una instancia de publicación AEM. Proporcionan almacenamiento en caché y servicios de seguridad para el sistema AEM, por lo que es fundamental probar el código y las actualizaciones de contenido para el despachante.

Una vez que se haya probado todo y funcione correctamente, estará listo para insertar las actualizaciones de código en un repositorio Git centralizado en Cloud Manager.

Una vez cargadas las actualizaciones en Cloud Manager, se pueden implementar en AEM como Cloud Service mediante la canalización de CD/CI de Cloud Manager.


## El SDK de AEM {#the-aem-sdk}

El SDK de AEM se utiliza para crear e implementar código personalizado. Contiene los siguientes artefactos:

* El Jar de inicio rápido: un archivo jar ejecutable que puede utilizarse para configurar una instancia de autor y de publicación
* Herramientas de Dispatcher: el módulo de Dispatcher y sus dependencias para sistemas basados en Windows y UNIX
* Java API Jar : la dependencia Java Jar/Maven que expone todas las API de Java permitidas que se pueden usar para desarrollar con AEM
* Javadoc jar: los javadocs para el jar de la API de Java

## Configuración del entorno de desarrollo local {#local-development-environment}

Para preparar el proyecto sin AEM para su lanzamiento, debe asegurarse de que todas las partes constitutivas del proyecto funcionen correctamente.

Para ello, debe juntar todo: código, contenido y configuración, y probarlo en un entorno de desarrollo local para estar preparado para la puesta en marcha.

El entorno de desarrollo local consta de tres esferas principales:

1. El proyecto AEM: esto contendrá todo el código personalizado, la configuración y el contenido en el que los desarrolladores de AEM estarán trabajando
1. Local AEM Runtime: versiones locales de los servicios de publicación y autor de AEM que se utilizarán para implementar código del proyecto de AEM
1. Tiempo de ejecución de Dispatcher local: versión local del servidor web Apache htttpd que incluye el módulo de Dispatcher.

## Herramientas de desarrollo {#development-tools}

Además del SDK de AEM, necesitará herramientas adicionales que faciliten el desarrollo y la prueba del código y el contenido localmente:

* Java
* Git
* Maven Apache
* La biblioteca Node.js
* El IDE de su elección

Como AEM es una aplicación Java, debe instalar Java y el SDK de Java para admitir el desarrollo de AEM como Cloud Service.

Git es la herramienta que utilizará para administrar el control de código fuente, así como para registrar los cambios en Cloud Manager y luego implementarlos en una instancia de producción.

AEM utiliza Apache Maven para crear proyectos generados a partir del tipo de archivo del proyecto Maven de AEM. Todos los IDE principales proporcionan compatibilidad con la integración de Maven.

Node.js es un entorno de tiempo de ejecución de JavaScript que se utiliza para trabajar con los recursos front-end del subproyecto ui.frontend de un proyecto AEM. Node.js se distribuye con npm, es el administrador de paquetes Node.js de facto, que se utiliza para administrar las dependencias de JavaScript.

## Siguientes {#what-is-next}

Debería continuar con su recorrido sin AEM al revisar el documento [How to Go Live with Your Headless Application](go-live.md) en el que realmente se lleva su proyecto sin encabezado de AEM.

## Recursos adicionales {#additional-resources}

* [Configuración del entorno de desarrollo local](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-dispatcher-runtime) : Aprenda a instalar las herramientas necesarias para empezar a desarrollarse para AEM
* [AEM como SDK de Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) : eche un vistazo al SDK de AEM