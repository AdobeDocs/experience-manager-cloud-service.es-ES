---
title: Cómo vivir con tu aplicación sin encabezado
description: En esta parte del Recorrido para desarrolladores sin encabezado de AEM, aprenda a implementar una aplicación sin encabezado en vivo tomando su código local en Git y mudándolo a Cloud Manager Git para la canalización CI/CD.
hide: true
hidefromtoc: true
index: false
exl-id: f79b5ada-8f59-4706-9f90-bc63301b2b7d
translation-type: tm+mt
source-git-commit: dc4f1e916620127ebf068fdcc6359041b49891cf
workflow-type: tm+mt
source-wordcount: '1039'
ht-degree: 0%

---

# Cómo poner en marcha su aplicación sin encabezado {#go-live}

>[!CAUTION]
>
>TRABAJO EN CURSO - La creación de este documento está en curso y no debe entenderse como completo o definitivo ni debe utilizarse con fines de producción.

En esta parte del [AEM Recorrido para desarrolladores sin encabezado,](overview.md) aprende a implementar una aplicación sin encabezado en vivo tomando su código local en Git y moviéndolo a Cloud Manager Git para la canalización CI/CD.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido sin AEM encabezado, [How to Put it All Together - Your App and Your Content in AEM Headless](put-it-all-together.md) ha aprendido a preparar su propio proyecto sin objetivos AEM para que se ponga en marcha y ahora debería:

* Comprender los requisitos para ponerse en marcha.

Este artículo se basa en estos fundamentos para que entienda cómo llevar su proyecto sin encabezado de AEM en vivo.

## Objetivo {#objective}

Este documento le ayuda a comprender la canalización de publicación sin AEM y las consideraciones de rendimiento que debe tener en cuenta antes de empezar a trabajar con la aplicación.

* Comprender los conceptos básicos AEM replicación de contenido y almacenamiento en caché
* Configure las herramientas necesarias para simular go live para su aplicación sin periféricos
* Asegurar y escalar la aplicación antes de Launch
* Monitorizar los problemas de rendimiento y depuración

## Conceptos básicos de replicación y almacenamiento en caché de contenido {#content-replication-and-caching}

Un entorno de AEM completo está formado por un Autor, una Publicación y un Dispatcher.

* **El servicio Autor** es donde los usuarios internos crean, administran y previsualizan contenido.

* **El servicio de publicación** se considera el entorno &quot;activo&quot; y es lo que los usuarios finales interactúan con él. El contenido, después de editarse y aprobarse en el servicio Autor, se distribuye al servicio Publicar .

* **El** Dispatcher es un servidor web estático que se complementa con el módulo AEM Dispatcher. Almacena en caché las páginas web producidas por la instancia de publicación para mejorar el rendimiento.

El patrón de implementación más común con AEM aplicaciones sin periféricos es tener la versión de producción de la aplicación conectada a un servicio de AEM Publish.

## Requisitos y configuración {#requirements-and-configuration}

1. Configure un [tiempo de ejecución local](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#install-java) mediante el SDK [AEM as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
2. Instale el [contenido de muestra de WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) y los puntos finales subsiguientes de GraphQL
3. Implementar y configurar un [servidor de nodos estático](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/production-deployment.html?lang=en#static-server).

## Proteja y escale su aplicación sin encabezado antes de iniciar {#secure-and-scale-before-launch}

1. Configurar [Autenticación basada en tokens](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)
2. Enlaces web seguros
3. Configuración del almacenamiento en caché y la escalabilidad

## Implementar en producción {#deploy-to-production}

Una vez que haya probado todo el código y el contenido localmente, ya estará listo para iniciar una implementación de producción con AEM.

### Estructura del modelo frente a salida de GraphQL {#structure-vs-output}

* Evite crear consultas que produzcan más de 15 kb de JSON (gzip comprimido). Los archivos JSON largos consumen muchos recursos para que la aplicación cliente los analice.
* Evite más de cinco niveles anidados de jerarquías de fragmento. Los niveles adicionales hacen que a los autores de contenido les resulte difícil considerar el impacto de sus cambios.
* Utilice consultas de varios objetos en lugar de modelar consultas con jerarquías de dependencia dentro de los modelos. Esto permite una mayor flexibilidad a largo plazo para reestructurar la salida de JSON sin tener que hacer muchos cambios de contenido.

### Maximice la relación de aciertos de caché de CDN {#maximize-cdn}

* No utilice consultas directas de GraphQL, a menos que solicite contenido activo desde la superficie.
   * En su lugar, utilice consultas persistentes.
   * Proporcione TTL de CDN por encima de 600 segundos para que la CDN pueda almacenarlas en caché.
   * AEM calcular el impacto de un cambio de modelo en consultas existentes.
* Dividir archivos JSON/consultas de GraphQL entre la tasa de cambio de contenido baja y alta para reducir el tráfico de clientes a CDN y asignar un TTL más alto. Esto minimiza la CDN que vuelve a validar el JSON con el servidor de origen.
* Para invalidar activamente el contenido de la CDN, utilice la Depuración leve. Esto permite que la CDN vuelva a descargar el contenido sin causar que falte una caché.

### Mejorar el tiempo para descargar contenido sin encabezado {#improve-download-time}

* Asegúrese de que los clientes HTTP utilicen HTTP/2.
* Asegúrese de que los clientes HTTP acepten la solicitud de encabezados para gzip.
* Minimice el número de dominios utilizados para alojar JSON y artefactos de referencia.
* Aproveche `Last-modified-since` para actualizar los recursos.
* Utilice la salida `_reference` en el archivo JSON para empezar a descargar recursos sin tener que analizar archivos JSON completos.

## Monitoreo {#monitoring}

### Cómo comprobar el rendimiento general {#check-overall-performance}

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

Para asegurarse de que la aplicación funciona correctamente antes del inicio, se recomienda seguir estos pasos como enfoque general para la depuración:

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

Debe continuar con su recorrido sin AEM al revisar el documento [Post Launch](post-launch.md) donde aprende a mantener su experiencia sin encabezado.

## Recursos adicionales {#additional-resources}
