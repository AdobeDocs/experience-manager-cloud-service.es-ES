---
title: Organizar sus recursos digitales
description: Organice los recursos digitales, las imágenes, los archivos, las carpetas, etc. mediante el Experience Manager.
contentOwner: AG
feature: Asset Management, Search
role: User
exl-id: 6b3ce076-2dd9-47f6-9b68-4fa52bfedd42
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 4%

---

# Organizar sus recursos digitales {#organize-digital-assets}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/organize-assets.html?lang=en) |
| AEM as a Cloud Service | Este artículo |

Todos los recursos digitales, metadatos y contenido de los documentos de Microsoft® Office y PDF se extraen y se pueden buscar. La búsqueda permite un filtrado sofisticado de los recursos y respeta por completo los permisos adecuados. Los metadatos se tratan en detalle en Metadatos de Digital Asset Management.

[!DNL Experience Manager Assets] admite varias formas de organizar contenido. Puede organizarlos de forma jerárquica mediante carpetas o puede organizarlos de forma desordenada y ad-hoc, por ejemplo etiquetas. Los usuarios pueden editar etiquetas en el Editor de recursos DAM, donde se muestran subrecursos, representaciones y metadatos.

<!-- Commenting to pull down the existing content before applying changes wrt CQDOC-15930
## Create folders {#create-folders}

When organizing a collection of assets, for example, all *Nature* images, you can create folders to keep them together. You can use folders to categorize and organize your assets. [!DNL Assets] does not require you to organize assets in folders to work better.

>[!NOTE]
>
>Sharing an Assets folder (in Marketing Cloud) of the type `sling:OrderedFolder`, is not supported. If you want to share a folder, do not select Ordered when creating a folder.

1. Navigate to the place in your digital assets folder where you want to create a new folder.
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

You can use folders or tags or both to organize assets. Adding tags to assets makes them more easy to retrieve during a search. To add tags to an asset, follow these steps:

1. In the Digital Asset Manager, double-click the asset to open it.
1. In the **Tags** area, open the menu to reveal the available tags. Select tags as appropriate. To delete a tag, hover the pointer over the tag and click `X` to delete it.
1. Click **Save** to save any tags you added.

Date24/08/2021
-->

## Organizar recursos en carpetas {#organize-using-folders}

La forma más básica de organizar los recursos es guardarlos en carpetas. Es similar a organizar archivos en carpetas en su sistema de archivos local. Para obtener más información sobre cómo crear y administrar carpetas, consulte [Administrar recursos](manage-digital-assets.md). La forma en que se asignan nombres a archivos y carpetas, cómo se organizan las subcarpetas y cómo se gestionan los archivos dentro de estas carpetas puede tener un impacto significativo en la forma en que se procesan esos recursos. Al utilizar estrategias de asignación de nombres de archivos y carpetas coherentes y adecuadas, junto con prácticas recomendadas en materia de metadatos, puede aprovechar al máximo su repositorio de recursos digitales.

* Normalmente, su repositorio de recursos digitales siempre está creciendo. Por lo tanto, es importante formalizar el uso de los metadatos, la estructura de carpetas y la nomenclatura de archivos al principio del ciclo de creación de contenido.
* Utilice carpetas solo para imponer una estructura de almacenamiento coherente para sus recursos digitales. Esta coherencia le ayuda a procesar y administrar mejor sus recursos. Por ejemplo, los recursos colocados en los siguientes tipos de carpetas pueden ayudarle a separar los recursos:

   * **Carpetas de desarrollo**: contiene recursos digitales en los que está trabajando.
   * **Carpetas de cliente**: contiene recursos digitales basados en clientes o nombres de proyectos.
   * **Carpetas principales**: contiene recursos digitales originales.
   * **Carpetas de representación**: contiene representaciones y copias de los recursos digitales de origen originales.
   * **Carpetas de tamaño de archivo**: contiene recursos digitales basados en tamaños de archivo pequeños, medianos o grandes.
   * **Carpetas de ensayo**: contiene recursos digitales listos para publicarse en el sitio web.
   * **Carpetas de tipo MIME**: contiene recursos digitales específicos de tipos MIME, como imágenes, documentos y multimedia.
   * **Archivar carpetas**: contiene activos digitales retirados.
   * **Carpetas basadas en fechas**: contiene recursos digitales basados en una fecha de creación o una fecha de última modificación.

* Cree un directorio de carpetas que no es probable que cambien para que cualquier personalización o automatización siga funcionando. Por ejemplo, los perfiles de procesamiento asignados siguen funcionando.
* Si un recurso ya está publicado, utilice [!DNL Experience Manager] para mover el recurso a otra carpeta y volver a publicar desde su nueva ubicación. La ubicación del recurso publicado originalmente sigue estando disponible junto con el recurso recién republicado. Sin embargo, el recurso publicado originalmente es *perdido* a [!DNL Experience Manager] y no se pueden cancelar. Por lo tanto, se recomienda cancelar la publicación de un recurso y moverlo a una carpeta diferente.

## Organización de recursos mediante etiquetas {#use-tags-to-organize-assets}

Añadir etiquetas a los recursos facilita su recuperación durante una búsqueda, crear colecciones utilizando los resultados de búsqueda, mejorar la clasificación de algunos recursos y aplicar algoritmos de IA de Adobe Sensei para la detección de recursos.

[!DNL Adobe Experience Manager Assets] utiliza un algoritmo de autoaprendizaje para crear etiquetas altamente descriptivas que le permitan encontrar el recurso adecuado en tan solo unos clics. El etiquetado inteligente utiliza Adobe Sensei, inteligencia artificial y un marco de aprendizaje automático, que se puede entrenar para reconocer y aplicar etiquetas estándar y específicas del negocio a las imágenes. Las etiquetas inteligentes también pueden identificar contenido, palabras individuales o frases, y aplicar automáticamente etiquetas descriptivas a los recursos.

A continuación se indican los pasos para agregar etiquetas a un recurso:

1. Iniciar sesión en [!DNL Experience Manager Assets].
1. Haga clic en **[!UICONTROL Recursos]** > **[!UICONTROL Archivos]**, seleccione el recurso y haga clic en **[!UICONTROL Propiedades]** para abrir las propiedades del recurso.
1. En el **[!UICONTROL Básico]** , haga clic en el icono de carpeta de **[!UICONTROL Etiquetas]** metadatos. Se abre una ventana emergente.
1. Busque o seleccione las etiquetas adecuadas de las etiquetas existentes en `cq-tags`. Puede asignar varias etiquetas al recurso.

   Puede ordenar la estructura de las etiquetas de forma ascendente o descendente en función de la variable **[!UICONTROL Nombre]** (orden alfabético), **[!UICONTROL Creado]** fecha, o **[!UICONTROL Modificado]** fecha. En la siguiente ilustración, la estructura de etiquetas se ordena alfabéticamente en función de la variable **[!UICONTROL Nombre]**.

   ![añadir etiquetas](assets/add-tags-to-asset.png)

1. Haga clic en **Guardar** para actualizar los cambios en los metadatos de los recursos.

Para obtener más información, consulte los siguientes artículos:

* [Editar metadatos de recursos](meta-edit.md)
* [Etiquetas inteligentes en recursos](smart-tags.md)
* [Agregar etiquetas predicadas al panel de búsqueda](/help/assets/search-facets.md/#adding-a-tags-predicate)

## Organizar como colecciones {#organize-as-collections}

Con colecciones de recursos en [!DNL Experience Manager Assets], puede optimizar la capacidad de crear, editar y compartir recursos entre usuarios. Cree varios tipos de colecciones en función de la forma en que las utilice, incluidas las colecciones que contienen una lista de referencia estática de recursos, carpetas, colecciones y colecciones que extraen recursos en función de criterios de búsqueda. Puede crear colecciones con recursos de distintas ubicaciones y compartirlas con varios usuarios con distintos niveles de privilegios de acceso, visualización y edición.

Para obtener más información, consulte [administrar colecciones](manage-collections.md)


## Utilice perfiles para organizar los recursos {#organize-to-use-profiles}

Un perfil de procesamiento contiene [!DNL Assets] comandos de procesamiento que se aplican a los recursos que se cargan en carpetas predefinidas. Los perfiles se utilizan para automatizar el procesamiento de los contenidos de una carpeta o de los recursos cargados recientemente. Puede utilizar perfiles para organizar mejor los recursos.

La estandarización del uso de metadatos, la asignación de nombres a archivos y la estructura de carpetas garantiza que, a medida que crezca el grupo de recursos digitales, podrá aplicar perfiles de procesamiento a las carpetas con buena precisión y coherencia.

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
>
>* [Uso de microservicios de recursos y perfiles de procesamiento](asset-microservices-configure-and-use.md)
>* [Perfiles de metadatos](metadata-profiles.md)
>* [Perfiles de vídeo](/help/assets/dynamic-media/video-profiles.md)
>* [Perfiles de imagen de Dynamic Media](/help/assets/dynamic-media/image-profiles.md)


