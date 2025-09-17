---
title: Visualización de registros del conjunto de migraciones en la herramienta de transferencia de contenido
description: Visualización de registros del conjunto de migraciones en la herramienta de transferencia de contenido
exl-id: aed1ac83-a2fb-425e-aca4-39cd0bb42fd3
feature: Migration
role: Admin
source-git-commit: e1089810b3bf3db0cc440bb397e5549ade6eac37
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 36%

---

# Visualización de registros del conjunto de migración {#view-logs-content-transfer-tool}


>[!CONTEXTUALHELP]
>id="aemcloud_ctt_logs"
>title="Visualización de registros"
>abstract="Una vez finalizada la extracción de la ingesta, compruebe los registros para detectar si hay errores/advertencias. Cualquier error debe solucionarse inmediatamente, ya sea abordando los problemas notificados o poniéndose en contacto con el servicio de soporte técnico de Adobe."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=es#troubleshooting" text="Resolución de problemas"
>additional-url="https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html?lang=es" text="Contactar con el servicio de soporte técnico de Adobe"

Una vez completado cada paso (extracción e ingesta), compruebe los registros y busque errores.  Cualquier error debe solucionarse inmediatamente, ya sea abordando los problemas notificados o poniéndose en contacto con el servicio de soporte técnico de Adobe.

## Pasos para Ver Registros {#viewing-logs}

### Registros de extracción

Para ver los registros de extracción, vaya a la instancia de Adobe Experience Manager de origen y seleccione el conjunto de migración deseado.

A continuación, siga los pasos a continuación:

1. Seleccione un conjunto de migración y haga clic en **Ver registro** en la barra de acciones. Esto abre el cuadro de diálogo Registros. Haga clic en **Registro de extracción** para ver los registros en una nueva pestaña.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/logs.png) \
   O bien, haga clic en el estado **FINALIZADO** para ver los registros en una nueva pestaña.

1. Para rastrear los registros sin utilizar la interfaz de usuario, puede SSH en el entorno AEM de origen y seguir el `crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`.

### Registros de ingesta

Para ver los registros de ingesta, vaya a la lista de Trabajos de ingesta en Cloud Acceleration Manager, busque el trabajo de migración deseado y haga clic en los tres puntos (**...**) del trabajo. A continuación, puede hacer clic en **Descargar registro** para descargar los registros.

![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam28.png)
