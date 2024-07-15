---
title: Metadatos XMP
description: XMP Obtenga información acerca del estándar de metadatos de la plataforma de metadatos extensible (EXTENSIBLE Metadata Platform) para la administración de metadatos. Experience Manager la utiliza como formato estandarizado para la creación, el procesamiento y el intercambio de metadatos.
contentOwner: AG
feature: Metadata
role: Admin, User
exl-id: fd9af408-d2a3-4c7a-9423-c4b69166f873
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 17%

---

# Metadatos XMP {#xmp-metadata}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/xmp-writeback.html) |
| AEM as a Cloud Service | Este artículo |

XMP (Plataforma de metadatos extensible) es el estándar de metadatos utilizado por Experience Manager Assets para la administración de todos los metadatos. XMP proporciona un formato estándar para la creación, el procesamiento y el intercambio de metadatos para una amplia variedad de aplicaciones.

XMP Además de ofrecer codificación de metadatos universal que se puede incrustar en todos los formatos de archivo, proporciona un modelo de contenido enriquecido de [y es [compatible con Adobe XMP](#advantages-of-xmp) y otras compañías, de modo que los usuarios de en combinación con [!DNL Assets] tienen una plataforma potente sobre la que construir.](#xmp-core-concepts)

## XMP Información general y ecosistema de la {#xmp-ecosystem}

XMP [!DNL Assets] admite de forma nativa el estándar de metadatos de la. XMP es un estándar para procesar y almacenar metadatos estandarizados y propios en recursos digitales. XMP está diseñado para ser el estándar común que permita que varias aplicaciones funcionen de forma eficaz con los metadatos.

XMP Los profesionales de la producción, por ejemplo, utilizan la compatibilidad integrada con las aplicaciones de Adobe para pasar información a través de varios formatos de archivo. XMP El repositorio [!DNL Assets] extrae los metadatos de la y los utiliza para administrar el ciclo de vida del contenido, además de ofrecer la capacidad de crear flujos de trabajo de automatización.

XMP La estandarización estandariza la forma en que se definen, crean y procesan los metadatos mediante un modelo de datos, un modelo de almacenamiento y esquemas. Todos estos conceptos se tratan en esta sección.

Todos los metadatos heredados de EXIF, ID3 o Microsoft XMP Office se traducen automáticamente a la versión de, que se puede ampliar para admitir esquemas de metadatos específicos del cliente, como catálogos de productos.

XMP Los metadatos de la constan de un conjunto de propiedades. Estas propiedades siempre están asociadas a una entidad específica denominada recurso; es decir, las propiedades se refieren al recurso. XMP En el caso de los recursos, el recurso siempre es el recurso

XMP define un modelo de [metadatos](https://es.wikipedia.org/wiki/Metadatos) que se puede utilizar con cualquier conjunto definido de elementos de metadatos. XMP también define [esquemas](https://en.wikipedia.org/wiki/XML_schema) específicos para propiedades básicas útiles para registrar el historial de un recurso a medida que pasa por varios pasos de procesamiento, desde ser fotografiado, [escaneado](https://es.wikipedia.org/wiki/Esc%C3%A1ner_inform%C3%A1tico) o creado como texto, pasando por etapas de edición fotográfica (como [recorte](https://en.wikipedia.org/wiki/Cropping_%28image%29) o ajuste de color), hasta ensamblarse en una imagen final. XMP permite a cada programa o dispositivo de software añadir su propia información a un recurso digital, que se puede retener en el archivo digital final.

XMP se serializa y almacena con mayor frecuencia mediante un subconjunto del [W3C](https://es.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://en.wikipedia.org/wiki/Resource_Description_Framework) (RDF), que a su vez se expresa en [XML](https://en.wikipedia.org/wiki/XML).

### XMP Ventajas de la {#advantages-of-xmp}

XMP tiene las siguientes ventajas con respecto a otros esquemas y estándares de codificación:

* XMP Los metadatos basados en el lenguaje de datos son muy completos y de gran alcance.
* XMP permite tener varios valores para una propiedad.
* XMP tiene codificación estandarizada, lo que permite intercambiar fácilmente metadatos.
* XMP La es extensible. Puede añadir información adicional a sus recursos.

XMP XMP El estándar de datos está diseñado para que sea ampliable, lo que le permite agregar tipos personalizados de metadatos a los datos de la. EXIF, por otro lado, no - tiene una lista fija de propiedades que no se pueden ampliar.

>[!NOTE]
>
>XMP Por lo general, no se permite incrustar tipos de datos binarios. XMP Para transportar datos binarios en imágenes en miniatura, por ejemplo, en el caso de las imágenes, deben estar codificados en un formato compatible con XML, como `Base64`.

### XMP conceptos principales de la {#xmp-core-concepts}

**Espacios de nombres y esquemas**

XMP Un esquema de datos es un conjunto de nombres de propiedad en un área de nombres XML común que incluye
el tipo de datos y la información descriptiva. XMP Un esquema de datos se identifica mediante su URI de área de nombres XML. El uso de áreas de nombres evita conflictos entre propiedades en esquemas diferentes que tienen el mismo nombre pero un significado diferente.

Por ejemplo, la propiedad **Creator** en dos esquemas diseñados de forma independiente podría significar la persona que creó el recurso o podría significar la aplicación que creó el recurso (por ejemplo, Adobe Photoshop).

XMP **propiedades y valores de la**

XMP Puede incluir propiedades de uno o más de los esquemas. Por ejemplo, un subconjunto típico utilizado por muchas aplicaciones de Adobe puede incluir lo siguiente:

* Esquema principal de Dublín: `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`
* XMP esquema básico: `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`
* XMP Esquema de administración de derechos de la: `xmpRights:WebStatement`, `xmpRights:Marked`
* XMP esquema de administración de medios de comunicación: `xmpMM:DocumentID`

**Alternativas de idioma**

XMP le ofrece la posibilidad de agregar una propiedad `xml:lang` a las propiedades de texto para especificar el idioma del texto.

## XMP respuesta de escritura a las representaciones de {#xmp-writeback-to-renditions}

XMP Esta característica de reescritura de la [!DNL Adobe Experience Manager Assets] replica los cambios de metadatos en las representaciones del recurso original.
Cuando cambia los metadatos de un recurso desde [!DNL Assets] o mientras lo carga, los cambios se almacenan inicialmente en el nodo de metadatos de la jerarquía de recursos. La función de reescritura permite propagar los cambios de metadatos a todas las representaciones del recurso o a algunas específicas. La característica sólo devuelve las propiedades de metadatos que utilizan el espacio de nombres `jcr`, es decir, se devuelve una propiedad denominada `dc:title`, pero no una propiedad denominada `mytitle`.

Por ejemplo, imagine un escenario en el que modifica la propiedad [!UICONTROL Title] del recurso con título `Classic Leather` a `Nylon`.

![metadatos](assets/metadata.png)

En este caso, [!DNL Assets] guarda los cambios realizados en la propiedad **[!UICONTROL Title]** en el parámetro `dc:title` para los metadatos de recursos almacenados en la jerarquía de recursos.

![metadatos almacenados en el nodo de recursos en el repositorio](assets/metadata_stored.png)

>[!IMPORTANT]
>
>La característica de reescritura no está habilitada de manera predeterminada en [!DNL Assets]. Consulte cómo [habilitar la reescritura de metadatos](#enable-xmp-writeback). MSM para recursos digitales no funciona con la reescritura de metadatos habilitada. Tras la reescritura, la herencia se interrumpe.

### XMP Habilitar reescritura de la {#enable-xmp-writeback}

El flujo de trabajo [!UICONTROL DAM Metadata Writeback] se usa para escribir de nuevo los metadatos de un recurso. Para habilitar la reescritura, siga uno de los tres métodos siguientes:

* Utilice los lanzadores.
* Iniciar manualmente `DAM MetaData Writeback` flujo de trabajo.
* Configure el flujo de trabajo para que forme parte del posprocesamiento.

Para utilizar los lanzadores, siga estos pasos:

1. Como administrador, acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Lanzadores]**.
1. Seleccione el [!UICONTROL lanzador] para el cual la columna **[!UICONTROL Flujo de trabajo]** muestra **[!UICONTROL reescritura de metadatos DAM]**. Haga clic en **[!UICONTROL Propiedades]** en la barra de herramientas.

   ![Seleccione el lanzador de reescritura de metadatos DAM para modificar sus propiedades y activarlo](assets/launcher-properties-metadata-writeback1.png)

1. Seleccione **[!UICONTROL Activar]** en la página **[!UICONTROL Propiedades del lanzador]**. Haga clic en **[!UICONTROL Guardar y cerrar]**.

Para aplicar manualmente el flujo de trabajo a un recurso una sola vez, aplique el flujo de trabajo [!UICONTROL reescritura de metadatos DAM] desde el carril izquierdo.

Para aplicar el flujo de trabajo a todos los recursos cargados, añada el flujo de trabajo a un perfil de posprocesamiento.

<!-- Commenting for now. Need to document how to enable metadata writeback. See CQDOC-17254.

### Enable XMP writeback {#enable-xmp-writeback}

To enable the metadata changes to be propagated to the renditions of the asset when uploading it, modify the **[!UICONTROL Adobe CQ DAM Rendition Maker]** configuration in Configuration Manager.

1. To open Configuration Manager, access `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL Adobe CQ DAM Rendition Maker]** configuration.
1. Select the **[!UICONTROL Propagate XMP]** option, and then save the changes.

### Enable XMP write-back for specific renditions {#enable-xmp-writeback-for-specific-renditions}

To let the XMP write-back feature propagate metadata changes to select renditions, specify these renditions to the [!UICONTROL XMP Writeback Process] workflow step of DAM Metadata WriteBack workflow. By default, this step is configured with the original rendition.

For the XMP write-back feature to propagate metadata to the rendition thumbnails 140.100.png and 319.319.png, perform these steps.

1. Select the Experience Manager logo, and then navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Workflow]** &gt; **[!UICONTROL Models]**.
1. From the Models page, open the **[!UICONTROL DAM Metadata Writeback]** workflow model.
1. In the **[!UICONTROL DAM Metadata Writeback]** properties page, open the **[!UICONTROL XMP Writeback Process]** step.
1. In the **[!UICONTROL Step Properties]** dialog box, select the **[!UICONTROL Process]** tab.
1. In the **[!UICONTROL Arguments]** box, add `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`, and then select **[!UICONTROL OK]**.

   ![step_properties](assets/step_properties.png)

1. Save the changes.
1. To regenerate the Pyramid TIFF (PTIFF) renditions for Dynamic Media images with the new attributes, add the **[!UICONTROL Dynamic Media Process Image Assets]** step to the DAM Metadata write-back workflow. PTIFF renditions are only created and stored locally in a Dynamic Media Hybrid implementation.

1. Save the workflow.

The metadata changes are propagated to the renditions renditions thumbnail.140.100.png and thumbnail.319.319.png of the asset, and not the others.
-->

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con recursos](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos de red](use-assets-across-connected-assets-instances.md)
* [Informes de recurso](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)
* [Publicación de recursos en AEM y Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
