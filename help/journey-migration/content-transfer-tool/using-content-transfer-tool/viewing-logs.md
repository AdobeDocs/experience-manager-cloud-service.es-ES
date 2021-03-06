---
title: Visualización de registros de un conjunto de migraciones en la herramienta de transferencia de contenido
description: Visualización de registros de un conjunto de migraciones en la herramienta de transferencia de contenido
exl-id: aed1ac83-a2fb-425e-aca4-39cd0bb42fd3
source-git-commit: 9a098eefbb730ae2930169cf7402ab4799043291
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 12%

---

# Visualización de registros del conjunto de migraciones {#view-logs-content-transfer-tool}


>[!CONTEXTUALHELP]
>id="aemcloud_ctt_logs"
>title="Visualización de registros"
>abstract="Una vez finalizada la Extracción de la Ingesta, compruebe los registros para ver si hay errores/advertencias. Cualquier error debe solucionarse inmediatamente, ya sea abordando los problemas notificados o poniéndose en contacto con el servicio de asistencia al Adobe."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#troubleshooting" text="Solución de problemas"
>additional-url="https://helpx.adobe.com/ca/enterprise/admin-guide.html/ca/enterprise/using/support-for-experience-cloud.ug.html" text="Contactar con el servicio de asistencia al Adobe"

Una vez completado cada paso (extracción e ingesta), compruebe los registros y busque errores.  Cualquier error debe solucionarse inmediatamente, ya sea abordando los problemas notificados o poniéndose en contacto con el servicio de asistencia al Adobe.

## Pasos para ver registros {#viewing-logs}

Para ver los registros de extracción, vaya a la instancia de Adobe Experience Manager de origen y seleccione el conjunto de migración deseado.

A continuación, siga los pasos a continuación:

1. Seleccione un conjunto de migración y haga clic en **Ver registro** de la barra de acciones. Esto abrirá el cuadro de diálogo Registros . Haga clic en **Registro de extracción** para ver los registros en una nueva pestaña.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam25.png) \
   O bien, haga clic en el botón **FINALIZADO** para ver los registros en una nueva pestaña.

1. Para rastrear los registros sin utilizar la interfaz de usuario, puede SSH en el entorno AEM de origen y seguir el `crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`.

1. Para ver los registros de ingesta, vaya a la lista Trabajos de ingesta en Cloud Acceleration Manager y haga clic en los tres puntos (**...**). A continuación, puede hacer clic en **Descargar registro** para descargar registros.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam28.png)
