---
title: Fase de implementación en Cloud Acceleration Manager
description: Esta página proporciona información general sobre la fase de implementación en Cloud Acceleration Manager.
source-git-commit: 6fcde5440a5e2eec57b69b14dca93192634b3c3a
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 2%

---


# Fase de implementación en Cloud Acceleration Manager {#implementation-phase-cam}

La fase de implementación incluye:

* [Desarrollo local](#local-development)
* [Refactorización de código](#code-refactoring)
* [Implementación de AEM as a Cloud Service](#aem-as-a-cloud-service-deployment)
* [Transferencia de contenido](#content-transfer)


Haga clic en la tarjeta del proyecto para abrir la página de aterrizaje del proyecto y vaya a la sección **Implementación**, como se muestra en la figura siguiente.

![image](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-1.png)

>[!NOTE]
>Consulte Creación y administración de un proyecto en Cloud Acceleration Manager para obtener más información.


## Uso de la tarjeta de desarrollo local {#local-development}

La tarjeta de desarrollo local proporciona todo el contenido relevante que le ayudará a configurar el entorno de desarrollo de AEM local al iniciar la fase de implementación de su recorrido de migración.

Siga esta sección para explorar la tarjeta de actividad de desarrollo local :

1. Haga clic en el botón **View** en la tarjeta **Local Development**.

   ![image](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-2.png)

1. Se muestra un carrusel de contenido con información relevante para esta fase del recorrido de migración.

   ![image](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-3.png)


## Uso de la tarjeta de refactorización de código {#code-refactoring}

La tarjeta de actividad Refactorización de código proporciona toda la información relevante y resalta las áreas de refactorización de código que debe revisar al pasar a AEM como Cloud Service.

Siga esta sección para explorar la tarjeta de actividad Refactorización de código :

1. Haga clic en el botón **Review** en la tarjeta de actividad **Code Refactoring**.

   ![image](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-4.png)

1. La página muestra la lista de actividades de refactorización de código organizadas por el nivel de gravedad. Para obtener más información, haga clic en los dos iconos resaltados.

   >[!NOTE]
   >Además, revise el contenido de las pestañas de la página para comprender algunas áreas adicionales que no están cubiertas por el Analizador de prácticas recomendadas.

   ![image](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-5.png)


## Uso de AEM como tarjeta de implementación de Cloud Service {#aem-as-a-cloud-service-deployment}

AEM tarjeta de implementación como Cloud Service proporciona todo el contenido relevante que le ayudará a implementar el código para AEM como Cloud Service.

Siga esta sección para explorar AEM como tarjeta de actividad de la tarjeta de implementación del Cloud Service:

1. Haga clic en el botón **View** en la tarjeta de actividad **AEM as a Cloud Service Deployment**.

   ![image](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-6.png)

1. Se muestra un carrusel de contenido con información relevante para esta fase del recorrido de migración.

   ![image](/help/move-to-cloud-service/cloud-acceleration-manager/assets/aem-deployment-card.png)


## Uso de la tarjeta de transferencia de contenido {#content-transfer}

La tarjeta de actividad Transferencia de contenido proporciona directrices y consideraciones que deben revisarse al utilizar la herramienta de transferencia de contenido para mover contenido de la instancia de AEM actual a AEM como Cloud Service.

Siga esta sección para explorar la tarjeta de actividad de transferencia de contenido:

1. Haga clic en el botón **View** en la tarjeta de actividad **Content Transfer**.

   ![image](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-8.png)

1. Se muestra un carrusel de contenido con información relevante para esta fase del recorrido de migración.

   ![image](/help/move-to-cloud-service/cloud-acceleration-manager/assets/content-transfertool-card.png)

   >[!NOTE]
   >Revise los [requisitos previos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=en) y las [prácticas recomendadas y directrices](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en) antes de utilizar la herramienta de transferencia de contenido.

### Calcular la actividad de la herramienta de transferencia de contenido {#calculating}

Se ha proporcionado una nueva calculadora de la herramienta de transferencia de contenido para estimar el tiempo que podría llevar completar la actividad de transferencia de contenido. Puede utilizar el control deslizante del tamaño del repositorio de contenido para seleccionar el tamaño que se aplica al proyecto. Los tiempos de transferencia varían para las fases de extracción e ingesta.

Para calcular el tamaño del Repositorio AEM, puede ejecutar el informe Uso del disco en `http://HOST:PORT/etc/reports/diskusage.html`.

También puede estimar el tamaño de las rutas específicas del repositorio utilizando el parámetro `path`, por ejemplo, `http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`.

## Siguientes pasos {#whats-next}

Una vez que haya aprendido a iniciar sesión en Cloud Acceleration Manager y a utilizar la fase de implementación, ya está listo para pasar a revisar el siguiente paso, Uso de la fase de GoLive.
