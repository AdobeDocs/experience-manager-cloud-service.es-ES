---
title: Uso de la herramienta de transferencia de contenido
description: Uso de la herramienta de transferencia de contenido
exl-id: a19b8424-33ab-488a-91b3-47f0d3c8abf5
source-git-commit: 04494e116fcdd38622ae2d4434d7cf8e4034d5aa
workflow-type: tm+mt
source-wordcount: '1503'
ht-degree: 52%

---

# Uso de la herramienta de transferencia de contenido {#using-content-transfer-tool}

## Proceso de Extracción en transferencia de contenido {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="Extracción de contenido"
>abstract="Extracción hace referencia a la extracción de contenido de la instancia de AEM de origen en un área temporal denominada conjunto de migración. El conjunto de migración es un área de almacenamiento en la nube proporcionada por Adobe para almacenar temporalmente el contenido transferido entre la instancia de AEM de origen y la instancia de AEM de Cloud Service."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-extraction-process" text="Extracción superior"

Siga los pasos a continuación para extraer el conjunto de migración de la herramienta de transferencia de contenido:
>[!NOTE]
>Si se utiliza Amazon S3 o Azure Data Store como tipo de almacén de datos, puede ejecutar el paso de precopia opcional para acelerar significativamente la fase de extracción. Para ello, debe configurar un archivo `azcopy.config` antes de ejecutar la extracción. Consulte [Gestión de repositorios de contenido de gran tamaño](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) para obtener más información.

1. Seleccione un conjunto de migraciones de la página *Información general* y haga clic en **Extracción** para empezar la extracción. Aparece el cuadro de diálogo **Migration Set extraction** y haga clic en **Extract** para iniciar la fase de extracción.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/06-content-extraction.png)

   >[!NOTE]
   >Tiene la opción de sobrescribir el contenedor de ensayo durante la fase de extracción.


1. El campo **EXTRACTION** ahora muestra el estado **RUNNING** para indicar que la extracción está en curso.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/07-extraction-job-running.png)

   Una vez finalizada la extracción, el estado del conjunto de migración se actualiza a **FINALIZADO** y aparece un icono de nube *verde lisa* debajo del campo **INFORMACIÓN** .

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/10-extraction-complete.png)

   >[!NOTE]
   >La interfaz de usuario tiene una función de recarga automática que vuelve a cargar la página de información general cada 30 segundos.
   >Cuando se inicia la fase de extracción, el bloqueo de escritura se crea y se libera después de *60 segundos*. Por lo tanto, si se detiene una extracción, hay que esperar un minuto para que se libere el bloqueo antes de volver a iniciarla.

### Extracción superior {#top-up-extraction-process}

La herramienta de transferencia de contenido tiene una función que permite agregar contenido diferencial donde solo es posible transferir los cambios realizados desde la actividad de transferencia de contenido anterior.

>[!NOTE]
>Después de la transferencia de contenido inicial, se recomienda realizar frecuentes recargas de contenido diferencial para acortar el período de congelación de contenido para la transferencia de contenido diferencial final antes de lanzarse a Cloud Service.
>Además, es esencial que la estructura de contenido del contenido existente no cambie desde el momento en que se toma la extracción inicial hasta cuando se ejecuta la extracción superior. Las superposiciones no se pueden ejecutar en contenido cuya estructura haya cambiado desde la extracción inicial. Asegúrese de restringir esto durante el proceso de migración.

Una vez completado el proceso de extracción, se puede transferir contenido delta mediante el método de extracción superior. Complete los siguientes pasos:

1. Vaya a la página *Información general* y seleccione el conjunto de migración para el que desea realizar la extracción superior. Haga clic en **Extracción** para iniciar la extracción superior. Aparece el cuadro de diálogo **extracción de conjunto de migración** .

   >[!IMPORTANT]
   >
   >Se debe desactivar la opción **Sobrescribir el contenedor de ensayo durante la extracción** .
   >
   >![image](/help/move-to-cloud-service/content-transfer-tool/assets/11-topup-extraction.png)

## Proceso de Ingesta en transferencia de contenido {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="Ingesta de contenido"
>abstract="La ingesta hace referencia a la ingesta de contenido del conjunto de migración en la instancia de Cloud Service de destino. La herramienta de transferencia de contenido tiene una función que permite agregar contenido diferencial donde solo es posible transferir los cambios realizados desde la actividad de transferencia de contenido anterior."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-ingestion-process" text="Ingesta superior"

Siga los pasos a continuación para ingerir el conjunto de migración de la herramienta de transferencia de contenido:
>[!NOTE]
>Si se utiliza Amazon S3 o Azure Data Store como tipo de almacén de datos, puede ejecutar el paso de precopia opcional para acelerar significativamente la fase de ingesta. Consulte [Ingesta con AzCopy](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#ingesting-azcopy) para obtener más información.

1. Seleccione un conjunto de migraciones de la página *Información general* y haga clic en **Ingesta** para comenzar la ingesta. Aparece el cuadro de diálogo **ingesta de conjunto de migración** . El contenido se puede ingerir en una instancia de Autor o en una instancia de Publicación a la vez. Seleccione la instancia en la que desee introducir el contenido. Haga clic en **Ingesta** para iniciar la fase de ingesta.

   >[!IMPORTANT]
   >Si se utiliza la ingesta con precopia (para S3 o Azure Data Store), se recomienda ejecutar la ingesta de Autor solo primero. Esto acelera la ingesta de Publicar cuando se ejecute más adelante.

   >[!IMPORTANT]
   >Cuando la opción **Borrar contenido existente en la instancia de Cloud antes de la ingesta** está habilitada, elimina todo el repositorio existente y crea un nuevo repositorio en el que introducir contenido. Esto significa que restablece toda la configuración, incluidos los permisos, en la instancia de Cloud Service de destino. Esto también se aplica a los usuarios administradores agregados al grupo **administradores**.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/content-ingestion-03.png)

   Además, haga clic en **Servicio de atención al cliente** para registrar un ticket, como se muestra en la figura anterior. Consulte también [Consideraciones importantes sobre el uso de la herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#pre-reqs) para obtener más información.

1. Una vez finalizada la ingesta, el estado se actualiza a **FINISHED**.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/15-ingestion-complete.png)

### Ingesta superior {#top-up-ingestion-process}

La herramienta de transferencia de contenido tiene una función que permite *agregar* contenido diferencial donde solo es posible transferir los cambios realizados desde la actividad de transferencia de contenido anterior.

>[!NOTE]
>
>Después de la transferencia de contenido inicial, se recomienda realizar frecuentes recargas de contenido diferencial para acortar el período de congelación de contenido para la transferencia de contenido diferencial final antes de lanzarse a Cloud Service.

Una vez completado el proceso de ingesta, se puede usar el contenido delta mediante el método de ingesta superior. Complete los siguientes pasos:

1. Vaya a la página *Información general* y seleccione el conjunto de migración para el que desea realizar la ingesta superior. Haga clic en **Ingesta** para iniciar la extracción superior. Aparece el cuadro de diálogo **ingesta de conjunto de migración** .

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/content-ingestion-02.png)

   >[!IMPORTANT]
   >Debe desactivar la opción **Borrar contenido existente en la instancia de Cloud antes de la ingesta** para evitar que se elimine el contenido existente de la actividad de ingesta anterior. Además, haga clic en **Servicio de atención al cliente** para registrar un ticket, como se muestra en la figura anterior.


### Visualización de registros del conjunto de migraciones {#viewing-logs-migration-set}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_logs"
>title="Visualización de registros"
>abstract="Una vez finalizada la Extracción de la Ingesta, compruebe los registros para ver si hay errores/advertencias. Cualquier error debe solucionarse inmediatamente, ya sea abordando los problemas notificados o poniéndose en contacto con el servicio de asistencia al Adobe."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#troubleshooting" text="Solución de problemas"
>additional-url="https://helpx.adobe.com/ca/enterprise/admin-guide.html/ca/enterprise/using/support-for-experience-cloud.ug.html" text="Contactar con el servicio de asistencia al Adobe"

Una vez completado cada paso (extracción e ingesta), compruebe los registros y busque errores.  Cualquier error debe solucionarse inmediatamente, ya sea abordando los problemas notificados o poniéndose en contacto con el servicio de asistencia al Adobe.

La visualización de registros de un conjunto de migraciones existente en la página *Información general* .
Complete los siguientes pasos:

1. Vaya a la página *Información general*, seleccione el conjunto de migración que desee eliminar y haga clic en **Visualización de registros** en la barra de acciones.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/view-log1.png)

1. Aparece el cuadro de diálogo **Registros** . Haga clic en **Extracción de registros** para ver los registros en una nueva pestaña.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/view-log2.png)
O

   también puede crear Visualización de registros para el conjunto de migraciones desde la pantalla *Información general* . Seleccione el conjunto de migración y haga clic en el estado en el campo **EXTRACCIÓN** . En este caso, haga clic en **FINALIZADO** para ver los registros de vista en una nueva pestaña.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/view-log3.png)

1. Para rastrear los registros sin utilizar la interfaz de usuario, puede SSH en el entorno AEM de origen y seguir el `crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`.

### Eliminación de un conjunto de migraciones {#deleting-migration-set}

Puede eliminar el conjunto de migraciones desde la página *Información general* .
Complete los siguientes pasos:

1. Vaya a la página *Información general*, seleccione el conjunto de migración que desee eliminar y haga clic en **Eliminar** en la barra de acciones.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/delete-1.png)

1. Haga clic en **Eliminar** del cuadro de diálogo **Eliminación del conjunto de migraciones** para confirmar la eliminación.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/delete-3.png)


## Ejecución de la herramienta de transferencia de contenido en una instancia de publicación {#running-ctt-on-publish}

Se recomienda que, al mover contenido a una instancia de Publish, CTT se instale en la instancia de Publish de origen para mover contenido a la instancia de Publish de destino. Siga el enfoque recomendado como se describe a continuación:

* Utilice la misma versión del CTT que se utilizó en la instancia de autor.

* Solo es necesario migrar un nodo de publicación único. Debe eliminarse del equilibrador de carga antes de comenzar la extracción.

* Al crear el conjunto de migración, utilice la URL del entorno AEMaaCS de autor.

* Durante la ingesta para publicar, el nivel de publicación NO se reducirá (a diferencia del autor). Como precaución, evite cualquier operación de escritura iniciada por el usuario, como:

   * Distribución de contenido de AEMaaCS Author para publicar en ese entorno
   * Sincronización de usuarios entre instancias de publicación


## Solución de problemas {#troubleshooting}

### ID de blob faltantes {#missing-blobs}

Si se notifican identificaciones de blob faltantes como se menciona a continuación, entonces es necesario ejecutar una prueba de consistencia en el repositorio existente y restaurar los blobs que faltan.
`ERROR o.a.j.o.p.b.AbstractSharedCachingDataStore - Error retrieving record [ba45c53f8b687e7056c85dceebf8156a0e6abc7e]`

Se ejecuta el siguiente comando:

>[!NOTE]
>
>`--verbose` se necesita el indicador para informar de las rutas de nodos desde donde se hace referencia a los blobs.

**Para repositorios AEM 6.5 (Oak 1.8 y posteriores)**

```shell
java -jar oak-run.jar datastorecheck --consistency --store [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds] <DATASTORE_CFG> --verbose <OUT_DIR> --dump
```

**Para repositorios con Oak > 1.10**

```shell
java -jar oak-run.jar datastore --check-consistency [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds|azureds] <DATASTORE_CFG> --out-dir <OUT_DIR> --work-dir <TEMP_DIR> --verbose
```

Consulte [Oak Runnable Jar](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) para obtener más detalles.

Los archivos creados en *OUT_DIR* especificados anteriormente para mantener la consistencia se pueden comprobar en busca de rutas en las que falten binarios y acciones adecuadas como restaurar desde una copia de seguridad, eliminar las rutas, volver a indexar, etc.


### Comportamiento de la IU {#ui-behavior}

Como usuario, es posible que vea los siguientes cambios de comportamiento en la IU (IU) para la herramienta de transferencia de contenido:

* Es posible que los iconos de la IU de la herramienta de transferencia de contenido sean diferentes de las capturas de pantalla que se muestran en esta guía o que no se muestren en absoluto según la versión de la instancia de origen de AEM.
