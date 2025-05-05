---
title: 'Introducción a Edge Delivery Services para AEM Forms: Tutorial para desarrolladores'
description: Este tutorial le ayudará a ponerse en marcha con un nuevo proyecto de Adobe Experience Manager Forms (AEM). En diez a veinte minutos, habrá creado sus propios formularios.
feature: Edge Delivery Services
exl-id: bb7e93ee-0575-44e1-9c5e-023284c19490
role: Admin, Architect, Developer
source-git-commit: e2259e542df5a12748705af901d073e4486292c4
workflow-type: tm+mt
source-wordcount: '1907'
ht-degree: 99%

---

# Introducción: Tutorial para desarrolladores

En la era digital de hoy en día, la creación de formularios fáciles de usar es esencial para cualquier organización. Edge Delivery Services para AEM Forms le permite crear formularios utilizando herramientas conocidas como Documentos de Google y Microsoft Office.

Estos formularios envían datos directamente a un archivo de Microsoft Excel o Google Sheets, lo que le permite utilizar un ecosistema dinámico y API sólidas de Google Sheets, Microsoft Excel y Microsoft SharePoint para procesar fácilmente los datos enviados o iniciar un flujo de trabajo empresarial existente.

AEM Forms proporciona un bloque, conocido como bloque de Formularios adaptables, para ayudarle a crear fácilmente formularios para capturar y almacenar los datos capturados. Puede [crear un nuevo proyecto de AEM previamente configurado con el bloque de formularios adaptables](#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) <!--or [add the Adaptive Forms Block to an existing AEM project](#add-adaptive-forms-block-to-your-existing-aem-project)-->.

Este tutorial de AEM Forms le guía a través de la creación, la previsualización y la publicación de su propio formulario personalizado con un nuevo proyecto de Adobe Experience Manager (AEM) Forms.

## Requisitos previos

* Tiene una cuenta de GitHub y comprende los conceptos básicos de Git.
* Tiene una cuenta de Google o Microsoft SharePoint.
* Comprende los conceptos básicos de HTML, CSS y JavaScript.
* Ha instalado Node/npm para el desarrollo local.

**Atención** Este tutorial utiliza macOS, Chrome y Visual Studio Code. Aunque los pasos se pueden adaptar para otras configuraciones, las capturas de pantalla y los elementos específicos de la IU pueden diferir según el sistema operativo, el explorador y el editor de código que haya elegido.


## Creación de un nuevo proyecto de AEM preconfigurado con el bloque de Formularios adaptables

La plantilla repetitiva de AEM Forms le permite empezar rápidamente con un proyecto de AEM preconfigurado con el bloque de Formularios adaptables. Es la forma más rápida y sencilla de seguir las prácticas recomendadas de AEM y empezar a crear formularios de forma directa.

### Introducción a la plantilla de repositorio repetitiva de AEM Forms

1. Cree un repositorio de GitHub para su proyecto de AEM. Para crear un repositorio, haga lo siguiente:
   1. Vaya a [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms).

      ![Elemento repetitivo de AEM Forms](/help/edge/assets/aem-forms-boilerplate.png)
   1. Haga clic en la opción **Usar esta plantilla** y seleccione la opción **Creación de un nuevo repositorio**. Se abrirá la pantalla Crear un nuevo repositorio.

      ![Crear un nuevo repositorio con el elemento repetitivo de AEM Forms](/help/edge/assets/create-new-repository-using-aem-forms-boilerplate.png)

   1. En la pantalla Crear un nuevo repositorio, seleccione el **propietario**, y especifique el **Nombre del repositorio**. Adobe recomienda que el repositorio se establezca en **Público**. Seleccione la opción **público** y haga clic en **Crear repositorio**.

   ![Configuración del repositorio como público](/help/edge/assets/create-a-new-repo-keep-it-public.png)


1. Instale la aplicación de GitHub de sincronización de código de AEM en su repositorio. Para instalar, haga lo siguiente:
   1. Vaya a [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new).
   1. En la pantalla Instalar sincronización de código de AEM, seleccione la opción **Seleccionar solo repositorios** y el repositorio recién creado. Haga clic en Guardar.

   ![Configuración del repositorio como público](/help/edge/assets/install-aem-code-sync-app-for-your-repo.png)

   >[!NOTE]
   >
   >
   > Si utiliza GitHub Enterprise con filtrado de IP, puede añadir la siguiente IP a la lista de permitidos: 3.227.118.73

   Enhorabuena. Tiene un nuevo sitio web en ejecución `https://<branch>--<repo>--<owner>.aem.page/`.

   * `<branch>` hace referencia a la rama del repositorio de GitHub.
   * `<repository>` indica su repositorio de GitHub.
   * `<owner>` hace referencia al nombre de usuario de la cuenta de GitHub que aloja el repositorio de GitHub.

   Por ejemplo, si el nombre de la rama es `main`, el repositorio es `wefinance` y el propietario es `wkndforms`, el sitio web estaría activo y en funcionamiento en `https://main--wefinance--wkndforms.aem.page`
&lt;!—(https://main--wefinance--wkndform.aem.page)-->

### Vincular su propio origen de contenido

<!--Your newly created GitHub repository points to [example content stored in a Google Drive folder](https://drive.google.com/drive/folders/1bvjfi6TqpYA7DvbX6kKc-m7FgHuJ4RUQ). This read-only content provides a great starting point for your forms. Feel free to copy it into your own Google Drive and customize it to fit your needs.

![Sample Content on Google Drive](/help/edge/assets/folder-with-sample-content.png)-->

Para copiar el contenido de muestra en su propia carpeta de contenido y dirigir el repositorio de GitHub a su propia carpeta de contenido, haga lo siguiente:

1. Cree una nueva carpeta específica para el contenido de AEM en Google Drive o Microsoft SharePoint. Este documento utiliza una carpeta creada en Microsoft SharePoint.

1. Comparta la carpeta con el usuario de Adobe Experience Manager (forms@adobe.com).

   ![Utilice la opción Administrar acceso para compartir la carpeta con el usuario de AEM: SharePoint](/help/edge/assets/share-folder-with-aem-user.png)

   ![Utilice la opción Administrar acceso para compartir la carpeta con el usuario de AEM: Google Drive](/help/edge/assets/share-google-drive-folder.png)


   Asegúrese de haber proporcionado derechos de edición sobre la carpeta al usuario de Adobe Experience Manager.

   ![Compartir carpeta con el usuario de AEM, proporcionar derechos de edición-SharePoint](/help/edge/assets/share-folder-with-aem-user-provide-editing-access.png){width=50%}

   ![Compartir la carpeta con el usuario de AEM, proporcionar derechos de edición- Google Drive](/help/edge/assets/add-aem-user-google-folder.png){width=50%}

1. Copie el [contenido de ejemplo](/help/edge/assets/wefinance1.zip) en su carpeta. Para copiar, haga lo siguiente:

   1. Descomprima la carpeta descargada y copie el contenido.

      ![Descargar contenido de muestra](/help/edge/assets/download-sample-content.png)

      Los archivos `nav` y `footer` definen el diseño básico de las páginas y cambian con poca frecuencia a lo largo de un proyecto. También tienen una estructura específica diferente de la mayoría de los demás archivos de contenido. Al examinar estos archivos, podrá hacerse una idea de cómo se organiza el contenido en los proyectos AEM.


   1. Cargue estos archivos en la carpeta Microsoft SharePoint o Google Drive.

      ![Contenido de muestra en Google Drive](/help/edge/assets/upload-sample-files-to-your-content-folder.png)

      Asegúrese de copiar la hoja `enquiry` del contenido de ejemplo a su carpeta en Google Drive o Microsoft SharePoint. Esta contiene la estructura de un formulario de ejemplo.

1. Ahora que tiene la carpeta de contenido configurada, es hora de vincularla al proyecto en GitHub que creó anteriormente con el elemento repetitivo de AEM Forms. Para conectarse, haga lo siguiente:

   1. Vaya al repositorio de GitHub que creó anteriormente con el elemento repetitivo de AEM Forms.
   1. Abra `fstab.yaml` para editarlo.
   1. Reemplace la referencia existente por la ruta de acceso a la carpeta que compartió con el usuario de AEM (forms@adobe.com).

      ![Contenido de muestra en Google Drive](/help/edge/assets/replace-path-in-fstab-yaml-with-your-content-folder.png)


      Si utiliza Microsoft SharePoint, la ruta de la carpeta utiliza el siguiente formato:

      ```HTML
      https://<tenant>.SharePoint.com/sites/<sp-site>/Shared%20Documents/<folder-name>
      ```

      Por ejemplo,

      ```HTML
      https://adobe.SharePoint.com/sites/wkndforms/Shared%20Documents/wefinance
      ```

      Para obtener más información sobre la administración de archivos en Microsoft SharePoint, consulte [Cómo utilizar Adobe SharePoint](https://www.aem.live/docs/setup-customer-sharepoint).


   1. Confirme el archivo actualizado `fsatb.yaml`, una vez que haya actualizado la referencia y todo se vea bien. Si tiene algún problema con la compilación, consulte [Solución de problemas de compilación de GitHub](#troubleshooting-github-build-issues).

      ![Confirme el archivo fsatab.yaml actualizado](/help/edge/assets/commit-updated-fstab-yaml.png)

      Esto conecta la carpeta de contenido con el sitio web. Después de actualizar la referencia, es posible que experimente inicialmente el error “404 Not Found”. Esto se debe a que el contenido aún no se ha previsualizado. En la siguiente sección se explica cómo empezar a crear y previsualizar el contenido.

### Previsualización y publicación del contenido

Después de completar el último paso, el nuevo origen de contenido no está vacío, pero no será visible en el sitio web hasta que se promocione a la vista previa o a las fases en directo. Actualmente, esto puede causar errores del tipo 404.

Para una vista previa del contenido sin publicar, haga lo siguiente:

1. Instale la extensión de Chrome llamada [AEM Sidekick](https://chrome.google.com/webstore/detail/helix-sidekick-beta/ccfggkjabjahcjoljmgmklhpaccedipo).

   ![Instalación de AEM SideKick](/help/edge/assets/install-aem-sidekick.png)

   Después de instalar la extensión en Chrome, no se olvide de fijarla, esto facilita su búsqueda.

   ![Fijar AEM Sidekick](/help/edge/assets/pin-aem-sidekick.png)

1. Para configurar la extensión Sidekick Chrome, vaya a la carpeta previamente compartida de Google Drive o Microsoft SharePoint y, a continuación, haga clic con el botón derecho en el icono de extensión de la barra de herramientas del explorador y seleccione `Add this project`.

   ![AEM Sidekick: Añadir un proyecto](/help/edge/assets/aem-sidekick-add-a-project.png)

   Cuando se instale la extensión y se añada el proyecto, estará listo para obtener una vista previa del contenido de Google Drive y publicarlo.

1. Seleccione todos los documentos de la carpeta Microsoft SharePoint o Google Drive. Para seleccionar varios documentos, mantenga pulsada la tecla Ctrl (Windows/Linux) o Cmd (Mac) mientras hace clic.

   ![Seleccionar todos los archivos](/help/edge/assets/select-all-files.png)

1. Haga clic en el icono AEM Sidekick anclado a la barra de extensiones de Chrome. Aparece una barra de herramientas en la pantalla. Puede elegir una vista previa del contenido o publicarlo.

   Si ha copiado los archivos `index`, `nav`, `footer` y `enquiry`, todos ellos son documentos independientes con sus propios ciclos de vista previa y publicación, por lo que debe asegurarse de previsualizar (y publicar) todos ellos.

   Al obtener una vista previa de los archivos, las nuevas pestañas del explorador muestran los documentos. Para obtener una vista previa del formulario de ejemplo, vaya a la siguiente URL:


   ```HTML
   https://<branch>--<repository>--<owner>.aem.live
   ```

   * `<branch>` hace referencia a la rama del repositorio de GitHub.
   * `<repository>` indica su repositorio de GitHub.
   * `<owner>` hace referencia al nombre de usuario de la cuenta de GitHub que aloja el repositorio de GitHub.


   URL `https://<branch>--<repo>--<owner>.aem.page/enquiry`.

   Por ejemplo, si el repositorio de su proyecto se llama &quot;wefinance”, está ubicado en el propietario de la cuenta “wkndform” y utiliza la rama “principal” y el nombre de formulario como `enquiry`, la dirección URL es la siguiente: `https://main--wefinance--wkndform.aem.live/enquiry`.
&lt;!—(https://main--wefinance--wkndform.aem.live/enquiry).-->

### Creación de un formulario

El contenido de ejemplo incluye una hoja de “consulta” que sirve como plantilla para el formulario de “consulta”. Cada fila de la hoja representa un [campo de formulario](/help/edge/docs/forms/form-components.md#available-components), y los encabezados de columna definen las [propiedades de campo](/help/edge/docs/forms/form-components.md#available-components). Este formulario de ejemplo le proporciona una ventaja inicial en la creación del formulario.

![Formulario de consulta](/help/edge/docs/forms/assets/enquiry-form-microsoft-sharepoint.png)

Empecemos por actualizar la etiqueta de campo. Abra la hoja “consulta” para editarla, cambie la etiqueta del botón de envío a `Let's Talk` y utilice AEM Sidekick para obtener una vista previa y publicar el archivo.

![Formulario de consulta](/help/edge/assets/enquiry-form-preview-publish.png)

Al obtener una vista previa o publicar el archivo, aparece una versión JSON del archivo en una nueva pestaña. Copie la URL de vista previa (.aem.page) o publicación (.aem.live) del archivo.

![JSON de la hoja de cálculo del formulario](/help/edge/assets/preview-and-publish-enquiry-form.png)

Abra el archivo `enquiry` y reemplace la URL en el bloque de formulario por la URL del archivo copiado en el paso anterior. Asegúrese de que la dirección URL sea un hipervínculo.

![Archivo de consulta con la dirección URL .json de la dirección URL de la hoja de cálculo](/help/edge/assets/enquiry-doc-to-embed-form.png)

Utilice AEM Sidekick para previsualizar y publicar el documento de consulta.

![Archivo de consulta con la dirección URL .json de la dirección URL de la hoja de cálculo](/help/edge/assets/preview-and-publish-enquiry-document.png)


Para obtener una vista previa del formulario de consulta actualizado, vaya a la siguiente URL:


```HTML
    https://<branch>--<repository>--<owner>.aem.page/enquiry
       
```

La etiqueta del botón Enviar se actualiza a `Let's Talk`.

![Formulario de consulta](/help/edge/assets/updated-form.png)

&lt;!—(https://main--wefinance--wkndform.aem.live/enquiry)-->

URL: `https://main--wefinance--wkndform.aem.live/enquiry`
&lt;!—(https://main--wefinance--wkndform.aem.live/enquiry)-->


Para obtener información detallada sobre la creación y publicación de un nuevo formulario, visite la guía [creación de un formulario](/help/edge/docs/forms/create-forms.md).

### Empiece a desarrollar el estilo y la funcionalidad


Para ponerse en marcha con un entorno de desarrollo de AEM local en poco tiempo, haga lo siguiente:

1. Instale la CLI de AEM: esta simplifica las tareas de desarrollo. Vamos a instalarla globalmente con npm:

   ```Bash
       npm install -g @adobe/aem-cli
   ```

1. Clone su proyecto de GitHub: clone su repositorio de proyecto desde GitHub mediante el siguiente comando, reemplazando &lt;owner> con el propietario del repositorio y &lt;repo> con el nombre del repositorio:

   ```
   git clone https://github.com/<owner>/<repo>
   ```

1. Inicie su entorno local: vaya al directorio del proyecto y active la instancia de AEM local con un solo comando.

   ```
   cd <repo>
   aem up
   ```

La carpeta Bloque de Formularios adaptables `blocks/form` es su patio de recreo para el estilo y el código de sus formularios. Edite cualquiera de los archivos `.css` o `.js` dentro de este directorio; verá los cambios reflejados instantáneamente en su navegador.

¿Está listo para mostrar su creación? Utilice Git para confirmar e insertar los cambios. Esto actualiza los entornos de vista previa y producción accesibles en estas direcciones URL (reemplace los marcadores de posición por los detalles del proyecto):

Vista previa: `https://<branch>--<repo>--<owner>.aem.page/`
Producción: `https://<branch>--<repo>--<owner>.aem.live/`

Enhorabuena. Ha configurado correctamente su entorno de desarrollo local e implementado los cambios.

## Añadir un bloque de formularios adaptables al proyecto de AEM existente

<!--
>[!VIDEO](https://video.tv.adobe.com/v/3427789)-->

Si tiene un proyecto de AEM existente, puede integrar el bloque de formularios adaptables en su proyecto actual para empezar a crear formularios.

>[!NOTE]
>
>
> Este paso se aplica a los proyectos creados con el [elemento repetitivo de AEM](https://github.com/adobe/aem-boilerplate). Si ha creado el proyecto de AEM con el [elemento repetitivo de AEM Forms](https://github.com/adobe-rnd/aem-boilerplate-forms), puede omitir este paso.

Para integrar, haga lo siguiente:

1. **Añada los archivos y las carpetas necesarios**
   1. Copie y pegue las siguientes carpetas y archivos del [elemento repetitivo de AEM Forms](https://github.com/adobe-rnd/aem-boilerplate-forms) en su proyecto de AEM:

      * carpeta [form block](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/blocks/form) 
      * carpeta [form-common](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/models/form-common)
      * carpeta [form-components](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/models/form-components)
      * archivo [form-editor-support.js](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.js) 
      * archivo [form-editor-support.css](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.css)

1. **Actualice las definiciones de componentes y archivos de modelos**
   1. Vaya al archivo `../models/_component-definition.json` de su proyecto de AEM y actualícelo con los cambios del [archivo _component-definition.json en el elemento repetitivo de AEM Forms](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/models/_component-definition.json#L39-L48).

   1. Vaya al archivo `../models/_component-models.json` de su proyecto de AEM y actualícelo con los cambios del [archivo _component-models.json en el elemento repetitivo de AEM Forms](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/models/_component-models.json#L24-L26)

1. **Añada el editor de formularios en el script del editor**
   1. Vaya al archivo `../scripts/editor-support.js` de su proyecto de AEM y actualícelo con los cambios del [archivo editor-support.js en el elemento repetitivo de AEM Forms](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/editor-support.js#L105-L106)
1. **Actualice el archivo de configuración ESLint**
   1. Vaya al archivo `../.eslintignore` de su proyecto de AEM y añada la línea de códigos siguiente para evitar errores relacionados con el motor de reglas del bloque de formularios:

      ```
          blocks/form/rules/formula/*
          blocks/form/rules/model/*
      ```

1. Confirme e inserte estos cambios en el repositorio del Proyecto de AEM en GitHub.

Eso es todo. El bloque de formularios adaptables ahora forma parte de su proyecto de AEM. Puede empezar a crear y agregar formularios a las páginas de AEM.

## Solución de problemas de compilación de GitHub

Asegúrese de que el proceso de generación de GitHub sea fluido y aborde los posibles problemas:

* **Resolver error de ruta del módulo:**
Si aparece el error &quot;No se puede resolver la ruta al módulo &quot;&#39;../../scripts/lib-franklin.js&quot;&quot;, vaya al archivo [Proyecto EDS]/blocks/forms/form.js. Actualice la instrucción de importación reemplazando el archivo lib-franklin.js por aem.js.

* **Controlar errores de linting:**
Si encuentra algún error de linting, puede omitirlo. Abra el archivo [EDS Project]/package.json y modifique la secuencia de comandos “lint” desde `"lint": "npm run lint:js && npm run lint:css"` hasta `"lint": "echo 'skipping linting for now'"`. Guarde el archivo y confirme los cambios en su proyecto de GitHub.


## Consulte también

{{see-more-forms-eds}}
