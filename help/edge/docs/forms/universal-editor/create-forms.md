---
title: Creación de formularios independientes basados en plantillas de componentes principales o de Edge Delivery Services y publicación en Edge Delivery Services.
description: En este artículo se explica cómo crear formularios adaptables seleccionando plantillas basadas en componentes principales o en Edge Delivery Services en el Asistente para la creación de formularios. También puede publicar los formularios en Edge Delivery Services de AEM.
feature: Edge Delivery Services
role: User
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: e1ead9342fadbdf82815f082d7194c9cdf6d799d
workflow-type: tm+mt
source-wordcount: '1687'
ht-degree: 95%

---


# De la creación a la publicación: AEM Forms en Edge Delivery Services

<span class="preview"> Esta función está disponible a través del programa de acceso rápido. Para solicitar acceso, envíe un correo electrónico con el nombre de su organización de GitHub y el nombre del repositorio desde su dirección oficial a <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a>. Por ejemplo, si la URL del repositorio es https://github.com/adobe/abc, el nombre de la organización es “adobe” y el nombre del repositorio es “abc”.</span>

Adobe Experience Manager (AEM) permite crear formularios atractivos, interactivos y dinámicos. Ofrece varios métodos de creación, cada uno adaptado a diferentes requisitos y niveles de experiencia del usuario.

Este artículo se centra en el método en el que los formularios se crean dentro del entorno de AEM y se publican a través de Edge Delivery Services. Los formularios creados con plantillas basadas en componentes principales se pueden publicar tanto en AEM como en Edge Delivery Services, lo que ofrece flexibilidad en la implementación. Por el contrario, los formularios creados con plantillas basadas en Edge Delivery Services solo se pueden publicar en Edge Delivery Services.

![Crear y publicar formularios adaptables](/help/edge/docs/forms/universal-editor/assets/author-publish-af.png){width=50% align=center}

## Ventajas de crear formularios en AEM y publicarlos con Edge Delivery Services:

* **Conservación de los flujos de trabajo de AEM existentes**: las organizaciones pueden seguir utilizando sus flujos de trabajo de AEM y las estructuras de control establecidas, lo que garantiza la coherencia y el control sobre la creación de contenido.

* **Mejora del rendimiento**: la publicación en Edge Delivery Services se renderiza más rápido, lo que reduce los tiempos de carga de la página, por lo tanto, mejora la experiencia del usuario.

* **Mejoras en la optimización de los motores de búsqueda**: Edge Delivery Services está concebido para ofrecer contenido con altas puntuaciones en Google Lighthouse, lo que optimiza el motor de búsqueda y aumenta la visibilidad.

* **Opciones de implementación flexibles**: los formularios creados con componentes principales se pueden publicar tanto en AEM como en Edge Delivery Services, lo que ofrece flexibilidad en las estrategias de implementación.

## Antes de comenzar

Antes de empezar a crear formularios en AEM y publicarlos a través de Edge Delivery Services, asegúrese de que se cumplen los siguientes requisitos previos:

* Asegúrese de tener un repositorio de Github configurado para Edge Delivery Services.
   * Si no tiene un repositorio, cree un [nuevo proyecto de AEM preconfigurado con el bloque de formularios adaptables](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block).
   * Si tiene un repositorio, añada el bloque de formularios adaptables al repositorio existente. Encontrará instrucciones detalladas en [Introducción a Edge Delivery Services para AEM Forms](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project).
* Establezca una conexión entre su entorno de AEM y el repositorio de GitHub. [¿Cómo hacerlo?](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template)

Diagrama de flujo de decisión como guía para la configuración y publicación de formularios adaptables:

![Flujo de trabajo de repositorio de Github](/help/forms/assets/repo-workflow.png){width=auto}

## Creación de formularios en AEM y publicación en Edge Delivery Services

Siga estos pasos para crear formularios en AEM y publicarlos en Edge Delivery Services:

[&#x200B;1. Elegir una plantilla y crear el formulario](#choose-a-template-and-create-the-form)

[&#x200B;2. Crear el formulario](#author-the-form)

[&#x200B;3. Publicar un formulario](#publish-a-form)

### Elegir una plantilla y crear el formulario

Puede crear formularios en una instancia de AEM para publicarlos en Edge Delivery Services mediante:

>[!BEGINTABS]

>[!TAB Plantilla basada en Edge Delivery Services]

Siga estos pasos para elegir la plantilla y crear el formulario:

1. Inicie sesión en su instancia de autor de AEM Forms as a Cloud Service.
1. Seleccione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.
1. Seleccione **[!UICONTROL Crear]** > **[!UICONTROL Formularios adaptables]**. Se abre el asistente.
1. En la pestaña **Fuente**, seleccione una **plantilla basada en Edge Delivery Services**:

   ![Creación de formularios EDS](/help/edge/assets/create-eds-forms.png)

   Al seleccionar una **plantilla basada en Edge Delivery Services**, se habilita el botón **[!UICONTROL Crear]**. 
1. (Opcional) En las pestañas **[!UICONTROL Fuente de datos]** o **[!UICONTROL Envío]**, puede seleccionar una fuente de datos o una acción de envío.
1. (Opcional) En la pestaña **[!UICONTROL Entrega]**, puede especificar una fecha de publicación o cancelación de publicación de un formulario.
1. Haga clic en **[!UICONTROL Crear]** y aparecerá el asistente para **crear formulario**:

   1. Especifique el **Nombre** y **Título**.
   1. Especifique la **URL de GitHub**. Por ejemplo, si el repositorio de GitHub se llama `edsforms` y está ubicado en la cuenta `wkndforms`, la URL es la siguiente:

      `https://github.com/wkndforms/edsforms`

   ![Asistente para crear formularios](/help/edge/assets/create-form-wizard.png)

   Al hacer clic en **[!UICONTROL Creación]**, el formulario se abre en el editor universal para la creación.

   ![Captura de pantalla del editor universal que muestra un formulario creado con la paleta de componentes a la izquierda, el lienzo del formulario en el centro y el panel de propiedades a la derecha](/help/edge/assets/author-form.png)
1. Haga clic en **[!UICONTROL Crear]** para crear el formulario. Ahora, puede [crear el formulario mediante el editor universal](#author-the-form).

>[!TAB Plantilla basada en componentes principales]

Siga estos pasos para elegir la plantilla y crear el formulario:

1. Inicie sesión en su instancia de autor de AEM Forms as a Cloud Service.
1. Seleccione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.
1. Seleccione **[!UICONTROL Crear]** > **[!UICONTROL Formularios adaptables]**. Se abre el asistente.
1. En la pestaña **Fuente**, seleccione una **plantilla basada en componentes principales** y un **tema**. El botón **[!UICONTROL Crear]** se activa:

   ![Plantilla basada en componentes principales](/help/forms/assets/core-component-based-template.png)

1. (Opcional) En las pestañas **[!UICONTROL Fuente de datos]** o **[!UICONTROL Envío]**, puede seleccionar una fuente de datos o una acción de envío.
1. (Opcional) En la pestaña **[!UICONTROL Entrega]**, puede especificar una fecha de publicación o cancelación de publicación de un formulario.
1. Haga clic en **[!UICONTROL Crear]** y aparecerá el asistente para **crear formulario**:
   1. Especifique el **Nombre** y el **Título**.
   1. Especifique la ubicación en el campo **Ruta** donde se va a guardar el formulario adaptable.

   ![Asistente para crear formulario](/help/forms/assets/create-cc-form.png)

   Al hacer clic en **[!UICONTROL Crear]**, el formulario se abrirá en el editor de formularios adaptables para la creación.

   ![Editor de formularios adaptables](/help/forms/assets/af-editor-form.png)

1. Haga clic en **[!UICONTROL Crear]** para crear el formulario. Ahora, puede [crear el formulario mediante el editor de formularios adaptables](#author-the-form).

>[!ENDTABS]

### Crear el formulario

Los formularios creados mediante la plantilla basada en Edge Delivery Services se abren en el [editor universal](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) para la creación. Sin embargo, los formularios creados mediante la plantilla basada en componentes principales se abren en el editor de formularios adaptables para su creación.

Realice los siguientes pasos para crear formularios mediante el editor universal para la plantilla basada en Edge Delivery Services o mediante el editor de formularios adaptables para la plantilla basada en componentes principales:

>[!BEGINTABS]

>[!TAB Plantilla basada en Edge Delivery Services]


1. Abra el explorador de contenido y vaya al componente **[!UICONTROL Formulario adaptable]** en el **Árbol de contenido**.

   ![árbol de contenido](/help/edge/assets/content-tree.png)

1. Haga clic en el icono de **[!UICONTROL Añadir]** y añada los componentes deseados de la lista **Componentes de formularios adaptables**.
   ![añadir componente](/help/edge/assets/add-component.png)

   La siguiente captura de pantalla muestra el `Registration Form` creado en el editor universal:

   ![Captura de pantalla de un formulario de contacto completado en el editor universal que muestra campos de formulario para nombre, correo electrónico, teléfono y mensaje con estilo y diseño adecuados](/help/edge/assets/contact-us.png)

>[!NOTE]
>
> Para obtener instrucciones detalladas sobre cómo crear un formulario adaptable con el editor universal, [haga clic aquí](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg).

Ahora puede [configurar y personalizar las acciones de envío de formularios](/help/edge/docs/forms/universal-editor/submit-action.md).

>[!TAB Plantilla basada en componentes principales]

1. Haga clic en **[!UICONTROL Insertar componente]** en la sección **Arrastre los componentes aquí**.

   ![Arrastre los componentes aquí](/help/forms/assets/drag-components-af-editor.png)

1. Añada los componentes deseados de la lista **Componentes de formularios adaptables**.

   ![Añadir componentes](/help/forms/assets/add-component-af.png)

La captura de pantalla siguiente muestra el `Enrollment Form` creado en el editor de formularios adaptables:

![Editor de formularios adaptables](/help/forms/assets/af-editor-form.png)

>[!NOTE]
>
> Para obtener instrucciones detalladas sobre la creación de un formulario adaptable basado en la plantilla de componentes principales, [haga clic aquí](/help/forms/creating-adaptive-form-core-components.md).

Ahora puede [configurar y personalizar las acciones de envío de formularios](/help/forms/configure-submit-actions-core-components.md).

>[!ENDTABS]

### Publicar el formulario

Para publicar un formulario adaptable en Edge Delivery Services, debe [crear una configuración de Edge Delivery Services en una instancia de AEM](#create-an-edge-delivery-services-configuration).

#### Crear una configuración de Edge Delivery Services

Siga estos pasos para crear la configuración de Edge Delivery Services:

>[!BEGINTABS]
>[!TAB Plantilla basada en Edge Delivery Services]


La configuración de Edge Delivery Services para los formularios basados en la plantilla basada en Edge Delivery Services se crea automáticamente en el contenedor de configuración del formulario.

![Configuración de Edge Delivery Services](/help/edge/assets/aem-instance-eds-configuration.png)

>[!TAB Plantilla basada en componentes principales]

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuración de Edge Delivery Services]** en la instancia de autor de AEM Forms as a Cloud Service.

   ![Seleccionar configuración de Edge Delivery Services](/help/edge/assets/select-eds-conf.png)

2. Seleccione la carpeta que coincida con el nombre del formulario. Por ejemplo, si el formulario se llama `enrollment-form`, elija la carpeta `forms/enrollment-form` y haga clic en **[!UICONTROL Crear]** > **[!UICONTROL Configuración]**:

   ![Configuración de Edge Delivery Services](/help/forms/assets/create-eds-conf.png)

3. Haga clic en **[!UICONTROL Configuración de Edge Delivery Services]** y luego en **[!UICONTROL Propiedades]** para abrir las propiedades:

   ![Configuración creada automáticamente](/help/forms/assets/eds-conf.png)

   Aparecerá la configuración de Edge Delivery Services.

4. Especifique lo siguiente en la configuración de Edge Delivery Services:

   * **Organización**: especifique el nombre de su organización de GitHub.

   * **Nombre del sitio**: especifique el nombre del repositorio de GitHub.
   * **Rama**: especifique el nombre de la rama. Deje el cuadro de texto vacío si utiliza la rama principal.
   * **(Opcional) Edge Host**: puede dejar la opción Edge Host tal como está. El formulario se publica en los entornos de vista previa (.page) y activo (.live).
   * **(opcional) Token de autenticación del sitio**: use el token de autenticación del sitio para autenticar de forma segura las solicitudes entre su instancia de AEM y Edge Delivery Services.

5. Haga clic en **[!UICONTROL Guardar y cerrar]**. Se ha creado la configuración.

>[!ENDTABS]

#### Acceso al formulario en Edge Delivery Services

Para acceder al formulario en Edge Delivery Services, es obligatorio publicarlo. Siga estos pasos para publicar el formulario:

>[!BEGINTABS]
>[!TAB En el editor universal]

1. Publique el formulario haciendo clic en el botón **[!UICONTROL Publicar]** en la esquina superior derecha del editor universal.

![Captura de pantalla del editor universal que muestra el cuadro de diálogo de publicación con opciones de publicación de formularios y botones de confirmación](/help/edge/assets/publish-form.png)

>[!NOTE]
>
> Consulte el artículo [Publicar e implementar](/help/edge/docs/forms/universal-editor/publish-forms.md) para obtener información sobre cómo publicar un formulario en Edge Delivery Services.

>[!TAB En el editor de formularios adaptables]

1. En la consola de Experience Manager Forms, vaya a la carpeta principal y seleccione el formulario que desea publicar.

1. Haga clic en la opción **[!UICONTROL Publicar]** en la barra de herramientas y observe todos los recursos de referencia que se publicarían con el formulario.

![Publicar formulario en el editor de formularios adaptables](/help/forms/assets/publish-af-editor.png)

>[!NOTE]
>
> Consulte el artículo [Administrar publicación en Experience Manager Forms](/help/forms/manage-publication.md) para obtener información sobre cómo publicar un formulario en el editor de formularios adaptables.

>[!ENDTABS]

* **Versión ensayada (para pruebas)**: la versión ensayada muestra la versión de trabajo sin publicar del formulario para realizar pruebas. Utilice el siguiente formato de URL para previsualizar el formulario antes de que se active:

  `https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>`



* **Versión activa (formulario publicado)**: la versión activa muestra la versión publicada más recientemente del formulario, accesible para los usuarios finales. Utilice el siguiente formato de URL para acceder a la versión publicada y activa del formulario:

  `https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>`

  La estructura de la URL sigue siendo la misma para las versiones ensayadas y activas. Sin embargo, el contenido que ve difiere según el contexto:

Las siguientes capturas de pantalla comparan las direcciones URL de los formularios clasificados y activos, así como las vistas previas visuales de los formularios creados con las plantillas basadas en Edge Delivery Services y las basadas en componentes principales:

>[!BEGINTABS]
>[!TAB Plantilla basada en Edge Delivery Services]

<table border="1" style="width: 100%; border-collapse: collapse; text-align: left;">
    <thead>
    <tr>
      <th style="width: 20%;"><strong>Versión</strong></th>
      <th style="width: 80%;"><strong>Imagen</strong></th>
    </tr>
    </thead>
    <tbody>
    <tr>
      <td>Versión ensayada</td>
      <td><img src="/help/forms/assets/registration-form-staged-version.png" alt="Versión ensayada del formulario de registro" style="width: 100%; height: auto;" /></td>
    </tr>
    <tr>
      <td>Versión activa</td>
      <td><img src="/help/forms/assets/registration-form-live-version.png" alt="Versión activa del formulario de registro" style="width: 100%; height: auto;" /></td>
    </tr>
    </tbody>
  </table>

>[!TAB Plantilla basada en componentes principales]

<table border="1" style="width: 100%; border-collapse: collapse; text-align: left;">
  <thead>
    <tr>
      <th style="width: 20%;"><strong>Versión</strong></th>
      <th style="width: 80%;"><strong>Imagen</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Versión ensayada</td>
      <td><img src="/help/forms/assets/enrollment-form-staged-version.png" alt="Versión ensayada del formulario de inscripción" style="width: 100%; height: auto;" /></td>
    </tr>
    <tr>
      <td>Versión activa</td>
      <td><img src="/help/forms/assets/enrollment-form-live-version.png" alt="Versión activa del formulario de inscripción" style="width: 100%; height: auto;" /></td>
    </tr>
  </tbody>
  </table>

>[!ENDTABS]

## Solución de problemas

¿Tiene problemas para cargar el formulario? Estos son algunos problemas comunes y cómo solucionarlos:

* **Dirección URL del formulario**: compruebe que la dirección URL del formulario no incluya la extensión &quot;.html&quot; al final. Edge Delivery Service no requiere esta extensión.

* **URL de autor de AEM**: asegúrese de que la URL de autor que aparece listada en el archivo `fstab.yaml` tenga el formato correcto. Debe incluir los siguientes detalles:

   * El propietario correcto de GitHub
   * El nombre de repositorio correcto
   * La rama específica que utiliza para Edge Delivery Services

## Empezar a crear formularios

{{universal-editor-see-also}}

<!-- * **JSON Display**: If you see only JSON data instead of the actual form, your form block might be outdated. You can update it to the latest version available on https://github.com/adobe-rnd/aem-boilerplate-forms.

### Managing a form

You can perform several operations on form using the AEM Forms user interface.

1. Login into your AEM Forms as a Cloud Service author instance.
1. Select **[!UICONTROL Adobe Experience Manager]** &gt; **[!UICONTROL Forms]** &gt; **[!UICONTROL Forms & Documents]**.

1. Select a form and the toolbar displays the following operations you can perform on the selected form.

<table>
 <tbody>
  <tr>
   <td><p><strong>Operation</strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
  </tr>
  <tr>
   <td><p>Edit</p> </td>
   <td><p>Opens the form in edit mode.<br /> <br /> </p> </td>
  </tr>
    <tr>
   <td><p>Properties</p> </td>
   <td><p>Provides options to modify the properties of the form.<br /> <br /> </p> </td>
  </tr>
  <td><p>Copy</p> </td>
   <td><p> Provides options to copy the form  and paste it at the desired location. <br /> <br /> </p> </td>
  </tr>
   <tr>
   <td><p>Preview</p> </td>
   <td><p>Provides options to preview the form as HTML or perform a custom preview by merging data from an XML file with the form. <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Download</p> </td>
   <td><p>Downloads the selected form.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Start Review/Manage Review</p> </td>
   <td><p>Allows initiating and managing a review of the selected form.<br /> <br /> </p> </td>
  </tr>
  <!--<tr>
   <td><p>Add Dictionary</p> </td>
   <td><p>Generates a dictionary for localizing the selected fragment. For more information, see <a>Localizing Adaptive Forms</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Publish / Unpublish</p> </td>
   <td><p>Publishes / unpublishes the selected form.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Delete</p> </td>
   <td><p>Deletes the selected form.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Compare</p> </td>
   <td><p>Compares two different form for previewing purposes.<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table> 


## How Edge Delivery Services Forms Work?

Users can author Edge Delivery Services Forms using document-based authoring tools such as Google Drive, SharePoint, or the Universal Editor (WYSIWYG authoring), while leveraging the basic styling, behaviour and components available in the GitHub repository. Once authored, Edge Delivery Services Forms can send data to any platform using the Forms Submission Service.

![How Edge Delivery Services Forms works](/help/edge/docs/forms/assets/eds-forms-working.png)

### Key components of Edge Delivery Services Forms

The key components of Edge Delivery Servies Forms are:

* **GitHub Repository**: The GitHub repository serves as a boilerplate for creating Edge Delivery Services Forms. The forms leverage basic styling and functionality from the repository and allow users to add customizations and custom components to the Edge Delivery Services Forms.

* **Form Authoring**: Edge Delivery Services Forms support two types of authoring: WYSIWYG and document-based authoring. Document-based authoring enables users to create forms using familiar tools like Google Docs and Microsoft Office. WYSIWYG authoring allows users to design forms visually using the Universal Editor, making it easy for non-technical users to create and manage forms. Universal Editor offers an intuitive form creation experience and provides access to numerous form capabilities.

* **Forms Submission Service**: The Forms Submission Service allows you to store data from forms submissions on any platform, such as OneDrive, SharePoint, or Google Sheets, making it easy to access and manage form data within your preferred system.-->
