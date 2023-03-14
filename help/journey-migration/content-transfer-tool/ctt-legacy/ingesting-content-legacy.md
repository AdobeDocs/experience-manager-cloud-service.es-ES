---
title: Ingesta de contenido en Target (heredado)
description: Ingesta de contenido en Target
hide: true
hidefromtoc: true
exl-id: 326b3e98-5055-49b5-a005-63fd3ca35202
source-git-commit: 22bbf15e33ab3d5608dc01ed293bb04b07cb6c8c
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 27%

---

# Ingesta de contenido en Target (heredado) {#ingesting-content}

## Proceso de ingesta en la herramienta de transferencia de contenido {#ingestion-process}

Siga los pasos a continuación para ingerir el conjunto de migración de la herramienta de transferencia de contenido:
>[!NOTE]
>Puede ejecutar el paso opcional previo a la copia para acelerar de forma significativa la fase de ingesta. Consulte [Ingesta con AzCopy](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#ingesting-azcopy) para obtener más información.

1. Seleccione un conjunto de migración de **Transferencia de contenido** y haga clic en **Ingesta** para iniciar la ingesta.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. Aparece el cuadro de diálogo **ingesta de conjunto de migración** . El contenido se puede introducir en la instancia de autor o en la instancia de publicación a la vez. Seleccione la instancia en la que desea introducir el contenido. Haga clic en **Ingesta** para iniciar la fase de ingesta.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-02.png)

   >[!IMPORTANT]
   >Si se utiliza la ingesta con copia previa (para S3 o Azure Data Store), se recomienda ejecutar primero la ingesta de autor solo. Esto acelera la ingesta de Publish cuando se ejecute más adelante.

   >[!IMPORTANT]
   >Si la variable **Borrar contenido existente en la instancia de Cloud antes de la ingesta** está activada, elimina todo el repositorio existente y crea un nuevo repositorio para introducir contenido en. Esto significa que restablece todos los ajustes, incluidos los permisos en la instancia del Cloud Service de destino. Esto también se aplica a un usuario administrador añadido a **administradores** grupo.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-03.png)

   Además, haga clic en **Atención al cliente** para registrar un ticket, como se muestra en la figura siguiente.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-04.png)

   Además, consulte [Consideraciones importantes sobre el uso de la herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en#important-considerations) para obtener más información.

1. Una vez finalizada la ingesta, el estado será **Ingesta de autor** actualizaciones de **FINALIZADO**.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-05.png)

## Ingesta superior {#top-up-ingestion-process}

La herramienta de transferencia de contenido tiene una función que permite *agregar* contenido diferencial donde solo es posible transferir los cambios realizados desde la actividad de transferencia de contenido anterior.

>[!NOTE]
>Después de la transferencia de contenido inicial, se recomienda realizar frecuentes recargas de contenido diferencial para acortar el período de congelación de contenido para la transferencia de contenido diferencial final antes de lanzarse a Cloud Service.

Una vez completado el proceso de ingesta, se puede usar el contenido delta mediante el método de ingesta superior. Complete los siguientes pasos:

1. Vaya a **Transferencia de contenido** y seleccione el conjunto de migración para el que desea realizar la ingesta superior. Haga clic en **Ingesta** para iniciar la extracción superior.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/topup-ingest1.png)


1. Aparece el cuadro de diálogo **ingesta de conjunto de migración** .

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/topup-ingest2.png)

   >[!IMPORTANT]
   >Debe deshabilitar la variable **Borrar contenido existente en la instancia de Cloud antes de la ingesta** , para evitar eliminar el contenido existente de la actividad de ingesta anterior. Además, haga clic en **Atención al cliente** para registrar un ticket, como se muestra en la figura anterior.

## Siguientes pasos {#whats-next}

Una vez que haya aprendido a ingerir contenido en Target en la herramienta de transferencia de contenido, puede ver los registros al finalizar cada paso (extracción e ingesta) y buscar errores. Consulte [Visualización de registros del conjunto de migraciones](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html?lang=en) para obtener más información.
