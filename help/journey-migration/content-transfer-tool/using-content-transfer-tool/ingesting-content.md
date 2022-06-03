---
title: Ingesta de contenido en Target
description: Ingesta de contenido en Target
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: 05765bdaa681502b60fc5a7c943e2265c09764ec
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 17%

---

# Ingesta de contenido en Target {#ingesting-content}

## Proceso de Ingesta en la herramienta de transferencia de contenido {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="Ingesta de contenido"
>abstract="La ingesta hace referencia a la ingesta de contenido del conjunto de migración en la instancia de Cloud Service de destino. La herramienta de transferencia de contenido tiene una función que permite agregar contenido diferencial donde solo es posible transferir los cambios realizados desde la actividad de transferencia de contenido anterior."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-ingestion-process" text="Ingesta superior"

Siga los pasos a continuación para ingerir el conjunto de migración de la herramienta de transferencia de contenido:
>[!NOTE]
>Puede ejecutar el paso de precopia opcional para acelerar significativamente la fase de ingesta. El paso de precopia es más eficaz para la primera extracción e ingesta completa. Consulte [Ingesta con AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) para obtener más información.

1. Vaya a Cloud Acceleration Manager. Haga clic en la tarjeta del proyecto y haga clic en la tarjeta de transferencia de contenido. Vaya a **Trabajos de Ingesta** y haga clic en **Nueva Ingesta**

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. Proporcione la información necesaria para crear una nueva ingesta.

   * Seleccione el conjunto de migración que acaba de extraer como origen
   * Seleccione el entorno de destino. Aquí es donde se incorporará el contenido del conjunto de migración. Seleccione el nivel. (Autor/Publicación).

   >[!NOTE]
   >
   >Si el origen era Autor, se recomienda ingerirlo en el nivel Autor del destino. Del mismo modo, si la fuente es Publicada, target también debe ser Publicado.

   >[!NOTE]
   >
   >Puede ejecutar el paso de precopia opcional para acelerar significativamente la fase de ingesta. Consulte [Ingesta con AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) para obtener más información.
   > 
   >Si se utiliza la ingesta con precopia (para S3 o Azure Data Store), se recomienda ejecutar la ingesta de Autor solo primero. Esto acelera la ingesta de Publicar cuando se ejecute más adelante.

   >[!IMPORTANT]
   >
   >Solo podrá iniciar una ingesta en el entorno de destino si pertenece al entorno local **Administradores de AEM** en la instancia de Cloud Service que está transfiriendo el contenido. Si no pertenece al grupo de administradores de AEM, verá un error como se muestra a continuación cuando intente iniciar una ingesta.
   >![image](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam21.png)

   >[!IMPORTANT]
   >
   >Si la configuración **Barrido** se habilita antes de la ingesta, elimina todo el repositorio existente y crea un nuevo repositorio en el que introducir contenido. Esto significa que restablece toda la configuración, incluidos los permisos, en la instancia de Cloud Service de destino. Esto también se aplica a los usuarios administradores agregados a la variable **administradores** grupo. Debe volver a agregarlo al grupo de administradores para iniciar una ingesta.

1. Haga clic en **Ingesta**

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. A continuación, puede controlar la fase de ingesta desde la vista de lista Trabajos de ingesta

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. Una vez finalizada la ingesta, haga clic en el botón (i) en la esquina superior derecha de la pantalla para obtener más información sobre el trabajo de ingesta.

<!-- Alexandru: hiding temporarily, until it's reviewed 

1. The **Migration Set ingestion** dialog box displays. Content can be ingested to either Author instance or Publish instance at a time. Select the instance to ingest content to. Click on **Ingest** to start the ingestion phase. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-02.png)

   >[!IMPORTANT]
   >If ingesting with pre-copy is used (for S3 or Azure Data Store), it is recommended to run Author ingestion first alone. This will speed up the Publish ingestion when it is run later. 

   >[!IMPORTANT]
   >When the **Wipe existing content on Cloud instance before ingestion** option is enabled, it deletes the entire existing repository and creates a new repository to ingest content into. This means that it resets all settings including permissions on the target Cloud Service instance. This is also true for an admin user added to the **administrators** group.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-03.png)

   Additionally, click on **Customer Care** to log a ticket, as shown in the figure below. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-04.png)
   
   Also, refer to [Important Considerations for Using Content Transfer Tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en#important-considerations) to learn more.

1. Once the ingestion is complete, the status under **Author ingestion** updates to **FINISHED**.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-05.png) -->

## Ingesta superior {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup" title="Top Up Ingestion"
>abstract="Utilice la función superior para mover el contenido modificado desde la actividad de transferencia de contenido anterior. Una vez finalizada la ingesta, compruebe los registros en busca de errores/advertencias. Cualquier error debe solucionarse inmediatamente, ya sea abordando los problemas notificados o poniéndose en contacto con el Servicio de atención al cliente de Adobe."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html?lang=en" text="Visualización de registros"

La herramienta de transferencia de contenido tiene una función que permite *agregar* contenido diferencial donde solo es posible transferir los cambios realizados desde la actividad de transferencia de contenido anterior.

>[!NOTE]
>Después de la transferencia de contenido inicial, se recomienda realizar frecuentes recargas de contenido diferencial para acortar el período de congelación de contenido para la transferencia de contenido diferencial final antes de lanzarse a Cloud Service. Si ha utilizado el paso de precopia para la primera ingesta completa, puede omitir la precopia para las próximas ingestas superiores (si el tamaño del conjunto de migración superior es inferior a 200 GB) porque puede añadir tiempo a todo el proceso.

Una vez completado el proceso de ingesta, para ingerir el contenido delta deberá ejecutar un [Extracción superior](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process) y, a continuación, utilice el método de ingesta superior.

Para ello, cree un nuevo trabajo de ingesta y asegúrese de que **Barrido** se desactiva durante la fase de ingesta, como se muestra a continuación:

![image](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)



## Siguientes pasos {#whats-next}

Una vez que haya aprendido a Ingresar contenido en Target en la herramienta de transferencia de contenido, puede ver los registros una vez completado cada paso (extracción e ingesta) y buscar errores. Consulte [Visualización de registros de un conjunto de migraciones](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html?lang=en) para obtener más información.
