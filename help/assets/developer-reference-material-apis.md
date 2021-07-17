---
title: Referencias del desarrollador para [!DNL Assets]
description: '[!DNL Assets] APIs and developer reference content lets you manage assets, including binary files, metadata, renditions, comments, and [!DNL Content Fragments].'
contentOwner: AG
feature: API, API HTTP de Assets
role: Developer,Architect,Admin
exl-id: c75ff177-b74e-436b-9e29-86e257be87fb
source-git-commit: 3051475d20d5b534b74c84f9d541dcaf1a5492f9
workflow-type: tm+mt
source-wordcount: '1436'
ht-degree: 2%

---

# [!DNL Adobe Experience Manager Assets] casos de uso para desarrolladores, API y material de referencia {#assets-cloud-service-apis}

El artículo contiene recomendaciones, materiales de referencia y recursos para desarrolladores de [!DNL Assets] como [!DNL Cloud Service]. Incluye un nuevo módulo de carga de recursos, una referencia de API y información sobre la compatibilidad proporcionada en los flujos de trabajo posteriores al procesamiento.

## [!DNL Experience Manager Assets] API y operaciones {#use-cases-and-apis}

[!DNL Assets] as a  [!DNL Cloud Service] proporciona varias API para interactuar mediante programación con recursos digitales. Cada API admite casos de uso específicos, como se menciona en la tabla siguiente. La interfaz de usuario [!DNL Assets], la aplicación de escritorio [!DNL Experience Manager] y [!DNL Adobe Asset Link] admiten todas o algunas de las operaciones.

>[!CAUTION]
>
>Algunas API siguen existiendo, pero no se admiten de forma activa (indicada con una ×). En la medida de lo posible, no utilice estas API.

| Nivel de asistencia | Descripción |
| ------------- | --------------------------- |
| ✓ | Compatible |
| × | No se admite. No usar. |
| - | No disponible |

| Caso de uso | [aem-upload](https://github.com/adobe/aem-upload) | [API de Experience Manager/Sling/](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/index.html) JCRJava | [servicio de asset compute](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html) | [[!DNL Assets] API HTTP](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html#create-an-asset) | Servlets [GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) / [POST](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html) de Sling | [GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) _(vista previa)_ |
| ----------------|:---:|:---:|:---:|:---:|:---:|:---:|
| **binario original** |  |  |  |  |  |  |
| Crear original | ✓ | × | - | × | × | - |
| Leer original | - | × | ✓ | ✓ | ✓ | - |
| Actualizar original | ✓ | × | ✓ | × | × | - |
| Eliminar original | - | ✓ | - | ✓ | ✓ | - |
| Copiar original | - | ✓ | - | ✓ | ✓ | - |
| Mover original | - | ✓ | - | ✓ | ✓ | - |
| **Metadatos** |  |  |  |  |  |  |
| Crear metadatos | - | ✓ | ✓ | ✓ | ✓ | - |
| Leer metadatos | - | ✓ | - | ✓ | ✓ | - |
| Actualizar metadatos | - | ✓ | ✓ | ✓ | ✓ | - |
| Eliminar metadatos | - | ✓ | ✓ | ✓ | ✓ | - |
| Copiar metadatos | - | ✓ | - | ✓ | ✓ | - |
| Mover metadatos | - | ✓ | - | ✓ | ✓ | - |
| **Fragmentos de contenido (CF)** |  |  |  |  |  |  |
| Crear CF | - | ✓ | - | ✓ | - | - |
| Leer CF | - | ✓ | - | ✓ | - | ✓ |
| Actualizar CF | - | ✓ | - | ✓ | - | - |
| Eliminar CF | - | ✓ | - | ✓ | - | - |
| Copiar CF | - | ✓ | - | ✓ | - | - |
| Mover CF | - | ✓ | - | ✓ | - | - |
| **Versiones** |  |  |  |  |  |  |
| Crear versión | ✓ | ✓ | - | - | - | - |
| Leer versión | - | ✓ | - | - | - | - |
| Eliminar versión | - | ✓ | - | - | - | - |
| **Carpetas** |  |  |  |  |  |  |
| Crear carpeta | ✓ | ✓ | - | ✓ | - | - |
| Leer carpeta | - | ✓ | - | ✓ | - | - |
| Eliminar carpeta | ✓ | ✓ | - | ✓ | - | - |
| Copiar carpeta | ✓ | ✓ | - | ✓ | - | - |
| Mover carpeta | ✓ | ✓ | - | ✓ | - | - |

## Carga de recursos {#asset-upload}

En [!DNL Experience Manager] como [!DNL Cloud Service], puede cargar directamente los recursos en el almacenamiento en la nube mediante la API HTTP. A continuación se indican los pasos para cargar un archivo binario. Ejecute estos pasos en una aplicación externa y no dentro de la JVM [!DNL Experience Manager].

1. [Enviar una solicitud](#initiate-upload) HTTP. Informa a la implementación [!DNL Experience Manage]r de su intención de cargar un nuevo binario.
1. [PUT el contenido del ](#upload-binary) binario a uno o más URI proporcionados por la solicitud de inicio.
1. [Envíe una ](#complete-upload) solicitud HTTP para informar al servidor de que el contenido del binario se cargó correctamente.

![Descripción general del protocolo de carga binaria directa](assets/add-assets-technical.png)

>[!IMPORTANT]
Ejecute los pasos anteriores en una aplicación externa y no dentro de la JVM [!DNL Experience Manager].

El método proporciona una gestión escalable y más eficaz de las cargas de recursos. Las diferencias con respecto a [!DNL Experience Manager] 6.5 son:

* Los binarios no pasan por [!DNL Experience Manager], que ahora simplemente está coordinando el proceso de carga con el almacenamiento en la nube binaria configurado para la implementación.
* El almacenamiento en la nube binaria funciona con una red de entrega de contenido (CDN) o una red perimetral. Una CDN selecciona un extremo de carga más cercano a un cliente. Cuando los datos se desplazan a una distancia más corta hasta un punto final cercano, el rendimiento de carga y la experiencia del usuario mejoran, especialmente para equipos distribuidos geográficamente.

>[!NOTE]
Consulte el código de cliente para implementar este método en la [biblioteca de carga de aem](https://github.com/adobe/aem-upload) de código abierto.

### Iniciar carga {#initiate-upload}

Envíe una solicitud de POST HTTP a la carpeta deseada. Los recursos se crean o actualizan en esta carpeta. Incluya el selector `.initiateUpload.json` para indicar que la solicitud es iniciar la carga de un archivo binario. Por ejemplo, la ruta a la carpeta donde se debe crear el recurso es `/assets/folder`. La solicitud del POST es `POST https://[aem_server]:[port]/content/dam/assets/folder.initiateUpload.json`.

El tipo de contenido del cuerpo de la solicitud debe ser `application/x-www-form-urlencoded` datos de formulario, que contengan los siguientes campos:

* `(string) fileName`: Requerido. El nombre del recurso tal como aparece en [!DNL Experience Manager].
* `(number) fileSize`: Requerido. El tamaño del archivo, en bytes, del recurso que se está cargando.

Se puede utilizar una sola solicitud para iniciar cargas para varios binarios, siempre que cada binario contenga los campos obligatorios. Si la solicitud se realiza correctamente, responde con un código de estado `201` y un cuerpo que contiene datos JSON en el siguiente formato:

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

* `completeURI` (cadena): Llame a este URI cuando el binario termine de cargarse. El URI puede ser absoluto o relativo, y los clientes deben poder gestionar cualquiera de ellos. Es decir, el valor puede ser `"https://[aem_server]:[port]/content/dam.completeUpload.json"` o `"/content/dam.completeUpload.json"` Consulte [carga completa](#complete-upload).
* `folderPath` (cadena): Ruta de acceso completa a la carpeta en la que se carga el binario.
* `(files)` (matriz): Una lista de elementos cuya longitud y orden coinciden con la longitud y el orden de la lista de información binaria proporcionada en la solicitud de inicio.
* `fileName` (cadena): El nombre del binario correspondiente, tal como se proporciona en la solicitud de inicio. Este valor debe incluirse en la solicitud completa.
* `mimeType` (cadena): Tipo mime del binario correspondiente, tal como se suministra en la solicitud de inicio. Este valor debe incluirse en la solicitud completa.
* `uploadToken` (cadena): Un token de carga para el binario correspondiente. Este valor debe incluirse en la solicitud completa.
* `uploadURIs` (matriz): Una lista de cadenas cuyos valores son URIs completas a las que se debe cargar el contenido del binario (consulte  [Cargar binario](#upload-binary)).
* `minPartSize` (número): Longitud mínima, en bytes, de los datos que se pueden proporcionar a cualquiera de los  `uploadURIs`, si hay más de un URI.
* `maxPartSize` (número): Longitud máxima, en bytes, de los datos que se pueden proporcionar a cualquiera de los  `uploadURIs`, si hay más de un URI.

### Cargar binario {#upload-binary}

El resultado del inicio de una carga incluye uno o más valores de URI de carga. Si se proporciona más de un URI, el cliente divide el binario en partes y realiza solicitudes de PUT de cada parte a cada URI, en orden. Utilice todas las URI. Asegúrese de que el tamaño de cada pieza esté dentro de los tamaños mínimo y máximo especificados en la respuesta de inicio. Los nodos perimetrales de CDN ayudan a acelerar la carga solicitada de binarios.

Un método potencial para lograr esto es calcular el tamaño de la parte en función del número de URI de carga que proporcione la API. Por ejemplo, supongamos que el tamaño total del binario es de 20 000 bytes y el número de URI de carga es de 2. A continuación, siga estos pasos:

* Calcule el tamaño de pieza dividiendo el tamaño total por número de URI: 20.000 / 2 = 10.000.
* Intervalo de bytes del POST 0-9.999 del binario con el primer URI de la lista de URI de carga.
* Intervalo de bytes del POST 10.000 - 19.999 del binario al segundo URI de la lista de URI de carga.

Si la carga se realiza correctamente, el servidor responde a cada solicitud con un código de estado `201`.

### Carga completa {#complete-upload}

Una vez cargadas todas las partes de un archivo binario, envíe una solicitud de POST HTTP al URI completo proporcionado por los datos de inicio. El tipo de contenido del cuerpo de la solicitud debe ser `application/x-www-form-urlencoded` datos de formulario, que contengan los siguientes campos.

| Fields | Tipo | Requerido o no | Descripción |
|---|---|---|---|
| `fileName` | Cadena | Requerido | El nombre del recurso, tal como lo proporcionaron los datos de inicio. |
| `mimeType` | Cadena | Requerido | El tipo de contenido HTTP del binario, tal como proporcionaron los datos de inicio. |
| `uploadToken` | Cadena | Requerido | Token de carga para el binario, tal como proporcionaban los datos de inicio. |
| `createVersion` | Booleano | Opcional | Si `True` y existe un recurso con el nombre especificado, [!DNL Experience Manager] crea una nueva versión del recurso. |
| `versionLabel` | Cadena | Opcional | Si se crea una nueva versión, la etiqueta asociada a la nueva versión de un recurso . |
| `versionComment` | Cadena | Opcional | Si se crea una nueva versión, los comentarios asociados a la versión. |
| `replace` | Booleano | Opcional | Si `True` y existe un recurso con el nombre especificado, [!DNL Experience Manager] elimina el recurso y lo vuelve a crear. |

>[!NOTE]
Si el recurso existe y no se especifica `createVersion` ni `replace`, [!DNL Experience Manager] actualiza la versión actual del recurso con el nuevo binario.

Al igual que el proceso de inicio, los datos de solicitud completos pueden contener información para más de un archivo.

El proceso de carga de un binario no se realiza hasta que se invoca la URL completa para el archivo. Un recurso se procesa una vez finalizado el proceso de carga. El procesamiento no se inicia aunque el archivo binario del recurso se cargue completamente, pero el proceso de carga no se haya completado. Si la carga se realiza correctamente, el servidor responde con un código de estado `200`.

### Biblioteca de carga de código abierto {#open-source-upload-library}

Para obtener más información sobre los algoritmos de carga o para crear sus propios scripts y herramientas de carga, Adobe proporciona bibliotecas y herramientas de código abierto:

* [Biblioteca de carga de aem de código abierto](https://github.com/adobe/aem-upload).
* [Herramienta](https://github.com/adobe/aio-cli-plugin-aem) de línea de comandos de código abierto.

### API de carga de recursos obsoletas {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

El nuevo método de carga solo se admite para [!DNL Adobe Experience Manager] como [!DNL Cloud Service]. Las API de [!DNL Adobe Experience Manager] 6.5 están en desuso. Los métodos relacionados con la carga o actualización de recursos o representaciones (cualquier carga binaria) quedan obsoletos en las siguientes API:

* [API HTTP de recursos de Experience Manager](mac-api-assets.md)
* `AssetManager` API de Java, como  `AssetManager.createAsset(..)`

>[!MORELIKETHIS]
* [Biblioteca de carga de aem de código abierto](https://github.com/adobe/aem-upload).
* [Herramienta](https://github.com/adobe/aio-cli-plugin-aem) de línea de comandos de código abierto.


## Flujos de trabajo de procesamiento y posprocesamiento de recursos {#post-processing-workflows}

En [!DNL Experience Manager], el procesamiento de recursos se basa en la configuración **[!UICONTROL Perfiles de procesamiento]** que utiliza [microservicios de recursos](asset-microservices-configure-and-use.md#get-started-using-asset-microservices). El procesamiento no requiere extensiones de desarrollador.

Para la configuración del flujo de trabajo posterior al procesamiento, utilice los flujos de trabajo estándar con extensiones con pasos personalizados.

## Compatibilidad de los pasos del flujo de trabajo en el flujo de trabajo posterior al procesamiento {#post-processing-workflows-steps}

Si actualiza desde una versión anterior de [!DNL Experience Manager], puede utilizar los microservicios de recursos para procesar los recursos. Los microservicios de recursos nativos de la nube son más sencillos de configurar y usar. No se admiten algunos pasos de flujo de trabajo utilizados en el flujo de trabajo [!UICONTROL DAM Update Asset] en la versión anterior. Para obtener más información sobre las clases admitidas, consulte la [Referencia de API de Java](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/index.html).

Los siguientes modelos técnicos de flujo de trabajo se sustituyen por microservicios de recursos o no hay compatibilidad disponible:

* `com.day.cq.dam.cameraraw.process.CameraRawHandlingProcess`
* `com.day.cq.dam.core.process.CommandLineProcess`
* `com.day.cq.dam.pdfrasterizer.process.PdfRasterizerHandlingProcess`
* `com.day.cq.dam.core.process.AddPropertyWorkflowProcess`
* `com.day.cq.dam.core.process.CreateSubAssetsProcess`
* `com.day.cq.dam.core.process.DownloadAssetProcess`
* `com.day.cq.dam.word.process.ExtractImagesProcess`
* `com.day.cq.dam.word.process.ExtractPlainProcess`
* `com.day.cq.dam.ids.impl.process.IDSJobProcess`
* `com.day.cq.dam.indd.process.INDDMediaExtractProcess`
* `com.day.cq.dam.indd.process.INDDPageExtractProcess`
* `com.day.cq.dam.core.impl.lightbox.LightboxUpdateAssetProcess`
* `com.day.cq.dam.pim.impl.sourcing.upload.process.ProductAssetsUploadProcess`
* `com.day.cq.dam.core.process.SendDownloadAssetEmailProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.switchengine.process.SwitchEngineHandlingProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.video.FFMpegTranscodeProcess`
* `com.day.cq.dam.core.process.ThumbnailProcess`
* `com.day.cq.dam.video.FFMpegThumbnailProcess`
* `com.day.cq.dam.core.process.CreateWebEnabledImageProcess`
* `com.day.cq.dam.core.process.CreatePdfPreviewProcess`
* `com.day.cq.dam.s7dam.common.process.VideoUserUploadedThumbnailProcess`
* `com.day.cq.dam.s7dam.common.process.VideoThumbnailDownloadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoProxyServiceProcess`
* `com.day.cq.dam.scene7.impl.process.Scene7UploadProcess`
* `com.day.cq.dam.s7dam.common.process.S7VideoThumbnailProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.adobe.cq.dam.dm.process.workflow.DMImageProcess`

<!-- Commenting the previous list documented at the time of GA. Replacing it with the updated list via cqdoc-18231.

* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
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
-->

<!-- PPTX source: slide in add-assets.md - overview of direct binary upload section of 
https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

>[!MORELIKETHIS]
* [[!DNL Experience Cloud] as a [!DNL Cloud Service] SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).

