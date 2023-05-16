---
title: Agregar un formulario adaptable (componentes principales) en la página de AEM Sites
seo-title: How to add an Adaptive Form (Core Components) to an AEM Sites page?
description: Puede utilizar el formulario adaptable (componentes principales) en una página de AEM Sites para rellenar y enviar un formulario sin salir de las páginas de AEM Sites.
feature: Adaptive Forms
hide: true
hidefromtoc: true
exl-id: 1046231f-787c-4e49-9ba0-e7dd59e41bce
source-git-commit: 0d21b4ba2e7ce7592e3f2c57e4d320adc0af1008
workflow-type: tm+mt
source-wordcount: '2207'
ht-degree: 21%

---

# Agregar Forms adaptable a una página de AEM Sites {#add-an-adaptive-form-to-aem-sites-page}

## Información general {#overview}

Puede crear o incrustar Forms adaptable sin problemas en una página de AEM Sites para permitir que los usuarios rellenen y envíen un formulario sin salir de la página Sitios. Ayuda al usuario a permanecer en el contexto de otros elementos de la página web e interactuar simultáneamente con el formulario.

Puede elegir uno de los siguientes métodos para crear o incrustar un formulario adaptable en una página de AEM Sites:

* **Crear un formulario adaptable arrastrando y soltando los componentes del formulario al componente contenedor de Forms adaptable**: Utilice la variable [Contenedor de Forms adaptable](#af-container-component) para crear un espacio en la página web que alojaría el formulario adaptable. Puede arrastrar y soltar el componente Formulario adaptable en este espacio para crear un formulario. Por ejemplo, consulte el siguiente vídeo para aprender a crear un formulario adaptable mediante [!UICONTROL Contenedor de Forms adaptable] componente:

La variable [Contenedor de formulario adaptable](#af-container-component) permite crear experiencias de inscripción digital utilizando los componentes de Forms adaptables directamente en el editor de AEM Sites. Esta integración proporciona una experiencia perfecta a los autores de AEM Sites que desean crear y administrar formularios dentro de sus páginas de AEM Sites.

* **Incrustar un formulario adaptable existente**: La variable [Forms adaptable: Incrustar (V2)](#embed-existing-af) permite incorporar fácilmente un formulario adaptable preexistente en una página de AEM Sites. Por ejemplo, incruste un formulario adaptable utilizando la variable [!UICONTROL Forms adaptable: incrustar] en la página del sitio, como se muestra en el siguiente vídeo:

Esta función mejora la adaptabilidad y la reutilización de Forms adaptable. Esta integración proporciona una forma cómoda para que los clientes puedan reutilizar el Forms adaptable que ya han creado.

* **Utilice el Asistente para Forms adaptable para crear un formulario**:

   Utilice la variable [Forms adaptable: Incrustar (v2)](#embed-new-af) para crear un formulario adaptable desde el editor de AEM Sites mediante el asistente de creación de formularios. El formulario se guarda como una entidad externa. Puede volver a utilizar este formulario en otras páginas de Sitios y también en formularios independientes.
Por ejemplo, consulte el siguiente vídeo para aprender a crear e incrustar un formulario adaptable recién creado mediante el [!UICONTROL Forms adaptable: incrustar] en la página del sitio.

### Consideración {#considerations}

Puede utilizar el Editor de reglas para añadir o controlar el comportamiento dinámico de los componentes del formulario adaptable. Por ejemplo, ocultar o mostrar un componente. El Editor de reglas no está disponible para los componentes de formulario no adaptable. Por lo tanto, utilice la diligencia mientras utiliza componentes de formulario no adaptable en el componente Contenedor de AEM Forms.

## Creación de un formulario adaptable mediante el componente contenedor de Forms adaptable {#af-container-component}

La variable [!UICONTROL Contenedor de formulario adaptable] permite crear experiencias de inscripción digital mediante los componentes de Forms adaptable en el editor de AEM Sites. Puede crear un formulario adaptable arrastrando y soltando los componentes del formulario.

### Requisitos previos {#prerequisites-af-container}

+++ Habilitar **[!UICONTROL Contenedor de Forms adaptable]** en la política de la plantilla asociada.

Para habilitar [!UICONTROL Contenedor de Forms adaptable] en la política de la plantilla, realice los siguientes pasos:

1. Vaya a la [!UICONTROL Información de la página] > [!UICONTROL Editar plantilla]
1. Haga clic en el [!UICONTROL Política] y seleccione **[!UICONTROL Contenedor de Forms adaptable]**  dentro de **[Nombre del proyecto de tipo de archivo AEM] - Formulario adaptable**.
1. Haga clic en **[!UICONTROL Listo]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++

+++ Incluir clientlibs en la página del sitio

Para utilizar componentes de Forms adaptable en una página de AEM Sites, incluya las bibliotecas de cliente Customheaderlibs y Customfooterlibs en la página de AEM Sites mediante el Repositorio de Tipo de archivo/Git de AEM y la canalización de implementación.

1. Abra su [Tipo de archivo de AEM Forms o repositorio de Git clonado](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es) proyecto en un editor de texto. Por ejemplo, código de Visual Studio.
1. Navegue hasta `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`.
1. Copiar el valor de `sling:resourceSuperType`. Por ejemplo, el valor es `core/wcm/components/page/v3/page`.

   ![recurso de sling](/help/forms/assets/slingresource.png)

1. Crear una estructura similar en la ubicación `ui.apps/src/main/content/jcr_root/apps` same `core/wcm/components/page/v3/page`.

   ![estructura de superposición](/help/forms/assets/overlaystructure.png)

1. Agregar `customheaderlibs.html` y `customfooterlibs.html` archivos.

   ```
   //Customheaderlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
   </sly> 
   
   //customfooterlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
   </sly> 
   ```

   customfooterlibs.html se utiliza para JavaScript y customheaderlibs.html para css.

1. [Ejecución de la canalización](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) para implementar los cambios.

+++

### Creación de un formulario adaptable mediante el componente Contenedor de Forms adaptable {#create-af-using-af-container}


Para crear un formulario adaptable utilizando [!UICONTROL Contenedor de Forms adaptable] componente:

1. Abra la página de AEM Sites en modo de edición.
1. En el panel Navegador de componentes , arrastre y suelte el **[!UICONTROL Contenedor de Forms adaptable]** en la página.
1. Cree un formulario adaptable utilizando los componentes de Forms adaptable .
1. Guarde la configuración.

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

Su formulario está listo. Cuando publica la página de AEM Sites, publica automáticamente un formulario adaptable y sus recursos de referencia asociados.

#### Configurar las propiedades del contenedor de formularios adaptables {#configure-additional-settings-container}

Puede personalizar la configuración avanzada del [!UICONTROL Contenedor de formulario adaptable] componente. Por ejemplo, puede configurar el servicio de relleno previo para cargar un formulario adaptable con valores precargados en la página de un sitio. La configuración del modelo de datos se configura para asociar el formulario adaptable a un modelo de datos. Si desea guardar los datos en OneDrive o SharePoint al enviar un formulario adaptable, configure las opciones para la acción Envío. También puede agregar una acción de envío personalizada para su Forms adaptable.

Para establecer las propiedades de la variable **[!UICONTROL Contenedor de Forms adaptable]** , haga clic en el botón ![settings_icon](/help/forms/assets/Smock_Wrench_18_N.svg) en la barra de acciones. La variable **[!UICONTROL Editar contenedor de Forms adaptable]** se abre.

![Cuadro de diálogo de edición](/help/forms/assets/adaptiveformcontainer-editdialog.png)

En el [!UICONTROL Editar contenedor de Forms adaptable] , puede especificar lo siguiente.
* **Pestaña Básicos**
   * **Servicio de precarga**: Puede utilizar el servicio de cumplimentación previa para rellenar automáticamente los campos de un formulario adaptable utilizando los datos existentes. Cuando un usuario abre un formulario, los valores de esos campos ya han sido rellenados. Para obtener información sobre el servicio de precarga, consulte [Rellene previamente los campos del formulario adaptable](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/prepopulate-adaptive-form-fields.html#configuring-prefill-service-using-configuration-manager)
   * **Categoría de la biblioteca del cliente**: Especifique la variable [Funciones de JavaScript](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=en#custom-functions) que se utilizan en expresiones y son compatibles con Adaptive Forms.
* **Modelo de datos**: Un modelo de datos permite integrar entidades y servicios de distintos orígenes de datos en un formulario adaptable. Choose **[!UICONTROL Modelo de datos de formulario]** si el formulario adaptable que está creando implica recuperar y escribir datos desde y hacia varias fuentes de datos.
   * **Modelo de datos de formulario**: Un modelo de datos de formulario permite que un formulario adaptable se comunique con distintos orígenes de datos. Para obtener información sobre la configuración de una fuente de datos, consulte [Configure las fuentes de datos.](/help/forms/configure-data-sources.md)
   * **Esquema**: El esquema representa la estructura en la que el sistema back-end de su organización produce o consume datos. Puede [asociar el esquema a un formulario adaptable](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/adaptive-form-json-schema-form-model.html) y utilice sus elementos para añadir contenido dinámico a un formulario adaptable.

      >[!NOTE]
      >
      > Después de configurar el modelo de datos de formulario, no se puede cambiar el modelo de formulario asociado. Sin embargo, es posible modificar el esquema asociado al modelo de datos de formulario.

* **Pestaña Envío**

   * **Redirigir a URL**

      **Dirección URL/ruta de redireccionamiento**: Especifica la dirección URL o la ruta a la que se redirige un formulario adaptable después de la acción de envío.

      **Enviar acción**: Una acción de envío se activa cuando un usuario hace clic en el botón Enviar de un formulario adaptable. Puede [configurar la acción de envío en el formulario adaptable](/help/forms/configuring-submit-actions.md). Los formularios adaptables proporcionan algunas acciones de envío listas para usar:
      * Enviar al punto final REST
      * Enviar correo electrónico
      * Enviar mediante modelo de datos de formulario
      * Invocar un flujo de trabajo de AEM
      * Enviar a SharePoint
      * Enviar a OneDrive
      * Enviar a Azure Blob Storage

   También puede [ampliar las acciones de envío predeterminadas](custom-submit-action-form.md) para crear su propia acción de envío personalizada.

* **Mostrar mensaje**
   * **Contenido del mensaje**: Escriba un mensaje con el editor de texto enriquecido para mostrarlo en el envío del formulario. Esta opción solo está disponible cuando elige mostrar un mensaje de agradecimiento.

## Incrustar un formulario adaptable  {#aem-container-component}

Uso **[!UICONTROL Forms adaptable: incrustar (V2)]** , puede incrustar un nuevo formulario adaptable o incrustar un formulario adaptable existente en la página del sitio. La variable [!UICONTROL Forms adaptable: incrustar] le permite:

* [Incrustar un formulario adaptable existente](#embed-new-af)

* [Crear e incrustar un nuevo formulario adaptable](#embed-existing-af)

### Requisitos previos {#prerequisites}

+++ Active la variable **Forms adaptable: incrustar** en la política de la plantilla asociada.

Para habilitar [!UICONTROL Forms adaptable: Incrustar (v2)] en la política de la plantilla, realice los siguientes pasos:

1. Vaya a la [!UICONTROL Información de la página] > [!UICONTROL Editar plantilla]

1. Haga clic en el [!UICONTROL Política] y seleccione **[!UICONTROL Formulario adaptable: incrustado (v2)]** dentro de **[!UICONTROL [Nombre del proyecto de tipo de archivo AEM] - Forms]** grupo .
1. Haga clic en **[!UICONTROL Listo]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419369?quality=12&learn=on)

+++

+++ Incluir clientlibs en la página del sitio

Cuando la variable **[!UICONTROL Cuando el formulario abarca toda la anchura de una página]** está seleccionada en la **[!UICONTROL Contenedores de formulario]** configure el cuadro de diálogo y **Forms adaptable con componentes principales** , es necesario incluir los clientlibs en la página del sitio correspondiente.

![Superposición de Gif](/help/forms/assets/overlaycorecomponent.gif)

Para utilizar componentes de Forms adaptable en una página de AEM Sites, incluya las bibliotecas de cliente Customheaderlibs y Customfooterlibs en la página de AEM Sites mediante el Repositorio de Tipo de archivo/Git de AEM y la canalización de implementación.

1. Abra su [Tipo de archivo de AEM Forms o repositorio de Git clonado](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es) proyecto en un editor de texto. Por ejemplo, código de Visual Studio.
1. Navegue hasta `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`.
1. Copiar el valor de `sling:resourceSuperType`. Por ejemplo, el valor es `core/wcm/components/page/v3/page`.

   ![recurso de sling](/help/forms/assets/slingresource.png)

1. Crear una estructura similar en la ubicación `ui.apps/src/main/content/jcr_root/apps` same `core/wcm/components/page/v3/page`.

   ![estructura de superposición](/help/forms/assets/overlaystructure.png)

1. Agregar `customheaderlibs.html` y `customfooterlibs.html` archivos.

   ```
   //Customheaderlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
       data-sly-use.form="com.adobe.cq.forms.core.components.models.aemform.AEMForm">
       <sly data-sly-test="${form.formVersion=='2.1' && !wcmmode.edit}" data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
   </sly>
   
   //customfooterlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
     data-sly-use.form="com.adobe.cq.forms.core.components.models.aemform.AEMForm">
     <sly data-sly-test="${form.formVersion=='2.1' && !wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
   </sly>
   ```

   customfooterlibs.html se utiliza para JavaScript y customheaderlibs.html para el CSS.

1. [Ejecución de la canalización](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) para implementar los cambios.

+++

### Incrustar nuevo formulario adaptable {#embed-new-af}

1. Abra la página de AEM Sites en modo de edición.
1. En el panel Navegador de componentes , arrastre y suelte el [!UICONTROL Forms adaptable: Incrustar (v2)] en la página.
1. Haga clic en el **Más** y se le redirige al asistente de creación de formularios.

   ![Forms adaptable: componente incrustado](/help/forms/assets/aemformcontainer.png)

1. Cree un nuevo formulario adaptable desde el [!UICONTROL Creación de formularios] asistente.
1. La variable [!UICONTROL Ruta de recursos] ya incluye la ruta de un formulario adaptable creado
1. Guarde la configuración. El formulario adaptable está ahora incrustado en la página.

>[!VIDEO](https://video.tv.adobe.com/v/3419366/adaptive-form-aem-forms?quality=12&learn=on)

### Incrustar formulario adaptable existente {#embed-existing-af}

1. Abra la página de AEM Sites en modo de edición.
1. En el panel Navegador de componentes , arrastre y suelte el [!UICONTROL Forms adaptable: incrustar] en la página.
1. Toque . [!UICONTROL Forms adaptable: incrustar] en la página Sitios y pulse ![settings_icon](/help/forms/assets/Smock_Wrench_18_N.svg) en la barra de acciones. La variable **[!UICONTROL Editar Forms adaptable: Incrustar]** se abre.
1. Busque y seleccione el formulario adaptable para incrustarlo en el [!UICONTROL Ruta de recursos].
1. Guarde la configuración. El formulario adaptable está ahora incrustado en la página.

>[!VIDEO](https://video.tv.adobe.com/v/3419368?quality=12&learn=on)

#### Configurar el formulario adaptable _ Incrustar propiedades

Puede personalizar la configuración avanzada del [!UICONTROL Formulario adaptable - Incrustar(v2)] componente. En el [!UICONTROL Editar Forms adaptable: Incrustar (v2)] , puede especificar lo siguiente.

* **Ruta del recurso**: examine y seleccione el formulario adaptable que desea incrustar. Se rellena automáticamente si ha colocado el formulario desde el Explorador de recursos.
* **Después del envío**: seleccione la acción que debe activarse después del envío del formulario. Puede elegir mostrar un mensaje o una página de agradecimiento.
   * **Mostrar mensaje de agradecimiento**: Escriba un mensaje con el editor de texto enriquecido para mostrarlo en el envío del formulario. Esta opción solo está disponible cuando elige mostrar un mensaje de agradecimiento.
   * **Mostrar página de agradecimiento**: Busque y seleccione la página que desea mostrar en el envío del formulario. Esta opción solo está disponible cuando elige mostrar una página de agradecimiento.
   * **Redirigir a la página de agradecimiento**: active la opción para reemplazar la página que contiene el formulario adaptable incrustado por una página de agradecimiento. De lo contrario, la página de agradecimiento sustituye al formulario adaptable en la [!UICONTROL Forms adaptable: incrustar] sin actualizar sitios subyacentes en la página. Esta opción solo está disponible cuando elige mostrar una página de agradecimiento.
* **Usar el idioma de la página**: utilice la configuración local de la página de AEM Sites en lugar de la configuración regional del formulario adaptable.
* **Definir el enfoque del formulario**: seleccione esta opción para establecer el enfoque en el primer campo del formulario adaptable.
* **El formulario abarca toda la anchura del marco**: Si se selecciona, el iframe no se utiliza para procesar el formulario.
* **Altura**: especifique la altura del contenedor. Déjelo en blanco para cambiar automáticamente el tamaño del contenedor.
* **Biblioteca de cliente CSS**: especifique la ruta a una biblioteca de cliente CSS.

### Publicar formulario adaptable incrustado {#publishing-embedded-adaptive-form}

Consideremos los siguientes escenarios a la hora de publicar un formulario adaptable incrustado en una página de AEM Sites:

* Si publica la página de AEM Sites por primera vez y esta incluye un formulario adaptable incrustado, publique la página de Sites y el recurso incrustado.
* Si ha modificado únicamente el formulario adaptable incrustado en una página de Sites ya publicada, publique el recurso original, y los cambios se reflejarán en la página de Sites publicada. La página de Sites publicada incluye una referencia al recurso y no requiere que vuelva a publicar la página.
* Si ha modificado la página de Sites y el formulario adaptable integrado, vuelva a publicar la página y el recurso incrustado.

### Modificar formulario adaptable incrustado  {#modifying-embedded-adaptive-form}

Para modificar cualquier configuración o propiedad del formulario adaptable incrustado, realice una de las siguientes acciones.

* Abra el formulario original en un formulario adaptable en el editor correspondiente y edítelo.
* Pulse el formulario adaptable desde la página de Sites en el modo Edición y, a continuación, pulse **[!UICONTROL Editar en una nueva ventana]**. El formulario original se abrirá en el modo Edición, en el cual puede modificarlo.

>[!NOTE]
>
>Los cambios realizados en el formulario adaptable original se reflejarán automáticamente en el formulario incrustado. Sin embargo, vuelva a publicar el formulario adaptable o la página del sitio para reflejar los cambios en la página publicada.

### Prácticas recomendadas {#best-practices}

* El encabezado y el pie de página del formulario original no se incluyen en el formulario incrustado.
* Los borradores de usuario y los envíos de formularios incrustados son compatibles y visibles en las fichas Borradores y Forms enviado del Portal de Forms.

[En la página AEM Sites, el modo Diseño](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/features/responsive-layout.html?#defining-layouts-layout-mode) permite cambiar el tamaño de un formulario adaptable que se haya creado o incrustado en una página de un sitio AEM.

![Soporte de diseño AF](/help/forms/assets/afsite-layoutsupport.gif)

AEM página sitios mantiene una referencia al formulario adaptable. Cuando se traduce una página de AEM Sites, se traduce automáticamente un formulario adaptable y sus recursos de referencia asociados mediante la variable [proyectos de traducción](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/reusing-content/translation/managing-projects.html?lang=en#adding-pages-assets-to-a-translation-job) en otros idiomas.
