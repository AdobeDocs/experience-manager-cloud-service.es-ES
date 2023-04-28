---
title: Metadatos XMP
description: Obtenga información sobre el estándar de metadatos XMP (Plataforma de metadatos extensible) para la administración de metadatos. Experience Manager lo utiliza como formato estandarizado para la creación, el procesamiento y el intercambio de metadatos.
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: fd9af408-d2a3-4c7a-9423-c4b69166f873
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 17%

---

# Metadatos XMP {#xmp-metadata}

XMP (Extensible Metadata Platform) es el estándar de metadatos que Experience Manager Assets utiliza para la administración de todos los metadatos. XMP proporciona un formato estándar para la creación, el procesamiento y el intercambio de metadatos para una amplia variedad de aplicaciones.

Además de ofrecer una codificación de metadatos universal que se puede incrustar en todos los formatos de archivo, XMP proporciona un [modelo de contenido](#xmp-core-concepts) y es [compatible con Adobe](#advantages-of-xmp) y otras empresas, de modo que los usuarios de XMP en combinación con [!DNL Assets] tienen una poderosa plataforma sobre la que construir.

## XMP descripción general y ecosistema {#xmp-ecosystem}

[!DNL Assets] nativamente admite el estándar de metadatos XMP. XMP es un estándar para procesar y almacenar metadatos estandarizados y de propiedad en recursos digitales. XMP está diseñado para ser el estándar común que permite que varias aplicaciones funcionen eficazmente con metadatos.

Los profesionales de producción, por ejemplo, utilizan la compatibilidad XMP integrada en las aplicaciones de Adobe para pasar información a través de varios formatos de archivo. La variable [!DNL Assets] el repositorio extrae los metadatos de XMP y los utiliza para administrar el ciclo de vida del contenido y ofrece la capacidad de crear flujos de trabajo de automatización.

XMP estandariza la forma en que se definen, crean y procesan los metadatos proporcionando un modelo de datos, un modelo de almacenamiento y esquemas. Todos estos conceptos se tratan en esta sección.

Todos los metadatos heredados de EXIF, ID3 o Microsoft Office se traducen automáticamente a XMP, lo que se puede ampliar para admitir esquemas de metadatos específicos del cliente, como catálogos de productos.

Los metadatos de XMP constan de un conjunto de propiedades. Estas propiedades siempre están asociadas a una entidad específica denominada recurso; es decir, las propiedades son &quot;about&quot; el recurso. En el caso de XMP, el recurso siempre es el recurso.

XMP define un modelo de [metadatos](https://es.wikipedia.org/wiki/Metadatos) que se puede utilizar con cualquier conjunto definido de elementos de metadatos. XMP también define [esquemas](https://en.wikipedia.org/wiki/XML_schema) específicos para propiedades básicas útiles para registrar el historial de un recurso a medida que pasa por varios pasos de procesamiento, desde ser fotografiado, [escaneado](https://es.wikipedia.org/wiki/Esc%C3%A1ner_inform%C3%A1tico) o creado como texto, pasando por etapas de edición fotográfica (como [recorte](https://en.wikipedia.org/wiki/Cropping_%28image%29) o ajuste de color), hasta ensamblarse en una imagen final. XMP permite a cada programa o dispositivo de software añadir su propia información a un recurso digital, que se puede retener en el archivo digital final.

XMP se serializa y almacena con mayor frecuencia mediante un subconjunto del [W3C](https://es.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://en.wikipedia.org/wiki/Resource_Description_Framework) (RDF), que a su vez se expresa en [XML](https://en.wikipedia.org/wiki/XML).

### Ventajas de XMP {#advantages-of-xmp}

XMP tiene las siguientes ventajas sobre otros estándares y esquemas de codificación:

* Los metadatos basados en XMP son muy potentes y detallados.
* XMP permite tener varios valores para una propiedad.
* XMP tiene codificación estandarizada, lo que permite intercambiar fácilmente metadatos.
* XMP es extensible. Puede añadir información adicional a los recursos.

El XMP estándar está diseñado para ser extensible, lo que le permite añadir tipos de metadatos personalizados a los datos de XMP. EXIF, por otro lado, no tiene - tiene una lista fija de propiedades que no se pueden ampliar.

>[!NOTE]
>
>XMP generalmente no permite incrustar tipos de datos binarios. Para cargar datos binarios en XMP, por ejemplo, imágenes en miniatura, deben codificarse en un formato compatible con XML, como `Base64`.

### XMP conceptos básicos {#xmp-core-concepts}

**Espacios de nombres y esquemas**

Un esquema XMP es un conjunto de nombres de propiedades en un espacio de nombres XML común que incluye el tipo de datos y la información descriptiva. Un esquema XMP se identifica mediante su URI de área de nombres XML. El uso de áreas de nombres evita conflictos entre propiedades en distintos esquemas que tienen el mismo nombre pero un significado diferente.

Por ejemplo, la variable **Creador** en dos esquemas diseñados de forma independiente, puede significar la persona que creó el recurso o puede significar la aplicación que lo creó (por ejemplo, Adobe Photoshop).

**XMP propiedades y valores**

XMP incluir propiedades de uno o varios esquemas. Por ejemplo, un subconjunto típico utilizado por muchas aplicaciones de Adobe puede incluir lo siguiente:

* Esquema central de Dublín: `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`
* XMP esquema básico: `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`
* esquema de administración de derechos de XMP: `xmpRights:WebStatement`, `xmpRights:Marked`
* esquema XMP media management: `xmpMM:DocumentID`

**Alternativas lingüísticas**

XMP le ofrece la posibilidad de agregar un `xml:lang` propiedad a propiedades de texto para especificar el idioma del texto.

## XMP escritura en representaciones {#xmp-writeback-to-renditions}

Esta función de reescritura XMP en [!DNL Adobe Experience Manager Assets] replica los cambios de metadatos en las representaciones del recurso original.
Al cambiar los metadatos de un recurso desde [!DNL Assets] o al cargar el recurso, los cambios se almacenan inicialmente en el nodo de metadatos de la jerarquía de recursos. La función de reescritura permite propagar los cambios de metadatos a todas las representaciones del recurso o a algunas de ellas. La función solo recupera las propiedades de metadatos que utilizan `jcr` namespace, es decir, una propiedad denominada `dc:title` se devuelve, pero una propiedad denominada `mytitle` no.

Por ejemplo, considere un escenario en el que modifique el [!UICONTROL Título] propiedad del recurso con título `Classic Leather` a `Nylon`.

![metadatos](assets/metadata.png)

En este caso, [!DNL Assets] guarda los cambios en la variable **[!UICONTROL Título]** en la variable `dc:title` para los metadatos de recurso almacenados en la jerarquía de recursos.

![metadatos almacenados en el nodo de recursos en el repositorio](assets/metadata_stored.png)

>[!IMPORTANT]
>
>La función de reescritura no está activada de forma predeterminada en [!DNL Assets]. Consulte cómo [activar reescritura de metadatos](#enable-xmp-writeback). MSM para recursos digitales no funciona con la reescritura de metadatos habilitada. Al reescribir, la herencia se rompe.

### Habilitar reescritura XMP {#enable-xmp-writeback}

[!UICONTROL Reescritura de metadatos DAM] flujo de trabajo se utiliza para reescribir los metadatos de un recurso. Para habilitar la reescritura, siga cualquiera de los tres métodos siguientes:

* Utilice Lanzadores.
* Inicio manual `DAM MetaData Writeback` flujo de trabajo.
* Configure el flujo de trabajo para que forme parte del posprocesamiento.

Para utilizar lanzadores, siga estos pasos:

1. Como administrador, acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Lanzadores]**.
1. Seleccione el [!UICONTROL Iniciador] para los que **[!UICONTROL Flujo de trabajo]** pantallas de columna **[!UICONTROL Reescritura de metadatos DAM]**. Haga clic en **[!UICONTROL Propiedades]** en la barra de herramientas.

   ![Seleccione el lanzador de reescritura de metadatos DAM para modificar sus propiedades y activarlo](assets/launcher-properties-metadata-writeback1.png)

1. Select **[!UICONTROL Activar]** en el **[!UICONTROL Propiedades del iniciador]** página. Haga clic en **[!UICONTROL Guardar y cerrar]**.

Para aplicar manualmente el flujo de trabajo a un recurso una sola vez, aplique [!UICONTROL Reescritura de metadatos DAM] flujo de trabajo desde el carril izquierdo.

Para aplicar el flujo de trabajo a todos los recursos cargados, agregue el flujo de trabajo a un perfil posterior al procesamiento.

<!-- Commenting for now. Need to document how to enable metadata writeback. See CQDOC-17254.

### Enable XMP writeback {#enable-xmp-writeback}

To enable the metadata changes to be propagated to the renditions of the asset when uploading it, modify the **[!UICONTROL Adobe CQ DAM Rendition Maker]** configuration in Configuration Manager.

1. To open Configuration Manager, access `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL Adobe CQ DAM Rendition Maker]** configuration.
1. Select the **[!UICONTROL Propagate XMP]** option, and then save the changes.

### Enable XMP write-back for specific renditions {#enable-xmp-writeback-for-specific-renditions}

To let the XMP write-back feature propagate metadata changes to select renditions, specify these renditions to the [!UICONTROL XMP Writeback Process] workflow step of DAM Metadata WriteBack workflow. By default, this step is configured with the original rendition.

For the XMP write-back feature to propagate metadata to the rendition thumbnails 140.100.png and 319.319.png, perform these steps.

1. Tap/click the Experience Manager logo, and then navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Workflow]** &gt; **[!UICONTROL Models]**.
1. From the Models page, open the **[!UICONTROL DAM Metadata Writeback]** workflow model.
1. In the **[!UICONTROL DAM Metadata Writeback]** properties page, open the **[!UICONTROL XMP Writeback Process]** step.
1. In the **[!UICONTROL Step Properties]** dialog box, tap/click the **[!UICONTROL Process]** tab.
1. In the **[!UICONTROL Arguments]** box, add `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`, and then tap/click **[!UICONTROL OK]**.

   ![step_properties](assets/step_properties.png)

1. Save the changes.
1. To regenerate the Pyramid TIFF (PTIFF) renditions for Dynamic Media images with the new attributes, add the **[!UICONTROL Dynamic Media Process Image Assets]** step to the DAM Metadata write-back workflow. PTIFF renditions are only created and stored locally in a Dynamic Media Hybrid implementation.

1. Save the workflow.

The metadata changes are propagated to the renditions renditions thumbnail.140.100.png and thumbnail.319.319.png of the asset, and not the others.
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
