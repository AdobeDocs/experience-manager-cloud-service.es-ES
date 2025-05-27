---
title: Creación de un formulario mediante el bloque de formularios adaptables
description: 'Empiece a utilizar Edge Delivery Services para AEM Forms. Elabore formularios perfectos rápidamente. Creación basada en documentos de AEM Forms Edge Delivery: velocidad increíble, formularios compatibles con SEO y motores de búsqueda para usuarios más satisfechos.'
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 0cf881a2-3784-45eb-afe8-3435e5e95cf4
source-git-commit: efd4fbb38724632865d87b80827611899e2c6d1f
workflow-type: ht
source-wordcount: '784'
ht-degree: 100%

---

# Creación de un formulario mediante el bloque de formularios adaptables

>[!VIDEO](https://video.tv.adobe.com/v/3427881?quality=12&learn=on)

Edge Delivery Services de AEM Forms proporciona un bloque de formularios adaptables, para crear fácilmente formularios para capturar y almacenar los datos capturados. Puede [crear un nuevo proyecto de AEM preconfigurado con el bloque de formularios adaptables](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) o [añadir el bloque de formularios adaptables a un proyecto de AEM existente](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project).

Estos formularios envían datos directamente a un archivo de Microsoft Excel o Google Sheets, lo que le permite utilizar un ecosistema dinámico y API sólidas de Google Sheets, Microsoft Excel y Microsoft SharePoint para procesar fácilmente los datos enviados o iniciar un flujo de trabajo empresarial existente.

![Ecosistema de creación basada en documentos](/help/edge/assets/document-based-authoring-workflow-create-form.png)


## Requisitos previos

Antes de comenzar, asegúrese de haber completado los siguientes pasos:

* Configure un [proyecto de AEM usando el bloque de formularios adaptables añadido](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) [del elemento repetitivo de AEM Forms al proyecto de AEM existente](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project) y clone el repositorio de GitHub correspondiente en su equipo local.
<!--In this document, the local folder of your Edge Delivery Services (EDS) project is referred as `[EDS Project repository]`.  -->
* Asegúrese de tener acceso a Google Sheets o a Microsoft SharePoint. Para configurar Microsoft SharePoint como fuente de contenido, consulte [Uso de SharePoint](https://www.aem.live/docs/setup-customer-sharepoint).



## Creación de un formulario

<!--
+++ Step 1: Add the Adaptive Forms Block to your Edge Delivery Services (EDS) project.

The Adaptive  empowers users to create forms for an Edge Delivery Service Site. However, this block isn't included in the default AEM boilerplate (used to create an Edge Delivery Services project). To seamlessly integrate the Adaptive Forms Block into your Edge Delivery Services project:

1. **Clone the Adaptive Forms Block repository**: Clone the [Adaptive Forms Block repository](https://github.com/adobe-rnd/form-block) on your local machine. It contains the code to render the form on an EDS webpage. In this document, the local folder of your Forms Block repository is referred as `[Adaptive Forms Block repository]`.
2. **Locate the Adaptive Forms Block Repository:** Access the [Adaptive Forms Block repository]/blocks/src folder and copy its content. 

3. on your local machine and copy the `form` folder. 
4. **Paste the Adaptive Forms Block's code into your EDS Project:**
Navigate to the [EDS Project repository]/blocks/ folder on your local machine and create a 'form' folder. Paste the `[Adaptive Forms Block repository]/blocks/src content`, copied in perevious step to the `[EDS Project repository]/blocks/form` folder.
1. **Commit Changes to GitHub:** Check in the `[EDS Project repository]/blocks/form` folder and its underlying files to your Edge Delivery Services project on GitHub.

After completing these steps, the Adaptive Forms Block is successfully added to your Edge Delivery Services (EDS) project repository on GitHub. You can now create and add forms to a EDS Sites page.
 

**Troubleshooting GitHub build issues**

Ensure a smooth GitHub build process by addressing potential issues:

* **Resolve Module Path Error:**
    If you encounter the error "Unable to resolve path to module "'../../scripts/lib-franklin.js'", navigate to the [EDS Project]/blocks/forms/form.js file. Update the import statement by replacing the lib-franklin.js file with the aem.js file.

* **Handle Linting Errors:**
    Should you come across any linting errors, you can bypass them. Open the [EDS Project]/package.json file and modify the "lint" script from "lint": "npm run lint:js && npm run lint:css" to "lint": "echo 'skipping linting for now'". Save the file and commit the changes to your GitHub project. -->

+++ Paso 1: Crear un formulario con Microsoft Excel o Google Sheets.

En lugar de navegar por procesos complejos, la creación de un formulario se puede lograr fácilmente con una hoja de cálculo. Puede definir las filas y columnas que componen la estructura del formulario. Cada fila representa un [campo de formulario](/help/edge/docs/forms/form-components.md#available-components) individual y los encabezados de columna definen las [propiedades de campo](/help/edge/docs/forms/form-components.md#components-properties) correspondientes.

Por ejemplo, considere la siguiente hoja de cálculo en la que las filas describen los campos de una hoja de cálculo de formulario de [consulta](/help/edge/assets/enquiry.xlsx) y los encabezados de columna definen sus propiedades:

![Hoja de cálculo de consulta](/help/edge/assets/enquiry-form-spreadsheet.png)

Para continuar con la creación del formulario, haga lo siguiente:

1. Acceda a la carpeta del proyecto de Edge Delivery de AEM en Microsoft SharePoint o Google Drive.

1. Cree un libro de Microsoft Excel o una hoja de Google Sheets en cualquier lugar dentro del directorio del proyecto de Edge Delivery de AEM. Por ejemplo, cree una hoja de cálculo llamada `enquiry` en el directorio de proyectos de Edge Delivery de AEM en Google Drive.

   <!-- ![Sample Content on Google Drive](/help/edge/assets/upload-sample-files-to-your-content-folder.png)-->

1. Asegúrese de que la hoja se comparte con el usuario de AEM correspondiente (por ejemplo, `forms@adobe.com`) [según las configuraciones especificadas para su proyecto](https://www.aem.live/docs/setup-customer-sharepoint). Conceda al usuario permiso de edición de la hoja.

1. Abra la hoja de cálculo creada y cambie el nombre de la hoja predeterminada a “shared-aem”.

   ![cambie el nombre de la hoja predeterminada a “shared-default”](/help/edge/assets/rename-sheet-to-shared-default.png)

1. Para añadir los campos del formulario, inserte las filas y los encabezados de columna en la hoja “shared-aem&quot;. Cada fila debe representar un [campo de formulario](/help/edge/docs/forms/form-components.md#available-components), con encabezados de columna que definan las [propiedades](/help/edge/docs/forms/form-components.md#components-properties) del campo correspondiente.


   Para empezar rápidamente, considere la posibilidad de copiar el contenido de la [hoja de cálculo de consulta](/help/edge/assets/enquiry.xlsx) en su hoja de cálculo. Después de copiar el contenido, guárdela.

   >[!VIDEO](https://video.tv.adobe.com/v/3427468?quality=12&learn=on)


1. Utilice [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para obtener una vista previa de la hoja.

   ![Utilice AEM Sidekick para obtener una vista previa de la hoja](/help/edge/assets/preview-form.png)

   Con la vista previa, las nuevas pestañas del explorador muestran el contenido de la hoja en formato JSON. Asegúrese de capturar la URL de la vista previa, ya que es necesaria para procesar el formulario junto a la sección. El formato de la dirección URL es el siguiente:


   ```JSON
       https://<branch>--<repository>--<owner>.aem.live/<form-path>/<form-file-name>.json
   ```

   * `<branch>` hace referencia a la rama del repositorio de GitHub.
   * `<repository>` indica su repositorio de GitHub.
   * `<owner>` hace referencia al nombre de usuario de la cuenta de GitHub que aloja el repositorio de GitHub.

   Por ejemplo, si el repositorio del proyecto se llama “wefinance”, está ubicado en la cuenta “wkndform” y se usa la rama “principal”, la dirección URL tiene el siguiente aspecto:

`https://main--wefinance--wkndform.aem.page/enquiry.json`
&lt;!—(https://main--wefinance--wkndform.aem.page/enquiry.json)-->


+++

+++ Paso 2: Previsualizar el formulario con la página de Edge Delivery Services.


Hasta ahora, ha preparado la estructura del formulario. Ahora, para obtener una vista previa del formulario:

1. Abra su cuenta de Microsoft SharePoint o de Google Drive y vaya al directorio del proyecto de Edge Delivery de AEM.



1. Abra un archivo de documento (por ejemplo, un archivo de índice) para incrustar el formulario. También puede [crear un nuevo documento](/help/edge/assets/enquiry-form.docx).

1. Desplácese hasta la ubicación deseada dentro del documento donde quiere añadir el formulario.

1. Para crear un bloque de formulario para procesar el formulario. Seleccione Insertar > Tabla y cree una tabla con una columna y dos filas. Asigne el nombre “Formulario” a la tabla y pegue la dirección URL de vista previa en la segunda fila. Asegúrese de que la dirección URL tenga el formato de hipervínculo, no de texto sin formato, como se muestra a continuación:

   | Formulario |
   |---|
   | `https://main--wefinance--wkndform.aem.live/enquiry.json` |


   ![Añadir un bloque de formularios adaptables a su página web](/help/edge/assets/enquiry-doc-to-embed-form.png)

   Este bloque sirve como marcador de posición donde está incrustado el formulario. En la segunda fila del bloque, añada la URL de vista previa de su archivo `<form>.json` como hipervínculo.

   >[!IMPORTANT]
   >
   >
   > Asegúrese de que la dirección URL tenga formato de hipervínculo en lugar de mostrarse como texto sin formato.


1. Utilice [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para obtener una vista previa del documento. La página ahora muestra el formulario. Por ejemplo, este es el formulario basado en la [hoja de cálculo consulta](/help/edge/assets/enquiry-form.docx):


   [![Un formulario EDS de muestra](/help/edge/assets/updated-form.png)](https://main--wefinance--wkndform.aem.page/enquiry-form)

   Ahora, rellene el formulario y haga clic en el botón Enviar. Se producirá un error similar al siguiente, ya que la hoja de cálculo aún no está configurada para aceptar los datos.

   ![error al enviar el formulario](/help/edge/assets/form-error.png)

+++


## Siguiente paso

[Prepare su hoja de cálculo](/help/edge/docs/forms/submit-forms.md) para empezar a aceptar datos al enviar el formulario.


## Véase también

{{see-more-forms-eds}}
