---
title: Uso de la herramienta de transferencia de contenido
description: Uso de la herramienta de transferencia de contenido
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '1412'
ht-degree: 2%

---


# Uso de la herramienta de transferencia de contenido {#using-content-transfer-tool}

## Consideraciones importantes sobre el uso de la herramienta de transferencia de contenido {#pre-reqs}

Siga la sección siguiente para comprender las consideraciones importantes al ejecutar la herramienta Transferencia de contenido:

* El requisito mínimo del sistema para la herramienta de transferencia de contenido es AEM 6.3 + y JAVA 8. Si dispone de una versión inferior de AEM, deberá actualizar el repositorio de contenido a AEM 6.5 para utilizar la herramienta de transferencia de contenido.

* Si utiliza un Entorno *de* Simulador para pruebas, asegúrese de que el entorno se actualiza a la versión del 29 de mayo de 2020 o posterior. Si utiliza un Entorno *de* producción, se actualiza automáticamente.

* Durante la fase de extracción, la herramienta de transferencia de contenido se ejecuta en una instancia de origen de AEM activa.

* La fase *de* ingestión del autor reducirá la implementación de todo el autor. Esto significa que el autor de AEM no estará disponible durante todo el proceso de inserción.

## Disponibilidad {#availability}

La herramienta de transferencia de contenido se puede descargar como archivo zip desde el portal de distribución de software. Puede instalar el paquete mediante el Administrador de paquetes en la instancia de origen de Adobe Experience Manager (AEM).

>[!NOTE]
>Consulte [Acceso a AEM como SDK](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html#accessing-the-aem-as-a-cloud-service-sdk) de servicio de nube para obtener más información.

## Ejecución de la herramienta de transferencia de contenido {#running-tool}

Siga esta sección para aprender a utilizar la herramienta de transferencia de contenido para migrar el contenido a AEM como un servicio de nube (autor/publicación):

1. Seleccione Adobe Experience Manager y vaya a las herramientas -> **Operaciones** -> Transferencia **de contenido**.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/content1.png)

1. Haga clic en **Crear conjunto** de migración para crear un nuevo conjunto de migración. Se muestran los detalles **del conjunto de migraciones de** contenido.

   >[!NOTE]
   >vista de los conjuntos de migración existentes en esta pantalla con su estado actual.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img4.png)

1. Rellene los campos de la pantalla de detalles **del conjunto de migraciones de** contenido, como se describe a continuación.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/content-3.png)


   1. **Nombre**: Introduzca el nombre del conjunto de migración.
      >[!NOTE]
      >No se permiten caracteres especiales para el nombre del conjunto de migración.

   1. **Configuración** del servicio de nube: Introduzca el AEM de destino como una URL de creación de servicios en la nube.

      >[!NOTE]
      >Puede crear y mantener un máximo de cuatro conjuntos de migración a la vez durante la actividad de transferencia de contenido.
      >Además, debe crear una migración por separado para cada uno de los entornos específicos: *Fase*, *Desarrollo* o *Producción*.

   1. **Token de acceso**: Introduzca el token de acceso.

      >[!NOTE]
      >Puede recuperar el token de acceso de la instancia de creación navegando hasta `/libs/granite/migration/token.json`.

   1. **Parámetros**: Seleccione los siguientes parámetros para crear el conjunto de migración:

      1. **Incluir versión**: Seleccione la opción que desee.

      1. **Rutas que se incluirán**: Utilice el navegador de rutas para seleccionar las rutas que deben migrarse.

         >[!IMPORTANT]
         >Las siguientes rutas están restringidas al crear un conjunto de migración:
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc`


1. Haga clic en **Guardar** después de rellenar todos los campos en la pantalla de detalles **del conjunto de migraciones de** contenido.

1. La vista del conjunto de migraciones se realizará en la página *Información general* .

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img4.png)

   Todos los conjuntos de migración existentes en esta pantalla se muestran en la página *Información general* con su estado actual y su información de estado.

   * Una nube *roja* indica que no se puede completar el proceso de extracción.
   * Una nube ** verde indica que puede completar el proceso de extracción.
   * Un icono ** amarillo indica que no creó el conjunto de migración existente y que el específico lo crea otro usuario en la misma instancia.

1. Seleccione un conjunto de migración de la página de información general y haga clic en **Propiedades** para realizar la vista o editar las propiedades del conjunto de migración.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img6.png)

### Proceso de Extracción en la transferencia de contenido {#extraction-process}

Siga los pasos a continuación para extraer el conjunto de migración de la herramienta de transferencia de contenido:

1. Seleccione un conjunto de migraciones de la página *Información general* y haga clic en **Extraer** a extracción de inicio.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/extraction-img1.png)

1. Aparece el cuadro de diálogo extracción **de conjunto de** migración y haga clic en **Extraer** para completar la fase de extracción.

   >[!NOTE]
   >Tiene la opción de sobrescribir el contenedor de ensayo durante la fase de extracción.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/extract-2.png)

1. El campo **EXTRACCIÓN** ahora muestra el estado **EJECUTANDO** para el proceso de extracción en curso.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/extract-3.png)

   Una vez finalizada la extracción, el estado del conjunto de migración se actualiza a **FINISHED** y aparece un icono de nube verde ** sólida en el campo **INFORMACIÓN** .

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/extract-4.png)

   >[!NOTE]
   > Tendrá que actualizar la página para vista del estado actualizado.

#### Extracción de arriba {#top-up-extraction-process}

La herramienta de transferencia de contenido tiene una función que admite la adición de contenido diferencial donde solo es posible transferir los cambios realizados desde la actividad de transferencia de contenido anterior.

>[!NOTE]
>Después de la transferencia de contenido inicial, se recomienda realizar frecuentes recargas de contenido diferencial para acortar el período de congelación de contenido para la transferencia de contenido diferencial final antes de lanzarse al servicio de nube.

Una vez completado el proceso de extracción, puede transferir contenido delta mediante el método de extracción de arriba. Siga los pasos a continuación:

1. Vaya a la página *Información general* y seleccione el conjunto de migración para el que desea realizar la extracción de arriba.

1. Haga clic en **Extraer** para inicio de la extracción superior.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/extraction-img1.png)

1. Aparece el cuadro de diálogo extracción **de conjunto de** migración.

   >[!IMPORTANT]
   >Debe desactivar la opción **Sobrescribir contenedor de ensayo durante la extracción** .
   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/extract-topup-1.png)

### Proceso de inserción en la transferencia de contenido {#ingestion-process}

Siga los pasos a continuación para ingerir el conjunto de migraciones desde la herramienta de transferencia de contenido:

1. Seleccione un conjunto de migraciones de la página *Información general* y haga clic en **Ingestar** a extracción de inicio.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-1.png)

1. Se abre el cuadro de diálogo **de ingesta** de conjunto de migración.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-2.png)

   Para fines de demostración, se desactiva la opción **Ingestar contenido en la instancia** Autor. Es posible ingerir contenido al mismo tiempo en Autor y Publicar.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-3.png)

   Haga clic en **Ingesta** para completar la fase de ingesta.

1. Una vez finalizada la ingestión, el estado en el campo **AUTHOR INGESTION** se actualiza a **FINISHED** y aparece un icono de nube verde sólido bajo la **INFORMACIÓN**.
   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-4.png)

   >[!NOTE]
   > Tendrá que actualizar la página para vista del estado actualizado.

#### Introducción superior {#top-up-ingestion-process}

La herramienta de transferencia de contenido tiene una función que admite la *recarga* de contenido diferencial donde solo es posible transferir los cambios realizados desde la actividad de transferencia de contenido anterior.

>[!NOTE]
>Después de la transferencia de contenido inicial, se recomienda realizar frecuentes recargas de contenido diferencial para acortar el período de congelación de contenido para la transferencia de contenido diferencial final antes de lanzarse al servicio de nube.

Una vez completado el proceso de ingestión, puede utilizar el contenido delta mediante el método de ingestión adicional. Siga los pasos a continuación:

1. Vaya a la página *Información general* y seleccione el conjunto de migración para el que desea realizar la ingesta de información adicional.

1. Haga clic en **Ingesta** para inicio de la extracción superior.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-1.png)

1. Aparece el cuadro de diálogo **Migración de conjuntos** .

   >[!NOTE]
   >Debe desactivar la opción *Borrar* para evitar que se elimine el contenido existente de la actividad de ingestión anterior.
   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-topup-1.png)

### Visualización de registros de un conjunto de migraciones {#viewing-logs-migration-set}

Los registros de vista de un conjunto de migraciones existente se pueden crear desde la página *Información general* .
Siga los pasos a continuación:

1. Vaya a la página *Información general* , seleccione el conjunto de migración que desee eliminar y haga clic en Registro **de** Vistas en la barra de acciones.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/view-log1.png)

1. Aparece el cuadro de diálogo **Registros** . Haga clic en Registros **de** Extracción para vista de los registros en una nueva ficha.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/view-log2.png)Or,

   También puede crear registros de vistas para el conjunto de migraciones desde la pantalla *Información general* . Seleccione el conjunto de migración y haga clic en el estado en el campo **EXTRACCIÓN** . En este caso, haga clic en **FINALIZADO** para ver los registros de vista en una nueva ficha.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/view-log3.png)

### Eliminación de un conjunto de migraciones {#deleting-migration-set}

Puede eliminar el conjunto de migraciones desde la página *Información general* .
Siga los pasos a continuación:

1. Vaya a la página *Información general* , seleccione el conjunto de migración que desee eliminar y haga clic en **Eliminar** en la barra de acciones.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/delete-1.png)

1. Haga clic en **Eliminar** del cuadro de diálogo **Eliminar conjunto** de migración para confirmar la eliminación.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/delete-3.png)

## Solución de problemas {#troubleshooting}

### Faltan ID de blob {#missing-blobs}

Si se notifican las identificaciones de blob que faltan, como se menciona a continuación, entonces es necesario ejecutar una comprobación de coherencia en el repositorio existente y restaurar los blobs que faltan.
`ERROR o.a.j.o.p.b.AbstractSharedCachingDataStore - Error retrieving record [ba45c53f8b687e7056c85dceebf8156a0e6abc7e]`

Se ejecuta el siguiente comando

>[!NOTE]
> `--verbose` se requiere para informar de las rutas de nodos desde donde se hace referencia a los blobs.

**Para repositorios AEM 6.5 (Oak 1.8 y posterior)**

```shell
java -jar oak-run.jar datastorecheck --consistency --store [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds] <DATASTORE_CFG> --verbose <OUT_DIR> --dump
```

**Para repositorios con Oak > 1.10**

```shell
java -jar oak-run.jar datastore --check-consistency [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds|azureds] <DATASTORE_CFG> --out-dir <OUT_DIR> --work-dir <TEMP_DIR> --verbose
```

Consulte [Oak Runnable Jar](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) para obtener más detalles.

Los archivos creados en *OUT_DIR* especificados anteriormente para mantener la coherencia se pueden comprobar en busca de rutas en las que falten binarios y acciones adecuadas como restaurar desde una copia de seguridad, eliminar las rutas, volver a indexar, etc.

### Comportamiento de la interfaz de usuario {#ui-behavior}

Como usuario, es posible que vea los siguientes cambios de comportamiento en la interfaz de usuario (IU) para la herramienta de transferencia de contenido:

1. El usuario crea un conjunto de migraciones para una URL de creación (Desarrollo/Fase/Producción) y realiza correctamente la extracción y la ingesta.

1. A continuación, el usuario crea un nuevo conjunto de migración para la misma URL de creación y realiza la extracción y la ingestión en el nuevo conjunto de migración. La interfaz de usuario muestra que el estado de inserción del primer conjunto de migración cambia a **FALLO** y que no hay registros disponibles.

1. Esto no significa que se haya producido un error en la ingestión del primer conjunto de migración. Este comportamiento se observa porque cuando se inicia un nuevo trabajo de ingestión, se elimina el trabajo de ingestión anterior. Por lo tanto, se debe ignorar el estado de los cambios en el primer conjunto de migración.


