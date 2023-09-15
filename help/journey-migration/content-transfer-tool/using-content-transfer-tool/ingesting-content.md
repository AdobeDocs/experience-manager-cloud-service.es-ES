---
title: Ingesta de contenido en Cloud Service
description: Aprenda a utilizar Cloud Acceleration Manager para introducir contenido del conjunto de migración en una instancia de Cloud Service de destino.
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: 5c482e5f883633c04d70252788b01f878156bac8
workflow-type: tm+mt
source-wordcount: '2142'
ht-degree: 6%

---

# Ingesta de contenido en Cloud Service {#ingesting-content}

## Proceso de ingesta en Cloud Acceleration Manager {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="Ingesta de contenido"
>abstract="La ingesta hace referencia a la ingesta de contenido del conjunto de migración en la instancia del Cloud Service de destino. La herramienta de transferencia de contenido tiene una función que permite agregar contenido diferencial donde solo es posible transferir los cambios realizados desde la actividad de transferencia de contenido anterior."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html#top-up-extraction-process" text="Extracción superior"

Siga los pasos a continuación para ingerir el conjunto de migración mediante Cloud Acceleration Manager:

>[!NOTE]
>¿Se acordó de registrar un ticket de asistencia para esta ingesta? Consulte [Consideraciones importantes antes de utilizar la herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html#important-considerations) por esa y otras consideraciones para ayudar a que la ingesta sea exitosa.

1. Vaya a Cloud Acceleration Manager. Haga clic en la tarjeta del proyecto y en la tarjeta Transferencia de contenido. Vaya a **Trabajos de ingesta** y haga clic en **Nueva ingesta**

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. Revise la lista de comprobación de ingesta y asegúrese de que se han completado todos los pasos. Estos pasos son necesarios para garantizar una ingesta correcta. Continúe con la **Siguiente** solo si se ha completado la lista de comprobación.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. Proporcione la información necesaria para crear una ingesta.

   * Seleccione el conjunto de migración que contiene los datos extraídos como origen.
      * Los conjuntos de migración caducarán después de un período de inactividad prolongado, por lo que se espera que la ingesta se produzca relativamente pronto después de realizar la extracción. Revisar [Caducidad del conjunto de migración](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) para obtener más información.
   * Seleccione el entorno de destino. En este entorno es donde se ingiere el contenido del conjunto de migración. Seleccione el nivel. (Autor/Publicación). Los entornos de desarrollo rápido no son compatibles.

   >[!NOTE]
   >Las siguientes notas se aplican a la ingesta de contenido:
   > Si el origen era Author, se recomienda ingerirlo en el nivel Author en el destino. Del mismo modo, si el origen era Publish, el destino también debería ser Publish.
   > Si el nivel de destino es `Author`, la instancia de autor se cierra durante la duración de la ingesta y no está disponible para los usuarios (por ejemplo, los autores o cualquier persona que realice mantenimiento). El motivo es proteger el sistema y evitar cualquier cambio que pueda perderse o causar un conflicto de ingesta. Asegúrese de que su equipo esté al tanto de este hecho. Tenga en cuenta también que el entorno parece hibernado durante la ingesta del autor.
   > Puede ejecutar el paso opcional previo a la copia para acelerar de forma significativa la ingesta. Consulte [Ingesta con AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) para obtener más información.
   > Si se utiliza la ingesta con copia previa (para S3 o Azure Data Store), se recomienda ejecutar primero la ingesta de autor solo. Al hacerlo, se acelera la ingesta de Publish cuando se ejecuta más adelante.
   > Las ingestas no admiten un destino de entorno de desarrollo rápido (RDE) y no aparecen como una posible opción de destino, aunque el usuario tenga acceso a él.

   >[!IMPORTANT]
   > Solo puede iniciar una ingesta en el entorno de destino si pertenece al entorno local de **AEM administradores de** en el servicio de creación del Cloud Service de destino. Si no puede iniciar una ingesta, consulte [No se puede iniciar la ingesta](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion) para obtener más información.

   * Elija la `Wipe` valor
      * El **Barrido** establece el punto de inicio del destino de la ingesta. If **Barrido** AEM Cuando está activada, el destino, incluido todo su contenido, se restablece a la versión de la especificada en Cloud Manager. Si no está habilitado, el destino mantiene su contenido actual como punto de partida.
      * Tenga en cuenta que esta opción sí **NO** afectar a cómo se realizará la ingesta de contenido. La ingesta siempre utiliza una estrategia de sustitución de contenido y _no_ una estrategia de combinación de contenido para que, en ambos **Barrido** y **Sin barrido** En algunos casos, la ingesta de un conjunto de migración sobrescribirá el contenido en la misma ruta en el destino. Por ejemplo, si el conjunto de migración contiene `/content/page1` y el destino ya contiene `/content/page1/product1`, la ingesta eliminará todo el `page1` ruta y sus subpáginas, incluidas `product1`y reemplácelo por el contenido del conjunto de migración. Esto significa que se debe realizar una planificación cuidadosa al realizar una **Sin barrido** la ingesta a un destino que incluya cualquier contenido que se deba mantener.

   >[!IMPORTANT]
   > Si la configuración **Barrido** está habilitado para la ingesta, restablece todo el repositorio existente, incluidos los permisos de usuario en la instancia de Cloud Service de destino. Este restablecimiento también es verdadero para un usuario administrador agregado a **administradores** y ese usuario deben volver a agregarse al grupo de administradores para iniciar una ingesta.

1. Clic **Ingesta**.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. A continuación, puede monitorizar la ingesta desde la vista de lista de Trabajos de ingesta y utilizar el menú de acciones de la ingesta para ver las duraciones y registrar como progresa la ingesta.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. Haga clic en **(i)** en la fila para obtener más información sobre el trabajo de ingesta. Puede ver la duración de cada paso de la ingesta cuando se está ejecutando o completando haciendo clic en **...** y, a continuación, haga clic en **Ver duraciones**. La información de la extracción también muestra que se da cuenta de lo que se está ingiriendo.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23b.png)

## Ingesta superior {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup"
>title="Ingesta superior"
>abstract="Utilice la función superior para mover el contenido modificado desde la actividad de transferencia de contenido anterior. Una vez finalizada la ingesta, compruebe si hay errores/advertencias en los registros. Los errores deben solucionarse inmediatamente, ya sea abordando los problemas notificados o poniéndose en contacto con el Servicio de atención al cliente de Adobe."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html?lang=es" text="Visualización de registros"

La herramienta de transferencia de contenido tiene una función que permite extraer contenido diferencial realizando una *recargar* del conjunto de migración. Esto permite modificar el conjunto de migración para incluir únicamente el contenido que ha cambiado desde la extracción anterior sin tener que extraer todo el contenido de nuevo.

>[!NOTE]
>Después de la transferencia de contenido inicial, se recomienda realizar frecuentes recargas de contenido diferencial para acortar el período de congelación de contenido para la transferencia de contenido diferencial final antes de lanzarse a Cloud Service. Si ha utilizado el paso de precopia para la primera ingesta, puede omitir la precopia para las ingestas de recarga posteriores (si el tamaño del conjunto de migración de recarga es inferior a 200 GB). El motivo es que puede añadir tiempo a todo el proceso.

Para introducir contenido diferencial una vez completadas algunas ingestas, debe ejecutar un [Extracción Superior](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)y, a continuación, utilice el método de ingesta con **Barrido** opción **inhabilitado**. Asegúrese de leer el **Barrido** Esta explicación anterior para evitar perder contenido que ya se encuentra en el destino.

Comience creando un trabajo de ingesta y asegúrese de que **Barrido** se desactiva durante la ingesta, como se muestra a continuación:

![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## Solución de problemas {#troubleshooting}

### CAM no puede recuperar el token de migración {#cam-unable-to-retrieve-the-migration-token}

La recuperación automática del token de migración puede fallar por diferentes motivos, entre los que se incluye [configuración de una lista de permitidos IP mediante Cloud Manager](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) en el entorno del Cloud Service de destino. En estos casos, verá el siguiente cuadro de diálogo cuando intente iniciar una ingesta:

![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/troubleshooting-token.png)

Recupere el token de migración manualmente haciendo clic en el vínculo &quot;Obtener token&quot; en el cuadro de diálogo. Se abre otra pestaña que muestra el token. A continuación, puede copiar el token y pegarlo en **Entrada de token de migración** field. Ahora, debería poder iniciar la ingesta.

>[!NOTE]
>
>El token está disponible para los usuarios que pertenecen al **AEM administradores de** en el servicio de creación del Cloud Service de destino.

### No se puede iniciar la ingesta {#unable-to-start-ingestion}

Solo puede iniciar una ingesta en el entorno de destino si pertenece al entorno local de **AEM administradores de** en el servicio de creación del Cloud Service de destino. AEM Si no pertenece al grupo de administradores de la, verá un error como se muestra a continuación cuando intente iniciar una ingesta. Puede pedir al administrador que le añada al local **AEM administradores de** o pida el token en sí, que puede pegar en el **Entrada de token de migración** field.

![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/error_nonadmin_ingestion.png)

### No se puede conectar con el servicio de migración {#unable-to-reach-migration-service}

Después de solicitar una ingesta, se puede presentar al usuario un mensaje como el siguiente: &quot;El servicio de migración en el entorno de destino es inaccesible. Si es así, vuelva a intentarlo más tarde o póngase en contacto con el soporte de Adobe&quot;.

![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/error_cannot_reach_migser.png)

Este mensaje indica que Cloud Acceleration Manager no pudo llegar al servicio de migración del entorno de destino para iniciar la ingesta. Esta situación puede ocurrir por varias razones.

>[!NOTE]
> 
> El campo &quot;Token de migración&quot; se muestra porque, en algunos casos, la recuperación de ese token es lo que realmente no está permitido. Al permitir que se proporcione manualmente, puede permitir al usuario iniciar la ingesta rápidamente, sin ninguna ayuda adicional. Si se proporciona el token y sigue apareciendo el mensaje, el problema no consistió en recuperar el token.

* AEM El as a Cloud Service mantiene el estado del entorno y, ocasionalmente, debe reiniciar el servicio de migración por varios motivos normales. Si ese servicio se está reiniciando, no se podrá acceder a él, pero estará disponible en algún momento.
* Es posible que se esté ejecutando otro proceso en la instancia. Por ejemplo, si Release Orchestrator aplica una actualización, el sistema puede estar ocupado y el servicio de migración no está disponible con regularidad. Por este motivo, y la posibilidad de corromper la instancia de fase o producción, es muy recomendable pausar las actualizaciones durante una ingesta.
* Si un [Se ha aplicado la Lista de permitidos IP](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) a través de Cloud Manager, impide que Cloud Acceleration Manager llegue al servicio de migración. No se puede añadir una dirección IP para ingestas porque es dinámica. Actualmente, la única solución es deshabilitar la lista de permitidos IP mientras se ejecuta la ingesta.
* Puede haber otras razones que requieren investigación. Si la ingesta sigue fallando, póngase en contacto con el Servicio de atención al cliente de Adobe.

### Actualizaciones automáticas a través de Release Orchestrator sigue activado

Release Orchestrator mantiene actualizados automáticamente los entornos mediante la aplicación automática de actualizaciones. Si la actualización se activa cuando se realiza una ingesta, puede causar resultados impredecibles, incluido el daño del entorno. Una buena razón para registrar un ticket de asistencia al cliente antes de iniciar una ingesta (consulte la &quot;Nota&quot; anterior), de modo que se pueda programar la desactivación temporal del Release Orchestrator.

Si Release Orchestrator sigue ejecutándose cuando se inicia una ingesta, la interfaz de usuario presenta este mensaje. Puede optar por continuar de todos modos, aceptando el riesgo, marcando el campo y pulsando el botón de nuevo.

>[!NOTE]
>
> Release Orchestrator se está implementando en entornos de desarrollo, por lo que también se deben pausar las actualizaciones en esos entornos.

![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/error_releaseorchestrator_ingestion.png)

### Error de ingesta superior debido a una infracción de la restricción de unicidad

Una causa común de una [Ingesta superior](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) el error es un conflicto en los id de nodo. Para identificar este error, descargue el registro de ingesta mediante la interfaz de usuario de Cloud Acceleration Manager y busque una entrada como la siguiente:

>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakConstraint0030: propiedad violada de la restricción de unicidad [jcr:uuid] con valor a1a1a1a1-b2b2-c3c3-d4d4-e5e5e5e5e5e5: /some/path/jcr:content, /some/other/path/jcr:content

AEM Cada nodo de la interfaz de usuario de debe tener un uuid único. Este error indica que un nodo que se está ingiriendo tiene el mismo uuid que uno que existe en otra parte en una ruta diferente en la instancia de destino.
Esta situación puede suceder si se mueve un nodo en el origen entre una extracción y una [Extracción Superior](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process).
También puede suceder si un nodo en el destino se mueve entre una ingesta y una ingesta superior subsiguiente.

Este conflicto debe resolverse manualmente. Alguien familiarizado con el contenido debe decidir cuál de los dos nodos se debe eliminar, teniendo en cuenta otro contenido que haga referencia a él. La solución puede requerir que la extracción superior se realice de nuevo sin el nodo infractor.

### Error de ingesta superior debido a que no se puede eliminar el nodo al que se hace referencia

Otra causa común de una [Ingesta superior](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) el error es un conflicto de versiones para un nodo en particular en la instancia de destino. Para identificar este error, descargue el registro de ingesta mediante la interfaz de usuario de Cloud Acceleration Manager y busque una entrada como la siguiente:
>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakIntegrity0001: No se puede eliminar el nodo al que se hace referencia: 8a2289f4-b904-4bd0-8410-15e41e0976a8

Esto puede suceder si se modifica un nodo en el destino entre una ingesta y una **Sin barrido** ingesta de tal manera que se ha creado una nueva versión. Si el conjunto de migración se ha extraído con la opción &quot;incluir versiones&quot; habilitada, puede producirse un conflicto, ya que el destino tiene ahora una versión más reciente a la que hacen referencia el historial de versiones y otro contenido. El proceso de ingesta no podrá eliminar el nodo de versión infractor porque se hace referencia a él.

La solución puede requerir que la extracción superior se realice de nuevo sin el nodo infractor. O bien, creando un pequeño conjunto de migración del nodo infractor, pero con la opción &quot;incluir versiones&quot; deshabilitada.

Las prácticas recomendadas indican que si **Sin barrido** La ingesta debe ejecutarse con un conjunto de migración que incluya versiones (es decir, extraídas con &quot;incluir versiones&quot; = true), es crucial que el contenido del destino se modifique lo menos posible, hasta que se complete el recorrido de migración. De lo contrario, pueden producirse estos conflictos.


## Siguientes pasos {#whats-next}

AEM Cuando la ingesta se haya realizado correctamente, la indexación de la se iniciará automáticamente. Consulte [Indexación después de migrar contenido](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/indexing-content.md) para obtener más información.

Una vez que haya completado la ingesta de contenido en Cloud Service, puede ver los registros de cada paso (extracción e ingesta) y buscar errores. Consulte [Visualización de registros del conjunto de migraciones](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/viewing-logs.md) para obtener más información.
