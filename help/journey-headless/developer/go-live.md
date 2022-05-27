---
title: Cómo vivir con tu aplicación sin encabezado
description: En esta parte del Recorrido para desarrolladores sin encabezado de AEM, aprenda a implementar una aplicación sin encabezado en vivo tomando su código local en Git y mudándolo a Cloud Manager Git para la canalización CI/CD.
exl-id: 81616e31-764b-44b0-94a6-3ae24ce56bf6
source-git-commit: 270eb35023e34eed2cd17674372794c6c2cc7757
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 0%

---

# Cómo vivir con tu aplicación sin encabezado {#go-live}

En esta parte del [recorrido para desarrolladores AEM sin encabezado](overview.md), aprenda a implementar una aplicación sin encabezado en directo tomando su código local en Git y moviéndolo a Cloud Manager Git para la canalización CI/CD.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido sin AEM, [Cómo ponerlo todo juntos: su aplicación y su contenido en AEM sin cabeza](put-it-all-together.md) aprendió a utilizar las herramientas de desarrollo de AEM para unir todas las facetas de su proyecto.

Este artículo se basa en estos fundamentos para que entienda cómo preparar su propio proyecto sin objetivos AEM para su lanzamiento.

## Objetivo {#objective}

Este documento le ayuda a comprender la canalización de publicación sin encabezado de AEM y las consideraciones de rendimiento que debe tener en cuenta antes de comenzar a trabajar con la aplicación.

* Asegurar y escalar la aplicación antes de Launch
* Monitorizar los problemas de rendimiento y depuración

<!-- Alexandru: this is a bit redundant, to review again later

## Prepare your AEM Headless Application for Go-Live {#prepare-your-aem-headless-application-for-golive}

-->
Para preparar la aplicación sin AEM para el inicio, siga las prácticas recomendadas que se describen a continuación.

## Asegurar y escalar su aplicación sin encabezado antes de Launch {#secure-and-scale-before-launch}

1. Configurar [Autenticación basada en tokens](/help/headless/security/authentication.md) con sus solicitudes de GraphQL
1. Configurar [Almacenamiento en caché](/help/implementing/dispatcher/caching.md).

## Estructura del modelo frente a salida de GraphQL {#structure-vs-output}

* Evite crear consultas que produzcan más de 15 kb de JSON (gzip comprimido). Los archivos JSON largos consumen muchos recursos para que la aplicación cliente los analice.
* Evite más de cinco niveles anidados de jerarquías de fragmento. Los niveles adicionales hacen que a los autores de contenido les resulte difícil considerar el impacto de sus cambios.
* Utilice consultas de varios objetos en lugar de modelar consultas con jerarquías de dependencia dentro de los modelos. Esto permite una mayor flexibilidad a largo plazo para reestructurar la salida de JSON sin tener que hacer muchos cambios de contenido.

## Maximizar la proporción de visitas en caché de CDN {#maximize-cdn}

* No utilice consultas directas de GraphQL, a menos que solicite contenido activo desde la superficie.
   * Utilice consultas persistentes siempre que sea posible.
   * Proporcione CDN TTL por encima de 600 segundos para que la CDN los almacene en caché.
   * AEM calcular el impacto de un cambio de modelo en consultas existentes.
* Dividir archivos JSON/consultas de GraphQL entre la tasa de cambio de contenido baja y alta para reducir el tráfico de clientes a CDN y asignar un TTL más alto. Esto minimiza la CDN que vuelve a validar el JSON con el servidor de origen.
* Para invalidar activamente el contenido de la CDN, utilice la Depuración leve. Esto permite que la CDN vuelva a descargar el contenido sin causar que falte una caché.

## Mejorar el tiempo para descargar contenido sin objetivos {#improve-download-time}

* Asegúrese de que los clientes HTTP utilicen HTTP/2.
* Asegúrese de que los clientes HTTP acepten la solicitud de encabezados para gzip.
* Minimice el número de dominios utilizados para alojar JSON y artefactos de referencia.
* Aprovechar `Last-modified-since` para actualizar los recursos.
* Uso `_reference` en el archivo JSON para iniciar la descarga de recursos sin tener que analizar los archivos JSON completos.

## Implementar en producción {#deploy-to-production}

Una vez que se haya probado todo y funcione correctamente, estará listo para insertar las actualizaciones de código en una [repositorio Git centralizado en Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html).

Una vez cargadas las actualizaciones en Cloud Manager, se pueden implementar en AEM as a Cloud Service mediante [Canalización de CD/CI de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html).

Puede empezar a implementar su código aprovechando la canalización de CD/CI de Cloud Manager, que se cubre ampliamente [here](/help/implementing/deploying/overview.md).

## Supervisión del rendimiento {#performance-monitoring}

Para que los usuarios tengan la mejor experiencia posible al utilizar la aplicación sin periféricos AEM, es importante que supervise las métricas clave de rendimiento, tal como se detalla a continuación:

* Validar las versiones de producción y previsualización de la aplicación
* Verificar páginas de estado AEM para el estado actual de disponibilidad del servicio
* Acceso a los informes de rendimiento
   * Rendimiento de entrega
      * Rendimiento de CDN (FIENTE): compruebe el número de llamadas, la tasa de caché, los índices de errores y el tráfico de carga útil
      * Servidores de origen: número de llamadas, tasas de error, cargas de CPU, tráfico de carga útil
   * Rendimiento del autor
      * Comprobar el número de usuarios, solicitudes y cargar
* Acceso a informes de rendimiento específicos de aplicaciones y espacio
   * Una vez que el servidor esté activo, compruebe si las métricas generales son verdes/naranjas/rojas y, a continuación, identifique los problemas específicos de la aplicación
   * Abra los mismos informes filtrados arriba a la aplicación o al espacio (por ejemplo, escritorio de Photoshop, paywall).
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

### Registro de un error con asistencia {#logging-a-bug-with-support}

Para registrar de forma eficaz un error con el servicio de asistencia en caso de que necesite más ayuda, siga los siguientes pasos:

* Tome capturas de pantalla del problema, si es necesario.
* Documentar una manera de reproducir el problema
* Documentar el contenido con el que se reproduce el problema
* Registre un problema a través del portal de soporte AEM con la prioridad adecuada

## El Recorrido Termina, ¿O Sí? {#journey-ends}

Felicitaciones! ¡Ha completado el Recorrido para desarrolladores AEM sin encabezado! Ahora debe comprender lo siguiente:

* La diferencia entre la entrega de contenido sin encabezado y con encabezado.
* AEM características sin periféricos.
* Organizar y AEM proyecto sin encabezado.
* Cómo crear contenido sin encabezado en AEM.
* Cómo recuperar y actualizar contenido sin encabezado en AEM.
* Cómo poner en marcha un proyecto AEM sin encabezado.
* Qué hacer después del lanzamiento.

Ya ha iniciado su primer proyecto AEM sin encabezado o ahora tiene todo el conocimiento que necesita para hacerlo. ¡bueno trabajo!

### Explorar aplicaciones de una sola página {#explore-spa}

Sin embargo, las tiendas sin periféricos de AEM no tienen que parar aquí. Puede que recuerde en la [Parte de introducción del recorrido](getting-started.md#integration-levels) analizamos brevemente cómo AEM no solo admite entregas sin periféricos y modelos de pila completa tradicionales, sino que también puede admitir modelos híbridos que combinan las ventajas de ambos.

Si este tipo de flexibilidad es algo que necesita para su proyecto, continúe con la parte opcional adicional del recorrido, [Cómo crear aplicaciones de una sola página (SPA) con AEM.](create-spa.md)

## Recursos adicionales {#additional-resources}

* [Información general sobre la implementación en AEM as a Cloud Service](/help/implementing/deploying/overview.md)
* [Uso de Cloud Manager para implementar el código](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)
* [Integración del repositorio Git de Cloud Manager con un repositorio Git externo e Implementación de un proyecto en AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html)
