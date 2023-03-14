---
title: Gestión de repositorios de contenido grandes (heredados)
description: En esta sección se describe la administración de repositorios de contenido grandes
hide: true
hidefromtoc: true
exl-id: 19021f40-d0a5-4e0c-a213-c421338cedeb
source-git-commit: 22bbf15e33ab3d5608dc01ed293bb04b07cb6c8c
workflow-type: tm+mt
source-wordcount: '1638'
ht-degree: 4%

---

# Gestión de repositorios de contenido grandes (heredados) {#handling-large-content-repositories}

## Información general {#overview}

Copiar un gran número de blobs con la herramienta de transferencia de contenido (CTT) puede tardar varios días.
AEM Para acelerar de forma significativa las fases de extracción e ingesta de la actividad de transferencia de contenido para mover el contenido a las fases de extracción y de ingesta de contenido as a Cloud Service, CTT puede aprovechar las ventajas de la transferencia de contenido a través de la [AzCopy](https://docs.microsoft.com/es-es/azure/storage/common/storage-use-azcopy-v10) como paso opcional previo a la copia. AEM Este paso previo a la copia se puede utilizar cuando la instancia de origen se configura para que utilice un almacén de datos de Amazon S3, Azure Blob Storage o un almacén de datos de archivo. Una vez configurado este paso previo, en la fase de extracción, AzCopy copia blobs de Amazon S3, Azure Blob Storage o el almacén de datos de archivo al almacén de blobs del conjunto de migración. AEM En la fase de ingesta, AzCopy copia los blobs del almacén de blobs del conjunto de migración al almacén de blobs as a Cloud Service de destino de la.

>[!NOTE]
> Esta funcionalidad se introdujo en la versión 1.5.4 de CTT.

## Consideraciones importantes antes de comenzar {#important-considerations}

En la sección siguiente se comprenden las consideraciones importantes antes de comenzar:

* AEM La versión de origen debe ser de 6.3 a 6.5.

* AEM El almacén de datos de origen está configurado para utilizar Amazon S3 o Azure Blob Storage. Para obtener más información, consulte [AEM Configuración de almacenes de nodos y almacenes de datos en el 6](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=en).

* Cada conjunto de migración copiará todo el almacén de datos, por lo que solo se debe utilizar un conjunto de migración único.

* Necesitará acceso para instalar [AzCopy](https://docs.microsoft.com/es-es/azure/storage/common/storage-use-azcopy-v10) AEM en la instancia (o VM) que ejecuta la instancia de origen de la instancia de la.

* La recolección de elementos no utilizados del almacén de datos se ha ejecutado en los últimos 7 días en el origen. Para obtener más información, consulte [Recopilación de residuos del almacén de datos](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=en#data-store-garbage-collection).


### AEM Consideraciones adicionales si la instancia de la fuente de datos está configurada para usar un almacén de datos de almacenamiento de Amazon S3 o Azure Blob {#additional-considerations-amazons3-azure}

* Dado que existe un coste asociado con la transferencia de datos desde Amazon AEM S3 y Azure Blob Storage, el coste de la transferencia será relativo a la cantidad total de datos en el contenedor de almacenamiento (se haga referencia en el campo de datos o no). Consulte [Amazon S3](https://aws.amazon.com/s3/pricing/) y [Almacenamiento de Azure Blob](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) para obtener más información.

* Necesitará un par de clave de acceso y clave secreta para el contenedor de Amazon S3 de origen o un URI SAS para el contenedor de almacenamiento de Azure Blob de origen (el acceso de solo lectura está bien).

### AEM Consideraciones adicionales si la instancia de origen está configurada para utilizar el almacén de datos de archivo {#additional-considerations-aem-instance-filedatastore}

* El sistema local debe tener un espacio libre estrictamente bueno al tamaño 1/256 del almacén de datos de origen. Por ejemplo, si el tamaño del almacén de datos es de 3 TB, debe existir espacio libre bueno a 11,72 GB en `crx-quickstart/cloud-migration` en el origen para que funcione AzCopy. Como mínimo, el sistema de origen debe tener 1 GB de espacio libre. El espacio libre se puede obtener utilizando `df -h` en instancias de Linux y el comando dir en instancias de Windows.

* Cada vez que se ejecuta la extracción con AzCopy habilitado, todo el almacén de datos de archivos se aplana y se copia en el contenedor de migración de la nube. Si el conjunto de migración es significativamente menor que el tamaño del almacén de datos, la extracción de AzCopy no es el enfoque óptimo.

* Una vez que AzCopy se haya utilizado para copiar sobre el almacén de datos, desactívelo para extracciones delta o de recarga.

## Configuración para utilizar AzCopy como paso previo a la copia {#setting-up-pre-copy-step}

AEM Siga esta sección para aprender a configurar para utilizar AzCopy como paso previo a la copia con la herramienta de transferencia de contenido para migrar el contenido a la as a Cloud Service:

### 0. Determinar el tamaño total de todo el contenido del almacén de datos {#determine-total-size}

Es importante determinar el tamaño total del almacén de datos por dos motivos:

* AEM Si la fuente de datos está configurada para utilizar el almacén de datos de archivo, el sistema local debe tener un espacio libre estrictamente bueno al tamaño 1/256 del almacén de datos de origen.

* Conocer el tamaño total del almacén de datos ayudará a estimar los tiempos de extracción e ingesta. Utilice el [Calculadora de herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=en#content-transfer) in [Cloud Acceleration Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/introduction-cam/overview-cam.html?lang=en) para obtener una estimación de los tiempos de extracción e ingesta.

#### Almacén de datos de almacenamiento de Azure Blob {#azure-blob-storage}

En la página de propiedades de contenedor del portal de Azure, utilice el **Calcular tamaño** para determinar el tamaño de todo el contenido del contenedor. Por ejemplo:

![imagen](/help/journey-migration/content-transfer-tool/assets/Azure-blob-storage-data-store.png)

#### Almacén de datos de Amazon S3 {#amazon-data}

Puede utilizar la pestaña Métricas del contenedor para determinar el tamaño de todo el contenido del contenedor. Por ejemplo:


![imagen](/help/journey-migration/content-transfer-tool/assets/amazon-s3-data-store.png)

#### Almacén de datos de archivo {#file-data-store-determine-size}

* En sistemas Mac y UNIX, ejecute el comando du en el directorio del almacén de datos para obtener su tamaño:
   `du -sh [path to datastore on the instance]`. Por ejemplo, si el almacén de datos se encuentra en `/mnt/author/crx-quickstart/repository/datastore`, el siguiente comando le proporcionará su tamaño: `du -sh /mnt/author/crx-quickstart/repository/datastore`.

* Para Windows, utilice el comando dir del directorio del almacén de datos para obtener su tamaño:
   `dir /a/s [location of datastore]`.

### 1. Instalar AzCopy {#install-azcopy}

[AzCopy](https://docs.microsoft.com/es-es/azure/storage/common/storage-use-azcopy-v10) es una herramienta de línea de comandos proporcionada por Microsoft que debe estar disponible en la instancia de origen para habilitar esta función.

En resumen, lo más probable es que quiera descargar el binario de Linux x86-64 desde el [Página de documentos de AzCopy](https://docs.microsoft.com/es-es/azure/storage/common/storage-use-azcopy-v10) y deshágalo en una ubicación como /usr/bin.

>[!IMPORTANT]
>Anote dónde colocó el binario, ya que necesitará la ruta completa para acceder a él en un paso posterior.

### 2. Instale una versión de herramienta de transferencia de contenido (CTT) compatible con AzCopy {#install-ctt-azcopy-support}

La compatibilidad con AzCopy para Amazon S3 y Azure Blob Storage se incluye en la versión CTT 1.5.4.
La compatibilidad con el almacén de datos de archivos está incluida en la versión CTT 1.7.2. Puede descargar la última versión de CTT desde el [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-es/aemcloud.html) portal.


### 3. Configurar un archivo azcopy.config {#configure-azcopy-config-file}

AEM En la instancia de origen de la, en `crx-quickstart/cloud-migration`, cree un nuevo archivo llamado `azcopy.config`.

>[!NOTE]
>AEM El contenido de este archivo de configuración será diferente en función de si la instancia de origen de la aplicación utiliza un almacén de datos de Azure o Amazon S3 o un almacén de datos de archivo.

#### Almacén de datos de almacenamiento de Azure Blob {#azure-blob-storage-data}

El archivo azcopy.config debe incluir las siguientes propiedades (asegúrese de utilizar azCopyPath y azureSas correctos para su instancia).

>[!NOTE]
>
> Si no desea conceder acceso de escritura al contenedor de almacenamiento del blob, puede generar un nuevo URI de SAS que solo tenga permisos de lectura y lista.

```
azCopyPath=/usr/bin/azcopy
azureSas=https://example-resource.blob.core.windows.net/example-container?sig=--REDACTED--
```

#### Almacén de datos de Amazon S3 {#amazon-sdata-store}

El archivo azcopy.config debe incluir las siguientes propiedades (asegúrese de utilizar los valores correctos para su instancia).

>[!NOTE]
>
> AEM Si la instancia utiliza funciones IAM para permitir a los usuarios acceder a S3, deberá crear una política y un usuario con las acciones ListBucket y GetObject habilitadas para el bloque S3. Una vez configurada, utilice la clave de acceso y la clave secreta de este usuario.

```
azCopyPath=/usr/bin/azcopy
s3Bucket=aem-63
s3Region=us-west-2
s3AccessKey=--REDACTED--
s3SecretKey=--REDACTED--
```

#### Almacén de datos de archivo {#file-data-store-azcopy-config}

Su `azcopy.config` el archivo debe contener la propiedad azcopyPath y una propiedad repository.home opcional que señale a la ubicación del almacén de datos del archivo. Utilice los valores correctos para su instancia.
Almacén de datos de archivo

```
azCopyPath=/usr/bin/azcopy
repository.home=/mnt/crx/author/crx-quickstart/repository/datastore
```

AEM La propiedad azcopyPath debe contener la ruta de acceso completa de la ubicación en la que está instalada la herramienta de línea de comandos azCopy en la instancia de origen de la. Si falta la propiedad azCopyPath, no se realizará el paso de precopia del blob.

If `repository.home` falta la propiedad en azcopy.config y, a continuación, la ubicación predeterminada del almacén de datos `/mnt/crx/author/crx-quickstart/repository/datastore` para realizar la precopia.

### 4. Extracción con AzCopy {#extracting-azcopy}

Con el archivo de configuración anterior en su lugar, la fase de precopia de AzCopy se ejecutará como parte de cada extracción posterior. Para evitar que se ejecute, puede cambiar el nombre de este archivo o quitarlo.

>[!NOTE]
>Si AzCopy no está configurado correctamente, verá este mensaje en los registros:
>`INFO c.a.g.s.m.c.a.AzCopyCloudBlobPreCopy - Blob pre-copy is not supported`.

1. Inicie una extracción desde la interfaz de usuario de CTT. Consulte [Introducción a la herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) y el [Proceso de extracción](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/extracting-content.html?lang=es) para obtener más información.

1. Confirme que la línea siguiente se imprime en el registro de extracción:

```
c.a.g.s.m.commons.ContentExtractor - *************** Beginning AzCopy Pre-Copy phase ***************
```

Felicitaciones. Esta entrada de registro significa que la configuración se consideró válida y que AzCopy está copiando actualmente todos los blobs del contenedor de origen al contenedor de migración.

Las entradas de registro de AzCopy aparecerán en el registro de extracción y se añadirán como prefijo c.a.g.s.m.c.azcopy.AzCopyBlobPreCopy - [Copia previa de AzCopy]

>[!CAUTION]
>
> Durante los primeros minutos de una extracción, observe atentamente los registros de extracción para detectar cualquier signo de problema. Por ejemplo, esto es lo que se registraría si no se encontrara el contenedor de origen de Azure:

```
[AzCopy pre-copy] failed to perform copy command due to error: cannot start job due to error: cannot list files due to reason -> github.com/Azure/azure-storage-blob-go/azblob.newStorageError, github.com/Azure/azure-storage-blob-go@v0.10.1-0.20210407023846-16cf969ec1c3/azblob/zc_storage_error.go:42
[AzCopy pre-copy] ===== RESPONSE ERROR (ServiceCode=ContainerNotFound) =====
[AzCopy pre-copy] Description=The specified container does not exist.
[AzCopy pre-copy] RequestId:5fb674b9-201e-001b-2a5b-527400000000
[AzCopy pre-copy] Time:2021-05-26T18:18:07.5931967Z, Details: 
[AzCopy pre-copy] Code: ContainerNotFound
```

En caso de que se produzca un problema con AzCopy, la extracción fallará inmediatamente y los registros de extracción contendrán detalles sobre el error.

AzCopy omitirá automáticamente todos los blobs que se hayan copiado antes del error en ejecuciones posteriores y no tendrán que copiarse de nuevo.

#### Para el almacén de datos de archivos {#file-data-store-extract}

Cuando se ejecuta AzCopy para el almacén de datos del archivo de origen, debe ver mensajes como estos en los registros que indican que se están procesando las carpetas:
`c.a.g.s.m.c.a.AzCopyFileSourceBlobPreCopy - [AzCopy pre-copy] Processing folder (1/24) crx-quickstart/repository/datastore/5d`

### 5. Ingesta con AzCopy {#ingesting-azcopy}

Con el lanzamiento de la herramienta de transferencia de contenido 1.5.4, añadimos la compatibilidad con AzCopy a la ingesta de autores.

>[!NOTE]
>La recomendación es ejecutar la ingesta de autor primero solo. Esto acelera la ingesta de Publish cuando se ejecute más adelante.

AEM Para aprovechar AzCopy durante la ingesta, es necesario que tenga una versión as a Cloud Service de AzCopy que sea al menos 2021.6.5561.

Inicie la ingesta de autor desde la interfaz de usuario de CTT. Consulte la [Proceso de ingesta](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/ingesting-content.html?lang=es) para obtener más información.
Las entradas de registro de AzCopy aparecerán en el registro de ingesta. Tendrán un aspecto similar al siguiente:

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

## Desactivación de AzCopy {#disable-azcopy}

Para deshabilitar AzCopy, cambie el nombre del archivo o elimínelo `azcopy.config` archivo.

Por ejemplo, la extracción de azcopy se puede deshabilitar con: `mv /mnt/crx/author/crx-quickstart/cloud-migration/azcopy.config /mnt/crx/author/crx-quickstart/cloud-migration/noazcopy.config`.

## Siguientes pasos {#whats-next}

AEM Una vez que haya aprendido a gestionar repositorios de contenido grandes para acelerar significativamente las fases de extracción e ingesta de la actividad de transferencia de contenido y mover contenido a los as a Cloud Service, ya puede aprender el proceso de extracción en la herramienta de transferencia de contenido. Consulte [Extracción de contenido del origen en la herramienta de transferencia de contenido](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md) para obtener información sobre cómo extraer el conjunto de migración de la herramienta de transferencia de contenido.
