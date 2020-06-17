---
title: Metadatos XMP
description: Obtenga información sobre el estándar de metadatos XMP (Extensible Metadata Platform) para la administración de metadatos. AEM lo utiliza como formato estandarizado para la creación, el procesamiento y el intercambio de metadatos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: b0436c74389ad0b3892d1258d993c00aa470c3ab
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 21%

---


# Metadatos XMP {#xmp-metadata}

XMP (Extensible Metadata Platform) es el estándar de metadatos utilizado por los AEM Assets para la administración de todos los metadatos. XMP proporciona un formato estándar para la creación, el procesamiento y el intercambio de metadatos para una amplia variedad de aplicaciones.

Además de ofrecer codificación de metadatos universales que se puede incrustar en todos los formatos de archivo, XMP proporciona un modelo [de](#xmp-core-concepts) contenido enriquecido y es [compatible con Adobe](#advantages-of-xmp) y otras compañías, de modo que los usuarios de XMP en combinación con AEM Assets tienen una plataforma sólida sobre la que construir.

## Visión general y ecosistema de XMP {#xmp-ecosystem}

Los AEM Assets admiten de forma nativa el estándar de metadatos XMP. XMP es un estándar para procesar y almacenar metadatos estandarizados y propietarios en activos digitales. XMP está diseñado para ser el estándar común que permite que varias aplicaciones funcionen eficazmente con metadatos.

Los profesionales de la producción, por ejemplo, utilizan la compatibilidad integrada con XMP en las aplicaciones de Adobe para pasar información a través de varios formatos de archivo. El repositorio de AEM Assets extrae los metadatos XMP y los utiliza para administrar el ciclo de vida del contenido y oferta la capacidad de crear flujos de trabajo de automatización.

XMP estandariza la forma en que se definen, crean y procesan los metadatos proporcionando un modelo de datos, un modelo de almacenamiento y esquemas. Todos estos conceptos se tratan en esta sección.

Todos los metadatos heredados de EXIF, ID3 o Microsoft Office se traducen automáticamente a XMP, que se pueden ampliar para admitir esquemas de metadatos específicos del cliente, como catálogos de productos.

Los metadatos en XMP constan de un conjunto de propiedades. Estas propiedades siempre están asociadas a una entidad específica denominada recurso; es decir, las propiedades son &quot;acerca&quot; del recurso. En el caso de XMP, el recurso es siempre el recurso.

XMP define un modelo de [metadatos](https://es.wikipedia.org/wiki/Metadatos) que se puede utilizar con cualquier conjunto definido de elementos de metadatos. XMP también define [esquemas](https://en.wikipedia.org/wiki/XML_schema) específicos para propiedades básicas útiles para registrar el historial de un recurso a medida que pasa por varios pasos de procesamiento, desde ser fotografiado, [escaneado](https://es.wikipedia.org/wiki/Esc%C3%A1ner_inform%C3%A1tico) o creado como texto, pasando por etapas de edición fotográfica (como [recorte](https://en.wikipedia.org/wiki/Cropping_%28image%29) o ajuste de color), hasta ensamblarse en una imagen final. XMP permite a cada programa o dispositivo de software añadir su propia información a un recurso digital, que se puede retener en el archivo digital final.

XMP se serializa y almacena con mayor frecuencia mediante un subconjunto del [W3C](https://es.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://en.wikipedia.org/wiki/Resource_Description_Framework) (RDF), que a su vez se expresa en [XML](https://en.wikipedia.org/wiki/XML).

### Ventajas de XMP {#advantages-of-xmp}

XMP tiene las siguientes ventajas con respecto a otros esquemas y estándares de codificación:

* Los metadatos basados en XMP son muy potentes y detallados.
* XMP permite tener varios valores para una propiedad.
* XMP tiene codificación estandarizada, lo que le permite intercambiar fácilmente metadatos.
* XMP es extensible. Puede agregar información adicional a los recursos.

El estándar XMP está diseñado para ser extensible, lo que le permite agregar tipos personalizados de metadatos a los datos XMP. EXIF, por otro lado, no - tiene una lista fija de propiedades que no puede ampliarse.

>[!NOTE]
>
>XMP generalmente no permite incrustar tipos de datos binarios. Para cargar datos binarios en XMP, por ejemplo, imágenes en miniatura, deben codificarse en un formato compatible con XML, como `Base64`.

### Conceptos básicos de XMP {#xmp-core-concepts}

**Áreas de nombres y esquemas**

Un esquema XMP es un conjunto de nombres de propiedades en una Área de nombres XML común que incluye el tipo de datos y la información descriptiva. Un esquema XMP se identifica mediante su URI de Área de nombres XML. El uso de Áreas de nombres evita conflictos entre propiedades en diferentes esquemas que tienen el mismo nombre pero un significado diferente.

Por ejemplo, la propiedad **Creator** en dos esquemas de diseño independiente puede significar la persona que creó el recurso o bien la aplicación que lo creó (por ejemplo, Adobe Photoshop).

**Propiedades y valores XMP**

XMP puede incluir propiedades de uno o varios de los esquemas. Por ejemplo, un subconjunto típico utilizado por muchas aplicaciones de Adobe puede incluir lo siguiente:

* esquema central de Dublín: `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`
* esquema básico XMP: `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`
* esquema de administración de derechos XMP: `xmpRights:WebStatement`, `xmpRights:Marked`
* esquema de administración de medios XMP: `xmpMM:DocumentID`

**Alternativas lingüísticas**

XMP oferta la capacidad de agregar una `xml:lang` propiedad a las propiedades de texto para especificar el idioma del texto.

## Reescritura XMP en representaciones {#xmp-writeback-to-renditions}

Esta función de eliminación de XMP en Recursos Adobe Experience Manager (AEM) replica los cambios de metadatos de los recursos en las representaciones del recurso.

Al cambiar los metadatos de un recurso desde dentro de AEM Assets o al cargarlo, los cambios se almacenan inicialmente en el nodo de recurso en CRXDE.

La función de reescritura XMP propaga los cambios de metadatos en todas las representaciones del recurso o en determinadas representaciones.

Considere un escenario en el que modifique la propiedad [!UICONTROL Title] del recurso `Classic Leather` al que se denomina `Nylon`.

![metadata](assets/metadata.png)

En este caso, los AEM Assets guardan los cambios en la propiedad **[!UICONTROL Title]** en el parámetro `dc:title` de los metadatos del recurso almacenados en la jerarquía de recursos.

![metadata_stored](assets/metadata_stored.png)

Sin embargo, los AEM Assets no propagan automáticamente ningún cambio de metadatos en las representaciones de un recurso.

La función de reescritura XMP permite propagar los cambios de metadatos a todas las representaciones del recurso o a determinadas representaciones del recurso. Sin embargo, los cambios no se almacenan en el nodo de metadatos de la jerarquía de recursos. En su lugar, esta función incrusta los cambios en los archivos binarios para las representaciones.

### Habilitar eliminación de XMP {#enable-xmp-writeback}

<!-- asgupta, Engg: Need attention here to update the configuration manager changes.
-->

Para permitir que los cambios de metadatos se propaguen a las representaciones del recurso al cargarlo, modifique la configuración de **[!UICONTROL Adobe CQ DAM Rendition Maker]** en Configuration Manager.

1. Para abrir Configuration Manager, acceda a `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra la configuración de **[!UICONTROL Adobe CQ DAM Rendition Maker]** .
1. Seleccione la opción **[!UICONTROL Propagar XMP]** y, a continuación, guarde los cambios.

### Habilitar la reescritura XMP para representaciones específicas {#enable-xmp-writeback-for-specific-renditions}

Para permitir que la función de reescritura XMP propague los cambios de metadatos para seleccionar representaciones, especifique estas representaciones en el paso de flujo de trabajo del proceso [!UICONTROL de reescritura] XMP del flujo de trabajo de reescritura de metadatos DAM. De forma predeterminada, este paso se configura con la representación original.

Para que la función de reescritura XMP propague metadatos a las miniaturas de representación 140.100.png y 319.319.png, lleve a cabo estos pasos.

1. Pulse o haga clic en el logotipo de AEM y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
1. En la página Modelos, abra el modelo de flujo de trabajo de reescritura de metadatos **[!UICONTROL DAM]** .
1. En la página de **[!UICONTROL propiedades de escritura de metadatos DAM]**, abra el paso **[!UICONTROL Proceso de escritura XMP]**.
1. En el cuadro de diálogo **[!UICONTROL Propiedades del paso]**, pulse o haga clic en la pestaña **[!UICONTROL Proceso]**.
1. En el cuadro **[!UICONTROL Argumentos]** , agregue `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`y toque o haga clic en **[!UICONTROL Aceptar]**.

   ![step_properties](assets/step_properties.png)

1. Guarde los cambios.
1. Para volver a generar las representaciones TIFF (PTIFF) piramidales para imágenes de Dynamic Media con los nuevos atributos, agregue el paso **[!UICONTROL Recursos de imagen de proceso de Dynamic Media]** al flujo de trabajo de reescritura de metadatos DAM. Las representaciones PTIFF solo se crean y almacenan localmente en una implementación híbrida de Dynamic Media.

1. Guarde el flujo de trabajo.

Los cambios en los metadatos se propagan a las representaciones thumbnail.140.100.png y thumbnail.319.319.png del recurso, y no a los demás.

<!--
>[!NOTE]
>
>For XMP writeback issues in 64 bit Linux, see [How to enable XMP write-back on 64-bit RedHat Linux](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>For more information about supported platforms, see [XMP metadata write-back prerequisites](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).
-->

<!--
TBD: The method has changed in AEMaaCS. Find the new ones.

### Filter XMP metadata {#filtering-xmp-metadata}

AEM Assets supports filtering of properties/nodes for XMP metadata that is read from asset binaries and stored in JCR when assets are ingested. Filtering is possible via a blocked list and an allowed list.

Filtering using a blocked list lets you import all XMP metadata properties except the properties that are specified for exclusion. However, for asset types such as INDD files that have huge amounts of XMP metadata (for example 1000 nodes with 10,000 properties), the names of nodes to be filtered are not always known in advance. If filtering using a blocked list allows a large number of assets with numerous XMP metadata to be imported, the AEM instance/cluster can encounter stability issues, for example clogged observation queues.

Filtering of XMP metadata via allowed list resolves this issue by letting you define the XMP properties to be imported. This way, other/unknown XMP properties are ignored. For backward compatibility, you can add some of these properties to the filter that uses a blocked list.

>[!NOTE]
>
>Filtering works only for the properties derived from XMP sources in asset binaries. For the properties derived from non-XMP sources, such as EXIF and IPTC formats, the filtering does not work. For example, the date of asset creation is stored in property named `CreateDate` in EXIF TIFF. AEM stories this value in the metadata field named `exif:DateTimeOriginal`. As the source is a non-XMP source, filtering does not work on this property.

1. To open Configuration Manager, access `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL Adobe CQ DAM XmpFilter]** configuration.
1. To apply filtering via an allowed list, select **[!UICONTROL Apply Whitelist to XMP Properties]**, and specify the properties to be imported in the **[!UICONTROL Whitelisted XML Names for XMP filtering]** box.

1. To filter out blocked XMP properties after applying filtering via allowed list, specify them in the **[!UICONTROL Blacklisted XML Names for XMP filtering]** box.

   >[!NOTE]
   >
   >The **[!UICONTROL Apply Blacklist to XMP Properties]** option is selected by default. In other words, filtering using a blocked list is enabled by default. To disable such filtering, deselect the **[!UICONTROL Apply Blacklist to XMP Properties]** option.

1. Save the changes.
-->

>[!MORELIKETHIS]
>
>* [Especificación XMP por Adobe](https://www.adobe.com/devnet/xmp.html)

