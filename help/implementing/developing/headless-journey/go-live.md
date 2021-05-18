---
title: Cómo vivir con tu aplicación sin encabezado
description: En esta parte del Recorrido para desarrolladores sin encabezado de AEM, aprenda a implementar una aplicación sin encabezado en vivo tomando su código local en Git y mudándolo a Cloud Manager Git para la canalización CI/CD.
hide: true
hidefromtoc: true
index: false
exl-id: f79b5ada-8f59-4706-9f90-bc63301b2b7d
source-git-commit: 4c743eede23f09f285d9da84b149226f7288fcc3
workflow-type: tm+mt
source-wordcount: '1886'
ht-degree: 0%

---

# Cómo poner en marcha su aplicación sin encabezado {#go-live}

>[!CAUTION]
>
>TRABAJO EN CURSO - La creación de este documento está en curso y no debe entenderse como completo o definitivo ni debe utilizarse con fines de producción.

En esta parte del [AEM Recorrido para desarrolladores sin encabezado](overview.md), aprenda a implementar una aplicación sin encabezado en vivo tomando su código local en Git y moviéndolo a Cloud Manager Git para la canalización CI/CD.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido sin AEM encabezado, [How to Put it All Together - Your App and Your Content in AEM Headless](put-it-all-together.md) ha aprendido a preparar su propio proyecto sin objetivos AEM para que se ponga en marcha y ahora debería:

* Comprender los requisitos para ponerse en marcha.

Este artículo se basa en estos fundamentos para que entienda cómo llevar su proyecto sin encabezado de AEM en vivo.

## Objetivo {#objective}

Este documento le ayuda a comprender la canalización de publicación sin AEM y las consideraciones de rendimiento que debe tener en cuenta antes de empezar a trabajar con la aplicación.

* Obtenga información sobre el SDK de AEM y las herramientas de desarrollo necesarias
* Configure un motor de ejecución de desarrollo local para simular el contenido antes de lanzarlo
* Comprender los conceptos básicos AEM replicación de contenido y almacenamiento en caché
* Asegurar y escalar la aplicación antes de Launch
* Monitorizar los problemas de rendimiento y depuración

## El SDK de AEM {#the-aem-sdk}

El SDK de AEM se utiliza para crear e implementar código personalizado. Es la principal herramienta que necesita para desarrollar y probar su aplicación sin encabezado antes de lanzarse. Contiene los siguientes artefactos:

* El Jar de inicio rápido: un archivo jar ejecutable que puede utilizarse para configurar una instancia de autor y de publicación
* Herramientas de Dispatcher: el módulo de Dispatcher y sus dependencias para sistemas basados en Windows y UNIX
* Java API Jar : la dependencia Java Jar/Maven que expone todas las API de Java permitidas que se pueden usar para desarrollar con AEM
* Javadoc jar: los javadocs para el jar de la API de Java

## Herramientas de desarrollo adicionales {#additional-development-tools}

Además del SDK de AEM, necesitará herramientas adicionales que faciliten el desarrollo y la prueba del código y el contenido localmente:

* Java
* Git
* Maven Apache
* La biblioteca Node.js
* El IDE de su elección

Como AEM es una aplicación Java, debe instalar Java y el SDK de Java para admitir el desarrollo de AEM como Cloud Service.

Git es lo que utilizará para administrar el control de código fuente, así como para registrar los cambios en Cloud Manager y luego implementarlos en una instancia de producción.

AEM utiliza Apache Maven para crear proyectos generados a partir del tipo de archivo del proyecto Maven de AEM. Todos los IDE principales proporcionan compatibilidad con la integración de Maven.

Node.js es un entorno de tiempo de ejecución de JavaScript que se utiliza para trabajar con los recursos front-end del subproyecto `ui.frontend` de un proyecto de AEM. Node.js se distribuye con npm, es el administrador de paquetes Node.js de facto, que se utiliza para administrar las dependencias de JavaScript.

## Componentes de un sistema AEM de un vistazo {#components-of-an-aem-system-at-a-glance}

A continuación, echemos un vistazo a las partes constitutivas de un entorno AEM.

Un entorno de AEM completo está formado por un Autor, una Publicación y un Dispatcher. Estos mismos componentes estarán disponibles en el tiempo de ejecución del desarrollo local para que le resulte más fácil previsualizar el código y el contenido antes de lanzarse.

* **El servicio Autor** es donde los usuarios internos crean, administran y previsualizan contenido.

* **El servicio de publicación** se considera el entorno &quot;activo&quot; y es lo que los usuarios finales interactúan con él. El contenido, después de editarse y aprobarse en el servicio Autor, se distribuye al servicio Publicar . El patrón de implementación más común con AEM aplicaciones sin periféricos es tener la versión de producción de la aplicación conectada a un servicio de AEM Publish.

* **El** Dispatcher es un servidor web estático que se complementa con el módulo AEM Dispatcher. Almacena en caché las páginas web producidas por la instancia de publicación para mejorar el rendimiento.

## Flujo de trabajo de desarrollo local {#the-local-development-workflow}

El proyecto de desarrollo local se basa en Apache Maven y utiliza Git para el control de código fuente. Para actualizar el proyecto, los desarrolladores pueden utilizar su entorno de desarrollo integrado preferido, como Eclipse, Visual Studio Code o IntelliJ, entre otros.

Para probar las actualizaciones de código o contenido que ingerirá la aplicación sin encabezado, debe implementar las actualizaciones en el tiempo de ejecución de AEM local, que incluye instancias locales del autor y los servicios de publicación de AEM.

Asegúrese de tomar nota de las distinciones entre cada componente en el tiempo de ejecución de AEM local, ya que es importante probar las actualizaciones donde más importen. Por ejemplo, pruebe las actualizaciones de contenido en la instancia de autor o pruebe el nuevo código en la instancia de publicación.

En un sistema de producción, un Dispatcher y un servidor http Apache siempre se sentarán frente a una instancia de publicación AEM. Proporcionan almacenamiento en caché y servicios de seguridad para el sistema AEM, por lo que es fundamental probar el código y las actualizaciones de contenido para el despachante.

## Vista previa del código y el contenido localmente con el entorno de desarrollo local {#previewing-your-code-and-content-locally-with-the-local-development-environment}

Para preparar el proyecto sin AEM para su lanzamiento, debe asegurarse de que todas las partes constitutivas del proyecto funcionen correctamente.

Para ello, hay que juntar todo: código, contenido y configuración, y pruébelo en un entorno de desarrollo local para estar listo para su lanzamiento.

El entorno de desarrollo local consta de tres esferas principales:

1. El proyecto AEM: esto contendrá todo el código personalizado, la configuración y el contenido en el que los desarrolladores de AEM estarán trabajando
1. Local AEM Runtime: versiones locales de los servicios de publicación y autor de AEM que se utilizarán para implementar código del proyecto de AEM
1. Tiempo de ejecución de Dispatcher local: versión local del servidor web Apache htttpd que incluye el módulo de Dispatcher.

Una vez configurado el entorno de desarrollo local, puede simular el contenido que sirve en la aplicación React mediante la implementación local de un servidor Nodo estático.

Para obtener una vista más detallada de la configuración de un entorno de desarrollo local y todas las dependencias necesarias para la vista previa del contenido, consulte [Documentación de implementación de producción](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/production-deployment.html?lang=en#prerequisites).

## Prepare su aplicación sin AEM para Go-Live {#prepare-your-aem-headless-application-for-golive}

Ahora, es el momento de preparar su aplicación sin AEM para el lanzamiento, siguiendo las prácticas recomendadas que se describen a continuación.

### Proteja y escale su aplicación sin encabezado antes de iniciar {#secure-and-scale-before-launch}

1. Configure [Autenticación basada en tokens](/help/assets/content-fragments/graphql-authentication-content-fragments.md) con sus solicitudes de GraphQL
1. Configure el [almacenamiento en caché](/help/implementing/dispatcher/caching.md).

### Estructura del modelo frente a salida de GraphQL {#structure-vs-output}

* Evite crear consultas que produzcan más de 15 kb de JSON (gzip comprimido). Los archivos JSON largos consumen muchos recursos para que la aplicación cliente los analice.
* Evite más de cinco niveles anidados de jerarquías de fragmento. Los niveles adicionales hacen que a los autores de contenido les resulte difícil considerar el impacto de sus cambios.
* Utilice consultas de varios objetos en lugar de modelar consultas con jerarquías de dependencia dentro de los modelos. Esto permite una mayor flexibilidad a largo plazo para reestructurar la salida de JSON sin tener que hacer muchos cambios de contenido.

### Maximice la relación de aciertos de caché de CDN {#maximize-cdn}

* No utilice consultas directas de GraphQL, a menos que solicite contenido activo desde la superficie.
   * Utilice consultas persistentes siempre que sea posible.
   * Proporcione CDN TTL por encima de 600 segundos para que la CDN los almacene en caché.
   * AEM calcular el impacto de un cambio de modelo en consultas existentes.
* Dividir archivos JSON/consultas de GraphQL entre la tasa de cambio de contenido baja y alta para reducir el tráfico de clientes a CDN y asignar un TTL más alto. Esto minimiza la CDN que vuelve a validar el JSON con el servidor de origen.
* Para invalidar activamente el contenido de la CDN, utilice la Depuración leve. Esto permite que la CDN vuelva a descargar el contenido sin causar que falte una caché.

### Mejorar el tiempo para descargar contenido sin encabezado {#improve-download-time}

* Asegúrese de que los clientes HTTP utilicen HTTP/2.
* Asegúrese de que los clientes HTTP acepten la solicitud de encabezados para gzip.
* Minimice el número de dominios utilizados para alojar JSON y artefactos de referencia.
* Aproveche `Last-modified-since` para actualizar los recursos.
* Utilice la salida `_reference` en el archivo JSON para empezar a descargar recursos sin tener que analizar archivos JSON completos.

## Implementar en producción {#deploy-to-production}

Una vez que se haya probado todo y funcione correctamente, estará listo para insertar las actualizaciones de código en un [repositorio Git centralizado en Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html).

Una vez cargadas las actualizaciones en Cloud Manager, se pueden implementar en AEM como Cloud Service mediante la canalización de CD/CI de [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html).

Puede empezar a implementar su código aprovechando la canalización de CD/CI de Cloud Manager, que se explica ampliamente [aquí](/help/implementing/deploying/overview.md).

## Monitorización del rendimiento {#performance-monitoring}

Para que los usuarios tengan la mejor experiencia posible al utilizar la aplicación sin periféricos AEM, es importante que supervise las métricas clave de rendimiento, tal como se detalla a continuación:

* Validar las versiones de producción y previsualización de la aplicación
* Verificar páginas de estado AEM para el estado actual de disponibilidad del servicio
* Acceso a los informes de rendimiento
   * Rendimiento de entrega
      * Finfinito (CDN): comprobar el número de llamadas, la tasa de caché, las tasas de error, el tráfico de carga útil
      * Servidores de origen: número de llamadas, tasas de error, cargas de CPU, tráfico de carga útil
   * Rendimiento del autor
      * Comprobar el número de usuarios, solicitudes y cargar
* Acceso a informes de rendimiento específicos de aplicaciones y espacio
   * Una vez que el servidor esté activo, compruebe si las métricas generales son verdes/naranjas/rojas y, a continuación, identifique los problemas específicos de la aplicación
   * Abra los mismos informes filtrados arriba a app/space (es decir, escritorio de Photoshop, paywall, etc.)
   * Utilice las API de registro de Splunk para acceder al rendimiento del servicio y la aplicación
   * Póngase en contacto con el servicio de atención al cliente en caso de que haya otros problemas.

## Solución de problemas {#troubleshooting}

### Depuración {#debugging}

Siga estas prácticas recomendadas como enfoque general de la depuración:

* Validar la funcionalidad y el rendimiento con la versión de vista previa de la aplicación
* Validar la funcionalidad y el rendimiento con la versión de producción de la aplicación
* Validar con la vista previa JSON del Editor de fragmentos de contenido
* Inspect el JSON en la aplicación cliente para comprobar la presencia de problemas de entrega o de aplicaciones de cliente
* Inspect el JSON mediante GraphQL para comprobar la presencia de problemas relacionados con contenido en caché o AEM

### Registro de un error con compatibilidad {#logging-a-bug-with-support}

Para registrar de forma eficaz un error con el servicio de asistencia en caso de que necesite más ayuda, siga los siguientes pasos:

* Tome capturas de pantalla del problema, si es necesario.
* Documentar una manera de reproducir el problema
* Documentar el contenido con el que se reproduce el problema
* Registre un problema a través del portal de soporte AEM con la prioridad adecuada

## Siguientes {#what-is-next}

Ahora que ha completado esta parte del Recorrido para desarrolladores sin encabezado de AEM, debe:

* Comprender los conceptos básicos AEM replicación de contenido y almacenamiento en caché.
* Obtenga información sobre cómo configurar las herramientas necesarias para simular go live para su aplicación sin periféricos.
* Obtenga información sobre cómo proteger y escalar la aplicación antes de Launch.
* Obtenga información sobre cómo monitorizar los problemas de rendimiento y depuración.

## El Recorrido Termina, ¿O Sí? {#journey-ends}

Felicitaciones! ¡Ha completado el Recorrido para desarrolladores AEM sin encabezado! Ahora debe comprender lo siguiente:

* La diferencia entre la entrega de contenido sin encabezado y con encabezado.
* AEM características sin periféricos.
* Organizar y AEM proyecto sin encabezado.
* Cómo crear contenido sin encabezado en AEM.
* Cómo recuperar y actualizar contenido sin encabezado en AEM.
* Cómo poner en marcha un proyecto AEM sin encabezado.
* Qué hacer después del lanzamiento.

## Recursos adicionales {#additional-resources}

* [Información general sobre la implementación en AEM como Cloud Service](/help/implementing/deploying/overview.md)
* [SDK de AEM as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
* [Configuración De Un Entorno AEM Local](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html)
* [Uso de Cloud Manager para implementar el código](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)
* [Integración del repositorio Git de Cloud Manager con un repositorio Git externo e Implementación de un proyecto para AEM como Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html)