---
title: Configuración de la asignación de metadatos de recursos entre Workfront y Experience Manager Assets
description: Asigne los campos de metadatos de recursos entre las aplicaciones as a Cloud Service de Adobe Workfront y Experience Manager. Como resultado de la asignación de campos de metadatos, al enviar un recurso de Workfront a Experience Manager Assets, puede ver los metadatos de recurso asignados en Experience Manager Assets.
exl-id: 71400769-b2bc-4f5d-8b6b-a73598e837b4
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 3%

---

# Configuración de la asignación de metadatos de recursos entre Adobe Workfront y Experience Manager Assets {#asset-metadata-mapping-workfront-aem-assets}

Puede asignar los campos de metadatos de recursos entre las aplicaciones as a Cloud Service de Adobe Workfront y Experience Manager. Como resultado de la asignación de campos de metadatos, al enviar un recurso de Workfront a Experience Manager Assets, puede ver los metadatos de recurso asignados en Experience Manager Assets.

Por ejemplo, si necesita conservar los campos de metadatos de una imagen, como nombre, descripción y el proyecto al que pertenece en Workfront cuando envía la imagen a Experience Manager Assets, configure y asigne estos campos a las propiedades de Experience Manager Assets.

**Caso práctico**

Una imagen `add-users-workfront.png` existe en la variable `Metadata Syncs` en la aplicación Adobe Workfront. Debe enviar esa imagen a Experience Manager Assets as a Cloud Service con los siguientes metadatos:

* Nombre del proyecto

* Nombre del documento

* Descripción del documento

## Requisitos previos {#prerequisites}

* Un acceso de administrador a las aplicaciones as a Cloud Service de Workfront y Experience Manager Assets.

* Una integración entre [Aplicaciones as a Cloud Service de Workfront y Experience Manager Assets](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FDocuments%2FAdobe_Workfront_for_Experience_Manager_Assets_Essentials%2Fsetup-asset-essentials.htm&amp;_LANG=enus).

## Configuración de la asignación de metadatos en Workfront {#set-up-metadata-mapping}

Para definir la asignación de metadatos para los campos Nombre del proyecto, Nombre del documento y Descripción del documento en Workfront:

1. Haga clic en el icono del menú principal ![Mostrar menú](assets/show-menu.svg) disponible en la esquina superior derecha de la aplicación Adobe Workfront y, a continuación, haga clic en **[!UICONTROL Configuración]**.

1. Select **[!UICONTROL Documentos]** en el panel izquierdo, seleccione **[!UICONTROL Experience Manager Assets]**.

1. Seleccione la integración de Experience Manager Assets y haga clic en **[!UICONTROL Editar]**.

1. Haga clic en **[!UICONTROL Metadatos]**. En el **[!UICONTROL Recursos]** , asigne la variable [!UICONTROL Proyecto] > [!UICONTROL Nombre] Campo de Workfront a la variable `wm:projectName` Campo Experience Manager Assets . Si no encuentra la coincidencia exacta, Adobe recomienda buscar la mejor coincidencia para asignar el campo Workfront y Experience Manager Assets . Puede evitar la asignación de campos de diferentes tipos de datos. Por ejemplo, si se asigna un campo de Workfront de fecha a un campo de descripción Recursos .
1. Asigne la variable [!UICONTROL Documento] > [!UICONTROL Nombre] Campo de Workfront a la variable `wm:documentName` Campo Experience Manager Assets .

   ![Asignación en Workfront](assets/workfront-metadata-mapping.png)

1. Asigne la variable [!UICONTROL Documento] > [!UICONTROL Descripción] Campo de Workfront a la variable `dc:description` Campo Experience Manager Assets .

   >[!VIDEO](https://video.tv.adobe.com/v/344255)

## Enviar la imagen de Workfront a Experience Manager Assets {#send-image-workfront-assets}

Para enviar la imagen de Workfront a Experience Manager Assets:

1. Haga clic en el icono del menú principal ![Mostrar menú](assets/show-menu.svg) disponible en la esquina superior derecha de la aplicación Adobe Workfront y, a continuación, haga clic en **[!UICONTROL Proyectos]**.

1. Haga clic en **[!UICONTROL Nuevo proyecto]** para crear un nuevo proyecto.

1. Haga clic en **[!UICONTROL Documentos]** disponible en el panel izquierdo, arrastre y, a continuación, seleccione la imagen que debe enviar a Experience Manager Assets.

1. Haga clic en **[!UICONTROL Enviar a]** y, a continuación, elija el nombre de integración de Experience Manager Assets Essentials.

   ![Enviar a AEM](assets/send-to-aem.png)

1. Elija la carpeta de destino del recurso y haga clic en **[!UICONTROL Seleccionar carpeta]**.

1. Haga clic en **[!UICONTROL Guardar]**.

## Configuración de la asignación de metadatos de recursos en Experience Manager as a Cloud Service {#metadata-mapping-aem}

Después [configuración de la asignación de metadatos de recursos en Adobe Workfront](#set-up-metadata-mapping), debe utilizar la misma asignación en la aplicación as a Cloud Service de Experience Manager Assets para mostrar los resultados de metadatos adecuados para la imagen.

La asignación de metadatos se realiza mediante esquemas de metadatos en Experience Manager Assets. Puede editar un formulario de esquema de metadatos nuevo o existente. El formulario de esquema de metadatos incluye fichas y elementos de formulario en fichas. Puede asignar/configurar estos elementos de formulario a un campo dentro de un nodo de metadatos en el repositorio CRX. Puede agregar fichas o elementos de formulario al formulario de esquema de metadatos. Para obtener más información, consulte [Esquemas de metadatos](metadata-schemas.md).

Para configurar la asignación de metadatos con un nuevo formulario de metadatos en Experience Manager Assets as a Cloud Service:

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Esquemas de metadatos]**.

1. Haga clic en **[!UICONTROL Crear]** en la barra de herramientas. En el cuadro de diálogo , proporcione el título del formulario de esquema y haga clic en **[!UICONTROL Crear]** para completar el proceso de creación del formulario.

1. Seleccione el formulario de esquema y haga clic en **[!UICONTROL Editar]**.

1. (Opcional) En el Editor de formularios de esquemas de metadatos, haga clic en `+` para crear una nueva pestaña para los campos de Workfront.

1. Haga clic en el **[!UICONTROL Generar formulario]** y arrastre el **[!UICONTROL Texto de una sola línea]** al formulario. Haga clic en el componente del formulario. En el **[!UICONTROL Generar formulario]** pestaña:

   1. Especifique `Project Name` en el **[!UICONTROL Etiqueta de campo]** campo .

   1. Especifique `./jcr:content/metadata/wm:projectName` en el **[!UICONTROL Asignar a la propiedad]** campo . Como guía, utilice la siguiente plantilla para definir las asignaciones de campo en Experience Manager Assets:
      `./jcr:content/metadata/<mapping defined for the field in workfront>`.

      Al configurar asignaciones en Workfront, asignó `wm:projectName` Campo Experience Manager Assets en Proyecto > Asignar nombre a Workfront .

      `wm` hace referencia al nombre del área de nombres y `projectName` hace referencia al título de la propiedad. Utilice la variable `namespace:propertyTitle` para definir asignaciones de campo de metadatos.

      ![Enviar a AEM](assets/metadata-schema-mapping.png)

1. Haga clic en el **[!UICONTROL Generar formulario]** y arrastre el **[!UICONTROL Texto de una sola línea]** al formulario. Haga clic en el componente del formulario. En el **[!UICONTROL Generar formulario]** pestaña:

   1. Especifique `Document Name` en el **[!UICONTROL Etiqueta de campo]** campo .

   1. Especifique `./jcr:content/metadata/wm:documentName` en el **[!UICONTROL Asignar a la propiedad]** campo .
Al configurar asignaciones en Workfront, asignó `wm:documentName` Campo de Experience Manager Assets a Documento > Asignar nombre a Workfront .

1. Haga clic en el **[!UICONTROL Generar formulario]** y arrastre el **[!UICONTROL Texto de varias líneas]** al formulario. Haga clic en el componente del formulario. En el **[!UICONTROL Generar formulario]** pestaña:

   1. Especifique `Document Description` en el **[!UICONTROL Etiqueta de campo]** campo .

   1. Especifique `./jcr:content/metadata/dc:description` en el **[!UICONTROL Asignar a la propiedad]** campo .
Al configurar asignaciones en Workfront, asignó `dc:description` Campo Experience Manager Assets en Documento > Descripción del campo Workfront.

1. Haga clic en **[!UICONTROL Guardar]** para guardar los cambios.

   >[!VIDEO](https://video.tv.adobe.com/v/344314)

## Aplicar configuración de metadatos a la carpeta de imágenes {#apply-metadata-settings-image-folder}

Después de configurar los metadatos en la aplicación as a Cloud Service de Experience Manager, aplique estos ajustes a la variable [carpeta que contiene la imagen que se envía desde la aplicación Workfront](#send-image-workfront-assets).

Para aplicar la configuración de metadatos a la carpeta de imágenes:

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Esquemas de metadatos]**.

1. Seleccione el esquema de metadatos de la lista de metadatos disponibles y haga clic en **[!UICONTROL Aplicar a carpetas]**.

1. Seleccione la carpeta de destino a la que [la imagen se envía desde la aplicación Adobe Workfront](#send-image-workfront-assets) y haga clic en **[!UICONTROL Aplicar]**.

Puede desplazarse a la imagen en Experience Manager Assets y ver los metadatos asociados a la imagen. Seleccione la imagen y haga clic en **[!UICONTROL Propiedades]** para ver los metadatos de la imagen.

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
