---
title: Ejecución de una canalización
description: En esta página se describe cómo ejecutar una canalización para Screens como proyecto de Cloud Service en Cloud Manager.
hide: true
hidefromtoc: true
index: false
source-git-commit: 83d2ac2d22827ebe13578b900907dd089d8d7e45
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 2%

---


# Ejecución de una canalización para Screens as a Cloud Service Program en Cloud Manager {#run-pipeline-screens-cloud}

En esta sección se describe cómo ejecutar la canalización e implementar el código para el programa en Cloud Manager.

>[!NOTE]
>Consulte [Configuración de la canalización de CD-CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en) e [Implementación del código](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en) para obtener información sobre cómo ejecutar la canalización de su programa en Cloud Manager.

## Objetivo {#objective}

En la siguiente sección se describe cómo configurar la canalización de CI/CD e implementar el código para el programa en Cloud Manager.

## Pasos para ejecutar una canalización para su proyecto Screens en Cloud Manager {#steps-branch-creation}

1. Una vez que la configuración del entorno se haya completado correctamente, verá la actualización de la tarjeta de llamada a la acción en la página **Información general** de Cloud Manager.

   ![image](/help/screens-cloud/assets/onboarding/add-environ3.png)

1. Haga clic en **Configuración de canalización** en la página **Información general**.

1. Haga clic en **Next** después de seleccionar la rama.

   ![image](/help/screens-cloud/assets/onboarding/run-pipeline1.png)

1. Seleccione las opciones en el asistente **Configuración de canalización**. Haga clic en **Save**.

   >[!NOTE]
   >Para obtener más información sobre las opciones del asistente Configuración de canalización , consulte [Configuración de canalización de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en) para obtener más información.

   ![image](/help/screens-cloud/assets/onboarding/run-pipeline2-a.png)

1. Una vez finalizada la canalización de configuración, la tarjeta de llamada a la acción se actualiza, como se muestra en la figura siguiente. Haga clic en Implementar.

   >[!NOTE]
   >Para obtener más información sobre las fases de implementación en Cloud Manager, consulte [Implementación del código](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en) para obtener más información.

   ![image](/help/screens-cloud/assets/onboarding/run-pipeline3.png)

1. Haga clic en **Build** para iniciar el proceso de compilación.

   ![image](/help/screens-cloud/assets/onboarding/run-pipeline4.png)

1. Una vez que se complete el proceso de compilación, verá un vínculo de autor desde la tarjeta **Environments** de la página **Overview** de Cloud Manager.

   ![image](/help/screens-cloud/assets/onboarding/run-pipeline5.png)

## Siguientes {#whats-next}

Una vez que haya aprendido a configurar un entorno para su programa en Cloud Manager, ya está listo para pasar al siguiente paso en el proceso de incorporación, es decir, [Navegar al proveedor de servicios de Screens](/help/screens-cloud/configuring/navigating-to-screens-services-provider.md).