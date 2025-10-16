---
title: Cómo hacer un lanzamiento con su aplicación sin encabezado
description: En esta parte del recorrido para desarrolladores de AEM sin encabezado, aprenda a implementar un lanzamiento de la aplicación sin encabezado tomando su código local en Git y mudándolo a Cloud Manager Git para la canalización de integración continua/entrega continua (CI/CD).
exl-id: 81616e31-764b-44b0-94a6-3ae24ce56bf6
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Architect, Developer
source-git-commit: 2ccca86a0e611b93c273e37abb6e0fd7870421d4
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 100%

---

# Cómo hacer un lanzamiento con su aplicación sin encabezado {#go-live}

En esta parte del [recorrido para desarrolladores de AEM sin encabezado](overview.md), aprenda a implementar un lanzamiento de la aplicación sin encabezado tomando su código local en Git y mudándolo a Cloud Manager Git para la canalización CI/CD.

## Lo que hemos visto hasta ahora {#story-so-far}

En el documento anterior del recorrido de AEM sin encabezado, [Cómo juntar su aplicación y contenido en AEM sin encabezado](put-it-all-together.md), aprendió a utilizar las herramientas de desarrollo de AEM para unir todas las facetas de su proyecto.

Este artículo se basa en estos fundamentos para que entienda cómo preparar su propio proyecto de AEM sin encabezado para su lanzamiento.

## Objetivo {#objective}

Este documento le ayuda a comprender la canalización de las publicaciones de AEM sin encabezado y las consideraciones de rendimiento que debe tener en cuenta antes de lanzar su aplicación.

* Asegurar y escalar su aplicación antes del lanzamiento
* Monitorizar los problemas de rendimiento y depuración

Para preparar su aplicación AEM sin encabezado para el lanzamiento, siga las prácticas recomendadas que se describen a continuación.

## Asegurar y escalar su aplicación sin encabezado antes del lanzamiento {#secure-and-scale-before-launch}

1. Configurar [Autenticación basada en token](/help/headless/security/authentication.md) con sus solicitudes de GraphQL
1. Configurar el [almacenamiento en caché](/help/implementing/dispatcher/caching.md).

## Estructura del modelo frente al output de GraphQL {#structure-vs-output}

* Evite crear consultas que produzcan más de 15 kb de JSON (gzip comprimido). Los archivos JSON largos consumen muchos recursos para que la aplicación cliente los analice.
* Evite más de cinco niveles anidados de jerarquías de fragmento. Los niveles adicionales hacen que a los autores de contenido les resulte difícil considerar el impacto de sus cambios.
* Utilice consultas de varios objetos en lugar de modelar consultas con jerarquías de dependencia dentro de los modelos. Esto permite una mayor flexibilidad a largo plazo para reestructurar el output de JSON sin tener que hacer muchos cambios de contenido.

## Maximizar la proporción de visitas en caché de CDN {#maximize-cdn}

* No utilice consultas directas de GraphQL, a menos que solicite contenido activo desde la superficie.
   * Utilice consultas persistentes siempre que sea posible.
   * Proporcione el tiempo de duración (TTL) de la red de distribución de contenido (CDN) por encima de 600 segundos para que la CDN los almacene en la caché.
   * AEM calcula el impacto de un cambio de modelo en las consultas existentes.
* Divida los archivos JSON o consultas GraphQL entre tasas de cambio de contenido bajas y altas para reducir el tráfico de clientes a la CDN y asignar un TTL más alto. Esto minimiza la CDN que vuelve a validar el JSON con el servidor de origen.
* Para invalidar activamente el contenido de la CDN, utilice la depuración leve. Esto permite a la CDN volver a descargar el contenido sin provocar una pérdida de caché.

## Mejora del tiempo para descargar contenido sin encabezado {#improve-download-time}

* Asegúrese de que los clientes HTTP utilicen HTTP/2.
* Asegúrese de que los clientes HTTP acepten la solicitud de encabezados para gzip.
* Minimice el número de dominios utilizados para alojar el formato JSON y los artefactos de referencia.
* Utilice `Last-modified-since` para actualizar los recursos.
* Use la salida `_reference` en el archivo JSON para iniciar la descarga de los recursos sin tener que analizar los archivos JSON completos.

## Implementación de la producción {#deploy-to-production}

Una vez que haya probado que todo funcione correctamente, estará listo para insertar las actualizaciones de código en un [repositorio Git centralizado en Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html?lang=es).

Una vez cargadas las actualizaciones en Cloud Manager, se pueden implementar en AEM as a Cloud Service mediante la [canalización CI/CD de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=es).

Puede empezar a implementar su código utilizando la canalización de CD/CI de Cloud Manager, que se trata detalladamente en [Implementación de paquetes de contenido mediante Cloud Manager y el Administrador de paquetes](/help/implementing/deploying/overview.md).

## Monitorización del rendimiento {#performance-monitoring}

Para que los usuarios tengan la mejor experiencia posible al utilizar la aplicación AEM sin encabezado, es importante que monitorice las métricas clave de rendimiento, tal como se detalla a continuación:

* Valide las versiones de producción y previsualización de la aplicación.
* Verifique las páginas de estado de AEM para el estado actual de disponibilidad del servicio.
* Acceda a los informes de rendimiento.
   * Rendimiento de entrega
      * Rendimiento (rápido) de CDN: compruebe el número de llamadas, la tasa de caché, los índices de errores y el tráfico de carga útil
      * Servidores de origen: número de llamadas, tasas de error, cargas de CPU, tráfico de carga útil
   * Rendimiento del autor
      * Comprobar el número de usuarios, solicitudes y cargas
* Acceso a informes de rendimiento específicos de aplicaciones y de espacio
   * Una vez que el servidor esté activo, compruebe si las métricas generales son verdes, naranjas o rojas y, a continuación, identifique los problemas específicos de la aplicación.
   * Abra los mismos informes filtrados anteriormente en la aplicación o el espacio (por ejemplo, escritorio de Photoshop, muro de pago).
   * Utilice las API de registro de Splunk para acceder al rendimiento del servicio y de la aplicación.
   * Póngase en contacto con asistencia al cliente en caso de que surjan otros problemas.

## Solución de problemas {#troubleshooting}

### Depuración {#debugging}

Siga estas prácticas recomendadas como enfoque general de la depuración:

* Valide la funcionalidad y el rendimiento con la versión previa de la aplicación.
* Valide la funcionalidad y el rendimiento con la versión de producción de la aplicación.
* Valide con la vista previa JSON del Editor de fragmentos de contenido.
* Examine el JSON en la aplicación cliente para comprobar si existen problemas en la aplicación cliente o en la entrega.
* Examine el JSON mediante GraphQL para comprobar si existen problemas relacionados con el contenido en caché o AEM.

### Registro de un error con asistencia {#logging-a-bug-with-support}

Para registrar un error de forma eficaz con la asistencia técnica en caso de que necesite asistencia adicional, haga lo siguiente:

* Tome capturas de pantalla del problema, si es necesario.
* Documente una manera de reproducir el problema.
* Documente el contenido con el que se reproduce el problema.
* Registre un problema a través del portal de asistencia de AEM con la prioridad adecuada.

## El recorrido ha terminado, ¿o no? {#journey-ends}

¡Enhorabuena! Ha completado el recorrido para desarrolladores de AEM sin encabezado. Ahora debe comprender lo siguiente:

* La diferencia entre la entrega de contenido sin encabezado y con encabezado.
* Las características sin encabezado de AEM.
* Cómo organizar un proyecto sin encabezado en AEM.
* Cómo crear contenido sin encabezado en AEM.
* Cómo recuperar y actualizar contenido sin encabezado en AEM.
* Cómo poner en marcha un proyecto de AEM sin encabezado.
* Qué hacer después del lanzamiento.

Ya ha iniciado su primer proyecto de AEM sin encabezado o ahora tiene los conocimientos necesarios para hacerlo. Buen trabajo.

### Explorar aplicaciones de una sola página {#explore-spa}

Sin embargo, las tiendas sin encabezado de AEM no tienen que detenerse aquí. Tal vez recuerde que en la [parte de introducción del recorrido](getting-started.md#integration-levels) analizamos brevemente cómo AEM no solo admite entregas sin encabezado y modelos de pila completa tradicionales, sino que también puede admitir modelos híbridos que combinan las ventajas de ambos.

Si este es el tipo de flexibilidad que necesita para su proyecto, continúe con la parte opcional adicional del recorrido, [Cómo crear aplicaciones de una sola página (SPA) con AEM](create-spa.md).

## Recursos adicionales {#additional-resources}

* [Introducción a AEM como CMS sin encabezado](/help/headless/introduction.md)
* [Portal para desarrolladores de AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=es)
* [Tutoriales de AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=es)
* [Información general sobre la implementación de AEM as a Cloud Service](/help/implementing/deploying/overview.md)
* [Uso de Cloud Manager para implementar el código](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=es)
* [Integración del repositorio Git de Cloud Manager con un repositorio Git externo e implementación de un proyecto en AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html?lang=es)
