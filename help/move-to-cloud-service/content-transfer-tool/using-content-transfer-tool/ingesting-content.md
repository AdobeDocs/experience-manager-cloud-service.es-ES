---
title: Ingesta de contenido en Target en la herramienta de transferencia de contenido
description: Ingesta de contenido en Target en la herramienta de transferencia de contenido
source-git-commit: d638fe0f4711bd152bd9c4be99a68662f12072e6
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 34%

---


# Ingesta de contenido en Target en la herramienta de transferencia de contenido {#ingesting-content}

## Proceso de Ingesta en la herramienta de transferencia de contenido {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="Ingesta de contenido"
>abstract="La ingesta hace referencia a la ingesta de contenido del conjunto de migración en la instancia de Cloud Service de destino. La herramienta de transferencia de contenido tiene una función que permite agregar contenido diferencial donde solo es posible transferir los cambios realizados desde la actividad de transferencia de contenido anterior."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-ingestion-process" text="Ingesta superior"

Siga los pasos a continuación para ingerir el conjunto de migración de la herramienta de transferencia de contenido:
>[!NOTE]
>Si se utiliza Amazon S3 o Azure Data Store como tipo de almacén de datos, puede ejecutar el paso de precopia opcional para acelerar significativamente la fase de ingesta. Consulte [Ingesta con AzCopy](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#ingesting-azcopy) para obtener más información.

1. Seleccione un conjunto de migración de la página **Transferencia de contenido** y haga clic en **Ingesta** para iniciar la ingesta.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ingestion-01.png)

1. Aparece el cuadro de diálogo **ingesta de conjunto de migración** . El contenido se puede ingerir en una instancia de Autor o en una instancia de Publicación a la vez. Seleccione la instancia en la que desee introducir el contenido. Haga clic en **Ingesta** para iniciar la fase de ingesta.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ingestion-02.png)

   >[!IMPORTANT]
   >Si se utiliza la ingesta con precopia (para S3 o Azure Data Store), se recomienda ejecutar la ingesta de Autor solo primero. Esto acelera la ingesta de Publicar cuando se ejecute más adelante.

   >[!IMPORTANT]
   >Cuando la opción **Borrar contenido existente en la instancia de Cloud antes de la ingesta** está habilitada, elimina todo el repositorio existente y crea un nuevo repositorio en el que introducir contenido. Esto significa que restablece toda la configuración, incluidos los permisos, en la instancia de Cloud Service de destino. Esto también se aplica a los usuarios administradores agregados al grupo **administradores**.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ingestion-03.png)

   Además, haga clic en **Servicio de atención al cliente** para registrar un ticket, como se muestra en la figura siguiente.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ingestion-04.png)

   Consulte también [Consideraciones importantes sobre el uso de la herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en#important-considerations) para obtener más información.

1. Una vez finalizada la ingesta, el estado en **Autor ingestion** se actualiza a **FINISHED**.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/15-ingestion-complete.png)

## Ingesta superior {#top-up-ingestion-process}

La herramienta de transferencia de contenido tiene una función que permite *agregar* contenido diferencial donde solo es posible transferir los cambios realizados desde la actividad de transferencia de contenido anterior.

>[!NOTE]
>Después de la transferencia de contenido inicial, se recomienda realizar frecuentes recargas de contenido diferencial para acortar el período de congelación de contenido para la transferencia de contenido diferencial final antes de lanzarse a Cloud Service.

Una vez completado el proceso de ingesta, se puede usar el contenido delta mediante el método de ingesta superior. Complete los siguientes pasos:

1. Vaya a la página *Información general* y seleccione el conjunto de migración para el que desea realizar la ingesta superior. Haga clic en **Ingesta** para iniciar la extracción superior. Aparece el cuadro de diálogo **ingesta de conjunto de migración** .

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/content-ingestion-02.png)

   >[!IMPORTANT]
   >Debe desactivar la opción **Borrar contenido existente en la instancia de Cloud antes de la ingesta** para evitar que se elimine el contenido existente de la actividad de ingesta anterior. Además, haga clic en **Servicio de atención al cliente** para registrar un ticket, como se muestra en la figura anterior.
