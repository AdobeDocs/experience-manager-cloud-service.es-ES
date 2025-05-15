---
title: 'Introducción a Edge Delivery Services para AEM Forms en el editor universal: Tutorial para desarrolladores'
description: Este tutorial le ayudará a ponerse en marcha con un nuevo proyecto de Adobe Experience Manager Forms (AEM). En diez a veinte minutos, habrá creado sus propios formularios de Edge Delivery Services en el editor universal.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 24a23d98-1819-4d6b-b823-3f1ccb66dbd8
source-git-commit: 95998daf04ae579ca11896953903852e6140c3a4
workflow-type: tm+mt
source-wordcount: '1853'
ht-degree: 91%

---


# Introducción a Edge Delivery Services para AEM Forms con el editor universal (WYSIWYG)

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| Creación basada en el editor universal | Este artículo |
| Creación basada en documentos | [Haga clic aquí](/help/edge/docs/forms/tutorial.md) |


<span class="preview"> Esta función está disponible a través del programa de acceso rápido. Para solicitar acceso, envíe un correo electrónico desde su dirección oficial a <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> con el nombre de la organización y el nombre del repositorio de GitHub. Por ejemplo, si la URL del repositorio es https://github.com/adobe/abc, el nombre de la organización es adobe y el nombre del repositorio es abc.</span>

En la era digital de hoy en día, unos formularios fáciles de usar son esenciales para todas las organizaciones. Edge Delivery Services Forms se crea mediante el editor universal, que ofrece funciones de WYSIWYG (lo que se ve es lo que se obtiene). Proporciona una interfaz moderna e intuitiva para la creación eficiente de formularios.

AEM Forms proporciona un bloque, conocido como bloque de formularios adaptables, para ayudarle a crear fácilmente formularios de Edge Delivery Services para capturar y almacenar los datos. Puede [crear un nuevo proyecto de AEM preconfigurado con el bloque de formularios adaptables](#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) o [añadir el bloque de formularios adaptables a un proyecto de AEM existente](#add-adaptive-forms-block-to-your-existing-aem-project).

![Flujo de trabajo de repositorio de Github](/help/edge/assets/repo-workflow.png){width=auto}

Este tutorial le guía a través de la creación, previsualización y publicación de su propio formulario con un proyecto de sitio de Adobe Experience Manager nuevo o existente mediante la creación de WYSIWYG en el editor universal.


## Requisitos previos

* Tiene una cuenta de GitHub y comprende los conceptos básicos de Git.
* Comprende los conceptos básicos de HTML, CSS y JavaScript.
* Ha instalado Node/npm para el desarrollo local.

## Creación de un nuevo proyecto de AEM preconfigurado con el bloque de Formularios adaptables

La plantilla repetitiva de AEM Forms le permite empezar rápidamente con un proyecto de AEM preconfigurado con el bloque de Formularios adaptables. Es la forma más rápida y sencilla de seguir las prácticas recomendadas de AEM y empezar a crear formularios de forma directa.

### Introducción a la plantilla de repositorio repetitiva de AEM Forms

1. Cree un repositorio de GitHub para su proyecto de AEM. Para crear un repositorio, haga lo siguiente:
   1. Vaya a [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms).

      ![Elemento repetitivo de AEM Forms](/help/edge/docs/forms/assets/eds-form-boilerplate.png)
   1. Haga clic en la opción **Usar esta plantilla** y seleccione la opción **Crear un nuevo repositorio**. 

      ![Crear un nuevo repositorio con el elemento repetitivo de AEM Forms](/help/edge/docs/forms/assets/use-eds-form-template.png)

      Se abrirá la pantalla **Crear un nuevo repositorio**.

   1. En la pantalla **Crear un nuevo repositorio**, seleccione el **propietario**, y especifique el **Nombre del repositorio** . Adobe recomienda establecer el repositorio en **Público**. Seleccione la opción **público** y haga clic en **Crear repositorio**.

      ![Configuración del repositorio como público](/help/edge/docs/forms/assets/name-eds-repo.png)

1. Instale la aplicación de GitHub de sincronización de código de AEM en su repositorio. Para instalar, haga lo siguiente:
   1. Vaya a [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new).
   1. En la pantalla **Instalar sincronización de código de AEM**, seleccione la opción **Seleccionar solo repositorios** y seleccione el repositorio recién creado. Haga clic en **Guardar**.

   ![Configuración del repositorio como público](/help/edge/docs/forms/assets/aem-code-sync-up.png)

1. Ahora, vincule el repositorio de GitHub que ha creado con el elemento repetitivo de AEM Forms a su entorno de creación de proyectos de AEM. Para conectarse, haga lo siguiente:

   1. Vaya al repositorio de GitHub que creó anteriormente con el elemento repetitivo de AEM Forms.
   1. Abra el archivo **fstab.yaml** para editarlo.

      ![abrir archivo fstab.yaml](/help/edge/docs/forms/assets/open-fstab.png)

   1. Edite el archivo **fstab.yaml** para actualizar el punto de montaje del proyecto. Reemplace la URL por la URL de la instancia de creación de AEM as a Cloud Service.

      `https://<aem-author>/bin/franklin.delivery/<owner>/<repository>/main`

      ![editar archivo fstab.yaml](/help/edge/docs/forms/assets/edit-fstab-file.png)

   1. Confirme el archivo actualizado **fstab.yaml**, una vez haya actualizado la referencia y todo se vea bien. 

      ![confirme los cambios](/help/edge/docs/forms/assets/commit-fstab-changes.png)

      Si tiene algún problema con la compilación, consulte [Solución de problemas de compilación de GitHub](#troubleshooting-github-build-issues).

### Crear un nuevo proyecto de AEM

Ahora que tiene un proyecto de GitHub, puede continuar con la creación y publicación de un nuevo proyecto de AEM en la instancia de creación de AEM as a Cloud Service.

1. Para crear un nuevo proyecto de AEM:

   1. Inicie sesión en la instancia de creación de AEM as a Cloud Service y seleccione **Sites**.

      ![seleccionar sitios](/help/edge/assets/select-sites.png)

   1. Haga clic en **Crear** > **Sitio a partir de una plantilla**.

      ![create-sites](/help/edge/docs/forms/assets/create-sites.png)

   1. Seleccione la plantilla de sitio de Edge Delivery Services y haga clic en **Siguiente**.

      ![select-site-template](/help/edge/docs/forms/assets/select-site-template.png)

      >[!NOTE]
      >
      > * Si la plantilla de sitio de Edge Delivery Services no está disponible en la instancia de creación, haga clic en el botón Importar para cargar la plantilla.
      > * Puede descargar las plantillas del sitio de Edge Delivery Services desde [GitHub](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases).

   1. Introduzca los siguientes datos para crear un nuevo proyecto de AEM:
      * **Título del sitio**: añada un título descriptivo para el sitio.
      * **Título del sitio**: Utilice el `site-name` que definió en el paso anterior.
      * **URL de GitHub**: utilice la URL del proyecto de GitHub que creó en el paso anterior.

      ![crear sitio de AEM](/help/edge/docs/forms/assets/create-aem-site.png)

   1. Aparecerá el cuadro de diálogo **Crear sitio**, haga clic en **Aceptar**.

      ![haga clic en aceptar](/help/edge/docs/forms/assets/click-ok-aem-site.png)

      En solo unos minutos, se crea su nuevo proyecto de AEM.

   1. Desplácese hasta el proyecto de AEM recién creado en la consola Sitios y haga clic en **Editar**.
En este caso, la página `index.html` se usa como ilustración.

      ![editar sitio de AEM](/help/edge/docs/forms/assets/edit-site.png)

      El proyecto de AEM se abre en el editor universal en una nueva pestaña, lo que permite la creación de WYSIWYG. Ahora puede editar su proyecto de AEM.

      ![El sitio se abre en el editor universal](/help/edge/docs/forms/assets/site-in-universal-editor.png)

1. Publicar el proyecto de AEM creado

   Una vez que termine de editar el proyecto de AEM, publíquelo. Para publicar:

   1. En la consola Sites, seleccione todas las páginas del proyecto de AEM y haga clic en **Publicación rápida**.

      ![publicar proyecto de AEM Sites](/help/edge/docs/forms/assets/publish-sites.png)

   1. Aparece el cuadro de diálogo de confirmación de **Publicación rápida**, haga clic en **Publicar** para iniciar el proceso de publicación.

      ![Confirmación de publicación rápida](/help/edge/docs/forms/assets/quick-publish.png)

      También puede publicar las páginas de su proyecto de AEM directamente desde la interfaz de usuario del Editor universal.

      ![Confirmación de publicación rápida](/help/edge/docs/forms/assets/qui.png)

   Enhorabuena. Tiene un nuevo sitio web en ejecución `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`.

   * `<branch>` hace referencia a la rama del repositorio de GitHub.
   * `<repository>` indica su repositorio de GitHub.
   * `<owner>` hace referencia al nombre de usuario de la cuenta de GitHub que aloja el repositorio de GitHub.
   * `<site-name>` hace referencia al nombre del sitio creado.

   Por ejemplo, si el nombre de la rama es `main`, el repositorio es `edsforms`, el propietario es `wkndforms` y el `site-name` es `eds-forms`, el sitio web estaría en funcionamiento a las `https://main--edsforms--wkndforms.aem.page/content/eds-forms/`

   >[!NOTE]
   >
   > * Para ver la página `index.html` del proyecto de AEM, use la dirección URL: `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`
   > * Para ver páginas que no sean la `index page` del proyecto de AEM, use la dirección URL: `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/<site-page-name>`

Ahora puede empezar a [crear y añadir formularios a su proyecto de AEM](#add-edge-delivery-services-forms-to-aem-project).

## Añadir un bloque de formularios adaptables a un proyecto de AEM existente

Si tiene un proyecto de AEM existente, puede integrar el bloque de formularios adaptables en su proyecto actual para empezar a crear formularios.

>[!NOTE]
>
>
> Este paso se aplica a los proyectos creados con [AEM Boilerplate XWalk](https://github.com/adobe-rnd/aem-boilerplate-xwalk). Si ha creado el proyecto de AEM mediante el [elemento repetitivo de AEM Forms](https://github.com/adobe-rnd/aem-boilerplate-forms), puede omitir este paso.

Para integrar, haga lo siguiente:

1. Vaya a la carpeta del repositorio de AEM Project del sistema local.

1. Copie y pegue las siguientes carpetas y archivos del [elemento repetitivo de AEM Forms](https://github.com/adobe-rnd/aem-boilerplate-forms) en su proyecto de AEM:

   * [bloque de formulario](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/blocks/form) carpeta
   * archivo [form-editor-support.js](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.js) 
   * archivo [form-editor-support.css](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.css)
1. Vaya al archivo `/scripts/editor-support.js` de su proyecto de AEM y actualícelo con el archivo [editor-support.js en la plantilla de AEM Forms](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/editor-support.js)
1. Vaya a `/models/_section.json` en su proyecto de AEM y anexe &quot;form&quot; y &quot;embed-adaptive-form&quot; a la matriz de componentes del objeto `filters`:

   ```
       "filters": [
       {
     "id": "section",
     "components": [
       .
       .
       .
       "form",
       "embed-adaptive-form"
     ]
    }]
   ```

1. (Opcional) Vaya a `/.eslintignore` en su proyecto de AEM y agregue las siguientes líneas de código:

   ```
   blocks/form/rules/formula/*
   blocks/form/rules/model/*
   blocks/form/rules/functions.js
   scripts/editor-support.js
   scripts/editor-support-rte.js
   ```

1. (Opcional) Vaya a `/.eslintrc.js` en su proyecto de AEM y agregue las siguientes líneas de código en el objeto `rules`:

   ```
   'xwalk/max-cells': ['error', {
     '*': 4, // default limit for all models
     form: 15,
     wizard: 12,
     'form-button': 7,
     'checkbox-group': 20,
     checkbox: 19,
     'date-input': 21,
     'drop-down': 19,
     email: 22,
     'file-input': 20,
     'form-fragment': 15,
     'form-image': 7,
     'multiline-input': 23,
     'number-input': 22,
     panel: 17,
     'radio-group': 20,
     'form-reset-button': 7,
     'form-submit-button': 7,
     'telephone-input': 20,
     'text-input': 23,
     accordion: 14,
     modal: 11,
     rating: 18,
     password: 20,
     tnc: 12,
   }],
   'xwalk/no-orphan-collapsible-fields': 'off', // Disable until enhancement is done for Forms properties
   ```

1. Abra el terminal y ejecute los siguientes comandos:

   ```
   npm i
   npm run build:json
   ```

   >[!NOTE]
   >
   > Antes de insertar los cambios en el repositorio del proyecto de AEM en GitHub, asegúrese de que los archivos de `component-definition.json`, `component-models.json` y `component-filters.json` ubicados en el nivel raíz del proyecto de AEM se actualicen con los objetos relacionados con el formulario.

1. Confirme e inserte estos cambios en el repositorio del Proyecto de AEM en GitHub.

   <!--
    1. **Update ESLint configuration file**
    2. Navigate to the `../.eslintignore` file in your AEM Project and add the following line of codes to prevent errors related to the Form Block rule engine:
        
            blocks/form/rules/formula/*
            blocks/form/rules/model/*
       * [form-common](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/models/form-common)  folder
       * [form-components](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/models/form-components) folder
    
     3. **Update component definitions and models files**
       1. Navigate to the `../models/_component-definition.json` file in your AEM Project and update it with the changes from the [_component-definition.json file in the AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/models/_component-definition.json#L39-L48).
    
    3. Navigate to the `../models/_component-models.json` file in your AEM Project and update it with the changes from the [_component-models.json file in the AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/models/_component-models.json#L24-L26) -->

Eso es todo. El Bloque de formularios adaptables ahora forma parte de su Proyecto de AEM. Puede [empezar a crear y añadir formularios a su proyecto de AEM](#add-edge-delivery-services-forms-to-aem-site-project).

## Crear formularios mediante WYSIWYG

Puede abrir el proyecto de AEM en el Editor universal para la creación de WYSIWYG, donde puede editar el proyecto y añadir la sección Formulario adaptable para incluir formularios de Edge Delivery Services en páginas del Proyecto de AEM.

1. Añada la sección Formulario adaptable a la página del Proyecto de AEM. Para añadir:
   1. Vaya al proyecto de AEM en la consola de Sites, seleccione la página del sitio que desee editar y haga clic en **Editar**. Se abrirá la página del proyecto de AEM en el Editor universal para editarlo.
En este caso, la página `index.html` se usa como ilustración.
   1. Abra el árbol de contenido y vaya hasta la sección en la que desea añadir la sección Formulario adaptable.
   1. Haga clic en el icono **[!UICONTROL Añadir]** y seleccione el componente **[!UICONTROL Formulario adaptable]** de la lista de componentes.

   ![árbol de contenido](/help/edge/docs/forms/assets/add-adaptive-form-block.png)

   Se añade la sección Formulario adaptable. Ahora puede empezar a añadir componentes a la página del Proyecto de AEM.

1. Añada componentes de formulario a la sección del formulario adaptable añadido. Para añadir componentes de formulario:
   1. Vaya a la sección del Formulario adaptable añadido en el árbol de contenido.

      ![bloque de formulario adaptable añadido](/help/edge/docs/forms/assets/adative-form-block.png)


   1. Haga clic en el icono de **[!UICONTROL Añadir]** y añada los componentes deseados de la lista **Componentes de formularios adaptables**.

      ![añadir componente](/help/edge/docs/forms/assets/add-component.png)

      También puede arrastrar y soltar los componentes de formularios adaptables necesarios, ya que el Editor universal ofrece una función intuitiva de arrastrar y soltar.

   1. Seleccione el componente de formulario adaptable añadido para actualizar sus propiedades mediante **[!UICONTROL Propiedades]**.

      ![abrir propiedades](/help/edge/docs/forms/assets/component-properties.png)

   1. Obtenga una vista previa del formulario. 
La siguiente captura de pantalla muestra el formulario creado en el Proyecto de AEM mediante la creación de WYSIWYG:

      ![se agregó el formulario](/help/edge/docs/forms/assets/added-form-aem-sites.png)

      Cuando esté satisfecho con la vista previa, el usuario podrá continuar publicando la página.

      >[!NOTE]
      >
      > Es importante volver a publicar la Página del proyecto de AEM después de realizar los cambios; de lo contrario, las actualizaciones no serán visibles en el explorador.

1. Vuelva a publicar la página del Proyecto de AEM.

   1. Haga clic en **Publicar** para publicar de nuevo la página del Proyecto de AEM después de añadir el formulario.

      ![publicar formulario](/help/edge/docs/forms/assets/publish-form.png)

   1. El cuadro de diálogo de confirmación **Publicar** aparece en pantalla. Haga clic en **Publicar** para iniciar la publicación.

      ![publicar formulario1](/help/edge/docs/forms/assets/publish-form1.png)

      Cuando haga clic en el botón **Publicar**, aparecerá el mensaje `Publish started successfully`.

      ![publicar formulario2](/help/edge/docs/forms/assets/publish-form2.png)

   Ahora puede ver la página Proyecto de AEM con el formulario de Edge Delivery Services añadido en la siguiente URL:
   `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`.

   Por ejemplo, si el nombre de la rama es `main`, el repositorio es `edsforms`, el propietario es `wkndforms` y el nombre del sitio es `eds-forms`, la dirección URL sería:
   `https://main--edsforms--wkndforms.aem.page/content/eds-forms/`

   ![página de índice](/help/edge/docs/forms/assets/publish-index-page.png)

Puede aplicar estilo a los formularios de Edge Delivery Services editando los archivos `.css` y `.js` en el bloque de formularios adaptables y [configurando un entorno de desarrollo de AEM local](#set-up-local-aem-development-environment) para ver los cambios al instante en su explorador.

>[!NOTE]
>
> También puede [crear un formulario independiente en el editor universal y publicarlo en Edge Delivery Services](/help/edge/docs/forms/universal-editor/create-forms.md).

## Configuración de un entorno de desarrollo de AEM local

Puede configurar un entorno de desarrollo de AEM local para desarrollar estilos y componentes personalizados localmente. Para ponerse en marcha con un entorno de desarrollo de AEM local en poco tiempo, haga lo siguiente:

1. **Instale la CLI de AEM**: esta simplifica las tareas de desarrollo. Vamos a instalarla globalmente con npm:

   ```Bash
       npm install -g @adobe/aem-cli
   ```

1. **Clone el proyecto de GitHub**: clone el repositorio del Proyecto de AEM desde GitHub mediante el siguiente comando, reemplazando &lt;owner> con el propietario del repositorio y &lt;repo> con el nombre del repositorio:

   ```
   git clone https://github.com/<owner>/<repo>
   ```

1. **Inicie el entorno local**: vaya al directorio del proyecto e inicie la instancia de AEM local con un solo comando.

   ```
   cd <repo>
   aem up
   ```

Puede realizar cambios locales en la carpeta `blocks/form` del Bloque de formularios adaptables para aplicar estilo y codificar a los formularios. Edite los archivos `.css` o `.js` dentro de este directorio; verá los cambios reflejados instantáneamente en su navegador.

Una vez completados los cambios, utilice los comandos de Git para confirmarlos e insertarlos. Esto actualiza los entornos de vista previa y producción accesibles en las siguientes direcciones URL (reemplace los marcadores de posición por los detalles del proyecto):

Vista previa: `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>`

Producción: `https://<branch>--<repo>--<owner>.aem.live/content/<site-name>`


## Solución de problemas de compilación de GitHub

Asegúrese de que el proceso de generación de GitHub sea fluido y aborde los posibles problemas:

* **Controlar errores de linting:**
Si encuentra algún error de linting, puede omitirlo. Abra el archivo [EDS Project]/package.json y modifique la secuencia de comandos “lint” desde `"lint": "npm run lint:js && npm run lint:css"` hasta `"lint": "echo 'skipping linting for now'"`. Guarde el archivo y confirme los cambios en su proyecto de GitHub.

* **Resolver error de ruta de módulo:**
Si aparece el error &quot;No se puede resolver la ruta de acceso al módulo &quot;&#39;/scripts/lib-franklin.js&#39;&quot;, vaya al archivo [Proyecto EDS]/blocks/forms/form.js. Actualice la instrucción de importación reemplazando el archivo lib-franklin.js por aem.js.

## Véase también

{{universal-editor-see-also}}
