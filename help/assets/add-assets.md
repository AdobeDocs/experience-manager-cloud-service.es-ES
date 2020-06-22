---
title: Añadir los recursos digitales en Adobe Experience Manager
description: Añada los recursos digitales a Adobe Experience Manager como Cloud Service
translation-type: tm+mt
source-git-commit: 68cf71054b1cd7dfb2790122ba4c29854ffdf703
workflow-type: tm+mt
source-wordcount: '1358'
ht-degree: 2%

---


# Añadir recursos digitales a Adobe Experience Manager {#add-assets-to-experience-manager}

Adobe Experience Manager enriquece el contenido binario de los archivos digitales cargados con metadatos enriquecidos, etiquetas inteligentes, representaciones y otros servicios de administración de recursos digitales (DAM). Puede cargar varios tipos de archivos, como imágenes, documentos y archivos de imagen sin procesar, desde la carpeta local o desde una unidad de red a Recursos Experience Manager.

Se proporcionan varios métodos de carga. Además de la carga del navegador que se utiliza con más frecuencia, existen otros métodos para añadir recursos al repositorio de Experience Manager, incluidos los clientes de escritorio, como Adobe Asset Link o la aplicación de escritorio de Experience Manager, los scripts de carga e inserción que crearían los clientes, y las integraciones de inserción automatizada se agregan como extensiones de AEM.

Nos centraremos en los métodos de carga para los usuarios finales aquí y proporcionaremos vínculos a artículos que describen los aspectos técnicos de la carga y la ingesta de recursos mediante API y SDK de Experience Manager.

Aunque puede cargar y administrar cualquier archivo binario en Experience Manager, los formatos de archivo más utilizados son compatibles con servicios adicionales, como la extracción de metadatos o la generación de previsualizaciones y representaciones. Consulte los formatos [de archivo](file-format-support.md) admitidos para obtener más información.

También puede elegir que se realice un procesamiento adicional en los recursos cargados. Se pueden configurar varios perfiles de procesamiento de recursos en la carpeta, en la que se cargan los recursos, para agregar metadatos, representaciones o servicios de procesamiento de imágenes específicos. Consulte Procesamiento [](#additional-processing) adicional a continuación para obtener más información.

>[!NOTE]
>
> Experience Manager como Cloud Service aprovecha una nueva forma de cargar recursos: la carga binaria directa. De forma predeterminada, es compatible con las prestaciones y los clientes del producto integrados, como la interfaz de usuario de AEM, Adobe Asset Link, la aplicación de escritorio de AEM y, por tanto, transparente para los usuarios finales.
>
> El código de carga personalizado o ampliado por los equipos técnicos de los clientes debe utilizar las nuevas API y protocolos de carga.

## Upload assets {#upload-assets}

Para cargar un archivo (o varios archivos), puede seleccionarlos en el escritorio y arrastrarlos y colocarlos en la interfaz de usuario (navegador web) a la carpeta de destino. También puede iniciar la carga desde la interfaz de usuario.

1. En la interfaz de usuario de Recursos, navegue hasta la ubicación en la que desee agregar recursos digitales.
1. Para cargar los recursos, realice una de las siguientes acciones:

   * En la barra de herramientas, toque el icono **[!UICONTROL Crear]** . A continuación, en el menú, toque **[!UICONTROL Archivos]**. Si es necesario, puede cambiar el nombre del archivo en el cuadro de diálogo presentado.
   * En un navegador compatible con HTML5, arrastre los recursos directamente en la interfaz de usuario de Recursos. No se muestra el cuadro de diálogo para cambiar el nombre del archivo.
   ![create_menu](assets/create_menu.png)

   Para seleccionar varios archivos, pulse la tecla Ctrl o Comando y seleccione los recursos en el cuadro de diálogo del selector de archivos. Al utilizar un iPad, solo puede seleccionar un archivo a la vez.

<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#

   You can pause the uploading of large assets (greater than 500 MB) and resume it later from the same page. Tap the **[!UICONTROL Pause]** icon beside progress bar that appears when an upload starts.

   ![chlimage_1-211](assets/chlimage_1-211.png)

   The size above which an asset is considered a large asset is configurable. For example, you can configure the system to consider assets above 1000 MB (instead of 500 MB) as large assets. In this case, **[!UICONTROL Pause]** appears on the progress bar when assets of size greater than 1000 MB are uploaded.

   The Pause button does not show if a file greater than 1000 MB is uploaded with a file less than 1000 MB. However, if you cancel the less than 1000 MB file upload, the **[!UICONTROL Pause]** button appears.

   To modify the size limit, configure the `chunkUploadMinFileSize` property of the `fileupload`node in the CRX repository.

   When you click the **[!UICONTROL Pause]** icon, it toggles to a **[!UICONTROL Play]** icon. To resume uploading, click the **[!UICONTROL Play]** icon.

   ![chlimage_1-212](assets/chlimage_1-212.png)
-->

1. Para cancelar una carga en curso, haga clic en Cerrar (`X`) al lado de la barra de progreso. Al cancelar la operación de carga, los AEM Assets eliminan la parte parcialmente cargada del recurso.

   Si cancela la operación de carga antes de que se carguen los archivos, los AEM Assets dejan de cargar el archivo actual y actualizan el contenido. Sin embargo, los archivos que ya se han cargado no se eliminan.


<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#
   The ability to resume uploading is especially helpful in low-bandwidth scenarios and network glitches, where it takes a long time to upload a large asset. You can pause the upload operation and continue later when the situation improves. When you resume, uploading starts from the point where you paused it.
-->

<!-- #ENGCHECK assuming this is not relevant? remove after confirming#
   During the upload operation, AEM saves the portions of the asset being uploaded as chunks of data in the CRX repository. When the upload completes, AEM consolidates these chunks into a single block of data in the repository.

   To configure the cleanup task for the unfinished chunk upload jobs, go to `https://[aem_server]:[port]/system/console/configMgr/org.apache.sling.servlets.post.impl.helper.ChunkCleanUpTask`.
-->


1. El cuadro de diálogo de progreso de carga en AEM Assets muestra el recuento de los archivos cargados correctamente y los archivos que no se pudieron cargar.

Además, la interfaz de usuario de Recursos muestra el recurso más reciente que se ha cargado o la carpeta que se ha creado primero.

>[!NOTE]
>
> Para cargar jerarquías de carpetas anidadas en AEM, consulte Carga [masiva de recursos](#bulk-upload).

<!-- #ENGCHECK I'm assuming this is no longer relevant.... If yes, this should be removed#

### Serial uploads {#serialuploads}

Uploading numerous assets in bulk consumes significant I/O resources, which may adversely impact the performance of your AEM Assets instance. In particular, if you have a slow internet connection, the time to upload drastically increases due to a spike in disk I/O. Moreover, your web browser may introduce additional restrictions to the number of POST requests AEM Assets can handle for concurrent asset uploads. As a result, the upload operation fails or terminate prematurely. In other words, AEM assets may miss some files while ingesting a bunch of files or altogether fail to ingest any file.

To overcome this situation, AEM Assets ingests one asset at a time (serial upload) during a bulk upload operation, instead of the concurrently ingesting all the assets.

Serial uploading of assets is enabled by default. To disable the feature and allow concurrent uploading, overlay the `fileupload` node in Crx-de and set the value of the `parallelUploads` property to `true`.

### Streamed uploads {#streamed-uploads}

If you upload many assets to AEM, the I/O requests to server increase drastically, which reduces the upload efficiency and can even cause some upload task to time out. AEM Assets supports streamed uploading of assets. Streamed uploading reduces the disk I/O during the upload operation by avoiding asset storage in a temporary folder on the server before copying it to the repository. Instead, the data is transferred directly to the repository. This way, the time to upload large assets and the possibility of timeouts is reduced. Streamed upload is enabled by default in AEM Assets.

>[!NOTE]
>
>Streaming upload is disabled for AEM running on JEE server with servlet-api version lower than 3.1.
-->

### Gestión de cargas cuando el recurso ya existe {#handling-upload-existing-file}

Si carga un recurso con el mismo nombre que el de un recurso ya disponible en la ubicación donde está cargando el recurso, se muestra un cuadro de diálogo de advertencia.

Puede elegir reemplazar un recurso existente, crear otra versión o mantener ambos cambiando el nombre del nuevo recurso que se carga. Si sustituye un recurso existente, se eliminarán los metadatos del recurso y las modificaciones anteriores (por ejemplo, anotaciones, recortes, etc.) que haya realizado en el recurso existente. Si decide conservar ambos recursos, se cambiará el nombre del nuevo recurso por el número `1` que se añadirá al nombre.

>[!NOTE]
>
>Al seleccionar **[!UICONTROL Reemplazar]** en el cuadro de diálogo Conflicto [!UICONTROL de] nombres, el ID de recurso se regenera para el nuevo recurso. Este ID es diferente del ID del recurso anterior.
>
>Si Asset Insights está habilitado para rastrear impresiones/clics con Adobe Analytics, el ID de recurso regenerado invalida los datos capturados para el recurso en Analytics.

Para conservar el recurso de duplicado en AEM Assets, toque o haga clic en **[!UICONTROL Mantener]**. Para eliminar el recurso de duplicado que ha cargado, toque o haga clic en **[!UICONTROL Eliminar]**.

### Administración de nombres de archivo y caracteres prohibidos {#filename-handling}

Los AEM Assets evitan que se carguen recursos con los caracteres prohibidos en sus nombres de archivo. Si intenta cargar un recurso con un nombre de archivo que contenga uno o varios caracteres no permitidos, los AEM Assets mostrarán un mensaje de advertencia y detendrán la carga hasta que se eliminen estos caracteres o se carguen con un nombre permitido.

Para adaptarse a las convenciones de nombres de archivo específicas de su organización, el cuadro de diálogo [!UICONTROL Cargar recursos] permite especificar nombres largos para los archivos que cargue.

Sin embargo, no se admiten los siguientes caracteres (lista separada por espacios):

* el nombre del archivo de recurso no debe contener `* / : [ \\ ] | # % { } ? &`
* el nombre de la carpeta de recursos no debe contener `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## Carga masiva de recursos {#bulk-upload}

Para cargar un mayor número de archivos, especialmente si existen en una jerarquía de carpetas anidada en disco, se pueden utilizar los siguientes métodos:

* Utilice un script o una herramienta de carga personalizada que aproveche las API [de carga de](developer-reference-material-apis.md#asset-upload-technical)recursos. Una herramienta personalizada de este tipo puede añadir una gestión adicional de los recursos (por ejemplo, traducir metadatos o cambiar el nombre de los archivos), si es necesario.
* Utilice la aplicación [de escritorio](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html) Experience Manager para cargar jerarquías de carpetas anidadas.

>[!NOTE]
>
> La carga masiva como parte de la migración de contenido desde otros sistemas cuando se configura e implementa en Experience Manager requiere una planificación, consideración y elección cuidadosas de las herramientas. Consulte la guía [de](/help/implementing/deploying/overview.md) implementación para obtener instrucciones sobre los enfoques de migración de contenido.

## Carga de recursos mediante clientes de escritorio {#upload-assets-desktop-clients}

Además de la interfaz de usuario del navegador web, Experience Manager admite otros clientes en el escritorio. También proporcionan una experiencia de carga sin necesidad de ir al navegador web.

* [Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html) proporciona acceso a recursos de AEM en aplicaciones de escritorio de Adobe Photoshop, Adobe Illustrator y Adobe InDesign. Puede cargar el documento abierto actualmente en AEM directamente desde la interfaz de usuario de Adobe Asset Link desde estas aplicaciones de escritorio.
* [La aplicación](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html) de escritorio Experience Manager simplifica el trabajo con los recursos en el escritorio, independientemente del tipo de archivo o la aplicación nativa que los gestione. Resulta especialmente útil cargar archivos en jerarquías de carpetas anidadas desde el sistema de archivos local, ya que la carga del navegador solo admite la carga de listas de archivos planos.

## Procesamiento adicional {#additional-processing}

Para realizar un procesamiento adicional en los recursos cargados, puede utilizar perfiles de perfiles de procesamiento de recursos en la carpeta, en la que se cargan los recursos. Están disponibles en el cuadro de diálogo **[!UICONTROL Propiedades]** de la carpeta.

![assets-folder-properties](assets/assets-folder-properties.png)

Están disponibles los siguientes perfiles:

* [Los perfiles](metadata-profiles.md) de metadatos permiten aplicar propiedades de metadatos predeterminadas a los recursos cargados en esa carpeta
* [Los perfiles](asset-microservices-configure-and-use.md#processing-profiles) de procesamiento permiten aplicar el procesamiento de representaciones y generar representaciones además de las predeterminadas

Además, si Dynamic Media está habilitado en el entorno:

* [Los perfiles](dynamic-media/image-profiles.md) de imagen de Dynamic Media le permiten aplicar a los recursos cargados una configuración de recorte y enfoque específicos (recorte **** inteligente y recorte de píxeles).
* [Los perfiles](dynamic-media/video-profiles.md) de vídeo de Dynamic Media le permiten aplicar perfiles de codificación de vídeo específicos (resolución, formato, parámetros).

>[!NOTE]
>
> El recorte de Dynamic Media y otras operaciones en los recursos no son destructivos, es decir, no cambian el original cargado, sino que proporcionan parámetros para el recorte o la transformación de medios que se debe realizar al entregar los recursos

Para las carpetas que tienen asignado un perfil de procesamiento, el nombre del perfil aparece en la miniatura de la vista de tarjeta. En la vista de lista, el nombre del perfil aparece en la columna Perfil **[!UICONTROL de]** procesamiento.

## Carga o ingesta de recursos mediante API {#upload-using-apis}

Los detalles técnicos de las API y el protocolo de carga, así como los vínculos al SDK de código abierto y a los clientes de muestra, se proporcionan en la sección de carga [de](developer-reference-material-apis.md#asset-upload-technical) recursos de la referencia del desarrollador.

>[!MORELIKETHIS]
>
>* [Aplicación de escritorio de Adobe Experience Manager](https://docs.adobe.com/content/help/es-ES/experience-manager-desktop-app/using/introduction.translate.html)
>* [Adobe Asset Link](https://www.adobe.com/creativecloud/business/enterprise/adobe-asset-link.html)
>* [Documentación de Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html)
>* [Referencia técnica para la carga de recursos](developer-reference-material-apis.md#asset-upload-technical)

