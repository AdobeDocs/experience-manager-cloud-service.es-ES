---
title: 'Introducción a los Edge Delivery Services de AEM Forms: Tutorial para desarrolladores '
description: Este tutorial le ayuda a ponerse en marcha con un nuevo proyecto de Adobe Experience Manager Forms AEM (). En diez a veinte minutos, habrá creado sus propios formularios.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: bae9a5178c025b3bafa8ac2da75a1203206c16e1
workflow-type: tm+mt
source-wordcount: '1850'
ht-degree: 0%

---


# Introducción: Tutorial para desarrolladores

En la era digital de hoy en día, la creación de formularios fáciles de usar es esencial para cualquier organización. Los Edge Delivery Services de AEM Forms (EDS) le permiten crear formularios utilizando herramientas conocidas como Google Docs y Microsoft Office.

Estos formularios envían datos directamente a un archivo de Microsoft Excel o Google Sheets, lo que le permite utilizar un ecosistema dinámico y API sólidas de Google Sheets, Microsoft Excel y Microsoft SharePoint para procesar fácilmente los datos enviados o iniciar un flujo de trabajo empresarial existente.

AEM Forms proporciona un bloque, conocido como bloque de Forms adaptable, para ayudarle a crear fácilmente formularios para capturar y almacenar los datos capturados. Puede [AEM crear un nuevo proyecto de preconfigurado con el bloque de Forms adaptable](#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) o [añadir el bloque de Forms AEM adaptable a un proyecto de existente](#add-adaptive-forms-block-to-your-existing-aem-project).

Este tutorial de AEM Forms le guía a través de la creación, la previsualización y la publicación de su propio formulario personalizado con un nuevo proyecto de Adobe Experience Manager AEM () Forms.



## Requisitos previos

* Tiene una cuenta de GitHub y comprende los conceptos básicos de Git.
* Tiene una cuenta de Google o Microsoft SharePoint.
* Comprenderá los conceptos básicos de HTML, CSS y JavaScript.
* Ha instalado Node/npm para el desarrollo local.

**¡Cuidado!** Este tutorial utiliza macOS, Chrome y Visual Studio Code. Aunque los pasos se pueden adaptar para otras configuraciones, las capturas de pantalla y los elementos específicos de la interfaz de usuario pueden diferir según el sistema operativo, el explorador y el editor de código que haya elegido.


## AEM Cree un nuevo proyecto de preconfigurado con el bloque de Forms adaptable

La plantilla de plantillas de AEM Forms AEM le permite empezar rápidamente con un proyecto de preconfigurado con el bloque de Forms adaptable. AEM Es la forma más rápida y sencilla de seguir las prácticas recomendadas de los usuarios y empezar a crear formularios de forma directa, y con mayor rapidez y facilidad.

### Introducción a la plantilla de repositorio de plantillas de AEM Forms

1. AEM Cree un repositorio de GitHub para su proyecto de. Para crear un repositorio:
   1. Ir a [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms).

      ![AEM Forms Boilerplate](/help/edge/assets/aem-forms-boilerplate.png)
   1. Haga clic en **Usar esta plantilla** y seleccione la opción **Creación de un nuevo repositorio** opción. Se abrirá la pantalla Crear un nuevo repositorio.

      ![Crear un nuevo repositorio con la plantilla de AEM Forms](/help/edge/assets/create-new-repository-using-aem-forms-boilerplate.png)

   1. En la pantalla Crear un nuevo repositorio, seleccione la **propietario** y especifique **Nombre del repositorio** . El Adobe recomienda que el repositorio se establezca en **Público**. Seleccione la opción **público** y haga clic en **Crear repositorio**.

   ![Configuración del repositorio como público](/help/edge/assets/create-a-new-repo-keep-it-public.png)


1. AEM Instale la aplicación de GitHub de sincronización de código de en su repositorio. Para instalar:
   1. Ir a [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new).
   1. AEM En la pantalla Instalar sincronización de código de, seleccione **Seleccionar solo repositorios** y seleccione el repositorio recién creado. Haga clic en Guardar.

   ![Configuración del repositorio como público](/help/edge/assets/install-aem-code-sync-app-for-your-repo.png)

   >[!NOTE]
   >
   >
   > Si utiliza GitHub Enterprise con filtrado de IP, puede agregar la siguiente IP a la lista de permitidos: 3.227.118.73

   Felicitaciones. Tiene un nuevo sitio web en ejecución `https://<branch>--<repo>--<owner>.hlx.page/`.

   * `<branch>` hace referencia a la rama del repositorio de GitHub.
   * `<repository>` indica su repositorio de GitHub.
   * `<owner>` hace referencia al nombre de usuario de la cuenta de GitHub que aloja el repositorio de GitHub.

   Por ejemplo, si el nombre de la rama es `main`, el repositorio es `wefinance`, y el propietario es `wkndforms`, el sitio web estaría en funcionamiento en [https://main--wefinance--wkndforms.hlx.page/](https://main--wefinance--wkndforms.hlx.page/).



### Vincular su propio origen de contenido

El repositorio de GitHub recién creado apunta a [contenido de ejemplo almacenado en una carpeta de Google Drive](https://drive.google.com/drive/folders/1bvjfi6TqpYA7DvbX6kKc-m7FgHuJ4RUQ). Este contenido de solo lectura proporciona un buen punto de partida para los formularios. No dude en copiarlo en su propia unidad de Google y personalizarlo para adaptarlo a sus necesidades.

![Contenido de muestra en Google Drive](/help/edge/assets/folder-with-sample-content.png)

Para copiar el contenido de muestra en su propia carpeta de contenido y dirigir el repositorio de GitHub a su propia carpeta de contenido:

1. AEM Cree una nueva carpeta específica para el contenido de su en Google Drive o Microsoft SharePoint. Este documento utiliza una carpeta creada en Microsoft SharePoint.

1. Comparta la carpeta con el usuario de Adobe Experience Manager (helix@adobe.com).

   ![AEM Utilice la opción Administrar acceso para compartir la carpeta con el usuario de: SharePoint](/help/edge/assets/share-folder-with-aem-user.png)

   ![AEM Utilice la opción Administrar acceso para compartir la carpeta con el usuario de la red - Google Drive (Usuario de)](/help/edge/assets/share-google-drive-folder.png)


   Asegúrese de haber proporcionado derechos de edición sobre la carpeta al usuario de Adobe Experience Manager.

   ![AEM Compartir carpeta con el usuario de la, proporcionar derechos de edición en SharePoint](/help/edge/assets/share-folder-with-aem-user-provide-editing-access.png)

   ![AEM Compartir la carpeta con el usuario de la carpeta, proporcionar derechos de edición: Google Drive](/help/edge/assets/add-aem-user-google-folder.png)

1. Copie el [contenido de ejemplo almacenado en la carpeta Google Drive](https://drive.google.com/drive/folders/17LSiMZC77N8tCJRW45TnHHGcG8V3SLG_) a su carpeta. Para copiar:

   1. Descargue los archivos juntos o descargue archivos individuales.

      ![Descargar contenido de muestra](/help/edge/assets/download-sample-content.png)

      El `nav` y `footer` Los archivos definen el diseño básico de las páginas y cambian con poca frecuencia a lo largo de un proyecto. También tienen una estructura específica diferente de la mayoría de los demás archivos de contenido. AEM Al examinar estos archivos, podrá hacerse una idea de cómo se organiza el contenido en los proyectos de los que se dispone en el sitio web, así como de cómo se organiza el contenido de los proyectos de los que se dispone en el sitio web.


   1. Cargue estos archivos en la carpeta Microsoft SharePoint o Google Drive.

      ![Contenido de muestra en Google Drive](/help/edge/assets/upload-sample-files-to-your-content-folder.png)

      Asegúrese de copiar el  `enquiry` del contenido de ejemplo a su carpeta en Google Drive o Microsoft SharePoint. Contiene la estructura de un formulario de ejemplo.

1. Ahora que tiene la carpeta de contenido configurada, es hora de vincularla al proyecto en GitHub que creó anteriormente con AEM Forms Boilerplate. Para conectarse:

   1. Vaya al repositorio de GitHub que creó anteriormente con las plantillas de AEM Forms.
   1. Abra `fstab.yaml` para editarlo.
   1. AEM Reemplace la referencia existente por la ruta de acceso a la carpeta que compartió con el usuario de la cuenta de usuario de la cuenta de usuario de la cuenta de usuario de la cuenta de usuario (helix@adobe.com).

      ![Contenido de muestra en Google Drive](/help/edge/assets/replace-path-in-fstab-yaml-with-your-content-folder.png)


      Si utiliza Microsoft SharePoint, la ruta de la carpeta utiliza el siguiente formato:

      ```HTML
      https://<tenant>.SharePoint.com/sites/  <sp-site>/Shared%20Documents/<folder-name>
      ```

      Por ejemplo,

      ```HTML
      https://adobe.SharePoint.com/sites/wkndforms/Shared%20Documents/wefinance
      ```

      Para obtener más información sobre la administración de archivos con en Microsoft SharePoint, consulte [Cómo usar Adobe SharePoint](https://www.aem.live/docs/setup-customer-SharePoint).



   1. Confirmar el actualizado `fsatb.yaml` , una vez que haya actualizado la referencia y todo se vea bien. Si tiene algún problema con la compilación, consulte [Solución de problemas de compilación de GitHub](#troubleshooting-github-build-issues).



      ![Confirme el archivo fsatab.yaml actualizado](/help/edge/assets/commit-updated-fstab-yaml.png)

      Esto conecta la carpeta de contenido con el sitio web. Después de actualizar la referencia, es posible que experimente inicialmente errores &quot;404 Not Found&quot;. Esto se debe a que el contenido aún no se ha previsualizado. En la siguiente sección se explica cómo empezar a crear y previsualizar el contenido.



### Previsualización y publicación del contenido

Después de completar el último paso, el nuevo origen de contenido no está vacío, pero no será visible en el sitio web hasta que se promocione a la vista previa o a las fases en directo. Actualmente, esto puede causar errores 404.

Para previsualizar contenido sin publicar:

1. Instale la extensión de Chrome llamada [AEM Sidekick](https://chrome.google.com/webstore/detail/helix-sidekick-beta/ccfggkjabjahcjoljmgmklhpaccedipo).

   ![AEM Sidekick de instalación](/help/edge/assets/install-aem-sidekick.png)

   Después de instalar la extensión en Chrome, no se olvide de fijarla, esto facilita su búsqueda.

   ![Fijar AEM Sidekick](/help/edge/assets/pin-aem-sidekick.png)

1. Para configurar la extensión de Sidekick Chrome, vaya a la carpeta previamente compartida de Google Drive o Microsoft SharePoint y, a continuación, haga clic con el botón derecho en el icono de extensión de la barra de herramientas del explorador y seleccione `Add this project`.

   ![AEM Sidekick - Añadir un proyecto](/help/edge/assets/aem-sidekick-add-a-project.png)

   Cuando se instale la extensión y se añada el proyecto, estará listo para obtener una vista previa y publicar el contenido de Google Drive.

1. Seleccione todos los documentos de la carpeta Microsoft SharePoint o Google Drive. Para seleccionar varios documentos, mantenga pulsada la tecla Ctrl (Windows/Linux) o Cmd (Mac) mientras hace clic en.

   ![Seleccionar todos los archivos](/help/edge/assets/select-all-files.png)

1. Haga clic en el AEM Sidekick de anclado a la barra de extensiones de Chrome. Aparecerá una barra de herramientas en la pantalla. Puede elegir previsualizar o publicar el contenido.

   Si ha copiado `index`, `nav`, `footer` y `enquiry` archivos, todos son documentos independientes con sus propios ciclos de vista previa y publicación, por lo que debe asegurarse de previsualizar (y publicar) todos ellos.

   Al obtener una vista previa de los archivos, las nuevas pestañas del explorador muestran los documentos. Para obtener una vista previa del formulario de ejemplo, vaya a la siguiente URL:


   ```HTML
   https://<branch>--<repository>--<owner>.hlx.live
   ```

   * `<branch>` hace referencia a la rama del repositorio de GitHub.
   * `<repository>` indica su repositorio de GitHub.
   * `<owner>` hace referencia al nombre de usuario de la cuenta de GitHub que aloja el repositorio de GitHub.


   `https://<branch>--<repo>--<owner>.hlx.page/enquiry` URL.

   Por ejemplo, si el repositorio de su proyecto se denomina &quot;wefinance&quot;, está ubicado en el propietario de la cuenta &quot;wkndforms&quot; y está utilizando la rama &quot;principal&quot;, la dirección URL es la siguiente:

   [https://main--wefinance--wkndforms.hlx.page](https://main--wefinance--wkndforms.hlx.page).

### Creación de un formulario

El contenido de ejemplo incluye una hoja de &quot;consulta&quot; que sirve como plantilla para el formulario de &quot;consulta&quot;. Cada fila de la hoja representa un [campo de formulario](/help/edge/docs/forms/form-components.md#available-components)y los encabezados de columna definen la variable [propiedades de campo](/help/edge/docs/forms/form-components.md#available-components). Este formulario de ejemplo le proporciona una ventaja inicial en la creación del formulario.

![Formulario de consulta](/help/edge/assets/enquiry-form-microsoft-sharepoint.png)

Empecemos por actualizar una etiqueta de campo. Abra la hoja &#39;consulta&#39; para editarla, cambie la etiqueta del botón de envío a `Let's Chat` y utilice el AEM Sidekick para obtener una vista previa y publicar el archivo.

![Formulario de consulta](/help/edge/assets/enquiry-form-preview-publish.png)

Al obtener una vista previa o publicar el archivo, aparece una versión JSON del archivo en una nueva pestaña. Copie la URL de vista previa (.hlx.page) o publicación (.hlx.live) del archivo.

![JSON de la hoja de cálculo del formulario](/help/edge/assets//preview-and-publish-enquiry-form.png)

Abra el `enquiry` y reemplace la URL en el bloque de formulario por la URL del archivo copiado en el paso anterior. Asegúrese de que la dirección URL sea un hipervínculo.

![Archivo de consulta con la dirección URL .json de la dirección URL de la hoja de cálculo](/help/edge/assets/enquiry-doc-to-embed-form.png)

Utilice AEM Sidekick para previsualizar y publicar el documento de consulta.

![Archivo de consulta con la dirección URL .json de la dirección URL de la hoja de cálculo](/help/edge/assets/preview-and-publish-enquiry-document.png)


Para obtener una vista previa del formulario de consulta actualizado, vaya a la siguiente URL:


```HTML
    https://<branch>--<repository>--<owner>.hlx.page/enquiry
       
```

La etiqueta del botón Enviar se actualiza a `Let's Chat`.

![Formulario de consulta](/help/edge/assets/updated-form.png)

Para obtener información detallada sobre la creación y publicación de un nuevo formulario, visite [creación de un formulario](/help/edge/docs/forms/create-forms.md) guía.

### Empiece a desarrollar el estilo y la funcionalidad


AEM Para ponerse en marcha con un entorno de desarrollo de la local en poco tiempo:

1. AEM AEM Instale la CLI de la: La CLI de la aplicación simplifica las tareas de desarrollo. Vamos a instalarlo globalmente con npm:

   ```Bash
       npm install -g @adobe/aem-cli
   ```

1. Clone su proyecto de GitHub: Clone su repositorio de proyecto desde GitHub mediante el siguiente comando, reemplazando <owner> con el propietario del repositorio y <repo> con el nombre del repositorio:

   ```
   git clone https://github.com/<owner>/<repo>
   ```

1. AEM Inicie su entorno local: vaya al directorio del proyecto y active la instancia de local con un solo comando:

   ```
   cd <repo>
   aem up
   ```

El bloque de Forms adaptable `blocks/form` La carpeta es el área de reproducción para el estilo y el código de los formularios. Editar cualquiera `.css` o `.js` Archivos dentro de este directorio, y verá los cambios reflejados instantáneamente en su navegador.

¿Listo para mostrar su creación? Utilice Git para confirmar e insertar los cambios. Esto actualiza los entornos de vista previa y producción accesibles en estas direcciones URL (reemplace los marcadores de posición por los detalles del proyecto):

Vista previa: `https://<branch>--<repo>--<owner>.hlx.page/`
Producción: `https://<branch>--<repo>--<owner>.hlx.live/`
¡Felicitaciones! Ha configurado correctamente su entorno de desarrollo local e implementado los cambios.



## Añadir un bloque de Forms AEM adaptable al proyecto de existente


>[!VIDEO](https://video.tv.adobe.com/v/3427789)

AEM Si tiene un proyecto de existente, puede integrar el bloque de Forms adaptable en su proyecto actual para empezar a crear formularios.

>
>
>
> Este paso se aplica a los proyectos creados con [AEM placa de boiler](https://github.com/adobe/aem-boilerplate). AEM Si ha creado el proyecto de con el [AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms), puede omitir este paso.

Para Integrar:

1. Clone el repositorio de bloque de Forms adaptable: [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms) a su equipo.

1. Dentro de la carpeta descargada, busque `blocks/form` carpeta. Copie esta carpeta. AEM A continuación, vaya a la configuración local del proyecto de la `blocks` y pegue la carpeta de formulario copiada aquí.

1. AEM Confirme e inserte estos cambios en su proyecto de en GitHub.


Eso es todo. El bloque de Forms AEM adaptable ahora forma parte de su proyecto de. AEM Puede empezar a crear y agregar formularios a las páginas de la.


## Solución de problemas de compilación de GitHub

Asegúrese de que el proceso de generación de GitHub sea fluido y aborde los posibles problemas:

* **Resolver error de ruta del módulo:**
Si aparece el error &quot;No se puede resolver la ruta al módulo &quot;&#39;../../scripts/lib-franklin.js&quot;&quot;, vaya al [Proyecto EDS]Archivo /blocks/forms/form.js. Actualice la instrucción import reemplazando el archivo lib-franklin.js por el archivo aem.js.

* **Controlar errores de vinculación:**
Si encuentra algún error de linting, puede evitarlo. Abra el [Proyecto EDS]/package.json y modifique la secuencia de comandos &quot;lint&quot; desde `"lint": "npm run lint:js && npm run lint:css"` hasta `"lint": "echo 'skipping linting for now'"`. Guarde el archivo y confirme los cambios en su proyecto de GitHub.


## Consulte también

{{see-more-forms-eds}}

