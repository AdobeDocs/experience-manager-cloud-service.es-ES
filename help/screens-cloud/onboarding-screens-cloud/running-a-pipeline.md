---
title: Ejecución de una canalización
description: En esta página se describe la ejecución de una canalización para el proyecto Screens as a Cloud Service en Cloud Manager.
exl-id: 3203cff7-5668-4f50-a2c5-80ae474b439d
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 3%

---

# Ejecución de una canalización para el programa as a Cloud Service Screens en Cloud Manager {#run-pipeline-screens-cloud}

En esta sección se describe cómo ejecutar la canalización e implementar el código para el programa en Cloud Manager.

>[!NOTE]
>Consulte [Configuración de la canalización de CI-CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/configuring-production-pipelines.html?lang=en) y [Implemente su código](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=en) para obtener información sobre cómo ejecutar la canalización para su programa en Cloud Manager.

## Objetivo {#objective}

En la siguiente sección se describe cómo configurar la canalización de CI/CD e implementar el código para su programa en Cloud Manager.

## Pasos para ejecutar una canalización para su proyecto de Screens en Cloud Manager {#steps-branch-creation}

1. Una vez completada correctamente la configuración del entorno, verá la actualización de la tarjeta de llamada a la acción en el **Información general** página.

   ![imagen](/help/screens-cloud/assets/onboarding/add-environ3.png)

1. Clic **Configurar canalización** desde el **Información general** página.

1. Clic **Siguiente** después de seleccionar la rama.

   ![imagen](/help/screens-cloud/assets/onboarding/run-pipeline1.png)

1. Seleccione las opciones en la **Configurar canalización** asistente. Haga clic en **Guardar**.

   >[!NOTE]
   >Para obtener más información sobre las opciones del asistente Configurar canalización, consulte [Configuración de la canalización desde Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/configuring-production-pipelines.html?lang=en) para obtener más información.

   ![imagen](/help/screens-cloud/assets/onboarding/run-pipeline2-a.png)

1. Una vez completada la configuración de la canalización, se actualiza la tarjeta de llamada a la acción.

   >[!NOTE]
   >Para obtener más información sobre las fases de la implementación en Cloud Manager, consulte [Implementar el código](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=en) para obtener más información.

   ![imagen](/help/screens-cloud/assets/onboarding/run-pipeline3.png)

1. Clic **Implementar**.

1. Clic **Generar** para iniciar el proceso de generación.

   ![imagen](/help/screens-cloud/assets/onboarding/run-pipeline4.png)

1. Una vez completado el proceso de generación, verá un vínculo de autor desde el **Entornos** Tarjeta del servidor de Cloud Manager **Información general** página.

   ![imagen](/help/screens-cloud/assets/onboarding/run-pipeline5.png)

## Siguientes pasos {#whats-next}

Después de haber aprendido a configurar un entorno para su programa en Cloud Manager, está listo para pasar al siguiente paso en el proceso de incorporación: [Navegación al proveedor de servicios de Screens](/help/screens-cloud/configuring/navigating-to-screens-services-provider.md).
