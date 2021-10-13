---
title: Gestión de repositorios de contenido grandes
description: Esta sección describe la administración de repositorios de contenido de gran tamaño
exl-id: 2eca7fa6-fb34-4b08-b3ec-4e9211e94275
source-git-commit: 5ae76fbc3926f5e2cd7ed5597a9d4521adc9ddb1
workflow-type: tm+mt
source-wordcount: '1253'
ht-degree: 1%

---

# Gestión de repositorios de contenido grandes {#handling-large-content-repositories}

## Información general {#overview}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_precopy"
>title="Gestión de repositorios de contenido grandes"
>abstract="Para acelerar de forma significativa las fases de extracción e ingesta de la actividad de transferencia de contenido y mover el contenido a AEM as a Cloud Service, CTT puede aprovechar AzCopy como paso previo opcional. Una vez configurado este paso previo, en la fase de extracción, AzCopy copia los blobs de Amazon S3 o Azure Blob Storage en el almacén de blob del conjunto de migración. En la fase de ingesta, AzCopy copia los blobs del almacén de blobs del conjunto de migración al destino AEM almacén de blobs as a Cloud Service."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#setting-up-pre-copy-step" text="Introducción a AzCopy como paso de precopia"

La copia de un gran número de blobs con la herramienta de transferencia de contenido (CTT) puede tardar varios días.
Para acelerar de forma significativa las fases de extracción e ingesta de la actividad de transferencia de contenido y mover el contenido a AEM as a Cloud Service, CTT puede aprovechar [AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) como paso previo opcional. Este paso de precopia se puede utilizar cuando la instancia de AEM de origen está configurada para utilizar un almacén de datos de almacenamiento de blob de Amazon S3 o Azure.  Una vez configurado este paso previo, en la fase de extracción, AzCopy copia los blobs de Amazon S3 o Azure Blob Storage en el almacén de blob del conjunto de migración. En la fase de ingesta, AzCopy copia los blobs del almacén de blobs del conjunto de migración al destino AEM almacén de blobs as a Cloud Service.

>[!NOTE]
> Esta funcionalidad se introdujo en la versión 1.5.4 de CTT.

## Consideraciones importantes antes de comenzar {#important-considerations}

Siga la sección siguiente para comprender las consideraciones importantes antes de comenzar:

* La versión de AEM de origen debe ser 6.3 - 6.5
* El almacén de datos AEM origen está configurado para utilizar Amazon S3 o Azure Blob Storage. Para obtener más información, consulte [Configuración de almacenes de nodos y almacenes de datos en AEM 6](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=en).
* El almacén de datos completo se copia durante la extracción. Dado que existe un coste asociado con la transferencia de datos desde Amazon S3 y Azure Blob Storage, el coste de transferencia se relaciona con la cantidad total de datos en el contenedor de almacenamiento (tanto si se hace referencia en AEM como si no). Consulte [Amazon S3](https://aws.amazon.com/s3/pricing/) y [Almacenamiento de Azure Blob](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) para obtener más información.
* Cada conjunto de migración copiará todo el almacén de datos, por lo que solo se debe utilizar un conjunto de migración único.
* Necesitará acceso para instalar [AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) en la instancia (o VM) que ejecuta la instancia de AEM de origen.
* Necesitará un par de clave de acceso y clave secreta para el bloque Amazon S3 de origen o un URI SAS para el contenedor de almacenamiento del blob de Azure de origen (el acceso de solo lectura está bien).
* La colección de residuos del almacén de datos se ha ejecutado en los últimos 7 días en el origen. Para obtener más información, consulte [Colección de residuos del almacén de datos](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=en#data-store-garbage-collection).
* La mayoría de los datos de la instancia de origen se incluirán en la migración.

## Configuración para utilizar AzCopy como paso de precopia {#setting-up-pre-copy-step}

Siga esta sección para aprender a configurar para utilizar AzCopy como paso previo a la copia con la herramienta de transferencia de contenido para migrar el contenido a AEM as a Cloud Service:

### 0. Determinar el tamaño total de todo el contenido del almacén de datos {#determine-total-size}

#### Almacenamiento de datos de Azure Blob {#azure-blob-storage}

Desde la página de propiedades del contenedor en el portal de Azure, utilice el botón **Calcular tamaño** para determinar el tamaño de todo el contenido del contenedor. Por ejemplo:

![image](/help/move-to-cloud-service/content-transfer-tool/assets/Azure-blob-storage-data-store.png)

#### Almacenamiento de datos de Amazon S3 {#amazon-data}

Puede utilizar la ficha Métricas del contenedor para determinar el tamaño de todo el contenido del contenedor. Por ejemplo:


![image](/help/move-to-cloud-service/content-transfer-tool/assets/amazon-s3-data-store.png)

### 1. Instale AzCopy {#install-azcopy}

[](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) AzCopy es una herramienta de línea de comandos proporcionada por Microsoft que debe estar disponible en la instancia de origen para habilitar esta función.

En resumen, lo más probable es que desee descargar el binario Linux x86-64 desde la [página de documentos de AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) y desiniciarlo en una ubicación como /usr/bin. Anote dónde colocó el binario, ya que necesitará la ruta completa para acceder a él en un paso posterior.

### 2. Instale una versión de la herramienta de transferencia de contenido (CTT) con compatibilidad con AzCopy {#install-ctt-azcopy-support}

La compatibilidad con AzCopy se incluye en la versión 1.5.4 de CTT. Puede descargar la última versión de CTT desde el portal [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/es-ES/aemcloud.html).

### 3. Configurar un archivo azcopy.config {#configure-azcopy-config-file}

En la instancia de AEM de origen, en crx-quickstart/cloud-migration , cree un nuevo archivo llamado azcopy.config .

El contenido de este archivo de configuración será diferente en función de si la instancia de AEM de origen utiliza un almacén de datos de Azure o Amazon S3.

#### Almacenamiento de datos de Azure Blob {#azure-blob-storage-data}

El archivo azcopy.config debe incluir las siguientes propiedades (asegúrese de utilizar las propiedades azCopyPath y azureSas correctas para su instancia).

>[!NOTE]
>
> Si no desea conceder acceso de escritura al contenedor de almacenamiento de blob, puede generar un nuevo URI SAS que solo tenga permisos de lectura y lista.

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

### 4. Extracción con AzCopy {#extracting-azcopy}

Con el archivo de configuración anterior en su lugar, la fase de precopia de AzCopy se ejecutará como parte de cada extracción posterior. Para evitar que se ejecute, puede cambiar el nombre de este archivo o eliminarlo.

1. Inicie una extracción desde la interfaz de usuario de CTT. Consulte [Ejecución de la herramienta de transferencia de contenido](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#running-tool) y [Proceso de extracción](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#extraction-process) para obtener más información.
1. Confirme que la línea siguiente se imprime en el registro de extracción:

```
c.a.g.s.m.commons.ContentExtractor - *************** Beginning AzCopy Pre-Copy phase ***************
```

Felicitaciones! Esta entrada de registro significa que la configuración se consideró válida y que AzCopy está copiando actualmente todos los blobs del contenedor de origen al contenedor de migración.

Las entradas de registro de AzCopy aparecerán en el registro de extracción y llevarán el prefijo c.a.g.s.m.c.azcopy.AzCopyBlobPreCopy - [AzCopy pre-copy]

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

### 5. Ingesta con AzCopy {#ingesting-azcopy}

Con el lanzamiento de la herramienta de transferencia de contenido 1.5.4, hemos añadido la compatibilidad con AzCopy a la ingesta de Autores.

>[!NOTE]
>La recomendación es ejecutar la ingesta de Autor solo primero. Esto acelera la ingesta de Publicar cuando se ejecute más adelante.

Para aprovechar AzCopy durante la ingesta, necesitamos que esté en una versión as a Cloud Service AEM que sea al menos de la versión 2021.6.5561.

Inicie la ingesta de autor desde la interfaz de usuario de CTT. Consulte [Proceso de Ingesta](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#ingestion-process) para obtener más información.
Las entradas de registro de AzCopy aparecerán en el registro de ingesta. Se verán así:

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

Una vez que haya aprendido Gestión de repositorios de contenido grandes para acelerar significativamente las fases de extracción e ingesta de la actividad de transferencia de contenido para mover contenido a AEM as a Cloud Service, ya está listo para aprender el proceso de Extracción en la herramienta de transferencia de contenido. Consulte [Extracción de contenido del origen en la herramienta de transferencia de contenido](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool/extracting-content.md) para obtener información sobre cómo extraer el conjunto de migración de la herramienta de transferencia de contenido.