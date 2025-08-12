---
title: Cómo importar, exportar y organizar formularios adaptables o PDF forms en una instancia de AEM Forms
description: Obtenga información sobre cómo migrar Forms adaptable, PDF form, temáticas y otros recursos de soporte desde y hacia instancias de AEM.
topic-tags: forms-manager
role: Admin, User
feature: Adaptive Forms
exl-id: f5105fb7-b8c0-4656-8095-b21d392746c0
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 100%

---

# Importar o exportar formularios adaptables y recursos de AEM Forms {#importing-and-exporting-assets-to-aem-forms}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/manage-administer-aem-forms/import-export-forms-templates) |
| AEM as a Cloud Service | Este artículo |

Puede mover formularios adaptables y recursos relacionados, como temáticas de formulario adaptable, modelo de datos de formulario (FDM), plantillas de formularios adaptables, fragmentos y PDF forms, entre las instancias de [!DNL AEM Forms].

## Descargar formularios adaptables, PDF forms o recursos relacionados {#download-forms-amp-documents-assets}

Para descargar formularios o recursos relacionados:

1. Inicie sesión en su instancia de [!DNL Experience Manager Forms].
1. Seleccione **[!UICONTROL Forms]** > **[!UICONTROL Formularios y documentos]**.

   ![Seleccionar Forms](/help/forms/assets/select-forms.png)

1. Seleccione los recursos y haga clic en el icono **[!UICONTROL Descargar]** del carril superior.

   ![Descargar Forms](/help/forms/assets/download-form.png)

   Cuando descargue el formulario, se abre el cuadro de diálogo **[!UICONTROL Descargar recursos]**.

   ![Descargar recursos de Forms](/help/forms/assets/download-form-assets.png)

1. Haga clic en **[!UICONTROL Descargar]**.

Los recursos seleccionados se descargan como un archivo (archivo .zip).

## Cargar formularios adaptables, PDF forms o recursos relacionados {#upload-forms-amp-documents-assets}

Puede cargar los tipos de recursos compatibles de forma individual o como archivo ZIP. Para un archivo ZIP, se muestran las rutas relativas de todos los recursos compatibles. Los recursos que no sean compatibles dentro del ZIP se ignoran y no aparecen en la lista. Sin embargo, si el archivo ZIP contiene solo los recursos no compatibles, se muestra un mensaje de error en lugar del cuadro de diálogo emergente.
Para cargar un formulario o un recurso relacionado:

1. Inicie sesión en su instancia de [!DNL Experience Manager Forms].
1. Seleccione **[!UICONTROL Forms]** > **[!UICONTROL Formularios y documentos]**.

   ![Seleccionar Forms](/help/forms/assets/select-forms.png)

1. Seleccione **[!UICONTROL Crear]** > **[!UICONTROL Cargar archivo]**. Aparecerá un cuadro de diálogo.

   ![Cargar Forms](/help/forms/assets/form-upload.png)

1. En el cuadro de diálogo, examine y seleccione el paquete o el archivo que desea importar. También puede seleccionar otros tipos de archivo compatibles. Seleccione **[!UICONTROL Abrir]**. La carpeta o el nombre de archivo que seleccione no deben incluir caracteres especiales.

   En el cuadro de diálogo, compruebe los detalles de los recursos que se están cargando y seleccione **[!UICONTROL Cargar]**.

   En caso de que cargue un recurso de formularios existente, este se actualizará.

   >[!NOTE]
   >
   > Cuando un nombre entra en conflicto con diferentes tipos de recursos, la carga de un paquete no reemplaza la jerarquía de carpetas existente. Por ejemplo, si tiene un formulario adaptable llamado “Formación” en la ubicación `/content/dam/formsanddocuments` en un servidor. Se puede descargar el formulario adaptable y cargarlo en otro servidor. El segundo servidor también tiene una carpeta llamada “Formación” en la misma ubicación `/content/dam/formsanddocuments`. La carga falla.

## Descargar una temática

Puede exportar temáticas en [!DNL AEM Forms], que puede utilizar en otros proyectos o instancias. AEM le permite descargar temáticas como archivo zip, que puede cargar en la instancia.
Para descargar una temática:

1. Inicie sesión en la instancia de autor de [!DNL Experience Manager Forms].
1. Seleccione **[!UICONTROL Formularios]** > **[!UICONTROL Temáticas]**.

   ![Seleccionar tema](/help/forms/assets/select-theme.png)

1. En la página Temáticas, seleccione el tema y haga clic en el icono **[!UICONTROL Descargar]** del carril superior.

   ![Descargar tema](/help/forms/assets/download-theme.png)

   Cuando descargue el tema, se abre el cuadro de diálogo **[!UICONTROL Descargar recursos]**.

   ![Descargar recursos del tema](/help/forms/assets/download-theme-asset.png)

1. Haga clic en **[!UICONTROL Descargar]**.

Los recursos seleccionados se descargan como un archivo (archivo .zip).

## Cargar una temática {#uploading-a-theme}

Se pueden cargar y usar las temáticas que otras personas hayan creado en sus formularios.
Para cargar una temática:

1. Inicie sesión en su instancia de [!DNL Experience Manager Forms].
1. En Experience Manager, vaya a **[!UICONTROL Formularios]** > **[!UICONTROL Temáticas]**.

   ![Seleccionar tema](/help/forms/assets/select-theme.png)

1. En la página Temáticas, haga clic en **[!UICONTROL Crear]** > **[!UICONTROL Cargar archivos]**.

   ![Cargar tema](/help/forms/assets/theme-upload.png)

1. Examine y seleccione un paquete de temas del equipo y haga clic en **[!UICONTROL Cargar]**. El tema cargado estará disponible en la página Temáticas.

## Utilizar carpetas para organizar formularios adaptables, PDF forms y otros recursos relacionados  {#folders-and-organizing-assets}

Puede utilizar carpetas para organizar los recursos. La organización de documentos y recursos en una carpeta le permite agrupar los archivos para facilitar la administración. Puede seleccionar una carpeta y elegir descargarla o eliminarla.

### Crear una carpeta. {#create-a-folder}

Para crear una carpeta:

1. Inicie sesión en su instancia de [!DNL Experience Manager Forms].
1. Seleccione **[!UICONTROL Forms]** > **[!UICONTROL Formularios y documentos]**.

   ![Seleccionar formulario](/help/forms/assets/select-forms.png)

1. Seleccione **[!UICONTROL Crear]** > **[!UICONTROL Carpeta]**.

   ![Crear carpeta](/help/forms/assets/create-folder.png)

   Se abre el cuadro de diálogo **[!UICONTROL Añadir carpeta]**.
1. Escriba el **[!UICONTROL Título]**. El **[!UICONTROL Nombre]** se rellena automáticamente a medida que escribe el **[!UICONTROL Título]**.

   ![Añadir carpeta](/help/forms/assets/add-folder.png)

1. Haga clic en **[!UICONTROL Crear]**.

   >[!NOTE]
   >
   >De forma predeterminada, el valor del campo de nombre se rellena automáticamente a partir del título. El nombre solo puede contener caracteres alfanuméricos o los caracteres especiales guion (-) y guion bajo (_). Cualquier otro carácter especial especificado en el título se reemplaza automáticamente por un guion y se le solicita que confirme el nuevo nombre. Puede elegir continuar con el nombre sugerido o editarlo más adelante.

Se muestra una nueva carpeta con el título que haya definido en la ubicación actual de la lista de recursos.

Si existe una carpeta con el nombre especificado, el envío falla con un error. Puede ver el mensaje de error pasando el puntero por encima del icono de error ![aem6forms_error_alert](assets/Smock_Alert_18_N.svg) que aparece junto al campo de nombre.

Puede seleccionar la carpeta creada para entrar en ella y crear recursos o carpetas dentro de la carpeta. Además, puede seleccionar una carpeta y elegir colocarla en la cola para descargarla, eliminarla o editar su nombre.

### Crear copias de uno o varios recursos {#create-copies-of-one-or-more-assets-or-letters}

Puede utilizar los recursos existentes para crear rápidamente un recurso con propiedades, contenido y recursos heredados similares.

Para crear copias de recursos:

1. Inicie sesión en su instancia de [!DNL Experience Manager Forms].
1. En la página de recursos correspondiente, seleccione uno o varios recursos. La interfaz de usuario muestra el icono **[!UICONTROL Copiar]**.
1. Seleccione **[!UICONTROL Copiar]**. La interfaz de usuario muestra el icono ![Pegar](/help/forms/assets/Smock_Paste_18_N.svg).

   ![Copiar recursos](/help/forms/assets/copy-asset.png)

   También puede ir a una carpeta o navegar por ella antes de pegar elementos en ella. Las distintas carpetas pueden contener recursos con los mismos nombres. Para obtener más información sobre las carpetas, consulte [Carpetas y organización de recursos](#folders-and-organizing-assets).
1. Seleccione **[!UICONTROL Pegar]**.

   ![Pegar recurso](/help/forms/assets/paste-asset.png)

1. Aparecerá el cuadro de diálogo **[!UICONTROL Pegar]**. El sistema genera automáticamente nombres y títulos para las nuevas copias de los recursos, pero puede editar tanto los títulos como los nombres.

   Si está copiando y pegando los recursos en el mismo sitio, se añade el sufijo “-CopyXX” al nombre existente del `asset`. Si no existe ningún título para el recurso copiado, el campo de título generado automáticamente permanece en blanco.

   ![Pegar recurso en una nueva ubicación](/help/forms/assets/paste-click-asset.png)

   Si es necesario, edite el **[!UICONTROL Título]** con el que desea guardar la copia del recurso. El **[!UICONTROL Nombre]** se rellena automáticamente a medida que escribe **[!UICONTROL Título]**.
1. Seleccione **[!UICONTROL Pegar]**. Se crean nuevas copias de los recursos copiados.

## Búsqueda {#search-forms}

Cuando hay un número elevado de recursos, la búsqueda del recurso adecuado puede tardar bastante tiempo. Puede realizar una búsqueda basada en texto de un recurso específico en la página de recursos.

Para buscar el recurso:

1. Inicie sesión en su instancia de [!DNL Experience Manager Forms].
1. Haga clic en el icono de búsqueda ![icono de búsqueda](assets/folder-search-icon.svg).

   ![Buscar formulario](/help/forms/assets/search-form.png)

1. Escriba el nombre del recurso que desea buscar en la barra de búsqueda.

1. Aparece una lista de los recursos relacionados. Seleccione el recurso que desee en la lista de recursos mostrada.

   ![Buscar recursos](/help/forms/assets/search-bar.png)

Para obtener más información e instrucciones sobre el uso de la búsqueda, consulte [Buscar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=es).

<!--
## Export or create a package {#export-a-workflow-application}

You can use packages to install new content, install new functionality, transfer content between instances, and back up content.
To export or create a package:

1. Log in to your [!DNL Experience Manager Forms] instance.
1. Navigate to **[!UICONTROL Tools]** ![hammer](assets/hammer.png) &gt; **[!UICONTROL Deployment]** &gt; **[!UICONTROL Packages]**.

   ![Package Manager](/help/forms/assets/package-manager.png)

1. Click **[!UICONTROL Create Package]**.

   ![Create package](/help/forms/assets/create-package.png)   
   
   When **[!UICONTROL Create Package]** is clicked, the **[!UICONTROL New Package]** dialog box appears.
1. Specify the package name, version, and group for the package. 
   
   ![New package](/help/forms/assets/new-package.png)  

   * **Package Name** - Select a descriptive name to help you identify the contents of the package.

   * **Version** - It is a textual field to indicate a version. This is appended to the package name to form the name of the zip file.

   * **Group** - This is the target group (or folder) name. Groups help you organize your packages. A folder is created for the group if it does not already exist. If you leave the group name blank, it creates the package in the main package list.

1. Click **[!UICONTROL OK]**.

   Once the package is created, it appears at the top of the list of packages.

1. Click **[!UICONTROL Edit]**.
   
   ![Edit Package](/help/forms/assets/edit-package.png)
    
1. Open the **[!UICONTROL Filters]** tab.
   
   ![Open filter tab](/help/forms/assets/add-filter-package.png)
   
1.  Click **[!UICONTROL Add Filter]**. 
   
      ![Add filter](/help/forms/assets/add-filter.png)

      You can specify the path of the package. You can also add rules and other validations for the package.

      ![Add path](/help/forms/assets/add-path.png)

1. Click **[!UICONTROL Save]** after you are finished editing the settings.
1. Click **[!UICONTROL Build]** to create the package.
    
     ![Build path](/help/forms/assets/build-package.png)

   After the package is built, you can download the package and import it to the other server. The workflow application appears on the server where the package is uploaded.

   >[!NOTE]
   >
   >For the workflow application to work properly, also export the corresponding Adaptive Form and workflow model with the work application.

   Once a package is uploaded to AEM, you can modify its settings. You can also download or delete the package.

## Import and export assets in Correspondence Management {#import-and-export-assets-in-correspondence-management}

To share assets, such as data dictionaries, letters, and document fragments, between two different implementations of Correspondence Management, you can create and share .cmp files. A .cmp file can include one or more data dictionaries, letters, document fragments, and forms.

### Export Document Fragments, Letters, and/or Data Dictionaries {#export-document-fragments-letters-and-or-data-dictionaries}

1. In the letters, document fragments, or data dictionary pages, select and select the assets you want to export to a single package, and then select Queue For Download. The assets are lined-up for export.
1. As required, repeat the above step to add letters, document fragments, and data dictionaries.
1. Select **Download**.
1. Correspondence Management displays Download Asset(s) dialog with a list of assets in the export list.

   ![export](assets/export.png)

1. To view the dependencies that are exported, Select Resolve. Or skip to the next step. Even if you do not select resolve, the dependencies are still exported.
1. To download the .cmp file, select **OK**.
1. Correspondence Management downloads a .cmp file to your computer.

   The .cmp file includes the exported assets. You can share the .cmp file with others. Other users can import the .cmp file in a different server to get all the assets in the new server.

### Export all the Correspondence Management assets as a package {#export-all-the-correspondence-management-assets-as-a-package}

Use this option to download all the Correspondence Management assets and related dependencies as a package from an [!DNL AEM Forms] instance.

For example, if Correspondence Management has a letter that uses an image and text, the downloaded package also contains the image and the text related to the letter. All the metadata properties (including custom properties) associated with the asset are also downloaded. Once you have downloaded the package (.cmp), you can [import the package to a different [!DNL AEM Forms] instance](import-export-forms-templates.md#p-upload-forms-documents-assets-p).

To download all the Correspondence Management assets and related dependencies as a package, complete the following steps:

1. Log in to [!DNL AEM Forms] server as a forms user.
1. Select **Adobe Experience Manager** in the Global Navigation bar.
1. Select tools ( ![tools](assets/tools.png)) and then select **Forms**.
1. Select **Export Correspondence Management Assets**.

   ![publish-cmp-assets-1](assets/publish-cmp-assets-1.png)

   ( ``The Export All Correspondence Management Assets page appears and displays the information about the last time the Export process was attempted and a link to download the last successfully exported package.

   ![export-last-run-details](assets/export-last-run-details.png)

1. Select **Export** and, in the confirm message, select **OK**.

   After a batch process is complete, the last run details and the link to download the package are updated. This includes information such as the Administrator login and if the batch run successfully or failed. The assets are exported to a package and the Download Exported Package link appears.

   >[!NOTE]
   >
   >The Export All Assets process cannot be canceled once initiated. Also, while the export all operation is in process, do not create, delete, modify, or publish any assets or initiate Publish All Assets process.a

1. Select the **Download Exported Package** link to download the package file.

   To add the assets in the package to another instance of Correspondence Management, [import the package to an [!DNL AEM Forms] instance](import-export-forms-templates.md#p-upload-forms-documents-assets-p).

<!-- ### Import Document Fragments, Letters and/or Data Dictionaries into Correspondence Management {#import-document-fragments-letters-and-or-data-dictionaries-into-correspondence-management}

You can import assets that are exported into a .cmp file. A .cmp file can have one or more letters, data dictionaries, document fragments, and dependent assets.

>[!NOTE]
>
>While importing old Correspondence Management assets for migration, log in using an Admin account. For more information on Migrating old Correspondence Management assets, see [Migrate Correspondence Management assets to AEM 6.1 forms](migration-utility.md).

1. On the data dictionary, letters, or document fragments page, select **Create &gt; File Upload** and select the .cmp file.
1. Correspondence Management displays the Import Assets dialog with the list of assets that are imported. Select **Import**.

   After importing the assets, the following properties of the assets are updated while the other properties remain the same:

    * Author: Displays the ID of the user that imported the asset to the server
    * Modified: The time when the asset was imported to the server

   >[!NOTE]
   >
   >For you to be able to upload XDPs (as part of the cmp file or otherwise), you need to be a part of forms-power-users group. For access rights, contact the administrator. -->

## Consulte también {#see-also}

{{see-also}}
