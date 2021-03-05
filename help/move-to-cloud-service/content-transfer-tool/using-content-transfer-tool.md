---
title: Uso de la herramienta de transferencia de contenido
description: Uso de la herramienta de transferencia de contenido
translation-type: tm+mt
source-git-commit: cef8c78e5fec840ea1cc4d391240e3bf9a4d7c02
workflow-type: tm+mt
source-wordcount: '2053'
ht-degree: 58%

---


# Uso de la herramienta de transferencia de contenido {#using-content-transfer-tool}

## Consideraciones importantes sobre el uso de la herramienta de transferencia de contenido {#pre-reqs}

En la sección siguiente se comprenden las consideraciones importantes al ejecutar la herramienta de transferencia de contenido:

* El requisito mínimo del sistema para la herramienta de transferencia de contenido es AEM 6.3+ y JAVA 8. Si dispone de una versión anterior de AEM, deberá actualizar el repositorio de contenido a AEM 6.5 para usar la herramienta de transferencia de contenido.

* Java debe configurarse en el entorno de AEM para que el usuario que inicia AEM pueda ejecutar el comando `java`.

* Se recomienda desinstalar las versiones anteriores de la herramienta de transferencia de contenido al instalar la versión 1.3.0, ya que se ha producido un cambio importante en la arquitectura de la herramienta. Con 1.3.0, también debe crear nuevos conjuntos de migración y volver a ejecutar la extracción y la ingesta en los nuevos conjuntos de migración.

* La herramienta de transferencia de contenido se puede utilizar con los siguientes tipos de almacén de datos: Almacén de datos de archivos, almacén de datos S3, almacén de datos compartido S3 y almacén de datos del blob de Azure.

* Si utiliza un *Entorno de espacio aislado*, asegúrese de que su entorno esté actualizado y actualizado a la última versión. Si utiliza un *Entorno de producción*, se actualiza automáticamente.

* Para utilizar la herramienta de transferencia de contenido, deberá ser un usuario administrador en la instancia de origen y pertenecer al grupo de administradores de AEM local en la instancia de Cloud Service a la que esté transfiriendo el contenido. Los usuarios sin privilegios no podrán recuperar el token de acceso para utilizar la herramienta de transferencia de contenido.

* El token de acceso puede caducar periódicamente después de un período de tiempo específico o después de actualizar el entorno de Cloud Service. Si el token de acceso ha caducado, no podrá conectarse a la instancia de Cloud Service y tendrá que recuperar el nuevo token de acceso. El icono de estado asociado con un conjunto de migración existente cambiará a una nube roja y mostrará un mensaje cuando pase el ratón por encima de él.

* Los usuarios y grupos que transfiere la herramienta de transferencia de contenido son solo aquellos que necesita el contenido para satisfacer los permisos. El proceso *Extraction* copia todo el `/home` en el conjunto de migración y el proceso *Ingestion* copia todos los usuarios y grupos a los que se hace referencia en las ACL de contenido migrado. Para asignar automáticamente los usuarios y grupos existentes a sus ID de IMS, consulte [Uso de la herramienta de asignación de usuarios](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration).

* Durante la fase de extracción, la herramienta de transferencia de contenido se ejecuta en una instancia de origen de AEM activa.

* Después de completar la fase *Extraction* del proceso de transferencia de contenido y antes de iniciar la *Fase de ingesta* para introducir contenido en AEM as a Cloud Service *Stage* o las instancias de *Producción*, deberá registrar un ticket de asistencia para notificar a Adobe su intención de ejecutar la *Ingesta&lt;a&lt;a>9/> para que Adobe pueda garantizar que no se produzcan interrupciones durante el proceso* Ingesta *.* Tendrá que registrar el ticket de soporte 1 semana antes de la fecha planificada *Ingesta*. Una vez que haya enviado el ticket de soporte, el equipo de soporte le proporcionará instrucciones sobre los pasos siguientes.
   * Registre un vale de soporte con los siguientes detalles:
      * Fecha exacta y hora estimada (con su zona horaria) en la que planea iniciar la fase *Ingesta*.
      * Tipo de entorno (fase o producción) en el que planea introducir datos.
      * ID del programa.

* La *fase de Ingesta* del autor reducirá la implementación de todo el autor. Esto significa que el autor de AEM no estará disponible durante todo el proceso de inserción. Asegúrese también de que no se ejecutan canalizaciones de Cloud Manager mientras está ejecutando la fase *Ingesta*.


## Disponibilidad {#availability}

La herramienta de transferencia de contenido se puede descargar como archivo zip desde el portal de distribución de software. Puede instalar el paquete mediante el Administrador de paquetes en la instancia de origen de Adobe Experience Manager (AEM). Asegúrese de descargar la última versión. Para obtener más información sobre la versión más reciente, consulte [Notas de la versión](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html).

>[!NOTE]
>Descargue Content Transfer Tool desde el portal de [distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-ES/aemcloud.html).

## Ejecución de la herramienta de transferencia de contenido {#running-tool}

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)


Siga esta sección para aprender a utilizar la herramienta de transferencia de contenido para migrar el contenido a AEM as a Cloud Service (autor/publicación):

1. Seleccione Adobe Experience Manager y vaya a las herramientas -> **Operaciones** -> **Migración de contenido**.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-entry-card01.png)

1. Seleccione la opción **Content Transfer** del asistente **Content Migration**.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-entry-card02.png)


1. La consola siguiente aparece al crear el primer conjunto de migración. Haga clic en **Crear conjunto** de migración para crear un conjunto de migración nuevo.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/01-create-migrationset.png)


   >[!NOTE]
   >Si tiene conjuntos de migración existentes, la consola mostrará la lista de conjuntos de migración existentes con su estado actual.

   Además, haga clic en **Crear configuración de asignación de usuarios** para acceder a la [Herramienta de asignación de usuarios](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool).

1. Rellene los campos de la pantalla **Crear conjunto de migración** como se describe a continuación.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/migration-set-creation-04.png)

   1. **Nombre**: introduzca el nombre del conjunto de migración.
      >[!NOTE]
      >No se permiten caracteres especiales para el nombre del conjunto de migración.

   1. **Configuración de Cloud Service**: introduzca la URL de Autor de destino de AEM as a Cloud Service.

      >[!NOTE]
      >Puede crear y mantener un máximo de cuatro conjuntos de migración a la vez durante la actividad de transferencia de contenido.
      >Además, debe crear una migración por separado para cada uno de los entornos específicos: *Fase*, *Desarrollo* o *Producción*.

   1. **Token de acceso**: introduzca el token de acceso.

      >[!NOTE]
      >Puede recuperar el token de acceso mediante el botón **Open access token**. Debe asegurarse de pertenecer al grupo de administradores de AEM en la instancia de Cloud Service de destino.

   1. **Parámetros**: seleccione los siguientes parámetros para crear el conjunto de migración:

      1. **Incluir versión**: seleccione la opción que desee.

      1. **Incluir asignación de usuarios y grupos de IMS**: Seleccione la opción para incluir la asignación de Usuarios y grupos de IMS.
Consulte [Herramienta de asignación de usuarios](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) para obtener más información.

      1. **Rutas que se incluyen**: utilice el explorador para seleccionar las rutas que deben migrarse. El selector de rutas acepta entradas mediante escritura o selección.

         >[!IMPORTANT]
         >Las siguientes rutas están restringidas al crear un conjunto de migración:
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc` (se permite seleccionar algunas  `/etc` rutas en CTT)


1. Haga clic en **Guardar** después de rellenar todos los campos en la pantalla de detalles **del conjunto de migraciones de contenido**.

1. La vista del conjunto de migraciones se realizará en la página de *Información general*.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/04-item-selection-and-quick-actions.png)

   Todos los conjuntos de migración existentes en esta pantalla se muestran en la página *Información general* con su estado actual y la información de estado. Puede ver algunos de estos iconos que se describen a continuación.

   * La *nube roja* indica que no se puede completar el proceso de extracción.
   * La *nube verde* indica que se puede completar el proceso de extracción.
   * El *icono amarillo* indica que no se creó el conjunto de migración existente y que el específico lo crea otro usuario en la misma instancia.

1. Seleccione un conjunto de migración de la página de información general y haga clic en **Propiedades** para consultar o editar las propiedades del conjunto de migración. Durante la edición de propiedades, no es posible cambiar el nombre del contenedor o la dirección URL del servicio.


### Proceso de Extracción en transferencia de contenido {#extraction-process}

Siga los pasos a continuación para extraer el conjunto de migración de la herramienta de transferencia de contenido:

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

#### Extracción superior {#top-up-extraction-process}

La herramienta de transferencia de contenido tiene una función que permite agregar contenido diferencial donde solo es posible transferir los cambios realizados desde la actividad de transferencia de contenido anterior.

>[!NOTE]
>Después de la transferencia de contenido inicial, se recomienda realizar frecuentes recargas de contenido diferencial para acortar el período de congelación de contenido para la transferencia de contenido diferencial final antes de lanzarse a Cloud Service.

Una vez completado el proceso de extracción, se puede transferir contenido delta mediante el método de extracción superior. Complete los siguientes pasos:

1. Vaya a la página *Información general* y seleccione el conjunto de migración para el que desea realizar la extracción superior. Haga clic en **Extracción** para iniciar la extracción superior. Aparece el cuadro de diálogo **extracción de conjunto de migración** .

   >[!IMPORTANT]
   >
   >Se debe desactivar la opción **Sobrescribir el contenedor de ensayo durante la extracción** .
   >
   >![image](/help/move-to-cloud-service/content-transfer-tool/assets/11-topup-extraction.png)

### Proceso de Ingesta en transferencia de contenido {#ingestion-process}

Siga los pasos a continuación para ingerir el conjunto de migración de la herramienta de transferencia de contenido:

1. Seleccione un conjunto de migraciones de la página *Información general* y haga clic en **Ingesta** para empezar la extracción. Aparece el cuadro de diálogo **ingesta de conjunto de migración** . Haga clic en **Ingesta** para iniciar la fase de ingesta. Es posible la ingesta del contenido al mismo tiempo en Autor y Publish.

   >[!IMPORTANT]
   >Cuando la opción **Borrar contenido existente en la instancia de Cloud antes de la ingesta** está habilitada, elimina todo el repositorio existente y crea un nuevo repositorio en el que introducir contenido. Esto significa que restablece toda la configuración, incluidos los permisos, en la instancia de Cloud Service de destino.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/top-ingestion-image01.png)

   Además, haga clic en **Servicio de atención al cliente** para registrar un ticket, como se muestra en la figura anterior. Consulte también [Consideraciones importantes sobre el uso de la herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#pre-reqs) para obtener más información.

1. Una vez finalizada la ingesta, el estado en el campo **PUBLISH INGESTION** se actualiza a **FINISHED**.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/15-ingestion-complete.png)

#### Ingesta superior {#top-up-ingestion-process}

La herramienta de transferencia de contenido tiene una función que permite *agregar* contenido diferencial donde solo es posible transferir los cambios realizados desde la actividad de transferencia de contenido anterior.

>[!NOTE]
>
>Después de la transferencia de contenido inicial, se recomienda realizar frecuentes recargas de contenido diferencial para acortar el período de congelación de contenido para la transferencia de contenido diferencial final antes de lanzarse a Cloud Service.

Una vez completado el proceso de ingesta, se puede usar el contenido delta mediante el método de ingesta superior. Complete los siguientes pasos:

1. Vaya a la página *Información general* y seleccione el conjunto de migración para el que desea realizar la ingesta superior. Haga clic en **Ingesta** para iniciar la extracción superior. Aparece el cuadro de diálogo **ingesta de conjunto de migración** .

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/content-ingestion-01.png)

   >[!IMPORTANT]
   >Debe desactivar la opción **Borrar contenido existente en la instancia de Cloud antes de la ingesta** para evitar que se elimine el contenido existente de la actividad de ingesta anterior.


### Visualización de registros del conjunto de migraciones {#viewing-logs-migration-set}

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


