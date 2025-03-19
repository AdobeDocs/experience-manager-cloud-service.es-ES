---
title: ¿Cómo se crea un Forms adaptable independiente mediante el editor universal?
description: Forms En este artículo se explica cómo crear formularios adaptables mediante el asistente de creación de formularios en la instancia de autor de AEM y cómo publicar formularios en AEM Edge Delivery Services.
feature: Edge Delivery Services
role: User
hide: true
hidefromtoc: true
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: 3db311812f6c4521baf1364523a0e0b1134fee65
workflow-type: tm+mt
source-wordcount: '1215'
ht-degree: 46%

---

# Crear formularios independientes mediante el Editor universal (WYSIWYG)

<span class="preview"> Esta función está disponible a través del programa de acceso rápido. Para solicitar acceso, envíe un correo electrónico con el nombre de su organización de GitHub y el nombre del repositorio desde su dirección oficial a <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> . Por ejemplo, si la URL del repositorio es https://github.com/adobe/abc, el nombre de la organización es adobe y el nombre del repositorio es abc.</span>

Este artículo le guía a través del proceso de creación de formularios independientes con el Editor universal seleccionando una plantilla basada en Edge Delivery Services en el Asistente para la creación de formularios. También puede publicar los formularios creados con el Editor universal en AEM Edge Delivery Services.

<!--To publish forms to Edge Delivery Services, you must first establish a connection between your AEM environment and your GitHub repository. Once connected, you can author the forms using the Universal Editor, which follows a WYSIWYG (What You See Is What You Get) approach for a seamless and consistent user experience with Sites.-->

Antes de empezar, obtenga información sobre el tipo de componentes de Forms disponibles para usted:

* [Edge Delivery Services para AEM Forms](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) es un conjunto de servicios componibles que permiten un entorno de desarrollo rápido en el que los autores pueden actualizar, publicar e iniciar nuevos formularios rápidamente mediante el Editor universal. El editor universal simplifica la creación de formularios para los servicios de envío perimetral de Adobe con una interfaz de WYSIWYG visual y fácil de usar.

* [Componentes principales de formularios adaptables](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es): son componentes estandarizados de captura de datos. Estos componentes proporcionan funcionalidades de personalización, un tiempo de desarrollo reducido y costes de mantenimiento más bajos para sus experiencias de inscripción digital. Un desarrollador puede personalizar y aplicar estilo fácilmente a estos componentes. Puede visitar [https://aemcomponents.dev/](https://aemcomponents.dev/) para ver los componentes principales disponibles en acción **Adobe recomienda utilizar estos componentes modernos y ampliables para desarrollar formularios adaptables**.

* [Componentes de base de formularios adaptables](/help/forms/creating-adaptive-form.md): estos son componentes clásicos (antiguos) de captura de datos. Puede seguir utilizándolos para editar su Formulario adaptable basado en componentes de base existentes. Si está creando formularios nuevos, Adobe recomienda utilizar los [Componentes principales de Formularios adaptables para crear Formularios adaptables](#create-an-adaptive-form-core-components).

AEM Forms proporciona un bloque, conocido como bloque de formularios adaptables, para ayudarle a crear fácilmente formularios de Edge Delivery Services para capturar y almacenar los datos. Puede [crear un nuevo proyecto de AEM preconfigurado con el bloque de Forms adaptable](#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) o [agregar el bloque de Forms adaptable a un proyecto de sitio de AEM existente](#add-adaptive-forms-block-to-your-existing-aem-project).

![Flujo De Trabajo Del Repositorio De Github](/help/edge/assets/repo-workflow.png)

## Requisitos previos

* [Configure su repositorio de GitHub](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template) para establecer una conexión entre su entorno de AEM y el repositorio de GitHub.
* Si ya usa Edge Delivery Services, añada la versión más reciente del [bloque de formularios adaptables](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project) a su repositorio de GitHub.
* La instancia de autor de AEM Forms incluye una plantilla basada en Edge Delivery Services. Asegúrese de que la [última versión de los componentes principales](https://github.com/adobe/aem-core-forms-components) esté instalada en su entorno.
* Tenga a mano la URL de la instancia de autor de AEM Forms as a Cloud Service y el repositorio de GitHub.

## Crear un formulario adaptable mediante el Editor universal

Con el editor universal, puede crear fácilmente formularios interactivos e interactivos independientes mediante componentes listos para usar, como campos de texto, casillas de verificación y botones de opción. Ofrece potentes funciones, como reglas dinámicas, integración de datos sin problemas y opciones de personalización, que le permiten crear formularios según sus necesidades exactas.

>[!NOTE]
>
> También puede [crear un formulario en el sitio de AEM mediante la plantilla del sitio de Edge Delivery Services en el editor universal y publicarlo en Edge Delivery Services](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project).

Para crear un formulario adaptable independiente mediante el Editor universal, realice los siguientes pasos:

1. **Crear un formulario adaptable en una instancia de autor de AEM Forms**

   1. Inicie sesión en la instancia de autor de AEM Forms as a Cloud Service.
   1. Seleccione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.
   1. Seleccione **[!UICONTROL Crear]** > **[!UICONTROL Formularios adaptables]**. Se abre el asistente.
   1. En la pestaña **Source**, seleccione una plantilla de formulario basada en Edge Delivery Services:

      ![Crear Forms de EDS](/help/edge/assets/create-eds-forms.png)


      Al seleccionar una plantilla basada en Edge Delivery Services, se habilita el botón **[!UICONTROL Crear]**.
   1. (Opcional) En las pestañas **[!UICONTROL Source de datos]** o **[!UICONTROL Envío]**, puede seleccionar un origen de datos o realizar una acción de envío.
   1. (Opcional) En la pestaña **[!UICONTROL Entrega]**, puede especificar una fecha de publicación o cancelación de publicación de un formulario adaptable.

   1. Haga clic en **[!UICONTROL Crear]** y aparecerá el asistente **Crear formulario**.
   1. Especifique **Name** y **Title**.
   1. Especifique la **URL de GitHub**. Por ejemplo, si el repositorio de GitHub se llama `edsforms` y se encuentra en la cuenta `wkndforms`, la dirección URL es:
      `https://github.com/wkndforms/edsforms`
   1. Haga clic en **[!UICONTROL Crear]**.

      ![Asistente para crear formularios](/help/edge/assets/create-form-wizard.png)

      Tan pronto como haga clic en **[!UICONTROL Crear]**, el formulario se abrirá en el editor universal para la creación.

      ![crear el formulario](/help/edge/assets/author-form.png)

      <!-- >[!NOTE]
        >
        > The Edge Delivery Services configuration for the forms based on Edge Delivery Services template is created automatically at the form's configuration container.-->

      Al hacer clic en **[!UICONTROL Crear]**, el formulario se abrirá en el editor universal para la creación.

1. **Crear el formulario en el editor universal**

   1. Abra el explorador de contenido y vaya al componente **[!UICONTROL Formulario adaptable]** en el **Árbol de contenido**.

      ![árbol de contenido](/help/edge/assets/content-tree.png)

   1. Haga clic en el icono de **[!UICONTROL Añadir]** y añada los componentes deseados de la lista **Componentes de formularios adaptables**.

      ![añadir componente](/help/edge/assets/add-component.png)

   1. Seleccione el componente de formulario adaptable añadido y actualice sus propiedades mediante **[!UICONTROL Propiedades]**.

      ![abrir propiedades](/help/edge/assets/component-properties.png)

      La siguiente captura de pantalla muestra el formulario `Registration Form` simple creado en el editor universal:

      ![formulario de contacto](/help/edge/assets/contact-us.png)

      Ahora puede [configurar y personalizar las acciones de envío de formularios](/help/edge/docs/forms/universal-editor/submit-action.md).


<!--
## **Edge Delivery Services configuration of form**



   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Edge Delivery Services Configuration]** on your AEM Forms as a Cloud Service author instance.

        ![Select Edge Delivery Services Configuration](/help/edge/assets/select-eds-conf.png)
   1. Select the folder that matches the form's name. For example, if your form is called 'registration-form' choose the folder `forms/registration-form` and selct the configuration and publish the configuration:

        ![Edge Delivery Services Configuration](/help/edge/assets/aem-instance-eds-configuration.png)

   1. Click **[!UICONTROL Properties]** to see the configuration.   
        ![Automatically created configuration](/help/edge/assets/aem-forms-create-configuration-github.png)

        You can leave the Edge Host option as it is. The form would be published to both preview (.page) and live (.live) environments. 

   1. Click **[!UICONTROL Save and Close]**. The configuration is saved. -->

## Publicación del formulario

Ahora, publique el formulario independiente en Edge Delivery Services haciendo clic en el botón **[!UICONTROL Publicar]** en la esquina superior derecha del Editor universal.

![publicar formulario](/help/edge/assets/publish-form.png)

>[!NOTE]
>
> Consulte el artículo [Publicar e implementar](/help/edge/docs/forms/universal-editor/publish-forms.md) para obtener información sobre cómo publicar un formulario en Edge Delivery Services.

A continuación, se explica cómo acceder al formulario en Edge Delivery Services:

* **Versión ensayada (para pruebas)**: la versión ensayada muestra la versión de trabajo sin publicar del formulario para realizar pruebas. Utilice el siguiente formato de URL para previsualizar el formulario antes de que se active:

  `https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>`

  Por ejemplo, si el repositorio de su proyecto se denomina &quot;edsforms&quot;, está ubicado en la cuenta &quot;wkndforms&quot;, y está utilizando la rama &quot;principal&quot; y el formulario como &quot;Formulario de registro&quot;, la URL de la versión ensayada tendrá el siguiente aspecto:
  `https://main--edsforms--wkndforms.aem.page/content/forms/af/registration-form`

* **Versión activa (formulario publicado)**: la versión activa muestra la versión publicada más recientemente del formulario, accesible para los usuarios finales. Utilice el siguiente formato de URL para acceder a la versión publicada y activa del formulario:

  `https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>`

  Por ejemplo, si el repositorio de su proyecto se denomina &quot;edsforms&quot;, está ubicado en la cuenta &quot;wkndforms&quot;, y está utilizando la rama &quot;principal&quot; y el formulario como &quot;Formulario de registro&quot;, la URL de la versión ensayada tendrá el siguiente aspecto:
  `https://main--edsforms--wkndforms.aem.live/content/forms/af/registration-form`

La estructura de la URL sigue siendo la misma para las versiones ensayadas y activas. Sin embargo, el contenido que ve difiere según el contexto:

![Ver formulario publicado](/help/edge/assets/eds-view-publish-form.png)

## Administrar formularios

Puede realizar varias operaciones en el formulario mediante la interfaz de usuario de AEM Forms.

1. Inicie sesión en la instancia de autor de AEM Forms as a Cloud Service.
1. Seleccione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.

1. Seleccione un formulario y la barra de herramientas mostrará las siguientes operaciones que puede realizar en el formulario seleccionado.

<table>
 <tbody>
  <tr>
   <td><p><strong>Operación</strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p>Editar</p> </td>
   <td><p>Abre el formulario en modo de edición.<br /> <br /> </p> </td>
  </tr>
    <tr>
   <td><p>Propiedades</p> </td>
   <td><p>Proporciona opciones para modificar las propiedades del formulario.<br /> <br /> </p> </td>
  </tr>
  <td><p>Copiar</p> </td>
   <td><p> Proporciona opciones para copiar el formulario y pegarlo en la ubicación deseada. <br /> <br /> </p> </td>
  </tr>
   <tr>
   <td><p>Vista previa</p> </td>
   <td><p>Proporciona opciones para obtener una vista previa del formulario como HTML o realizar una vista previa personalizada combinando los datos de un archivo XML con el formulario. <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Descargar</p> </td>
   <td><p>Descarga el formulario seleccionado.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Iniciar revisión/Administrar revisión</p> </td>
   <td><p>Permite iniciar y administrar una revisión del formulario seleccionado.<br /> <br /> </p> </td>
  </tr>
  <!--<tr>
   <td><p>Add Dictionary</p> </td>
   <td><p>Generates a dictionary for localizing the selected fragment. For more information, see <a>Localizing Adaptive Forms</a>.<br /> <br /> </p> </td>
  </tr>-->
  <tr>
   <td><p>Publicar o cancelar la publicación</p> </td>
   <td><p>Publica/cancela la publicación del formulario seleccionado.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Eliminar</p> </td>
   <td><p>Elimina el formulario seleccionado.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Comparar</p> </td>
   <td><p>Compara dos formularios diferentes con fines de vista previa.<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

## Solución de problemas

¿Tiene problemas para cargar el formulario? Estos son algunos problemas comunes y cómo solucionarlos:

* **Dirección URL del formulario**: compruebe que la dirección URL del formulario no incluya la extensión &quot;.html&quot; al final. Edge Delivery Service no requiere esta extensión.

* **URL de autor de AEM**: asegúrese de que la URL de autor que aparece listada en el archivo `fstab.yaml` tenga el formato correcto. Debe incluir los siguientes detalles:

   * El propietario correcto de GitHub
   * El nombre de repositorio correcto
   * La rama específica que utiliza para Edge Delivery Services

<!-- * **JSON Display**: If you see only JSON data instead of the actual form, your form block might be outdated. You can update it to the latest version available on https://github.com/adobe-rnd/aem-boilerplate-forms.
-->

## Empezar a crear formularios

{{universal-editor-see-also}}
