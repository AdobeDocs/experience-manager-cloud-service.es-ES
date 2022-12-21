---
title: Ingesta de contenido en Target
description: Ingesta de contenido en Target
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: acddd68b61173ab956cafcc7168fd7f898973638
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 9%

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

>[!NOTE]
>¿Se acuerda de registrar un ticket de soporte para esta ingesta? Consulte [Consideraciones importantes antes de usar la herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html#important-considerations) para que esa y otras consideraciones ayuden a que la ingesta tenga éxito.

1. Vaya a Cloud Acceleration Manager. Haga clic en la tarjeta del proyecto y haga clic en la tarjeta de transferencia de contenido. Vaya a **Trabajos de Ingesta** y haga clic en **Nueva Ingesta**

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)


1. Revise la lista de comprobación de ingesta y asegúrese de que se han completado todos los pasos. Estos son pasos necesarios para garantizar una ingesta correcta. Podrá continuar con el **Siguiente** solo si se ha completado la lista de comprobación.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. Proporcione la información necesaria para crear una nueva ingesta.

   * Seleccione el conjunto de migración que acaba de extraer como origen
   * Seleccione el entorno de destino. Aquí es donde se incorporará el contenido del conjunto de migración. Seleccione el nivel. (Autor/Publicación).

   >[!NOTE]
   >
   >Si el origen era Autor, se recomienda ingerirlo en el nivel Autor del destino. Del mismo modo, si la fuente es Publicada, target también debe ser Publicado.

   >[!NOTE]
   >
   >Si el nivel de destino es `Author`, la instancia de autor se cerrará durante la ingesta y no estará disponible para los usuarios (por ejemplo, autores o cualquier persona que realice el mantenimiento, etc.). Esto es para proteger el sistema y evitar cualquier cambio que pueda perderse o causar un conflicto de ingesta. Asegúrese de que su equipo sea consciente de este hecho. Tenga en cuenta también que el entorno aparecerá en hibernación durante la ingesta del autor.

   >[!NOTE]
   >
   >Puede ejecutar el paso de precopia opcional para acelerar significativamente la fase de ingesta. Consulte [Ingesta con AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) para obtener más información.
   > 
   >Si se utiliza la ingesta con precopia (para S3 o Azure Data Store), se recomienda ejecutar la ingesta de Autor solo primero. Esto acelera la ingesta de Publicar cuando se ejecute más adelante.

   >[!IMPORTANT]
   >
   >Solo podrá iniciar una ingesta en el entorno de destino si pertenece al entorno local **Administradores de AEM** en el servicio de autor del Cloud Service de destino. Si no puede iniciar una ingesta, consulte [No se puede iniciar la ingesta](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion) para obtener más información.

   >[!IMPORTANT]
   >
   >Si la configuración **Barrido** se habilita antes de la ingesta, elimina todo el repositorio existente y crea un nuevo repositorio en el que introducir contenido. Esto significa que restablece toda la configuración, incluidos los permisos, en la instancia de Cloud Service de destino. Esto también se aplica a los usuarios administradores agregados a la variable **administradores** grupo. Debe volver a agregarlo al grupo de administradores para iniciar una ingesta.

1. Haga clic en **Ingesta**

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. A continuación, puede controlar la fase de Ingesta desde la vista de la lista Trabajos de Ingesta y utilizar el menú de acción de la ingesta para ver el registro a medida que progresa la ingesta.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

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
>id="aemcloud_ctt_ingestion_topup"
>title="Ingesta superior"
>abstract="Utilice la función superior para mover el contenido modificado desde la actividad de transferencia de contenido anterior. Una vez finalizada la ingesta, compruebe los registros en busca de errores/advertencias. Cualquier error debe solucionarse inmediatamente, ya sea abordando los problemas notificados o poniéndose en contacto con el Servicio de atención al cliente de Adobe."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html?lang=en" text="Visualización de registros"

La herramienta de transferencia de contenido tiene una función que permite *agregar* contenido diferencial donde solo es posible transferir los cambios realizados desde la actividad de transferencia de contenido anterior.

>[!NOTE]
>Después de la transferencia de contenido inicial, se recomienda realizar frecuentes recargas de contenido diferencial para acortar el período de congelación de contenido para la transferencia de contenido diferencial final antes de lanzarse a Cloud Service. Si ha utilizado el paso de precopia para la primera ingesta completa, puede omitir la precopia para las próximas ingestas superiores (si el tamaño del conjunto de migración superior es inferior a 200 GB) porque puede añadir tiempo a todo el proceso.

Una vez completado el proceso de ingesta, para ingerir el contenido delta deberá ejecutar un [Extracción superior](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process) y, a continuación, utilice el método de ingesta superior.

Para ello, cree un nuevo trabajo de ingesta y asegúrese de que **Barrido** se desactiva durante la fase de ingesta, como se muestra a continuación:

![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## Solución de problemas {#troubleshooting}

### CAM No se puede recuperar el token de migración {#cam-unable-to-retrieve-the-migration-token}

La recuperación automática del token de migración puede fallar por diferentes motivos, incluido usted [configuración de una lista de permitidos IP mediante Cloud Manager](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) en el entorno de Cloud Service de destino. En estos casos, verá el cuadro de diálogo siguiente cuando intente iniciar una ingesta:

![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/troubleshooting-token.png)

Deberá recuperar el token de migración manualmente haciendo clic en el vínculo &quot;Obtener token&quot; del cuadro de diálogo. Se abrirá otra ficha que muestra el token. A continuación, puede copiar el token y pegarlo en el **Entrada del token de migración** campo . Ahora, debería poder iniciar la ingesta.

>[!NOTE]
>
>El token estará disponible para los usuarios que pertenezcan a la función local **Administradores de AEM** en el servicio de autor del Cloud Service de destino.

### No se puede iniciar la ingesta {#unable-to-start-ingestion}

Solo podrá iniciar una ingesta en el entorno de destino si pertenece al entorno local **Administradores de AEM** en el servicio de autor del Cloud Service de destino. Si no pertenece al grupo de administradores de AEM, verá un error como se muestra a continuación cuando intente iniciar una ingesta. Puede solicitar al administrador que lo añada a la **Administradores de AEM** o pida el propio token, que puede pegar en el **Entrada del token de migración** campo .

![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/error_nonadmin_ingestion.png)

### Las actualizaciones automáticas a través de Release Orchestrator siguen habilitadas

Release Orchestrator mantiene los entornos actualizados automáticamente mediante la aplicación de actualizaciones. Si la actualización se activa cuando se realiza una ingesta, puede causar resultados impredecibles, incluida la corrupción del entorno. Esta es una de las razones por las que se debe registrar un ticket de soporte antes de iniciar una ingesta (consulte &quot;Nota&quot; anterior), de modo que se pueda programar la desactivación temporal de Release Orchestrator.

Si Release Orchestrator aún se está ejecutando cuando se está iniciando una ingesta, la interfaz de usuario presentará este mensaje de error. Puede optar por continuar de todas formas, aceptando el riesgo, marcando el campo y presionando el botón de nuevo.

![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/error_releaseorchestrator_ingestion.png)

### Fallo de ingesta superior

Una causa común de una [Ingesta superior](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) error es un conflicto en los id de nodo. Para identificar este error, descargue el registro de ingesta mediante la interfaz de usuario de Cloud Acceleration Manager y busque una entrada como la siguiente:

>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakConstraint0030: Propiedad de restricción de uniformidad violada [jcr:uuid] con el valor a1a1a1a1-b2b2-c3c3-d4d4-e5e5e5e5e5e5: /some/path/jcr:content, /some/other/path/jcr:content

Cada nodo de AEM debe tener un uuid único. Este error indica que un nodo que se está incorporando tiene el mismo uuid que uno que ya existe en una ruta diferente de la instancia de destino.
Esto puede suceder si se mueve un nodo en el origen entre una extracción y una [Extracción superior](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process).
También puede ocurrir si un nodo del destino se mueve entre una ingesta y una ingesta superior posterior.

Este conflicto debe resolverse manualmente. Alguien familiarizado con el contenido debe decidir cuál de los dos nodos debe eliminarse, teniendo en cuenta otro contenido que hace referencia a él. La solución puede requerir que la extracción superior se realice de nuevo sin el nodo infractor.

## Siguientes pasos {#whats-next}

Una vez que haya completado la ingesta de contenido en Target, puede ver los registros de cada paso (extracción e ingesta) y buscar errores. Consulte [Visualización de registros de un conjunto de migraciones](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html?lang=en) para obtener más información.