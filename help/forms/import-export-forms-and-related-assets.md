---
title: Cómo importar y exportar recursos a [!DNL AEM Forms]?
description: Aprenda a utilizar DocuSign con un formulario adaptable para recopilar firmas electrónicas.
source-git-commit: 7e3eb3426002408a90e08bee9c2a8b7a7bfebb61
workflow-type: tm+mt
source-wordcount: '1314'
ht-degree: 95%

---


# Importar y exportar recursos {#importing-and-exporting-assets-to-aem-forms}

Puede mover formularios, temáticas, plantillas, fragmentos de documentos, y otros recursos entre diferentes instancias de [!DNL AEM Forms]. Este movimiento es necesario al migrar sistemas o mover formularios de un servidor de desarrollo o pruebas a un servidor de producción.

Para aquellos recursos para los que es compatible cargar e importar mediante la interfaz de usuario de [!DNL AEM Forms], el uso de la interfaz de usuario de Forms es la forma recomendada de exportar o importar. No se recomienda utilizar el administrador de paquetes de AEM para exportar o importar estos recursos.

## Descargar o cargar recursos de formularios y documentos {#download-or-upload-forms-amp-documents-assets}

[!DNL AEM Forms] AEM AEM La interfaz de usuario de permite exportar recursos desde una instancia de descargándolos como un paquete CRX o como archivos binarios de la interfaz de usuario de CRX de la. A continuación, puede importar el paquete CRX de AEM descargado o el archivo binario en otra instancia de AEM.

Exportar e importar mediante la interfaz de usuario de [!DNL AEM Forms] es compatible para todos los recursos, excepto para las plantillas de formulario adaptable y las directivas de contenido de formulario adaptable. Por lo tanto, al exportar un formulario adaptable desde la interfaz de usuario de [!DNL AEM Forms], la plantilla del formulario adaptable y las directivas de contenido relacionadas no se exportan automáticamente como otros recursos relacionados.

Para estos tipos de recursos, debe utilizar el administrador de paquetes de AEM para crear un paquete CRX en el servidor de AEM fuente e instalar el paquete en el servidor de destino. Para obtener información sobre cómo crear e instalar paquetes, consulte [Implementar en AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=es).

### Descargar recursos de formularios y documentos {#download-forms-amp-documents-assets}

Para descargar recursos de formularios y documentos:

1. Inicie sesión en la instancia de [!DNL AEM Forms].
1. Pulse en el icono de Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) > Navegación ![icono de brújula](assets/Smock_Compass_18_N.svg) > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.
1. Seleccione los recursos de los formularios y pulse en el icono **[!UICONTROL Descargar]**.
1. En Descargar recursos, elija una de las siguientes opciones y pulse **[!UICONTROL Descargar]**.

   * **Descargar como paquete CRX:** Utilice la opción para descargar y mover todos los recursos seleccionados y las dependencias relacionadas de una instancia de [!DNL AEM Forms] a otra. Descarga todos los recursos y carpetas como un paquete crx. Cualquier activo de formulario, incluidos los formularios creados en AEM (formularios adaptables y fragmentos de formularios adaptables), documentos PDF y recursos (XSD, XFS, imágenes), se puede descargar como paquete desde la interfaz de usuario de [!DNL AEM Forms]. 
La ventaja de descargar recursos como un paquete es que también descarga recursos que el recurso seleccionado para descargar ha utilizado. Por ejemplo, si tiene un formulario adaptable que utiliza una plantilla de formulario, XSD y una imagen. Al seleccionar este formulario adaptable y descargarlo como paquete, el paquete descargado también contiene la plantilla de formulario, XSD y la imagen. También se descargan todas las propiedades de metadatos (incluidas las propiedades personalizadas) asociadas al recurso.

   * **Descargar recursos como archivos binarios:** Utilice la opción para descargar solo plantillas de formulario (XDP), Formularios PDF (PDF), documento (PDF) y recursos (imágenes, esquemas, hojas de estilo). Puede editar estos recursos con aplicaciones externas. Descarga los recursos de formularios que poseen binarios, como XSD, XDP, imágenes, PDF y XDP como un archivo .zip. 
No puede descargar formularios adaptables, fragmentos de formularios adaptables y temáticas con la opción **[!UICONTROL Descargar recursos como archivos binarios]**. Para descargar estos recursos, debe utilizar la opción **[!UICONTROL Descargar como paquete CRX]**.

   Los recursos seleccionados se descargan como un archivo (archivo .zip).

   >[!NOTE]
   >
   >Tanto el paquete de AEM como los archivos binarios se descargan como un archivo (archivo .zip). Las plantillas de los recursos no se descargan junto con los recursos. Debe exportar las plantillas de recursos por separado.

### Cargar recursos {#upload-forms-amp-documents-assets}

Para cargar recursos de formularios y documentos:

1. Inicie sesión en la instancia de [!DNL AEM Forms].
1. Pulse en el icono de Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) > Navegación ![icono de brújula](assets/Smock_Compass_18_N.svg) > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.
1. Pulse **Crear** > **Cargar archivo**. Aparecerá un cuadro de diálogo para cargar formularios o paquetes.
1. En el cuadro de diálogo, examine y seleccione el paquete o el archivo que desea importar. También puede seleccionar documentos PDF, XSD, imágenes, hojas de estilo y formularios XDP. Pulse **[!UICONTROL Abrir]**. La carpeta o el nombre de archivo que seleccione no deben incluir caracteres especiales.

   En el cuadro de diálogo, compruebe los detalles de los recursos que se están cargando y pulse **[!UICONTROL Cargar]**.

   En caso de que cargue un recurso de formularios existente, este se actualizará.

   >[!NOTE]
   >
   >La carga de un paquete no reemplaza la jerarquía de carpetas existente. Por ejemplo, si tiene un formulario adaptable llamado “Aprendizaje” en la ubicación /content/dam/formsanddocuments en un servidor. El formulario adaptable se descarga y se carga en otro servidor. El segundo servidor también tiene una carpeta llamada “Aprendizaje” en la misma ubicación /content/dam/formsanddocuments. La carga falla.

## Descargar o cargar una temática {#downloading-or-uploading-a-theme}

Con [!DNL AEM Forms], puede crear, descargar o cargar temáticas. Se crea una temática como otros recursos, como formularios, documentos y cartas. Puede crear una temática, descargarla y cargarla en una instancia independiente para reutilizarla. Para obtener más información sobre las temáticas, consulte [Temáticas](themes.md), en [!DNL AEM Forms].

### Descargar una temática {#downloading-a-theme}

Puede exportar temáticas en [!DNL AEM Forms], que puede utilizar en otros proyectos o instancias. AEM le permite descargar una temática como archivo zip, que puede cargar en la instancia.

Para descargar una temática:

1. Inicie sesión en la instancia de [!DNL AEM Forms].
1. Pulse en el icono de Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) > Navegación ![icono de brújula](assets/Smock_Compass_18_N.svg) > **[!UICONTROL Formularios]** > **[!UICONTROL Temáticas]**.
1. Seleccione la temática y pulse **[!UICONTROL Descargar]**. La temática se descarga como archivo (archivo .zip).

### Cargar una temática {#uploading-a-theme}

Puede utilizar las temáticas creadas con ajustes preestablecidos de estilo en su proyecto. Puede importar paquetes de temáticas que otros creen cargándolos en su proyecto.

Para cargar una temática:

1. En Experience Manager, vaya a **[!UICONTROL Formularios]** > **[!UICONTROL Temáticas de formularios]**.
1. En la página Temáticas, haga clic en **[!UICONTROL Crear formularios]** > **[!UICONTROL Cargar archivos de formularios]**.
1. En la solicitud de carga de archivos, examine y seleccione un paquete de temáticas en su equipo y haga clic en **[!UICONTROL Cargar formularios]**. Se carga la temática.

<!--

## Import and export assets in Correspondence Management {#import-and-export-assets-in-correspondence-management}

To share assets, such as data dictionaries, letters, and document fragments, between two different implementations of Correspondence Management, you can create and share .cmp files. A .cmp file can include one or more data dictionaries, letters, document fragments, and forms.

### Export Document Fragments, Letters, and/or Data Dictionaries {#export-document-fragments-letters-and-or-data-dictionaries}

1. In the letters, document fragments, or data dictionary pages, tap and select the assets you want to export to a single package, and then tap Queue For Download. The assets are lined-up for export.
1. As required, repeat the above step to add letters, document fragments, and data dictionaries.
1. Tap **Download**.
1. Correspondence Management displays Download Asset(s) dialog with a list of assets in the export list.

   ![export](assets/export.png)

1. To view the dependencies that are exported, Tap Resolve. Or skip to the next step. Even if you do not tap resolve, the dependencies are still exported.
1. To download the .cmp file, tap **OK**.
1. Correspondence Management downloads a .cmp file to your computer.

   The .cmp file includes the exported assets. You can share the .cmp file with others. Other users can import the .cmp file in a different server to get all the assets in the new server.

### Export all the Correspondence Management assets as a package {#export-all-the-correspondence-management-assets-as-a-package}

Use this option to download all the Correspondence Management assets and related dependencies as a package from an [!DNL AEM Forms] instance.

For example, if Correspondence Management has a letter that uses an image and text, the downloaded package also contains the image and the text related to the letter. All the metadata properties (including custom properties) associated with the asset are also downloaded. Once you have downloaded the package (.cmp), you can [import the package to a different [!DNL AEM Forms] instance](import-export-forms-templates.md#p-upload-forms-documents-assets-p).

To download all the Correspondence Management assets and related dependencies as a package, complete the following steps:

1. Log in to [!DNL AEM Forms] server as a forms user.
1. Tap **Adobe Experience Manager** in the Global Navigation bar.
1. Tap tools ( ![tools](assets/tools.png)) and then tap **Forms**.
1. Tap **Export Correspondence Management Assets**.

   ![publish-cmp-assets-1](assets/publish-cmp-assets-1.png)

   ( ``The Export All Correspondence Management Assets page appears and displays the information about the last time the Export process was attempted and a link to download the last successfully exported package.

   ![export-last-run-details](assets/export-last-run-details.png)

1. Tap **Export** and, in the confirm message, tap **OK**.

   After a batch process is complete, the last run details and the link to download the package are updated. This includes information such as the Administrator login and if the batch run successfully or failed. The assets are exported to a package and the Download Exported Package link appears.

   >[!NOTE]
   >
   >The Export All Assets process cannot be canceled once initiated. Also, while the export all operation is in process, do not create, delete, modify, or publish any assets or initiate Publish All Assets process.a

1. Tap the **Download Exported Package** link to download the package file.

   To add the assets in the package to another instance of Correspondence Management, [import the package to an [!DNL AEM Forms] instance](import-export-forms-templates.md#p-upload-forms-documents-assets-p).

### Import Document Fragments, Letters and/or Data Dictionaries into Correspondence Management {#import-document-fragments-letters-and-or-data-dictionaries-into-correspondence-management}

You can import assets that are exported into a .cmp file. A .cmp file can have one or more letters, data dictionaries, document fragments, and dependent assets.

>[!NOTE]
>
>While importing old Correspondence Management assets for migration, log in using an Admin account. For more information on Migrating old Correspondence Management assets, see [Migrate Correspondence Management assets to AEM 6.1 forms](migration-utility.md).

1. On the data dictionary, letters, or document fragments page, tap **Create &gt; File Upload** and select the .cmp file.
1. Correspondence Management displays the Import Assets dialog with the list of assets that are imported. Tap **Import**.

   After importing the assets, the following properties of the assets are updated while the other properties remain the same:

    * Author: Displays the ID of the user that imported the asset to the server
    * Modified: The time when the asset was imported to the server

   >[!NOTE]
   >
   >For you to be able to upload XDPs (as part of the cmp file or otherwise), you need to be a part of forms-power-users group. For access rights, contact the administrator.
-->

## Exportar una aplicación de flujo de trabajo {#export-a-workflow-application}

Puede utilizar el administrador de paquetes de AEM para exportar aplicaciones de flujo de trabajo. El procedimiento es el siguiente:

1. Abra el administrador de paquetes de [!DNL AEM Forms].
1. Haga clic en **[!UICONTROL Crear paquete]**. Se abre el cuadro de diálogo **[!UICONTROL Nuevo paquete]**.
1. Especifique el nombre, la versión y el grupo para el paquete. Haga clic en **[!UICONTROL Aceptar]**.
1. Haga clic en **[!UICONTROL Editar]** y abra la pestaña **[!UICONTROL Filtros]**. Haga clic en **[!UICONTROL Añadir filtro]**. Especifique la ruta de la aplicación de flujo de trabajo. Por ejemplo: /etc/fd/dashboard/startpoints/homemortgage. Haga clic en **[!UICONTROL Añadir regla]**.

1. Abra la pestaña **[!UICONTROL Avanzado]**. Seleccione **[!UICONTROL Combinar]** o **[!UICONTROL Sobrescribir]** en el campo Administrar ACL. Haga clic en **[!UICONTROL Guardar]**.
1. Haga clic en **[!UICONTROL Generar]** para crear el paquete.

   Una vez generado el paquete, puede descargarlo e importarlo al otro servidor. La aplicación de flujo de trabajo aparece en el servidor donde se carga el paquete.

   >[!NOTE]
   >
   >Para que la aplicación de flujo de trabajo funcione correctamente, exporte también el correspondiente modelo de flujo de trabajo y formulario adaptable con la aplicación de trabajo.

## Carpetas y organización de recursos {#folders-and-organizing-assets}

La interfaz de usuario de [!DNL AEM Forms] utiliza carpetas para organizar los recursos. Estas carpetas se utilizan para organizar los recursos creados en la interfaz de usuario de [!DNL AEM Forms]. Puede cambiar el nombre, crear subcarpetas y almacenar recursos y documentos en estas carpetas. La organización de documentos y recursos en una carpeta permite agrupar los archivos para facilitar la administración. Puede seleccionar una carpeta y elegir descargarla o eliminarla.

Para crear una carpeta, complete los siguientes pasos:

### Cree una carpeta. {#create-a-folder}

1. Inicie sesión en la interfaz de usuario de [!DNL AEM Forms], en `https://<server>:<port>/aem/forms.html`.
1. Vaya a la ubicación en la que desea crear una carpeta.
1. Pulse **[!UICONTROL Crear]** > **[!UICONTROL Carpeta]**.
1. Introduzca la siguiente información:

   * **Título:** Nombre para mostrar de la carpeta
   * **Nombre:** *(Obligatorio)* El nombre del nodo en el que desea almacenar la carpeta en el repositorio

   >[!NOTE]
   >
   >De forma predeterminada, el valor del campo de nombre se rellena automáticamente a partir del título. El nombre solo puede contener caracteres alfanuméricos o los caracteres especiales guion (-) y guion bajo (_). Cualquier otro carácter especial especificado en el título se reemplaza automáticamente por un guion y se le solicita que confirme el nuevo nombre. Puede elegir continuar con el nombre sugerido o editarlo más adelante.

1. Se muestra una nueva carpeta con el título que haya definido en la ubicación actual de la lista de recursos.

   Si existe una carpeta con el nombre especificado, el envío falla con un error. Puede ver el mensaje de error pasando el puntero sobre el icono de error ![aem6forms_error_alert](assets/Smock_Alert_18_N.svg) que aparece junto al campo de nombre.

   Puede pulsar la carpeta recién creada para entrar en ella y crear recursos o carpetas dentro de la carpeta. Además, puede seleccionar una carpeta y elegir colocarla en la cola para descargarla, eliminarla o editar su nombre.

<!-- ### Create copies of one or more assets or letters {#create-copies-of-one-or-more-assets-or-letters}

You can use an existing assets and letters to quickly create a assets and letters with similar properties, content, and inherited assets. You can copy and paste data dictionaries, document fragments, and letters.

Complete the following steps to create copies of assets and letters:

1. In the relevant Assets or Letters page, select one or more assets/letters. The UI displays the Copy icon.
1. Tap Copy. The UI displays the Paste icon. You can also choose to go/navigate inside a folder before you paste. Different folders can contain assets with same names. For more information on folders, see [Folders and organizing assets](#folders-and-organizing-assets).
1. Tap Paste. The Paste dialog appears. The system auto generates names and titles to the new copies of assets/letters, but you can edit the titles and names of the assets/letters.

   If you are copying and pasting the assets/letters at the same place, a suffix "-CopyXX" gets added to the existing name of the asset/letter. If no title existed for the copied asset/letter, the auto generated title field remains blank.

1. If required, edit the Title and Name with which you want to save the copy of the asset/letter.
1. Tap Paste. New copies of the copied assets are created.

## Search {#search-forms}

[!DNL AEM Forms] UI lets you search your content. Using the top bar, you can tap Search **[A]** to search your content for resources such as assets and documents.

When you search for assets, [!DNL AEM Forms] displays the side panel. You can also tap ![assets-browser-content-only](assets/assets-browser-content-only.png) &gt; Filter **[B]** to invoke the side panel. Using the various filters in the side panel, you can narrow down your search. The side panel also lets you save your searches.

![search_topbar](assets/search_topbar.png)

**A.** Search **B.** Filter

![Side panel - Filters](assets/search_sidepanel.png)

Side panel - Filters

On the side panel, you can use the following to narrow down your search results:

* Search Directory
* Tags
* Search Criteria; for example, Modified Dates, Publish Status, LiveCopy Status.

The side panel also lets you save your search settings with names of your choice.

For more information and instructions on using search, filters, saved search, and side panel, see [Search](/help/sites-authoring/search.md).

-->
