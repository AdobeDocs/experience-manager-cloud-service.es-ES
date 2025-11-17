---
title: Ingesta de contenido en Cloud Service
description: Aprenda a utilizar Cloud Acceleration Manager para introducir contenido del conjunto de migración en una instancia de Cloud Service de destino.
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
feature: Migration
role: Admin
source-git-commit: 7c0703d746601742a28c3c98f35e69de70f25e05
workflow-type: tm+mt
source-wordcount: '3647'
ht-degree: 12%

---

# Ingesta de contenido en Cloud Service {#ingesting-content}

## Proceso de ingesta en Cloud Acceleration Manager {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="Ingesta de contenido"
>abstract="Hace referencia a la ingesta de contenido del conjunto de migración en la instancia de Cloud Service de destino. La herramienta de transferencia de contenido tiene una función que permite agregar contenido diferencial donde solo es posible transferir los cambios realizados desde la actividad de transferencia de contenido anterior."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content#top-up-extraction-process" text="Extracción superior"

Siga los pasos a continuación para ingerir el conjunto de migración mediante Cloud Acceleration Manager:

1. Vaya a Cloud Acceleration Manager. Haga clic en la tarjeta del proyecto y en la tarjeta Transferencia de contenido. Vaya a **Trabajos de ingesta** y haga clic en **Nueva ingesta**

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. Revise la lista de comprobación de ingesta y asegúrese de que se han completado todos los pasos. Estos pasos son necesarios para garantizar una ingesta correcta. Continúe con el paso **Siguiente** solo si la lista de comprobación se ha completado.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. Proporcione la información necesaria para crear una ingesta.

   * **Conjunto de migración:** Seleccione el conjunto de migración que contiene los datos extraídos como Source.
      * Los conjuntos de migración caducarán después de un período de inactividad prolongado, por lo que se espera que la ingesta se produzca relativamente pronto después de realizar la extracción. Revise [Expiración del conjunto de migración](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) para obtener detalles.

   >[!TIP]
   > Si la extracción se está ejecutando, el cuadro de diálogo lo indicará. Una vez que la extracción ha finalizado correctamente, la ingesta se inicia automáticamente. Si la extracción falla o se detiene, el trabajo de ingesta se rescindirá.

   * **Destino:** Seleccione el entorno de destino. En este entorno es donde se ingiere el contenido del conjunto de migración.
      * Las ingestas no admiten destinos de tipo Entorno de desarrollo rápido (RDE) o Vista previa, y no aparecen como una posible opción de destino, aunque el usuario tenga acceso a ellos.
      * Aunque un conjunto de migración se puede ingerir en varios destinos simultáneamente, un destino solo puede ser el destino de una ingesta en ejecución o en espera a la vez.

   * **Nivel:** Seleccione el nivel. (Autor/Publicación).
      * Si el origen era `Author`, se recomienda ingerirlo en el nivel `Author` en el destino. Del mismo modo, si el origen era `Publish`, el destino debería ser `Publish` también.

   >[!NOTE]
   > Si el nivel de destino es `Author`, la instancia de autor se cierra durante toda la ingesta y no está disponible para los usuarios (por ejemplo, los autores o cualquier persona que realice tareas de mantenimiento). El motivo es proteger el sistema y evitar cualquier cambio que pueda perderse o causar un conflicto de ingesta. Asegúrese de que su equipo esté al tanto de este hecho. Tenga en cuenta también que el entorno parece hibernado durante la ingesta del autor.

   >[!NOTE]
   > Si el nivel de destino es `Publish`, la instancia de publicación permanece en ejecución durante la ingesta.  Sin embargo, si el proceso de compactación se está ejecutando mientras se produce la ingesta, es probable que se produzca un conflicto entre los dos procesos.  Por este motivo, el proceso de ingesta 1) desactiva el script temporizado de compactación, de modo que la compactación no se inicia durante la ingesta, y 2) comprueba si la compactación se está ejecutando actualmente y, si lo está, espera a que se complete antes de que la ingesta continúe.  Si la ingesta de publicación está tardando más de lo esperado, compruebe los registros de ingesta para ver si hay instrucciones de registro relacionadas.

   * **Borrar:** Elija el valor `Wipe`
      * La opción **Borrar** establece el punto de inicio de la ingesta en el destino. Si **Borrar** está habilitado, el destino, incluido todo su contenido, se restablecerá a la versión de AEM especificada en Cloud Manager. Si no está habilitado, el destino mantiene su contenido actual como punto de partida.
      * Esta opción **NOT** afecta a la forma en que se realizará la ingesta de contenido. La ingesta siempre usa una estrategia de reemplazo de contenido y _no_ una estrategia de combinación de contenido, por lo que, en los casos de **borrado** y **sin borrado**, la ingesta de un conjunto de migración sobrescribirá el contenido en la misma ruta de acceso del destino. Por ejemplo, si el conjunto de migración contiene `/content/page1` y el destino ya contiene `/content/page1/product1`, la ingesta elimina toda la ruta de acceso de `page1` y sus subpáginas, incluida `product1`, y la reemplaza por el contenido del conjunto de migración. Esto significa que se debe realizar una planificación cuidadosa al realizar una ingesta de **Sin borrado** en un destino que contenga cualquier contenido que se deba mantener.
      * Las ingestas sin borrado están diseñadas específicamente para el caso de uso de ingesta superior. Estas ingestas están pensadas para tener una cantidad incremental de contenido nuevo que ha cambiado desde la última ingesta en un conjunto de migración existente. La realización de ingestas sin borrado fuera de este caso de uso podría provocar tiempos de ingesta muy largos.

   >[!IMPORTANT]
   > Si el ajuste **Borrar** está habilitado para la ingesta, restablecerá todo el repositorio existente, incluidos los permisos de usuario en la instancia de Cloud Service de destino. Este restablecimiento también se aplica a un usuario administrador agregado al grupo de **administradores** y ese usuario debe agregarse de nuevo al grupo de administradores para iniciar una ingesta.

   * **Copia previa:** Elija el valor `Pre-copy`
      * Puede ejecutar el paso opcional previo a la copia para acelerar de forma significativa la ingesta. Consulte [Ingesta con AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) para obtener más información.
      * Si se utiliza la ingesta con copia previa (para S3 o Azure Data Store), se recomienda ejecutar la ingesta de `Author` primero solo. Al hacerlo, se acelera la ingesta de `Publish` cuando se ejecuta más adelante.

   >[!IMPORTANT]
   > Solo puede iniciar una ingesta en el entorno de destino si pertenece al grupo local **administradores de AEM** en el servicio de Cloud Service Author de destino. Si no puede iniciar una ingesta, consulte [No se puede iniciar la ingesta](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion) para obtener más detalles.

1. Una vez seleccionadas las opciones de ingesta, se puede mostrar una estimación de su duración. Se trata de una estimación del esfuerzo máximo basada en datos históricos de ingestas similares.

   * Esta estimación no se calcula ni se muestra para **ingestas sin borrado**, ya que CAM no sabe cuánto contenido hay en el sistema de destino en este caso.
   * Esta estimación solo se calcula y se muestra si los valores &quot;Comprobar tamaño&quot; de la extracción se recopilaron y están disponibles.
   * Este valor es una estimación y, aunque se calcula de forma inteligente, no debe considerarse exacto. Varios factores pueden cambiar la duración real.
   * Mientras se ejecuta la ingesta, este valor también estará disponible en el cuadro de diálogo de duraciones, al que se accede mediante la acción &quot;**Ver duraciones**&quot; de la ingesta.

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_estimate"
>title="Estimación de la duración de una ingesta"
>abstract="Se puede mostrar una duración aproximada de una ingesta determinada para proporcionar una idea general de cuánto tiempo tardará. Existen limitaciones a su precisión."

![imagen](/help/journey-migration/content-transfer-tool/assets/estimate.png)

1. Haga clic en **Ingesta**.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. A continuación, puede monitorizar la ingesta desde la vista de lista de Trabajos de ingesta y utilizar el menú de acciones de la ingesta para ver las duraciones y registrar como progresa la ingesta.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. Haga clic en el botón **(i)** de la fila para obtener más información sobre el trabajo de ingesta. Puede ver la duración de cada paso de la ingesta cuando se está ejecutando o se ha completado haciendo clic en **...** y, a continuación, haciendo clic en **Ver duraciones**. La información de la extracción también muestra que se da cuenta de lo que se está ingiriendo.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23b.png)

## Ingesta superior {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup"
>title="Ingesta superior"
>abstract="Utilice la función superior para mover el contenido modificado desde la actividad de transferencia de contenido anterior. Una vez finalizada la ingesta, compruebe los registros para ver si hay errores o advertencias. Los errores deben solucionarse inmediatamente, ya sea abordando los problemas notificados o poniéndose en contacto con el Servicio de atención al cliente de Adobe."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs" text="Visualización de registros"

La herramienta de transferencia de contenido tiene una característica que permite extraer contenido diferencial realizando una *recarga* del conjunto de migración. Esto permite modificar el conjunto de migración para incluir únicamente el contenido que ha cambiado desde la extracción anterior sin tener que extraer todo el contenido de nuevo.

>[!NOTE]
>Después de la transferencia de contenido inicial, se recomienda realizar frecuentes recargas de contenido diferencial para acortar el período de congelación de contenido para la transferencia de contenido diferencial final antes de lanzarse a Cloud Service. Si ha utilizado el paso de precopia para la primera ingesta, puede omitir la precopia para las ingestas de recarga posteriores (si el tamaño del conjunto de migración de recarga es inferior a 200 GB). El motivo es que puede añadir tiempo a todo el proceso.

Para ingerir contenido diferencial una vez que se hayan completado algunas ingestas, debe ejecutar una [Extracción superior](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process) y luego usar el método de ingesta con la opción **Borrar** **deshabilitada**. No olvide leer la explicación **Borrar** anterior para evitar perder contenido que ya se encuentra en el destino.

Comience creando un trabajo de ingesta y asegúrese de que **Borrar** esté deshabilitado durante la ingesta, como se muestra a continuación:

![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## Resolución de problemas {#troubleshooting}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_troubleshooting"
>title="Resolución de problemas de ingesta de contenidos"
>abstract="Consulte los registros de la ingesta y la documentación para encontrar soluciones a los motivos habituales por los que puede fallar una ingesta y encuentre la forma de solucionar el problema. Una vez corregida, la ingesta se puede ejecutar de nuevo."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers" text="Validación de transferencias de contenido"

### CAM no puede recuperar el token de migración {#cam-unable-to-retrieve-the-migration-token}

La recuperación automática del token de migración puede fallar por diferentes motivos, entre ellos [configurar una lista de permitidos IP a través de Cloud Manager](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) en el entorno de Cloud Service de destino. En estos casos, verá el siguiente cuadro de diálogo cuando intente iniciar una ingesta:

![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/troubleshooting-token.png)

Recupere el token de migración manualmente haciendo clic en el vínculo &quot;Obtener token&quot; en el cuadro de diálogo. Se abre otra pestaña que muestra el token. A continuación, puede copiar el token y pegarlo en el campo **Entrada de token de migración**. Ahora, debería poder iniciar la ingesta.

>[!NOTE]
>
>El token está disponible para los usuarios que pertenecen al grupo local **administradores de AEM** en el servicio de Cloud Service Author de destino.

### No se puede iniciar la ingesta {#unable-to-start-ingestion}

Solo puede iniciar una ingesta en el entorno de destino si pertenece al grupo local **administradores de AEM** en el servicio de Cloud Service Author de destino. Si no pertenece al grupo de administradores de AEM, verá un error como se muestra a continuación cuando intente iniciar una ingesta. Puede pedirle al administrador que le añada a los **administradores locales de AEM** o que le pida el token en sí, que puede pegar en el campo **Entrada del token de migración**.

![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/error_nonadmin_ingestion.png)

### No se puede conectar con el servicio de migración {#unable-to-reach-migration-service}

Después de solicitar una ingesta, se puede presentar al usuario un mensaje como el siguiente: &quot;El servicio de migración en el entorno de destino es inaccesible. Si es así, vuelva a intentarlo más tarde o póngase en contacto con el soporte de Adobe&quot;.

![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/error_cannot_reach_migser.png)

Este mensaje indica que Cloud Acceleration Manager no pudo contactar con el servicio de migración del entorno de destino para iniciar la ingesta. Esta situación puede ocurrir por varias razones.

>[!NOTE]
> 
> El campo &quot;Token de migración&quot; se muestra porque, en algunos casos, la recuperación de ese token es lo que realmente no está permitido. Al permitir que se proporcione manualmente, puede permitir al usuario iniciar la ingesta rápidamente, sin ninguna ayuda adicional. Si se proporciona el token y sigue apareciendo el mensaje, el problema no consistió en recuperar el token.

* AEM as a Cloud Service mantiene el estado del entorno y, ocasionalmente, debe reiniciar el servicio de migración por varios motivos normales. Si ese servicio se está reiniciando, no se podrá acceder a él, pero estará disponible en algún momento.
* Es posible que se esté ejecutando otro proceso en la instancia. Por ejemplo, si [Actualizaciones de la versión de AEM](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates) está aplicando una actualización, es posible que el sistema esté ocupado y que el servicio de migración no esté disponible con regularidad. Una vez completado ese proceso, se puede volver a intentar iniciar la ingesta.
* Si se ha aplicado una Lista de permitidos de [IP](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) a través de Cloud Manager, se bloquea el acceso de Cloud Acceleration Manager al servicio de migración. No se puede añadir una dirección IP para ingestas porque es dinámica. Actualmente, la única solución es deshabilitar la lista de permitidos IP durante el proceso de ingesta e indexación agregando temporalmente 0.0.0.0/0 a la lista de permitidos mientras se ejecuta el proceso de ingesta e indexación.
* Puede haber otras razones que requieren investigación. Si la ingesta o la indexación siguen fallando, póngase en contacto con el Servicio de atención al cliente de Adobe.

### Actualizaciones e ingestas de versiones de AEM {#aem-version-updates-and-ingestions}

[Las actualizaciones de la versión de AEM](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates) se aplican automáticamente a los entornos para mantenerlos actualizados con la última versión de AEM as a Cloud Service. Si la actualización se activa cuando se realiza una ingesta, puede causar resultados impredecibles, incluido el daño del entorno.

Si &quot;Actualizaciones de la versión de AEM&quot; está incorporado en el programa de destino, el proceso de ingesta intenta desactivar su cola antes de iniciarse. Cuando se completa la ingesta, el estado del actualizador de versiones se devuelve a como estaba antes de que se iniciaran las ingestas.

>[!NOTE]
>
> Ya no es necesario registrar un ticket de asistencia para desactivar &quot;Actualizaciones de versión de AEM&quot;.

Si &quot;Actualizaciones de versión de AEM&quot; está activo (es decir, las actualizaciones se están ejecutando o están en cola para ejecutarse), la ingesta no comenzará y la interfaz de usuario mostrará el siguiente mensaje. Una vez completadas las actualizaciones, se puede iniciar la ingesta. Cloud Manager se puede utilizar para ver el estado actual de las canalizaciones del programa.

>[!NOTE]
>
> &quot;Actualizaciones de versión de AEM&quot; se ejecuta en el canal del entorno y espera hasta que el canal esté libre. Si las actualizaciones se ponen en cola durante más tiempo del esperado, asegúrese de que un flujo de trabajo personalizado no tenga la canalización bloqueada de forma involuntaria.

![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/error_releaseorchestrator_active.png)

### Error de ingesta debido a que el entorno de nube no está listo {#ingestion-failure-due-to-cloud-environment-not-in-ready-state}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_cloud_environment_not_in_ready_state"
>title="El entorno de nube no está listo"
>abstract="En casos excepcionales, el entorno de la nube de destino podría estar experimentando problemas inesperados, lo que hará que la ingesta falle."

En casos excepcionales, el entorno de Cloud Service de destino de la ingesta puede estar experimentando problemas inesperados. Como resultado, la ingesta fallará ya que el entorno no está en el estado de preparado esperado. Consulte el registro de ingesta para mostrar más detalles del estado de error encontrado.

Asegúrese de que el entorno de creación esté disponible y espere unos minutos antes de volver a intentar la ingesta. Si el problema persiste, póngase en contacto con el servicio de atención al cliente con el estado de error encontrado.

### Error de ingesta de recarga debido a una infracción de la restricción de unicidad {#top-up-ingestion-failure-due-to-uniqueness-constraint-violation}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_uuid"
>title="Infracción de restricción de unicidad"
>abstract="Una causa común de un error de ingesta que no es de borrado es un conflicto en los identificadores de nodo. Solo puede existir uno de los nodos en conflicto."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content#top-up-ingestion-process" text="Ingesta de recarga"

Una causa común de un error de [ingesta superior](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) es un conflicto en los identificadores de nodo. Para identificar este error, descargue el registro de ingesta mediante la interfaz de usuario de Cloud Acceleration Manager y busque una entrada como la siguiente:

>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakConstraint0030: La restricción de unicidad violó la propiedad [jcr:uuid] con valor a1a1a1a1-b2b2-c3c3-d4d4-e5e5e5e5e5e5: /some/path/jcr:content, /some/other/path/jcr:content

Cada nodo de AEM debe tener un uuid único. Este error indica que un nodo que se está ingiriendo tiene el mismo uuid que uno que existe en una ruta diferente en la instancia de destino. Esta situación puede ocurrir por dos razones:

* Un nodo se mueve en el origen entre una extracción y una [extracción superior](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process) posterior
   * _RECORDAR_: Para las extracciones de nivel superior, el nodo seguirá existiendo en el conjunto de migración, aunque ya no exista en el origen.
* Un nodo en el destino se mueve entre una ingesta y una ingesta superior subsiguiente.

Este conflicto debe resolverse manualmente. Alguien familiarizado con el contenido debe decidir cuál de los dos nodos se debe eliminar, teniendo en cuenta otro contenido que haga referencia a él. La solución puede requerir que la extracción superior se realice de nuevo sin el nodo infractor.

### Error de ingesta de recarga debido a que no se puede eliminar el nodo al que se hace referencia {#top-up-ingestion-failure-due-to-unable-to-delete-referenced-node}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_referenced_node"
>title="No se puede eliminar el nodo de referencia"
>abstract="Una causa común de un error de ingesta sin borrado es un conflicto de versiones para un nodo en particular en la instancia de destino. Se deben corregir las versiones del nodo."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content#top-up-ingestion-process" text="Ingesta de recarga"

Otra causa común de un error de [Ingesta superior](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) es un conflicto de versión para un nodo en particular en la instancia de destino. Para identificar este error, descargue el registro de ingesta mediante la interfaz de usuario de Cloud Acceleration Manager y busque una entrada como la siguiente:

>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakIntegrity0001: No se puede eliminar el nodo al que se hace referencia: 8a2289f4-b904-4bd0-8410-15e41e0976a8

Esto puede ocurrir si se modifica un nodo en el destino entre una ingesta y una ingesta posterior de **Sin borrado** de tal manera que se ha creado una nueva versión. Si el conjunto de migración se ha extraído con la opción &quot;incluir versiones&quot; habilitada, puede producirse un conflicto, ya que el destino tiene ahora una versión más reciente a la que hacen referencia el historial de versiones y otro contenido. El proceso de ingesta no puede eliminar el nodo de versión infractor porque se hace referencia a él.

La solución puede requerir que la extracción superior se realice de nuevo sin el nodo infractor. O bien, creando un pequeño conjunto de migración del nodo infractor, pero con la opción &quot;incluir versiones&quot; deshabilitada.

Las prácticas recomendadas indican que si se debe ejecutar una ingesta de **Non-Wipe** mediante un conjunto de migración que incluya versiones, es crucial que el contenido del destino se modifique lo menos posible, hasta que se complete el recorrido de migración. De lo contrario, pueden producirse estos conflictos.

### Error de ingesta debido a valores de propiedad de nodos grandes {#ingestion-failure-due-to-large-node-property-values}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_bson"
>title="Propiedad de nodo grande"
>abstract="Una causa común de un error de ingesta es el exceso del tamaño máximo de los valores de propiedad del nodo. Consulte la documentación, incluida la relacionada con el informe de BPA, para solucionar esta situación."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool" text="Requisitos previos de migración"

Los valores de propiedad del nodo almacenados en MongoDB no pueden superar los 16 MB. Si el valor de un nodo supera el tamaño admitido, la ingesta falla y el registro contiene lo siguiente:

* un error `BSONObjectTooLarge` y especifique qué nodo superó el máximo, o
* error `BsonMaximumSizeExceededException`, que indica que es probable que haya un nodo que contenga caracteres unicode que exceda el tamaño máximo **

Esta es una restricción de MongoDB.

Consulte la nota `Node property value in MongoDB` en [Requisitos previos para la herramienta de transferencia de contenido](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/prerequisites-content-transfer-tool.md) para obtener más información y un vínculo a una herramienta de Oak que pueda ayudar a encontrar todos los nodos grandes. Una vez corregidos todos los nodos con tamaños grandes, ejecute de nuevo la extracción y la ingesta.

Para evitar posiblemente esta restricción, ejecute el [Analizador de prácticas recomendadas](/help/journey-migration/best-practices-analyzer/using-best-practices-analyzer.md) en la instancia de AEM de origen y revise los resultados que presenta, en particular el patrón [&quot;Estructura de repositorio no admitida&quot; (URS)](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/urs).

>[!NOTE]
>
>[Analizador de prácticas recomendadas](/help/journey-migration/best-practices-analyzer/using-best-practices-analyzer.md) versión 2.1.50+ informará sobre nodos grandes que contengan caracteres Unicode que superen el tamaño máximo. Asegúrese de que está ejecutando la versión más reciente. Las versiones de BPA anteriores a la 2.1.50 no identificarán estos nodos grandes ni generarán informes al respecto, por lo que deberán descubrirse por separado mediante la herramienta de Oak de requisitos previos mencionada anteriormente.

### Error de ingesta debido a errores intermitentes inesperados {#ingestion-failure-due-to-unexpected-intermittent-errors}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_intermittent_errors"
>title="Errores intermitentes inesperados"
>abstract="A veces, pueden producirse errores intermitentes inesperados en el servicio descendente y, por desgracia, el único recurso es, simplemente, volver a intentar la ingesta."

A veces, problemas intermitentes inesperados podrían prestarse a ingestas fallidas donde, por desgracia, el único recurso es reintentar la ingesta. Investigue el registro de ingesta para descubrir la causa del error y ver si se ajusta a alguno de los errores enumerados a continuación, donde se debe intentar un reintento.

#### Problemas de MongoDB {#mongo-db-issues}

* `Atlas prescale timeout error`: en la fase de ingesta se intentará escalar previamente la base de datos de la nube de Target a un tamaño adecuado que se ajuste al tamaño del contenido del conjunto de migración que se está ingiriendo. De forma poco frecuente, esta operación no se completa dentro del intervalo de tiempo esperado.
* `Exhausted mongo restore retries`: se agotaron los intentos de restaurar un volcado local del contenido del conjunto de migración ingerido en la base de datos de la nube. Esto indica un problema general de salud/red con MongoDB, que a menudo se cura solo después de unos minutos.
* `Mongo network error`: a veces, el establecimiento de una conexión con MongoDB puede fallar, lo que provoca que el proceso de ingesta se cierre antes y notifique como fallido. Se debe intentar un simple reintento de la ingesta.
* `Mongo server selection error`: se trata de un error de tiempo de espera inusual del lado del cliente que puede producirse por varias razones subyacentes. Un reintento posterior probablemente corregirá el problema.
* `Mongo took too long to start`: en casos extremadamente excepcionales, el MongoDB local utilizado en el flujo de trabajo de ingesta puede no iniciarse. Un reintento posterior probablemente corregirá el problema.

#### Problemas de AZCopy {#azcopy-issues}

* `AZCopy critical failure`: en casos excepcionales, la herramienta AZCopy utilizada para realizar el paso previo a la copia de la ingesta puede fallar inesperadamente. En este caso, se debe intentar reintentar la ingesta.

### Ingesta rescindida {#ingestion-rescinded}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_rescinded"
>title="Ingesta rescindida"
>abstract="La extracción que la ingesta estaba esperando no finalizó correctamente. La ingesta se ha rescindido porque no se ha podido ejecutar."

Una ingesta creada con una extracción en ejecución como el conjunto de migración de origen espera pacientemente hasta que la extracción se realice correctamente y, en ese momento, comienza con normalidad. Si la extracción falla o se detiene, la ingesta y su trabajo de indexación no comenzarán, pero se rescindirán. En este caso, compruebe la extracción para determinar por qué ha fallado, corrija el problema y vuelva a empezar a extraer. Una vez que se esté ejecutando la extracción fija, se puede programar una nueva ingesta.

### No se pudo iniciar la ingesta en espera {#waiting-ingestion-not-started}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_waiting_ingestion_not_started"
>title="Ingesta en espera no iniciada"
>abstract="La ingesta no se ha podido iniciar después de esperar a que se completara una extracción."

Una ingesta que se ha creado con una extracción en ejecución como el conjunto de migración de origen espera hasta que dicha extracción se realice correctamente y, en ese momento, la ingesta intenta iniciarse de forma normal. Si la ingesta no se inicia, se marca como fallida. Las posibles razones para no iniciarlo son las siguientes: hay una Lista de permitidos IP configurada en el entorno de creación de Target y el entorno de destino no está disponible por otro motivo.  En este caso, compruebe por qué no se pudo iniciar la ingesta, corrija el problema e inicie la ingesta de nuevo (no es necesario volver a ejecutar la extracción).

### El recurso eliminado no está presente después de volver a ejecutar la ingesta

En general, no se recomienda modificar los datos del entorno de la nube entre ingestas.

Cuando se elimina un recurso del destino de Cloud Service mediante la IU táctil de Assets, los datos del nodo se eliminan, pero el blob de recursos con la imagen no se elimina inmediatamente. Se marca para su eliminación de modo que ya no aparezca en la interfaz de usuario; sin embargo, permanece en el almacén de datos hasta que se produce la recolección de elementos no utilizados y se elimina el blob.

En el escenario en el que se elimina un recurso migrado anteriormente y la siguiente ingesta se ejecuta antes de que el recolector de elementos no utilizados haya terminado de eliminar el recurso, la ingesta del mismo conjunto de migración no restaurará el recurso eliminado. Cuando la ingesta comprueba el entorno de nube del recurso, no hay datos del nodo; por lo tanto, la ingesta copiará los datos del nodo en el entorno de nube. Sin embargo, cuando comprueba el almacén de blobs, ve que el blob está presente y omite la copia del blob. Por este motivo, los metadatos están presentes después de la ingesta cuando se mira el recurso desde la interfaz de usuario táctil, pero la imagen no. Recuerde que los conjuntos de migración y la ingesta de contenido no se diseñaron para manejar este caso. Su objetivo es añadir contenido nuevo al entorno de la nube y no restaurar el contenido migrado anteriormente.

## Siguientes pasos {#whats-next}

Cuando la ingesta se haya realizado correctamente, la indexación de AEM se iniciará automáticamente. Consulte [Indexación después de migrar contenido](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/indexing-content.md) para obtener más información.

Una vez que haya completado la ingesta de contenido en Cloud Service, puede ver los registros de cada paso (extracción e ingesta) y buscar errores. Consulte [Visualización de registros de un conjunto de migración](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/viewing-logs.md) para obtener más información.
