---
title: Ingesta de contenido en Target
description: Ingesta de contenido en Target
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1732'
ht-degree: 12%

---

# Ingesta de contenido en Target {#ingesting-content}

## Proceso de ingesta en la herramienta de transferencia de contenido {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="Ingesta de contenido"
>abstract="Hace referencia a la ingesta de contenido del conjunto de migración en la instancia de Cloud Service del destinatario. La herramienta de transferencia de contenido tiene una función que permite agregar contenido diferencial donde solo es posible transferir los cambios realizados desde la actividad de transferencia de contenido anterior."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=es#top-up-ingestion-process" text="Ingesta superior"

Siga los pasos a continuación para ingerir el conjunto de migración de la herramienta de transferencia de contenido:

>[!NOTE]
>¿Se acordó de registrar un ticket de asistencia para esta ingesta? Consulte [Consideraciones importantes antes de utilizar la herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html#important-considerations) por esa y otras consideraciones para ayudar a que la ingesta sea exitosa.

1. Vaya a Cloud Acceleration Manager. Haga clic en la tarjeta de proyecto y en la tarjeta Transferencia de contenido. Vaya a **Trabajos de ingesta** y haga clic en **Nueva ingesta**

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. Revise la lista de comprobación de ingesta y asegúrese de que se han completado todos los pasos. Estos son los pasos necesarios para garantizar una ingesta correcta. Continúe con la **Siguiente** solo si se ha completado la lista de comprobación.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. Proporcione la información necesaria para crear una nueva ingesta.

   * Seleccione el conjunto de migración que contiene los datos extraídos como origen.
      * Los conjuntos de migración caducarán después de un período de inactividad prolongado, por lo que se espera que la ingesta se produzca relativamente pronto después de realizar la extracción. Revisar [Caducidad del conjunto de migración](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) para obtener más información.
   * Seleccione el entorno de destino. En este entorno es donde se ingiere el contenido del conjunto de migración. Seleccione el nivel. (Autor/Publicación). Los entornos de desarrollo rápido no son compatibles.

   >[!NOTE]
   >Las siguientes notas se aplican a la ingesta de contenido:
   > Si el origen era Author, se recomienda ingerirlo en el nivel Author en el destino. Del mismo modo, si el origen era Publish, el destino también debería ser Publish.
   > Si el nivel de destino es `Author`Sin embargo, la instancia de autor se apaga durante la duración de la ingesta y no está disponible para los usuarios (por ejemplo, los autores o cualquier persona que realice mantenimiento). El motivo es proteger el sistema y evitar cualquier cambio que pueda perderse o causar un conflicto de ingesta. Asegúrese de que su equipo esté al tanto de este hecho. Tenga en cuenta también que el entorno parece hibernado durante la ingesta del autor.
   > Puede ejecutar el paso opcional previo a la copia para acelerar de forma significativa la fase de ingesta. Consulte [Ingesta con AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) para obtener más información.
   > Si se utiliza la ingesta con copia previa (para S3 o Azure Data Store), se recomienda ejecutar primero la ingesta de autor solo. Al hacerlo, se acelera la ingesta de Publish cuando se ejecuta más adelante.
   > Las ingestas no admiten un destino de entorno de desarrollo rápido (RDE) y no aparecen como una posible opción de destino, aunque el usuario tenga acceso a él.

   >[!IMPORTANT]
   > Los siguientes avisos importantes se aplican a la ingesta de contenido:
   > Solo puede iniciar una ingesta en el entorno de destino si pertenece al entorno local de **AEM administradores de** en el servicio de creación del Cloud Service de destino. Si no puede iniciar una ingesta, consulte [No se puede iniciar la ingesta](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion) para obtener más información.
   > Si la configuración **Barrido** está habilitado antes de la ingesta, elimina todo el repositorio existente y crea un nuevo repositorio en el que introducir contenido. Esto significa que restablece todos los ajustes, incluidos los permisos en la instancia del Cloud Service de destino. Esto también se aplica a un usuario administrador añadido a **administradores** grupo. Debe volver a agregarse al grupo de administradores para iniciar una ingesta.

1. Haga clic en **Ingesta**

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. A continuación, puede monitorizar la fase de ingesta desde la vista de lista de Trabajos de ingesta y utilizar el menú de acción de la ingesta para ver el registro a medida que progresa la ingesta.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. Haga clic en **(i)** en la fila para obtener más información sobre el trabajo de ingesta. Puede ver la duración de cada paso de la ingesta cuando se ejecuta o completa haciendo clic en **...** y luego en **Ver duraciones**. La información de la extracción también muestra que se da cuenta de lo que se está ingiriendo.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23b.png)

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
   
   Also, refer to [Important Considerations for Using Content Transfer Tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html#important-considerations) to learn more.

1. Once the ingestion is complete, the status under **Author ingestion** updates to **FINISHED**.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-05.png) -->

## Ingesta superior {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup"
>title="Ingesta superior"
>abstract="Utilice la función superior para mover el contenido modificado desde la actividad de transferencia de contenido anterior. Una vez finalizada la ingesta, compruebe si hay errores/advertencias en los registros. Los errores deben solucionarse inmediatamente, ya sea abordando los problemas notificados o poniéndose en contacto con el Servicio de atención al cliente de Adobe."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html?lang=es" text="Visualización de registros"

La herramienta de transferencia de contenido tiene una función que permite *agregar* contenido diferencial donde solo es posible transferir los cambios realizados desde la actividad de transferencia de contenido anterior.

>[!NOTE]
>Después de la transferencia de contenido inicial, se recomienda realizar frecuentes recargas de contenido diferencial para acortar el período de congelación de contenido para la transferencia de contenido diferencial final antes de lanzarse a Cloud Service. Si ha utilizado el paso de precopia para la primera ingesta completa, puede omitir la precopia para las ingestas de recarga posteriores (si el tamaño del conjunto de migración de recarga es inferior a 200 GB), ya que puede añadir tiempo a todo el proceso.

Una vez completado el proceso de ingesta, para ingerir el contenido delta deberá ejecutar un [Extracción Superior](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process) y, a continuación, utilice el método de ingesta superior.

Puede hacerlo creando un nuevo trabajo de ingesta y asegurándose de que **Barrido** se desactiva durante la fase de Ingesta, como se muestra a continuación:

![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## Solución de problemas {#troubleshooting}

### CAM no puede recuperar el token de migración {#cam-unable-to-retrieve-the-migration-token}

La recuperación automática del token de migración puede fallar por diferentes motivos, entre los que se incluye [configuración de una lista de permitidos IP mediante Cloud Manager](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) en el entorno del Cloud Service de destino. En estos casos, verá el siguiente cuadro de diálogo cuando intente iniciar una ingesta:

![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/troubleshooting-token.png)

Deberá recuperar el token de migración manualmente haciendo clic en el vínculo &quot;Obtener token&quot; del cuadro de diálogo. Se abrirá otra pestaña que muestra el token. A continuación, puede copiar el token y pegarlo en **Entrada de token de migración** field. Ahora, debería poder iniciar la ingesta.

>[!NOTE]
>
>El token está disponible para los usuarios que pertenecen al **AEM administradores de** en el servicio de creación del Cloud Service de destino.

### No se puede iniciar la ingesta {#unable-to-start-ingestion}

Solo puede iniciar una ingesta en el entorno de destino si pertenece al entorno local de **AEM administradores de** en el servicio de creación del Cloud Service de destino. AEM Si no pertenece al grupo de administradores de la, verá un error como se muestra a continuación cuando intente iniciar una ingesta. Puede pedir al administrador que le añada al local **AEM administradores de** o pida el token en sí, que puede pegar en la variable **Entrada de token de migración** field.

![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/error_nonadmin_ingestion.png)

### No se puede conectar con el servicio de migración {#unable-to-reach-migration-service}

Después de solicitar una ingesta, se puede presentar al usuario un mensaje como el siguiente: &quot;Actualmente, no se puede acceder al servicio de migración en el entorno de destino. Vuelva a intentarlo más tarde o póngase en contacto con el soporte de Adobe&quot;.

![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/error_cannot_reach_migser.png)

Esto indica que Cloud Acceleration Manager no pudo llegar al servicio de migración del entorno de destino para iniciar la ingesta. Esto puede ocurrir por varias razones.

>[!NOTE]
> 
> El campo &quot;Token de migración&quot; se muestra porque, en algunos casos, la recuperación de ese token es lo que realmente no está permitido. Al permitir que se proporcione manualmente, puede permitir al usuario iniciar la ingesta rápidamente, sin ninguna ayuda adicional. Si se proporciona el token, y sigue apareciendo el mensaje, la recuperación del token no fue el problema.

* AEM El estado del entorno se mantiene en as a Cloud Service y, ocasionalmente, es posible que deba reiniciar el servicio de migración por varios motivos normales. Si ese servicio se está reiniciando, no se puede acceder a él, pero suele estar disponible pronto.
* Es posible que se esté ejecutando otro proceso en la instancia. Por ejemplo, si Release Orchestrator aplica una actualización, el sistema puede estar ocupado y el servicio de migración no está disponible con regularidad. Esta es la razón por la que se recomienda pausar las actualizaciones durante una ingesta, así como la posibilidad de corromper la instancia de fase o producción.
* Si un [Se ha aplicado la Lista de permitidos IP](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) a través de Cloud Manager, bloqueará Cloud Acceleration Manager para que no llegue al servicio de migración. No se puede añadir una dirección IP para ingestas porque es muy dinámica. Actualmente, la única solución es deshabilitar la lista de permitidos IP mientras se ejecuta la ingesta.
* Puede haber otras razones que requieren investigación. Si la ingesta sigue fallando, póngase en contacto con el Servicio de atención al cliente de Adobe.

### Actualizaciones automáticas a través de Release Orchestrator sigue activado

Release Orchestrator mantiene actualizados automáticamente los entornos mediante la aplicación automática de actualizaciones. Si la actualización se activa cuando se realiza una ingesta, puede causar resultados impredecibles, incluido el daño del entorno. Esa es una de las razones por las que se debe registrar un ticket de asistencia antes de iniciar una ingesta (consulte la &quot;Nota&quot; anterior), de modo que se pueda programar la desactivación temporal del Release Orchestrator.

Si Release Orchestrator sigue ejecutándose cuando se inicia una ingesta, la interfaz de usuario mostrará este mensaje. Puede optar por continuar de todos modos, aceptando el riesgo, marcando el campo y pulsando el botón de nuevo.

>[!NOTE]
>
> Release Orchestrator se está implementando en entornos de desarrollo, por lo que también se deben pausar las actualizaciones en esos entornos.

![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/error_releaseorchestrator_ingestion.png)

### Error de ingesta superior

Una causa común de una [Ingesta superior](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) el error es un conflicto en los id de nodo. Para identificar este error, descargue el registro de ingesta mediante la interfaz de usuario de Cloud Acceleration Manager y busque una entrada como la siguiente:

>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakConstraint0030: propiedad violada de la restricción de unicidad [jcr:uuid] con valor a1a1a1a1-b2b2-c3c3-d4d4-e5e5e5e5e5e5: /some/path/jcr:content, /some/other/path/jcr:content

AEM Cada nodo de la interfaz de usuario de debe tener un uuid único. Este error indica que un nodo que se está ingiriendo tiene el mismo uuid que uno que ya existe en una ruta diferente en la instancia de destino.
Esto puede suceder si un nodo se mueve en el origen entre una extracción y una [Extracción Superior](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process).
También puede suceder si un nodo en el destino se mueve entre una ingesta y una ingesta superior posterior.

Este conflicto debe resolverse manualmente. Alguien familiarizado con el contenido debe decidir cuál de los dos nodos se debe eliminar, teniendo en cuenta otro contenido que haga referencia a él. La solución puede requerir que la extracción superior se realice de nuevo sin el nodo infractor.

## Siguientes pasos {#whats-next}

Una vez que haya completado la ingesta de contenido en Target, puede ver los registros de cada paso (extracción e ingesta) y buscar errores. Consulte [Visualización de registros del conjunto de migraciones](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html) para obtener más información.
