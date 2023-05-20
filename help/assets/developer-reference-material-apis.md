---
title: Referencias de desarrollador para [!DNL Assets]
description: "[!DNL Assets] Las API y el contenido de referencia del desarrollador le permiten administrar recursos, incluidos archivos binarios, metadatos, representaciones, comentarios y [!DNL Content Fragments]."
contentOwner: AG
feature: APIs,Assets HTTP API
role: Developer,Architect,Admin
exl-id: c75ff177-b74e-436b-9e29-86e257be87fb
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1899'
ht-degree: 6%

---

# [!DNL Adobe Experience Manager Assets] casos de uso para desarrolladores, API y material de referencia {#assets-cloud-service-apis}

El artículo contiene recomendaciones, materiales de referencia y recursos para desarrolladores de [!DNL Assets] as a [!DNL Cloud Service]. Incluye nuevo módulo de carga de recursos, referencia de la API e información sobre la compatibilidad proporcionada en los flujos de trabajo posteriores al procesamiento.

## [!DNL Experience Manager Assets] API y operaciones {#use-cases-and-apis}

[!DNL Assets] as a [!DNL Cloud Service] proporciona varias API para interactuar mediante programación con recursos digitales. Cada API admite casos de uso específicos, como se menciona en la tabla siguiente. El [!DNL Assets] interfaz de usuario, [!DNL Experience Manager] aplicación de escritorio y [!DNL Adobe Asset Link] admiten todas o algunas de las operaciones.

>[!CAUTION]
>
>Algunas API siguen existiendo, pero no son compatibles de forma activa (indicadas con un ×). En la medida de lo posible, no utilice estas API.

| Niveles de soporte | Descripción |
| ------------- | --------------------------- |
| ✓ | Compatibilidad |
| × | No compatible. No utilice. |
| - | No disponible |

| Caso de uso | [aem-upload](https://github.com/adobe/aem-upload) | [Experience Manager/Sling/JCR](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) API de Java | [servicio de asset compute](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html) | [[!DNL Assets] API HTTP](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html#create-an-asset) | Sling [GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) / [POST](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html) servlets | [GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=es) |
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
| Actualización de metadatos | - | ✓ | ✓ | ✓ | ✓ | - |
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
| Versión de lectura | - | ✓ | - | - | - | - |
| Eliminar versión | - | ✓ | - | - | - | - |
| **Carpetas** |  |  |  |  |  |  |
| Crear carpeta | ✓ | ✓ | - | ✓ | - | - |
| Leer carpeta | - | ✓ | - | ✓ | - | - |
| Eliminar carpeta | ✓ | ✓ | - | ✓ | - | - |
| Copiar carpeta | ✓ | ✓ | - | ✓ | - | - |
| Mover carpeta | ✓ | ✓ | - | ✓ | - | - |

## Carga de recursos {#asset-upload}

Entrada [!DNL Experience Manager] as a [!DNL Cloud Service], puede cargar directamente los recursos en el almacenamiento en la nube mediante la API HTTP. A continuación se indican los pasos para cargar un archivo binario. Ejecute estos pasos en una aplicación externa y no dentro de [!DNL Experience Manager] JVM.

1. [Envío de una solicitud HTTP](#initiate-upload). Informa a [!DNL Experience Manage]o implementación de su intención de cargar un nuevo binario.
1. [PUT el contenido del binario](#upload-binary) a uno o más URI proporcionados por la solicitud de inicio.
1. [Envío de una solicitud HTTP](#complete-upload) para informar al servidor de que el contenido del binario se ha cargado correctamente.

![Descripción general del protocolo de carga binaria directa](assets/add-assets-technical.png)

>[!IMPORTANT]
Ejecute los pasos anteriores en una aplicación externa y no dentro de [!DNL Experience Manager] JVM.

El método ofrece una administración escalable y más eficaz de las cargas de recursos. Las diferencias con respecto a [!DNL Experience Manager] 6.5 son:

* Los binarios no pasan [!DNL Experience Manager], que ahora simplemente coordina el proceso de carga con el almacenamiento en la nube binario configurado para la implementación.
* El almacenamiento en la nube binario funciona con una red de distribución de contenido (CDN) o una red perimetral. Una CDN selecciona un punto final de carga más cercano a un cliente. Cuando los datos viajan a una distancia menor a un punto final cercano, el rendimiento de carga y la experiencia del usuario mejoran, especialmente para equipos distribuidos geográficamente.

>[!NOTE]
Consulte el código de cliente para implementar este enfoque en el código abierto [biblioteca de carga de aem](https://github.com/adobe/aem-upload).
[!IMPORTANT]
En determinadas circunstancias, es posible que los cambios no se propaguen completamente entre solicitudes y Experience Manager debido a la naturaleza finalmente coherente del almacenamiento en Cloud Service. Esto provoca que se produzcan respuestas 404 para iniciar o completar llamadas de carga debido a que no se propagan las creaciones de carpetas necesarias. Los clientes deben esperar respuestas 404 y gestionarlas implementando un reintento con una estrategia de back-off.

### Iniciar carga {#initiate-upload}

Envíe una solicitud de POST HTTP a la carpeta deseada. Los recursos se crean o actualizan en esta carpeta. Incluir el selector `.initiateUpload.json` para indicar que la solicitud es para iniciar la carga de un archivo binario. Por ejemplo, la ruta a la carpeta donde se debe crear el recurso es `/assets/folder`. La solicitud del POST es `POST https://[aem_server]:[port]/content/dam/assets/folder.initiateUpload.json`.

El tipo de contenido del cuerpo de la solicitud debe ser `application/x-www-form-urlencoded` datos de formulario, que contienen los siguientes campos:

* `(string) fileName`: Requerido. El nombre del recurso tal como aparece en [!DNL Experience Manager].
* `(number) fileSize`: Requerido. El tamaño de archivo, en bytes, del recurso que se carga.

Se puede utilizar una sola solicitud para iniciar cargas para varios binarios, siempre que cada binario contenga los campos obligatorios. Si se realiza correctamente, la solicitud responde con un `201` código de estado y un cuerpo que contiene datos JSON en el siguiente formato:

```json
{
    "completeURI": "(string)",
    "folderPath": "(string)",
    "files": [
        {
            "fileName": "(string)",
            "mimeType": "(string)",
            "uploadToken": "(string)",
            "uploadURIs": [
                "(string)"
            ],
            "minPartSize": (number),
            "maxPartSize": (number)
        }
    ]
}
```

* `completeURI` (cadena): Invoque este URI cuando el binario termine de cargarse. El URI puede ser absoluto o relativo, y los clientes deben poder gestionarlo. Es decir, el valor puede ser `"https://[aem_server]:[port]/content/dam.completeUpload.json"` o `"/content/dam.completeUpload.json"` Consulte [carga completa](#complete-upload).
* `folderPath` (cadena): Ruta de acceso completa a la carpeta en la que se carga el binario.
* `(files)` (matriz): Una lista de elementos cuya longitud y orden coinciden con la longitud y el orden de la lista de información binaria proporcionada en la solicitud de inicio.
* `fileName` (cadena): El nombre del binario correspondiente, tal como se proporciona en la solicitud de inicio. Este valor debe incluirse en la solicitud completa.
* `mimeType` (cadena): el tipo mime del binario correspondiente, tal como se proporciona en la solicitud de inicio. Este valor debe incluirse en la solicitud completa.
* `uploadToken` (cadena): Un token de carga para el binario correspondiente. Este valor debe incluirse en la solicitud completa.
* `uploadURIs` (matriz): Una lista de cadenas cuyos valores son URI completos a los que se debe cargar el contenido del binario (consulte [Cargar binario](#upload-binary)).
* `minPartSize` (número): La longitud mínima, en bytes, de datos que se pueden proporcionar a cualquiera de los `uploadURIs`, si hay más de un URI.
* `maxPartSize` (número): La longitud máxima, en bytes, de datos que se pueden proporcionar a cualquiera de los `uploadURIs`, si hay más de un URI.

### Cargar binario {#upload-binary}

La salida del inicio de una carga incluye uno o más valores de URI de carga. Si se proporciona más de un URI, el cliente puede dividir el binario en partes y realizar solicitudes de PUT de cada parte a los URI de carga proporcionados, por orden. Si decide dividir el binario en partes, siga las siguientes directrices:

* Cada parte, excepto la última, debe tener un tamaño bueno o igual a `minPartSize`.
* Cada pieza debe tener un tamaño inferior o igual a `maxPartSize`.
* Si el tamaño del binario supera `maxPartSize`, divida el binario en partes para cargarlo.
* No es necesario que utilice todos los URI.

Si el tamaño del binario es menor o igual que `maxPartSize`, en su lugar, puede cargar el binario completo en un único URI de carga. Si se proporciona más de un URI de carga, utilice el primero e ignore el resto. No es necesario que utilice todos los URI.

Los nodos perimetrales de CDN ayudan a acelerar la carga solicitada de binarios.

La forma más sencilla de lograrlo es utilizar el valor de `maxPartSize` como tamaño de la pieza. El contrato de API garantiza que haya suficientes URI de carga para cargar el binario si utiliza este valor como tamaño de parte. Para ello, divida el binario en partes de tamaño `maxPartSize`, utilizando un URI para cada parte, en orden. La parte final puede ser de cualquier tamaño inferior o igual a `maxPartSize`. Por ejemplo, supongamos que el tamaño total del binario es de 20 000 bytes, la variable `minPartSize` tiene 5000 bytes, `maxPartSize` tiene 8000 bytes y el número de URI de carga es 5. Siga estos pasos:

* Cargue los primeros 8000 bytes del binario con el primer URI de carga.
* Cargue los segundos 8000 bytes del binario mediante el segundo URI de carga.
* Cargue los últimos 4000 bytes del binario con el tercer URI de carga. Dado que esta es la parte final, no necesita ser mayor que `minPartSize`.
* No es necesario utilizar los dos últimos URI de carga. Puedes ignorarlos.

Un error común es calcular el tamaño de la parte en función del número de URI de carga proporcionados por la API. El contrato de API no garantiza que este enfoque funcione, y en realidad puede dar como resultado tamaños de pieza que estén fuera del intervalo entre `minPartSize` y `maxPartSize`. Esto puede provocar errores de carga de archivos binarios.

De nuevo, la forma más fácil y segura es simplemente utilizar partes de tamaño igual a `maxPartSize`.

Si la carga se realiza correctamente, el servidor responde a cada solicitud con un `201` código de estado.

>[!NOTE]
Para obtener más información sobre el algoritmo de carga, consulte la [documentación oficial de funciones](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload) y [Documentación de API](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/api/binary/BinaryUpload.html) en el proyecto Apache Jackrabbit Oak.

### Carga completa {#complete-upload}

Una vez cargadas todas las partes de un archivo binario, envíe una solicitud de POST HTTP al URI completo proporcionado por los datos de inicio. El tipo de contenido del cuerpo de la solicitud debe ser `application/x-www-form-urlencoded` datos de formulario, que contienen los siguientes campos.

| Campos | Tipo | Requerido o no | Descripción |
|---|---|---|---|
| `fileName` | Cadena | Requerido | El nombre del recurso, tal como lo proporcionaron los datos de inicio. |
| `mimeType` | Cadena | Requerido | El tipo de contenido HTTP del binario, tal como lo proporcionaron los datos de inicio. |
| `uploadToken` | Cadena | Requerido | Cargue el token para el binario, tal como lo proporcionaron los datos de inicio. |
| `createVersion` | Booleano | Opcional | If `True` y existe un recurso con el nombre especificado, [!DNL Experience Manager] crea una nueva versión del recurso. |
| `versionLabel` | Cadena | Opcional | Si se crea una nueva versión, la etiqueta asociada a la nueva versión de un recurso |
| `versionComment` | Cadena | Opcional | Si se crea una nueva versión, los comentarios asociados con la versión. |
| `replace` | Booleano | Opcional | If `True` y existe un recurso con el nombre especificado, [!DNL Experience Manager] elimina el recurso y lo vuelve a crear. |
| `uploadDuration` | Número | Opcional | Tiempo total, en milisegundos, que el archivo se va a cargar en su totalidad. Si se especifica, la duración de la carga se incluye en los archivos de registro del sistema para el análisis de la velocidad de transferencia. |
| `fileSize` | Número | Opcional | El tamaño, en bytes, del archivo. Si se especifica, el tamaño del archivo se incluye en los archivos de registro del sistema para el análisis de velocidad de transferencia. |

>[!NOTE]
Si el recurso existe y ninguno `createVersion` ni `replace` se especifica, entonces [!DNL Experience Manager] actualiza la versión actual del recurso con el nuevo binario.

Al igual que el proceso de inicio, los datos de solicitud completos pueden contener información de más de un archivo.

El proceso de carga de un binario no termina hasta que se invoca la dirección URL completa del archivo. Una vez completado el proceso de carga, se procesa un recurso. El procesamiento no se inicia aunque el archivo binario del recurso se haya cargado completamente, pero el proceso de carga no se haya completado. Si la carga se realiza correctamente, el servidor responde con un `200` código de estado.

### Biblioteca de carga de código abierto {#open-source-upload-library}

Para obtener más información sobre los algoritmos de carga o para crear sus propios scripts y herramientas de carga, Adobe proporciona bibliotecas y herramientas de código abierto:

* [Biblioteca de código abierto aem-upload](https://github.com/adobe/aem-upload).
* [Herramienta de línea de comandos de código abierto](https://github.com/adobe/aio-cli-plugin-aem).

>[!NOTE]
La biblioteca de carga de aem y la herramienta de línea de comandos utilizan la variable [biblioteca node-httptransfer](https://github.com/adobe/node-httptransfer/)

### API de carga de recursos obsoletas {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

El nuevo método de carga solo es compatible para [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]. Las API de [!DNL Adobe Experience Manager] 6.5 está obsoleto. Los métodos relacionados con la carga o actualización de recursos o representaciones (cualquier carga binaria) están en desuso en las siguientes API:

* [API HTTP de Experience Manager Assets](mac-api-assets.md)
* `AssetManager` API de Java, como `AssetManager.createAsset(..)`

>[!MORELIKETHIS]
* [Biblioteca de código abierto aem-upload](https://github.com/adobe/aem-upload).
* [Herramienta de línea de comandos de código abierto](https://github.com/adobe/aio-cli-plugin-aem).
* [Documentación de Apache Jackrabbit Oak para carga directa](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload).


## Flujos de trabajo de procesamiento de recursos y posprocesamiento {#post-processing-workflows}

Entrada [!DNL Experience Manager], el procesamiento de recursos se basa en **[!UICONTROL Perfiles de procesamiento]** configuración que utiliza [microservicios de recursos](asset-microservices-configure-and-use.md#get-started-using-asset-microservices). El procesamiento no requiere extensiones de desarrollador.

Para la configuración del flujo de trabajo posterior al procesamiento, utilice los flujos de trabajo estándar con extensiones con pasos personalizados.

## Compatibilidad con los pasos del flujo de trabajo en el flujo de trabajo posterior al procesamiento {#post-processing-workflows-steps}

Si actualiza desde una versión anterior de [!DNL Experience Manager], puede utilizar los microservicios de recursos para procesar recursos. Los microservicios de recursos nativos de la nube son más fáciles de configurar y utilizar. Algunos pasos del flujo de trabajo utilizados en [!UICONTROL Recurso de actualización DAM] no se admiten los flujos de trabajo de la versión anterior. Para obtener más información sobre las clases compatibles, consulte la [Referencia de la API de Java para Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html).

Los siguientes modelos de flujo de trabajo técnico se han sustituido por microservicios de recursos o la compatibilidad no está disponible:

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

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de Recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con Assets](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos conectados](use-assets-across-connected-assets-instances.md)
* [Informes de Asset](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)

>[!MORELIKETHIS]
* [[!DNL Experience Cloud] as a [!DNL Cloud Service] SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).

