---
title: Utilice el Asesor de contenido para acceder a los AEM Assets de Adobe Express
description: Utilice el Asesor de contenido para detectar y acceder a los AEM Assets directamente desde la integración nativa de Adobe Express.
exl-id: d43e4451-da2a-444d-9aa4-4282130ee44f
feature: Collaboration
role: User
source-git-commit: 54e66597d60621743cb39ef0b8edb21b6eea6c8d
workflow-type: tm+mt
source-wordcount: '2514'
ht-degree: 0%

---

# Utilice el Asesor de contenido para acceder a los AEM Assets de Adobe Express {#native-integration-adobe-express-using-content-advisor}

Adobe Experience Manager (AEM) Assets se integra de forma nativa con Adobe Express, lo que le permite detectar, acceder y utilizar recursos de AEM Assets directamente en la interfaz Express mediante el Asesor de contenido.

El Asesor de contenido transforma la forma en que descubre y utiliza los recursos en Adobe Express al llevar la detección de recursos inteligente y según el contexto directamente a su flujo de trabajo creativo. En lugar de buscar recursos escribiendo palabras clave, el Asesor de contenido muestra recursos relevantes y aprobados en función del contenido del lienzo, el resumen de la campaña y la intención, lo que le ayuda a encontrar el recurso adecuado más rápido.

Con sugerencias inteligentes, acceso a representaciones de Dynamic Media y una visibilidad completa de los metadatos de recursos, el Asesor de contenido le permite localizar, evaluar y utilizar recursos de AEM Assets de forma eficaz sin salir de Adobe Express. Esto garantiza una creación de contenido más rápida, una reutilización de recursos mejorada y un uso coherente de recursos aprobados y compatibles con la marca.

![Imagen de titular del Asesor de contenido](assets/content-advisor-banner-image.png)

También puede colocar recursos en el lienzo rápido y guardar contenido nuevo o editado en los AEM Assets, lo que garantiza una administración y un control centralizados de los recursos. La integración nativa con Adobe Express ofrece las siguientes ventajas clave:

* Creación de contenido acelerada con detección de recursos según el contexto y recomendaciones.

* Se ha aumentado la reutilización del contenido al editar los recursos existentes y guardar nuevos recursos en los AEM Assets.

* Acceso más rápido a representaciones de Dynamic Media aprobadas y optimizadas para el canal.

* Se ha reducido el tiempo y el esfuerzo para crear nuevos recursos o versiones sin perder la coherencia de la marca.

## Requisitos previos {#prerequisites}

Derechos para acceder a Adobe Express y al menos a un entorno dentro de los AEM Assets. El entorno puede ser cualquiera de los repositorios de Assets as a Cloud Service.

## Uso de AEM Assets en el editor de Adobe Express {#use-aem-assets-in-express}

Siga estos pasos para empezar a utilizar AEM Assets en el editor de Adobe Express:

1. Abra la aplicación web de Adobe Express.

2. Abra un nuevo lienzo en blanco cargando una nueva plantilla o proyecto, o creando un recurso.

3. Haga clic en **[!UICONTROL Assets]**, disponible en el panel de navegación izquierdo. Adobe Express muestra [Asesor de contenido](#intelligent-asset-discovery-content-advisor), que enumera los repositorios a los que tiene derecho de acceso junto con la lista de recursos y carpetas disponibles en el nivel raíz.

4. Examine o busque recursos en su repositorio con [Asesor de contenido](#intelligent-asset-discovery-content-advisor) y arrástrelos y suéltelos en el lienzo. También puede hacer clic en los recursos para colocarlos en el lienzo. También puede filtrar los recursos ![filter](assets/do-not-localize/filter.svg) según varios criterios, como el estado de aprobación, el tipo de archivo, el tipo MIME y las dimensiones.

   >[!NOTE]
   >
   >El filtro por dimensión no se aplica a los vídeos.

   ![Incluir recursos del complemento Recursos](assets/native-express-content-advisor-home.png)

## Detección inteligente de recursos con el Asesor de contenido {#intelligent-asset-discovery-content-advisor}

El Asesor de contenido le ayuda a descubrir recursos relevantes mediante recomendaciones inteligentes según el contexto, basadas en el contenido del lienzo o en los informes de la campaña. También le permite seleccionar representaciones de Dynamic Media listas para el canal optimizadas para su caso de uso.


El Asesor de contenido muestra la lista de archivos, carpetas y colecciones en las vistas Lista y Cuadrícula. Permite agregar recursos en los formatos PNG, JPEG, PSD, MP4, SVG y PDF al lienzo Express. También puede obtener una vista previa de los archivos PDF desplazables o de cualquier otro tipo de formato haciendo clic en el icono ![Información](assets/info-icon.svg) disponible en la tarjeta de recursos.

Haga clic en el icono ![Información](assets/info-icon.svg) para ver también los metadatos de recursos disponibles en la pestaña **[!UICONTROL Básico]** o las representaciones de Dynamic Media disponibles en la pestaña [Dynamic Media](#dynamic-media-renditions-content-advisor). Arrastre y suelte el contenido sugerido en el lienzo. También puede hacer clic en el recurso para colocarlos automáticamente en el lienzo.

![Metadatos de recursos en Adobe Express](assets/express-native-integration-metadata.png)


>[!IMPORTANT]
> 
>Asegúrese de seleccionar un repositorio **author** de la lista desplegable **Repository**. Un repositorio **delivery** no muestra las características del Asesor de contenido.
>
> Además, el repositorio **delivery** no tiene recursos organizados en carpetas y colecciones. Todos los recursos se muestran en el nivel raíz en una estructura plana.

El Asesor de contenido proporciona las siguientes funciones clave:

* [Búsqueda por IA para una detección de recursos más inteligente](#content-advisor-ai-search)

* [Sugerencias inteligentes basadas en el contexto y la intención](#smart-suggestions-content-advisor)

* [Información de Campaign para descubrir recursos relevantes](#campaign-briefs-content-advisor)

* [Representaciones de recursos de Dynamic Media disponibles para su uso](#dynamic-media-renditions-content-advisor)

* [Acceso a metadatos de recursos coherente con la vista de Assets](#asset-metadata-content-advisor)

* [Filtros de acceso coherentes con la vista de Assets](#filters-content-advisor)

* [Acceder y reutilizar búsquedas recientes y guardadas](#saved-searches-content-advisor)

* [Buscar recursos en y entre colecciones](#search-collections-content-advisor)

### Búsqueda por IA para una detección de recursos más inteligente {#content-advisor-ai-search}

El Asesor de contenido utiliza una capacidad de búsqueda avanzada que comprende el significado y la intención detrás de la consulta de un usuario, en lugar de depender de coincidencias de palabras clave exactas. Utiliza la inteligencia artificial (IA) y el aprendizaje automático para ofrecer resultados más precisos y sensibles al contexto.

A diferencia de la búsqueda tradicional basada en palabras clave, que busca términos exactos, la Búsqueda por IA interpreta las relaciones entre palabras, conceptos e intención del usuario. Esto garantiza que los usuarios encuentren lo que están buscando, incluso si su consulta está redactada de forma diferente, contiene errores tipográficos o está en otro idioma.

![Búsqueda por IA para recursos en Adobe Express](assets/express-native-integration-ai-search.png)

Algunos de sus beneficios clave incluyen:

* Asistencia multilingüe: busque en varios idiomas sin necesidad de traducciones exactas. Los usuarios pueden encontrar contenido relevante independientemente del idioma de la consulta.

* Maneja errores ortográficos: Interpreta errores ortográficos y ortográficos, lo que garantiza resultados precisos incluso con entradas imperfectas.

* Comprende los sinónimos: Proporciona resultados para términos y frases relacionados, de modo que los usuarios no necesitan adivinar la palabra clave correcta.

* Búsqueda según el contexto: Reconoce la intención detrás de una consulta, no solo las palabras exactas.

>[!IMPORTANT]
> 
>* La versión mínima requerida de AEM para acceder a la Búsqueda por IA en el Asesor de contenido es `21994`.


### Sugerencias inteligentes basadas en el contexto y la intención {#smart-suggestions-content-advisor}

El Asesor de contenido muestra sugerencias inteligentes basadas en el contexto y la intención del contenido en el lienzo Express. Esto le ayuda a descubrir y utilizar rápidamente recursos que se alinean con sus necesidades de contenido sin la laboriosa búsqueda manual.

![Contenido sugerido del Asesor de contenido en Adobe Express](assets/express-native-integration-suggested-content.png)

>[!IMPORTANT]
> 
>* El Asesor de contenido muestra sugerencias inteligentes basadas en el contexto y la intención del contenido disponible en las capas de texto o en el título del lienzo Express. No muestra los resultados en función de las imágenes disponibles en el lienzo.
>* Debe firmar a un piloto de GenAI para acceder a esta función dentro del Asesor de contenido. Para firmar GenAI rider, póngase en contacto con su representante de Adobe.
>* La versión mínima de AEM requerida para acceder a esta función es `21994`.
>* Las sugerencias inteligentes no se actualizan automáticamente al actualizar el lienzo. Haga clic en el icono de actualización en el panel **Contenido sugerido** para ver la lista actualizada de sugerencias,

### Información de Campaign para descubrir recursos relevantes {#campaign-briefs-content-advisor}

El Asesor de contenido le permite cargar un documento de resumen de campaña para descubrir recursos relevantes sin introducir manualmente las palabras clave de búsqueda. El Asesor de contenido analiza la información de la información de la campaña para comprender la intención de la campaña y recomienda los activos relevantes disponibles en los AEM Assets.

![Incluir recursos del complemento Recursos](assets/upload-brief-native-express.png)

>[!IMPORTANT]
>
>* El Asesor de contenido analiza la información disponible como texto en la información de la campaña para recomendar recursos relevantes. No analiza la información disponible como imágenes en la información de la campaña.
>* Los tipos de archivo admitidos que puede cargar como resumen de campaña incluyen documentos PDF, DOCX y TXT.
>* Debe firmar a un piloto de GenAI para acceder a esta función dentro del Asesor de contenido. Para firmar GenAI rider, póngase en contacto con su representante de Adobe.
>* La versión mínima de AEM requerida para acceder a esta función es `21994`.

### Representaciones de recursos de Dynamic Media disponibles para su uso {#dynamic-media-renditions-content-advisor}

Las representaciones de Dynamic Media proporcionan versiones de recursos listas para usar y optimizadas para el canal, incluidos [ajustes preestablecidos de imagen](/help/assets/dynamic-media/managing-image-presets.md), [recortes inteligentes](/help/assets/dynamic-media/image-profiles.md), tipos de formato y perfiles de color. Estas representaciones ayudan a garantizar que el recurso seleccionado cumpla los requisitos de canal y diseño sin necesidad de editar manualmente o duplicar recursos.

También puede aplicar modificadores de Dynamic Media para previsualizar los ajustes en tiempo real antes de colocar la representación en el lienzo rápido, lo que permite una selección más rápida de la representación más adecuada y, al mismo tiempo, mantener la coherencia y la calidad del recurso.

Haga clic en el icono ![Información](assets/info-icon.svg) de la tarjeta de recursos y seleccione la pestaña **[!UICONTROL Dynamic Media]** para ver las representaciones disponibles de un recurso. Puede seleccionar ver [representaciones de Dynamic Media Scene7](/help/assets/dynamic-media/dynamic-media.md) o [Dynamic Media con representaciones de OpenAPI](/help/assets/dynamic-media-open-apis-overview.md). Al seleccionar **[!UICONTROL OpenAPI]** para un recurso, las representaciones disponibles solo se mostrarán si el recurso está aprobado y disponible para Dynamic Media con OpenAPI.

Debe tener una licencia de Dynamic Media de AEM válida para ver la pestaña Dynamic Media.

![Ver representaciones de Dynamic Media](assets/native-express-dynamic-media.png)

Haga clic en el icono ![vista previa](assets/do-not-localize/preview-icon.svg) para obtener una vista previa de la representación o haga clic en el nombre de la representación para colocarlos automáticamente en el lienzo. También puede obtener una vista previa de la representación y, a continuación, arrastrarla y soltarla para colocar la imagen en el lienzo.

![Previsualizar representaciones de Dynamic Media](assets/native-express-dynamic-media-preview.png)

Haga clic en **[!UICONTROL Agregar modificadores]**, especifique un modificador en el cuadro de texto y presione Entrar para aplicar la transformación a las representaciones en tiempo real. Del mismo modo, puede agregar varios modificadores a una representación y previsualizar esas transformaciones. Arrastre y suelte el recurso de la vista previa en el lienzo. La representación después de aplicar esos modificadores no se guarda. Consulte la lista de modificadores admitidos para [Dynamic Media Scene7](https://experienceleague.adobe.com/es/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference) y [Dynamic Media con OpenAPI](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat).

>[!IMPORTANT]
> 
>Dynamic Media ayuda a superar la limitación de tamaño de archivo de carga de 80 MB en Adobe Express (web) al proporcionar representaciones optimizadas de recursos grandes. Las representaciones de Dynamic Media reducen significativamente el tamaño del archivo y conservan la calidad visual. Por ejemplo, un recurso de TIFF de 300 MB se puede entregar como una representación de 2,5 MB sin poner en riesgo la calidad, lo que permite un uso eficiente de los recursos de alta resolución en Adobe Express.

### Acceso a metadatos de recursos coherente con la vista de Assets {#asset-metadata-content-advisor}

El Asesor de contenido proporciona acceso a las propiedades de recursos definidas en los AEM Assets, incluidos los metadatos disponibles en la vista de Assets. El Asesor de contenido utiliza la misma configuración de metadatos que en la vista de Assets, replicando la lista de pestañas de metadatos y el contenido en la página de detalles del recurso de la vista de Assets. Esto le permite revisar detalles clave del recurso, como el título, la descripción, el formato, el tamaño y otros metadatos, antes de seleccionar un recurso. El acceso a las propiedades del recurso le ayuda a asegurarse de que elige el recurso correcto y aprobado para su contenido.

![Assets ve los metadatos en el Asesor de contenido](assets/native-express-asset-metadata.png)

Haga clic en el icono ![Información](assets/info-icon.svg) de la tarjeta de recursos y seleccione la pestaña **[!UICONTROL Básico]** para ver los metadatos de los recursos. También puede ver otras pestañas de metadatos de recursos, como Producto, Campaña y Etiquetas, en consonancia con los metadatos de recursos que existen en la vista de Assets.

El Asesor de contenido muestra las propiedades (metadatos) de los archivos en una vista de sólo lectura. Las propiedades no se muestran para colecciones y carpetas.

### Filtros de acceso coherentes con la vista de Assets {#filters-content-advisor}

El Asesor de contenido proporciona las mismas capacidades de filtrado en Express que están disponibles en la vista de Assets, lo que permite refinar los recursos mediante filtros predefinidos. Las mismas capacidades de filtrado que están disponibles en la vista Assets también se aplican a los filtros específicos de los tipos de contenido, como archivos, carpetas y colecciones. Esto garantiza una experiencia de detección de recursos coherente y le ayuda a localizar de forma eficaz los recursos relevantes en Adobe Express.

Si no tiene filtros configurados en la vista de Assets mediante el esquema de filtros, el Asesor de contenido muestra filtros predeterminados, incluidos el tipo de archivo, el formato de archivo, el estado del recurso, el tamaño de archivo, el ancho de la imagen, el alto de la imagen, la fecha de modificación y la fecha de creación.

### Acceder y reutilizar búsquedas recientes y guardadas {#saved-searches-content-advisor}

Las búsquedas guardadas creadas en la vista de Assets también están disponibles, lo que permite reutilizar criterios de búsqueda predefinidos. Las búsquedas guardadas funcionan de forma coherente entre la vista de Assets y el Asesor de contenido en todos los exploradores. Esto le ayuda a localizar recursos de forma eficaz mediante patrones de búsqueda coherentes entre AEM Assets y Adobe Express.

Para guardar la búsqueda utilizada con frecuencia mediante el Asesor de contenido:

1. Especifique un término de búsqueda (opcional), haga clic en el icono de filtros y seleccione las opciones según sus necesidades para crear una consulta de búsqueda.

1. Haga clic en **[!UICONTROL Aplicar]** para ver los resultados.

1. Haga clic en el icono de filtros > **Administrar búsquedas guardadas** > **Crear nueva búsqueda guardada**.

1. Especifique el nombre de la búsqueda y haga clic en ![Icono de información](assets/do-not-localize/checkmark-icon.svg) para guardarla. La búsqueda se muestra en la lista de elementos.

   ![Asesor de contenido de búsquedas guardadas](assets/native-express-saved-searches.png)

Para aplicar cualquiera de los elementos de búsqueda guardados, haga clic en el icono de filtros, seleccione el elemento de búsqueda en la lista desplegable **[!UICONTROL Búsquedas guardadas]** y haga clic en **[!UICONTROL Aplicar]**.

El Asesor de contenido guarda sus búsquedas recientes y también le permite guardar las búsquedas usadas con frecuencia para acceder rápidamente más adelante. La lista de búsquedas recientes no es coherente entre la vista de Assets y el Asesor de contenido. El mismo usuario puede tener un conjunto diferente de búsquedas recientes en la vista de Assets y en el Asesor de contenido. Si utiliza el modo de incógnito para acceder al Asesor de contenido, la lista de búsquedas recientes no está disponible. Además, las búsquedas recientes no se comparten en distintos exploradores para el mismo usuario y son específicas del entorno de AEM.



La función Búsqueda guardada predeterminada, disponible en la vista de Assets, aún no está disponible en el Asesor de contenido.

### Buscar recursos en y entre colecciones {#search-collections-content-advisor}

El Asesor de contenido le permite buscar recursos o colecciones en todas las colecciones o limitar la búsqueda a una colección específica. Esto le ayuda a localizar y utilizar rápidamente recursos de colecciones depuradas, conservando el contexto organizativo deseado.

## Reemplazar imagen al cargar AEM {#replace-image-using-aem-upload}

Además, puede reemplazar las imágenes agregadas usando **[!UICONTROL Carga de AEM]**. Para ello, ejecute los siguientes pasos:

1. Examine o busque recursos y arrástrelos y suéltelos en el lienzo.

1. Seleccione la imagen que desea reemplazar. Haga clic en **[!UICONTROL Reemplazar]** y seleccione **[!UICONTROL AEM Assets]** entre otras opciones.

   ![Reemplazar AEM](assets/aem-replace.png)

1. [El Asesor de contenido](#intelligent-asset-discovery-content-advisor) se abre en el panel de navegación izquierdo. Adobe Express muestra la lista de repositorios a los que puede acceder junto con la lista de recursos y carpetas disponibles en el nivel raíz. Seleccione un recurso desde allí para previsualizar el reemplazo en el lienzo y luego haga clic en **[!UICONTROL Reemplazar]** para confirmar.

   >[!NOTE]
   >
   > Los tipos de archivo de SVG no son compatibles.

## Guardar proyectos de Adobe Express en AEM Assets {#save-express-projects-in-assets}

Después de incorporar las modificaciones adecuadas en el lienzo Express, puede guardarlo en AEM Assets.

1. Haga clic en **[!UICONTROL Compartir]** para abrir el cuadro de diálogo **[!UICONTROL Compartir]**.

   ![Guardar recursos en AEM](assets/adobe-express-share.png)

2. Seleccionar **AEM Assets**. Adobe Express muestra el cuadro de diálogo de carga.

3. Seleccione **Página actual** o **Todas las páginas**. Especifique un nombre y un formato para los recursos que desea exportar. Puede exportar el contenido del lienzo en los formatos PNG, JPEG, PDF, MP4, MP4+PNG o MP4+JPEG. El formato se ajusta automáticamente en función de los recursos de las páginas de lienzo.
Al seleccionar **Página actual**, se guardará el recurso de la página actual en la carpeta de destino. Si selecciona **Todas las páginas** y el formato de exportación no es PDF, todas las páginas de lienzo se guardarán como archivos independientes en una nueva carpeta dentro de la carpeta de destino. Si el formato de exportación es PDF, todas las páginas de lienzo se guardan como un solo archivo PDF en la carpeta de destino.

4. Haga clic en el icono de la carpeta en **Carpeta de destino** para seleccionar una ubicación y guardar los recursos.

   ![Guardar recursos en AEM](/help/assets/assets/page-selection-and-destination-folder.png)

5. Opcional: puede agregar metadatos de campaña para la carga mediante el campo **Nombre del proyecto o de la campaña**. Puede utilizar un nombre existente o crear uno nuevo. Puede definir varios nombres de proyecto o campaña para la carga. Para registrar el nombre, simplemente escriba el nombre y pulse Intro.
Como práctica recomendada, Adobe recomienda especificar valores en el resto de los campos, así como crear una experiencia de búsqueda mejorada para los recursos cargados.

6. Del mismo modo, defina los valores para los campos **[!UICONTROL Palabras clave]** y **[!UICONTROL Canales]**.

7. Haga clic en **[!UICONTROL Cargar]** para cargar los recursos a los AEM Assets.

   <table> 
    <tbody>
     <tr>
      <th><strong>Formatos compatibles</strong></th>
      <th><strong>Tamaño</strong></th>
     </tr>
    </tr>
    <tr>
        <td>[!UICONTROL JPEG]</td>
        <td> 65 MP (por ejemplo, 8 K x 8 K o 16 K x 4 K) </td>
    </tr>
    <tr>
        <td>[!UICONTROL PNG]</td>
        <td> 65 MP (por ejemplo, 8 K x 8 K o 16 K x 4 K) </td>
    </tr>
    <tr>
        <td>[!UICONTROL SVG]</td>
        <td> Máximo 250 KB</td>
    </tr>
    <tr>
        <td>[!UICONTROL MP4]</td>
        <td> 3840 X 3840 píxeles, máximo 200 MB</td>
    </tr>
    <tr>
      <td colspan="2"> <i>: el tamaño del recurso debe ser inferior a 80 MB para dispositivos de escritorio y a 40 MB para dispositivos móviles. </i></td>
   </tr>
    </tbody>
   </table>

## Limitaciones {#limitations}

1. Para importar y exportar, el tipo de archivo de vídeo admitido es MP4.

2. Para la **importación de vídeo MP4**, no se admiten vídeos con fondos transparentes (canal alfa).
   <!--
   1. The maximum file size supported is 200 MB. If this limit exceeds, an alert message displays.
   2. The maximum supported resolution is 3840 X 3840 pixels.
   3. Videos with transparent backgrounds (alpha channel) are not supported.
   -->

3. Para la **exportación de vídeo MP4**, el tamaño máximo de archivo admitido es de 200 MB. Si se supera este límite, se recomienda recortar el vídeo a 200 MB o menos o cargarlo manualmente en la carpeta de destino de AEM Assets después de descargarlo.

<!--
## Content Advisor Properties {#content-advisor-props}

You can configure following properties for the content advisor:

* `featureSet` : This property enables the Content Advisor MFE.

    ```
    featureSet: [
        ...defaultFeatures, /* to include all default features */
        'advisor', /* enables Content Advisor features */
        'content-fragments', /* enables Content Fragments */
    ],
    ```

* `rail:true/false` : If marked true, Content Advisor is rendered in a left rail view. If it is marked false, the Content Advisor is rendered in modal view.

## Browse assets using Content Advisor {#browse-assets-content-advisor}

<!--In the Modal View of Content Advisor, you can access both [Assets](#using-assets-tab) and [Content Fragments](#using-content-fragments) within a unified interface.

### Assets tab{#assets-tab}

The **[!UICONTROL Assets]** tab allows you to browse or filter available assets, preview them before selection, and choose appropriate **[!UICONTROL Dynamic Media]** [renditions](renditions.md) or [smart crops](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles) as needed. Assets, folders, and collections are presented together in a single, streamlined experience. The interface also provides contextual recommendations based on the integrated application context, helping you quickly identify relevant content.

Within assets tab, you can access content by browsing [Files and folders](#content-advisor-files-and-folders) or viewing [Collections](#content-advisor-collections).

### Files and Folders tab{#content-advisor-files-and-folders}

Browsing content using Files and Folders allows you navigate your assets in a familiar hierarchical structure, making it easy to locate assets within the repository. To browse assets within files and folders, navigate to the **[!UICONTROL Assets]** tab and select **[!UICONTROL Files & Folders]**. A hierarchical structure is then displayed, allowing you to easily locate and select the desired assets.

![Browse assets using files and folder](assets/browse-assets-content-advisor.png)

### Collections tab{#content-advisor-collections}

Browsing content using Collections allows you to access curated groups of assets within Collections. To browse assets within Collections, navigate to the **[!UICONTROL Assets]** tab and select **[!UICONTROL Collections]**. The interface then displays curated groups of assets, enabling you to browse the content you need.

![Browse assets using Collections](assets/browse-assets-collections.png)

<!--
### Content Fragments tab{#content-fragments}

The [Content Fragments](/help/assets/content-fragments/content-fragments.md) tab displays structured assets, allowing you to browse, search, and filter fragments efficiently within the same interface. To browse assets using Content Fragments, navigate to the **[!UICONTROL Content Fragments]** tab to access and explore the fragments available in the repository.

![Browse assets using Content Fragments](assets/browse-assets-content-fragment.png)
-->


