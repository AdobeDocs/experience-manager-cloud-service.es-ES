---
title: Crear y usar temáticas
description: Puede utilizar temáticas para aplicar estilo y proporcionar una identidad visual a un formulario adaptable mediante componentes principales. Puede compartir una temática en cualquier número de formularios adaptables.
seo-description: You can create a new theme by customizing the available theme. The themes are customized and deployed using frontend pipeline.
keywords: crear una temática nueva, personalizar una temática, cargar una temática nueva, utilizar una temática en formularios, personalizar una temática mediante la canalización de front-end
exl-id: 11c52b66-dbb1-4c47-a94d-322950cbdac1
source-git-commit: 1cec6e01e72cb286949f64749e2386a2b652920e
workflow-type: tm+mt
source-wordcount: '2697'
ht-degree: 17%

---

# Temáticas en Forms adaptable {#themes-for-af-using-core-components}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/create-or-customize-themes-for-adaptive-forms-core-components.html) |
| AEM as a Cloud Service | Este artículo |

Puede crear y aplicar temáticas para aplicar estilo a un formulario adaptable. Una temática contiene detalles de estilo para los componentes y paneles. Los estilos incluyen propiedades como colores de fondo, colores de estado, transparencia, alineación y tamaño. Al aplicar una temática, el estilo especificado se refleja en los componentes correspondientes. Una temática se administra de forma independiente sin hacer referencia a un formulario adaptable y se puede reutilizar en varios formularios adaptables de Forms.

## Temas disponibles

Forms como Cloud Service proporciona los siguientes temas para componentes principales basados en Forms adaptables:

* [Tema de lienzo](https://github.com/adobe/aem-forms-theme-canvas)
* [Tema WKND](https://github.com/adobe/aem-forms-theme-wknd)
* [Tema EASEL](https://github.com/adobe/aem-forms-theme-easel)

## Comprender la estructura de las temáticas

Una temática es un paquete que incluye el archivo CSS, los archivos JavaScript y los recursos (como iconos) que definen el estilo de su Forms adaptable. Una temática de formulario adaptable sigue una organización específica, que consta de los siguientes componentes:

* `src/theme.scss`: Esta carpeta incluye el archivo CSS que tiene un impacto amplio en toda la temática. Sirve como una ubicación centralizada para definir y administrar el estilo y el comportamiento de la temática. Al realizar ediciones en este archivo, puede realizar cambios que se apliquen universalmente en toda la temática, lo que influye en el aspecto y la funcionalidad tanto de las páginas de AEM Sites como de Forms adaptable.

* `src/site`AEM : esta carpeta contiene archivos CSS que se aplican a toda la página de un sitio de la red de distribución de contenido (CSS) de la página de un sitio de. AEM Estos archivos constan de código y estilos que afectan a la funcionalidad y al diseño generales de la página de su sitio de la red de la red de distribución de contenido (SITE) de su sitio de la red de distribución de contenido (OSGi). Cualquier modificación realizada aquí se reflejará en todas las páginas del sitio. [¿Cuándo se usa?]

* `src/components`AEM : los archivos CSS de esta carpeta están diseñados para componentes principales individuales de la. Cada carpeta dedicada para un componente incluye una `.scss` que aplica estilo a ese componente en particular dentro de un formulario adaptable. Por ejemplo, el archivo /src/components/accordion/_accordion.scss contiene información de estilo para el componente Acordeón de Forms adaptable.

  ![estructura de la temática basada en formularios adaptables](/help/forms/assets/theme_structure.png)

* `src/resources`: esta carpeta contiene archivos estáticos como iconos, logotipos y fuentes. Estos recursos se utilizan para mejorar los elementos visuales y el diseño general del tema.

## Crear una temática

Forms como Cloud Service proporciona los siguientes temas para componentes principales basados en Forms adaptables.

* [Tema de lienzo](https://github.com/adobe/aem-forms-theme-canvas)
* [Tema WKND](https://github.com/adobe/aem-forms-theme-wknd)
* [Tema EASEL](https://github.com/adobe/aem-forms-theme-easel)

Puede [personalizar cualquiera de estas temáticas para crear una nueva](#customize-a-theme-core-components).

![Flujo de trabajo de personalización de temas](/help/forms/assets/workflow-of-customization-of-theme.png)

## Personalizar una temática {#customize-a-theme-core-components}

La personalización de una temática hace referencia al proceso de modificación y personalización de la apariencia de una temática. Al personalizar una temática, cambia sus elementos de diseño, diseño, colores, tipografía y, a veces, el código subyacente. Le permite crear un aspecto único y personalizado para su sitio web o aplicación, al tiempo que mantiene la estructura y la funcionalidad básicas proporcionadas por la temática.

### Requisitos previos {#prerequisites-to-customize}

* Familiarícese con [configuración de una canalización en Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=es#setup-pipeline) y tener conocimientos básicos sobre cómo configurar una canalización le ayuda a administrar e implementar de forma eficaz las personalizaciones de temas.
* Obtenga información sobre cómo [configurar un usuario con la función colaborador](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem.html?lang=es). Si sabe cómo configurar un usuario con la función de colaborador, puede conceder los permisos necesarios para personalizar temáticas.
* Instale la última versión de [Apache Maven.](https://maven.apache.org/download.cgi) Apache Maven es una herramienta de automatización de compilaciones que se utiliza comúnmente en proyectos Java™. La instalación de la última versión garantiza que tenga las dependencias necesarias para la personalización de temáticas.
* Instale un editor de texto sin formato. Por ejemplo, Microsoft® Visual Studio Code. Utilizar un editor de texto sin formato como Microsoft® Visual Studio Code proporciona un entorno fácil de usar para editar y modificar archivos de temas.

### Configurar su entorno

* [Habilitar los componentes principales de Forms adaptable](/help/forms/enable-adaptive-forms-core-components.md)  para su entorno de desarrollo local y Cloud Service.
* Configurar [canalización de implementación front-end](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/enable-frontend-pipeline-devops/create-frontend-pipeline.html) para su entorno de Cloud Service. Como alternativa, puede configurar la canalización más adelante, lo que le ofrece la flexibilidad de priorizar la prueba y el refinamiento del tema antes de configurar la canalización de implementación.

<!-- 
To deploy your themes to a Forms as a Cloud Service environment, first test theme on a local development environment to address any issues. Once the theme is tested, configure the front-end deployment pipeline, which is responsible for deploying the themes.

These themes are deployed to a Forms as a Cloud Service environment via the front-end pipeline. You can configure the pipeline later also, after testing the theme on a local development environment. 

-->

Después de conocer los requisitos previos y configurar el entorno de desarrollo, está bien preparado para empezar a personalizar el tema según sus requisitos específicos.

### Personalizar una temática {#steps-to-customize-a-theme-core-components}

La personalización de una temática es un proceso de varios pasos. Para personalizar la temática, realice los pasos en el orden indicado:

1. [Clonar una temática](#download-a-theme-core-components)
1. [Establecer nombre de temática](#set-name-of-theme)
1. [Personalizar una temática](#customize-the-theme)
1. [Probar una temática](#test-the-theme)
1. [Implementar un tema](#deploy-the-theme)

Los ejemplos proporcionados en el documento se basan en la variable **Lienzo** tema, pero es importante tener en cuenta que puede clonar cualquier tema y personalizarlo con las mismas instrucciones. Estas instrucciones se aplican a cualquier tema, lo que le permite modificarlas según sus necesidades específicas.

#### 1. Clonar una temática {#download-a-theme-core-components}

Para clonar una temática para componentes principales basados en Forms adaptable, elija una de las siguientes temáticas:

* [Tema de lienzo](https://github.com/adobe/aem-forms-theme-canvas)
* [Tema WKND](https://github.com/adobe/aem-forms-theme-wknd)
* [Tema EASEL](https://github.com/adobe/aem-forms-theme-easel)

Para clonar una temática, siga estas instrucciones:

1. Abra el símbolo del sistema o la ventana de terminal en su entorno de desarrollo local.

1. Ejecute el `git clone` para clonar una temática.

   ```
      git clone [Path of Git Repository of the theme]
   ```

   Reemplace el [Ruta del repositorio Git de la temática] con la URL real del repositorio de Git correspondiente de la temática

   Por ejemplo, para clonar la temática Lienzo, ejecute el siguiente comando:

   ```
      git clone https://github.com/adobe/aem-forms-theme-canvas
   ```

   Después de ejecutar el comando correctamente, tiene una copia local del tema disponible en el equipo en el  `aem-forms-theme-canvas` carpeta.


#### 2. Establecer el nombre de una temática {#set-name-of-theme}

1. Abra la carpeta de temáticas en un editor de texto sin formato. Por ejemplo, para abrir `aem-forms-theme-canvas` en el editor de código de Visual Studio.

1. Navegue hasta la carpeta `aem-forms-theme-canvas`. 

1. Ejecute el siguiente comando:

   ```
         code .
   ```

   ![Abra la carpeta de temáticas en un editor de texto sin formato](/help/forms/assets/aem-forms-theme-folder-in-vs-code.png)

   La carpeta se abre en Visual Studio Code.

1. Abra el archivo `package.json` para editarlo.

1. Establezca los valores de `name` y `description` atributos.

   El atributo name se utiliza para identificar la temática de forma exclusiva, como &quot;aem-forms-wknd-theme&quot; y se muestra en la variable **Estilo** pestaña de **Asistente de creación de formularios**. El atributo description proporciona detalles adicionales sobre la temática, incluido su propósito y los escenarios para los que está diseñada. También puede especificar la versión, la descripción y la licencia para la temática.

1. Guarde y cierre el archivo.

![Canvas Nombre del tema Cambiar imagen](/help/forms/assets/changename_canvastheme.png)


#### 3. Personalizar una temática {#customize-the-theme}

Puede personalizar componentes individuales o realizar cambios en el nivel de tema mediante variables globales de una temática. Cualquier cambio realizado en las variables globales afecta a todos los componentes individuales. Por ejemplo, puede utilizar variables globales para cambiar el color del borde de todos los componentes de un formulario adaptable y un color de relleno brillante para establecer CTA (llamada a la acción) mediante el componente de botón:

* [Establecer estilos de nivel de tema](#theme-customization-global-level)

* [Definir estilos de nivel de componente](#component-based-customization)

##### Establecer estilos de nivel de tema{#theme-customization-global-level}

El `variable.scss` contiene las variables globales de la temática. Al actualizar estas variables, puede realizar cambios relacionados con los estilos en el nivel de la temática. Para aplicar estilos de nivel de tema, siga estos pasos:

1. Abra el archivo `<your-theme-sources>/src/site/_variables.scss` para editarlo.
1. Cambie el valor de cualquier propiedad. Por ejemplo, el color de error predeterminado es `red`. Para cambiar el color del error de `red` hasta `blue`, cambie el código hexadecimal de color del `$errorvariable`. Por ejemplo, `$error: #196ee5`.
1. Guarde y cierre el archivo.

   ![Editar tema](/help/forms/assets/edit_theme.png)

Del mismo modo, puede utilizar la variable `variable.scss` archivo para establecer la familia y el tipo de fuente, los colores de la temática y la fuente, el tamaño de fuente, el espaciado del tema, el icono de error, los estilos de borde del tema y más variables que afectan a varios componentes del formulario adaptable.

##### Definir estilos de nivel de componente {#component-based-customization}

También puede cambiar la fuente, el color, el tamaño y otras propiedades CSS de un componente principal de formulario adaptable específico. Por ejemplo, botón, casilla de verificación, contenedor, pie de página, etc. Puede aplicar estilo a un botón o una casilla de verificación editando el archivo CSS del componente específico para alinearlo con el estilo de su organización. Para personalizar el estilo de un componente:

1. Abra el archivo `<your-theme-sources>/src/components/<component>/<component.scss>` para editar. Por ejemplo, para cambiar el color de fuente del componente Botón, abra el `<your-theme-sources>/src/components/button/button.scss`, archivo .
1. Cambie el valor de cualquiera según sus necesidades. Por ejemplo, para cambiar el color del componente Botón al pasar el ratón por encima de `green`, cambie el valor del `color: $white` propiedad en el `cmp-adaptiveform-button__widget:hover` clase a código hexadecimal `#12B453` o cualquier otro tono de `green`. El código final tiene el siguiente aspecto:

   ```
   .cmp-adaptiveform-button__widget:hover {
   background: $dark-gray;
   color: #12B453;
   }
   ```

1. Guarde y cierre el archivo.

   ![Editar CSS de cuadro de texto](/help/forms/assets/edit_color_textbox.png)

   >
   >
   > Cuando se define un estilo tanto en el nivel de tema como de componente, el estilo definido en el nivel de componente tiene prioridad.

#### 4. Probar una temática personalizada {#test-the-theme}

AEM Para obtener una vista previa y probar los cambios en el entorno local y personalizar la temática según los requisitos de diferentes componentes de la, realice los siguientes pasos:

* 4,1 [Configuración del entorno local para pruebas](#rename-env-file-theme-folder)
* 4,2 [Probar la temática mediante el entorno local](#start-a-local-proxy-server)

##### 4.1. Configurar el entorno local para realizar pruebas {#rename-env-file-theme-folder}

1. Abra la carpeta de temáticas en un editor de texto sin formato. Por ejemplo, abra el `aem-forms-theme-canvas` en el editor de código de Visual Studio.
1. Cambie el nombre del `env_template` archivo a `.env` en la carpeta theme y agregue los siguientes parámetros:

   ```
   * **AEM url**
   AEM_URL=https://[author-instance] 
   
   * **AEM Adaptive form name**
   AEM_ADAPTIVE_FORM=Form_name
   
   * **AEM proxy port**
   AEM_PROXY_PORT=7000
   ```

   Por ejemplo, la dirección URL del formulario es `http://localhost:4502/editor.html/content/forms/af/contactusform.html`. Por lo tanto, los valores de:

   * AEM URL_de_la_= `http://localhost:4502/`
   * AEM FORMULARIO_ADAPTABLE_ADAPTABLE_= `contactusform`

1. Guarde el archivo.

   ![Estructura de la temática Lienzo](/help/forms/assets/env-file-canvas-theme.png)

##### 4.2 Probar la temática mediante el entorno local {#start-a-local-proxy-server}

1. Vaya a la raíz de la carpeta de temáticas. En este caso, el nombre de la carpeta de temas es `aem-forms-theme-canvas`.
1. Abra el símbolo de comando o el terminal.
1. Ejecutar `npm install` para instalar las dependencias.
1. Ejecutar `npm run live` para obtener una vista previa del formulario con la temática actualizada en el explorador local.

   >[!NOTE]
   >
   > Si se produce un error durante la ejecución de `npm run live` , ejecute los siguientes comandos antes de `npm run live` comando:
   >
   > * `npm install parcel --save-dev`
   > * `npm i @parcel/transformer-sass`

Esta es una implementación activa. Por lo tanto, cada vez que realice cambios y guarde el `_variables.scss` y `button.scss` archivos, el servidor selecciona automáticamente los cambios y obtiene una vista previa del resultado más reciente. La línea `[Browsersync] File event [change]` significa que el servidor ha reconocido los cambios más recientes y está implementando los cambios en el entorno local.

![Sincronización de exploradores proxy](/help/forms/assets/browser_sync.png)

Después de haber seguido los ejemplos proporcionados tanto a nivel de tema como de componente para las personalizaciones de temas, los mensajes de error de un formulario adaptable se cambian a `blue` color, mientras que el color de la etiqueta del componente de botón cambia a `green` al pasar el ratón por encima.

**Vista previa del estilo de nivel de tema**

![Ejemplo: Color de error establecido en azul](/help/forms/assets/theme-level-changes.png)

**Vista previa del estilo de nivel de componente**

![Ejemplo: Color de desplazamiento establecido en verde](/help/forms/assets/button-customization.png)

###### Probar la temática para formularios alojados en un entorno de Cloud Service

También puede probar la temática del formulario adaptable alojado en la instancia as a Cloud Service de AEM Forms. Para configurar y establecer el entorno local para probar las temáticas con el Forms adaptable alojado en la instancia de nube, realice los siguientes pasos:

1. Abra la carpeta de temáticas en un editor de texto sin formato. Por ejemplo, abra el `aem-forms-theme-canvas` en el editor de código de Visual Studio.
1. Cambie el nombre del `env_template` archivo a `.env` y agregue los siguientes parámetros:

   ```
   * **AEM url**
   AEM_URL=https://[author-instance] 
   
   * **AEM Adaptive form name**
   AEM_ADAPTIVE_FORM=Form_name
   
   * **AEM proxy port**
   AEM_PROXY_PORT=7000
   ```

   Por ejemplo, la URL del formulario en el entorno de la nube es `https://author-XXXX.adobeaemcloud.com/editor.html/content/forms/af/contactusform.html`. Por lo tanto, los valores de:

   * AEM URL_de_la_= `https://author-XXXX-cmstg.adobeaemcloud.com/`
   * AEM FORMULARIO_ADAPTABLE_ADAPTABLE_= `contactusform`
1. Guarde el archivo.
1. Cree un usuario local.

   >[!NOTE]
   >
   > Para crear un usuario local:
   >
   > * Ir a **[!UICONTROL AEM Página de inicio]** > **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Usuarios]** .
   > * Asegúrese de que el usuario sea miembro de `forms-users` grupo.

1. Vaya a la raíz de la carpeta de temáticas. En este caso, el nombre de la carpeta de temas es `aem-forms-theme-canvas`.
1. Ejecutar `npm run live` y se le redirigirá a un explorador local.
1. Clic `SIGN IN LOCALLY (ADMIN TASKS ONLY)` e inicie sesión con las credenciales del usuario local.

Puede obtener una vista previa del formulario adaptable con los cambios más recientes. Una vez que esté satisfecho con las modificaciones realizadas en una carpeta de temas, implemente el tema en el entorno de AEM Cloud Service mediante la canalización front-end.

#### 5. Implementar un tema {#deploy-the-theme}

Para implementar el tema en el entorno del Cloud Service mediante la canalización front-end:

* 5,1 [Crear un repositorio para la temática](#create-a-new-theme-repo)
* 5,2 [Insertar los cambios en el repositorio](#committing-the-changes)
* 5,3 [Ejecutar la canalización de front-end](#run-a-frontend-pipeline)

##### 5.1 Crear un repositorio para la temática{#create-a-new-theme-repo}

Se necesita un repositorio para implementar la temática. Inicie sesión en su [AEM Repositorio de Cloud Manager de](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=es#accessing-git) y agregue un nuevo repositorio para la temática.

1. Cree un nuevo repositorio para la temática haciendo clic en **[!UICONTROL Repositorios]** > **[!UICONTROL Añadir repositorio]**.

   ![crear nuevo repositorio de temáticas](/help/forms/assets/createrepo_canvastheme.png)


1. Especifique el **Nombre del repositorio** en el **Añadir repositorio** Cuadro de diálogo. Por ejemplo, el nombre proporcionado es `custom-canvas-theme-repo`.
1. Haga clic en **[!UICONTROL Guardar]**.

   ![Adición de repositorios de temática Lienzo](/help/forms/assets/addcanvasthemerepo.png)

1. Clic **[!UICONTROL Copiar URL del repositorio]** para copiar la URL del repositorio.

   ![URL de temática Lienzo](/help/forms/assets/copyurl_canvastheme.png)

   >[!NOTE]
   > 
   > * Puede utilizar un único repositorio para varias temáticas.
   > * Para implementar diferentes temáticas, debe crear canalizaciones front-end independientes.
   >* Por ejemplo, puede utilizar el mismo repositorio que `custom-canvas-theme-repo`, para la temática Lienzo, la temática WKND y la temática EASEL. Sin embargo, para implementar los temas, debe crear canalizaciones front-end independientes. Las futuras personalizaciones de un tema específico se implementan mediante la canalización front-end correspondiente.

##### 5.2. Insertar los cambios en el repositorio {#committing-the-changes}

Ahora, inserte los cambios en el repositorio de temáticas de su Cloud Service de AEM Forms. .

1. Vaya a la raíz de la carpeta de temáticas.  En este caso, el nombre de la carpeta de temas es `aem-forms-theme-canvas`.
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



##### 5.3 Ejecutar la canalización de front-end {#run-a-frontend-pipeline}

El tema se implementa mediante la variable [canalización front-end.](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/enable-frontend-pipeline-devops/create-frontend-pipeline.html). Para implementar una temática, realice los siguientes pasos:

1. AEM Inicie sesión en el repositorio de Cloud Manager de.
1. Clic **[!UICONTROL Añadir]** del menú contextual **[!UICONTROL Canalizaciones]** sección.
1. Seleccionar **[!UICONTROL Agregar canalización que no sea de producción]** o **[!UICONTROL Agregar canalización de producción]** en función del entorno Cloud Service. Por ejemplo, aquí el **[!UICONTROL Agregar canalización de producción]** La opción está seleccionada.
1. En el **[!UICONTROL Agregar canalización de producción]** como parte del **[!UICONTROL Configuración]** , especifique el nombre de la canalización. Por ejemplo, el nombre de la canalización es `customcanvastheme`.
1. Haga clic en **[!UICONTROL Continuar]**.
1. Seleccione el **[!UICONTROL Implementación objetivo]** > el **[!UICONTROL Código front-end]** opciones, en la **[!UICONTROL Código fuente]** pasos.
1. Seleccione el **[!UICONTROL Repositorio]** y el **[!UICONTROL Rama Git]** valores que tienen sus cambios más recientes. Por ejemplo, aquí el nombre de repositorio seleccionado es `custom-canvas-theme-repo` y la rama Git es `main`.
1. Seleccione el **[!UICONTROL Ubicación del código]** as `/`, si los cambios están presentes en la carpeta raíz.
1. Haga clic en **[!UICONTROL Guardar]**.
   ![crear canalización front-end](/help/forms/assets/canvas-theme-frontendpipeline.gif)

   Una vez completada la configuración de la canalización, se actualiza la tarjeta de llamada a la acción.

1. Haga clic con el botón derecho en la canalización creada.
1. Clic **[!UICONTROL Ejecutar]** .

   ![run-a-pipleine](/help/forms/assets/canvas-theme-run-pipeline.png)

Una vez finalizada la compilación, la temática está disponible en la instancia de autor para el uso. Aparece bajo la etiqueta **[!UICONTROL Estilo]** en el asistente de creación de formularios adaptables, mientras crea un nuevo formulario adaptable.

![tema personalizado disponible en la pestaña estilo](/help/forms/assets/custom-theme-style-tab.png)

## Aplicar una temática a un formulario adaptable {#using-theme-in-adaptive-form}

Los pasos para aplicar una temática a un formulario adaptable son los siguientes:

1. Inicie sesión en la instancia de creación de AEM Forms.

1. Vaya a **Adobe Experience Manager** > **Formularios** > **Formularios y documentos**.

1. Haga clic en **Crear** > **Formularios adaptables**. Se abre el asistente para crear formularios adaptables.

1. Seleccione la plantilla del componente principal en la pestaña **Fuente**.
1. Seleccione la temática en la **Estilo** pestaña.
1. Haga clic en **Crear**.

Las temáticas se utilizan como parte de una plantilla de formulario adaptable para definir el estilo al crear un formulario adaptable.

## Prácticas recomendadas {#best-practices}

* **Evitar recursos de otra temática**

  Al editar una temática, puede examinar y agregar recursos (como imágenes) de otras temáticas. Por ejemplo, quiere editar el fondo de una página. Al seleccionar **[!UICONTROL Página]** ![edit-button](assets/edit-button.png) > **[!UICONTROL Fondo]** > **[!UICONTROL Agregar]** > **[!UICONTROL Imagen]**, verá un cuadro de diálogo que le permite examinar y agregar imágenes en otras temáticas.

  Puede tener problemas con la temática actual si se agrega un recurso desde otra y esta se mueve o se elimina. Se recomienda evitar explorar y agregar recursos de otras temáticas.

* **Cambio de la anchura de diseño del panel contenedor**

  No se recomienda cambiar la anchura del diseño del panel contenedor. Cuando se especifica la anchura de un panel contenedor, este se vuelve estático y no se adapta a distintas pantallas.

* **Uso del editor de formularios o de temáticas para trabajar con encabezado y pie de página**

  Utilice el editor de temáticas si desea aplicar estilo al encabezado y al pie de página mediante opciones de estilo como estilo de fuente, fondo y transparencia. 
Si desea proporcionar información como un logotipo, el nombre de la empresa en el encabezado e información de copyright en el pie de página, utilice las opciones del editor de formularios.

## Preguntas frecuentes {#faq}

**P:** ¿Qué personalización tiene prioridad al realizar personalizaciones en una carpeta de temas tanto a nivel global como a nivel de componente?

**R:** Cuando las personalizaciones se realizan tanto en el nivel global como en el nivel de componente, tiene prioridad la personalización en el nivel de componente.

## Ver siguiente

* [Definir la presentación de los formularios para diferentes tamaños de pantalla y tipos de dispositivos](/help/sites-cloud/authoring/features/responsive-layout.md)
* [Generar documento de registro para Forms adaptable (componentes principales)](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
* [Creación de un Forms adaptable con secciones repetibles](/help/forms/create-forms-repeatable-sections.md)


## Artículo relacionado {#related-article}

* [Habilitar los componentes principales de formularios adaptables en el entorno de desarrollo as a Cloud Service y local de AEM Forms](/help/forms/enable-adaptive-forms-core-components.md)
* [Crear un formulario adaptable independiente basado en componentes principales](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html?lang=es)
