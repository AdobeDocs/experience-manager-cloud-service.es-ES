---
title: Configuración de la asignación de metadatos de recursos entre Workfront y Experience Manager Assets
description: Asigne los campos de metadatos del recurso entre Adobe Workfront y las aplicaciones as a Cloud Service del Experience Manager. Como resultado de la asignación de campos de metadatos, cuando envía un recurso de Workfront a Experience Manager Assets, puede ver los metadatos del recurso asignado en Experience Manager Assets.
exl-id: 71400769-b2bc-4f5d-8b6b-a73598e837b4
source-git-commit: 097c17b37cc308dc906cd4af7dc7c5d51862bdfa
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 1%

---

# Configuración de la asignación de metadatos de recursos entre Adobe Workfront y Experience Manager Assets {#asset-metadata-mapping-workfront-aem-assets}

Puede asignar los campos de metadatos de recursos entre Adobe Workfront y las aplicaciones as a Cloud Service de Experience Manager. Como resultado de la asignación de campos de metadatos, cuando envía un recurso de Workfront a Experience Manager Assets, puede ver los metadatos del recurso asignado en Experience Manager Assets.

Por ejemplo, si necesita conservar los campos de metadatos de una imagen, como el nombre, la descripción y el proyecto al que pertenece en Workfront al enviar la imagen a Experience Manager Assets, configure y asigne estos campos a las propiedades de Experience Manager Assets.

**Caso práctico**

Una imagen `add-users-workfront.png` existe en `Metadata Syncs` proyecto en la aplicación de Adobe Workfront. Debe enviar esa imagen a Experience Manager Assets as a Cloud Service con los siguientes metadatos:

* Nombre del proyecto

* Nombre de documento

* Descripción del documento

## Requisitos previos {#prerequisites}

* Un administrador puede acceder a las aplicaciones as a Cloud Service de Workfront y Experience Manager Assets.

* Una integración entre [Aplicaciones as a Cloud Service de Workfront y Experience Manager Assets](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FDocuments%2FAdobe_Workfront_for_Experience_Manager_Assets_Essentials%2Fsetup-asset-essentials.htm&amp;_LANG=enus).

## Configuración de la asignación de metadatos en Workfront {#set-up-metadata-mapping}

Para establecer la asignación de metadatos para los campos Nombre del proyecto, Nombre del documento y Descripción del documento en Workfront:

1. Haga clic en el icono Menú principal ![Mostrar menú](assets/show-menu.svg) disponible en la esquina superior derecha de la aplicación de Adobe Workfront y, a continuación, haga clic en **[!UICONTROL Configurar]**.

1. Seleccionar **[!UICONTROL Documentos]** en el panel izquierdo, seleccione **[!UICONTROL Experience Manager Assets]**.

1. Seleccione la integración de Experience Manager Assets y haga clic en **[!UICONTROL Editar]**.

1. Clic **[!UICONTROL Metadatos]**. En el **[!UICONTROL Assets]** pestaña, asigne el [!UICONTROL Proyecto] > [!UICONTROL Nombre] Campo de Workfront a `wm:projectName` Campo de Experience Manager Assets. Si no encuentra la coincidencia exacta, el Adobe recomienda buscar la mejor coincidencia para asignar el campo Workfront y Experience Manager Assets. Puede evitar asignar campos de diferentes tipos de datos. Por ejemplo, asignar un campo de Workfront de fecha a un campo de Assets de descripción.
1. Asignar el [!UICONTROL Documento] > [!UICONTROL Nombre] Campo de Workfront a `wm:documentName` Campo de Experience Manager Assets.

   ![Asignación en Workfront](assets/workfront-metadata-mapping.png)

1. Asignar el [!UICONTROL Documento] > [!UICONTROL Descripción] Campo de Workfront a `dc:description` Campo de Experience Manager Assets.

   >[!VIDEO](https://video.tv.adobe.com/v/344255)

## Envío de la imagen de Workfront a Experience Manager Assets {#send-image-workfront-assets}

Para enviar la imagen de Workfront a Experience Manager Assets:

1. Haga clic en el icono Menú principal ![Mostrar menú](assets/show-menu.svg) disponible en la esquina superior derecha de la aplicación de Adobe Workfront y, a continuación, haga clic en **[!UICONTROL Proyectos]**.

1. Clic **[!UICONTROL Nuevo proyecto]** para crear un nuevo proyecto.

1. Clic **[!UICONTROL Documentos]** opción disponible en el panel izquierdo, arrastre y, a continuación, seleccione la imagen que debe enviar a Experience Manager Assets.

1. Clic **[!UICONTROL Enviar a]**, luego elija el nombre de la integración de Experience Manager Assets Essentials.

   ![Enviar a AEM](assets/send-to-aem.png)

1. Seleccione la carpeta de destino del recurso y haga clic en **[!UICONTROL Seleccionar carpeta]**.

1. Haga clic en **[!UICONTROL Guardar]**.

## Configuración de la asignación de metadatos de recursos en Experience Manager as a Cloud Service {#metadata-mapping-aem}

Después [configuración de la asignación de metadatos de recursos en Adobe Workfront](#set-up-metadata-mapping), debe utilizar la misma asignación en la aplicación as a Cloud Service de Experience Manager Assets para mostrar los resultados de metadatos adecuados para la imagen.

La asignación de metadatos se realiza mediante esquemas de metadatos en Experience Manager Assets. Puede editar un formulario de esquema de metadatos recién agregado o existente. El formulario de esquema de metadatos incluye pestañas y elementos de formulario en pestañas. Puede asignar o configurar estos elementos de formulario a un campo dentro de un nodo de metadatos en el repositorio CRX. Puede agregar pestañas o elementos de formulario al formulario de esquema de metadatos. Para obtener más información, consulte [Esquemas de metadatos](metadata-schemas.md).

Para configurar la asignación de metadatos mediante un nuevo formulario de metadatos en Experience Manager Assets as a Cloud Service:

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de metadatos]**.

1. Clic **[!UICONTROL Crear]** en la barra de herramientas. En el cuadro de diálogo, proporcione el título del formulario de esquema y haga clic en **[!UICONTROL Crear]** para completar el proceso de creación del formulario.

1. Seleccione el formulario de esquema y haga clic en **[!UICONTROL Editar]**.

1. (Opcional) En el Editor de formularios de esquemas de metadatos, haga clic en `+` para crear una nueva pestaña para los campos de Workfront.

1. Haga clic en **[!UICONTROL Generar formulario]** y arrastre la pestaña **[!UICONTROL Texto de línea única]** al formulario. Haga clic en el componente en el formulario. En el **[!UICONTROL Generar formulario]** pestaña:

   1. Especificar `Project Name` en el **[!UICONTROL Etiqueta de campo]** field.

   1. Especificar `./jcr:content/metadata/wm:projectName` en el **[!UICONTROL Asignar a la propiedad]** field. Como guía, utilice la siguiente plantilla para definir las asignaciones de campos en Experience Manager Assets:
      `./jcr:content/metadata/<mapping defined for the field in workfront>`.

      Al configurar asignaciones en Workfront, ha asignado `wm:projectName` Campo de Experience Manager Assets a Proyecto > Nombre del campo de Workfront.

      `wm` hace referencia al nombre de área de nombres y `projectName` hace referencia al título de la propiedad. Utilice el `namespace:propertyTitle` para definir asignaciones de campos de metadatos.

      ![Enviar a AEM](assets/metadata-schema-mapping.png)

1. Haga clic en **[!UICONTROL Generar formulario]** y arrastre la pestaña **[!UICONTROL Texto de línea única]** al formulario. Haga clic en el componente en el formulario. En el **[!UICONTROL Generar formulario]** pestaña:

   1. Especificar `Document Name` en el **[!UICONTROL Etiqueta de campo]** field.

   1. Especificar `./jcr:content/metadata/wm:documentName` en el **[!UICONTROL Asignar a la propiedad]** field.
Al configurar asignaciones en Workfront, ha asignado `wm:documentName` Campo de Experience Manager Assets a Documento > Nombre campo de Workfront.

1. Haga clic en **[!UICONTROL Generar formulario]** y arrastre la pestaña **[!UICONTROL Texto de varias líneas]** al formulario. Haga clic en el componente en el formulario. En el **[!UICONTROL Generar formulario]** pestaña:

   1. Especificar `Document Description` en el **[!UICONTROL Etiqueta de campo]** field.

   1. Especificar `./jcr:content/metadata/dc:description` en el **[!UICONTROL Asignar a la propiedad]** field.
Al configurar asignaciones en Workfront, ha asignado `dc:description` Campo de Experience Manager Assets al campo de Workfront Documento > Descripción.

1. Clic **[!UICONTROL Guardar]** para guardar los cambios.

   >[!VIDEO](https://video.tv.adobe.com/v/344314)

## Aplicar configuración de metadatos a la carpeta de imágenes {#apply-metadata-settings-image-folder}

Después de establecer la configuración de metadatos en la aplicación as a Cloud Service de Experience Manager, aplique esa configuración a la variable [que contiene la imagen enviada desde la aplicación de Workfront](#send-image-workfront-assets).

Para aplicar la configuración de metadatos a la carpeta de imágenes:

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de metadatos]**.

1. Seleccione el esquema de metadatos de la lista disponible y haga clic en **[!UICONTROL Aplicar a las carpetas]**.

1. Seleccione la carpeta de destino a la que [la imagen se envía desde la aplicación de Adobe Workfront](#send-image-workfront-assets) y haga clic en **[!UICONTROL Aplicar]**.

Puede navegar a la imagen en Experience Manager Assets y ver los metadatos asociados a la imagen. Seleccione la imagen y haga clic en **[!UICONTROL Propiedades]** para ver los metadatos de la imagen.
