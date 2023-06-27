---
title: Fase de implementación en Cloud Acceleration Manager
description: Esta página proporciona información general sobre la fase de implementación en Cloud Acceleration Manager.
exl-id: e6ac88f0-4b3f-43a1-98bc-8c6608713784
source-git-commit: d361ddc9a50a543cd1d5f260c09920c5a9d6d675
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 4%

---

# Fase de implementación en Cloud Acceleration Manager {#implementation-phase-cam}

La fase de implementación incluye:

* [Desarrollo local](#local-development)
* [Refactorización de código](#code-refactoring)
* [AEM Implementación as a Cloud Service](#aem-as-a-cloud-service-deployment)
* [Transferencia de contenido](#content-transfer)


Haga clic en la tarjeta del proyecto para poder abrir la página de aterrizaje del proyecto y navegar hasta el **Implementación** , como se muestra en la siguiente figura.

![imagen](/help/journey-migration/cloud-acceleration-manager/assets/implementation-1.png)

>[!NOTE]
>Consulte [Creación y administración de un proyecto en Cloud Acceleration Manager](getting-started-cam.md#create-project) para obtener más información.


## Uso de la tarjeta de desarrollo local {#local-development}

AEM La tarjeta de desarrollo local proporciona todo el contenido relevante que puede ayudarle a configurar su entorno de desarrollo de local al iniciar la fase de implementación del recorrido de migración.

Siga esta sección para poder explorar la tarjeta de actividad Desarrollo local:

1. Clic **Ver** desde el **Desarrollo local** Tarjeta de.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/implementation-2.png)

1. Un carrusel de contenido muestra la información relevante para esta fase del recorrido de migración.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/implementation-3.png)


## Uso de la tarjeta de refactorización de código {#code-refactoring}

AEM La tarjeta de actividad de refactorización de código proporciona toda la información relevante y resalta las áreas de refactorización de código que se deben revisar y resolver al pasar a la fase de refactorización de código as a Cloud Service.

Siga esta sección para poder explorar la tarjeta de actividad de Refactorización de código:

1. Clic **Revisar** desde el **Refactorización de código** tarjeta de actividad.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/implementation-4.png)

1. La página muestra la lista de actividades de refactorización de código organizadas por el nivel de gravedad. Para obtener más información, haga clic en los dos iconos resaltados.

   La página muestra las consideraciones sobre la refactorización del código en tres pestañas diferentes:

   * Información general
   * Dispatcher
   * Pruebas

>[!NOTE]
>Revise el contenido de estas pestañas para comprender algunas áreas adicionales que no cubre el Analizador de prácticas recomendadas.

El **Dispatcher** AEM proporciona información sobre cómo estructurar las configuraciones as a Cloud Service de Apache y Dispatcher, así como cómo validarla y ejecutarla localmente antes de implementarla en entornos en la nube. También describe la depuración en entornos en la nube.

![imagen](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-2.png)

El **Pruebas** proporciona información sobre las pruebas funcionales, de auditoría de experiencias y de interfaz de usuario.

![imagen](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-3.png)


## AEM Uso de la tarjeta Implementación as a Cloud Service {#aem-as-a-cloud-service-deployment}

AEM La tarjeta Implementación as a Cloud Service AEM proporciona todo el contenido relevante que le ayuda a implementar su código para que se as a Cloud Service.

AEM Siga esta sección para poder explorar la tarjeta de actividad de la tarjeta de implementación as a Cloud Service:

1. Clic **Ver** desde el **AEM Implementación as a Cloud Service** tarjeta de actividad.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/implementation-6.png)

1. Un carrusel de contenido muestra la información relevante para esta fase del recorrido de migración.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/aem-deployment-card.png)


## Uso de la tarjeta de transferencia de contenido {#content-transfer}

AEM AEM La tarjeta Transferencia de contenido le permite iniciar y administrar la transferencia de contenido desde su instancia de actual a la as a Cloud Service de la.

Siga esta sección para poder explorar la tarjeta de actividad de transferencia de contenido:

1. Clic **Revisar** desde el **Transferencia de contenido** tarjeta de actividad.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-1.png)

1. Para iniciar una transferencia de contenido, debe crear un conjunto de migración. Clic **Crear conjunto de migración**. AEM Un conjunto de migración permite transferir contenido a los as a Cloud Service de la.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-2.png)

   >[!NOTE]
   >Un conjunto de migración caduca después de un período prolongado de inactividad. Consulte [Caducidad del conjunto de migración](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) para obtener más información.

   >[!NOTE]
   >Consulte [requisitos previos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html) y el [prácticas recomendadas y directrices](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) antes de utilizar la herramienta de transferencia de contenido.

1. Descargue e instale la herramienta de transferencia de contenido para rellenar el conjunto de migración y completar la fase de extracción de la transferencia de contenido. Revisar [Introducción a la herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=es) para aprender a utilizar la herramienta de transferencia de contenido.

1. AEM Para ingerir contenido del conjunto de migración en un entorno en el que esté as a Cloud Service, debe iniciar una ingesta. Vaya a **Trabajos de ingesta** y haga clic en **Nueva ingesta**. Revisar [Ingesta de contenido en Target](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html) para que pueda aprender a completar la fase de Ingesta de la transferencia de contenido.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-3.png)

<!--### Estimating Content Transfer Time {#calculating}

A Content Transfer Tool calculator has been provided to estimate how long it could take to complete the content transfer activity. You can use the content repository size slider to select the size that applies to your project. The transfer times vary for the extraction and ingestion phases. 

   ![image](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-4.png)

   >[!NOTE]
   >These times are estimates only. Factor such as network speeds and time to scale up instances have not been accounted for in these estimates.

To estimate the size of the AEM Repository, you can run the Disk Usage report under `http://HOST:PORT/etc/reports/diskusage.html`. 

You can also estimate the size of specific repository paths by using the `path` parameter, for example, `http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`. -->

## Siguientes pasos {#whats-next}

Después de haber aprendido a iniciar sesión en Cloud Acceleration Manager y a utilizar la fase de implementación, está listo para pasar a revisar el siguiente paso en la [Fase de lanzamiento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-golive-phase.html).
