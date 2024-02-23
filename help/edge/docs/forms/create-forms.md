---
title: Introducción al servicio de entrega de AEM Forms Edge
description: ¡Crea formas perfectas, rápido! ⚡ la creación basada en documentos de AEM Forms Edge Delivery = una velocidad increíble y formularios compatibles con SEO para usuarios y motores de búsqueda más felices.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 87ed5f0aed5554f56e28f317d1399429245a2d06
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 1%

---


# Creación de un formulario en el servicio de entrega perimetral de AEM Forms

En la era digital de hoy en día, la creación de formularios fáciles de usar es esencial para cualquier organización. AEM Forms Edge Delivery le permite crear formularios con herramientas conocidas, como documentos de Word o Google.

Estos formularios envían datos directamente a un archivo de Microsoft Excel o Google Sheets, lo que le permite utilizar un ecosistema dinámico y API sólidas de Google Sheets, Microsoft Excel y Microsoft Sharepoint para procesar fácilmente los datos enviados o iniciar un flujo de trabajo empresarial existente.


## Requisitos previos

Antes de comenzar, asegúrese de haber completado los siguientes pasos:

* Configure y clone su proyecto de servicio de entrega de Edge (EDS). Consulte [tutorial para desarrolladores](https://www.aem.live/developer/tutorial) para obtener más información. En este documento, la carpeta local del proyecto de servicio de entrega perimetral (EDS) se denomina `[EDS Project repository]` .
* Clonar el [Repositorio de bloques de Forms](https://github.com/adobe/afb). Contiene el código para procesar el formulario en una página web de EDS. En este documento, la carpeta local del repositorio de bloques de Forms se denomina `[Forms Block repository]` en este documento.
* Asegúrese de que tiene acceso a las hojas de Google o a Microsoft SharePoint.


## Creación de un formulario

+++ Paso 1: Añadir el bloque de formulario al proyecto de servicio de envío de Edge (EDS).

AEM Forms Edge Delivery incluye un bloque de formulario para ayudarle a crear fácilmente formularios para capturar y almacenar los datos capturados. Para incluir el bloque de formulario en el proyecto de servicio de entrega de Edge:

1. Vaya a `[Forms Block repository]/blocks` y copie el `forms` carpeta.

1. Vaya a `[EDS Project repository]/blocks/` y pegue el `forms` carpeta.

   >[!VIDEO](https://video.tv.adobe.com/v/3427487?quality=12&learn=on)

1. Marque en `form` y archivos subyacentes al proyecto del servicio de envío de Edge en GitHub.

   El bloque de formulario se agrega al repositorio del proyecto EDS en GitHub. Asegúrese de que la compilación de GitHub no falla:

   * Si aparece el error &quot;No se puede resolver la ruta al módulo &quot;&#39;../../scripts/lib-franklin.js&#39;&quot;, abra el `[EDS Project]/blocks/forms/form.js` archivo. En la instrucción import, reemplace `lib-franklin.js` archivo con la variable `aem.js` archivo.

   * Si encuentra algún error de linting, no dude en ignorarlo. Para omitir las comprobaciones de linting, abra el `[EDS Project]\package.json` y actualice el script &quot;lint&quot; desde `"lint": "npm run lint:js && npm run lint:css"` hasta `"lint": "echo 'skipping linting for now'"`. Guarde el archivo y configúrelo en su proyecto de GitHub.

Ahora puede crear un formulario y agregarlo al sitio.

+++

+++ Paso 2: Crear un formulario con Microsoft Excel o Google Sheet.

En lugar de procesos complejos, puede crear fácilmente un formulario con una hoja de cálculo. Para empezar, puede agregar las filas y los encabezados de columna a una hoja de cálculo, donde cada fila define un campo de formulario y cada encabezado de columna define las propiedades de los campos de formulario correspondientes.

Por ejemplo, en la siguiente hoja de cálculo, las filas definen los campos de un `contact us` el encabezado de formulario y columna define las propiedades de los campos correspondientes.

![hoja de cálculo](/help/edge/assets/contact-us-form-spreadsheet.png)

Para crear un formulario:

1. AEM Abra la carpeta del proyecto Entrega de Edge de la cuenta de la cuenta de usuario en Microsoft SharePoint o Google Drive.

1. Cree un libro o una hoja de Google AEM de Microsoft Excel en cualquier parte bajo el directorio del proyecto de entrega perimetral de. Por ejemplo, cree una hoja de cálculo llamada `contact-us` AEM en el directorio de proyectos de entrega de Edge en Google Drive.

1. AEM Asegúrese de que la hoja se comparte con el usuario (por ejemplo, si es un usuario de ). `helix@adobe.com`) [configurado para su proyecto](https://www.aem.live/docs/setup-customer-sharepoint) y el usuario tiene permisos de edición para la hoja.

1. Abra la hoja de cálculo que ha creado y cambie el nombre de la hoja predeterminada a &quot;shared-default&quot;.

   ![cambiar el nombre de la hoja predeterminada por &quot;shared-default&quot;](/help/edge/assets/rename-sheet-to-shared-default.png)

1. Para agregar los campos del formulario, agregue los encabezados de filas y columnas al `shared-default` hoja, donde cada fila define un campo de formulario y cada encabezado de columna define el [propiedades](/help/edge/docs/forms/eds-form-field-properties)) de los campos de formulario correspondientes.

   Para empezar rápidamente, puede copiar el contenido del [hoja de cálculo](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link) a la hoja de cálculo.

   >[!VIDEO](https://video.tv.adobe.com/v/3427468?quality=12&learn=on)

1. Uso [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para obtener una vista previa y publicar la hoja.

   ![Utilizar el AEM Sidekick para obtener una vista previa y publicar la hoja](/help/edge/assets/preview-form.png)

   Al obtener una vista previa y publicar, el explorador abre nuevas pestañas que muestran el contenido de la hoja en formato JSON. Asegúrese de tomar nota de la dirección URL activa, ya que es necesaria para procesar el formulario más adelante.

   El formato de la URL es el siguiente:

   ```JSON
   https://<branch>--<repository>--<owner>.hlx.live/<form>.json
   
   For example, https://main--portal--wkndforms.hlx.live/contact-us.json
   ```

+++

+++ Paso 3: Previsualizar el formulario mediante la página del servicio de entrega de Edge (EDS).


Hasta ahora, ha agregado el bloque de formulario al proyecto EDS y ha preparado la estructura del formulario. Ahora, para obtener una vista previa del formulario:

1. Vaya a la cuenta de Microsoft SharePoint o Google AEM Drive y abra el directorio del proyecto de entrega perimetral de la cuenta de.

1. Abra un archivo doc para incrustar el formulario en él. Por ejemplo, abra el archivo de índice. También puede crear un nuevo archivo doc.

1. Vaya a la ubicación deseada dentro del documento en el que desea agregar el formulario.

1. Agregue un bloque denominado &quot;Form&quot; al archivo, similar al que se muestra a continuación.

   ![](/help/edge/assets/form-block-in-sites-page-example.png)

   En la segunda fila, incluya la dirección URL registrada en la sección anterior como hipervínculo. Utilice la URL de vista previa (URL .page) con fines de desarrollo o prueba, o la URL de publicación (.live) para producción.

   >[!IMPORTANT]
   >
   >
   > Asegúrese de que la dirección URL tenga un hipervínculo en lugar de presentarse como texto sin formato.


1. Uso [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para previsualizar la página. La página ahora muestra el formulario.

   Por ejemplo, este es el formulario basado en [hoja de cálculo](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link):


   ![Formulario EDS de ejemplo](/help/edge/assets/eds-form.png)

   Ahora, rellene el formulario y haga clic en el botón Enviar . Se producirá un error similar al siguiente, ya que la hoja de cálculo aún no está configurada para aceptar los datos.

   ![error al enviar el formulario](/help/edge/assets/form-error.png)

+++


## Siguiente paso

[Preparar hoja de cálculo](/help/edge/docs/forms/submit-forms.md) para empezar a aceptar datos al enviar el formulario.



## Más información

* [Propiedades del campo de formulario](/help/edge/docs/forms/eds-form-field-properties)
* [Creación y previsualización de un formulario](/help/edge/docs/forms/create-forms.md)
* [Habilitar formulario para enviar datos](/help/edge/docs/forms/submit-forms.md)
* [Publicar un formulario en la página de Sites](/help/edge/docs/forms/publish-eds-forms.md)
* [Agregar validaciones a campos de formulario](/help/edge/docs/forms/validate-forms.md)
* [Cambiar temáticas y estilo de formulario](/help/edge/docs/forms/style-theme-forms.md)
