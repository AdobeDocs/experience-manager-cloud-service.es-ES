---
title: Referencias de desarrollador para la administración de recursos digitales [!DNL Adobe Experience Manager] como Cloud Service.
description: Las API de [!DNL Assets] y el contenido de referencia del desarrollador le permiten administrar recursos, incluidos archivos binarios, metadatos, representaciones, comentarios y [!DNL Content Fragments].
contentOwner: AG
translation-type: tm+mt
source-git-commit: cfcb9fb85cffeabc5d5af94c30bd8ace8039ac83
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 1%

---


# [!DNL Assets] API y material de referencia para desarrolladores {#assets-cloud-service-apis}

El artículo contiene material de referencia y recursos para desarrolladores de [!DNL Assets] como Cloud Service. Incluye nuevo método de carga, referencia de API e información sobre la compatibilidad proporcionada en los flujos de trabajo de postprocesamiento.

## Carga de recursos {#asset-upload-technical}

[!DNL Experience Manager] como Cloud Service proporciona un nuevo método para cargar recursos en el repositorio. Los usuarios pueden cargar directamente los recursos en el almacenamiento de la nube mediante la API HTTP. Los pasos para cargar un archivo binario son:

1. [Envíe una solicitud](#initiate-upload)HTTP. Informa [!DNL Experience Manage]o implementa su intención de cargar un nuevo binario.
1. [POST el contenido del archivo binario](#upload-binary) a uno o más URI proporcionados por la solicitud de inicio.
1. [Envíe una solicitud](#complete-upload) HTTP para informar al servidor de que el contenido del binario se cargó correctamente.

![Descripción general del protocolo de carga binaria directa](assets/add-assets-technical.png)

Este método ofrece una gestión escalable y más eficaz de las cargas de recursos. Las diferencias con respecto a [!DNL Experience Manager] 6.5 son:

* Los binarios no pasan por [!DNL Experience Manager], lo que ahora es simplemente coordinar el proceso de carga con el almacenamiento de nube binario configurado para la implementación.
* El almacenamiento de nube binaria funciona con una red de Envío de contenido (CDN) o una red de Edge. Un CDN selecciona un punto final de carga más cercano para un cliente. Cuando los datos pasan una distancia más corta a un punto final cercano, el rendimiento de carga y la experiencia del usuario mejoran, especialmente para equipos distribuidos geográficamente.

>[!NOTE]
>
>Consulte el código de cliente para implementar este método en la biblioteca [de carga de](https://github.com/adobe/aem-upload)aem de código abierto.

### Iniciar carga {#initiate-upload}

Envíe una solicitud de POST HTTP a la carpeta deseada. Los recursos se crean o actualizan en esta carpeta. Incluya el selector `.initiateUpload.json` para indicar que la solicitud es iniciar la carga de un archivo binario. Por ejemplo, la ruta a la carpeta en la que se debe crear el recurso es `/assets/folder`. La solicitud del POST es `POST https://[aem_server]:[port]/content/dam/assets/folder.initiateUpload.json`.

El tipo de contenido del cuerpo de la solicitud deben ser datos `application/x-www-form-urlencoded` de formulario, que contengan los campos siguientes:

* `(string) fileName`: Requerido. Nombre del recurso tal como aparece en [!DNL Experience Manager].
* `(number) fileSize`: Requerido. El tamaño de archivo, en bytes, del recurso que se está cargando.

Se puede utilizar una sola solicitud para iniciar cargas para varios binarios, siempre que cada binario contenga los campos obligatorios. Si se realiza correctamente, la solicitud responde con un código `201` de estado y un cuerpo que contiene datos JSON en el siguiente formato:

```json
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
```

* `completeURI` (cadena): Llame a este URI cuando termine de cargarse el binario. El URI puede ser un URI absoluto o relativo y los clientes deben poder gestionar cualquiera de los dos. Es decir, el valor puede ser `"https://author.acme.com/content/dam.completeUpload.json"` o `"/content/dam.completeUpload.json"` Ver carga [completa](#complete-upload).
* `folderPath` (cadena): Ruta de acceso completa a la carpeta en la que se carga el binario.
* `(files)` (matriz): Una lista de elementos cuya longitud y orden coinciden con la longitud y el orden de la lista de información binaria proporcionada en la solicitud de inicio.
* `fileName` (cadena): El nombre del binario correspondiente, tal como se indica en la solicitud de inicio. Este valor debe incluirse en la solicitud completa.
* `mimeType` (cadena): El tipo MIME del binario correspondiente, tal como se proporciona en la solicitud de inicio. Este valor debe incluirse en la solicitud completa.
* `uploadToken` (cadena): Un distintivo de carga para el binario correspondiente. Este valor debe incluirse en la solicitud completa.
* `uploadURIs` (matriz): Una lista de cadenas cuyos valores son URIs completos a las que se debe cargar el contenido del binario (consulte [Cargar binario](#upload-binary)).
* `minPartSize` (número): Longitud mínima, en bytes, de los datos que se pueden proporcionar a cualquiera de los URIs de carga, si hay más de un URI.
* `maxPartSize` (número): Longitud máxima, en bytes, de los datos que se pueden proporcionar a cualquiera de los URIs de carga, si hay más de un URI.

### Cargar binario {#upload-binary}

El resultado del inicio de una carga incluye uno o varios valores de URI de carga. Si se proporciona más de un URI, el cliente divide el binario en partes y realiza una solicitud POST de cada parte en cada URI, en orden. Utilice todos los URI. Asegúrese de que el tamaño de cada artículo esté dentro de los tamaños mínimo y máximo especificados en la respuesta de inicio. Los nodos perimetrales CDN ayudan a acelerar la carga solicitada de binarios.

Un método posible para lograr esto es calcular el tamaño de la pieza en función del número de URI de carga proporcionados por la API. Por ejemplo, supongamos que el tamaño total del binario es de 20.000 bytes y que el número de URI de carga es de 2. A continuación, siga estos pasos:

* Calcule el tamaño de la pieza dividiendo el tamaño total por el número de URI: 20.000 / 2 = 10.000.
* Intervalo de bytes del POST 0-9,999 del binario al primer URI en la lista de URI de carga.
* Intervalo de bytes POST 10.000 - 19.999 del binario al segundo URI en la lista de URI de carga.

Si la carga se realiza correctamente, el servidor responde a cada solicitud con un código `201` de estado.

### Carga completa {#complete-upload}

Una vez cargadas todas las partes de un archivo binario, envíe una solicitud de POST HTTP al URI completo proporcionado por los datos de inicio. El tipo de contenido del cuerpo de la solicitud debe ser datos `application/x-www-form-urlencoded` de formulario, que contengan los campos siguientes.

| Fields | Tipo | Obligatorio o no | Descripción |
|---|---|---|---|
| `fileName` | Cadena | Requerido | El nombre del recurso, tal y como lo proporcionaron los datos de inicio. |
| `mimeType` | Cadena | Requerido | El tipo de contenido HTTP del binario, tal como se proporcionó con los datos de inicio. |
| `uploadToken` | Cadena | Requerido | Distintivo de carga para el binario, tal y como proporcionaban los datos de inicio. |
| `createVersion` | Booleano | Opcional | Si `True` y existe un recurso con el nombre especificado, [!DNL Experience Manager] crea una nueva versión del recurso. |
| `versionLabel` | Cadena | Opcional | Si se crea una nueva versión, la etiqueta asociada con la nueva versión de un recurso. |
| `versionComment` | Cadena | Opcional | Si se crea una nueva versión, los comentarios asociados a ella. |
| `replace` | Booleano | Opcional | Si `True` y existe un recurso con el nombre especificado, [!DNL Experience Manager] elimina el recurso y vuelve a crearlo. |

>!![NOTE]
Si el recurso existe `createVersion` y no `replace` se especifica, [!DNL Experience Manager] actualiza la versión actual del recurso con el nuevo binario.

Al igual que el proceso de inicio, los datos completos de la solicitud pueden contener información para más de un archivo.

El proceso de carga de un binario no se realiza hasta que se invoque la dirección URL completa para el archivo. Un recurso se procesa una vez finalizado el proceso de carga. El procesamiento no tiene inicios aunque el archivo binario del recurso se haya cargado completamente, pero el proceso de carga no se haya completado.

Si se realiza correctamente, el servidor responde con un código `200` de estado.

### Biblioteca de carga de código abierto {#open-source-upload-library}

Para obtener más información sobre los algoritmos de carga o para crear sus propias herramientas y secuencias de comandos de carga, Adobe proporciona bibliotecas y herramientas de código abierto:

* [Biblioteca](https://github.com/adobe/aem-upload)de carga de aem de código abierto.
* [Herramienta](https://github.com/adobe/aio-cli-plugin-aem)de línea de comandos de código abierto.

### API de carga de recursos obsoletas {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

El nuevo método de carga solo se admite [!DNL Adobe Experience Manager] como Cloud Service. Las API de [!DNL Adobe Experience Manager] 6.5 están en desuso. Los métodos relacionados con la carga o actualización de recursos o representaciones (cualquier carga binaria) están obsoletos en las siguientes API:

* [API HTTP de Experience Manager Assets](mac-api-assets.md)
* `AssetManager` API de Java, como `AssetManager.createAsset(..)`

>[!MORELIKETHIS]
* [Biblioteca](https://github.com/adobe/aem-upload)de carga de aem de código abierto.
* [Herramienta](https://github.com/adobe/aio-cli-plugin-aem)de línea de comandos de código abierto.


## Flujos de trabajo de procesamiento y postprocesamiento de recursos {#post-processing-workflows}

En [!DNL Experience Manager], el procesamiento de recursos se basa en la configuración **[!UICONTROL de Perfiles]** de procesamiento que utiliza [los microservicios](asset-microservices-configure-and-use.md#get-started-using-asset-microservices)de recursos. El procesamiento no requiere extensiones de desarrollador.

Para la configuración del flujo de trabajo posterior al procesamiento, utilice los flujos de trabajo estándar con extensiones con pasos personalizados.

## Compatibilidad con los pasos del flujo de trabajo en el flujo de trabajo posterior al procesamiento {#post-processing-workflows-steps}

Los clientes que actualicen desde versiones anteriores de [!DNL Experience Manager] pueden utilizar los microservicios de recursos para procesar los recursos. Los microservicios de recursos nativos de la nube son mucho más sencillos de configurar y utilizar. No se admiten algunos pasos de flujo de trabajo utilizados en el flujo de trabajo de recursos [!UICONTROL de actualización de] DAM de la versión anterior.

[!DNL Experience Manager] como Cloud Service admite los siguientes pasos del flujo de trabajo:

* `com.day.cq.dam.similaritysearch.internal.workflow.process.AutoTagAssetProcess`
* `com.day.cq.dam.core.impl.process.CreateAssetLanguageCopyProcess`
* `com.day.cq.wcm.workflow.process.CreateVersionProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.core.impl.process.TranslateAssetLanguageCopyProcess`
* `com.day.cq.dam.core.impl.process.UpdateAssetLanguageCopyProcess`
* `com.adobe.cq.workflow.replication.impl.ReplicationWorkflowProcess`
* `com.day.cq.dam.core.impl.process.DamUpdateAssetWorkflowCompletedProcess`

Los siguientes modelos técnicos de flujo de trabajo se sustituyen por microservicios de recursos o no se admite:

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

>[!MORELIKETHIS]
* [El Experience Cloud como Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).

