---
title: Metadatos XMP
description: Obtenga información sobre el estándar de metadatos XMP (Extensible Metadata Platform) para la administración de metadatos. AEM lo utiliza como formato estandarizado para la creación, el procesamiento y el intercambio de metadatos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Metadatos XMP {#xmp-metadata}

XMP (Extensible Metadata Platform) es el estándar de metadatos utilizado por AEM Assets para la gestión de todos los metadatos. XMP proporciona un formato estándar para la creación, el procesamiento y el intercambio de metadatos para una amplia variedad de aplicaciones.

Además de ofrecer codificación de metadatos universales que se puede incrustar en todos los formatos de archivo, XMP proporciona un modelo [de](#xmp-core-concepts) contenido enriquecido y es [compatible con Adobe](#advantages-of-xmp) y otras empresas, de modo que los usuarios de XMP en combinación con Recursos AEM tienen una plataforma sólida sobre la que construir.

## Visión general y ecosistema de XMP {#xmp-ecosystem}

Recursos AEM admite de forma nativa el estándar de metadatos XMP. XMP es un estándar para procesar y almacenar metadatos estandarizados y propietarios en activos digitales. XMP está diseñado para ser el estándar común que permite que varias aplicaciones funcionen eficazmente con metadatos.

Los profesionales de la producción, por ejemplo, utilizan la compatibilidad integrada con XMP en las aplicaciones de Adobe para pasar información a través de varios formatos de archivo. El repositorio de AEM Assets extrae los metadatos XMP y los utiliza para administrar el ciclo de vida del contenido y ofrece la posibilidad de crear flujos de trabajo de automatización.

XMP estandariza cómo se definen, crean y procesan los metadatos proporcionando un modelo de datos, un modelo de almacenamiento y esquemas. Todos estos conceptos se tratan en esta sección.

Todos los metadatos heredados de EXIF, ID3 o Microsoft Office se traducen automáticamente a XMP, que se pueden ampliar para admitir esquemas de metadatos específicos del cliente, como catálogos de productos.

Los metadatos en XMP constan de un conjunto de propiedades. Estas propiedades siempre están asociadas a una entidad específica denominada recurso; es decir, las propiedades son &quot;acerca&quot; del recurso. En el caso de XMP, el recurso es siempre el recurso.

XMP define un modelo de [metadatos](https://en.wikipedia.org/wiki/Metadata) que se puede utilizar con cualquier conjunto definido de elementos de metadatos. XMP también define [esquemas](https://en.wikipedia.org/wiki/XML_schema) específicos para propiedades básicas útiles para registrar el historial de un recurso a medida que pasa por varios pasos de procesamiento, desde ser fotografiado, [escaneado](https://en.wikipedia.org/wiki/Image_scanner)o creado como texto, pasando por pasos de edición fotográfica (como [recorte](https://en.wikipedia.org/wiki/Cropping_%28image%29) o ajuste de color), hasta ensamblarse en una imagen final. XMP permite a cada programa o dispositivo de software añadir su propia información a un recurso digital, que se puede retener en el archivo digital final.

XMP se serializa y almacena con mayor frecuencia mediante un subconjunto del [W3C](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://en.wikipedia.org/wiki/Resource_Description_Framework) (RDF), que a su vez se expresa en [XML](https://en.wikipedia.org/wiki/XML).

### Ventajas de XMP {#advantages-of-xmp}

XMP tiene las siguientes ventajas con respecto a otros esquemas y estándares de codificación:

* Los metadatos basados en XMP son muy potentes y detallados.
* XMP permite tener varios valores para una propiedad.
* XMP tiene codificación estandarizada, lo que le permite intercambiar fácilmente metadatos.
* XMP es extensible. Puede agregar información adicional a los recursos.

El estándar XMP está diseñado para ser extensible, lo que le permite agregar tipos personalizados de metadatos a los datos XMP. EXIF, por otro lado, no tiene - tiene una lista fija de propiedades que no puede ampliarse.

>[!NOTE]
>
>XMP generalmente no permite incrustar tipos de datos binarios. Para cargar datos binarios en XMP, por ejemplo, imágenes en miniatura, deben codificarse en un formato compatible con XML, como `Base64`.

### Conceptos básicos de XMP {#xmp-core-concepts}

**Espacios de nombres y esquemas**

Un esquema XMP es un conjunto de nombres de propiedades en un espacio de nombres XML común que incluye el tipo de datos y la información descriptiva. Un esquema XMP se identifica mediante su URI de espacio de nombres XML. El uso de espacios de nombres evita conflictos entre propiedades en distintos esquemas que tienen el mismo nombre pero un significado diferente.

Por ejemplo, la propiedad **Creator** de dos esquemas de diseño independiente puede significar la persona que creó el recurso o bien la aplicación que lo creó (por ejemplo, Adobe Photoshop).

**Propiedades y valores XMP**

XMP puede incluir propiedades de uno o varios esquemas. Por ejemplo, un subconjunto típico utilizado por muchas aplicaciones de Adobe puede incluir lo siguiente:

* Esquema central de Dublín: `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`
* Esquema básico XMP: `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`
* Esquema de administración de derechos XMP: `xmpRights:WebStatement`, `xmpRights:Marked`
* Esquema de administración de medios XMP: `xmpMM:DocumentID`

**Alternativas lingüísticas**

XMP le permite agregar una `xml:lang` propiedad a las propiedades de texto para especificar el idioma del texto.

## Reescritura XMP en representaciones {#xmp-writeback-to-renditions}

Esta función de eliminación de XMP en Recursos Adobe Experience Manager (AEM) replica los cambios de metadatos de los recursos en las representaciones del recurso.

Al cambiar los metadatos de un recurso desde Recursos AEM o al cargar el recurso, los cambios se almacenan inicialmente en el nodo de recurso en CRXDE.

La función de reescritura XMP propaga los cambios de metadatos en todas las representaciones del recurso o en determinadas representaciones.

Considere un escenario en el que modifique la propiedad [!UICONTROL Title] del recurso `Classic Leather` al que se denomina `Nylon`.

![metadata](assets/metadata.png)

En este caso, Recursos AEM guarda los cambios en la propiedad **[!UICONTROL Title]** en el parámetro `dc:title` de los metadatos del recurso almacenados en la jerarquía de recursos.

![metadata_stored](assets/metadata_stored.png)

Sin embargo, Recursos AEM no propaga automáticamente ningún cambio de metadatos en las representaciones de un recurso.

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

1. Toque o haga clic en el logotipo de AEM y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
1. En la página Modelos, abra el modelo de flujo de trabajo de reescritura de metadatos **[!UICONTROL DAM]** .
1. En la página de propiedades de escritura **[!UICONTROL de metadatos]** DAM, abra el paso Proceso **[!UICONTROL de escritura]** XMP.
1. En el cuadro de diálogo Propiedades **[!UICONTROL del]** paso, toque o haga clic en la ficha **[!UICONTROL Proceso]** .
1. En el cuadro **[!UICONTROL Argumentos]** , agregue `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`y toque o haga clic en **[!UICONTROL Aceptar]**.

   ![step_properties](assets/step_properties.png)

1. Guarde los cambios.
1. Para volver a generar las representaciones TIFF (PTIFF) piramidales para imágenes de Dynamic Media con los nuevos atributos, agregue el paso Recursos **[!UICONTROL de imagen de proceso de]** Dynamic Media al flujo de trabajo de reescritura de metadatos DAM. Las representaciones PTIFF solo se crean y almacenan localmente en una implementación híbrida de Dynamic Media.

1. Guarde el flujo de trabajo.

Los cambios en los metadatos se propagan a las representaciones thumbnail.140.100.png y thumbnail.319.319.png del recurso, y no a los demás.

<!--
>[!NOTE]
>
>For XMP writeback issues in 64 bit Linux, see [How to enable XMP write-back on 64-bit RedHat Linux](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>For more information about supported platforms, see [XMP metadata write-back prerequisites](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).
-->

### Filtrar metadatos XMP {#filtering-xmp-metadata}

Recursos AEM admite el filtrado de propiedades/nodos de listas negras y listas blancas para los metadatos XMP que se leen de los binarios de recursos y se almacenan en JCR cuando se ingestan recursos.

El filtrado de listas negras permite importar todas las propiedades de metadatos XMP, excepto las propiedades especificadas para la exclusión. Sin embargo, para tipos de recursos como archivos INDD que tienen grandes cantidades de metadatos XMP (por ejemplo, 1000 nodos con 10.000 propiedades), los nombres de los nodos que se van a filtrar no siempre se conocen por adelantado. Si el filtrado de listas negras permite importar un gran número de recursos con numerosos metadatos XMP, la instancia/clúster de AEM puede encontrar problemas de estabilidad, por ejemplo, colas de observación obstruidas.

El filtrado de la lista blanca de metadatos XMP resuelve este problema permitiéndole definir las propiedades XMP que se van a importar. De este modo, se omiten otras propiedades XMP desconocidas. Puede agregar algunas de estas propiedades al filtro de lista negra para obtener compatibilidad con versiones anteriores.

>[!NOTE]
>
>El filtrado solo funciona para las propiedades derivadas de orígenes XMP en los binarios de recursos. Para las propiedades derivadas de orígenes no XMP, como los formatos EXIF e IPTC, el filtrado no funciona. Por ejemplo, la fecha de creación de recursos se almacena en la propiedad denominada `CreateDate` en TIFF EXIF. AEM registra este valor en el campo de metadatos denominado `exif:DateTimeOriginal`. Como el origen es un origen que no es XMP, el filtrado no funciona en esta propiedad.

1. Para abrir Configuration Manager, acceda a `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra la configuración de **[!UICONTROL Adobe CQ DAM XmpFilter]** .
1. Para aplicar el filtrado de listas blancas, seleccione **[!UICONTROL Aplicar lista blanca a las propiedades]** XMP y especifique las propiedades que desea importar en el cuadro de filtrado **[!UICONTROL Nombres XML]** admitidos para XMP.

1. Para filtrar las propiedades XMP bloqueadas después de aplicar el filtro de la lista blanca, especifíquelas en el cuadro de filtrado **[!UICONTROL Nombres XML]** bloqueados para XMP.

   >[!NOTE]
   >
   >La opción **[!UICONTROL Aplicar lista negra a propiedades]** XMP está seleccionada de forma predeterminada. En otras palabras, el filtrado de listas negras está habilitado de forma predeterminada. Para desactivar el filtrado de listas negras, desactive la opción **[!UICONTROL Aplicar lista negra a propiedades]** XMP.

1. Guarde los cambios.

>[!MORELIKETHIS]
>
>* [Especificación XMP por Adobe](https://www.adobe.com/devnet/xmp.html)