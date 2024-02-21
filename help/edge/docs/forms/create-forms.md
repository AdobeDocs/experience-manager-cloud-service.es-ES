---
title: Introducción al servicio de entrega de AEM Forms Edge
description: ¡Crea formas perfectas, rápido! ⚡ la creación basada en documentos de AEM Forms Edge Delivery = una velocidad increíble y formularios compatibles con SEO para usuarios y motores de búsqueda más felices.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: f37a99cd5cbfb745cb591e3be2a46a5f52139cb2
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 1%

---


# Creación de un formulario en el servicio de entrega perimetral de AEM Forms

En la era digital de hoy en día, la creación de formularios fáciles de usar es esencial para cualquier organización. AEM Forms Edge Delivery le permite crear formularios con herramientas conocidas, como documentos de Word o Google.

Estos formularios envían datos directamente a un archivo de Microsoft Excel o Google Sheets, lo que le permite utilizar un ecosistema dinámico y API sólidas de Google Sheets, Microsoft Excel y Microsoft Sharepoint para procesar fácilmente los datos enviados o iniciar un flujo de trabajo empresarial existente.

## Requisitos previos

* Tiene una cuenta de Github.
* Tiene acceso a las hojas de Google o a Microsoft SharePoint.
* Comprenderá los conceptos básicos de Git, HTML, CSS y JavaScript.
* Tiene Node y NPM instalados para el desarrollo local.

## Antes de comenzar

* Configure y clone su proyecto de servicio de entrega de Edge (EDS). Consulte [tutorial para desarrolladores](https://www.aem.live/developer/tutorial) para obtener más información.
* Clonar el [Repositorio de bloques de Forms](https://github.com/adobe/afb). Incluye el bloque Formulario necesario para procesar el formulario.

![Introducción a Edge Delivery Forms](/help/edge/assets/getting-started-with-eds-forms.png)

## Añadir el bloque de formulario al proyecto de servicio de entrega de Edge (EDS) {#add-forms-block-to-an-eds-project}

AEM Forms Edge Delivery incluye un bloque de formulario para ayudarle a crear fácilmente formularios para capturar y almacenar los datos capturados. Para incluir el bloque de formulario en el proyecto de servicio de entrega de Edge:

1. Vaya a la carpeta del proyecto Edge Delivery Service (EDS) en su entorno de desarrollo local.


   ```Shell
   cd [EDS Project folder]
   ```

1. Cree una carpeta llamada `form` en el directorio del proyecto EDS. Por ejemplo, en el directorio del proyecto EDS denominado `Portal`, cree una carpeta llamada `form`.

   ```Shell
   mkdir form
   ```


1. Añada el [Bloque de Forms](https://github.com/adobe/afb/tree/main/blocks/form) archivos a la carpeta &quot;formulario&quot;.

   ```shell
   cp -R <source:path of the form block> <destination: path of the form folder created in the previous step>
   
   For example
   
   cp -R Documents/afb/blocks/form Documents/portal/blocks/
   ```

1. Compruebe la carpeta &quot;formulario&quot; y los archivos subyacentes en el proyecto de servicio de entrega de Edge en GitHub.

   ```Shell
   git add .
   git commit -m "Added form block"
   git push origin
   ```

   Ya está listo para procesar un formulario EDS.

   >[!NOTE]
   >
   > * Si la generación del proyecto de solicitud de extracción/finalizaciones falla y aparece un error relacionado con la importación de `franklin-lib.js` , actualice la instrucción import para hacer referencia al archivo `aem.js` en lugar del archivo `franklin-lib.js` archivo.
   > * Si encuentra algún error de linting, no dude en ignorarlo. Para omitir las comprobaciones de vinculación, vaya al archivo package.json y actualice la secuencia de comandos &quot;lint&quot; desde `"lint": "npm run lint:js && npm run lint:css"` hasta `"lint": "echo 'skipping linting for now'"`. A continuación, confirme los cambios en el archivo package.json.

## Crear un formulario con Microsoft Excel o Google Sheet {#create-a-form-for-an-eds-project}

Puede resultar útil permitir a los desarrolladores de sitios web crear formularios y elegir qué información recopilar de los visitantes del sitio web. En lugar de procesos complejos, los autores pueden configurar fácilmente un formulario con una hoja de cálculo. Deben agregar los encabezados de columna correctos y, a continuación, utilizar un bloque de formulario para mostrarlo en el sitio web sin ningún inconveniente. Para crear un formulario:

1. Cree un libro o una hoja de Google AEM de Microsoft Excel en cualquier lugar bajo el directorio del proyecto de entrega perimetral de en Microsoft SharePoint o Google Drive.

1. AEM Asegúrese de que el usuario de la (por ejemplo, `helix@adobe.com`) configurado para el proyecto tiene permisos de edición para la hoja.

1. Abra el libro que ha creado y cambie el nombre de la hoja predeterminada a &quot;shared-default&quot;.

   ![cambiar el nombre de la hoja predeterminada por &quot;shared-default&quot;](/help/edge/assets/rename-sheet-to-helix-default.png)

1. Copie el contenido del [hoja de cálculo](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link) a su propia hoja de cálculo.

   ![hoja de cálculo](/help/edge/assets/contact-us-form-spreadsheet.png)

1. Uso [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para obtener una vista previa y publicar la hoja.

   Al obtener una vista previa y publicar, el explorador abre nuevas pestañas que muestran el contenido de la hoja en formato JSON. Asegúrese de tomar nota de la dirección URL activa, ya que es necesaria para procesar el formulario más adelante.

   El formato de la URL es el siguiente:

   ```shell
   https://<branch>--<repository>--<owner>.hlx.live/<form>.json
   
   For example, https://main--portal--wkndforms.hlx.live/contact-us.json
   ```

## Vista previa del formulario mediante la página del servicio de entrega de Edge (EDS) {#add-a-form-to-your-eds-page}

Hasta ahora, ha habilitado el bloque de formulario para el proyecto EDS y ha preparado la estructura del formulario. Ahora, para incluir el formulario en la página EDS y procesarlo:

1. AEM Vaya al directorio del proyecto de entrega de Edge de la red de distribución de la red en Microsoft SharePoint o Google Drive.

1. Para agregar el formulario a una página, abra el archivo doc correspondiente. Por ejemplo, abra el archivo de índice.

1. Vaya a la ubicación deseada dentro del documento en el que desea agregar el formulario.

1. Agregue un bloque denominado &quot;Form&quot; al archivo, similar al que se muestra a continuación.

   ![](/help/edge/assets/form-block-in-sites-page-example.png)

   En la segunda fila, incluya la dirección URL anotada en la sección anterior como hipervínculo.

1. Uso [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para obtener una vista previa y publicar la página. Se procesará el formulario.

   Por ejemplo, este es el formulario basado en [hoja de cálculo](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link):


   ![Contáctenos (formulario EDS)](/help/edge/assets/eds-form.png)

   El bloque de formulario procesa el formulario, pero aún no está listo para aceptar los datos. Al hacer clic en el botón Enviar, se produce un error similar al siguiente:

   ![error al enviar el formulario](/help/edge/assets/form-error.png)

   [Preparar la hoja para aceptar datos](/help/edge/docs/forms/submit-forms.md). Puede enviar los datos a la hoja después de prepararlos para aceptar los datos.


## Más información

* [Creación y previsualización de un formulario](/help/edge/docs/forms/create-forms.md)
* [Habilitar formulario para enviar datos](/help/edge/docs/forms/submit-forms.md)
* [Publicar un formulario en la página de Sites](/help/edge/docs/forms/publish-eds-forms.md)
* [Agregar validaciones a campos de formulario](/help/edge/docs/forms/validate-forms.md)
* [Cambiar temáticas y estilo de formulario](/help/edge/docs/forms/style-theme-forms.md)