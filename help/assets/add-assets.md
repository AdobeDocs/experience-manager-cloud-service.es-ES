---
title: Agregue los recursos digitales a [!DNL Adobe Experience Manager].
description: Agregue los recursos digitales a [!DNL Adobe Experience Manager] como [!DNL Cloud Service].
feature: Asset Management,Upload
role: User,Admin
exl-id: 0e624245-f52e-4082-be21-13cc29869b64
source-git-commit: 510e71a3bbfb231182ff525415f1e6967723096f
workflow-type: tm+mt
source-wordcount: '2263'
ht-degree: 1%

---

# Añadir recursos digitales a [!DNL Adobe Experience Manager] como [!DNL Cloud Service] [!DNL Assets] {#add-assets-to-experience-manager}

[!DNL Adobe Experience Manager Assets] acepta muchos tipos de recursos digitales de muchas fuentes. Almacena los binarios y las representaciones creadas, puede realizar el procesamiento de recursos mediante diversos flujos de trabajo y [!DNL Adobe Sensei] , permite la distribución a través de muchos canales en muchas superficies.

[!DNL Adobe Experience Manager] enriquece el contenido binario de los archivos digitales cargados con metadatos enriquecidos, etiquetas inteligentes, representaciones y otros servicios de administración de recursos digitales (DAM). Puede cargar varios tipos de archivos, como imágenes, documentos y archivos de imagen sin procesar, desde la carpeta local o una unidad de red a [!DNL Experience Manager Assets].

Además de la carga del explorador más utilizada, existen otros métodos para agregar recursos al [!DNL Experience Manager] existe un repositorio, incluidos los clientes de escritorio, como Adobe Asset Link o [!DNL Experience Manager] aplicación de escritorio, secuencias de comandos de carga e ingesta que los clientes podrían crear e integraciones de ingesta automatizada añadidas como [!DNL Experience Manager] extensiones.

Aunque puede cargar y administrar cualquier archivo binario en [!DNL Experience Manager], los formatos de archivo más utilizados son compatibles con servicios adicionales, como la extracción de metadatos o la generación de vista previa/representación. Consulte [formatos de archivo compatibles](file-format-support.md) para obtener más información.

También puede optar por realizar un procesamiento adicional en los recursos cargados. Se pueden configurar varios perfiles de procesamiento de recursos en la carpeta, en la que se cargan los recursos, para añadir metadatos, representaciones o servicios de procesamiento de imágenes específicos. Consulte [procesar recursos al cargarlos](#process-when-uploaded).

[!DNL Assets] proporciona los siguientes métodos de carga. Adobe recomienda comprender el caso de uso y la aplicabilidad de una opción de carga antes de utilizarla.

| Método de carga | Cuándo se usa? | Personal principal |
|---------------------|----------------|-----------------|
| [Interfaz de usuario de la consola Assets](#upload-assets) | Carga ocasional, facilidad de presionar y arrastrar, carga del buscador. No utilice para cargar un gran número de recursos. | Todos los usuarios |
| [Cargar API](#upload-using-apis) | Para decisiones dinámicas durante la carga. | Desarrollador |
| Aplicación de escritorio de [[!DNL Experience Manager]  ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | Ingesta de recursos de bajo volumen, pero no para migración. | Administrador, experto en marketing |
| [[!DNL Adobe Asset Link]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html) | Resulta útil cuando los creativos y los especialistas en marketing trabajan en recursos dentro de los [!DNL Creative Cloud] aplicaciones de escritorio. | Creativo, experto en marketing |
| [Ingesta masiva de recursos](#asset-bulk-ingestor) | Recomendado para migraciones a gran escala y entradas masivas ocasionales. Solo para almacenes de datos compatibles. | Administrador, Desarrollador |

## Cargar recursos {#upload-assets}

<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#

   You can pause the uploading of large assets (greater than 500 MB) and resume it later from the same page. Tap the **[!UICONTROL Pause]** icon beside progress bar that appears when an upload starts.

   The size above which an asset is considered a large asset is configurable. For example, you can configure the system to consider assets above 1000 MB (instead of 500 MB) as large assets. In this case, **[!UICONTROL Pause]** appears on the progress bar when assets of size greater than 1000 MB are uploaded.

   The [!UICONTROL Pause] option does not show if a file greater than 1000 MB is uploaded with a file less than 1000 MB. However, if you cancel the less than 1000 MB file upload, the **[!UICONTROL Pause]** option appears.

   To modify the size limit, configure the `chunkUploadMinFileSize` property of the `fileupload` node in the CRX repository.

   When you click the **[!UICONTROL Pause]** icon, it toggles to a **[!UICONTROL Play]** icon. To resume uploading, click **[!UICONTROL Play]** option.
-->

<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#
   The ability to resume uploading is especially helpful in low-bandwidth scenarios and network glitches, where it takes a long time to upload a large asset. You can pause the upload operation and continue later when the situation improves. When you resume, uploading starts from the point where you paused it.
-->

<!-- #ENGCHECK assuming this is not relevant? remove after confirming#
   During the upload operation, [!DNL Experience Manager] saves the portions of the asset being uploaded as chunks of data in the CRX repository. When the upload completes, [!DNL Experience Manager] consolidates these chunks into a single block of data in the repository.

   To configure the cleanup task for the unfinished chunk upload jobs, go to `https://[aem_server]:[port]/system/console/configMgr/org.apache.sling.servlets.post.impl.helper.ChunkCleanUpTask`.
-->

Para cargar un archivo (o varios archivos), puede seleccionarlos en el escritorio y arrastrarlos en la interfaz de usuario (explorador web) a la carpeta de destino. También puede iniciar la carga desde la interfaz de usuario.

1. En el [!DNL Assets] , vaya a la ubicación en la que desee agregar recursos digitales.
1. Para cargar los recursos, siga uno de estos procedimientos:

   * En la barra de herramientas, haga clic en **[!UICONTROL Crear]** > **[!UICONTROL Archivos]**. Si es necesario, puede cambiar el nombre del archivo en el cuadro de diálogo presentado.
   * En un explorador compatible con HTML 5, arrastre los recursos directamente sobre la [!DNL Assets] interfaz de usuario. No se muestra el cuadro de diálogo para cambiar el nombre del archivo.

   ![create_menu](assets/create_menu.png)

   Para seleccionar varios archivos, seleccione la opción `Ctrl` o `Command` y seleccione los recursos en el cuadro de diálogo selector de archivos. Al utilizar un iPad, solo puede seleccionar un archivo a la vez.

1. Para cancelar una carga continua, haga clic en cerrar (`X`) junto a la barra de progreso. Al cancelar la operación de carga, [!DNL Assets] elimina la parte cargada parcialmente del recurso.
Si cancela una operación de carga antes de que se carguen los archivos, [!DNL Assets] detiene la carga del archivo actual y actualiza el contenido. Sin embargo, los archivos que ya se han cargado no se eliminan.

1. El cuadro de diálogo de progreso de carga de [!DNL Assets] muestra el recuento de los archivos cargados correctamente y los archivos que no se cargaron correctamente.
Además, la variable [!DNL Assets] interfaz de usuario de muestra el recurso más reciente que ha cargado o la carpeta que ha creado primero.

>[!NOTE]
>
>Para cargar jerarquías de carpetas anidadas, consulte [recursos de carga masiva](#bulk-upload).

<!-- #ENGCHECK I'm assuming this is no longer relevant.... If yes, this should be removed#

### Serial uploads {#serialuploads}

Uploading numerous assets in bulk consumes significant I/O resources, which may adversely impact the performance of [!DNL Assets]. In particular, if you have a slow internet connection, the time to upload drastically increases due to a spike in disk I/O. Moreover, your web browser may introduce additional restrictions to the number of POST requests [!DNL Assets] can handle for concurrent asset uploads. As a result, the upload operation fails or terminate prematurely. In other words, [!DNL Assets] may miss some files while ingesting a bunch of files or altogether fail to ingest any file.

To overcome this situation, [!DNL Assets] ingests one asset at a time (serial upload) during a bulk upload operation, instead of the concurrently ingesting all the assets.

Serial uploading of assets is enabled by default. To disable the feature and allow concurrent uploading, overlay the `fileupload` node in CRX-DE and set the value of the `parallelUploads` property to `true`.

### Streamed uploads {#streamed-uploads}

If you upload many assets to [!DNL Experience Manager], the I/O requests to server increase drastically, which reduces the upload efficiency and can even cause some upload task to time out. [!DNL Assets] supports streamed uploading of assets. Streamed uploading reduces the disk I/O during the upload operation by avoiding asset storage in a temporary folder on the server before copying it to the repository. Instead, the data is transferred directly to the repository. This way, the time to upload large assets and the possibility of timeouts is reduced. Streamed upload is enabled by default in [!DNL Assets].

>[!NOTE]
>
>Streaming upload is disabled for [!DNL Experience Manager] running on JEE server with servlet-api version lower than 3.1.
-->

### Gestión de cargas cuando el recurso ya existe {#handling-upload-existing-file}

Puede cargar un recurso con la misma ruta (el mismo nombre y ubicación) que el de un recurso existente. Sin embargo, se muestra un cuadro de diálogo de advertencia con las siguientes opciones:

* Reemplazar recurso existente: Si reemplaza un recurso existente, se eliminarán los metadatos del recurso y las modificaciones anteriores (por ejemplo, anotaciones, recorte, etc.) que haya realizado en el recurso existente.
* Cree otra versión: Se crea una nueva versión del recurso existente en el repositorio. Puede ver las dos versiones en la [!UICONTROL Cronología] y pueden volver a la versión existente anteriormente si es necesario.
* Mantenga ambos: Si decide conservar ambos recursos, se cambiará el nombre del nuevo recurso.

Para conservar el recurso duplicado en [!DNL Assets], haga clic en **[!UICONTROL Keep]**. Para eliminar el recurso duplicado que ha cargado, haga clic en **[!UICONTROL Eliminar]**.

### Tratamiento de nombres de archivo y caracteres prohibidos {#filename-handling}

[!DNL Experience Manager Assets] intenta evitar cargar recursos con los caracteres prohibidos en sus nombres de archivo. Si intenta cargar un recurso con un nombre de archivo que contenga uno o más caracteres no permitidos, [!DNL Assets] muestra un mensaje de advertencia y detiene la carga hasta que elimina estos caracteres o carga con un nombre permitido.

Para adaptarlo a las convenciones específicas de nomenclatura de archivos de su organización, la variable [!UICONTROL Cargar recursos] permite especificar nombres largos para los archivos que se cargan. No se admiten los siguientes caracteres (lista de) separados por espacios:

* caracteres no válidos para el nombre del archivo de recursos `* / : [ \\ ] | # % { } ? &`
* caracteres no válidos para el nombre de la carpeta de recursos `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## Carga masiva de recursos {#bulk-upload}

El importador masivo de recursos puede gestionar un gran número de recursos de forma eficaz. Sin embargo, una ingesta a gran escala no es solo un volcado de archivos amplio o una migración casual. Para que una ingesta a gran escala sea un proyecto significativo que satisfaga sus objetivos comerciales y sea eficaz, planifique la migración y depure la organización de recursos. Todas las ingestas son diferentes, por lo que en lugar de generalizar, tienen en cuenta la composición matizada del repositorio y las necesidades del negocio. A continuación se presentan algunas sugerencias generales para planificar y ejecutar una ingesta masiva:

* Depurar recursos: Elimine los recursos que no sean necesarios en DAM. Considere la posibilidad de eliminar recursos no utilizados, obsoletos o duplicados. Esto reduce la transferencia de datos y la ingesta de recursos, lo que permite una ingesta más rápida.
* Organizar recursos: Considere la posibilidad de organizar el contenido en un orden lógico, por ejemplo, por tamaño de archivo, formato de archivo, caso de uso o prioridad. En general, los archivos complejos de gran tamaño requieren más procesamiento. También puede considerar la ingesta de archivos grandes por separado utilizando la opción de filtrado de tamaño de archivo (que se describe a continuación).
* Ingestas más grandes: Considere la posibilidad de dividir la ingesta en varios proyectos de ingesta masiva. Esto le permite ver el contenido antes y actualizar su ingesta según sea necesario. Por ejemplo, puede ingerir recursos con gran densidad de procesamiento durante las horas de menor actividad o de forma gradual en varios fragmentos. Sin embargo, puede ingerir recursos más pequeños y simples que no requieran mucho procesamiento de una sola vez.

Para cargar un mayor número de archivos, utilice uno de los siguientes métodos. Consulte también la [casos de uso y métodos](#upload-methods-comparison)

* [API de carga de recursos](developer-reference-material-apis.md#asset-upload): Utilice un script de carga personalizado o una herramienta que aproveche las API para agregar un control adicional de los recursos (por ejemplo, traducir metadatos o cambiar el nombre de archivos), si es necesario.
* [[!DNL Experience Manager] aplicación de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html): Útil para los profesionales creativos y los especialistas en marketing que cargan recursos desde su sistema de archivos local. Utilícelo para cargar carpetas anidadas disponibles localmente.
* [Herramienta de ingesta masiva](#asset-bulk-ingestor): Se utiliza para la ingesta de grandes cantidades de recursos, ya sea ocasionalmente o inicialmente al implementar [!DNL Experience Manager].

### Herramienta de ingesta masiva de recursos {#asset-bulk-ingestor}

La herramienta solo se proporciona al grupo de administradores para su uso en ingesta a gran escala de recursos de los almacenes de datos de Azure o S3. Consulte un vídeo de introducción a la configuración y la ingesta.

>[!VIDEO](https://video.tv.adobe.com/v/329680/?quality=12&learn=on)

Para configurar la herramienta, siga estos pasos:

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Importación masiva]**. Seleccione el **[!UICONTROL Crear]** .

![Configuración del importador masivo](assets/bulk-import-config.png)

1. Activado **[!UICONTROL configuración de importación masiva]** , proporcione los valores necesarios y, a continuación, seleccione **[!UICONTROL Guardar]**.

   * [!UICONTROL Título]: Un título descriptivo.
   * [!UICONTROL Importar origen]: Seleccione la fuente de datos aplicable.
   * [!UICONTROL Cuenta de almacenamiento de Azure]: Proporcione el nombre del [!DNL Azure] cuenta de almacenamiento.
   * [!UICONTROL Contenedor de Azure Blob]: Proporcione la variable [!DNL Azure] contenedor de almacenamiento.
   * [!UICONTROL Clave de acceso de Azure]: Proporcione la clave de acceso a [!DNL Azure] cuenta.
   * [!UICONTROL Carpeta de origen]: Este filtro suele ser compatible con los proveedores de almacenamiento en la nube de Azure y AWS.
   * [!UICONTROL Filtrar por tamaño mínimo]: Proporcione un tamaño de archivo mínimo de los recursos en MB.
   * [!UICONTROL Filtrar por tamaño máximo]: Proporcione el tamaño máximo de archivo de los recursos en MB.
   * [!UICONTROL Excluir tipos de mime]: Lista de tipos MIME separados por comas que se excluirán de la ingesta. Por ejemplo, `image/jpeg, image/.*, video/mp4`. Consulte [todos los formatos de archivo compatibles](/help/assets/file-format-support.md).
   * [!UICONTROL Incluir tipos de MIME]: Lista de tipos MIME separados por comas que se incluirán en la ingesta. Consulte [todos los formatos de archivo compatibles](/help/assets/file-format-support.md).
   * [!UICONTROL Eliminar archivo de origen después de la importación]: Seleccione esta opción para eliminar los archivos originales del almacén de datos de origen después de importar los archivos en [!DNL Experience Manager].
   * [!UICONTROL Modo de importación]: Seleccione Omitir, Reemplazar o Crear versión. El modo Omitir es el predeterminado y en este modo el ingestor omite importar un recurso si ya existe. Ver el significado de [reemplazar y crear opciones de versión](#handling-upload-existing-file).
   * [!UICONTROL Carpeta de destino de recursos]: Importar carpeta en DAM donde se van a importar los recursos. Por ejemplo, `/content/dam/imported_assets`
   * [!UICONTROL Archivo de metadatos]: El archivo de metadatos que se va a importar, proporcionado en formato CSV. Especifique el archivo CSV en la ubicación del blob de origen y consulte la ruta al configurar la herramienta Ingesta masiva. El formato de archivo CSV al que se hace referencia en este campo es el mismo que el del formato de archivo CSV cuando [Importación y exportación metadatos de recursos de forma masiva](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/metadata-import-export.html). Si selecciona la opción **Eliminar archivo de origen después de la importación** , filtre los archivos CSV utilizando la opción **Excluir** o **Incluir tipo MIME** o **Filtrar por ruta/archivo** campos. Puede utilizar una expresión regular para filtrar archivos CSV en estos campos.

1. Puede eliminar, modificar, ejecutar y hacer más con las configuraciones de ingestor creadas. Cuando selecciona una configuración de ingestor de importación masiva, las siguientes opciones están disponibles en la barra de herramientas.

   * [!UICONTROL Editar]: Edite la configuración seleccionada.
   * [!UICONTROL Eliminar]: Eliminar la configuración seleccionada.
   * [!UICONTROL Marque]: Valide la conexión con el almacén de datos.
   * [!UICONTROL Ensayo]: Invoque una ejecución de prueba de la ingesta masiva.
   * [!UICONTROL Ejecutar]: Ejecute la configuración seleccionada.
   * [!UICONTROL Stop]: Finalice una configuración activa.
   * [!UICONTROL Programación]: Defina una programación recurrente o única para la ingesta de recursos.
   * [!UICONTROL Estado del trabajo]: Ver el estado de la configuración cuando se utiliza en un trabajo de importación en curso o se utiliza para un trabajo completado.
   * [!UICONTROL Historial de trabajos]: Instancias anteriores del trabajo.
   * [!UICONTROL Ver recursos]: Ver la carpeta de destino si existe.

   ![Opciones de barra de herramientas para configuraciones de ingestor](assets/bulk-ingest-toolbar-options.png)

Para programar una importación masiva única o recurrente, siga estos pasos:

1. Cree una configuración de importación masiva.
1. Seleccione la configuración y seleccione **[!UICONTROL Programación]** en la barra de herramientas.
1. Establezca una ingesta única o programe una programación por hora, diaria o semanal. Haga clic en **[!UICONTROL Submit]**.

   ![Programar trabajo de ingesta masiva](assets/bulk-ingest-schedule1.png)

## Carga de recursos mediante clientes de escritorio {#upload-assets-desktop-clients}

Además de la interfaz de usuario del explorador web, [!DNL Experience Manager] admite otros clientes en el escritorio. También proporcionan una experiencia de carga sin necesidad de ir al explorador web.

* [[!DNL Adobe Asset Link]](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html) proporciona acceso a los recursos desde [!DNL Experience Manager] en aplicaciones de escritorio de Adobe Photoshop, Adobe Illustrator y Adobe InDesign. Puede cargar el documento abierto actualmente en [!DNL Experience Manager] directamente desde la interfaz de usuario de Adobe Asset Link desde estas aplicaciones de escritorio.
* [[!DNL Experience Manager] aplicación de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) simplifica el trabajo con recursos en el escritorio, independientemente de su tipo de archivo o aplicación nativa que los gestione. Resulta especialmente útil cargar archivos en jerarquías de carpetas anidadas desde el sistema de archivos local, ya que la carga del explorador solo admite la carga de listas de archivos planos.

## Procesar recursos al cargarlos {#process-when-uploaded}

Para realizar un procesamiento adicional en los recursos cargados, puede aplicar perfiles de procesamiento en las carpetas de carga. Los perfiles están disponibles en la **[!UICONTROL Propiedades]** página de una carpeta de [!DNL Assets]. Un recurso digital sin extensión o con una extensión incorrecta no se procesa como desee. Por ejemplo, al cargar estos recursos, puede que no suceda nada o que se aplique un perfil de procesamiento incorrecto al recurso. Los usuarios aún pueden almacenar los archivos binarios en DAM.

![Propiedades de una carpeta de recursos con opciones para agregar un perfil de procesamiento](assets/assets-folder-properties.png)

Las fichas disponibles son las siguientes:

* [Perfiles de metadatos](metadata-profiles.md) permite aplicar propiedades de metadatos predeterminadas a los recursos cargados en esa carpeta.
* [Perfiles de procesamiento](asset-microservices-configure-and-use.md) permite generar más representaciones de las posibles de forma predeterminada.

Además, si [!DNL Dynamic Media] en la implementación, están disponibles las siguientes pestañas:

* [[!DNL Dynamic Media] Perfiles de imagen](dynamic-media/image-profiles.md) permite aplicar recortes específicos (**[!UICONTROL Recorte inteligente]** y recorte de píxeles) y configuración de nitidez en los recursos cargados.
* [[!DNL Dynamic Media] Perfiles de vídeo](dynamic-media/video-profiles.md) permite aplicar perfiles de codificación de vídeo específicos (resolución, formato, parámetros).

>[!NOTE]
>
>[!DNL Dynamic Media] el recorte y otras operaciones en los recursos no son destructivas, es decir, las operaciones no cambian el original cargado. En su lugar, proporciona parámetros para recortar o transformar al enviar los recursos.

Para las carpetas que tienen asignado un perfil de procesamiento, el nombre del perfil aparece en la miniatura de la vista de tarjeta. En la vista de lista, el nombre del perfil aparece en la **[!UICONTROL Perfil de procesamiento]** para abrir el Navegador.

## Carga o ingesta de recursos mediante API {#upload-using-apis}

Se proporcionan detalles técnicos sobre las API de carga y el protocolo, así como vínculos al SDK de código abierto y a clientes de muestra en [carga de recursos](developer-reference-material-apis.md#asset-upload) de la referencia del desarrollador.

## Sugerencias, prácticas recomendadas y limitaciones {#tips-limitations}

* La carga binaria directa es un nuevo método para cargar recursos. Es compatible de forma predeterminada con las capacidades del producto y los clientes, como [!DNL Experience Manager] interfaz de usuario, [!DNL Adobe Asset Link]y [!DNL Experience Manager] aplicación de escritorio. Cualquier código personalizado que los equipos técnicos de los clientes personalicen o amplíen debe utilizar las nuevas API y protocolos de carga.

* Adobe recomienda añadir no más de 1000 activos en cada carpeta de [!DNL Experience Manager Assets]. Aunque puede agregar más recursos a una carpeta, es posible que experimente problemas de rendimiento como una navegación más lenta a dichas carpetas.

* Al seleccionar **[!UICONTROL Reemplazar]** en el [!UICONTROL Conflicto de nombres] , el ID de recurso se regenera para el nuevo recurso. Este ID es diferente del ID del recurso anterior. If [Información sobre Assets](/help/assets/assets-insights.md) está habilitado para rastrear impresiones o clics con [!DNL Adobe Analytics], el ID de recurso regenerado invalida los datos capturados para el recurso en [!DNL Analytics].

* Algunos métodos de carga no le impiden cargar recursos con [caracteres prohibidos](#filename-handling) en los nombres de archivo. Los caracteres se sustituyen por `-` símbolo.

* La carga de recursos mediante el explorador solo admite listas de archivos planos y no jerarquías de carpetas anidadas. Para cargar todos los recursos dentro de una carpeta anidada, considere la posibilidad de utilizar [aplicación de escritorio](#upload-assets-desktop-clients).

* El método de importación masiva importa toda la estructura de carpetas tal como existe en el origen de datos. Sin embargo, solo se crean las carpetas que no están vacías en [!DNL Experience Manager].


<!-- TBD: Link to file name handling in DA docs when it is documented. 
-->

>[!MORELIKETHIS]
>
>* Aplicación de escritorio de [[!DNL Adobe Experience Manager]  ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html)
>* [Acerca de [!DNL Adobe Asset Link]](https://www.adobe.com/creativecloud/business/enterprise/adobe-asset-link.html)
>* [[!DNL Adobe Asset Link] documentación.](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)
>* [Referencia técnica para la carga de recursos](developer-reference-material-apis.md#asset-upload)

