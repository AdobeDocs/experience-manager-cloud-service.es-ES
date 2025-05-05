---
title: Ejecución de una canalización
description: En esta página se describe la ejecución de una canalización para el proyecto de Screens como Cloud Service en Cloud Manager.
exl-id: 3203cff7-5668-4f50-a2c5-80ae474b439d
feature: Screens Deployments
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 4%

---

# Ejecución de una canalización para el programa as a Cloud Service de Screens en Cloud Manager {#run-pipeline-screens-cloud}

En esta sección se describe cómo ejecutar la canalización e implementar el código para el programa en Cloud Manager.

>[!NOTE]
>Consulte [Configuración de la canalización de CI-CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/configuring-production-pipelines.html?lang=es) e [Implementación del código](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=es) para obtener información sobre cómo ejecutar la canalización para su programa en Cloud Manager.

## Objetivo {#objective}

En la siguiente sección se describe cómo configurar la canalización de CI/CD e implementar el código para el programa en Cloud Manager.

## Pasos para ejecutar una canalización para su proyecto de Screens en Cloud Manager {#steps-branch-creation}

1. Una vez que la configuración del entorno se haya completado correctamente, verá la actualización de la tarjeta de llamada a la acción en la página **Información general** de Cloud Manager.

   ![imagen](/help/screens-cloud/assets/onboarding/add-environ3.png)

1. Haga clic en **Configurar canalización** desde la página **Información general**.

1. Haga clic en **Siguiente** después de seleccionar la rama.

   ![imagen](/help/screens-cloud/assets/onboarding/run-pipeline1.png)

1. Seleccione sus opciones en el asistente **Configurar canalización**. Haga clic en **Guardar**.

   >[!NOTE]
   >Para obtener más información sobre las opciones del asistente Configurar canalización, consulte [Configuración de la canalización desde Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/configuring-production-pipelines.html?lang=es).

   ![imagen](/help/screens-cloud/assets/onboarding/run-pipeline2-a.png)

1. Una vez completada la configuración de la canalización, se actualiza la tarjeta de llamada a la acción.

   >[!NOTE]
   >Para obtener más información sobre las fases de la implementación en Cloud Manager, consulte [Implementación del código](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=es) para obtener más información.

   ![imagen](/help/screens-cloud/assets/onboarding/run-pipeline3.png)

1. Haga clic en **Implementar**.

1. Haga clic en **Generar** para iniciar el proceso de generación.

   ![imagen](/help/screens-cloud/assets/onboarding/run-pipeline4.png)

1. Una vez completado el proceso de compilación, puede ver un vínculo de autor desde la tarjeta **Entornos** de la página **Información general** de Cloud Manager.

   ![imagen](/help/screens-cloud/assets/onboarding/run-pipeline5.png)

## Siguientes pasos {#whats-next}

Después de haber aprendido a configurar un entorno para su programa en Cloud Manager, está listo para pasar al siguiente paso del proceso de incorporación: [Navegación al proveedor de servicios de Screens](/help/screens-cloud/configuring/navigating-to-screens-services-provider.md).
