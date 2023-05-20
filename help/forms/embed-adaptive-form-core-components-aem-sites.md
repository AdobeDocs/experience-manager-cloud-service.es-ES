---
title: Agregar o crear un formulario adaptable (componentes principales) en la página de AEM Sites
seo-title: How to add or create an Adaptive Form (Core Components) to an AEM Sites page?
description: Puede utilizar el formulario adaptable (componentes principales) en una página de AEM Sites para rellenar y enviar un formulario sin salir de las páginas de AEM Sites.
feature: Adaptive Forms
hide: true
hidefromtoc: true
exl-id: 1046231f-787c-4e49-9ba0-e7dd59e41bce
source-git-commit: 1d5641dd07cc68dade247fe30bb57663872e5560
workflow-type: tm+mt
source-wordcount: '2135'
ht-degree: 15%

---

# Crear o agregar un formulario adaptable mediante el Editor de AEM Sites {#add-an-adaptive-form-to-aem-sites-page}

Puede crear o incrustar fácilmente Forms adaptable en una página de AEM Sites para permitir a los usuarios rellenar y enviar un formulario sin salir de la página de Sites. Esto permite al usuario mantenerse en el contexto de otros elementos de la página web e interactuar simultáneamente con el formulario.

Puede elegir uno de los siguientes métodos para crear o agregar un formulario adaptable a una página de AEM Sites:

* **Crear un formulario adaptable mediante el componente Contenedor de Forms adaptable**: La [Contenedor de formulario adaptable](#af-container-component) Este componente le permite crear experiencias de inscripción digitales utilizando componentes de Forms adaptables directamente en el editor de AEM Sites. Esta integración ofrece una experiencia perfecta para los autores de AEM Sites que deseen crear y administrar formularios en sus páginas de AEM Sites.

* **Agregar un formulario adaptable existente**: La [Forms adaptable: incrustado (v2)](#embed-existing-af) Este componente le permite agregar fácilmente un formulario adaptable preexistente a una página dentro de AEM Sites. Esta función mejora la adaptabilidad y reutilización de Adaptive Forms. Esta integración proporciona una forma cómoda para que los clientes reutilicen el Forms adaptable que ya han creado.

* **Uso del Asistente para Forms adaptable para crear un formulario**: utilice el [Forms adaptable: incrustado (v2)](#embed-new-af) para crear un formulario adaptable desde el editor de AEM Sites con el asistente para la creación de formularios. El formulario se guarda como una entidad externa. Puede reutilizar este formulario en otras páginas de Sites y también en formularios independientes.

* **Añadir varios Forms adaptables en una página de AEM Sites**: para añadir varios Forms adaptables en una página de AEM Sites, utilice los componentes de contenedor de AEM Forms: [Forms adaptable: incrustado (v2)](#embed-new-af) y [Contenedor de formulario adaptable](#af-container-component). En caso de que necesite agregar más de un formulario adaptable como div dentro de una página de AEM Sites, puede utilizar el componente Contenedor de formulario adaptable.

Puede utilizar el Editor de reglas para agregar o controlar el comportamiento dinámico de los componentes de un formulario adaptable. Por ejemplo, ocultar o mostrar un componente. El Editor de reglas no está disponible para componentes de formularios no adaptables. Por lo tanto, aplique su diligencia mientras utiliza componentes de formulario no adaptables en el componente Contenedor de AEM Forms.

## Crear un formulario adaptable mediante el componente Contenedor de Forms adaptable {#af-container-component}

El [!UICONTROL Contenedor de formulario adaptable] Este componente permite crear experiencias de inscripción digitales utilizando componentes de Forms adaptable en el editor de AEM Sites. Puede crear un formulario adaptable arrastrando y soltando los componentes del formulario.

### Requisitos previos {#prerequisites-af-container}

+++ Activar **[!UICONTROL Contenedor de Forms adaptable]** componente.

Para habilitar [!UICONTROL Contenedor de Forms adaptable] en la directiva de la plantilla, realice los siguientes pasos:

1. Vaya a la [!UICONTROL Información de página] > [!UICONTROL Editar plantilla]
1. Haga clic en [!UICONTROL Política] y seleccione la **[!UICONTROL Contenedor de Forms adaptable]**  en la casilla de verificación **[AEM Nombre de proyecto de tipo de archivo] - Formulario adaptable**.
1. Haga clic en **[!UICONTROL Listo]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++

+++ Incluir bibliotecas de cliente de Forms adaptables en la página de AEM Sites

Para utilizar componentes de Forms adaptables en una página de AEM Sites, incluya las bibliotecas de cliente Customheaderlibs y Customfooterlibs en la página de AEM Sites AEM mediante el Repositorio de tipo de archivo/Git y la canalización de implementación de.

1. Abra su [Arquetipo de AEM Forms o repositorio Git clonado](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es) proyecto en un editor de texto. Por ejemplo, Visual Studio Code.
1. Navegue hasta `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`.
1. Copie el valor de `sling:resourceSuperType`. Por ejemplo, el valor es `core/wcm/components/page/v3/page`.

   ![recurso de sling](/help/forms/assets/slingresource.png)

1. Cree la estructura similar en la ubicación `ui.apps/src/main/content/jcr_root/apps` igual que `core/wcm/components/page/v3/page`.

   ![estructura de superposición](/help/forms/assets/overlaystructure.png)

1. Añadir `customheaderlibs.html` y `customfooterlibs.html` archivos.

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

   customfoterlibs.html se utiliza para JavaScript y customheaderlibs.html para css.

1. [Ejecutar la canalización](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) para implementar los cambios.

+++

### Crear un formulario adaptable mediante el componente Contenedor de Forms adaptable {#create-af-using-af-container}


Para crear un formulario adaptable con [!UICONTROL Contenedor de Forms adaptable] componente:

1. Abra la página de AEM Sites en modo de edición.
1. En el panel Explorador de componentes, arrastre y suelte el **[!UICONTROL Contenedor de Forms adaptable]** en la página.
1. Crear un formulario adaptable mediante los componentes de Forms adaptable.
1. Guarde la configuración.

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

Su formulario está listo. Cuando publica la página de AEM Sites, publica automáticamente el formulario adaptable y sus recursos de referencia asociados.

#### Configurar propiedades del contenedor del formulario adaptable {#configure-additional-settings-container}

Puede personalizar la configuración avanzada del [!UICONTROL Contenedor de formulario adaptable] componente. Por ejemplo,

* Puede configurar el servicio de rellenado previo para cargar un formulario adaptable con valores rellenados previamente en la página de un sitio.
* Puede configurar los ajustes del modelo de datos para asociar el formulario adaptable con una fuente de datos.
* Puede configurar las acciones de envío para enviar los datos en Microsoft® OneDrive, Microsoft® OneDrive u otras fuentes de datos al enviar un formulario. También puede crear y seleccionar una acción de envío personalizada para su Forms adaptable.

Para establecer las propiedades de **[!UICONTROL Contenedor de Forms adaptable]** haga clic en el componente ![settings_icon](/help/forms/assets/Smock_Wrench_18_N.svg) en la barra de acciones. El **[!UICONTROL Editar contenedor de Forms adaptable]** se abre.

![Cuadro de diálogo de edición](/help/forms/assets/adaptiveformcontainer-editdialog.png)

En el [!UICONTROL Editar contenedor de Forms adaptable] , puede especificar lo siguiente.
* **Pestaña Básicos**
   * **Servicio de prerrellenar**: Puede utilizar el servicio de rellenado previo para rellenar automáticamente los campos de un formulario adaptable mediante los datos existentes. Cuando un usuario abre un formulario, los valores de esos campos ya han sido rellenados. Para obtener información sobre el servicio de relleno previo, consulte [Rellenar previamente campos de formulario adaptable](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/prepopulate-adaptive-form-fields.html#configuring-prefill-service-using-configuration-manager)
   * **Categoría de biblioteca de cliente**: especifique el [Funciones de JavaScript](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=en#custom-functions) que se utilizan en expresiones y que son compatibles con el Forms adaptable.
* **Modelo de datos**: Un modelo de datos permite integrar entidades y servicios de distintas fuentes de datos en un formulario adaptable. Elegir **[!UICONTROL Modelo de datos de formulario]** si el formulario adaptable que está creando implica recuperar y escribir datos desde y hacia varias fuentes de datos.
   * **Modelo de datos de formulario**: Un modelo de datos de formulario permite que un formulario adaptable se comunique con fuentes de datos diferentes. Para obtener información sobre la configuración de una fuente de datos, consulte [Configure las fuentes de datos.](/help/forms/configure-data-sources.md)
   * **Esquema**: el esquema representa la estructura en la que el sistema back-end de su organización produce o consume datos. Puede [asociar el esquema a un formulario adaptable](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/adaptive-form-json-schema-form-model.html) y utilizar sus elementos para agregar contenido dinámico a un formulario adaptable.

      >[!NOTE]
      >
      > Después de configurar el modelo de datos de formulario, no se puede cambiar el modelo de formulario asociado. Sin embargo, es posible modificar el esquema asociado al modelo de datos de formulario.

* **Pestaña Envío**

   * **Redirigir a URL**
      * **URL/ruta de redireccionamiento**: Especifica la dirección URL o la ruta a la que se redirige un formulario adaptable después del envío.

      * **Acción de envío**: se activa una acción de envío cuando un usuario hace clic en el botón Enviar en un formulario adaptable. Puede [configurar la acción de envío en el formulario adaptable](/help/forms/configuring-submit-actions.md). Los formularios adaptables proporcionan las siguientes acciones de envío listas para usar:
         * Enviar al punto final REST
         * Enviar correo electrónico
         * Enviar mediante modelo de datos de formulario
         * Invocar un flujo de trabajo de AEM
         * Enviar a SharePoint
         * Enviar a OneDrive
         * Enviar a Azure Blob Storage

   También puede [ampliar las acciones de envío predeterminadas](custom-submit-action-form.md) para crear su propia acción de envío personalizada.

* **Mostrar mensaje**
   * **Contenido del mensaje**: escriba un mensaje con el editor de texto enriquecido para mostrarlo después del envío del formulario. Esta opción solo está disponible cuando elige mostrar un mensaje de agradecimiento.

## Incrustar un formulario adaptable  {#aem-container-component}

Uso de **[!UICONTROL Forms adaptable: incrustado (V2)]** puede incrustar un formulario adaptable nuevo o incrustar uno existente en la página del sitio. El [!UICONTROL Forms adaptable: incrustado (v2)] Este componente le permite:

* [Agregar un formulario adaptable existente](#embed-new-af)

* [Crear y agregar un nuevo formulario adaptable](#embed-existing-af)

### Requisitos previos {#prerequisites}

+++ Habilite la **Forms adaptable: incrustado** componente.

Para habilitar [!UICONTROL Forms adaptable: incrustado (v2)] en la directiva de la plantilla, realice los siguientes pasos:

1. Vaya a la [!UICONTROL Información de página] > [!UICONTROL Editar plantilla]

1. Haga clic en [!UICONTROL Política] y seleccione la **[!UICONTROL Formulario adaptable: incrustado (v2)]** en la casilla de verificación **[!UICONTROL [AEM Nombre de proyecto de tipo de archivo] - FORMS]** grupo .
1. Haga clic en **[!UICONTROL Listo]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419369?quality=12&learn=on)

+++

+++ Incluir bibliotecas de cliente de Forms adaptables en la página de AEM Sites

Si la variable **[!UICONTROL Cuando el formulario abarca el ancho completo de una página]** está seleccionada en la **[!UICONTROL Contenedores de formulario]** cuadro de diálogo de configuración y **Forms adaptable con componentes principales** , es necesario incluir los clientlibs en la página de su sitio correspondiente.

![GIF superpuesto](/help/forms/assets/overlaycorecomponent.gif)

Para utilizar componentes de Forms adaptable en una página de AEM Sites, incluya la variable `Customheaderlibs` y `Customfooterlibs` Las bibliotecas de cliente se transfieren a la página de AEM Sites AEM mediante el repositorio de tipo de archivo/Git de y la canalización de implementación.

1. Abra su [Arquetipo de AEM Forms o repositorio Git clonado](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es) proyecto en un editor de texto. Por ejemplo, Visual Studio Code.
1. Navegue hasta `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`.
1. Copie el valor de `sling:resourceSuperType`. Por ejemplo, el valor es `core/wcm/components/page/v3/page`.

   ![recurso de sling](/help/forms/assets/slingresource.png)

1. Cree la estructura similar en la ubicación `ui.apps/src/main/content/jcr_root/apps` igual que `core/wcm/components/page/v3/page`.

   ![estructura de superposición](/help/forms/assets/overlaystructure.png)

1. Añadir `customheaderlibs.html` y `customfooterlibs.html` archivos.

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

   El `customfooterlibs.html` se utiliza para JavaScript y `customheaderlibs.html` para CSS.

1. [Ejecutar la canalización](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) para implementar los cambios.

+++

### Agregar un formulario adaptable existente a la página de AEM Sites {#embed-existing-af}

1. Abra la página de AEM Sites en modo de edición.
1. En el panel Explorador de componentes, arrastre y suelte el [!UICONTROL Forms adaptable: incrustado] en la página.
1. Pulse el botón [!UICONTROL Forms adaptable: incrustado] en la página sitios y pulse ![settings_icon](/help/forms/assets/Smock_Wrench_18_N.svg) en la barra de acciones. El **[!UICONTROL Editar Forms adaptable: incrustar]** se abre.
1. Busque y seleccione el formulario adaptable que desea incrustar en la [!UICONTROL Ruta de recursos].
1. Guarde la configuración. El formulario adaptable está ahora incrustado en la página.

>[!VIDEO](https://video.tv.adobe.com/v/3419368?quality=12&learn=on)



### Crear y agregar un nuevo formulario adaptable a la página de AEM Sites {#embed-new-af}

1. Abra la página de AEM Sites en modo de edición.
1. En el panel Explorador de componentes, arrastre y suelte el [!UICONTROL Forms adaptable: incrustado (v2)] en la página.
1. Haga clic en **Plus** y se le redirigirá al asistente para la creación de formularios.

   ![Forms adaptable: componente incrustado](/help/forms/assets/aemformcontainer.png)

1. Cree un nuevo formulario adaptable a partir de [!UICONTROL Creación de formularios] asistente.
1. El [!UICONTROL Ruta de recursos] ya incluye la ruta de un formulario adaptable creado
1. Guarde la configuración. El formulario adaptable está ahora incrustado en la página.

>[!VIDEO](https://video.tv.adobe.com/v/3419366/adaptive-form-aem-forms?quality=12&learn=on)

#### Configurar formulario adaptable - Propiedades de incrustación (v2) {#configure-adaptive-form-embed}

Puede personalizar la configuración avanzada del [!UICONTROL Formulario adaptable: incrustado (v2)] componente. En el [!UICONTROL Editar Forms adaptable: incrustado (v2)] , puede especificar lo siguiente.

* **Ruta del recurso**: examine y seleccione el formulario adaptable que desea incrustar. Se rellena automáticamente si ha colocado el formulario desde el Explorador de recursos.
* **Después del envío**: seleccione la acción que debe activarse después del envío del formulario. Puede elegir mostrar un mensaje o una página de agradecimiento.
   * **Mostrar mensaje de agradecimiento**: escriba un mensaje con el editor de texto enriquecido para mostrarlo después del envío del formulario. Esta opción solo está disponible cuando elige mostrar un mensaje de agradecimiento.
   * **Mostrar página de agradecimiento**: examine y seleccione la página que desea mostrar al enviar el formulario. Esta opción solo está disponible cuando elige mostrar una página de agradecimiento.
   * **Redirigir a la página de agradecimiento**: active la opción para reemplazar la página que contiene el formulario adaptable incrustado por una página de agradecimiento. De lo contrario, la página de agradecimiento reemplazará al formulario adaptable en el [!UICONTROL Forms adaptable: incrustado] componente, sin actualizar los sitios subyacentes de la página. Esta opción solo está disponible cuando elige mostrar una página de agradecimiento.
* **Usar el idioma de la página**: utilice la configuración local de la página de AEM Sites en lugar de la configuración regional del formulario adaptable.
* **Definir el enfoque del formulario**: seleccione esta opción para establecer el enfoque en el primer campo del formulario adaptable.
* **El formulario abarca toda la anchura del marco**: Si se selecciona, iframe no se utiliza para procesar el formulario.
* **Altura**: especifique la altura del contenedor. Déjelo en blanco para cambiar automáticamente el tamaño del contenedor.
* **Biblioteca de cliente CSS**: especifique la ruta a una biblioteca de cliente CSS.

### Publicar Forms adaptable agregado mediante el componente Formulario adaptable - Incrustar (v2)  {#publish-embedded-adaptive-form}

Considere los siguientes escenarios para publicar Forms adaptable agregado usando **[!UICONTROL Formulario adaptable: incrustado (v2)]** componente:

* Cuando publica una página de AEM Sites por primera vez, los formularios agregados a la página de Sites se publican automáticamente.
* Cuando modifique un formulario adaptable agregado a una página de Sites ya publicada, publique manualmente el Forms adaptable correspondiente.
* Cuando modifique una página de Sites y el Forms adaptable correspondiente, vuelva a publicar la página de Sites y todo el Forms adaptable agregado a la página de Sites.

### Modificación de un Forms adaptable agregado mediante el componente Formulario adaptable - Incrustar (v2)  {#modifying-embedded-adaptive-form}

Para modificar cualquier configuración o propiedad de un formulario adaptable, realice una de las siguientes acciones:

* Abra el formulario original en un formulario adaptable en el editor correspondiente y modifíquelo.
* Pulse el formulario adaptable desde la página de Sites en el modo Edición y, a continuación, pulse **[!UICONTROL Editar en una nueva ventana]**. El formulario original se abrirá en el modo Edición, en el cual puede modificarlo.

## Cambiar el diseño de un formulario adaptable agregado a una página de AEM Sites {#change-layout-af-aem-sites-page}

En la página de AEM Sites, la variable [Modo Diseño](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/features/responsive-layout.html?#defining-layouts-layout-mode) permite cambiar el tamaño de un formulario adaptable que se crea o agrega a una página de AEM Sites.

![AF-layout-support](/help/forms/assets/afsite-layoutsupport.gif)

AEM La página de Sites de mantiene una referencia al formulario adaptable. Al traducir una página de AEM Sites, traduce automáticamente un formulario adaptable y sus recursos de referencia asociados utilizando [proyectos de traducción](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/reusing-content/translation/managing-projects.html?lang=en#adding-pages-assets-to-a-translation-job) a otros idiomas.

## Prácticas recomendadas {#best-practices}

* El encabezado y el pie de página del formulario original no se incluyen en el formulario incrustado.
* Los borradores de los usuarios y los envíos de formularios incrustados son compatibles y visibles en las pestañas Borradores y Forms enviados del portal de Forms.