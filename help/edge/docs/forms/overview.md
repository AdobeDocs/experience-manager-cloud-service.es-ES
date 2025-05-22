---
title: Información general sobre Edge Delivery Services para AEM Forms
description: Edge Delivery Services para AEM Forms
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: 8be0a9894bb5b3a138c0ec40a437d6c8e4bc7e25
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 97%

---

# Edge Delivery Services para AEM Forms


Edge Delivery Services para AEM Forms es un conjunto de servicios que permiten un entorno de desarrollo rápido en el que los autores pueden actualizar, publicar e iniciar nuevos formularios con rapidez. Estos servicios ofrecen experiencias de formularios excepcionales y de gran impacto que fomentan la participación y las conversiones. Estas experiencias de formulario son fáciles de crear y desarrollar.

Estos servicios le permiten:

* **Crear experiencias de inscripción con las herramientas que elija:** aumente la eficacia de la creación desacoplando las fuentes de contenido. De forma predeterminada, puede utilizar la creación basada en documentos (Microsoft SharePoint o Google Drive) y la creación WYSIWYG (editor universal o editor de formularios adaptables). Puede trabajar con varias fuentes de contenido en el mismo sitio de formularios y utilizar sus herramientas de creación preferidas, como Microsoft Excel, Google Sheets, el editor universal o el editor de formularios adaptables.

* **Ofrezca experiencias excepcionales de inscripción digital:** Ofrezca experiencias de inscripción digital que se carguen y procesen de forma rápida y continua para supervisar el rendimiento de los formularios mediante la telemetría operativa. Los tiempos de carga más rápidos y la experiencia del usuario optimizada contribuyen a que las tasas de finalización y conversión de formularios sean más altas.

* **Utilice un conjunto de herramientas fácil de usar para el desarrollador:** Edge Delivery Services para AEM Forms 
utiliza HTML simples, CSS modernos y JavaScript convencionales para crear experiencias excepcionales, y evita la pronunciada curva de aprendizaje de una plataforma específica. Un desarrollador con habilidades básicas de desarrollo web puede personalizar y crear fácilmente componentes y experiencias de formularios. No es necesario esperar a que se ejecute una canalización, solo tiene que registrar el código en GitHub y los cambios estarán activos.

## Información general sobre Edge Delivery Services para AEM Forms {#edge-overview}

Edge Delivery Services para AEM Forms ofrece un alto grado de flexibilidad en la forma en que se crean formularios en el sitio web. Puede crear contenido y formularios con [Creación WYSIWYG](/help/forms/creating-adaptive-form-core-components.md) y con [Creación basada en documentos](/help/edge/docs/forms/create-forms.md). Edge Delivery Services para AEM Forms 
proporciona un bloque de formularios denominado [Bloque de formularios adaptables](/help/edge/docs/forms/create-forms.md) para añadir un formulario a su sitio de Edge Delivery Services.

Por ejemplo, los formularios se crean directamente en Microsoft Excel o en Google Sheets y estas hojas de cálculo se transforman en formularios para su sitio web. Cualquier formulario o contenido nuevo, como un campo de formulario nuevo, estará disponible instantáneamente en su sitio web sin necesidad de volver a compilar el proceso.

En el diagrama siguiente se ilustra cómo puede editar formularios en Microsoft Excel o Google Sheets (creación basada en documentos) y publicarlos en Edge Delivery Services. También muestra el método de publicación de AEM mediante la creación WYSIWYG (editor universal o editor de formularios adaptable).

![Publicación en Edge Delivery Services y AEM](/help/edge/docs/forms/assets/AEM-forms-with-EDS-publishing.png)

Edge Delivery Services para AEM Forms aprovecha GitHub para que los clientes puedan administrar e implementar código directamente desde su repositorio de GitHub. Por ejemplo, puede escribir contenido en [Google Sheets](/help/edge/docs/forms/create-forms.md) o [Microsoft Excel](/help/edge/docs/forms/create-forms.md) y la funcionalidad del sitio se puede desarrollar mediante CSS y JavaScript en un repositorio de GitHub. 

Cuando los formularios estén listos, puede utilizar [AEM Sidekick](/help/edge/docs/forms/tutorial.md#preview-and-publish-your-content), una extensión del explorador Chrome, para obtener una vista previa y publicar actualizaciones de contenido.

![Instalación de AEM SideKick](/help/edge/assets/aem-sidekick-preview-publish-forms.png)

La elección entre [Creación basada en documentos](#document-based-authoring-features) y [Creación de WYSIWYG](#wysiwyg-authoring-features) depende de sus necesidades específicas:

* Para formularios simples que solo recopilan información básica con algunos campos (como formularios de contacto, formularios de generación de posibles clientes o formularios de solicitud de servicio) y en los que necesita conectividad de datos rápida mediante una hoja de cálculo, la [Creación basada en documentos](#document-based-authoring-features) es una buena opción. Puede crear estos formularios como lo haría con un documento en Google Sheets o Microsoft Excel.

* Para formularios complejos, como formularios que requieren varios paneles, reglas complejas y lógica empresarial, manipulación de datos, integración con sistemas externos o flujos de trabajo optimizados mediante funciones de AEM, la [Creación WYSIWYG](#wysiwyg-authoring-features) es la mejor opción.


### Funciones principales de la creación basada en documentos y la creación WYSIWYG

La creación basada en documentos ofrece un conjunto básico de funciones y la creación WYSIWYG ofrece capacidades adicionales más allá de la creación basada en documentos, lo que le permite generar formularios más complejos e interactivos. Las funciones principales de la creación basada en documentos y de la creación WYSIWYG son:

#### Funciones de la creación basadas en documentos

La creación basada en documentos permite crear formularios utilizando herramientas conocidas como Microsoft Excel o Google Sheets.  Estos formularios ofrecen las siguientes funcionalidades:

* Componentes accesibles para una experiencia fácil de usar.
* Estructura del HTML estandarizada para un procesamiento coherente.
* Reglas y validaciones para garantizar la precisión de los datos.
* Opciones de archivo adjunto para recopilar información adicional.
* Integración de reCAPTCHA de Google para la protección contra spam.
* Capacidad para crear componentes de formularios personalizados para necesidades específicas.
* Envíe los datos del formulario directamente a Microsoft Excel o Google Sheets o a direcciones de correo electrónico.
* Supervise el rendimiento de los formularios mediante la telemetría operativa

#### Funciones de la creación WYSIWYG

La creación WYSIWYG proporciona interfaces WYSIWYG (editor universal y editor de formularios adaptables) para generar formularios y ofrece todas las capacidades de la creación basada en documentos, además de una amplia gama de funciones adicionales:

* Editor de reglas avanzado para crear lógica compleja.
* Extensibilidad del lado del servidor para funcionalidades personalizadas.
* Experiencia de edición WYSIWYG para facilitar la creación y visualización de formularios.
* Funcionalidad de documento de registro para crear archivos a prueba de manipulaciones de los datos enviados.
* Integración con Adobe Sign para firmas electrónicas.
* Integración con Adobe Workfront Fusion para activar los escenarios de Adobe Workfront Fusion al enviar el formulario.
* Integración con varias fuentes de datos para rellenar previamente formularios y enviar datos.
* El modelo de datos de formulario sirve para definir la estructura de datos y las interacciones con varias fuentes de datos.
* Capacidad para elegir entre varias acciones de envío para administrar los envíos de formularios, incluido el envío de datos a Microsoft SharePoint, Microsoft OneDrive, Adobe Workfront Fusion, Salesforce, Microsoft Dynamics y muchas más fuentes de datos.

Todas las funciones anteriores también están disponibles a través del editor de formularios adaptables.

En esencia, la creación WYSIWYG (editor universal y [editor de formularios adaptables](/help/forms/creating-adaptive-form-core-components.md)) se basa en los conceptos básicos de la [Creación basada en documentos](/help/edge/docs/forms/create-forms.md), pero proporcionando un kit de herramientas más avanzado para crear y administrar formularios complejos.

>[!NOTE]
>
>
> La capacidad de Creación WYSIWYG está disponible en el programa para primeros usuarios. Si está interesado, envíe un correo electrónico rápido desde su dirección de trabajo a aem-forms-ea@adobe.com para solicitar acceso a la funcionalidad.

### Edge Delivery Services para AEM Forms

: Creación, publicación y envío de formularios

Los siguientes diagramas ilustran el proceso de creación, publicación y envío de formularios mediante la creación basada en documentos y la creación WYSIWYG.

![Creación basada en documentos](/help/edge/assets/document-based-authoring-workflow.png)

![Creación WYSIWYG](/help/edge/assets/wysiwyg-authoring-workflow.png)

## Empezar a crear formularios

* [Introducción a Edge Delivery Services para AEM Forms](/help/edge/docs/forms/tutorial.md)
* [Crear un formulario con Google Sheets o Microsoft Excel](/help/edge/docs/forms/create-forms.md)
* [Configurar Google Sheets o los archivos de Microsoft Excel para empezar a aceptar datos](/help/edge/docs/forms/submit-forms.md)
* [Publicar el formulario y empezar a recopilar datos](/help/edge/docs/forms/publish-forms.md)
* [Personalizar el aspecto de los formularios](/help/edge/docs/forms/style-theme-forms.md)
* [Añadir secciones repetibles a un formulario](/help/edge/docs/forms/repeatable-forms.md)
* [Mostrar un mensaje de agradecimiento personalizado después del envío del formulario](/help/edge/docs/forms/thank-you-page-form.md)
* [Componentes de bloque de formulario adaptable y sus propiedades](/help/edge/docs/forms/form-components.md)
* [Monitorización de usuarios reales](https://www.aem.live/developer/rum#authentication)

<!-- 

## Start creating forms

<div>

  <style>
    .card-container {
        width: calc(33.33% - 10px);;
        margin: 5px;
        border: 1px solid #ccc;
        border-radius: 5px;
        padding: 5px;
        box-sizing: border-box;
        transition: background-color 0.3s ease; /* Adding transition effect */
    }
    .card-container:hover {
        background-color: #f0f0f0; /* Changing background color on hover */
    }
</style>

<div style="display: flex; flex-wrap: wrap; justify-content: space-between; margin: -5px;">
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md">
            <img src="/help/edge/assets/smock_devices_18_n.svg" alt="Create a form using eds forms" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Create a form using Google Sheets or Microsoft Excel</b>
        </a>
        <p>Create forms that load and render quickly and automatically reflows on mobile devices.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="Submit form" alt="Use Form Fragments in an EDS Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Submit form to spreadsheet</b>
        </a>
        <p>Submit forms directly to your Microsoft Excel or Google Sheets.</p>
    </div>
     <div class="card-container">
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="Apply styles or themes to an eds form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Customize a theme</b>
        </a>
        <p>Create a consistent brand image by applying the same theme across forms.</p>
    </div>
      <div class="card-container">
        <a href="/help/edge/docs/forms/validate-forms.md">
            <img src="/help/edge/assets/smock_condition_18_n.svg" alt="Add validations to form fields" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Apply field validations</b>
        </a>
        <p>Reduce errors and frustration by checking form inputs for proper formatting.</p>
    </div> 
            <div class="card-container">
        <a href="/help/edge/docs/forms/rules-forms.md">
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="Use rules to add dynamic behaviour to a form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Use rules to add dynamic behaviour to a form</b>
        </a>
        <p>Reuse preconfigured fragments across multiple forms.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/translate-forms.md">  
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="Translate an EDS Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Translate a form</b>
        </a>
        <p>Extend the reach of your forms while keeping costs in check.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/repeatable-forms.md">  
            <img src="/help/edge/assets/smock_addto_18_n.svg" alt="Add repeatable sections to an EDS Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Add repeatable sections</b>
        </a>
        <p>Effortlessly create and add repeatable sections to a form.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/custom-components-forms.md"> 
            <img src="/help/edge/assets/smock_userdeveloper_18_n.svg" alt="Create custom forms components using standard JavaScript and CSS"  style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Create custom components</b>
        </a>
        <p>Use standard JavaScript and CSS to create components and themes.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/recaptacha-forms.md">  
            <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="Use reCAPTCHA in an EDS Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Use reCAPTCHA</b>
        </a>
        <p>Use OOTB reCAPTCHA integration for robust spam and bot protection.</p>
    </div>


</div>


</br>


-->