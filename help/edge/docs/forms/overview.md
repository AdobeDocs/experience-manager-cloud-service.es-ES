---
title: Información general sobre Edge Delivery Services AEM Forms
description: Los Edge Delivery Services de AEM Forms están diseñados para ofrecer un rendimiento máximo, lo que le permite visualizar el futuro de la recopilación de datos y la participación del usuario optimizadas.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
source-git-commit: d91254b52c257a3758da200a2c74b736ca457884
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 0%

---

# Edge Delivery Services de AEM Forms

Los Edge Delivery Services de AEM Forms son un conjunto de servicios componibles que permiten un entorno de desarrollo rápido en el que los autores pueden actualizar, publicar e iniciar nuevos formularios rápidamente. Estos servicios ofrecen experiencias de formularios excepcionales y de alto impacto que impulsan la participación y las conversiones. Estas experiencias de formulario son fáciles de crear y desarrollar.


Estos servicios le permiten:

* **Cree experiencias de inscripción con las herramientas que elija:** Aumente la eficacia de la creación desacoplando las fuentes de contenido. De forma predeterminada, puede utilizar la creación basada en documentos (Microsoft SharePoint o Google AEM Drive) y la creación de (editor de Forms adaptable). Puede trabajar con varios orígenes de contenido en el mismo sitio de formularios y utilizar sus herramientas de creación preferidas, como Microsoft Excel, Hojas de cálculo de Google o Editor de Forms adaptable.

* **Ofrezca experiencias excepcionales de inscripción digital:** Ofrezca experiencias de inscripción digital que se carguen y procesen rápidamente. Los tiempos de carga más rápidos y la experiencia de usuario optimizada contribuyen a que las tasas de finalización y conversión de formularios sean más altas.

* **Utilice un conjunto de herramientas fácil de desarrollar:** AEM Forms utiliza HTML sin formato, CSS moderno y JavaScript convencional para crear experiencias excepcionales, evitando la pronunciada curva de aprendizaje de un módulo específico. Un desarrollador con habilidades básicas de desarrollo web puede personalizar y crear fácilmente componentes y experiencias de formulario. No hay necesidad de esperar a que se ejecute una canalización, solo tiene que registrar el código en Github y los cambios estarán activos.

## Información general sobre Edge Delivery Services AEM Forms {#edge-overview}

El diagrama siguiente ilustra cómo se pueden editar formularios en Microsoft Excel o en hojas de Google (creación basada en documentos ) y publicar en Edge Delivery Services. AEM También muestra el método de publicación de la mediante el Editor de Forms AEM adaptable (creación de la).

![Arquitectura de Edge Delivery](/help/edge/assets/AEM-forms-with-EDS-publishing.png)

Los servicios de envío perimetral de AEM Forms son un conjunto de servicios componibles que permiten un alto grado de flexibilidad en la forma en que se crean formularios en el sitio web. AEM Puede utilizar tanto la administración de contenido de la con [AEM creación de](/help/forms/creating-adaptive-form-core-components.md) así como [Creación basada en documentos](/help/edge/docs/forms/create-forms.md).

Por ejemplo, los formularios se crean directamente en Microsoft Excel o en Hojas de cálculo de Google y estas se transforman en formularios para el sitio web. Cualquier formulario o contenido nuevo, como un campo de formulario nuevo, está disponible instantáneamente en el sitio web sin necesidad de volver a compilar el proceso.

Los Edge Delivery Services de AEM Forms utilizan GitHub para que los clientes puedan administrar e implementar código directamente desde su repositorio de GitHub. Por ejemplo, puede escribir formularios en [Hojas de cálculo de Google o Microsoft Excel](/help/edge/docs/forms/create-forms.md) y los componentes de los formularios se pueden desarrollar mediante CSS y JavaScript en GitHub.

Cuando esté listo, puede usar el complemento [AEM Sidekick](/help/edge/docs/forms/tutorial.md#preview-and-publish-your-content), una extensión del explorador chrome, para obtener una vista previa y publicar actualizaciones de contenido.

![AEM Sidekick de instalación](/help/edge/assets/install-aem-sidekick.png)

Los Edge Delivery Services de AEM Forms proporcionan un bloque de formularios denominado [Bloque de Forms adaptable](/help/edge/docs/forms/create-forms.md) para agregar un formulario al sitio de Edge Delivery Services.

La elección entre [Creación basada en documentos](#document-based-authoring-features) y [AEM creación de](#aem-authoring-features) depende de sus necesidades específicas.

Para formularios simples que solo recopilan información básica como nombres y correos electrónicos (como formularios de contacto, formularios de generación de posibles clientes o formularios de solicitud de servicio) y donde solo necesita los datos para ir a una hoja de cálculo, la variable [Creación basada en documentos](/help/edge/docs/forms/create-forms.md) es un ajuste perfecto. Puede crear estos formularios como lo haría con un documento en Google Sheets o Microsoft Excel.

AEM Si los formularios se vuelven más complejos, como requerir varios paneles, reglas complejas y lógica empresarial, manipulación de datos, integración con sistemas externos o flujos de trabajo optimizados mediante funciones de la aplicación de, entonces [AEM Creación de](/help/forms/creating-adaptive-form-core-components.md) es una mejor opción.


### AEM Características principales de la creación basada en documentos y la creación de

AEM La creación basada en documentos ofrece un conjunto básico de funciones y la creación de documentos desbloquea capacidades adicionales más allá de la creación basada en documentos, lo que le permite crear formularios más complejos e interactivos. AEM Las características principales de la creación basada en documentos y la creación de documentos de la creación de la son:

<!-- 

>[!BEGINTABS]

>[!TAB Document-based Authoring ]

Document-based Authoring  is a versatile option suitable for creating simple forms with essential functionalities. It allows you to integrate various input types like text fields, dropdown menus, and radio buttons, enabling you to collect user data effectively. It offers a basic version of rules to add dynamic behaviour to forms. Key features of Document-based Authoring  are: 

* **[HTML5-based Form Field components](/help/edge/docs/forms/form-components.md)**: AEM Forms Edge Delivery Services allow you to create user-friendly and interactive forms using form components based on HTML5 [input types](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types), <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">textarea</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">select</a>, and <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset</a>  elements. These components cater to different types of data collection and can be easily customized to fit your specific needs.  

* **Accessibility**: The fields in the form block are accessible. Each label is linked with its respective input element, and IDs are auto-generated for linking. Descriptions associated with fields are linked via the aria-describedby attribute. Keyboard navigation using the standard Tab/Shift + Tab keys is supported.

* **[Styling](/help/edge/docs/forms/style-theme-forms.md)**: Each form field has a fixed HTML structure that can be easily decorated using custom CSS or JavaScript files. Selectors for targeting fields in CSS and JS are provided based on type and name. You can easily create new selectors due to the standradized structure and style your form. 

* **Basic Rules**: Easily create logic that adjusts field visibility, validation, and behavior based on user input or predefined conditions. Rules offer a flexible and intuitive way to add intelligence to your forms, ensuring they adapt seamlessly based on user inputs.

* **Validations**: Before submission, the form is validated, and invalid fields are appropriately marked with error messages displayed to the user. Adaptive Forms Block support all the HTML form validation, supported by modern browsers, and provide additional validation mechanism like validation script, file size, file type, overall file size, and more. 

* **File Uploads**: You can add file attachment capabilities to your forms. Whether you need to gather documents, images, or other files from your users, file upload functionality serves you effortlessly. With custom handling options available, you can tailor the file upload process to suit your specific requirements.

* **reCAPTCHA**: Benefit from seamless integration of Google reCAPTCHA into your forms with our out-of-the-box (OOTB) support. Safeguard your forms against fraudulent activities, spam, and abuse, while maintaining a smooth and uninterrupted user experience. Adaptive Forms Block supports reCaptcha V3 and reCaptcha Enterprise. 

* **Send email notification on form submission**: Eliminate the hassle of manual follow-ups and ensure timely communication with our built-in email automation for form submissions. This integrated solution lets you effortlessly notify relevant parties, including sending form data, whenever someone fills out a form on your website. No need for complex configurations or additional tools – it's ready to use out of the box.

>[!TAB AEM Authoring]

AEM Authoring unlocks additional capabilities beyond the Document-based Authoring , empowering you to build more complex and interactive forms. In additon to the features of Document-based Authoring , AEM authoring offers the following additional features:  

* Advanced Rules: Define logic-based actions within your forms. You can use rules to conditionally show or hide form sections, pre-populate fields based on user input, and perform various validations to ensure data integrity.

* Server-side extensibility: Extend the functionalities of your forms by integrating them with server-side logic. This allows you to perform complex calculations, interact with external systems, and automate specific tasks based on user actions within the form.
* Streamline workflows and data management: Leverage the power of AEM to:
    * Design user-friendly forms using AEM editors.
    * Generate a "Document of Record" for secure and tamper-proof archiving of submitted data.
    * Facilitate e-signing with Adobe Sign for a smooth and secure signing experience.
    * Automate business processes through AEM workflows, triggering actions based on form submissions.
    * Effortlessly integrate with various data sources, enabling seamless data flow and exchange.

>[!ENDTABS]



## Start creating forms

-->

#### Funciones de creación basadas en documentos

La creación basada en documentos permite crear formularios utilizando herramientas conocidas como Microsoft Excel o Hojas de cálculo de Google. Estos formularios ofrecen las siguientes funcionalidades:

* Componentes accesibles para una experiencia fácil de usar.
* Estructura del HTML estandarizada para un procesamiento coherente.
* Reglas y validaciones para garantizar la precisión de los datos.
* Opciones de archivo adjunto para recopilar información adicional.
* Integración de Google reCAPTCHA para la protección contra spam.
* Capacidad para crear componentes de formulario personalizados para necesidades específicas.
* Envíe datos de formulario directamente a las direcciones de correo electrónico o a las hojas de cálculo de Microsoft Excel o Google.

#### AEM Funciones de creación de

AEM La creación de documentos proporciona una interfaz WYSIWYG (editor de Forms adaptable) para crear formularios y ofrece todas las capacidades de la creación basada en documentos, además de una amplia gama de funciones adicionales:

* Editor de reglas avanzado para crear lógica compleja.
* Extensibilidad del lado del servidor para funcionalidades personalizadas.
* Experiencia de edición WYSIWYG para facilitar la creación y visualización de formularios.
* Funcionalidad de documento de registro para crear archivos de datos enviados a prueba de manipulaciones.
* Integración con Adobe Sign para firmas electrónicas.
* Integración con Adobe Workfront Fusion para activar los escenarios de Adobe Workfront Fusion al enviar el formulario.
* Integración con varias fuentes de datos para rellenar previamente formularios y enviar datos.
* Modelo de datos de formulario para definir la estructura de datos y las interacciones con varias fuentes de datos.
* Capacidad para configurar varias acciones de envío para administrar los envíos de formularios, incluido el envío de datos a Microsoft SharePoint, Microsoft OneDrive, Adobe Workfront Fusion, Salesforce, Microsoft Dynamics y muchas más fuentes de datos.

AEM Básicamente, la creación de documentos se basa en la creación basada en documentos, que proporciona un conjunto de herramientas más avanzadas para crear y administrar formularios complejos.

### Flujo de trabajo de creación

![Creación basada en documentos ](/help/edge/assets/document-based-authoring-workflow.png)

![AEM creación de](/help/edge/assets/aem-authoring-workflow.png)


## Empezar a crear formularios

* [Introducción a los Edge Delivery Services de AEM Forms](/help/edge/docs/forms/tutorial.md)
* [Crear un formulario con hojas de Google o Microsoft Excel](/help/edge/docs/forms/create-forms.md)
* [Configure las hojas de Google o los archivos de Microsoft Excel para empezar a aceptar datos&#x200B;](/help/edge/docs/forms/submit-forms.md)
* [Publicar el formulario y empezar a recopilar datos](/help/edge/docs/forms/publish-forms.md)
* [Personalice el aspecto de los formularios&#x200B;](/help/edge/docs/forms/style-theme-forms.md)
* [Agregar secciones repetibles a un formulario&#x200B;](/help/edge/docs/forms/repeatable-forms.md)
* [Mostrar un mensaje de agradecimiento personalizado después del envío del formulario&#x200B;](/help/edge/docs/forms/thank-you-page-form.md)
* [Componentes de bloque de formulario adaptable y sus propiedades](/help/edge/docs/forms/form-components.md)



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