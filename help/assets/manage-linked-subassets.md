---
title: Administración de recursos compuestos
description: Obtenga información sobre cómo crear referencias a recursos de AEM desde archivos de Indesign, Adobe Illustrator y Photoshop. Aprenda también a utilizar la función Visor de páginas para ver páginas individuales de archivos de varias páginas, incluidos archivos PDF, INDD, PPT, PPTX y Ai.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# Administración de recursos compuestos {#managing-compound-assets}

Los recursos de Adobe Experience Manager (AEM) pueden identificar si un archivo cargado contiene referencias a recursos que ya existen en el repositorio. Esta función solo está disponible para los formatos de archivo admitidos. Si el recurso cargado contiene referencias a recursos de AEM, se crea un vínculo bidireccional entre los recursos cargados y los a los que se hace referencia.

Además de eliminar la redundancia, hacer referencia a los recursos de AEM en las aplicaciones de Adobe Creative Cloud mejora la colaboración y aumenta la eficiencia y la productividad de los usuarios.

Recursos AEM admite referencias **bidireccionales**. Los recursos a los que se hace referencia se encuentran en la página de detalles del recurso del archivo cargado. Además, puede ver los archivos de referencia de los recursos de AEM en la página de detalles de recursos del recurso al que se hace referencia.

Las referencias se resuelven en función de la ruta de acceso, el ID del documento y el ID de instancia de los recursos a los que se hace referencia.

## AEM Assets como referencias en Adobe Illustrator {#refai}

Puede hacer referencia a recursos de AEM existentes desde un archivo de Adobe Illustrator.

1. Con la aplicación [de escritorio de](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html)AEM, monte el repositorio de AEM Assets como una unidad en el equipo local. En la unidad montada, navegue a la ubicación del recurso al que desee hacer referencia.
1. Arrastre el recurso desde la unidad montada al archivo de Illustrator.
1. Guarde el archivo de Illustrator en la unidad montada o [cárguelo](/help/assets/manage-digital-assets.md#uploading-assets) en el repositorio de AEM.
1. Una vez finalizado el flujo de trabajo, vaya a la página de detalles del recurso. Las referencias a los recursos de AEM existentes se enumeran en **Dependencias** en la columna **Referencias** .

   ![chlimage_1-84](assets/chlimage_1-84.png)

1. Los recursos a los que se hace referencia y que aparecen en **Dependencias** también pueden ser referenciados por otros archivos que no sean el actual. Para ver una lista de archivos de referencia para un recurso, haga clic en el recurso en la sección **Dependencias**.

   ![chlimage_1-85](assets/chlimage_1-85.png)

1. Haga clic en el icono **Ver propiedades** de la barra de herramientas. En la página de propiedades, la lista de archivos que hacen referencia al recurso actual aparece en la columna **Referencias** de la ficha **Básico** .

   ![chlimage_1-86](assets/chlimage_1-86.png)

## Adición de recursos de AEM como referencias en Adobe InDesign {#add-aem-assets-as-references-in-adobe-indesign}

Para hacer referencia a recursos de AEM desde un archivo de InDesign, arrastre los recursos de AEM al archivo de InDesign o exporte el archivo de InDesign como archivo ZIP.

Los recursos a los que se hace referencia ya existen en Recursos AEM. <!-- You can extract subassets by [configuring InDesign server](/help/assets/indesign.md). Embedded assets in an InDesign file are extracted as subassets. -->

>[!NOTE]
>
>Si se procesa como proxy el servidor de InDesign, la vista previa de los archivos de InDesign se incrusta en los metadatos XMP. En este caso, no se requiere explícitamente la extracción de miniaturas. Sin embargo, si el servidor de InDesign no se procesa como proxy, las miniaturas se deben extraer explícitamente para los archivos de InDesign.

### Creación de referencias arrastrando recursos de AEM {#create-references-by-dragging-aem-assets}

Este procedimiento es similar a [Añadir recursos de AEM como referencias en Adobe Illustrator](#refai).

### Creación de referencias a recursos de AEM mediante la exportación de un archivo ZIP {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. Cree un nuevo modelo de flujo de trabajo.
1. Utilice la función Empaquetar de Adobe InDesign para exportar el documento.
Adobe InDesign puede exportar un documento y los recursos vinculados como un paquete. En este caso, la carpeta exportada contiene una carpeta Links que contiene subrecursos en el archivo de InDesign.
1. Cree un archivo ZIP y cárguelo en el repositorio de AEM.
1. Inicie el flujo de trabajo de Unarchiver.
1. Cuando se completa el flujo de trabajo, se hace referencia automáticamente a las referencias de la carpeta Vínculos como subrecursos. Para ver una lista de los recursos referidos, vaya a la página de detalles del recurso de InDesign y cierre el [raíl](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector).

## Adición de recursos de AEM como referencias en Adobe Photoshop {#refps}

1. Con un cliente WebDav, monte Recursos AEM como unidad.
1. Para crear referencias a recursos AEM en un archivo de Photoshop, navegue hasta los recursos correspondientes de la unidad montada utilizando la función Colocar el vínculo en Photoshop.

   ![chlimage_1-87](assets/chlimage_1-87.png)

1. Guarde el archivo en Photoshop en la unidad montada o [cárguelo](/help/assets/manage-digital-assets.md#uploading-assets) en el repositorio de AEM.
1. Una vez finalizado el flujo de trabajo, las referencias a los recursos de AEM existentes se muestran en la página de detalles de los recursos.

   Para ver los recursos a los que se hace referencia, cierre el [raíl](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector) en la página de detalles del recurso.

1. Los recursos a los que se hace referencia también contienen la lista de recursos desde los que se hace referencia. Para ver una lista de los recursos a los que se hace referencia, vaya a la página de detalles del recurso y cierre el [raíl](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector).

>[!NOTE]
>
>También se puede hacer referencia a los recursos dentro de los recursos compuestos en función de su ID de documento y su ID de instancia. Esta funcionalidad solo está disponible en las versiones de Adobe Illustrator y Adobe Photoshop. Para otros, la referencia se realiza en función de la ruta relativa de los recursos vinculados en el recurso compuesto principal, como se hacía en versiones anteriores de AEM.

## Ver páginas de un archivo de varias páginas {#view-pages-of-a-multi-page-file}

La función Visor de páginas de Recursos AEM le permite ver páginas individuales de archivos de varias páginas, incluidos archivos PDF, INDD, PPT, PPTX y Ai. En InDesign, puede extraer páginas con el servidor de InDesign. Si las vistas previas de las páginas se guardan durante la creación de archivos de InDesign, no se requiere InDesign Server para la extracción de páginas.

Puede navegar por páginas individuales de un archivo desde la página de recursos. Puede utilizar las opciones de la barra de herramientas para anotar páginas individuales del archivo. También puede utilizar la opción **Información general** de página para ver todas las páginas simultáneamente.

1. Vaya a la carpeta de Recursos AEM que contiene el archivo de varias páginas.
1. Haga clic en el recurso para ver su página de recursos.

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. Haga clic en el icono Navegación global y, a continuación, elija **Páginas** en el menú.

   ![chlimage_1-89](assets/chlimage_1-89.png)

1. Haga clic en las flechas izquierda o derecha debajo de la imagen para desplazarse a páginas individuales del archivo.

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. Para realizar anotaciones en una página, haga clic en el icono **Anotar** de la barra de herramientas y agregue un comentario.

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. Para descargar el archivo, haga clic en el icono **Descargar** .

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. Para ver todas las páginas del archivo de forma simultánea, haga clic en el icono **Información general** de página.

   ![chlimage_1-93](assets/chlimage_1-93.png)

1. Para ver el flujo de actividades del archivo, incluidas las anotaciones y las descargas, haga clic en el icono de navegación global y, a continuación, elija **Cronología** en el menú.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. Para ver y editar las propiedades de metadatos de la página, haga clic en el icono **Ver propiedades** de la barra de herramientas.

   ![chlimage_1-95](assets/chlimage_1-95.png)
