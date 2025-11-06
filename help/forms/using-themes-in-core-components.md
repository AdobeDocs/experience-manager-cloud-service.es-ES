---
title: ¿Cómo se generan y utilizan las temáticas en el Forms adaptable?
description: Puede utilizar temáticas para aplicar estilo y proporcionar una identidad visual a un formulario adaptable mediante los componentes principales. Puede compartir una temática en cualquier número de formularios adaptables.
keywords: temáticas de form builder, componentes principales de estilo de formularios adaptables, generador de temáticas de formulario, estilo de formularios adaptables, personalizar temáticas, crear temáticas de formulario
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: 11c52b66-dbb1-4c47-a94d-322950cbdac1
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2806'
ht-degree: 99%

---

# Utilizar temáticas para aplicar estilo a los formularios adaptables basados en componentes principales{#themes-for-af-using-core-components}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/create-or-customize-themes-for-adaptive-forms-core-components.html?lang=es) |
| AEM as a Cloud Service | Este artículo |

Puede crear y aplicar temáticas para diseñar un formulario adaptable. Una temática contiene detalles de estilo para los componentes y paneles. Los estilos incluyen propiedades como colores de fondo, colores de estado, transparencia, alineación y tamaño. Al aplicar una temática, el estilo especificado se refleja en los componentes correspondientes. Una temática se administra de forma independiente sin hacer referencia a un formulario adaptable y se puede reutilizar en varios de estos.

En este artículo, entenderemos cómo diseñar aspectos personalizados para formularios adaptables basados en componentes principales mediante temáticas.

## Temáticas disponibles para aplicar estilo a los componentes principales

Forms como Cloud Service proporciona los siguientes temas para componentes principales basados en los formularios adaptables:

* [Temática Lienzo](https://github.com/adobe/aem-forms-theme-canvas)
* [Tema WKND](https://github.com/adobe/aem-forms-theme-wknd)
* [Temática Caballete](https://github.com/adobe/aem-forms-theme-easel)

## Comprender la estructura de las temáticas

Una temática es un paquete que incluye componentes de estilo como el archivo CSS, los archivos JavaScript y recursos (como iconos) que definen el estilo de los formularios adaptables. Una temática de formulario adaptable sigue una organización específica, que consta de los siguientes componentes:

* `src/theme.scss`: esta carpeta incluye el archivo CSS que tiene un impacto amplio en toda la temática. Sirve como una ubicación centralizada para definir y administrar el estilo y el comportamiento de la temática. Al realizar ediciones en este archivo, puede realizar cambios que se apliquen universalmente en toda la temática, lo que influye en el aspecto y la funcionalidad tanto de las páginas de AEM Sites como de formularios adaptables.

* `src/site`: esta carpeta contiene archivos CSS que se aplican a toda la página de un sitio de AEM. Estos archivos constan de código y estilos que afectan a la funcionalidad y al diseño general de la página del sitio de AEM. Cualquier modificación realizada aquí se reflejará en todas las páginas del sitio. [¿Cuándo se usa?]

* `src/components`: los archivos CSS de esta carpeta están diseñados para los componentes principales individuales de AEM. Cada carpeta dedicada para un componente incluye un archivo `.scss` que aplica estilo a ese componente en particular dentro de un formulario adaptable. Por ejemplo, el archivo /src/components/accordion/_accordion.scss contiene información de estilo para el componente Acordeón del formulario adaptable.

  ![estructura de la temática basada en formularios adaptables](/help/forms/assets/theme_structure.png)

* `src/resources`: esta carpeta contiene archivos estáticos como iconos, logotipos y fuentes. Estos recursos se utilizan para mejorar los elementos visuales y el diseño general del tema.

## Crear una temática

Forms as Cloud Service proporciona las siguientes temáticas de estilos de formularios adaptables para formularios adaptables basados en componentes principales.

* [Temática Lienzo](https://github.com/adobe/aem-forms-theme-canvas)
* [Tema WKND](https://github.com/adobe/aem-forms-theme-wknd)
* [Temática Caballete](https://github.com/adobe/aem-forms-theme-easel)

Puede [personalizar cualquiera de estas temáticas para crear una nueva](#customize-a-theme-core-components).

![Flujo de trabajo de personalización de temas](/help/forms/assets/workflow-of-customization-of-theme.png)

## Personalizar una temática {#customize-a-theme-core-components}

La personalización de una temática hace referencia al proceso de modificación, aplicación de estilo y personalización de la apariencia de una temática. Al personalizar una temática, cambia sus elementos de diseño, diseño, colores, tipografía y, a veces, el código subyacente. Permite crear un aspecto único y personalizado para el sitio web o la aplicación, al tiempo que mantiene la estructura y la funcionalidad básicas proporcionadas por la temática.

### Requisitos previos {#prerequisites-to-customize}

* Familiarícese con la [configuración de una canalización en Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=es#setup-pipeline) y cómo tener los conocimientos básicos para configurar una canalización ayuda a administrar e implementar de forma eficaz las personalizaciones de temas.
* Obtenga información sobre cómo [configurar un usuario con la función colaborador](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem.html?lang=es). Si sabe cómo configurar un usuario con la función de colaborador, puede conceder los permisos necesarios para personalizar temáticas.
* Instale la última versión de [Apache Maven](https://maven.apache.org/download.cgi). Apache Maven es una herramienta de automatización de compilaciones que se utiliza comúnmente en proyectos Java™. La instalación de la última versión garantiza que tenga las dependencias necesarias para la personalización de temáticas.
* Instale un editor de texto sin formato. Por ejemplo, Microsoft® Visual Studio Code. Utilizar un editor de texto sin formato como Microsoft® Visual Studio Code proporciona un entorno fácil de usar para editar y modificar archivos de temas.

### Configurar su entorno

* Instale la última versión para habilitar los componentes principales de formularios adaptables para su entorno de AEM as a Cloud Service.
* Configure una [canalización de implementación front-end](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/enable-frontend-pipeline-devops/create-frontend-pipeline.html?lang=es) para su entorno de Cloud Service. Como alternativa, puede configurar la canalización más adelante, lo que le ofrece la flexibilidad de priorizar la prueba y el refinamiento del tema antes de configurar la canalización de implementación.

<!-- 
To deploy your themes to a Forms as a Cloud Service environment, first test theme on a local development environment to address any issues. Once the theme is tested, configure the front-end deployment pipeline, which is responsible for deploying the themes.

These themes are deployed to a Forms as a Cloud Service environment via the front-end pipeline. You can configure the pipeline later also, after testing the theme on a local development environment. 

-->

Después de conocer los requisitos previos y configurar el entorno de desarrollo, estará bien preparado para empezar a personalizar el tema o aplicarle estilo según sus requisitos específicos.

### Personalizar una temática {#steps-to-customize-a-theme-core-components}

La personalización de una temática es un proceso de varios pasos. Para personalizar la temática, realice los pasos en el orden indicado:

1. [Clonar una temática](#download-a-theme-core-components)
1. [Establecer el nombre de la temática](#set-name-of-theme)
1. [Personalizar una temática](#customize-the-theme)
1. [Probar una temática](#test-the-theme)
1. [Implementar una temática](#deploy-the-theme)

Los ejemplos proporcionados en el documento se basan en la temática **Lienzo**, pero es importante tener en cuenta que puede clonar cualquier temática y personalizarla con las mismas instrucciones. Estas instrucciones se aplican a cualquier tema, lo que le permite modificarlas según sus necesidades específicas.

Empecemos con un proceso para crear una experiencia de marca para sus formularios adaptables basados en el componente principal mediante temáticas.

#### &#x200B;1. Clonar una temática {#download-a-theme-core-components}

Para clonar una temática para componentes principales basados en formularios adaptables, elija una de las siguientes temáticas:

* [Temática Lienzo](https://github.com/adobe/aem-forms-theme-canvas)
* [Tema WKND](https://github.com/adobe/aem-forms-theme-wknd)
* [Temática Caballete](https://github.com/adobe/aem-forms-theme-easel)

Para copiar una temática, realice los siguientes pasos:

1. Abra el símbolo del sistema o la ventana de terminal en su entorno de desarrollo local.

1. Ejecuta el comando `git clone` para clonar una temática.

   ```
      git clone [Path of Git Repository of the theme]
   ```

   Reemplace la [Ruta del repositorio Git de la temática] por la URL real del repositorio Git correspondiente de la temática

   Por ejemplo, para clonar la temática Lienzo, ejecute el siguiente comando:

   ```
      git clone https://github.com/adobe/aem-forms-theme-canvas
   ```

   Después de ejecutar el comando correctamente, tendrá una copia local de la temática disponible en la carpeta `aem-forms-theme-canvas` de su equipo. 


#### &#x200B;2. Establecer el nombre de una temática {#set-name-of-theme}

1. Abra la carpeta de temáticas en su IDE. Por ejemplo, para abrir la carpeta `aem-forms-theme-canvas` en el editor de código de Visual Studio.

1. Navegue hasta la carpeta `aem-forms-theme-canvas`.

1. Ejecute el siguiente comando:

   ```
      code .
   ```

   ![Abre la carpeta de temáticas en un editor de texto sin formato](/help/forms/assets/aem-forms-theme-folder-in-vs-code.png)

   La carpeta se abre en Visual Studio Code.

1. Abra el archivo `package.json` para editarlo.

1. Establezca los valores de los atributos `name` y `version`.

   ![Cambiar imagen de nombre del tema de lienzo](/help/forms/assets/changename_canvastheme.png)

   >[!NOTE]
   >
   > * El atributo de nombre se utiliza para identificar la temática de forma exclusiva y el nombre se muestra en la pestaña **Estilo** del **Asistente de creación de formularios**.
   > * Tiene la opción de seleccionar un nombre para el tema según su elección, por ejemplo, `mytheme` o `customtheme`. Sin embargo, para este caso, hemos especificado el nombre como `aem-forms-wknd-theme`.

1. Abra el archivo `package-lock.json` para editarlo.
1. Establezca los valores de los atributos `name` y `version`. Asegúrese de que los valores de los atributos `name` y `version` en el archivo `Package-lock`.json coinciden con los del archivo `Package.json`.

   ![Cambiar imagen de nombre del tema de lienzo](/help/forms/assets/changename_canvastheme-package-lock.png)

1. (Opcional) Abra el archivo `ReadMe` para editar y actualizar el nombre del tema.

   ![Cambiar imagen de nombre del tema de lienzo](/help/forms/assets/changename_canvastheme-readme-file.png)

1. Guarde y cierre los archivos.

**Consideraciones al establecer el nombre del tema**

* Es obligatorio quitar `@aemforms` del nombre de tema en el archivo `Package.json` y el archivo `Package-lock.json`. En caso de que no pueda quitar `@aemforms` del nombre del tema personalizado, se producirá un error en la canalización de front-end durante la implementación del tema.
* Se recomienda actualizar el tema `version` en el archivo `Package.json` y el archivo `Package-lock.json` para reflejar con precisión los cambios y mejoras realizados con el tiempo en el tema.
* Para obtener la información importante sobre el uso, las instrucciones de instalación y otros detalles relevantes, se recomienda actualizar el nombre del tema en el archivo `ReadMe`.

#### &#x200B;3. Personalizar una temática {#customize-the-theme}

Puede personalizar componentes individuales o realizar cambios en el nivel de temática mediante variables globales de una temática. Cualquier cambio realizado en las variables globales afecta a todos los componentes individuales. Por ejemplo, puede utilizar variables globales para cambiar el color del borde de todos los componentes de un formulario adaptable y un color de relleno brillante para establecer CTA (llamada a la acción) mediante el componente de botón:

* [Establecer estilos de nivel de temática](#theme-customization-global-level)

* [Definir estilos de nivel de componente](#component-based-customization)

##### Establecer estilos de nivel de temática{#theme-customization-global-level}

El archivo `variable.scss` contiene las variables globales de la temática. Al actualizar estas variables, puede realizar cambios relacionados con los estilos en el nivel de la temática. Para aplicar estilos de nivel de tema, siga estos pasos:

1. Abra el archivo `<your-theme-sources>/src/site/_variables.scss` para editarlo.
1. Cambia el valor de cualquier propiedad. Por ejemplo, el color de error predeterminado es `red`. Para cambiar el color del error de `red` hasta `blue`, cambia el código hexadecimal de color del `$errorvariable`. Por ejemplo, `$error: #196ee5`.
1. Guarde y cierre el archivo.

   ![Editar tema](/help/forms/assets/edit_theme.png)

Del mismo modo, puede utilizar el archivo `variable.scss` para establecer la familia y el tipo de fuente, los colores de la temática y la fuente, el tamaño de fuente, el espaciado del tema, el icono de error, los estilos de borde del tema y más variables que afectan a varios componentes del formulario adaptable.

##### Definir estilos de nivel de componente {#component-based-customization}

También puede cambiar la fuente, el color, el tamaño y otras propiedades CSS de un componente principal de un formulario adaptable específico. Por ejemplo, botón, casilla de verificación, contenedor, pie de página, etc. Puede aplicar estilo a un botón o una casilla de verificación editando el archivo CSS del componente específico para alinearlo con el estilo de su organización. Para personalizar el estilo de un componente, haga lo siguiente:

1. Abra el archivo `<your-theme-sources>/src/components/<component>/<component.scss>` para editarlo. Por ejemplo, para cambiar el color de fuente del componente de botón, abra el archivo `<your-theme-sources>/src/components/button/button.scss`.
1. Cambie el valor de cualquiera según sus necesidades. Por ejemplo, para cambiar el color del componente Botón al pasar el ratón por encima de `green`, cambia el valor de la propiedad `color: $white` en la clase `cmp-adaptiveform-button__widget:hover` a código hexadecimal `#12B453` o cualquier otro tono de `green`. El código final tiene el siguiente aspecto:

   ```
   .cmp-adaptiveform-button__widget:hover {
   background: $dark-gray;
   color: #12B453;
   }
   ```

1. Guarde y cierre el archivo.

   ![Editar CSS del cuadro de texto](/help/forms/assets/edit_color_textbox.png)

   >[!NOTE]
   >
   > Cuando se define un estilo tanto a nivel de temática como de componente, el estilo definido en el nivel de componente tiene prioridad.

#### &#x200B;4. Probar una temática personalizada {#test-the-theme}

Para obtener una vista previa y probar los cambios en el entorno local y personalizar la temática según los requisitos de diferentes componentes de la AEM, realice los siguientes pasos:

* 4.1 [Configurar un entorno local para realizar pruebas](#rename-env-file-theme-folder)
* 4.2 [Probar la temática mediante el entorno local](#start-a-local-proxy-server)

##### 4.1. Configurar un entorno local para realizar pruebas {#rename-env-file-theme-folder}

1. Abra la carpeta de temáticas en su IDE. Por ejemplo, abra la carpeta `aem-forms-theme-canvas` en el editor de código de Visual Studio.
1. Cambie el nombre del archivo `env_template` a `.env` en la carpeta tema y agregue los siguientes parámetros:

   ```
   * **AEM url**
   AEM_URL=https://[author-instance] 
   
   * **AEM Adaptive form name**
   AEM_ADAPTIVE_FORM=Form_name
   
   * **AEM proxy port**
   AEM_PROXY_PORT=7000
   ```

   Por ejemplo, la dirección URL del formulario es `http://localhost:4502/editor.html/content/forms/af/contactusform.html`. Por lo tanto, los siguientes valores:

   * AEM URL_de_la_= `http://localhost:4502/`
   * AEM_ADAPTIVE_FORM = `contactusform`

1. Guarde el archivo.

   ![Estructura de la temática Lienzo](/help/forms/assets/env-file-canvas-theme.png)

##### 4.2 Probar la temática mediante un entorno local {#start-a-local-proxy-server}

1. Vaya hasta la raíz de la carpeta de temáticas. En este caso, el nombre de la carpeta de temáticas es `aem-forms-theme-canvas`.
1. Abra el símbolo de comando o el terminal.
1. Ejecute `npm install` para instalar las dependencias.
1. Ejecute `npm run live` para obtener una vista previa del formulario con la temática actualizada en el explorador local.

   >[!NOTE]
   >
   > Si se produce un error durante la ejecución del comando `npm run live`, ejecute los siguientes comandos antes del comando `npm run live`:
   >
   > * `npm install parcel --save-dev`
   > * `npm i @parcel/transformer-sass`

Esta es una implementación activa. Por lo tanto, cada vez que realice cambios y guarde los archivos `_variables.scss` y `button.scss`, el servidor selecciona automáticamente los cambios y se obtiene una vista previa del resultado más reciente. La línea `[Browsersync] File event [change]` significa que el servidor ha reconocido los cambios más recientes y está implementando los cambios en el entorno local.

![Sincronización de exploradores proxy](/help/forms/assets/browser_sync.png)

Después de haber seguido los ejemplos de aplicación de estilo a un formulario adaptable (componentes principales) tanto a nivel de temática como de componente para las personalizaciones de temas, los mensajes de error de un formulario adaptable se cambian al color `blue`, mientras que el color de la etiqueta del componente de botón cambia a `green` al pasar el ratón por encima.

**Vista previa del estilo de nivel de tema**

![Ejemplo: color de error establecido en azul](/help/forms/assets/theme-level-changes.png)

**Vista previa del estilo de nivel de componente**

![Ejemplo: color de desplazamiento establecido en verde](/help/forms/assets/button-customization.png)

La personalización de una temática ayuda a diseñar los aspectos personalizados de formularios adaptables basados en el componente principal según los requisitos de la organización.

###### Probar la temática para formularios alojados en un entorno de Cloud Service

También puede probar la temática del formulario adaptable alojado en la instancia de AEM Forms as a Cloud Service. Para configurar y establecer el entorno local para probar las temáticas con el formulario adaptable alojado en la instancia de nube, realice los siguientes pasos:

1. Abra la carpeta de temáticas en su IDE. Por ejemplo, abra la carpeta `aem-forms-theme-canvas` en el editor de código de Visual Studio.
1. Cambie el nombre del `env_template` archivo a `.env` y agregue los siguientes parámetros:

   ```
   * **AEM url**
   AEM_URL=https://[author-instance] 
   
   * **AEM Adaptive form name**
   AEM_ADAPTIVE_FORM=Form_name
   
   * **AEM proxy port**
   AEM_PROXY_PORT=7000
   ```

   Por ejemplo, la URL del formulario en el entorno de la nube es `https://author-XXXX.adobeaemcloud.com/editor.html/content/forms/af/contactusform.html`. Por lo tanto, los siguientes valores:

   * AEM URL_de_la_= `https://author-XXXX-cmstg.adobeaemcloud.com/`
   * AEM_ADAPTIVE_FORM = `contactusform`
1. Guarde el archivo.
1. Cree un usuario local.

   >[!NOTE]
   >
   > Para crear un usuario local, haga lo siguiente:
   >
   > * Vaya a la **[!UICONTROL Página de inicio de AEM]** > **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Usuarios]**.
   > * Asegúrese de que el usuario sea miembro del grupo `forms-users`.

1. Vaya hasta la raíz de la carpeta de temáticas. En este caso, el nombre de la carpeta de temas es `aem-forms-theme-canvas`.
1. Ejecute `npm run live` y se le redirigirá a un explorador local.
1. Haga clic en `SIGN IN LOCALLY (ADMIN TASKS ONLY)` e inicie sesión con las credenciales del usuario local.

Puede obtener una vista previa del formulario adaptable con los cambios más recientes. Una vez que esté satisfecho con las modificaciones realizadas en una carpeta de temas, implemente el tema en el entorno de AEM Cloud Service mediante la canalización front-end.

#### &#x200B;5. Implementar una temática {#deploy-the-theme}

Para implementar la temática en el entorno de Cloud Service mediante la canalización front-end, haga lo siguiente:

* 5.1 [Crear un repositorio para la temática](#create-a-new-theme-repo)
* 5.2 [Insertar los cambios en el repositorio](#committing-the-changes)
* 5.3. [Ejecutar la canalización de front-end](#run-a-frontend-pipeline)

##### 5.1 Crear un repositorio para la temática{#create-a-new-theme-repo}

Se necesita un repositorio para implementar la temática. Inicie sesión en el [Repositorio de Cloud Manager de AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=es#accessing-git) y añada un nuevo repositorio para la temática.

1. Cree un nuevo repositorio para una temática haciendo clic en **[!UICONTROL Repositorios]** > **[!UICONTROL Añadir repositorio]**.

   ![crear nuevo repositorio de temáticas](/help/forms/assets/createrepo_canvastheme.png)


1. Especifique el **Nombre del repositorio** en el cuadro de diálogo **Añadir repositorio**. Por ejemplo, el nombre proporcionado es `custom-canvas-theme-repo`.
1. Haga clic en **[!UICONTROL Guardar]**.

   ![Adición de repositorios de temática Lienzo](/help/forms/assets/addcanvasthemerepo.png)

1. Haga clic en **[!UICONTROL Copiar URL del repositorio]** para copiar la URL del repositorio.

   ![URL de temática Lienzo](/help/forms/assets/copyurl_canvastheme.png)

   >[!NOTE]
   > 
   >* Puede utilizar un único repositorio para varias temáticas.
   >* Para implementar diferentes temáticas, debe crear canalizaciones front-end independientes.
   >* Por ejemplo, puede utilizar el mismo repositorio que `custom-canvas-theme-repo` para la temática Lienzo, la temática WKND y la temática Cabellete. Sin embargo, para implementar los temas, debe crear canalizaciones front-end independientes. Las futuras personalizaciones de un tema específico se implementan mediante la canalización front-end correspondiente.

##### 5.2. Insertar los cambios en el repositorio {#committing-the-changes}

Ahora, inserte los cambios en el repositorio de temáticas de AEM Forms Cloud Service.

1. Vaya hasta la raíz de la carpeta de temáticas.  En este caso, el nombre de la carpeta de temas es `aem-forms-theme-canvas`.
1. Abra el símbolo de comando o el terminal.
1. Ejecute el siguiente comando en el orden indicado:

   ```
   git remote add [alias-name-for-repository] [URL of repository]
   git add .
   git commit
   git push [name-for-createdrepository]
   ```

   Por ejemplo:

   ```
   git remote add canvascloudthemerepo https://git.cloudmanager.adobe.com/stage-aemformsdev/customcanvastheme/
   git add .
   git commit
   git push canvascloudthemerepo 
   ```

   ![Cambios confirmados](/help/forms/assets/cmd_git_push.png)



##### 5.3. Ejecutar la canalización de front-end {#run-a-frontend-pipeline}

La temática se implementa mediante la [canalización front-end](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/enable-frontend-pipeline-devops/create-frontend-pipeline.html?lang=es).  Para implementar una temática, siga estos pasos:

1. Inicie sesión en el repositorio de AEM Cloud Manager.
1. Haga clic en el botón **[!UICONTROL Añadir]** en la sección **[!UICONTROL Canalizaciones]**.
1. Seleccione **[!UICONTROL Agregar canalización que no sea de producción]** o **[!UICONTROL Agregar canalización de producción]** en función del entorno de Cloud Service. Por ejemplo, aquí la opción **[!UICONTROL Agregar canalización de producción]** está seleccionada.
1. En el cuadro de diálogo **[!UICONTROL Añadir canalización de producción]** como parte de los pasos de **[!UICONTROL Configuración]**, indique el nombre de la canalización. Por ejemplo, el nombre de la canalización es `customcanvastheme`.
1. Haga clic en **[!UICONTROL Continuar]**.
1. Seleccione **[!UICONTROL Implementación objetivo]** > las opciones **[!UICONTROL Código front-end]**, 
en los pasos **[!UICONTROL Código fuente]**.
1. Seleccione el **[!UICONTROL Repositorio]** y los valores **[!UICONTROL Rama Git]** que tienen sus cambios más recientes. Por ejemplo, aquí el nombre de repositorio seleccionado es `custom-canvas-theme-repo` y la rama Git es `main`.
1. Seleccione la **[!UICONTROL Ubicación del código]** como `/`, si los cambios están presentes en la carpeta raíz.
1. Haga clic en **[!UICONTROL Guardar]**.
   ![crear canalización front-end](/help/forms/assets/canvas-theme-frontendpipeline.gif)

   Una vez completada la configuración de la canalización, se actualiza la tarjeta de llamada a la acción.

1. Haga clic con el botón derecho en la canalización creada.
1. Haga clic **[!UICONTROL Ejecutar]**.

   ![run-a-pipeline](/help/forms/assets/canvas-theme-run-pipeline.png)

Una vez finalizada la compilación, la temática está disponible en la instancia de autor para el uso. Aparece bajo la pestaña **[!UICONTROL Estilo]** en el asistente de creación de formularios adaptables, mientras se crea un formulario adaptable.

![temática personalizada disponible en la pestaña estilo](/help/forms/assets/custom-theme-style-tab.png)

La temática personalizada ayuda a crear una experiencia de marca para los formularios adaptables basados en el componente principal

## Aplicar una temática a un formulario adaptable {#using-theme-in-adaptive-form}

Los pasos para aplicar una temática a un formulario adaptable son los siguientes:

1. Inicie sesión en la instancia de autor de AEM Forms.

1. Seleccione **Adobe Experience Manager** > **Formularios** > **Formularios y documentos**.

1. Haga clic en **Crear** > **Formularios adaptables**. Se abre el asistente para crear formularios adaptables.

1. Seleccione la plantilla del componente principal en la pestaña **Fuente**.
1. Seleccione la temática en la pestaña **Estilo**.
1. Haga clic en **Crear**.

Las temáticas se utilizan como parte de una plantilla de formulario adaptable para definir el estilo al crear un formulario adaptable.

## Prácticas recomendadas {#best-practices}

* **Evitar recursos de otra temática**

  Al editar una temática, puede examinar y agregar recursos (como imágenes) de otras temáticas. Por ejemplo, quiere editar el fondo de una página. Al seleccionar **[!UICONTROL Página]** ![edit-button](assets/edit-button.png) > **[!UICONTROL Fondo]** > **[!UICONTROL Agregar]** > **[!UICONTROL Imagen]**, verá un cuadro de diálogo que le permite examinar y agregar imágenes en otras temáticas.

  Puede tener problemas con la temática actual si se agrega un recurso desde otra y esta se mueve o se elimina. Se recomienda evitar explorar y agregar recursos de otras temáticas.

* **Cambio de la anchura de diseño del panel contenedor**

  No se recomienda cambiar la anchura del diseño del panel contenedor. Cuando se especifica la anchura de un panel contenedor, este se vuelve estático y no se adapta a distintas pantallas.

## Preguntas frecuentes {#faq}

**P:** ¿Qué personalización tiene prioridad al realizar personalizaciones en una carpeta de temas tanto a nivel global como a nivel de componente?

**R:** Cuando las personalizaciones se realizan tanto en el nivel global como en el nivel de componente, tiene prioridad la personalización en el nivel de componente.

<!--

## See next

* [Set layout of forms for different screen sizes and device types](/help/sites-cloud/authoring/page-editor/responsive-layout.md)
* [Generate Document of Record for Adaptive Forms (Core Components](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
* [Create an Adaptive Forms with Repeatable sections](/help/forms/create-forms-repeatable-sections.md)
* [Sample themes templates and form data models](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html)

-->


## Ver también {#see-also}

{{see-also}}

* [Definición del diseño de los formularios para diferentes tamaños de pantalla y tipos de dispositivos](/help/sites-cloud/authoring/page-editor/responsive-layout.md)
* [Generar documento de registro para formularios adaptables (Componentes principales](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
* [Creación de un formulario adaptable con secciones repetibles](/help/forms/create-forms-repeatable-sections.md)
* [Plantillas temáticas y modelos de datos de formulario de ejemplo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=es)
