---
title: Gestión de repositorios de contenido grandes
description: En esta sección se describe la administración de repositorios de contenido grandes
exl-id: 21bada73-07f3-4743-aae6-2e37565ebe08
feature: Migration
role: Admin
source-git-commit: b729c07c78519cd9b6536a0dd142aa8ed01d2a22
workflow-type: tm+mt
source-wordcount: '1842'
ht-degree: 7%

---

# Gestión de repositorios de contenido grandes {#handling-large-content-repositories}

## Información general {#overview}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_precopy"
>title="Gestión de repositorios de contenido grandes"
>abstract="Para acelerar de forma significativa las fases de extracción e ingesta de la actividad de transferencia de contenido y mover el contenido a AEM as a Cloud Service, la Herramienta de Transferencia de Contenido (CTT, por sus siglas en inglés), puede aprovechar AzCopy como paso previo opcional a la copia. Una vez configurado este paso previo, en la fase de extracción, AzCopy copia los blobs de Amazon S3 o Azure Blob Storage en el almacén de blobs del conjunto de migración. En la fase de ingesta, AzCopy copia los blobs del almacén de blobs del conjunto de migración al almacén de blobs de destino de AEM as a Cloud Service."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=es#setting-up-pre-copy-step" text="Introducción a AzCopy como paso previo a la copia"

Copiar muchos blobs con la herramienta de transferencia de contenido (CTT) puede tardar varios días.
Para acelerar las fases de extracción e ingesta de la actividad de transferencia de contenido y mover contenido a AEM as a Cloud Service, CTT puede usar [AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) como un paso previo a la copia opcional. Este paso previo a la copia se puede utilizar cuando la instancia de AEM de origen está configurada para utilizar un almacén de datos de Amazon S3, Azure Blob Storage o File Data Store. El paso previo a la copia es más eficaz para la primera extracción e ingesta completas. Sin embargo, no se recomienda utilizar la copia previa para recargas posteriores (si el tamaño de la recarga es inferior a 200 GB), ya que puede añadir tiempo a todo el proceso. Una vez configurado este paso previo, en la fase de extracción, AzCopy copia blobs de Amazon S3, Azure Blob Storage o el almacén de datos de archivo al almacén de blobs del conjunto de migración. En la fase de ingesta, AzCopy copia los blobs del almacén de blobs del conjunto de migración al almacén de blobs de destino de AEM as a Cloud Service.

## Consideraciones importantes antes de comenzar {#important-considerations}

En la sección siguiente se comprenden las consideraciones importantes antes de comenzar:

* A partir de la versión 2.0.16 de CTT, la configuración de precopia se realiza automáticamente cuando se instala el paquete. Además, si el tamaño del conjunto de migración es mayor de 200 GB, el proceso de extracción utiliza automáticamente la función de precopia. El archivo azcopy.config se crea en el directorio crx-quickstart/cloud-migration/. No es necesario que realice manualmente la configuración de precopia si utiliza la versión 2.0.16 o posterior de CTT.

* La versión de Source AEM debe ser 6.3 - 6.5.

* El almacén de datos de Source AEM está configurado para utilizar Amazon S3 o Azure Blob Storage. Para obtener más información, consulte [Configuración de almacenes de nodos y almacenes de datos en AEM 6](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html).

* Cada conjunto de migración copia todo el almacén de datos, por lo que solo se debe utilizar un conjunto de migración único.

* Necesita acceso para instalar [AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) en la instancia (o VM) que ejecuta la instancia de origen de AEM.

* La recolección de elementos no utilizados del almacén de datos se ha ejecutado en los siete días anteriores en el origen. Para obtener más información, consulte [Recopilación de residuos del almacén de datos](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html#data-store-garbage-collection).

### Consideraciones adicionales si la instancia de AEM de origen está configurada para utilizar un almacén de datos de almacenamiento de Amazon S3 o Azure Blob {#additional-considerations-amazons3-azure}

* La transferencia de datos desde Amazon S3 y Azure Blob Storage conlleva un coste. El coste de la transferencia es relativo a la cantidad total de datos del contenedor de almacenamiento existente (independientemente de si se hace referencia en AEM o no). Consulte [Amazon S3](https://aws.amazon.com/s3/pricing/) y [Azure Blob Storage](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) para obtener más información.

* Necesita un par de clave de acceso y clave secreta para el bloque de Amazon S3 de origen existente o un URI SAS para el contenedor de almacenamiento de Azure Blob de origen existente (el acceso de solo lectura está bien).

### Consideraciones adicionales si la instancia de origen de AEM está configurada para utilizar el almacén de datos de archivos {#additional-considerations-aem-instance-filedatastore}

* El sistema local debe tener un espacio libre estrictamente superior a 1/256 del almacén de datos de origen. Por ejemplo, si el tamaño del almacén de datos es de 3 terabytes, debe existir espacio libre superior a 11,72 GB en la carpeta `crx-quickstart/cloud-migration` del origen para que funcione AzCopy. Como mínimo, el sistema de origen debe tener 1 GB de espacio libre. Se puede obtener espacio libre utilizando el comando `df -h` en instancias de Linux® y el comando dir en instancias de Windows.

* Cada vez que se ejecuta la extracción con AzCopy habilitado, todo el almacén de datos de archivos se aplana y se copia en el contenedor de migración de la nube. Si el conjunto de migración es menor que el tamaño del almacén de datos, la extracción de AzCopy no es el enfoque óptimo.

* Una vez que AzCopy se haya utilizado para copiar sobre el almacén de datos existente, deshabilite para extracciones delta o de recarga.

## Configuración para utilizar AzCopy como paso previo a la copia {#setting-up-pre-copy-step}

>[!NOTE]
>A partir de la versión 2.0.16 de CTT, la configuración de precopia se realiza automáticamente cuando se instala el paquete. Además, si el tamaño del conjunto de migración es mayor de 200 GB, el proceso de extracción utiliza automáticamente la función de precopia. El archivo azcopy.config se crea en el directorio crx-quickstart/cloud-migration/. Si desea actualizar la configuración del archivo manualmente, revise las secciones a continuación.

Siga esta sección para aprender a configurar para utilizar AzCopy como paso previo a la copia con la herramienta de transferencia de contenido para migrar el contenido a AEM as a Cloud Service:

### &#x200B;0. Determinar el tamaño total de todo el contenido del almacén de datos {#determine-total-size}

Es importante determinar el tamaño total del almacén de datos por dos motivos:

* Si AEM de origen está configurado para utilizar el almacén de datos de archivo, el sistema local debe tener un espacio libre estrictamente superior al tamaño 1/256 del almacén de datos de origen.

#### Almacén de datos de almacenamiento de Azure Blob {#azure-blob-storage}

Desde la página de propiedades de contenedor existente en el portal de Azure, utilice el botón **Calcular tamaño** para determinar el tamaño de todo el contenido del contenedor. Por ejemplo:

![imagen](/help/journey-migration/content-transfer-tool/assets/Azure-blob-storage-data-store.png)

#### Almacén de datos de Amazon S3 {#amazon-data}

Puede utilizar la pestaña Métricas del contenedor para determinar el tamaño de todo el contenido del contenedor. Por ejemplo:


![imagen](/help/journey-migration/content-transfer-tool/assets/amazon-s3-data-store.png)

#### Almacén de datos de archivo {#file-data-store-determine-size}

* En sistemas Mac y UNIX®, ejecute el comando du en el directorio del almacén de datos para obtener su tamaño:
  `du -sh [path to datastore on the instance]`. Por ejemplo, si el almacén de datos está en `/mnt/author/crx-quickstart/repository/datastore`, el siguiente comando le dará su tamaño: `du -sh /mnt/author/crx-quickstart/repository/datastore`.

* Para Windows, utilice el comando dir del directorio del almacén de datos para obtener su tamaño:
  `dir /a/s [location of datastore]`.

### &#x200B;1. Instalar AzCopy {#install-azcopy}

[AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) es una herramienta de línea de comandos proporcionada por Microsoft® que debe estar disponible en la instancia de origen para habilitar esta característica.

En resumen, desea descargar el binario Linux® x86-64 desde la [página de documentos de AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) y descomprimirlo en una ubicación como /usr/bin.

>[!IMPORTANT]
>Anote dónde colocó el binario, ya que necesita la ruta completa para acceder a él en un paso posterior.

### &#x200B;2. Instale la versión de la herramienta de transferencia de contenido (CTT) con compatibilidad con AzCopy {#install-ctt-azcopy-support}

>[!IMPORTANT]
>Debe usarse la versión más reciente de CTT.

La compatibilidad con AzCopy para Amazon S3, Azure Blob Storage y File Data Store se incluye en la última versión de CTT.
Puede descargar la última versión de CTT desde el portal [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).
Debe tenerse en cuenta que solo se admiten las versiones 2.0.0 y posteriores, y es aconsejable utilizar la versión más reciente.

### &#x200B;3. Configurar un archivo azcopy.config {#configure-azcopy-config-file}

En la instancia de AEM de origen, en `crx-quickstart/cloud-migration`, cree un archivo denominado `azcopy.config`.

>[!NOTE]
>El contenido de este archivo de configuración es diferente en función de si la instancia de AEM de origen utiliza un almacén de datos de Azure o Amazon S3 o un almacén de datos de archivo.

#### Almacén de datos de almacenamiento de Azure Blob {#azure-blob-storage-data}

El archivo azcopy.config debe incluir las siguientes propiedades (asegúrese de utilizar azCopyPath y azureSas correctos para su instancia).

>[!NOTE]
>
> Si no desea conceder acceso de escritura al contenedor de almacenamiento del blob existente, puede generar un nuevo URI de SAS que solo tenga permisos de lectura y lista.

```
azCopyPath=/usr/bin/azcopy
azureSas=https://example-resource.blob.core.windows.net/example-container?sig=--REDACTED--
```

#### Almacén de datos de Amazon S3 {#amazon-sdata-store}

El archivo azcopy.config debe incluir las siguientes propiedades (asegúrese de utilizar los valores correctos para su instancia).

>[!NOTE]
>
> Si la instancia utiliza funciones IAM para permitir que AEM acceda a S3, debe crear una directiva y un usuario con las acciones ListBucket y GetObject habilitadas para el bloque S3. Una vez configurada, utilice la clave de acceso y la clave secreta de este usuario.

```
azCopyPath=/usr/bin/azcopy
s3Bucket=aem-63
s3Region=us-west-2
s3AccessKey=--REDACTED--
s3SecretKey=--REDACTED--
```

#### Almacén de datos de archivo {#file-data-store-azcopy-config}

El archivo `azcopy.config` debe contener la propiedad azCopyPath y una propiedad repository.home opcional que señale a la ubicación del almacén de datos del archivo. Utilice los valores correctos para su instancia.
Almacén de datos de archivo

```
azCopyPath=/usr/bin/azcopy
repository.home=/mnt/crx/author/crx-quickstart/repository/datastore
```

La propiedad azCopyPath debe contener la ruta de acceso completa de la ubicación donde está instalada la herramienta de línea de comandos azCopy en la instancia de origen de AEM. Si falta la propiedad azCopyPath, no se realiza el paso de precopia del blob.

Si falta la propiedad `repository.home` en azcopy.config, se usa la ubicación predeterminada del almacén de datos `/mnt/crx/author/crx-quickstart/repository/datastore` para realizar la precopia.

### &#x200B;4. Extracción con AzCopy {#extracting-azcopy}

Con el archivo de configuración anterior en su lugar, la fase de precopia de AzCopy se ejecuta como parte de cada extracción posterior. Para evitar que se ejecute, puede cambiar el nombre de este archivo o quitarlo.

>[!NOTE]
>Si AzCopy no está configurado correctamente, verá el siguiente mensaje en los registros:
>&#x200B;>`INFO c.a.g.s.m.c.a.AzCopyCloudBlobPreCopy - Blob pre-copy is not supported`.

1. Inicie una extracción desde la interfaz de usuario de CTT. Consulte [Introducción a la herramienta de transferencia de contenido](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md) y el [proceso de extracción](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md) para obtener más información.

1. Confirme que la línea siguiente está impresa en el registro de extracción:

```
c.a.g.s.m.commons.ContentExtractor - *************** Beginning AzCopy Pre-Copy phase ***************
```

¡Enhorabuena! Esta entrada de registro significa que la configuración se consideró válida y que AzCopy está copiando todos los blobs del contenedor de origen al contenedor de migración.

Las entradas de registro de AzCopy aparecen en el registro de extracción y llevan el prefijo c.a.g.s.m.c.azcopy.AzCopyBlobPreCopy - [Copia previa de AzCopy]

>[!CAUTION]
>
> Durante los primeros minutos de una extracción, observe atentamente los registros de extracción para detectar cualquier signo de problema. Por ejemplo, esto es lo que se registraría si no se encontrara el contenedor de origen de Azure:

```
[AzCopy pre-copy] failed to perform copy command due to error: cannot start job due to error: cannot list files due to reason > github.com/Azure/azure-storage-blob-go/azblob.newStorageError, github.com/Azure/azure-storage-blob-go@v0.10.1-0.20210407023846-16cf969ec1c3/azblob/zc_storage_error.go:42
[AzCopy pre-copy] ===== RESPONSE ERROR (ServiceCode=ContainerNotFound) =====
[AzCopy pre-copy] Description=The specified container does not exist.
[AzCopy pre-copy] RequestId:5fb674b9-201e-001b-2a5b-527400000000
[AzCopy pre-copy] Time:2021-05-26T18:18:07.5931967Z, Details: 
[AzCopy pre-copy] Code: ContainerNotFound
```

Si hay un problema con AzCopy, la extracción falla inmediatamente y los registros de extracción contienen detalles sobre el error.

AzCopy omite automáticamente los blobs copiados antes del error en ejecuciones posteriores y no es necesario copiarlos de nuevo.

>[!TIP]
>Ahora se puede programar una ingesta para que se inicie automáticamente inmediatamente después de que una extracción se realice correctamente. Consulte [Ingesta de contenido en Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) para obtener más información.

>[!TIP]
>Si la transferencia de blob con AzCopy progresó durante un tiempo pero luego falló solo para algunos blobs, vuelva a ejecutar la extracción con las opciones Precopiar y Sobrescribir contenedor de ensayo desmarcadas. Esto migrará solo los blobs restantes que no se transfirieron anteriormente.

#### Para el almacén de datos de archivos {#file-data-store-extract}

Cuando se ejecuta AzCopy para el almacén de datos del archivo de origen, debe ver mensajes como estos en los registros que indican que se están procesando las carpetas:
`c.a.g.s.m.c.a.AzCopyFileSourceBlobPreCopy - [AzCopy pre-copy] Processing folder (1/24) crx-quickstart/repository/datastore/5d`

### &#x200B;5. Ingesta con AzCopy {#ingesting-azcopy}

Consulte [Ingesta de contenido en Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) para obtener información general sobre la ingesta de contenido en el destino desde Cloud Acceleration Manager (CAM), incluidas instrucciones sobre cómo usar AzCopy (copia previa) o no en el cuadro de diálogo &quot;Nueva ingesta&quot;.

Para aprovechar AzCopy durante la ingesta, Adobe requiere que esté en una versión de AEM as a Cloud Service que sea al menos la 2021.6.5561.

Consulte la lista &quot;Trabajos de ingesta&quot; en Cloud Acceleration Manager y los registros de ingesta para poder ver el progreso. Las entradas de registro relacionadas con la variable
Las tareas de AzCopy correctas aparecen de la siguiente manera (lo que permite algunas diferencias). Comprobar los registros ocasionalmente podría alertarle sobre problemas
al principio, y le ayudará a encontrar una solución rápida a cualquier problema.

```
*************** Beginning AzCopy pre-copy phase ***************
INFO: Scanning...
INFO: Failed to create one or more destination container(s). Your transfers may still succeed if the container already exists.
INFO: Any empty folders will not be processed, because source and/or destination does not have full folder support
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

Ya ha aprendido a gestionar repositorios de contenido grandes para acelerar las fases de extracción e ingesta de la actividad de transferencia de contenido y mover contenido a AEM as a Cloud Service. Ya está listo para aprender el proceso de extracción con la herramienta de transferencia de contenido. Consulte [Extracción de contenido de Source en la herramienta de transferencia de contenido](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md) para que pueda aprender a extraer el conjunto de migración de la herramienta de transferencia de contenido.
