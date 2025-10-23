---
title: Agregar un formulario adaptable a una página de AEM Sites
description: Puede incrustar formularios adaptables en una página de AEM Sites o en una página web alojada fuera de AEM.
feature: Adaptive Forms
role: Admin, User, Developer
Keywords: Forms AEM Sites, Embed Form to a Sites page, Adaptive Forms AEM Sites, Embed Adaptive Forms to AEM Page, Embed Forms in an AEM Sites page
exl-id: 359b05e8-d8c1-4a77-9e70-6f6b6e668560
source-git-commit: 958c166585ac7eeb667d73744403558b2dc5ce94
workflow-type: tm+mt
source-wordcount: '3323'
ht-degree: 96%

---

# Incrustar un formulario adaptable en una página de AEM Sites {#embed-an-adaptive-form-to-aem-sites-page}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/embed-adaptive-form-aem-sites.html?lang=es) |
| AEM as a Cloud Service | Este artículo |


## Información general {#overview}

AEM Forms permite a los desarrolladores de formularios incrustar sin problemas formularios adaptables en una página de AEM Sites o en una página web hospedada fuera de AEM. El formulario adaptable incrustado es completamente funcional, y los usuarios pueden rellenarlo y enviarlo sin abandonar la página. Esto permite al usuario a mantenerse en el contexto de otros elementos de la página web e interactuar simultáneamente con el formulario. Esto permite a los visitantes rellenar y enviar formularios cómodamente sin salir de la página en la que se encuentran. Esta integración proporciona una forma cómoda para que los clientes puedan reutilizar los formularios adaptables que ya han creado.

Puede utilizar el Editor de páginas de AEM para incrustar rápidamente varios formularios a las páginas de AEM Sites. El uso del Editor de páginas de AEM permite a los autores de contenido crear experiencias de captura de datos sin problemas dentro de una página de Sites mediante la potencia de los componentes de los formularios adaptables, incluido el comportamiento dinámico, las validaciones, la integración de datos, la generación de documentos de registro y la automatización de procesos empresariales. También le permite utilizar varias funciones de las páginas de AEM Sites, como versiones, segmentación, traducción y administrador de varios sitios.

AEM Forms proporciona el **[!UICONTROL contenedor del formulario adaptable]** y los componentes **[!UICONTROL Formularios adaptables – Incrustados (v2)]**. Puede utilizar el componente **[!UICONTROL Formularios adaptables: Incrustados (v2)]** para agregar un formulario adaptable existente o crear un formulario con el Editor de Formularios adaptables, y el **[!UICONTROL Contenedor de formulario adaptable]** para crear un nuevo formulario dentro de una página de Fragmento de experiencia o AEM Sites.

![Ejemplo de un formulario adaptable en una página de AEM Sites](/help/forms/assets/adaptive-form-in-sites-page.png)

<!-- For information about embedding an Adaptive Form in an external web page, see [Embed Adaptive Form in external web page](/help/forms/using/embed-adaptive-form-external-web-page.md). 

## Why embed an Adaptive Form in AEM Sites page or AEM Experience Fragment? 

Using **[!UICONTROL Adaptive Forms – Embed(v2)]** in AEM Page Editor lets you create seamless data capture experiences within a Sites page using the power of Adaptive Forms components including dynamic behavior, validations, data integration, generate document of record and business process automation. It also lets you use various features of AEM Sites pages like, versioning, targeting, translation, and multi-site manager, enhancing the overall form creation and management experience. Let's explore some of these features:

* **Versioning:** AEM Sites pages offer [robust versioning capabilities](/help/sites-cloud/authoring/sites-console/page-versions.md), allowing you to track and manage different versions of your forms. This enables you to make changes and enhancements to forms while maintaining the ability to roll back to previous versions if needed. Versioning ensures a controlled and organized approach to form development and evolution.
* **Targeting (Integration with Adobe Target):** With AEM Sites pages targeting capabilities, you can also [personalize the form experience for different audiences](/help/sites-cloud/integrating/integrating-adobe-target.md). By using user segments and targeting criteria, you can tailor the form's content, design, or behavior to specific groups of users. This enables you to provide a personalized and relevant form experience, increasing engagement and conversion rates.
* **Translation:** AEM Sites [seamless integration with translation services](/help/sites-cloud/administering/translation/overview.md), allowing you to translate forms into multiple languages easily. This feature simplifies the localization process, ensuring that your forms are accessible to a global audience. You can manage translations efficiently within AEM translation projects, reducing time and effort required for multilingual form support. See considerations section for more information on translation.  
* **Multi-site Management and Live Copy:** AEM Sites provide robust [Multi-site Management and Live Copy capabilities](/help/sites-cloud/administering/msm/overview.md), enabling you to create and manage multiple websites within a single environment. This feature now lets you reuse forms across different sites, ensuring consistency and reducing duplication efforts. With centralized control and management, you can efficiently maintain and update forms across multiple websites.
* **Themes:** AEM Sites pages provide a framework for designing and maintaining consistent visual styles across multiple web pages. These define colors, fonts, style sheets, and other visual elements that contribute to the overall look and feel of the website. [You can use the themes designed for an AEM Sites page for an Adaptive Form, saving time and effort](/help/sites-cloud/administering/site-creation/site-themes.md#using-site-themes-using-themes). 
* **Tagging:** AEM Sites pages allow you to [assign tags or labels to a page, an asset, or other content](/help/implementing/developing/introduction/tagging-framework.md). Tags are keywords or metadata labels that provide a way to categorize and organize content based on specific criteria. You can assign one or more tags to pages, assets, or any other content items within AEM to improve search and categorize the assets. 
* **Locking and Unlocking content:** AEM Sites allow users to [control access and modifications to pages](/help/sites-cloud/authoring/page-editor/edit-content.md) within the AEM Sites environment. When a page is locked, it means that it is protected from unauthorized changes or edits by other users. Only the user who has locked the content or a designated administrator can unlock it to allow modifications. 

In addition, Adaptive Forms in AEM Page Editor use [Adaptive Forms Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es#features). These Core Components provide a standard and easier methods to style and customize the components, identical to [AEM Sites WCM Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es).

-->

## ¿Cómo se crea o se incrustar un formulario adaptable en una página de AEM Sites o en un fragmento de experiencia de AEM? {#various-options-to-create-or-embed-an-adaptive-form-in-aem-sites-page-or-aem-experience-fragment}

Puede aprovechar al máximo esta función utilizando las siguientes opciones:

* **[Crear un formulario adaptable con plantillas aprobadas e incrustarlo en una página de AEM Sites](#embed-form-using-adaptive-form-wizzard-aem-sites):** puede utilizar las plantillas aprobadas previamente para crear e incrustar rápidamente Formularios adaptables que se ajusten a las directrices de personalización de marca y los estándares de diseño de su organización.

* **[Incruste formularios existentes a una página de AEM Sites](#embed-an-adaptive-form-in-sites-editor):** puede integrar fácilmente formularios que ya haya creado en sus sitios web, lo que permite a los visitantes interactuar con ellos directamente.

* **[Convertir un formulario adaptable en fragmento de experiencia](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment):** convierta un formulario adaptable agregado a una página de AEM Sites en un fragmento de experiencia para reutilizar el formulario en varias páginas de AEM Sites.

* **[Crear y agregar un formulario adaptable personalizado a una página de AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md#create-an-adaptive-form-in-sites-editor-or-experience-fragment):**&#x200B;**[!UICONTROL puede utilizar el componente contenedor de formulario adaptable]** para crear un formulario completamente nuevo desde cero y adaptarlo específicamente a sus necesidades y preferencias de diseño.

* **[Crear y agregar un formulario adaptable personalizado a los fragmentos de experiencias](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md#create-an-adaptive-form-in-sites-editor):** puede ampliar el alcance de los formularios añadiéndolos a los fragmentos de experiencias de AEM, lo que permite una reutilización perfecta en varias páginas o sitios.

* **Agregar varios formularios a una página de AEM Sites o a un fragmento de experiencia:** puede crear o agregar varios formularios adaptables a una página AEM Sites para proporcionar varias opciones a los usuarios en función de sus preferencias y requisitos. Puede utilizar el Editor de páginas de AEM para incrustar rápidamente varios formularios a las páginas de AEM Sites. Puede usar el componente **[!UICONTROL Contenedor de formulario adaptable]** varias veces para añadir Formularios adaptables en una página de AEM Sites. Puede usar el componente **[!UICONTROL Formularios adaptables: incrustados]** varias veces en una página de AEM Sites, solo si se selecciona la opción **[!UICONTROL El formulario abarca toda la anchura del marco]**. En caso de que la opción **[!UICONTROL El formulario abarca toda la anchura del marco]** no esté activada, la página de AEM Sites solo admite que un formulario adaptable exista sin un iframe. Para agregar más Formularios adaptables con el componente **[!UICONTROL Formularios adaptables: incrustados]**, seleccione la opción **[!UICONTROL El formulario abarca toda la anchura del marco]**.

## Consideraciones para incrustar un formulario adaptable en una página de AEM Sites o un fragmento de experiencia de AEM {#consideration}

* Cuando se crea o se añade un formulario utilizando el componente **[!UICONTROL Formularios adaptables: Incrustados (v2)]**, los formularios pasan por un proceso de traducción y localización utilizando el flujo de traducción de AEM Forms. En este caso, se mantiene un único formulario y se hace referencia a él en todas las copias de idioma de las páginas de Sites. El componente **[!UICONTROL Formularios adaptables: Incrustados (v2)]** no proporciona acceso a varias funcionalidades de páginas de AEM Sites, como versiones, segmentación, traducción y administrador de varios sitios.

* Cuando se utiliza el **[!UICONTROL Contenedor de formularios adaptables]** para crear un formulario, los formularios pasan por un proceso de traducción y localización a través del flujo de traducción de AEM Sites. Para cada idioma, se genera una copia independiente (copia de idioma) de la página de Sites y de los formularios correspondientes y, cuando un autor de contenido modifica una regla en un formulario de la página principal, se deben realizar los mismos cambios en todas las copias de idioma del formulario. El **[!UICONTROL contenedor de formularios adaptables]** también permite utilizar varias funcionalidades de las páginas de AEM Sites, como versiones, segmentación, traducción y administrador de varios sitios.


## Consideraciones para incrustar un formulario adaptable en una página de AEM Sites o un fragmento de experiencia de AEM {#before-you-start-embedding-an-adaptive-form}

Antes de empezar a incrustar un nuevo formulario adaptable o un formulario adaptable preexistente mediante **[!UICONTROL Formularios adaptables: Incrustados (v2)]**, habilite **Componentes principales de Formularios adaptables** y agregue **Bibliotecas de cliente de Formularios adaptables** a su página de AEM Sites:

### Habilite los componentes principales de formularios adaptables para su entorno de Cloud Service de AEM

Instale la última versión para habilitar los componentes principales de formularios adaptables para su entorno de AEM as a Cloud Service.

### Añada bibliotecas de cliente de formularios adaptables a los componentes de la página de AEM Sites o de fragmentos de experiencia

Cuando la opción **[!UICONTROL Cuando el formulario abarca toda la anchura de una página]** está seleccionada en el cuadro de diálogo de configuración de **[!UICONTROL Contenedores de formulario]** y se utilizan los Formularios adaptables con componentes principales, es necesario incluir las bibliotecas de cliente en la página del sitio correspondiente.

![Cuando se selecciona la opción Formulario abarca todo el ancho de una página, y se utiliza un formulario adaptable con componentes principales](/help/forms/assets/overlaycorecomponent.gif)

**Caso 1: usar componentes de página de sitios independientes**

Añada las bibliotecas de cliente **Customheaderlibs** y **Customfoterlibs** a la página de AEM Sites mediante la canalización de implementación. Para añadir las bibliotecas de cliente, haga esto:

1. Acceda a [Repositorio de Git de AEM Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/repositories.html?lang=es) y clónelo.
2. Abra la carpeta Repositorio de Git de AEM Cloud Service en un editor de texto del plan. Por ejemplo, Microsoft® Visual Code.
3. Abra el archivo `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\customheaderlibs.html` y añada el siguiente código al archivo:

   ```
       //Customheaderlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

4. Abra el archivo `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\customfooterlibs.html` y añada el siguiente código al archivo:

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

5. Abra el archivo `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\xfpage\customheaderlibs.html` y añada el siguiente código al archivo:

   ```
       //Customheaderlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

6. Abra el archivo `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\xfpage\customfooterlibs.html` y añada el siguiente código al archivo:

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

7. [Ejecute la canalización de implementación](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html?lang=es) para implementar las bibliotecas de cliente en el entorno de AEM as a Cloud Service.

>[!NOTE]
>
> Codifique la biblioteca de cliente de funciones personalizadas solo cuando sea necesaria para todos los formularios. Para las bibliotecas que difieren según el tipo de formulario, añádalas a través de directivas de página de plantilla, como se explica en la siguiente sección.

**Caso 2: usar el mismo componente de página de sitios**

Incluya las bibliotecas de cliente en tiempo de ejecución o las bibliotecas de funciones personalizadas en la directiva de página de la plantilla utilizada para crear páginas con formularios.

1. Abra la página de AEM Sites o el Fragmento de experiencia para editarlos. Para abrir la página para editarla, selecciónela y haga clic en **[!UICONTROL Editar]**.
2. Abra la plantilla de su página Sites o Fragmento de experiencia. Para abrir la plantilla, vaya a **[!UICONTROL Información de página]** ![Información de página](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL Editar plantilla]**. Se abre la plantilla correspondiente en el editor de plantillas.
3. Vaya a la sección **[!UICONTROL Información de página]** ![Información de página](/help/forms/assets/Smock_Properties_18_N.svg) de la plantilla y seleccione la opción **[!UICONTROL Política de página]**. Esto abre las propiedades de la plantilla de AEM Sites, donde puede definir funciones personalizadas o bibliotecas de cliente de tiempo de ejecución.
4. Haga clic en el botón **[!UICONTROL Agregar]** de la ficha **[!UICONTROL Propiedades]** para agregar nuevas bibliotecas de funciones personalizadas o bibliotecas de tiempo de ejecución.
5. Haga clic en **[Listo]**.

>[!VIDEO](https://video.tv.adobe.com/v/3476178?quality=12&learn=on)

### Habilitar formularios adaptables: incrustados (v2) para su página de AEM Sites o fragmento de experiencia

Para habilitar el componente **[!UICONTROL Formularios adaptables: Incrustados (v2)]** en la política de la plantilla, siga los siguientes pasos:

1. Abra la página de AEM Sites o el Fragmento de experiencia para editarlos. Para abrir la página para editarla, selecciónela y haga clic en **[!UICONTROL Editar]**.
1. Abra la plantilla de su página Sites o Fragmento de experiencia. Para abrir la plantilla, vaya a **[!UICONTROL Información de página]** ![Información de página](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL Editar plantilla]**. Se abre la plantilla correspondiente en el editor de plantillas.
1. En la vista Estructura, haga clic en el icono **[!UICONTROL Política]** ![Política](/help/forms/assets/Smock_FeedManagement_18_N.svg) en la barra de menús. En la lista **[!UICONTROL Componentes permitidos]**, seleccione la casilla de verificación **[!UICONTROL Formularios adaptables: Incrustados (v2)]** en **[Nombre de proyecto de tipo de archivo de AEM]: formulario adaptable**.
1. Haga clic en **[!UICONTROL Listo]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419369?quality=12&learn=on)

## Para incrustar un formulario adaptable utilizando el componente Formularios adaptables: incrustados (v2) {#embed-an-adaptive-form-in-sites-editor-or-experience-fragment}

Utilice el componente de **[!UICONTROL Formularios adaptables: incrustados (v2)]** para crear un formulario adaptable desde AEM Sites Editor mediante el asistente de creación de formularios. El formulario resultante se guarda como una entidad externa, lo que permite su reutilización en otras páginas de Sites y en formularios independientes. Puede incrustar un formulario completamente nuevo desde cero y adaptarlo específicamente a sus necesidades y preferencias de diseño, directamente en una página de AEM Sites o en un Fragmento de experiencia. Para formularios de un solo uso, se recomienda la creación directa en una página de AEM Sites, mientras que los Fragmentos de experiencias son ideales para formularios que deben reutilizarse en varias páginas del sitio web.

Puede incrustar fácilmente un formulario nuevo mediante **[!UICONTROL Formularios adaptables: incrustados (v2)]**.  Por ejemplo, imagine que incorpora un nuevo formulario de contacto a una página de AEM Sites o un Fragmento de experiencia de AEM. Cualquier actualización o modificación realizada en el formulario de contacto dentro de la página de AEM Sites o del Fragmento de experiencia se aplicará automáticamente a todas las páginas en las que esté implementado. Esto simplifica la administración de los formularios del sitio web, lo que garantiza una experiencia del usuario perfecta y optimiza el proceso general.

Con los **[!UICONTROL Formularios adaptables: incrustados (v2)]** puede hacer lo siguiente:

* [Incrustar un nuevo formulario con el Asistente para Formularios adaptables en una página de AEM Sites](#embed-form-using-adaptive-form-wizzard-aem-sites)
* [Incrustar un nuevo formulario mediante el Asistente para Formularios adaptables en un Fragmento de experiencia](#embed-form-using-adaptive-form-wizzard-experience-fragment)
* [Incrustar un formulario adaptable en una página de AEM Sites](#embed-an-adaptive-form-in-sites-editor)
* [Incrustar un formulario existente en un Fragmento de experiencia](#embed-an-adaptive-form-in-experience-fragment)
* [Conversión de un formulario adaptable en una página de AEM Sites a un Fragmento de experiencia](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)

### Incrustar un nuevo formulario con el Asistente para Formularios adaptables en una página de AEM Sites {#embed-form-using-adaptive-form-wizzard-aem-sites}

Los pasos para incrustar un nuevo formulario en una página de AEM Sites son los siguientes:

1. Abra la página de AEM Sites en el modo de edición.
1. En el panel Explorador de componentes, arrastre y coloque el componente **[!UICONTROL Formularios adaptables: incrustar(v2)]** en la página.
1. Haga clic en el icono **Más** y se le redirigirá al asistente de creación de formularios.

   Componente ![Formularios adaptables: incrustar](/help/forms/assets/aemformcontainer.png)

1. Cree un nuevo formulario adaptable desde el asistente de **[!UICONTROL Creación de formularios.]**
La variable **[!UICONTROL Ruta de recursos]** ya incluye la ruta de un formulario adaptable creado
1. Guarde la configuración. El formulario adaptable está ahora incrustado en la página.

>[!VIDEO](https://video.tv.adobe.com/v/3419366/adaptive-form-aem-forms?quality=12&learn=on)

A continuación, puede [establecer la acción de envío](/help/forms/configuring-submit-actions.md) y las propiedades avanzadas de un formulario adaptable incrustado mediante el asistente para la creación de formularios.


### Incrustar un nuevo formulario mediante el Asistente para Formularios adaptables en un Fragmento de experiencia {#embed-form-using-adaptive-form-wizzard-experience-fragment}

Los pasos para incrustar un nuevo formulario en un Fragmento de experiencia son los siguientes:

1. Abra el Fragmento de experiencia en modo de edición.
1. En el panel Explorador de componentes, arrastre y coloque el componente **[!UICONTROL Formularios adaptables: incrustar(v2)]** en la página.
1. Haga clic en el icono **Más** y se le redirigirá al asistente de creación de formularios.

   Componente ![Formularios adaptables: incrustar](/help/forms/assets/aemformcontainer.png)

1. Cree un nuevo formulario adaptable desde el asistente de **[!UICONTROL Creación de formularios.]**
La variable **[!UICONTROL Ruta de recursos]** ya incluye la ruta de un formulario adaptable creado
1. Guarde la configuración. El formulario adaptable está ahora incrustado en el Fragmento de experiencia.

A continuación, puede [establecer la acción de envío](/help/forms/configuring-submit-actions.md) y propiedades avanzadas de un formulario adaptable incrustado mediante el asistente para la creación de formularios.

### Incrustar un formulario adaptable en una página de AEM Sites {#embed-an-adaptive-form-in-sites-editor}

Con el componente **[!UICONTROL Formularios adaptables:incrustados (v2)]** puede integrar fácilmente un formulario adaptable preexistente en una página de AEM Sites. Esta función mejora significativamente la adaptabilidad y reutilización de Formularios adaptables, ofreciendo a los clientes una forma cómoda de reutilizar formularios que ya han creado. Por ejemplo, imagine que incorpora un formulario de contacto a una página de AEM Sites, lo que elimina la necesidad de volver a crear el formulario varias veces.

Para incrustar un formulario adaptable en una página de Sites, haga lo siguiente:

1. Abra la página de AEM Sites en el modo de edición.
1. Arrastre y suelte el componente **[!UICONTROL Formularios adaptables: incrustados (v2)]** del explorador de componentes a la página de Sites.
1. Seleccione el componente **[!UICONTROL Formularios adaptables: incrustados]** en la página de Sites y, a continuación, seleccione ![propiedades del Contenedor de formulario adaptable](/help/forms/assets/configure-icon.svg) en la barra de acciones. Se abre el cuadro de diálogo **[!UICONTROL Editar formularios adaptables: incrustados (v2)]**.
1. Busque y seleccione el formulario adaptable para incrustarlo en la **[!UICONTROL Ruta de recursos]**.
1. Guarde la configuración. El formulario adaptable está ahora incrustado en la página.

>[!VIDEO](https://video.tv.adobe.com/v/3419368?quality=12&learn=on)

A continuación, puede [establecer la Acción Enviar](/help/forms/configuring-submit-actions.md) y las propiedades avanzadas de un formulario adaptable incrustado mediante el asistente para la creación de formularios.

### Incrustar un formulario adaptable existente en un Fragmento de experiencia {#embed-an-adaptive-form-in-experience-fragment}

También puede ampliar la accesibilidad de los formularios incrustándolos en el Fragmento de experiencia de AEM. Para incrustar un Formulario adaptable en un Fragmento de experiencia, haga lo siguiente:

1. Abra un Fragmento de experiencia en modo de edición.
1. Arrastre y suelte el componente **[!UICONTROL Formularios adaptables: incrustados (v2)]** del explorador de componentes al Fragmento de experiencia.
1. Seleccione el componente **[!UICONTROL Formularios adaptables: incrustados]** en el Fragmento de experiencia y ![Propiedades del contenedor del formulario adaptable](/help/forms/assets/configure-icon.svg) en la barra de acciones. Se abre el cuadro de diálogo **[!UICONTROL Editar formularios adaptables: incrustados (v2)]**.
1. Busque y seleccione el formulario adaptable para incrustarlo en la **[!UICONTROL Ruta de recursos]**.
1. Guarde la configuración. El formulario adaptable ahora está incrustado en el Fragmento de experiencia.

A continuación, puede [establecer la acción de envío](/help/forms/configuring-submit-actions.md) y propiedades avanzadas de un formulario adaptable incrustado mediante el asistente para la creación de formularios.

### Conversión de un formulario en una página de AEM Sites a un fragmento de experiencia {#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment}

Puede convertir un formulario adaptable existente en un editor de páginas de Sites a un Fragmento de experiencia para reutilizar el formulario en varias páginas o sitios.

Para convertir un formulario adaptable en una página de AEM Sites en un Fragmento de experiencia:

1. Abra la página de AEM Sites que contiene el formulario adaptable (en el componente Contenedor de formularios adaptables) en el modo Editar.
1. Abra el árbol de contenido y seleccione el **[!UICONTROL Contenedor de formularios adaptables]** que aloja su formulario adaptable. Una página de AEM Sites puede alojar varios formularios adaptables. Por lo tanto, seleccione cuidadosamente el contenedor de formularios adaptables correcto.
1. En la barra de menús, seleccione el ![Icono Convertir para la variación del fragmento de experiencia](/help/forms/assets/Smock_FilingCabinet_18_N.svg) Icono Convertir en variación de Fragmento de experiencia.

   ![Haga clic en el logotipo del archivador para convertir un formulario adaptable de la página de AEM Sites en un fragmento de experiencia](/help/forms/assets/convert-form-in-sites-page-to-an-experience-fragment.png)

   Aparece un cuadro de diálogo para convertir el contenedor del formulario adaptable a un nuevo fragmento de experiencia o agregar a un fragmento de experiencia existente.

1. En el cuadro de diálogo de variación **[!UICONTROL Convertir en Fragmento de experiencia]**, establezca los valores de las siguientes opciones:

   * **Acción:** seleccione crear un Fragmento de experiencia o añadir a un Fragmento de experiencia existente.
   * **Ruta principal:** especifique la ruta de la carpeta en la que se alojará el Fragmento de experiencia. La opción solo está disponible para crear un nuevo Fragmento de experiencia.
   * **Plantilla:** especifique la ruta de la plantilla del Fragmento de experiencia. Si no tiene una plantilla de fragmento de experiencia, [créela](/help/implementing/developing/extending/experience-fragments.md). La opción solo está disponible para agregar formularios adaptables a un Fragmento de experiencia existente.
   * **Título del fragmento:** Especifique el título del Fragmento de experiencia. El título identifica de forma exclusiva un Fragmento de experiencia.
   * **Etiquetas del fragmento:** especifique la etiqueta del Fragmento de experiencia. La etiqueta identifica de forma exclusiva la categoría de un Fragmento de experiencia.

## Configurar las propiedades de incrustación del Formulario adaptable (v2)

Puede personalizar la configuración avanzada del componente **[!UICONTROL Formulario adaptable: incrustados (v2)]**. En el cuadro de diálogo **[!UICONTROL Editar formularios adaptables: incrustados]**, puede especificar lo siguiente:

* **Ruta del recurso**: examine y seleccione el formulario adaptable que desea incrustar. Se rellena automáticamente si ha colocado el formulario desde el Explorador de recursos.
* **Después del envío**: seleccione la acción que debe activarse después del envío del formulario. Puede elegir mostrar un mensaje o una página de agradecimiento.
   * **Mostrar mensaje de agradecimiento**: escriba un mensaje usando el editor de texto enriquecido para mostrar en el envío del formulario. Esta opción solo está disponible cuando elige mostrar un mensaje de agradecimiento.
   * **Página de agradecimiento**: examine y seleccione la página que desea mostrar después al enviar el formulario. Esta opción solo está disponible cuando elige mostrar una página de agradecimiento.
   * **Redirigir a la página de agradecimiento**: habilite la opción para reemplazar la página que contiene el formulario adaptable incrustado por una página de agradecimiento. De lo contrario, la página de agradecimiento reemplaza al formulario adaptable en el componente **[!UICONTROL Formularios adaptables: incrustados]**, sin actualizar la página de Sites subyacente. Esta opción solo está disponible cuando elige mostrar una página de agradecimiento.
   * **Mensaje de agradecimientos**: confirmación breve o que se muestra en la pantalla después de enviar correctamente un formulario.
   * **Página de agradecimiento**: examine y seleccione la página que desea mostrar después del envío correcto de un formulario.

* **Usar el idioma de la página**: utilice la configuración local de la página de AEM Sites en lugar de la configuración regional del formulario adaptable. Esta opción solo es aplicable al formulario adaptable (Foundation).
* **Definir el enfoque del formulario**: seleccione esta opción para establecer el enfoque en el primer campo del formulario adaptable. Esta opción solo es aplicable al formulario adaptable (Foundation).
* **Tema**: seleccione un tema que defina el estilo de los componentes del formulario adaptable. El estilo incluye propiedades de apariencia, como el estilo de fuente, el color de fondo, las dimensiones y la alineación. Esta opción solo es aplicable al formulario adaptable (Foundation).

  >[!NOTE]
  >
  > Puede usar las opciones **Usar idioma de la página**, **Definir enfoque en formulario** y **Tema** solo para formularios adaptables (Foundation).

* **El formulario abarca toda la anchura del marco**:
un marco en línea (iframe) es un elemento de HTML que carga un formulario adaptable en una página de AEM Sites.

   * Si la casilla de verificación **[!UICONTROL El formulario abarca toda la anchura del marco]** está seleccionada, significa que ese formulario adaptable ocupa la anchura completa del contenedor en el que se coloca. En este caso, no se utiliza un iframe para procesar el formulario. La presentación y el diseño de un formulario adaptable se ajustan para abarcar toda la anchura del contenedor, lo que lo hace adaptable y capaz de ajustarse a diferentes tamaños de pantalla. Esta opción permite incrustar varios Formularios adaptables en una página de AEM Sites.

     >[!NOTE]
     >
     > Para incrustar varios formularios en una página de AEM Sites, seleccione la casilla de verificación **[!UICONTROL El formulario abarca toda la anchura del marco]**.

   * Si la casilla de verificación **[!UICONTROL El formulario abarca toda la anchura del marco]** no está seleccionada, ese formulario adaptable no cubre toda la anchura del contenedor. En su lugar, se utiliza un iframe para procesar el formulario, que no se puede extender más allá de una anchura específica. Este método es útil cuando el formulario adaptable tiene límites definidos y necesita coexistir con otros componentes de AEM que se encuentran junto a él dentro del contenedor. Si esta opción no está seleccionada, solo permite incrustar un Formulario adaptable en la página de AEM Sites sin un iframe.

     >[!NOTE]
     >
     > La página de AEM Sites solo admite que exista un formulario adaptable sin un iframe. Para agregar más Formularios adaptables con el componente **[!UICONTROL Formularios adaptables: incrustados]**, seleccione la opción **[!UICONTROL El formulario abarca toda la anchura del marco]**.

* **Altura**: especifique la altura del contenedor. Déjelo en blanco para cambiar automáticamente el tamaño del contenedor.
* **Biblioteca de cliente CSS**: especifique la ruta a una biblioteca de cliente CSS.

<!--
In AEM Sites page, you can add an Adaptive Form using:

* **Adaptive Forms - Embed component**
   Adaptive Forms - Embed component enables AEM Sites authors to include an existing Adaptive Form within an AEM Sites page, thereby enhancing the reusability of adaptive forms. Existing Adaptive Forms can be used standalone or embedded in the site page. This integration provides a convenient way for customers to reuse Adaptive Forms they have already created.

* **Asset browser**
  All the forms are available under Assets. You can drag-drop the form as an asset on your page.

## Prerequisites {#prerequisites}

 To embed an Adaptive Form in an AEM Sites page that uses an editable template, ensure that the AEM Form component is configured as an allowed component in the associated template. 

In case **Adaptive Forms - Embed component** is not visible in the **Component browser panel** of AEM sites page, perform the following steps as illustrated in the video.

>[!VIDEO](https://video.tv.adobe.com/v/3410544)

In case Sites page is using a static template, you need to configure it in the paragraph system of the site page. 

## Embedding an Adaptive Form {#af-component}

To embed an Adaptive Form using the **[!UICONTROL Adaptive Forms - Embed]** component:

1. Open the AEM sites page, in edit mode, in which you want to embed an Adaptive Form.
1. From the Component browser panel, drag-drop the [!UICONTROL Adaptive Forms - Embed] component on the page. Alternatively, you can search for an Adaptive Form in the Assets browser and drag-drop it onto the Sites page. You can add a new Adaptive Form or embed an existing Adaptive Form. 

   >[!NOTE]
   >
   >Multiple Adaptive Forms - Embed components on a page are not supported.

1. To create and embed a new form, on the component toolbar, select the **Create Form** icon. A window to create the form opens. 

1. Select the embedded Adaptive Forms - Embed component in the sites page, and then select ![settings_icon](assets/settings_icon.png) on the action bar. The **[!UICONTROL Edit Adaptive Forms - Embed]** dialog opens.
1. In the Edit Adaptive Forms - Embed dialog, specify the following.

    **Asset Type:** Select the type of asset to embed. 
    * **Asset Path**: Browse and select the Adaptive Form to embed. It is auto-populated if you dropped it from the Assets browser.
    * **Post Submission** : Select the action to trigger on form submission. You can choose to show a thank you message or a thank you page.
        * Show

        * **Thank You Message**: Write a message using the rich text editor to show on form submission. This option is available only when you choose to show a thank you message.
        * **Thank You Page**: Browse and select the page to display on form submission. This option is available only when you choose to show a thank you page.
           * **Redirect to thank you page**: Enable the option to replace the page containing the embedded Adaptive Form with thank you page. Otherwise, the thank you page replaces the Adaptive Form in the [!UICONTROL Adaptive Forms - Embed] component, without refreshing underlying sites the page. This option is available only when you choose to show a thank you page.
    * **Use Page Language**: Use local of the AEM Sites page instead locale of Adaptive Form.
    * **Set Focus on Form**: Select to set the focus on the first field of the Adaptive Form.
    * **Theme**: Select a theme that defines styling for components of your Adaptive Form. Styling includes appearance properties such as font style, background color, dimensions, and alignment.
    * **Form covers entire width of the frame**: If checked, iframe is not used to render the form. 
    * **Height**: Specify the height of the container. Leave it blank to automatically resize the container.
    * **CSS Client library**: Specify path to a CSS client library.

1. Save the settings. The Adaptive Form  is now embedded in the page.


AEM site also lets you create an Adaptive Form on the fly using the Adaptive Forms - Embed component. Follow the steps to create an Adaptive Form using the **Adaptive Forms - Embed component** on AEM sites page:
1. Open the AEM sites page, in edit mode, in which you want to embed an Adaptive Form.
1. From the Component browser panel, drag-drop the Adaptive Forms - Embed component on the page.
1. Click the **Plus** icon and you are redirected to the form creation wizard.

    ![Adaptive Forms - Embed Component](/help/forms/assets/aemformcontainer.png)

1. You can now embed an Adaptive Form on AEM site pages using the [!UICONTROL AEM Forms Container Component].
-->

## Publicación de un formulario adaptable incrustado {#publishing-embedded-adaptive-form}

Consideremos los siguientes escenarios a la hora de publicar un formulario adaptable incrustado en una página de AEM Sites:

* Si publica la página de AEM Sites por primera vez y esta incluye un formulario adaptable incrustado, publique la página de Sites y el recurso incrustado.
* Si ha modificado únicamente el formulario adaptable incrustado en una página de Sites ya publicada, publique el recurso original, y los cambios se reflejarán en la página de Sites publicada. La página de Sites publicada incluye una referencia al recurso y no requiere que vuelva a publicar la página.
* Si ha modificado la página de Sites y el formulario adaptable integrado, vuelva a publicar la página y el recurso incrustado.

## Modificación de un formulario adaptable incrustado  {#modifying-embedded-adaptive-form}

Para modificar cualquier configuración o propiedad del formulario adaptable incrustado, realice una de las siguientes acciones.

* Abra el formulario original en Formularios adaptables en los respectivos editores y modifíquelo.
* Seleccione el formulario adaptable desde la página de Sites en el modo Edición y, a continuación, seleccione **[!UICONTROL Editar en una nueva ventana]**. El formulario original se abrirá en el modo de edición, donde puede modificarlo.

>[!NOTE]
>
>Los cambios realizados en el formulario adaptable original se reflejarán automáticamente en el formulario incrustado. No obstante, vuelva a publicar el formulario adaptable o la página de Sites para reflejar los cambios en la página publicada.

## Prácticas recomendadas {#best-practices}

Tenga en cuenta los siguientes puntos al incrustar formularios adaptables en páginas de AEM Sites:

* El encabezado y el pie de página del formulario original no se incluyen en el formulario incrustado.
* Los borradores de los usuarios y los envíos de formularios incrustados son compatibles y visibles en las pestañas Borradores y Formularios enviados del portal de Formularios.
* La acción de envío configurada en el formulario original se mantiene en el formulario incrustado.
* Si Adobe Analytics está configurado para el formulario original, los datos de análisis del formulario incrustado se capturan en esta aplicación. Sin embargo, no está disponible en el informe de análisis de Forms.

## Ver también {#see-also}

* [Crear formularios adaptables independientes basados en los componentes principales](/help/forms/creating-adaptive-form-core-components.md)
* [Creación de un formulario adaptable basado en componentes principales directamente en una página de AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
