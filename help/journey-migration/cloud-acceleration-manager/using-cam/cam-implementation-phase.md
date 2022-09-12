---
title: Fase de implementación en Cloud Acceleration Manager
description: Esta página proporciona información general sobre la fase de implementación en Cloud Acceleration Manager.
exl-id: e6ac88f0-4b3f-43a1-98bc-8c6608713784
source-git-commit: 24331b974ded34ef949cc3d6fb157b124c145dee
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 4%

---

# Fase de implementación en Cloud Acceleration Manager {#implementation-phase-cam}

La fase de implementación incluye:

* [Desarrollo local](#local-development)
* [Refactorización de código](#code-refactoring)
* [Implementación as a Cloud Service AEM](#aem-as-a-cloud-service-deployment)
* [Transferencia de contenido](#content-transfer)


Haga clic en la tarjeta del proyecto para abrir la página de aterrizaje del proyecto y vaya hasta la página **Implementación** como se muestra en la figura siguiente.

![imagen](/help/journey-migration/cloud-acceleration-manager/assets/implementation-1.png)

>[!NOTE]
>Consulte [Creación y administración de un proyecto en Cloud Acceleration Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=en#create-project) para obtener más información.


## Uso de la tarjeta de desarrollo local {#local-development}

La tarjeta de desarrollo local proporciona todo el contenido relevante que le ayudará a configurar el entorno de desarrollo de AEM local al iniciar la fase de implementación de su recorrido de migración.

Siga esta sección para explorar la tarjeta de actividad de desarrollo local :

1. Haga clic en el **Ver** del **Desarrollo local** tarjeta.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/implementation-2.png)

1. Un carrusel de contenido muestra la información relevante para esta fase del recorrido de migración.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/implementation-3.png)


## Uso de la tarjeta de refactorización de código {#code-refactoring}

La tarjeta de actividad Refactorización de código proporciona toda la información relevante y resalta las áreas de refactorización de código que debe revisar y resolver al pasar a AEM as a Cloud Service.

Siga esta sección para explorar la tarjeta de actividad Refactorización de código :

1. Haga clic en el **Consulte** del **Refactorización de código** tarjeta de actividad.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/implementation-4.png)

1. La página muestra la lista de actividades de refactorización de código organizadas por el nivel de gravedad. Para obtener más información, haga clic en los dos iconos resaltados.

   La página muestra las consideraciones de refactorización de código en tres pestañas diferentes:

   * Información general
   * Dispatcher
   * Pruebas

>[!NOTE]
>Revise el contenido de estas pestañas para comprender algunas áreas adicionales que no están cubiertas por el Analizador de prácticas recomendadas.

La variable **Dispatcher** proporciona información sobre cómo estructurar las configuraciones as a Cloud Service de Apache y Dispatcher de AEM, así como sobre cómo validarlas y ejecutarlas localmente antes de implementarlas en entornos en la nube. También describe la depuración en entornos de Cloud.

![imagen](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-2.png)

La variable **Pruebas** proporciona información sobre las pruebas funcionales, de auditoría de experiencias y de interfaz de usuario.

![imagen](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-3.png)


## Uso de AEM tarjeta de implementación as a Cloud Service {#aem-as-a-cloud-service-deployment}

AEM tarjeta de implementación as a Cloud Service proporciona todo el contenido relevante que le ayudará a implementar el código para AEM as a Cloud Service.

Siga esta sección para explorar AEM tarjeta de actividad de la tarjeta de implementación as a Cloud Service:

1. Haga clic en el **Ver** del **Implementación as a Cloud Service AEM** tarjeta de actividad.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/implementation-6.png)

1. Un carrusel de contenido muestra la información relevante para esta fase del recorrido de migración.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/aem-deployment-card.png)


## Uso de la tarjeta de transferencia de contenido {#content-transfer}

La tarjeta de transferencia de contenido le permite iniciar y administrar la transferencia de contenido desde la instancia de AEM actual a AEM as a Cloud Service.

Siga esta sección para explorar la tarjeta de actividad de transferencia de contenido:

1. Haga clic en el **Consulte** del **Transferencia de contenido** tarjeta de actividad.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-1.png)

1. Para iniciar una transferencia de contenido, debe crear un conjunto de migración. Haga clic en **Crear conjunto de migración**. Un conjunto de migración permite transferir contenido a AEM as a Cloud Service.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-2.png)

   >[!NOTE]
   >Revise el [requisitos previos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=en) y [prácticas recomendadas y directrices](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en) antes de usar la herramienta de transferencia de contenido.

1. Deberá descargar e instalar la herramienta de transferencia de contenido para rellenar el conjunto de migración y completar la fase de extracción de la transferencia de contenido. Consulte [Introducción a la herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=es) para aprender a utilizar la herramienta de transferencia de contenido.

1. Para ingerir contenido del conjunto Migración en un entorno AEM as a Cloud Service, deberá iniciar una ingesta. Vaya a **Trabajos de Ingesta** y haga clic en **Nueva ingesta**. Consulte [Ingesta de contenido en Target](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html?lang=en) para aprender a completar la fase de ingesta de la transferencia de contenido.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-3.png)

### Calcular el tiempo de transferencia de contenido {#calculating}

Se ha proporcionado una calculadora de la herramienta de transferencia de contenido para estimar el tiempo que podría llevar completar la actividad de transferencia de contenido. Puede utilizar el control deslizante del tamaño del repositorio de contenido para seleccionar el tamaño que se aplica al proyecto. Los tiempos de transferencia varían para las fases de extracción e ingesta.

![imagen](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-4.png)

>[!NOTE]
>Estos tiempos son sólo estimaciones. En estas estimaciones no se han tenido en cuenta factores como las velocidades de red y el tiempo para aumentar las instancias.

Para estimar el tamaño del Repositorio AEM, puede ejecutar el informe Uso del disco en `http://HOST:PORT/etc/reports/diskusage.html`.

También puede estimar el tamaño de las rutas específicas del repositorio utilizando la variable `path` , por ejemplo, `http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`.

## Siguientes pasos {#whats-next}

Una vez que sepa cómo iniciar sesión en Cloud Acceleration Manager y cómo utilizar la fase de implementación, ya estará listo para pasar a revisar el siguiente paso en la [Ir a la fase de lanzamiento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-golive-phase.html?lang=en).
