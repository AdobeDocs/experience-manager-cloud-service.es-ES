---
title: Organizar sus recursos digitales
description: Organice sus recursos digitales, imágenes, archivos, carpetas, etc. con Experience Manager.
contentOwner: AG
feature: Asset Management, Best Practices
role: User
exl-id: 6b3ce076-2dd9-47f6-9b68-4fa52bfedd42
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 6%

---

# Organizar sus recursos digitales {#organize-digital-assets}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/organize-assets.html?lang=es) |
| AEM as a Cloud Service | Este artículo |

Todos los recursos digitales, metadatos y contenido de los documentos de Microsoft® Office y PDF se extraen y se pueden buscar. La búsqueda permite un filtrado sofisticado de los recursos y respeta completamente los permisos adecuados. Los metadatos se tratan en detalle en Metadatos en la administración de recursos digitales.

[!DNL Experience Manager Assets] admite varias formas de organizar el contenido. Puede organizarlas de forma jerárquica utilizando carpetas o puede organizarlas de forma no ordenada y ad hoc, por ejemplo, etiquetas. Los usuarios pueden editar etiquetas en el editor de recursos DAM, donde se muestran subrecursos, representaciones y metadatos.

<!-- Commenting to pull down the existing content before applying changes wrt CQDOC-15930
## Create folders {#create-folders}

When organizing a collection of assets, for example, all *Nature* images, you can create folders to keep them together. You can use folders to categorize and organize your assets. [!DNL Assets] does not require you to organize assets in folders to work better.

>[!NOTE]
>
>Sharing an Assets folder (in Marketing Cloud) of the type `sling:OrderedFolder`, is not supported. If you want to share a folder, do not select Ordered when creating a folder.

1. Navigate to the place in your digital assets folder where you want to create a folder.
1. In the menu, click **[!UICONTROL Create]**. Select **[!UICONTROL New Folder]**.
1. In the **[!UICONTROL Title]** field, provide a folder name. By default, DAM uses the title that you provided as the folder name. Once the folder is created, you can override the default and specify another folder name.
1. Click **[!UICONTROL Create]**. Your folder is displayed in the digital assets folder.

## Add CUG properties to folders {#add-cug-properties-to-folders}

You can limit who can access certain folders in Assets by making the folder part of a closed user group (CUG). To make a folder part of a CUG:

1. In Assets, right-click the folder you want to add closed user group properties for and select **Properties**.  
1. Click the **CUG** tab.
1. Select the **Enabled** check box to make the folder and its assets available only to a closed user group.  
1. Browse to the login page, if there is one, to add that information. Add admitted groups by clicking **Add item**. If necessary, add the realm. Click **OK** to save your changes.

## Use tags to organize assets {#use-tags-to-organize-assets}

You can use folders or tags or both to organize assets. Adding tags to assets makes them easier to retrieve during a search. To add tags to an asset, follow these steps:

1. In the Digital Asset Manager, double-click the asset to open it.
1. In the **Tags** area, open the menu to reveal the available tags. Select tags as appropriate. To delete a tag, hover the pointer over the tag and click `X` to delete it.
1. Click **Save** to save any tags you added.

Date24/08/2021
-->

## Organización de recursos en carpetas {#organize-using-folders}

La forma más básica de organizar los recursos es guardarlos en carpetas. Es análogo a organizar archivos en carpetas en el sistema de archivos local. Para obtener más información sobre cómo crear y administrar carpetas, consulte [Administrar recursos](manage-digital-assets.md). El modo de asignar nombres a los archivos y carpetas, organizar las subcarpetas y administrar los archivos de estas carpetas puede tener un impacto significativo en el modo en que se procesan esos recursos. Si utiliza estrategias de nomenclatura de archivos y carpetas coherentes y adecuadas, junto con una buena práctica de metadatos, puede sacar el máximo partido a su repositorio de recursos digitales.

* Normalmente, el repositorio de recursos digitales siempre está creciendo. Por lo tanto, es importante formalizar el uso de metadatos, la estructura de carpetas y la nomenclatura de archivos al principio del ciclo de creación de contenido.
* Utilice carpetas únicamente para imponer una estructura de almacenamiento coherente para los recursos digitales. Esta coherencia le ayuda a procesar y administrar mejor sus recursos. Por ejemplo, los recursos colocados en los siguientes tipos de carpetas pueden ayudarle a separar sus recursos:

   * **Carpetas de desarrollo**: contiene recursos digitales en los que está trabajando.
   * **Carpetas de cliente**: contiene recursos digitales basados en nombres de clientes o proyectos.
   * **Carpetas principales**: contiene recursos digitales de origen originales.
   * **Carpetas de representación**: contiene representaciones y copias de los recursos digitales originales.
   * **Carpetas de tamaño de archivo**: contiene recursos digitales basados en tamaños de archivo pequeños, medianos o grandes.
   * **Carpetas de ensayo**: contiene recursos digitales que están listos para publicarse en el sitio web.
   * **Carpetas de tipo MIME**: contiene recursos digitales específicos de tipos MIME como imágenes, documentos y multimedia.
   * **Archivar carpetas**: contiene recursos digitales retirados.
   * **Carpetas basadas en fechas**: contiene recursos digitales basados en una fecha de creación o en una fecha de última modificación.

* Cree un directorio de carpetas que no tengan probabilidades de cambiar para que la personalización o automatización sigan funcionando. Por ejemplo, los perfiles de procesamiento asignados siguen funcionando.
* Si un recurso ya se ha publicado, utilice [!DNL Experience Manager] para mover el recurso a otra carpeta y vuelva a publicar desde su nueva ubicación. La ubicación del recurso publicado original aún está disponible junto con el recurso publicado recientemente. Sin embargo, el recurso publicado original está *perdido* a [!DNL Experience Manager] y no se puede cancelar su publicación. Por lo tanto, como práctica recomendada, primero debe cancelar la publicación de un recurso y, a continuación, moverlo a una carpeta diferente.

## Organización de recursos mediante etiquetas {#use-tags-to-organize-assets}

Añadir etiquetas a los recursos facilita su recuperación durante la búsqueda, crear colecciones con los resultados de búsqueda, aumentar la clasificación de búsqueda de algunos recursos y aplicar algoritmos de IA de Adobe Sensei para la detección de recursos.

[!DNL Adobe Experience Manager Assets] utiliza un algoritmo de autoaprendizaje para crear etiquetas altamente descriptivas que le permiten encontrar el recurso correcto en solo unos clics. El etiquetado inteligente utiliza Adobe Sensei, inteligencia artificial y un marco de trabajo de aprendizaje automático, que puede formarse para reconocer y aplicar etiquetas estándar y específicas de la empresa a las imágenes. Las etiquetas inteligentes también pueden identificar contenido, palabras o frases individuales y aplicar automáticamente etiquetas descriptivas a los recursos.

A continuación se indican los pasos para agregar etiquetas a un recurso:

1. Inicie sesión en [!DNL Experience Manager Assets].
1. Haga clic en **[!UICONTROL Assets]** > **[!UICONTROL Archivos]**, seleccione el recurso y haga clic en **[!UICONTROL Propiedades]** para abrir las propiedades del recurso.
1. En la ficha **[!UICONTROL Básico]**, haga clic en el icono de carpeta en los metadatos de **[!UICONTROL Etiquetas]**. Se abrirá una ventana emergente.
1. Busque o seleccione las etiquetas adecuadas de las etiquetas existentes en `cq-tags`. Puede asignar varias etiquetas al recurso.

   Puede ordenar la estructura de las etiquetas en orden ascendente o descendente, en función de **[!UICONTROL Nombre]** (orden alfabético), **[!UICONTROL Creado]** fecha o **[!UICONTROL Modificado]** fecha. En la siguiente ilustración, la estructura de etiquetas se ordena alfabéticamente en función del **[!UICONTROL Nombre]**.

   ![add-tags](assets/add-tags-to-asset.png)

1. Haga clic en **Guardar** para actualizar los cambios en los metadatos del recurso.

Para obtener más información, consulte los siguientes artículos:

* [Editar metadatos de recursos](meta-edit.md)
* [Etiquetas inteligentes en Assets](smart-tags.md)
* [Añadir predicado de etiquetas al panel de búsqueda](/help/assets/search-facets.md/#adding-a-tags-predicate)

## Organizar como colecciones {#organize-as-collections}

Con las colecciones de recursos de [!DNL Experience Manager Assets], puede optimizar la capacidad para crear, editar y compartir recursos entre los usuarios. Cree varios tipos de colecciones en función de su uso, incluidas las que contienen una lista de referencia estática de recursos, carpetas y colecciones y las que extraen recursos en función de criterios de búsqueda. Puede crear colecciones con recursos de diferentes ubicaciones y compartirlas con varios usuarios con diferentes niveles de acceso, visualización y edición de privilegios.

Para obtener más información, consulte [administrar colecciones](manage-collections.md)


## Uso de perfiles para organizar los recursos {#organize-to-use-profiles}

Un perfil de procesamiento contiene [!DNL Assets] comandos de procesamiento que se aplican a los recursos que se cargan en carpetas predefinidas. Los perfiles se utilizan para automatizar el procesamiento del contenido de una carpeta o de los recursos recién cargados. Puede utilizar perfiles para organizar mejor los recursos.

La estandarización del uso de metadatos, los nombres de archivo y la estructura de carpetas garantiza que, a medida que el grupo de recursos digitales crezca, pueda aplicar perfiles de procesamiento a las carpetas con mayor precisión y coherencia.

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

>[!MORELIKETHIS]
>
>* [Usar microservicios de recursos y perfiles de procesamiento](asset-microservices-configure-and-use.md)
>* [Perfiles de metadatos](metadata-profiles.md)
>* [Perfiles de vídeo](/help/assets/dynamic-media/video-profiles.md)
>* [Perfiles de imagen de Dynamic Media](/help/assets/dynamic-media/image-profiles.md)

