---
title: 'API de recursos para la administración de recursos digitales en Adobe Experience Manager como servicio de nube '
description: Las API de recursos permiten operaciones básicas de creación, lectura, actualización y eliminación (CRUD) para administrar recursos, incluidos binarios, metadatos, representaciones, comentarios y fragmentos de contenido.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0686acbc61b3902c6c926eaa6424828db0a6421a

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
Para revisar el código de cliente que implementa este método, consulte la biblioteca de carga de [aem de código abierto](https://github.com/adobe/aem-upload)

### Iniciar carga {#initiate-upload}

El primer paso es enviar una solicitud HTTP POST a la carpeta en la que se debe crear o actualizar el recurso; incluya el selector `.initiateUpload.json` para indicar que la solicitud debe comenzar una carga binaria. Por ejemplo, la ruta a la carpeta en la que se debe crear el recurso es `/assets/folder`:

```
POST https://[aem_server]/content/dam/assets/folder.initiateUpload.json
````

El tipo de contenido del cuerpo de la solicitud deben ser datos `application/x-www-form-urlencoded` de formulario, que contengan los campos siguientes:

* `(string) fileName`: Requerido. Nombre del recurso tal como aparecerá en la instancia.
* `(number) fileSize`: Requerido. Longitud total, en bytes, del binario que se va a cargar.

Se puede utilizar una sola solicitud para iniciar cargas para varios binarios, siempre que cada binario contenga los campos obligatorios. Si se realiza correctamente, la solicitud responde con un código `201` de estado y un cuerpo que contiene datos JSON en el siguiente formato:

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
```

* `completeURI` (cadena): Invoque este URI cuando termine de cargarse el binario. El URI puede ser un URI absoluto o relativo y los clientes deben poder gestionar cualquiera de los dos. Es decir, el valor puede ser `"https://author.acme.com/content/dam.completeUpload.json"` o `"/content/dam.completeUpload.json"` Ver carga [completa](#complete-upload).
* `folderPath` (cadena): Ruta de acceso completa a la carpeta en la que se está cargando el binario.
* `(files)` (matriz): Una lista de elementos cuya longitud y orden coincidirán con la longitud y el orden de la lista de información binaria proporcionada en la solicitud de inicio.
* `fileName` (cadena): El nombre del binario correspondiente, tal como se indica en la solicitud de inicio. Este valor debe incluirse en la solicitud completa.
* `mimeType` (cadena): El tipo mime del binario correspondiente, tal como se proporciona en la solicitud de inicio in. Este valor debe incluirse en la solicitud completa.
* `uploadToken` (cadena): Un distintivo de carga para el binario correspondiente. Este valor debe incluirse en la solicitud completa.
* `uploadURIs` (matriz): Una lista de cadenas cuyos valores son URIs completos a las que se debe cargar el contenido del binario (consulte [Cargar binario](#upload-binary)).
* `minPartSize` (número): Longitud mínima, en bytes, de los datos que se pueden proporcionar a cualquiera de los URIs de carga, si hay más de un URI.
* `maxPartSize` (número): Longitud máxima, en bytes, de los datos que se pueden proporcionar a cualquiera de los URIs de carga, si hay más de un URI.

### Cargar binario {#upload-binary}

El resultado del inicio de una carga incluirá uno o varios valores de URI de carga. Si se proporciona más de un URI, es responsabilidad del cliente &quot;dividir&quot; el binario en partes y POST cada parte, en orden, a cada URI, en orden. Se deben utilizar todos los URI y cada parte debe ser mayor que el tamaño mínimo y menor que el tamaño máximo especificado en la respuesta de inicio. Estas solicitudes serán enviadas por nodos perimetrales CDN para acelerar la carga de binarios.

Una forma posible de lograrlo es calcular el tamaño de la pieza en función del número de URI de carga proporcionados por la API. Ejemplo suponiendo que el tamaño total del binario es de 20.000 bytes y el número de URI de carga es de 2:

* Calcule el tamaño de la pieza dividiendo el tamaño total por el número de URI: 20.000 / 2 = 10.000
* Intervalo de bytes POST 0-9,999 del binario al primer URI en la lista de URI de carga
* Intervalo de bytes POST 10.000 - 19.999 del binario al segundo URI en la lista de URI de carga

Si se realiza correctamente, el servidor responde a cada solicitud con un código `201` de estado.

### Carga completa {#complete-upload}

Una vez cargadas todas las partes de un archivo binario, envíe una solicitud HTTP POST al URI completo proporcionado por los datos de inicio. El tipo de contenido del cuerpo de la solicitud debe ser datos `application/x-www-form-urlencoded` de formulario, que contengan los campos siguientes.

| Fields | Tipo | Obligatorio o no | Descripción |
|---|---|---|---|
| `fileName` | Cadena | Requerido | El nombre del recurso, tal y como lo proporcionaron los datos de inicio. |
| `mimeType` | Cadena | Requerido | El tipo de contenido HTTP del binario, tal como se proporcionó con los datos de inicio. |
| `uploadToken` | Cadena | Requerido | Distintivo de carga para el binario, tal y como proporcionaban los datos de inicio. |
| `createVersion` | Booleano | Opcional | Si `True` y ya existe un recurso con el nombre especificado, Experience Manager crea una nueva versión del recurso. |
| `versionLabel` | Cadena | Opcional | Si se crea una nueva versión, la etiqueta asociada con la nueva versión de un recurso. |
| `versionComment` | Cadena | Opcional | Si se crea una nueva versión, los comentarios asociados a ella. |
| `replace` | Booleano | Opcional | Si ya existe `True` un recurso con el nombre especificado, Experience Manager lo elimina y lo vuelve a crear. |

>!![NOTE]
>
> Si el recurso ya existe `createVersion` y no `replace` se especifica, Experience Manager actualiza la versión actual del recurso con el nuevo binario.

Al igual que el proceso de inicio, los datos completos de la solicitud pueden contener información para más de un archivo.

El proceso de carga de un binario no se realiza hasta que se invoque la dirección URL completa para el archivo. Aunque el binario de un archivo se cargue en su totalidad, la instancia no procesará el recurso hasta que se complete el proceso de carga.

Si se realiza correctamente, el servidor responde con un código `200` de estado.

### Biblioteca de carga de código abierto {#open-source-upload-library}

Para obtener más información sobre los algoritmos de carga o para crear sus propios scripts y herramientas de carga, Adobe proporciona bibliotecas y herramientas de código abierto como punto de partida:

* [Biblioteca de carga de aem de código abierto](https://github.com/adobe/aem-upload)
* [Herramienta de línea de comandos de código abierto](https://github.com/adobe/aio-cli-plugin-aem)

### API de carga de recursos obsoletas {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

Para Adobe Experience Manager como servicio de nube, solo se admiten las nuevas API de carga. Las API de Adobe Experience Manager 6.5 están en desuso. Los métodos relacionados con la carga o actualización de recursos o representaciones (cualquier carga binaria) están obsoletos en las siguientes API:

* [API HTTP de AEM Assets](mac-api-assets.md)
* `AssetManager` API de Java, como `AssetManager.createAsset(..)`

>[!MORELIKETHIS]
* [Biblioteca](https://github.com/adobe/aem-upload)de carga de aem de código abierto.
* [Herramienta](https://github.com/adobe/aio-cli-plugin-aem)de línea de comandos de código abierto.


## flujos de trabajo de procesamiento y postprocesamiento de recursos {#post-processing-workflows}

En Experience Manager, el procesamiento de recursos se basa en la configuración **[!UICONTROL de Perfiles]** de procesamiento que utiliza [los microservicios](asset-microservices-configure-and-use.md#get-started-using-asset-microservices)de recursos. El procesamiento no requiere extensiones de desarrollador.

Para la configuración del flujo de trabajo posterior al procesamiento, utilice los flujos de trabajo estándar con extensiones con pasos personalizados.

## Compatibilidad con los pasos del flujo de trabajo en el flujo de trabajo posterior al procesamiento {#post-processing-workflows-steps}

Los clientes que actualicen a Experience Manager como servicio de nube desde versiones anteriores de Experience Manager pueden utilizar los microservicios de recursos para procesar los recursos. Los microservicios de recursos nativos de la nube son mucho más sencillos de configurar y utilizar. No se admiten algunos pasos de flujo de trabajo utilizados en el flujo de trabajo de recursos [!UICONTROL de actualización de] DAM de la versión anterior.

Experience Manager admite los siguientes pasos de flujo de trabajo como servicio de nube.

* `com.day.cq.dam.similaritysearch.internal.workflow.process.AutoTagAssetProcess`
* `com.day.cq.dam.core.impl.process.CreateAssetLanguageCopyProcess`
* `com.day.cq.wcm.workflow.process.CreateVersionProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.core.impl.process.TranslateAssetLanguageCopyProcess`
* `com.day.cq.dam.core.impl.process.UpdateAssetLanguageCopyProcess`
* `com.adobe.cq.workflow.replication.impl.ReplicationWorkflowProcess`
* `com.day.cq.dam.core.impl.process.DamUpdateAssetWorkflowCompletedProcess`

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
