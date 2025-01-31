---
title: 'Introducción a Edge Delivery Services para AEM Forms en el editor universal: tutorial para desarrolladores'
description: Este tutorial le ayudará a ponerse en marcha con un nuevo proyecto de Adobe Experience Manager Forms (AEM). En diez a veinte minutos, habrá creado sus propios Edge Delivery Services Forms en el editor universal.
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: c27b8e413c060de601a72a669d86c4add2a4167d
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 23%

---


# Introducción a Edge Delivery Services para AEM Forms con el editor universal (WYSIWYG)

En la era digital actual, los formularios fáciles de usar son esenciales para todas las organizaciones. Edge Delivery Services Forms se crea mediante el editor universal, que ofrece funciones de WYSIWYG (lo que se ve es lo que se obtiene). Proporciona una interfaz moderna e intuitiva para la creación eficiente de formularios.

AEM Forms proporciona un bloque, conocido como bloque de Forms adaptable, para ayudarle a crear fácilmente Forms de Edge Delivery Services para capturar y almacenar datos. AEM Puede [crear un nuevo proyecto de preconfigurado con el bloque de Forms adaptable](#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) o [agregar el bloque de Forms AEM adaptable a un proyecto de existente](#add-adaptive-forms-block-to-your-existing-aem-project).

Este tutorial le guía a través de la creación, previsualización y publicación de su propio formulario con un proyecto de sitio de Adobe Experience Manager nuevo o existente mediante la creación de WYSIWYG en el Editor universal.


## Requisitos previos

* Tiene una cuenta de GitHub y comprende los conceptos básicos de Git.
* Tiene una cuenta de Google o Microsoft SharePoint.
* Comprende los conceptos básicos de HTML, CSS y JavaScript.
* Ha instalado Node/npm para el desarrollo local.

## Creación de un nuevo proyecto de AEM preconfigurado con el bloque de Formularios adaptables

La plantilla repetitiva de AEM Forms le permite empezar rápidamente con un proyecto de AEM preconfigurado con el bloque de Formularios adaptables. AEM Es la forma más rápida y sencilla de seguir las prácticas recomendadas de la aplicación y empezar a crear formularios de manera directa, y con mayor rapidez y facilidad.

### Introducción a la plantilla de repositorio repetitiva de AEM Forms

1. Cree un repositorio de GitHub para su proyecto de AEM. Para crear un repositorio, haga lo siguiente:
   1. Vaya a [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms).

      ![Elemento repetitivo de AEM Forms](/help/edge/docs/forms/assets/eds-form-boilerplate.png)
   1. Haga clic en la opción **Usar esta plantilla** y seleccione la opción **Crear un nuevo repositorio**.

      ![Crear un nuevo repositorio con el elemento repetitivo de AEM Forms](/help/edge/docs/forms/assets/use-eds-form-template.png)

      Se abre la pantalla **Crear un nuevo repositorio**.

   1. En la pantalla **Crear un nuevo repositorio**, seleccione el **propietario** y especifique el **nombre del repositorio** El Adobe recomienda establecer el repositorio en **Público**. Seleccione la opción **público** y haga clic en **Crear repositorio**.

      ![Configuración del repositorio como público](/help/edge/docs/forms/assets/name-eds-repo.png)

1. Instale la aplicación de GitHub de sincronización de código de AEM en su repositorio. Para instalar, haga lo siguiente:
   1. Vaya a [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new).
   1. AEM En la pantalla **Instalar sincronización de código de**, seleccione la opción **Seleccionar solo repositorios** y seleccione el repositorio recién creado. Haga clic en **Guardar**.

   ![Configuración del repositorio como público](/help/edge/docs/forms/assets/aem-code-sync-up.png)

1. Ahora, vincule el repositorio de GitHub que ha creado con las plantillas de AEM Forms AEM a su entorno de creación de proyectos de. Para conectarse, haga lo siguiente:

   1. Vaya al repositorio de GitHub que creó anteriormente con el elemento repetitivo de AEM Forms.
   1. Abra el archivo **fstab.yaml** para editarlo.

      ![abrir archivo fstab.yaml](/help/edge/docs/forms/assets/open-fstab.png)

   1. Edite el archivo **fstab.yaml** para actualizar el punto de montaje del proyecto. Reemplace la URL por la URL de la instancia de creación de AEM as a Cloud Service.
      `https://<aem-author>/bin/franklin.delivery/<owner>/<repository>/main`

      ![editar archivo fstab.yaml](/help/edge/docs/forms/assets/edit-fstab-file.png)

   1. Confirme el archivo **fstab.yaml** actualizado, una vez que haya actualizado la referencia y todo se vea bien.

      ![confirmar los cambios](/help/edge/docs/forms/assets/commit-fstab-changes.png)

      Si tiene algún problema con la compilación, consulte [Solución de problemas de compilación de GitHub](#troubleshooting-github-build-issues).

### AEM Creación de un nuevo proyecto de

AEM Ahora que tiene un proyecto de GitHub, puede continuar con la creación y publicación de un nuevo proyecto en la instancia de creación de AEM as a Cloud Service, que se encuentra en la fase de creación de un nuevo proyecto de GitHub.
1. AEM Para crear un nuevo proyecto de:

   1. Inicie sesión en la instancia de creación de AEM as a Cloud Service y seleccione **Sitios**.

      ![seleccionar sitios](/help/edge/assets/select-sites.png)

   1. Haga clic en **Crear** > **Sitio a partir de la plantilla**.

      ![create-sites](/help/edge/docs/forms/assets/create-sites.png)

   1. Seleccione la plantilla del sitio de Edge Delivery Services y haga clic en **Siguiente**.

      ![select-site-template](/help/edge/docs/forms/assets/select-site-template.png)

      >[!NOTE]
      >
      > * Si la plantilla del sitio de Edge Delivery Services no está disponible en la instancia de creación, haga clic en el botón Importar para cargar la plantilla.
      > * Puede descargar las plantillas del sitio de Edge Delivery Services desde [GitHub](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases).

   1. AEM Introduzca los siguientes detalles para crear un nuevo proyecto de:
      * **Título del sitio**: añada un título descriptivo para el sitio.
      * **Título del sitio** - Use el `site-name` que definió en el paso anterior.
      * **URL de GitHub**: utilice la dirección URL del proyecto de GitHub que creó en el paso anterior.

      AEM ![crear sitio de](/help/edge/docs/forms/assets/create-aem-site.png)

   1. Aparecerá el cuadro de diálogo **Crear sitio**, haga clic en **Aceptar**.

      ![haga clic en aceptar](/help/edge/docs/forms/assets/click-ok-aem-site.png)

      AEM En solo unos minutos, se crea su nuevo proyecto de.

   1. AEM Desplácese hasta el proyecto de código recién creado en la consola Sitios y haga clic en **Editar**.
En este caso, la página `index.html` se usa como ilustración.

      AEM ![editar sitio de](/help/edge/docs/forms/assets/edit-site.png)

      AEM El proyecto de se abre en el editor universal en una nueva pestaña, lo que permite la creación de WYSIWYG. AEM Ahora puede editar su proyecto de la.

      ![El sitio se abre en el editor universal](/help/edge/docs/forms/assets/site-in-universal-editor.png)

1. Publish AEM el proyecto de la creada

   AEM Una vez que termine de editar el proyecto de, publíquelo. Para publicar:

   1. AEM En la consola Sitios, seleccione todas las páginas del proyecto de la y haga clic en **Quick Publish**.

      ![publicar proyecto de AEM Sites](/help/edge/docs/forms/assets/publish-sites.png)

   1. Aparece el cuadro de diálogo de confirmación **Quick Publish**, haga clic en **Publish** para iniciar el proceso de publicación.

      ![Cuadro de diálogo de confirmación rápida de Publish](/help/edge/docs/forms/assets/quick-publish.png)

      AEM También puede publicar las páginas de su proyecto de directamente desde la interfaz de usuario del Editor universal.

      ![Cuadro de diálogo de confirmación rápida de Publish](/help/edge/docs/forms/assets/qui.png)

   Enhorabuena. Tiene un nuevo sitio web en ejecución `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`.

   * `<branch>` hace referencia a la rama del repositorio de GitHub.
   * `<repository>` indica su repositorio de GitHub.
   * `<owner>` hace referencia al nombre de usuario de la cuenta de GitHub que aloja el repositorio de GitHub.
   * `<site-name>` hace referencia al nombre del sitio creado.

   Por ejemplo, si el nombre de la rama es `main`, el repositorio es `edsforms`, el propietario es `wkndforms` y `site-name` es `eds-forms`, el sitio web estaría activo y en ejecución a las `https://main--edsforms--wkndforms.aem.page/content/eds-forms/`

   >[!NOTE]
   >
   > * AEM Para ver la página `index.html` del proyecto de, use la dirección URL: `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`
   > * AEM Para ver páginas que no sean la `index page` del proyecto de, use la dirección URL: `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/<site-page-name>`

AEM Ahora, puedes empezar a [crear y agregar formularios a tu proyecto de](#add-edge-delivery-services-forms-to-aem-project).

## Añadir un bloque de Forms AEM adaptable al proyecto de existente

Si tiene un proyecto de AEM existente, puede integrar el bloque de formularios adaptables en su proyecto actual para empezar a crear formularios.

>[!NOTE]
>
>
> Este paso se aplica a los proyectos creados con el [elemento repetitivo de AEM](https://github.com/adobe-rnd/aem-boilerplate-xwalk). Si ha creado el proyecto de AEM con el [elemento repetitivo de AEM Forms](https://github.com/adobe-rnd/aem-boilerplate-forms), puede omitir este paso.

Para integrar, haga lo siguiente:

1. Clone el repositorio adaptable de GitHub del bloque de Forms: [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms) en su equipo.
1. Dentro de la carpeta descargada, busque la carpeta `blocks/form` y copie esta carpeta.
1. AEM Clone su repositorio de GitHub de proyecto de en su equipo.
1. AEM A continuación, vaya a la carpeta `blocks` del repositorio local de proyecto de la aplicación de datos de la aplicación de datos y pegue allí la carpeta de formulario copiada.
1. AEM Confirme e inserte estos cambios en el repositorio de proyecto de la en GitHub.

Eso es todo. El bloque de Forms AEM adaptable ahora forma parte de su proyecto de. AEM Puede [empezar a crear y agregar formularios a su proyecto de](#add-edge-delivery-services-forms-to-aem-site-project).

## Crear AEM Forms con WYSIWYG

AEM Puede abrir el proyecto de en el Editor universal para la creación de WYSIWYG, donde puede editar el proyecto y agregar la sección Formulario adaptable para incluir formularios de Edge Delivery Services AEM en páginas de proyecto de la.

1. AEM Agregue la sección Formulario adaptable a la página de proyecto de. Para agregar:
   1. AEM Vaya a su proyecto de en la consola Sitios y haga clic en **Editar**. AEM Se abrirá la página Proyecto de en el Editor universal para editarlo.
En este caso, la página `index.html` se usa como ilustración.
   1. Abra el árbol de contenido y vaya a la ubicación en la que desea agregar la sección Formulario adaptable.
   1. Haga clic en el icono **[!UICONTROL Agregar]** y seleccione el componente **[!UICONTROL Formulario adaptable]** de la lista de componentes.

   ![árbol de contenido](/help/edge/docs/forms/assets/add-adaptive-form-block.png)

   La sección Formulario adaptable se agrega en la ubicación especificada. AEM Ahora puede empezar a agregar componentes de formulario a la página Proyecto de.

1. Agregue componentes de formulario a la sección del formulario adaptable agregada. Para agregar componentes de formulario:
   1. Vaya a la sección Formulario adaptable agregado en el árbol de contenido.

      ![bloque de formulario adaptable agregado](/help/edge/docs/forms/assets/adative-form-block.png)


   1. Haga clic en el icono de **[!UICONTROL Añadir]** y añada los componentes deseados de la lista **Componentes de formularios adaptables**.

      ![agregar componente](/help/edge/docs/forms/assets/add-component.png)

      También puede arrastrar y soltar los componentes adaptables de Forms necesarios, ya que el editor universal ofrece una función intuitiva de arrastrar y soltar.

   1. Seleccione el componente de formulario adaptable agregado para actualizar sus propiedades mediante **[!UICONTROL Propiedades]**.

      ![abrir propiedades](/help/edge/docs/forms/assets/component-properties.png)

      AEM La siguiente captura de pantalla muestra el formulario creado en el proyecto de mediante la creación de WYSIWYG:

      ![se agregó el formulario](/help/edge/docs/forms/assets/added-form-aem-sites.png)

   >[!NOTE]
   >
   > AEM Es importante volver a publicar la página de su proyecto de después de realizar los cambios; de lo contrario, las actualizaciones no serán visibles en el explorador.

1. AEM Vuelva a publicar la página de proyecto de la.

   1. Haga clic en **Publish AEM** para publicar de nuevo la página del proyecto de la después de agregar el formulario.

      ![publicar formulario](/help/edge/docs/forms/assets/publish-form.png)

   1. El cuadro de diálogo de confirmación **Publish** aparece en pantalla. Haga clic en **Publish** para iniciar la publicación.

      ![publicar formulario1](/help/edge/docs/forms/assets/publish-form1.png)

      Cuando haga clic en el botón **Publish**, aparecerá el mensaje `Publish started successfully`.

      ![publicar formulario2](/help/edge/docs/forms/assets/publish-form2.png)

   AEM Ahora puede ver la página Proyecto de con el Formulario de Edge Delivery Services agregado en la siguiente URL:
   `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`.

   Por ejemplo, si el nombre de la rama es `main`, el repositorio es `edsforms`, el propietario es `wkndforms` y el nombre del sitio es `eds-forms`, la dirección URL sería:
   `https://main--edsforms--wkndforms.aem.page/content/eds-forms/`

   ![página de índice](/help/edge/docs/forms/assets/publish-index-page.png)

Puede aplicar estilo al Forms de Edge Delivery Services editando los archivos de `.css` y `.js` en el bloque de Forms AEM adaptable y [configurando un entorno de desarrollo de local](#set-up-local-aem-development-environment) para ver los cambios al instante en su explorador.

## AEM Configuración del entorno de desarrollo de la local

AEM Puede configurar un entorno de desarrollo local de para desarrollar estilos y componentes personalizados localmente. AEM Para ponerse en marcha con un entorno de desarrollo de local:

1. AEM AEM **Instale la CLI de la**: La CLI de la simplifica las tareas de desarrollo. Vamos a instalarla globalmente con npm:

   ```Bash
       npm install -g @adobe/aem-cli
   ```

1. AEM **Clone su proyecto de GitHub**: Clone su repositorio de proyecto de GitHub desde GitHub mediante el siguiente comando, reemplazando <owner> con el propietario del repositorio y <repo> con el nombre del repositorio:

   ```
   git clone https://github.com/<owner>/<repo>
   ```

1. AEM **Inicie el entorno local**: Vaya al directorio del proyecto e inicie la instancia de la instancia local con un solo comando:

   ```
   cd <repo>
   aem up
   ```

Puede realizar cambios locales en la carpeta `blocks/form` del bloque de Forms adaptable para aplicar estilo y codificar a los formularios. Edite los archivos de `.css` o `.js` dentro de este directorio y verá que los cambios se reflejaron instantáneamente en el explorador.

Una vez completados los cambios, utilice los comandos de Git para confirmarlos e insertarlos. Esto actualiza los entornos de vista previa y producción, accesibles en las siguientes direcciones URL (reemplace los marcadores de posición por los detalles del proyecto):

Vista previa: `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>`
Producción: `https://<branch>--<repo>--<owner>.aem.live/content/<site-name>`


## Solución de problemas de compilación de GitHub

Asegúrese de que el proceso de generación de GitHub sea fluido y aborde los posibles problemas:

* **Controlar errores de linting:**
Si encuentra algún error de linting, puede omitirlo. Abra el archivo [EDS Project]/package.json y modifique la secuencia de comandos “lint” desde `"lint": "npm run lint:js && npm run lint:css"` hasta `"lint": "echo 'skipping linting for now'"`. Guarde el archivo y confirme los cambios en su proyecto de GitHub.

<!-- * **Resolve Module Path Error:**
    If you encounter the error "Unable to resolve path to module "'../../scripts/lib-franklin.js'", navigate to the [EDS Project]/blocks/forms/form.js file. Update the import statement by replacing the lib-franklin.js file with the aem.js file. -->
