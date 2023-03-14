---
title: Ejecución de una canalización
description: En esta página se describe la ejecución de una canalización para el proyecto Screens as a Cloud Service en Cloud Manager.
exl-id: 3203cff7-5668-4f50-a2c5-80ae474b439d
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 8%

---

# Ejecución de una canalización para el programa as a Cloud Service Screens en Cloud Manager {#run-pipeline-screens-cloud}

En esta sección se describe cómo ejecutar la canalización e implementar el código para el programa en Cloud Manager.

>[!NOTE]
>Consulte [Configuración de la canalización de CD-CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en) y [Implemente su código](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=es) para obtener información sobre cómo ejecutar la canalización para su programa en Cloud Manager.

## Objetivo {#objective}

En la siguiente sección se describe cómo configurar la canalización de CI/CD e implementar el código para su programa en Cloud Manager.

## Pasos para ejecutar una canalización para su proyecto de Screens en Cloud Manager {#steps-branch-creation}

1. Una vez que la configuración del entorno se haya completado correctamente, verá la actualización de la tarjeta de llamada a la acción en el **Información general** página.

   ![imagen](/help/screens-cloud/assets/onboarding/add-environ3.png)

1. Haga clic en **Configurar canalización** desde el **Información general** página.

1. Haga clic en **Siguiente** después de seleccionar la rama.

   ![imagen](/help/screens-cloud/assets/onboarding/run-pipeline1.png)

1. Seleccione las opciones en la **Configurar canalización** asistente. Haga clic en **Guardar**.

   >[!NOTE]
   >Para obtener más información sobre las opciones del asistente Configurar canalización, consulte [Configuración de la canalización desde Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en) para obtener más información.

   ![imagen](/help/screens-cloud/assets/onboarding/run-pipeline2-a.png)

1. Una vez completada la configuración, la tarjeta de llamada a la acción se actualiza, como se muestra en la figura siguiente. Haga clic en Implementar.

   >[!NOTE]
   >Para obtener más información sobre las fases de la implementación en Cloud Manager, consulte [Implementar el código](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=es) para obtener más información.

   ![imagen](/help/screens-cloud/assets/onboarding/run-pipeline3.png)

1. Haga clic en **Generar** para iniciar el proceso de generación.

   ![imagen](/help/screens-cloud/assets/onboarding/run-pipeline4.png)

1. Una vez completado el proceso de generación, verá un vínculo de autor desde el **Entornos** Tarjeta del servidor de Cloud Manager **Información general** página.

   ![imagen](/help/screens-cloud/assets/onboarding/run-pipeline5.png)

## Siguientes pasos {#whats-next}

Una vez que haya aprendido a configurar un entorno para su programa en Cloud Manager, ya está listo para pasar al siguiente paso en el proceso de incorporación y es decir, [Navegación al proveedor de servicios de Screens](/help/screens-cloud/configuring/navigating-to-screens-services-provider.md).
