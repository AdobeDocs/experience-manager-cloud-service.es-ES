---
title: 'API de recursos para la administración de recursos digitales en Adobe Experience Manager como servicio de nube '
description: Las API de recursos permiten operaciones básicas de creación, lectura, actualización y eliminación (CRUD) para administrar recursos, incluidos binarios, metadatos, representaciones, comentarios y fragmentos de contenido.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Assets as a Cloud Service APIs {#assets-cloud-service-apis}

<!-- 
Give a list of and overview of all reference information available.
* New upload method
* Javadocs
* Assets HTTP API documented at [https://helpx.adobe.com/experience-manager/6-5/assets/using/mac-api-assets.html](https://helpx.adobe.com/experience-manager/6-5/assets/using/mac-api-assets.html)

-->

## Carga de recursos {#asset-upload-technical}

Experience Manager como servicio en la nube ofrece una nueva forma de cargar recursos en el repositorio: carga binaria directa en el almacenamiento de nube binario. En esta sección se ofrece una descripción general técnica.

### Descripción general de la carga binaria directa {#overview-binary-upload}

El algoritmo de alto nivel para cargar un binario es:

1. Envíe una solicitud HTTP informando a AEM de la intención de cargar un nuevo binario.
1. Publique el contenido del binario en uno o más URI proporcionados por la solicitud de inicio.
1. Envíe una solicitud HTTP para informar al servidor de que el contenido del binario se cargó correctamente.

![Descripción general del protocolo de carga binaria directa](assets/add-assets-technical.png)

Las diferencias importantes en comparación con versiones anteriores de AEM incluyen:

* Los binarios no pasan por AEM, que ahora simplemente está coordinando el proceso de carga con el almacenamiento de nube binario configurado para la implementación
* El almacenamiento de nube binaria está precedido por una red de Envío de contenido (CDN, Red perimetral), que acerca el punto final de carga al cliente, lo que ayuda a mejorar el rendimiento de carga y la experiencia del usuario, especialmente para los equipos distribuidos que cargan recursos

Este método debería proporcionar una gestión más escalable y eficaz de las cargas de recursos.

> !![NOTE]
Para revisar el código de cliente que implementa este método, consulte la biblioteca de carga de [correo electrónico de código abierto](https://github.com/adobe/aem-upload)

### Iniciar carga {#initiate-upload}

El primer paso es enviar una solicitud HTTP POST a la carpeta en la que se debe crear o actualizar el recurso; incluya el selector `.initiateUpload.json` para indicar que la solicitud debe comenzar una carga binaria. Por ejemplo, la ruta a la carpeta en la que se debe crear el recurso es `/assets/folder`:

```
POST https://[aem_server]/content/dam/assets/folder.initiateUpload.json
````

El tipo de contenido del cuerpo de la solicitud deben ser datos `application/x-www-form-urlencoded` de formulario, que contengan los campos siguientes:

* `(string) fileName`: Requerido. Nombre del recurso tal como aparecerá en la instancia.
* `(number) fileSize`: Requerido. Longitud total, en bytes, del binario que se va a cargar.

Tenga en cuenta que se puede utilizar una sola solicitud para iniciar cargas para varios binarios, siempre y cuando cada binario contenga los campos obligatorios.

Si se realiza correctamente, la solicitud responderá con un código de estado de 201 y un cuerpo que contenga datos JSON en el siguiente formato:

```
{
    "completeURI": "(string)",
    "folderPath": (string)",
    "files": [
        {
            "fileName": "(string)",
            "mimeType": "(string)",
            "uploadToken": "(string)",
            "uploadURIs": [
                "(string)"
            ]
        }
    ]
}
````

* `(string) completeURI`:: URI que debe invocarse cuando el binario ha terminado de cargarse. Podría ser un URI absoluto o relativo, y los clientes deberían poder gestionar cualquiera de ellos. es decir, el valor puede ser `"https://author.acme.com/content/dam.completeUpload.json"` o `"/content/dam.completeUpload.json"` (consulte Carga [](#complete-upload)completa).
* `(string) folderPath`:: Ruta de acceso completa a la carpeta en la que se está cargando el binario.
* `(array) (files)`:: Una lista de elementos cuya longitud y orden coincidirán con la longitud y el orden de la lista de información binaria proporcionada en la solicitud de inicio.
* `(string) fileName`:: El nombre del binario correspondiente, tal como se indica en la solicitud de inicio. Este valor debe incluirse en la solicitud completa.
* `(string) mimeType`:: El tipo mime del binario correspondiente, tal como se proporciona en la solicitud de inicio in. Este valor debe incluirse en la solicitud completa.
* `(string) uploadToken`:: Un distintivo de carga para el binario correspondiente. Este valor debe incluirse en la solicitud completa.
* `(array) uploadURIs`:: Una lista de cadenas cuyos valores son URIs completos a las que se debe cargar el contenido del binario (consulte [Cargar binario](#upload-binary)).
* `(number) minPartSize`:: Longitud mínima, en bytes, de los datos que se pueden proporcionar a cualquiera de los URIs de carga, si hay más de un URI.
* `(number) maxPartSize`:: Longitud máxima, en bytes, de los datos que se pueden proporcionar a cualquiera de los URIs de carga, si hay más de un URI.

### Cargar binario {#upload-binary}

El resultado del inicio de una carga incluirá uno o varios valores de URI de carga. Si se proporciona más de un URI, es responsabilidad del cliente &quot;dividir&quot; el binario en partes y POST cada parte, en orden, a cada URI, en orden. Se deben utilizar todos los URI y cada parte debe ser mayor que el tamaño mínimo y menor que el tamaño máximo especificado en la respuesta de inicio. Estas solicitudes serán enviadas por nodos perimetrales CDN para acelerar la carga de binarios.

Una forma posible de lograrlo es calcular el tamaño de la pieza en función del número de URI de carga proporcionados por la API. Ejemplo suponiendo que el tamaño total del binario es de 20.000 bytes y el número de URI de carga es de 2:

* Calcule el tamaño de la pieza dividiendo el tamaño total por el número de URI: 20.000 / 2 = 10.000
* Intervalo de bytes POST 0-9,999 del binario al primer URI en la lista de URI de carga
* Intervalo de bytes POST 10.000-19.999 del binario al segundo URI en la lista de URI de carga

Si se realiza correctamente, el servidor responde a cada solicitud con un código `201` de estado.

### Carga completa {#complete-upload}

Una vez cargadas todas las partes de un binario, el paso final es enviar una solicitud HTTP POST al URI completo proporcionado por los datos de inicio. El tipo de contenido del cuerpo de la solicitud debe ser datos de aplicación/`x-www-form-urlencoded` formulario que contengan los siguientes campos:

* `(string) fileName`: Requerido. El nombre del recurso, tal y como lo proporcionaron los datos de inicio.
* `(string) mimeType`: Requerido. El tipo de contenido HTTP del binario, tal como se proporcionó con los datos de inicio.
* `(string) uploadToken`: Requerido. Distintivo de carga para el binario, tal y como proporcionaban los datos de inicio.
* `(bool) createVersion`: Opcional. Si el valor es true y ya existe un recurso con el nombre especificado, la instancia creará una nueva versión del recurso.
* `(string) versionLabel`: Opcional. Si se crea una nueva versión, la etiqueta que se asociará a la versión.
* `(string) versionComment`: Opcional. Si se crea una nueva versión, los comentarios que se asociarán a la versión.
* `(bool) replace`:: Opcional: Si el valor es true y ya existe un recurso con el nombre especificado, la instancia eliminará el recurso y lo volverá a crear.

>!![NOTE]
>
> Si el recurso ya existe y no se especifica createVersion ni replace, la instancia actualizará la versión actual del recurso con el nuevo binario.

Al igual que el proceso de inicio, los datos completos de la solicitud pueden contener información para más de un archivo.

El proceso de carga de un binario no se realiza hasta que se invoque la dirección URL completa para el archivo. Aunque el binario de un archivo se cargue en su totalidad, la instancia no procesará el recurso hasta que se complete el proceso de carga.

Si se realiza correctamente, el servidor responde con un código `200` de estado.

### Biblioteca de carga de código abierto {#open-source-upload-library}

Para obtener más información sobre los algoritmos de carga o para crear sus propias herramientas y secuencias de comandos de carga, Adobe proporciona herramientas y bibliotecas de código abierto como punto de partida:

* [Abrir biblioteca de carga de aem de origen](https://github.com/adobe/aem-upload)
* [Herramienta de línea de comandos de código abierto](https://github.com/adobe/aio-cli-plugin-aem)

### API de carga de recursos obsoletas {#deprecated-asset-upload-api}

<!-- #ENGCHECK please review / update the list of deprecated APIs below -->

>[!NOTE]
Para Experience Manager como servicio de nube, solo se admiten las nuevas API de carga. Las API de Experience Manager 6.5 están en desuso.

Los métodos relacionados con la carga o actualización de recursos o representaciones (cualquier carga binaria) están en desuso en las siguientes API:

* [API HTTP de AEM Assets](mac-api-assets.md)
* `AssetManager` API de Java, como `AssetManager.createAsset(..)`

>[!MORELIKETHIS]
* [Abrir biblioteca de carga de aem de origen](https://github.com/adobe/aem-upload)
* [Herramienta de línea de comandos de código abierto](https://github.com/adobe/aio-cli-plugin-aem)


## flujos de trabajo de procesamiento y postprocesamiento de recursos {#post-processing-workflows}

La mayor parte del procesamiento de recursos se ejecuta en función de la configuración **[!UICONTROL de Perfiles]** de procesamiento mediante [los microservicios](asset-microservices-configure-and-use.md#get-started-using-asset-microservices)de recursos y no requiere extensiones de desarrollador.

Para la configuración del flujo de trabajo posterior al procesamiento, se pueden utilizar Flujos de trabajo de AEM estándar con extensiones (por ejemplo, se pueden usar pasos personalizados). Revise la subsección siguiente para comprender qué pasos del flujo de trabajo se pueden utilizar en los flujos de trabajo de postprocesamiento de recursos.

### Pasos del flujo de trabajo en el flujo de trabajo posterior al procesamiento {#post-processing-workflows-steps}

>[!NOTE]
Esta sección se aplica principalmente a los clientes que actualizan a AEM como servicio de nube desde versiones anteriores de AEM.

Debido a un nuevo modelo de implementación introducido con Experience Manager como servicio de nube, es posible que algunos pasos de flujo de trabajo utilizados en el flujo de trabajo antes de la introducción de los `DAM Update Asset` microservicios de recursos ya no sean compatibles con los flujos de trabajo posteriores al procesamiento. Tenga en cuenta que la mayoría de ellos son reemplazados por un método mucho más sencillo de configurar y utilizar los microservicios de recursos.

A continuación se muestra una lista de los modelos técnicos de flujo de trabajo y su nivel de asistencia en AEM como servicio de nube:

### Pasos de flujo de trabajo admitidos {#supported-workflow-steps}

Los siguientes pasos del flujo de trabajo son compatibles con el servicio de nube.

* `com.day.cq.dam.similaritysearch.internal.workflow.process.AutoTagAssetProcess`
* `com.day.cq.dam.core.impl.process.CreateAssetLanguageCopyProcess`
* `com.day.cq.wcm.workflow.process.CreateVersionProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.core.impl.process.TranslateAssetLanguageCopyProcess`
* `com.day.cq.dam.core.impl.process.UpdateAssetLanguageCopyProcess`
* `com.adobe.cq.workflow.replication.impl.ReplicationWorkflowProcess`
* `com.day.cq.dam.core.impl.process.DamUpdateAssetWorkflowCompletedProcess`

### Modelos no admitidos o reemplazados {#unsupported-replaced-models}

Los siguientes modelos técnicos de flujo de trabajo se sustituyen por microservicios de recursos o no se admite.

* `com.day.cq.dam.core.impl.process.DamMetadataWritebackWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
* `com.day.cq.dam.core.process.XMPWritebackProcess`
* `com.adobe.cq.dam.dm.process.workflow.DMImageProcess`
* `com.day.cq.dam.s7dam.common.process.S7VideoThumbnailProcess`
* `com.day.cq.dam.scene7.impl.process.Scene7UploadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoProxyServiceProcess`
* `com.day.cq.dam.s7dam.common.process.VideoThumbnailDownloadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoUserUploadedThumbnailProcess`
* `com.day.cq.dam.core.process.CreatePdfPreviewProcess`
* `com.day.cq.dam.core.process.CreateWebEnabledImageProcess`
* `com.day.cq.dam.video.FFMpegThumbnailProcess`
* `com.day.cq.dam.core.process.ThumbnailProcess`
* `com.day.cq.dam.cameraraw.process.CameraRawHandlingProcess`
* `com.day.cq.dam.core.process.CommandLineProcess`
* `com.day.cq.dam.pdfrasterizer.process.PdfRasterizerHandlingProcess`
* `com.day.cq.dam.core.process.AddPropertyWorkflowProcess`
* `com.day.cq.dam.core.process.CreateSubAssetsProcess`
* `com.day.cq.dam.core.process.DownloadAssetProcess`
* `com.day.cq.dam.word.process.ExtractImagesProcess`
* `com.day.cq.dam.word.process.ExtractPlainProcess`
* `com.day.cq.dam.video.FFMpegTranscodeProcess`
* `com.day.cq.dam.ids.impl.process.IDSJobProcess`
* `com.day.cq.dam.indd.process.INDDMediaExtractProcess`
* `com.day.cq.dam.indd.process.INDDPageExtractProcess`
* `com.day.cq.dam.core.impl.lightbox.LightboxUpdateAssetProcess`
* `com.day.cq.dam.pim.impl.sourcing.upload.process.ProductAssetsUploadProcess`
* `com.day.cq.dam.core.process.ScheduledPublishBPProcess`
* `com.day.cq.dam.core.process.ScheduledUnPublishBPProcess`
* `com.day.cq.dam.core.process.SendDownloadAssetEmailProcess`
* `com.day.cq.dam.core.impl.process.SendTransientWorkflowCompletedEmailProcess`

<!-- PPTX source: slide in add-assets.md - overview of direct binary upload section of 
https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->
