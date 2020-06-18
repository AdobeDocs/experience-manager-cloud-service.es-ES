---
title: Uso de la herramienta de transferencia de contenido
description: Uso de la herramienta de transferencia de contenido
translation-type: tm+mt
source-git-commit: 3da4c659893e55f5ffe104ea08ea89cc296050c1
workflow-type: tm+mt
source-wordcount: '1582'
ht-degree: 91%

---


# Uso de la herramienta de transferencia de contenido {#using-content-transfer-tool}

## Consideraciones importantes sobre el uso de la herramienta de transferencia de contenido {#pre-reqs}

En la sección siguiente se comprenden las consideraciones importantes al ejecutar la herramienta de transferencia de contenido:

* El requisito mínimo del sistema para la herramienta de transferencia de contenido es AEM 6.3+ y JAVA 8. Si dispone de una versión anterior de AEM, deberá actualizar el repositorio de contenido a AEM 6.5 para usar la herramienta de transferencia de contenido.

* If you are using a *Sandbox Environment*, ensure that your environment is upgraded to June 10 2020 Release or later. Si utiliza un *Entorno de producción*, se actualiza automáticamente.

* Para utilizar la herramienta de transferencia de contenido, deberá ser un usuario administrador en la instancia de origen y pertenecer al grupo de administradores de AEM en la instancia de Cloud Service a la que esté transfiriendo contenido. Los usuarios sin privilegios no podrán recuperar el token de acceso para utilizar la herramienta de transferencia de contenido.

* Durante la fase de extracción, la herramienta de transferencia de contenido se ejecuta en una instancia de origen de AEM activa.

* La *fase de Ingesta* del autor reducirá la implementación de todo el autor. Esto significa que el autor de AEM no estará disponible durante todo el proceso de inserción.

* El límite superior recomendado para el tamaño del repositorio que la herramienta de transferencia de contenido puede admitir a la vez es de 20 GB.

## Disponibilidad {#availability}

La herramienta de transferencia de contenido se puede descargar como archivo zip (Content Transfer Tool v1.0.0) desde el portal de distribución de software. Puede instalar el paquete mediante el Administrador de paquetes en la instancia de origen de Adobe Experience Manager (AEM).

>[!NOTE]
>Descargue Content Transfer Tool, desde el portal [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/es-ES/aemcloud.html) .

## Ejecución de la herramienta de transferencia de contenido {#running-tool}

Siga esta sección para aprender a utilizar la herramienta de transferencia de contenido para migrar el contenido a AEM as a Cloud Service (autor/publicación):

1. Seleccione Adobe Experience Manager y vaya a las herramientas -> **Operaciones** -> Transferencia **de contenido**.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/content1.png)

1. Haga clic en **Crear conjunto** de migración para crear un conjunto de migración nuevo. Se muestran los detalles **del conjunto de migraciones de** contenido.

   >[!NOTE]
   >Vista los conjuntos de migración existentes en esta pantalla con su estado actual.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img4.png)

1. Rellene los campos de la pantalla de detalles **del conjunto de migraciones de contenido** como se describe a continuación.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/content-3.png)


   1. **Nombre**: introduzca el nombre del conjunto de migración.
      >[!NOTE]
      >No se permiten caracteres especiales para el nombre del conjunto de migración.

   1. **Configuración de Cloud Service**: introduzca la URL de Autor de destino de AEM as a Cloud Service.

      >[!NOTE]
      >Puede crear y mantener un máximo de cuatro conjuntos de migración a la vez durante la actividad de transferencia de contenido.
      >Además, debe crear una migración por separado para cada uno de los entornos específicos: *Fase*, *Desarrollo* o *Producción*.

   1. **Token de acceso**: introduzca el token de acceso.

      >[!NOTE]
      >Puede recuperar el token de acceso de la instancia de autor navegando hasta `/libs/granite/migration/token.json`. El token de acceso se recupera de la instancia de creación del Cloud Service.

   1. **Parámetros**: seleccione los siguientes parámetros para crear el conjunto de migración:

      1. **Incluir versión**: seleccione la opción que desee.

      1. **Rutas que se incluyen**: utilice el explorador para seleccionar las rutas que deben migrarse.

         >[!IMPORTANT]
         >Las siguientes rutas están restringidas al crear un conjunto de migración:
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc`


1. Haga clic en **Guardar** después de rellenar todos los campos en la pantalla de detalles **del conjunto de migraciones de contenido**.

1. La vista del conjunto de migraciones se realizará en la página de *Información general*.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img4.png)

   Todos los conjuntos de migración existentes en esta pantalla se muestran en la página *Información general* con su estado actual y la información de estado.

   * La *nube roja* indica que no se puede completar el proceso de extracción.
   * La *nube verde* indica que se puede completar el proceso de extracción.
   * El *icono amarillo* indica que no se creó el conjunto de migración existente y que el específico lo crea otro usuario en la misma instancia.

1. Seleccione un conjunto de migración de la página de información general y haga clic en **Propiedades** para consultar o editar las propiedades del conjunto de migración.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img6.png)

### Proceso de Extracción en transferencia de contenido {#extraction-process}

Siga los pasos a continuación para extraer el conjunto de migración de la herramienta de transferencia de contenido:

1. Seleccione un conjunto de migraciones de la página *Información general* y haga clic en **Extracción** para empezar la extracción.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/extraction-img1.png)

1. Cuando aparezca el cuadro de diálogo **extracción de conjunto de migración** y haga clic en **Extracción** para completar la fase.

   >[!NOTE]
   >Tiene la opción de sobrescribir el contenedor de ensayo durante la fase de extracción.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/extract-2.png)

1. El campo **EXTRACCIÓN** ahora muestra el estado **EJECUTANDO** para el proceso de extracción en curso.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/extract-3.png)

   Una vez finalizada la extracción, el estado del conjunto de migración se actualiza a **FINALIZADO** y aparece un icono de nube *verde lisa* debajo del campo **INFORMACIÓN** .

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/extract-4.png)

   >[!NOTE]
   >Se tiene que actualizar la página para ver el estado actualizado.
   >Cuando se inicia la fase de extracción, el bloqueo de escritura se crea y se libera después de *60 segundos*. Por lo tanto, si se detiene una extracción, hay que esperar un minuto para que se libere el bloqueo antes de volver a iniciarla.

#### Extracción superior {#top-up-extraction-process}

La herramienta de transferencia de contenido tiene una función que permite agregar contenido diferencial donde solo es posible transferir los cambios realizados desde la actividad de transferencia de contenido anterior.

>[!NOTE]
>Después de la transferencia de contenido inicial, se recomienda realizar frecuentes recargas de contenido diferencial para acortar el período de congelación de contenido para la transferencia de contenido diferencial final antes de lanzarse a Cloud Service.

Una vez completado el proceso de extracción, se puede transferir contenido delta mediante el método de extracción superior. Complete los siguientes pasos:

1. Vaya a la página *Información general* y seleccione el conjunto de migración para el que desea realizar la extracción superior.

1. Haga clic en **Extracción** para iniciar la extracción superior.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/extraction-img1.png)

1. Aparece el cuadro de diálogo **extracción de conjunto de migración** .

   >[!IMPORTANT]
   >Se debe desactivar la opción **Sobrescribir el contenedor de ensayo durante la extracción** .
   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/extract-topup-1.png)

### Proceso de Ingesta en transferencia de contenido {#ingestion-process}

Siga los pasos a continuación para ingerir el conjunto de migración de la herramienta de transferencia de contenido:

1. Seleccione un conjunto de migraciones de la página *Información general* y haga clic en **Ingesta** para empezar la extracción.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-1.png)

1. Aparece el cuadro de diálogo **ingesta de conjunto de migración** .

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-2.png)

   Para fines de demostración, se desactiva la opción **Ingesta de contenido de Autor** . Es posible la ingesta del contenido al mismo tiempo en Autor y Publish.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-3.png)

   Haga clic en **Ingesta** para completar la fase.

1. Una vez finalizada la extracción, el campo del estado **INGESTA DE AUTOR** se actualiza a **FINALIZADO** y aparece un icono de nube verde lisa debajo de **INFORMACIÓN**.
   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-4.png)

   >[!NOTE]
   > Se tiene que actualizar la página para ver el estado actualizado.

#### Ingesta superior {#top-up-ingestion-process}

La herramienta de transferencia de contenido tiene una función que permite *agregar* contenido diferencial donde solo es posible transferir los cambios realizados desde la actividad de transferencia de contenido anterior.

>[!NOTE]
>Después de la transferencia de contenido inicial, se recomienda realizar frecuentes recargas de contenido diferencial para acortar el período de congelación de contenido para la transferencia de contenido diferencial final antes de lanzarse a Cloud Service.

Una vez completado el proceso de ingesta, se puede usar el contenido delta mediante el método de ingesta superior. Complete los siguientes pasos:

1. Vaya a la página *Información general* y seleccione el conjunto de migración para el que desea realizar la ingesta superior.

1. Haga clic en **Ingesta** para iniciar la extracción superior.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-1.png)

1. Aparece el cuadro de diálogo **ingesta de conjunto de migración** .

   >[!NOTE]
   >Debe desactivar la opción *Borrar* para evitar que se elimine el contenido existente de la actividad de ingesta anterior.
   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-topup-1.png)

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
> `--verbose` se necesita el indicador para informar de las rutas de nodos desde donde se hace referencia a los blobs.

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

* El usuario crea un conjunto de migraciones para una URL de creación (Desarrollo, fase, producción) y realiza correctamente la extracción y la ingesta.

* A continuación, el usuario crea un nuevo conjunto de migración para la misma URL de creación y realiza la extracción y la ingesta en el nuevo conjunto de migración. La IU muestra que el estado de ingesta del primer conjunto de migración cambia a **ERRÓNEO** y que no hay registros disponibles.

* Esto no significa que se haya producido un error en la ingesta del primer conjunto de migración. Este comportamiento se observa porque cuando se inicia un nuevo trabajo de ingesta, se elimina el trabajo de ingesta anterior. Por lo tanto, se debe ignorar el estado de los cambios en el primer conjunto de migración.

* Es posible que los iconos de la IU de la herramienta de transferencia de contenido sean diferentes de las capturas de pantalla que se muestran en esta guía o que no se muestren en absoluto según la versión de la instancia de origen de AEM.


