---
title: Metadatos XMP
description: Obtenga información sobre el estándar de metadatos XMP (Extensible Metadata Platform) para la administración de metadatos. La utiliza AEM como formato estandarizado para la creación, el procesamiento y el intercambio de metadatos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0c915b32d676ff225cbe276be075d3ae1a865f11
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 21%

---


# Metadatos XMP {#xmp-metadata}

XMP (Extensible Metadata Platform) es el estándar de metadatos utilizado por AEM Assets para la administración de todos los metadatos. XMP proporciona un formato estándar para la creación, el procesamiento y el intercambio de metadatos para una amplia variedad de aplicaciones.

Además de ofrecer codificación de metadatos universales que se puede incrustar en todos los formatos de archivo, XMP proporciona un [modelo de contenido enriquecido](#xmp-core-concepts) y [es compatible con Adobe](#advantages-of-xmp) y otras compañías, de modo que los usuarios de XMP en combinación con AEM Assets tienen una poderosa plataforma sobre la que construir.

## XMP descripción general y ecosistema {#xmp-ecosystem}

AEM Assets admite de forma nativa el estándar de metadatos de XMP. XMP es un estándar para procesar y almacenar metadatos estandarizados y propietarios en activos digitales. XMP está diseñado para ser el estándar común que permite que varias aplicaciones funcionen eficazmente con metadatos.

Los profesionales de la producción, por ejemplo, utilizan la compatibilidad de XMP integrada en las aplicaciones de Adobe para pasar información a través de varios formatos de archivo. El repositorio de AEM Assets extrae los metadatos XMP y los utiliza para administrar el ciclo de vida del contenido y oferta la capacidad de crear flujos de trabajo de automatización.

XMP estandariza la forma en que se definen, crean y procesan los metadatos proporcionando un modelo de datos, un modelo de almacenamiento y esquemas. Todos estos conceptos se tratan en esta sección.

Todos los metadatos heredados de EXIF, ID3 o Microsoft Office se traducen automáticamente a XMP, lo que se puede ampliar para admitir el esquema de metadatos específico del cliente, como catálogos de productos.

Los metadatos de XMP constan de un conjunto de propiedades. Estas propiedades siempre están asociadas a una entidad específica denominada recurso; es decir, las propiedades son &quot;acerca&quot; del recurso. En el caso de XMP, el recurso es siempre el recurso.

XMP define un modelo de [metadatos](https://es.wikipedia.org/wiki/Metadatos) que se puede utilizar con cualquier conjunto definido de elementos de metadatos. XMP también define [esquemas](https://en.wikipedia.org/wiki/XML_schema) específicos para propiedades básicas útiles para registrar el historial de un recurso a medida que pasa por varios pasos de procesamiento, desde ser fotografiado, [escaneado](https://es.wikipedia.org/wiki/Esc%C3%A1ner_inform%C3%A1tico) o creado como texto, pasando por etapas de edición fotográfica (como [recorte](https://en.wikipedia.org/wiki/Cropping_%28image%29) o ajuste de color), hasta ensamblarse en una imagen final. XMP permite a cada programa o dispositivo de software añadir su propia información a un recurso digital, que se puede retener en el archivo digital final.

XMP se serializa y almacena con mayor frecuencia mediante un subconjunto del [W3C](https://es.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://en.wikipedia.org/wiki/Resource_Description_Framework) (RDF), que a su vez se expresa en [XML](https://en.wikipedia.org/wiki/XML).

### Ventajas de XMP {#advantages-of-xmp}

XMP tiene las siguientes ventajas con respecto a otros esquemas y estándares de codificación:

* Los metadatos basados en XMP son muy potentes y detallados.
* XMP permite tener varios valores para una propiedad.
* XMP cuenta con codificación estandarizada, lo que le permite intercambiar fácilmente metadatos.
* XMP es extensible. Puede agregar información adicional a los recursos.

El XMP estándar está diseñado para ser extensible, lo que le permite agregar tipos personalizados de metadatos a los datos XMP. EXIF, por otro lado, no - tiene una lista fija de propiedades que no puede ampliarse.

>[!NOTE]
>
>XMP generalmente no permite incrustar tipos de datos binarios. Para cargar datos binarios en XMP, por ejemplo, imágenes en miniatura, deben codificarse en un formato compatible con XML como `Base64`.

### Conceptos principales de XMP {#xmp-core-concepts}

**Áreas de nombres y esquemas**

Un esquema XMP es un conjunto de nombres de propiedades en una Área de nombres XML común que incluye
el tipo de datos y la información descriptiva. Un esquema de XMP se identifica mediante su URI de Área de nombres XML. El uso de Áreas de nombres evita conflictos entre propiedades en diferentes esquemas que tienen el mismo nombre pero un significado diferente.

Por ejemplo, la propiedad **Creator** en dos esquemas de diseño independiente puede significar la persona que creó el recurso o bien la aplicación que lo creó (por ejemplo, Adobe Photoshop).

**XMP propiedades y valores**

XMP pueden incluir propiedades de uno o varios de los esquemas. Por ejemplo, un subconjunto típico utilizado por muchas aplicaciones Adobe puede incluir lo siguiente:

* Esquema central de Dublín: `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`, &lt;a4/>
* XMP esquema básico: `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`
* esquema de gestión de derechos de XMP: `xmpRights:WebStatement`, `xmpRights:Marked`
* esquema de administración de medios XMP: `xmpMM:DocumentID`

**Alternativas lingüísticas**

XMP le oferta la capacidad de agregar una propiedad `xml:lang` a las propiedades de texto para especificar el idioma del texto.

## Reescritura XMP en representaciones {#xmp-writeback-to-renditions}

Esta función de XMP escritura en marcha atrás en Adobe Experience Manager (AEM) Assets replica los cambios de metadatos de los recursos en las representaciones del recurso.

Al cambiar los metadatos de un recurso desde AEM Assets o al cargarlo, los cambios se almacenan inicialmente en el nodo de recurso en CRXDE.

La función de XMP escritura en marcha hace que los cambios de metadatos se propaguen a todas las representaciones del recurso o a determinadas representaciones del recurso.

Considere un escenario en el que modifique la propiedad [!UICONTROL Title] del recurso titulada `Classic Leather` a `Nylon`.

![metadata](assets/metadata.png)

En este caso, AEM Assets guarda los cambios en la propiedad **[!UICONTROL Title]** en el parámetro `dc:title` para los metadatos de recurso almacenados en la jerarquía de recursos.

![metadata_stored](assets/metadata_stored.png)

Sin embargo, AEM Assets no propaga automáticamente ningún cambio de metadatos en las representaciones de un recurso.

La función de XMP escritura en marcha permite propagar los cambios de metadatos a todas las representaciones del recurso o a determinadas representaciones del recurso. Sin embargo, los cambios no se almacenan en el nodo de metadatos de la jerarquía de recursos. En su lugar, esta función incrusta los cambios en los archivos binarios para las representaciones.

### Habilitar XMP devolución de escritura {#enable-xmp-writeback}

<!-- asgupta, Engg: Need attention here to update the configuration manager changes.
-->

Para permitir que los cambios de metadatos se propaguen a las representaciones del recurso al cargarlo, modifique la configuración de **[!UICONTROL Adobe CQ DAM Rendition Maker]** en Configuration Manager.

1. Para abrir Configuration Manager, acceda a `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra la configuración **[!UICONTROL Adobe CQ DAM Rendition Maker]**.
1. Seleccione la opción **[!UICONTROL Propagar XMP]** y, a continuación, guarde los cambios.

### Habilitar XMP devolución de escritura para representaciones específicas {#enable-xmp-writeback-for-specific-renditions}

Para permitir que la función XMP de escritura en marcha propague los cambios de metadatos para seleccionar representaciones, especifique estas representaciones en el paso de flujo de trabajo [!UICONTROL Proceso de escritura en XMP] del flujo de trabajo de escritura de metadatos DAM. De forma predeterminada, este paso se configura con la representación original.

Para que la función de XMP escritura en marcha atrás propague metadatos a las miniaturas de representación 140.100.png y 319.319.png, lleve a cabo estos pasos.

1. Pulse o haga clic en el logotipo de AEM y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
1. En la página Modelos, abra el modelo de flujo de trabajo **[!UICONTROL Reescritura de metadatos DAM]**.
1. En la página de **[!UICONTROL propiedades de escritura de metadatos DAM]**, abra el paso **[!UICONTROL Proceso de escritura XMP]**.
1. En el cuadro de diálogo **[!UICONTROL Propiedades del paso]**, pulse o haga clic en la pestaña **[!UICONTROL Proceso]**.
1. En el cuadro **[!UICONTROL Argumentos]**, agregue `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png` y, a continuación, toque o haga clic en **[!UICONTROL Aceptar]**.

   ![step_properties](assets/step_properties.png)

1. Guarde los cambios.
1. Para volver a generar las representaciones TIFF (PTIFF) piramidales para imágenes de Dynamic Media con los nuevos atributos, agregue el paso **[!UICONTROL Recursos de imagen de proceso de Dynamic Media]** al flujo de trabajo de reescritura de metadatos DAM. Las representaciones PTIFF solo se crean y almacenan localmente en una implementación híbrida de Dynamic Media.

1. Guarde el flujo de trabajo.

Los cambios en los metadatos se propagan a las representaciones thumbnail.140.100.png y thumbnail.319.319.png del recurso, y no a los demás.

>[!MORELIKETHIS]
>
>* [Especificación XMP por Adobe](https://www.adobe.com/devnet/xmp.html)

