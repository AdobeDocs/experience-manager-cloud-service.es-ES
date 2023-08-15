---
title: Agregar o crear un formulario adaptable (componentes principales) en la página de AEM Sites
seo-title: How to add or create an Adaptive Form (Core Components) to an AEM Sites page?
description: Puede utilizar el formulario adaptable (componentes principales) en una página de AEM Sites para rellenar y enviar un formulario sin salir de las páginas de AEM Sites.
feature: Adaptive Forms
hide: true
hidefromtoc: true
exl-id: 1046231f-787c-4e49-9ba0-e7dd59e41bce
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '2131'
ht-degree: 96%

---

# Crear o agregar un formulario adaptable mediante el Editor de AEM Sites {#add-an-adaptive-form-to-aem-sites-page}

Puede crear o incrustar formularios adaptables sin problemas en una página de AEM Sites para permitir que los usuarios rellenen y envíen un formulario sin salir de la página Sites. Esto permite al usuario mantenerse dentro del contexto de otros elementos de la página web e interactuar simultáneamente con el formulario.

Puede elegir uno de los siguientes métodos para crear o agregar un formulario adaptable en una página de AEM Sites:

* **Crear un formulario adaptable mediante el componente Contenedor de Forms adaptable**: La [Contenedor de formulario adaptable](#af-container-component) Este componente le permite crear experiencias de inscripción digitales utilizando componentes de Forms adaptables directamente en el editor de AEM Sites. Esta integración proporciona una experiencia perfecta a los creadores de AEM Sites que desean crear y administrar formularios dentro de sus páginas de AEM Sites.

* **Agregar un formulario adaptable existente**: La [Forms adaptable: incrustado (v2)](#embed-existing-af) Este componente le permite agregar fácilmente un formulario adaptable preexistente a una página dentro de AEM Sites. Esta función mejora la adaptabilidad y la reutilización de formularios adaptables. Esta integración proporciona una forma cómoda para que los clientes puedan reutilizar los formularios adaptables que ya han creado.

* **Utilice el Asistente para formularios adaptables para crear un formulario**: Utilice el componente de [Formularios adaptables: incrustar(v2)](#embed-new-af) para crear un formulario adaptable desde el editor de AEM Sites mediante el asistente de creación de formularios. El formulario se guarda como una entidad externa. Puede volver a utilizar este formulario en otras páginas de Sites y también en formularios independientes.

* **Agregar varios Formularios adaptables en una página de AEM Sites**: para agregar varios Formularios adaptables en una página de AEM Sites, utilice los componentes de contenedor de AEM Forms: [Formularios adaptables: incrustado(v2)](#embed-new-af) y [Contenedor de formulario adaptable](#af-container-component). En caso de que necesite agregar más de un formulario adaptable como div dentro de una página de AEM Sites, puede utilizar el componente Contenedor de formulario adaptable.

Puede utilizar el Editor de reglas para añadir o controlar el comportamiento dinámico de los componentes del formulario adaptable. Por ejemplo, ocultar o mostrar un componente. El Editor de reglas no está disponible para los componentes de formularios no adaptables. Por lo tanto, utilice la diligencia mientras utiliza componentes de formulario no adaptable en el componente de Contenedor de AEM Forms.

## Creación de un formulario adaptable mediante el componente Contenedor de formularios adaptables {#af-container-component}

El componente de [!UICONTROL Contenedor de formulario adaptable] permite crear experiencias de inscripción digital mediante los componentes de formularios adaptables en el editor de AEM Sites. Puede crear un formulario adaptable arrastrando y soltando los componentes del formulario.

### Requisitos previos {#prerequisites-af-container}

+++ Habilitar componente de **[!UICONTROL Contenedor de Formularios adaptables]**.

Para habilitar el [!UICONTROL Contenedor de formularios adaptables] en la política de la plantilla, siga los siguientes pasos:

1. Vaya a la [!UICONTROL Información de la página] > [!UICONTROL Editar plantilla]
1. Haga clic en [!UICONTROL Política] y seleccione la casilla de verificación **[!UICONTROL Contenedor de Formularios adaptables]** en **[Nombre de proyecto de tipo de archivo de AEM] - Formulario adaptable**.
1. Haga clic en **[!UICONTROL Listo]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++

+++ Incluir bibliotecas de cliente de Formularios adaptables en la página de AEM Sites

Para utilizar componentes de formularios adaptables en una página de AEM Sites, incluya las bibliotecas de cliente Customheaderlibs y Customfooterlibs en la página de AEM Sites mediante el Repositorio de Arquetipo/Git de AEM y la canalización de implementación.

1. Abra su proyecto de [Arquetipo de AEM Forms o repositorio de Git clonado](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es) en un editor de texto. Por ejemplo, código de Visual Studio.
1. Navegue hasta `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`.
1. Copiar el valor de `sling:resourceSuperType`. Por ejemplo, el valor es `core/wcm/components/page/v3/page`.

   ![recurso de sling](/help/forms/assets/slingresource.png)

1. Crear una estructura similar en la ubicación `ui.apps/src/main/content/jcr_root/apps` igual que `core/wcm/components/page/v3/page`.

   ![estructura de superposición](/help/forms/assets/overlaystructure.png)

1. Agregar archivos `customheaderlibs.html` y `customfooterlibs.html`.

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

1. [Ejecución de la canalización](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html?lang=es) para implementar los cambios.

+++

### Creación de un formulario adaptable mediante el componente Contenedor de formularios adaptables {#create-af-using-af-container}


Para crear un formulario adaptable mediante el componente [!UICONTROL Contenedor de formularios adaptables]:

1. Abra la página de AEM Sites en el modo de edición.
1. En el panel Explorador de componentes, arrastre y coloque el componente **[!UICONTROL Contenedor de formularios adaptables]** en la página.
1. Cree un formulario adaptable utilizando los componentes de los formularios adaptables.
1. Guarde la configuración.

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

Su formulario está listo. Cuando publica la página de AEM Sites, publica automáticamente un formulario adaptable y sus archivos de referencia asociados.

#### Configurar las propiedades del Contenedor de formularios adaptables {#configure-additional-settings-container}

Puede personalizar la configuración avanzada del componente de [!UICONTROL Contenedor de formulario adaptable]. Por ejemplo,

* Por ejemplo, puede configurar el servicio de relleno previo para cargar un formulario adaptable con valores precargados en la página de un sitio.
* La configuración del modelo de datos se configura para asociar el formulario adaptable a una fuente de datos.
* Puede configurar las acciones de envío para enviar los datos en Microsoft® OneDrive, Microsoft® OneDrive u otras fuentes de datos al enviar un formulario. También puede crear y seleccionar una acción de envío personalizada para su formulario adaptable.

Para establecer las propiedades del componente **[!UICONTROL Contenedor de formularios adaptables]**, haga clic en el ![settings_icon](/help/forms/assets/Smock_Wrench_18_N.svg) en la barra de acciones. Se abre el cuadro de diálogo **[!UICONTROL Editar contenedor de AEM Forms]**.

![Cuadro de diálogo de edición](/help/forms/assets/adaptiveformcontainer-editdialog.png)

En el cuadro de diálogo [!UICONTROL Editar contenedor de AEM Forms], especifique lo siguiente.
* **Pestaña Básicos**
   * **Servicio de rellenado automático**: puede utilizar el servicio de cumplimentación previa para rellenar automáticamente los campos de un formulario adaptable utilizando los datos existentes. Cuando un usuario abre un formulario, los valores de esos campos ya han sido rellenados. Para obtener información sobre el servicio de rellenado automático, consulte [Rellenar previamente los campos del formulario adaptable](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/prepopulate-adaptive-form-fields.html?lang=es#configuring-prefill-service-using-configuration-manager)
   * **Categoría de la biblioteca del cliente**: especifique las [Funciones de JavaScript](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=es#custom-functions) que se utilizan en expresiones y son compatibles con Adaptive Forms.
* **Modelo de datos**: un modelo de datos de formulario permite integrar entidades y servicios de distintas fuentes de datos en un formulario adaptable. Elija un **[!UICONTROL modelo de datos de formulario]** si el formulario adaptable que está creando implica recuperar y escribir datos desde y hacia varias fuentes de datos.
   * **Modelo de datos de formulario**: un modelo de datos de formulario permite que un formulario adaptable se comunique con distintas fuentes de datos. Para obtener información sobre la configuración de una fuente de datos, consulte [Configurar fuentes de datos](/help/forms/configure-data-sources.md).
   * **Esquema**: el esquema representa la estructura en la que el sistema back-end de su organización produce o consume datos. Puede [asociar el esquema a un formulario adaptable](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/adaptive-form-json-schema-form-model.html?lang=es) y utilizar sus elementos para agregar contenido dinámico a un formulario adaptable.

     >[!NOTE]
     >
     > Después de configurar el modelo de datos de formulario, no se puede cambiar el modelo de formulario asociado. Sin embargo, es posible modificar el esquema asociado al modelo de datos de formulario.

* **Pestaña Envío**

   * **Redirigir a URL**
      * **URL/ruta de redireccionamiento**: especifica la dirección URL o la ruta a la que se redirige un formulario adaptable después de la acción de envío.

      * **Acción de envío**: se activa una acción de envío cuando un usuario hace clic en el botón Enviar en un formulario adaptable. Puede [configurar la acción de envío en el formulario adaptable](/help/forms/configuring-submit-actions.md). Los formularios adaptables proporcionan algunas acciones de envío listas para usar:
         * Enviar al punto final REST
         * Enviar correo electrónico
         * Enviar mediante modelo de datos de formulario
         * Invocar un flujo de trabajo de AEM
         * Enviar a SharePoint
         * Enviar a OneDrive
         * Enviar a Azure Blob Storage

  También puede [ampliar las acciones de envío predeterminadas](custom-submit-action-form.md) para crear su propia acción de envío personalizada.

* **Mostrar mensaje**
   * **Mensaje de contenido**: escriba un mensaje con el editor de texto enriquecido para mostrarlo al enviar el formulario. Esta opción solo está disponible cuando elige mostrar un mensaje de agradecimiento.

## Incrustar un formulario adaptable  {#aem-container-component}

Si usa el componente de **[!UICONTROL Formularios adaptables: incrustar (V2)]**, puede incrustar un nuevo formulario adaptable o incrustar un formulario adaptable existente en la página del sitio. El [!UICONTROL Forms adaptable: incrustado (v2)] Este componente le permite:

* [Agregar un formulario adaptable existente](#embed-new-af)

* [Crear y agregar un nuevo formulario adaptable](#embed-existing-af)

### Requisitos previos {#prerequisites}

+++ Habilite el componente de **Formularios adaptables: incrustado**.

Para habilitar el componente de [!UICONTROL Formularios adaptables: incrustar(v2)] en la política de la plantilla, siga los siguientes pasos:

1. Vaya a la [!UICONTROL Información de la página] > [!UICONTROL Editar plantilla]

1. Haga clic en [!UICONTROL Política] y seleccione la casilla de verificación **[!UICONTROL Formulario adaptable: incrustado (v2)]** en el grupo **[!UICONTROL [Nombre de proyecto de tipo de archivo de AEM] - Formularios]**.
1. Haga clic en **[!UICONTROL Listo]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419369?quality=12&learn=on)

+++

+++ Incluir bibliotecas de cliente de Formularios adaptables en la página de AEM Sites

Cuando la opción **[!UICONTROL Cuando el formulario abarca toda la anchura de una página]** está seleccionada en los **[!UICONTROL Contenedores de formulario]** configure el cuadro de diálogo y use los **Formularios adaptables con componentes principales**, es necesario incluir los clientlibs en la página del sitio correspondiente.

![Superposición de Gif](/help/forms/assets/overlaycorecomponent.gif)

Para utilizar componentes de formularios adaptables en una página de AEM Sites, incluya las bibliotecas de cliente `Customheaderlibs` y `Customfooterlibs` en la página de AEM Sites mediante el Repositorio de Arquetipo/Git de AEM y la canalización de implementación.

1. Abra su proyecto de [Arquetipo de AEM Forms o repositorio de Git clonado](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es) en un editor de texto. Por ejemplo, código de Visual Studio.
1. Navegue hasta `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`.
1. Copiar el valor de `sling:resourceSuperType`. Por ejemplo, el valor es `core/wcm/components/page/v3/page`.

   ![recurso de sling](/help/forms/assets/slingresource.png)

1. Crear una estructura similar en la ubicación `ui.apps/src/main/content/jcr_root/apps` igual que `core/wcm/components/page/v3/page`.

   ![estructura de superposición](/help/forms/assets/overlaystructure.png)

1. Agregar archivos `customheaderlibs.html` y `customfooterlibs.html`.

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

   El `customfooterlibs.html` se utiliza para JavaScript y el `customheaderlibs.html` para CSS.

1. [Ejecución de la canalización](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html?lang=es) para implementar los cambios.

+++

### Agregar un formulario adaptable existente a la página de AEM Sites {#embed-existing-af}

1. Abra la página de AEM Sites en el modo de edición.
1. Desde el panel del explorador de componentes, arrastre y suelte el componente [!UICONTROL Formularios adaptables: incrustar] en la página.
1. Pulse el componente [!UICONTROL Formularios adaptables: incrustar] en la página de Sites y, a continuación, pulse en ![settings_icon](/help/forms/assets/Smock_Wrench_18_N.svg) en la barra de acciones. Se abrirá el cuadro de diálogo de **[!UICONTROL Editar formularios adaptables: incrustar]**.
1. Busque y seleccione el formulario adaptable para incrustarlo en la [!UICONTROL Ruta de recursos].
1. Guarde la configuración. El formulario adaptable está ahora incrustado en la página.

>[!VIDEO](https://video.tv.adobe.com/v/3419368?quality=12&learn=on)



### Crear y agregar un nuevo formulario adaptable a la página de AEM Sites {#embed-new-af}

1. Abra la página de AEM Sites en el modo de edición.
1. En el panel Explorador de componentes, arrastre y coloque el componente [!UICONTROL Formularios adaptables: incrustar(v2)] en la página.
1. Haga clic en el icono **Más** y se le redirigirá al asistente de creación de formularios.

   ![Formularios adaptables: componente incrustado](/help/forms/assets/aemformcontainer.png)

1. Cree un nuevo formulario adaptable desde el asistente de [!UICONTROL Creación de formularios].
1. La variable [!UICONTROL Ruta de recursos] ya incluye la ruta de un formulario adaptable creado
1. Guarde la configuración. El formulario adaptable está ahora incrustado en la página.

>[!VIDEO](https://video.tv.adobe.com/v/3419366/adaptive-form-aem-forms?quality=12&learn=on)

#### Configurar el formulario adaptable: incrustar(v2) propiedades {#configure-adaptive-form-embed}

Puede personalizar la configuración avanzada del componente [!UICONTROL Formulario adaptable: incrustar(v2)]. En el cuadro de diálogo [!UICONTROL Editar formularios adaptables: incrustar(v2)], puede especificar lo siguiente.

* **Ruta del recurso**: examine y seleccione el formulario adaptable que desea incrustar. Se rellena automáticamente si ha colocado el formulario desde el Explorador de recursos.
* **Después del envío**: seleccione la acción que debe activarse después del envío del formulario. Puede elegir mostrar un mensaje o una página de agradecimiento.
   * **Mostrar mensaje de agradecimiento**: escriba un mensaje usando el editor de texto enriquecido para mostrar en el envío del formulario. Esta opción solo está disponible cuando elige mostrar un mensaje de agradecimiento.
   * **Página de agradecimiento**: examine y seleccione la página que desea mostrar después al enviar el formulario. Esta opción solo está disponible cuando elige mostrar una página de agradecimiento.
   * **Redirigir a la página de agradecimiento**: active la opción para reemplazar la página que contiene el formulario adaptable incrustado por una página de agradecimiento. De lo contrario, la página de agradecimiento reemplaza al formulario adaptable en el componente de [!UICONTROL Formularios adaptables: incrustar] sin actualizar la página de Sites subyacente. Esta opción solo está disponible cuando elige mostrar una página de agradecimiento.
* **Usar el idioma de la página**: utilice la configuración local de la página de AEM Sites en lugar de la configuración regional del formulario adaptable.
* **Definir el enfoque del formulario**: seleccione esta opción para establecer el enfoque en el primer campo del formulario adaptable.
* **El formulario abarca la anchura completa del fotograma**: si se activa, iframe no se utiliza para procesar el formulario.
* **Altura**: especifique la altura del contenedor. Déjelo en blanco para cambiar automáticamente el tamaño del contenedor.
* **Biblioteca de cliente CSS**: especifique la ruta a una biblioteca de cliente CSS.

### Publicar Formularios adaptables agregados mediante el componente Formulario adaptable - Incrustar(v2)  {#publish-embedded-adaptive-form}

Considere los siguientes escenarios para publicar Formularios adaptables agregados usando el componente **[!UICONTROL Formulario adaptable: incrustado(v2)]**:

* Cuando publica una página de AEM Sites por primera vez, los formularios agregados a la página de Sites se publican automáticamente.
* Cuando modifique un formulario adaptable agregado a una página de Sites ya publicada, publique manualmente los Formularios adaptables correspondientes.
* Cuando modifique una página de Sites y los Formularios adaptables correspondientes, vuelva a publicar la página de Sites y todos los Formularios adaptables agregados a la página de Sites.

### Modificación de Formularios adaptables agregados mediante el componente Formulario adaptable - Incrustar (v2)  {#modifying-embedded-adaptive-form}

Para modificar cualquier configuración o propiedad de un formulario adaptable, realice una de las siguientes acciones:

* Abra el formulario original en Formularios adaptables en los respectivos editores y modifíquelo.
* Pulse el formulario adaptable desde la página de Sites en el modo Edición y, a continuación, pulse **[!UICONTROL Editar en una nueva ventana]**. El formulario original se abrirá en el modo Edición, en el cual puede modificarlo.

## Cambiar el diseño de un formulario adaptable agregado a una página de AEM Sites {#change-layout-af-aem-sites-page}

En la página de AEM Sites, el [Modo Diseño](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/features/responsive-layout.html?lang=es#defining-layouts-layout-mode) permite cambiar el tamaño de un formulario adaptable que se crea o agrega a una página de AEM Sites.

![Soporte de diseño AF](/help/forms/assets/afsite-layoutsupport.gif)

La página de AEM Sites mantiene una referencia al formulario adaptable. Cuando se traduce una página de AEM Sites, se traduce automáticamente un formulario adaptable y sus recursos de referencia asociados mediante la variable [proyectos de traducción](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/reusing-content/translation/managing-projects.html?lang=es#adding-pages-assets-to-a-translation-job) en otros idiomas.

## Prácticas recomendadas {#best-practices}

* El encabezado y el pie de página del formulario original no se incluyen en el formulario incrustado.
* Los borradores de los usuarios y los envíos de formularios incrustados son compatibles y visibles en las pestañas Borradores y Formularios enviados del portal de Formularios.