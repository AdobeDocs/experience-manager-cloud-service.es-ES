---
title: Gestión de repositorios de contenido grandes
description: Esta sección describe la administración de repositorios de contenido de gran tamaño
exl-id: 21bada73-07f3-4743-aae6-2e37565ebe08
source-git-commit: d07a4fd0a335295d399057ea1eef567e757e2d92
workflow-type: tm+mt
source-wordcount: '1771'
ht-degree: 3%

---

# Gestión de repositorios de contenido grandes {#handling-large-content-repositories}

## Información general {#overview}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_precopy"
>title="Gestión de repositorios de contenido grandes"
>abstract="Para acelerar de forma significativa las fases de extracción e ingesta de la actividad de transferencia de contenido y mover el contenido a AEM as a Cloud Service, CTT puede aprovechar AzCopy como paso previo opcional. Una vez configurado este paso previo, en la fase de extracción, AzCopy copia los blobs de Amazon S3 o Azure Blob Storage en el almacén de blob del conjunto de migración. En la fase de ingesta, AzCopy copia los blobs del almacén de blobs del conjunto de migración al destino AEM almacén de blobs as a Cloud Service."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#setting-up-pre-copy-step" text="Introducción a AzCopy como paso de precopia"

La copia de un gran número de blobs con la herramienta de transferencia de contenido (CTT) puede tardar varios días.
Para acelerar de forma significativa las fases de extracción e ingesta de la actividad de transferencia de contenido y así mover el contenido a AEM as a Cloud Service, CTT puede aprovechar [AzCopy](https://docs.microsoft.com/es-es/azure/storage/common/storage-use-azcopy-v10) como paso previo a la copia opcional. Este paso de precopia se puede utilizar cuando la instancia de AEM de origen está configurada para utilizar un almacén de datos de almacenamiento de blob de Amazon S3, Azure o File Data Store. El paso de precopia es más eficaz para la primera extracción e ingesta completa. Sin embargo, no se recomienda utilizar la precopia para las subsiguientes recargas (si el tamaño superior es inferior a 200 GB) porque puede añadir tiempo a todo el proceso. Una vez configurado este paso previo, en la fase de extracción, AzCopy copia los blobs de Amazon S3, Azure Blob Storage o File Data Store en el almacén de blobs del conjunto de migración. En la fase de ingesta, AzCopy copia los blobs del almacén de blobs del conjunto de migración al destino AEM almacén de blobs as a Cloud Service.

## Consideraciones importantes antes de comenzar {#important-considerations}

Siga la sección siguiente para comprender las consideraciones importantes antes de comenzar:

* La versión de AEM de origen debe ser 6.3 - 6.5.

* El almacén de datos AEM origen está configurado para utilizar Amazon S3 o Azure Blob Storage. Para obtener más información, consulte [Configuración de almacenes de nodos y almacenes de datos en AEM 6](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=en).

* Cada conjunto de migración copiará todo el almacén de datos, por lo que solo se debe utilizar un conjunto de migración único.

* Necesitará acceso para instalar [AzCopy](https://docs.microsoft.com/es-es/azure/storage/common/storage-use-azcopy-v10) en la instancia (o VM) que ejecuta la instancia de AEM de origen.

* La colección de residuos del almacén de datos se ha ejecutado en los últimos 7 días en el origen. Para obtener más información, consulte [Colección de residuos del almacén de datos](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=en#data-store-garbage-collection).

### Consideraciones adicionales al usar AzCopy

Actualmente, la precopia con AzCopy no es compatible con Windows durante la extracción de CTT.

### Consideraciones adicionales si la instancia de AEM de origen está configurada para usar un almacén de datos de almacenamiento de Amazon S3 o Azure Blob {#additional-considerations-amazons3-azure}

* Dado que existe un coste asociado con la transferencia de datos desde Amazon S3 y Azure Blob Storage, el coste de transferencia se relaciona con la cantidad total de datos en el contenedor de almacenamiento existente (tanto si se hace referencia en AEM como si no). Consulte [Amazon S3](https://aws.amazon.com/s3/pricing/) y [Almacenamiento de Azure Blob](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) para obtener más información.

* Necesitará un par clave de acceso y clave secreta para el bloque Amazon S3 de origen existente, o un URI SAS para el contenedor de almacenamiento del blob de Azure de origen existente (el acceso de solo lectura está bien).

### Consideraciones adicionales si la instancia de origen AEM está configurada para utilizar el almacén de datos de archivo {#additional-considerations-aem-instance-filedatastore}

* El sistema local debe tener un espacio libre estrictamente bueno a un tamaño de 1/256 del almacén de datos de origen. Por ejemplo, si el tamaño del almacén de datos es de 3 TB, el espacio libre bueno de 11,72 GB debe existir en la variable `crx-quickstart/cloud-migration` en el origen para que AzCopy funcione. Como mínimo, el sistema de origen debe tener 1 GB de espacio libre. El espacio libre se puede obtener utilizando `df -h` en instancias Linux, y comando dir en instancias de Windows.

* Cada vez que se ejecuta la extracción con AzCopy habilitado, todo el almacén de datos del archivo se acopla y se copia al contenedor de migración de la nube. Si el conjunto de migración es significativamente menor que el tamaño del almacén de datos, la extracción de AzCopy no es el enfoque óptimo.

* Una vez que AzCopy se ha utilizado para copiar sobre el almacén de datos existente, desactívelo para extracciones delta o superiores.

## Configuración para utilizar AzCopy como paso de precopia {#setting-up-pre-copy-step}

Siga esta sección para aprender a configurar para utilizar AzCopy como paso previo a la copia con la herramienta de transferencia de contenido para migrar el contenido a AEM as a Cloud Service:

### 0. Determinar el tamaño total de todo el contenido del almacén de datos {#determine-total-size}

Es importante determinar el tamaño total del almacén de datos por dos motivos:

* Si el AEM de origen está configurado para utilizar el almacén de datos de archivo, el sistema local debe tener espacio libre estrictamente bueno a un tamaño de 1/256 del almacén de datos de origen.

#### Almacenamiento de datos de Azure Blob {#azure-blob-storage}

Desde la página de propiedades de contenedor existente en el portal de Azure, use el **Calcular tamaño** para determinar el tamaño de todo el contenido del contenedor. Por ejemplo:

![imagen](/help/journey-migration/content-transfer-tool/assets/Azure-blob-storage-data-store.png)

#### Almacenamiento de datos de Amazon S3 {#amazon-data}

Puede utilizar la ficha Métricas del contenedor para determinar el tamaño de todo el contenido del contenedor. Por ejemplo:


![imagen](/help/journey-migration/content-transfer-tool/assets/amazon-s3-data-store.png)

#### Almacén de datos de archivo {#file-data-store-determine-size}

* Para los sistemas mac, UNIX, ejecute el comando du en el directorio datastore para obtener su tamaño:
   `du -sh [path to datastore on the instance]`. Por ejemplo, si el almacén de datos se encuentra en `/mnt/author/crx-quickstart/repository/datastore`, el siguiente comando le dará su tamaño: `du -sh /mnt/author/crx-quickstart/repository/datastore`.

* Para Windows, utilice el comando dir en el directorio del almacén de datos para obtener su tamaño:
   `dir /a/s [location of datastore]`.

### 1. Instale AzCopy {#install-azcopy}

[AzCopy](https://docs.microsoft.com/es-es/azure/storage/common/storage-use-azcopy-v10) es una herramienta de línea de comandos proporcionada por Microsoft que debe estar disponible en la instancia de origen para habilitar esta función.

En resumen, lo más probable es que desee descargar el binario Linux x86-64 del [Página documentos de AzCopy](https://docs.microsoft.com/es-es/azure/storage/common/storage-use-azcopy-v10) y envíelo a una ubicación como /usr/bin.

>[!IMPORTANT]
>Anote dónde colocó el binario, ya que necesitará la ruta completa para acceder a él en un paso posterior.

### 2. Instalación de la versión de la herramienta de transferencia de contenido (CTT) con compatibilidad con AzCopy {#install-ctt-azcopy-support}

>[!IMPORTANT]
>Se debe utilizar la versión más reciente de CTT.

La compatibilidad con AzCopy para Amazon S3, Azure Blob Storage y File Data Store se incluye en la última versión de CTT.
Puede descargar la última versión de CTT desde el [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-es/aemcloud.html) portal.
Cabe señalar que solo se admitirán las versiones 2.0.0 y posteriores, y es aconsejable utilizar la versión más reciente.

### 3. Configurar un archivo azcopy.config {#configure-azcopy-config-file}

En la instancia de AEM de origen, en `crx-quickstart/cloud-migration`, cree un nuevo archivo llamado `azcopy.config`.

>[!NOTE]
>El contenido de este archivo de configuración será diferente en función de si la instancia de AEM de origen utiliza un almacén de datos de Azure o Amazon S3 o un almacén de datos de archivo.

#### Almacenamiento de datos de Azure Blob {#azure-blob-storage-data}

El archivo azcopy.config debe incluir las siguientes propiedades (asegúrese de utilizar las propiedades azCopyPath y azureSas correctas para su instancia).

>[!NOTE]
>
> Si no desea conceder acceso de escritura al contenedor de almacenamiento de blob existente, puede generar un nuevo URI SAS que solo tenga permisos de lectura y lista.

```
azCopyPath=/usr/bin/azcopy
azureSas=https://example-resource.blob.core.windows.net/example-container?sig=--REDACTED--
```

#### Almacenamiento de datos de Amazon S3 {#amazon-sdata-store}

El archivo azcopy.config debe incluir las siguientes propiedades (asegúrese de utilizar los valores correctos para su instancia).

>[!NOTE]
>
> Si su instancia utiliza funciones de IAM para permitir que AEM acceda a S3, deberá crear una directiva y un usuario con las acciones ListBucket y GetObject habilitadas para el bloque S3. Una vez configurada, utilice la clave de acceso y la clave secreta de este usuario.

```
azCopyPath=/usr/bin/azcopy
s3Bucket=aem-63
s3Region=us-west-2
s3AccessKey=--REDACTED--
s3SecretKey=--REDACTED--
```

#### Almacén de datos de archivo {#file-data-store-azcopy-config}

Su `azcopy.config` debe contener la propiedad azCopyPath y una propiedad opcional repository.home que señale a la ubicación del almacén de datos del archivo. Utilice los valores correctos para la instancia.
Almacén de datos de archivo

```
azCopyPath=/usr/bin/azcopy
repository.home=/mnt/crx/author/crx-quickstart/repository/datastore
```

La propiedad azCopyPath debe contener la ruta completa de la ubicación donde está instalada la herramienta de línea de comandos azCopy en la instancia de AEM de origen. Si falta la propiedad azCopyPath, no se realizará el paso de precopia del blob.

If `repository.home` falta la propiedad de azcopy.config y, a continuación, la ubicación predeterminada del almacén de datos `/mnt/crx/author/crx-quickstart/repository/datastore` se utilizará para realizar la precopia.

### 4. Extracción con AzCopy {#extracting-azcopy}

Con el archivo de configuración anterior en su lugar, la fase de precopia de AzCopy se ejecutará como parte de cada extracción posterior. Para evitar que se ejecute, puede cambiar el nombre de este archivo o eliminarlo.

>[!NOTE]
>Si AzCopy no está configurado correctamente, verá este mensaje en los registros:
>`INFO c.a.g.s.m.c.a.AzCopyCloudBlobPreCopy - Blob pre-copy is not supported`.

1. Inicie una extracción desde la interfaz de usuario de CTT. Consulte [Introducción a la herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) y [Proceso de extracción](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/extracting-content.html?lang=en) para obtener más información.

1. Confirme que la línea siguiente se imprime en el registro de extracción:

```
c.a.g.s.m.commons.ContentExtractor - *************** Beginning AzCopy Pre-Copy phase ***************
```

¡Enhorabuena! Esta entrada de registro significa que la configuración se consideró válida y que AzCopy está copiando actualmente todos los blobs del contenedor de origen al contenedor de migración.

Las entradas de registro de AzCopy aparecerán en el registro de extracción y llevarán el prefijo c.a.g.s.m.c.azcopy.AzCopyBlobPreCopy - [Copia previa de AzCopy]

>[!CAUTION]
>
> Durante los primeros minutos de una extracción, observe atentamente los registros de extracción para ver si hay algún signo de problema. Por ejemplo, esto es lo que se registraría si no se encontrara el contenedor Azure de origen:

```
[AzCopy pre-copy] failed to perform copy command due to error: cannot start job due to error: cannot list files due to reason -> github.com/Azure/azure-storage-blob-go/azblob.newStorageError, github.com/Azure/azure-storage-blob-go@v0.10.1-0.20210407023846-16cf969ec1c3/azblob/zc_storage_error.go:42
[AzCopy pre-copy] ===== RESPONSE ERROR (ServiceCode=ContainerNotFound) =====
[AzCopy pre-copy] Description=The specified container does not exist.
[AzCopy pre-copy] RequestId:5fb674b9-201e-001b-2a5b-527400000000
[AzCopy pre-copy] Time:2021-05-26T18:18:07.5931967Z, Details: 
[AzCopy pre-copy] Code: ContainerNotFound
```

En caso de que se produzca un problema con AzCopy, la extracción fallará inmediatamente y los registros de extracción contendrán detalles sobre el error.

AzCopy omitirá automáticamente cualquier blobs que se haya copiado antes del error en ejecuciones posteriores y no será necesario volver a copiarlo.

#### Para el almacén de datos de archivos {#file-data-store-extract}

Cuando AzCopy se está ejecutando para el almacén de datos del archivo de origen, debería ver mensajes como estos en los registros indicando que las carpetas se están procesando:
`c.a.g.s.m.c.a.AzCopyFileSourceBlobPreCopy - [AzCopy pre-copy] Processing folder (1/24) crx-quickstart/repository/datastore/5d`

### 5. Ingesta con AzCopy {#ingesting-azcopy}

Consulte [Ingesta de contenido en Target](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html)
para obtener información general sobre la ingesta de contenido en el destino desde Cloud Acceleration Manager (CAM), incluidas instrucciones sobre cómo utilizar AzCopy (precopia), o no, en el cuadro de diálogo &quot;Nueva ingesta&quot;.

Para aprovechar AzCopy durante la ingesta, necesitamos que esté en una versión as a Cloud Service AEM que sea al menos de la versión 2021.6.5561.

Consulte la lista &quot;Trabajos de ingesta&quot; en Cloud Acceleration Manager y los registros de ingesta para ver el progreso.  Las entradas de registro relacionadas con las tareas AzCopy correctas aparecerán de la siguiente manera (lo que permite algunas diferencias). Comprobar los registros ocasionalmente podría avisar de problemas al principio y ayudarle a encontrar una solución rápida para cualquier problema.

```
*************** Beginning AzCopy pre-copy phase ***************
INFO: Scanning...
INFO: Failed to create one or more destination container(s). Your transfers may still succeed if the container already exists.
INFO: Any empty folders will not be processed, because source and/or destination doesn't have full folder support
INFO: azcopy: A newer version 10.11.0 is available to download
 
Job 419d98da-fc05-2a45-70cc-797fee632031 has started
Log file is located at: /root/.azcopy/419d98da-fc05-2a45-70cc-797fee632031.log
 
0.0 %, 0 Done, 0 Failed, 886 Pending, 0 Skipped, 886 Total,
 
Job 419d98da-fc05-2a45-70cc-797fee632031 summary
Elapsed Time (Minutes): 0.0334
Number of File Transfers: 886
Number of Folder Property Transfers: 0
Total Number of Transfers: 886
Number of Transfers Completed: 17
Number of Transfers Failed: 0
Number of Transfers Skipped: 869
TotalBytesTransferred: 248350
Final Job Status: CompletedWithSkipped
 
*************** Completed AzCopy pre-copy phase ***************
```

## Siguientes pasos {#whats-next}

Una vez que haya aprendido Gestión de repositorios de contenido grandes para acelerar significativamente las fases de extracción e ingesta de la actividad de transferencia de contenido para mover contenido a AEM as a Cloud Service, ya está listo para aprender el proceso de extracción mediante la herramienta de transferencia de contenido. Consulte [Extracción de contenido del origen en la herramienta de transferencia de contenido](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md) para aprender a extraer el conjunto de migración de la herramienta de transferencia de contenido.
