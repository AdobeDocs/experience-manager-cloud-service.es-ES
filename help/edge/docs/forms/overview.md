---
title: Información general sobre Edge Delivery Services AEM Forms
description: Los Edge Delivery Services de AEM Forms están diseñados para ofrecer un rendimiento máximo, lo que le permite visualizar el futuro de la recopilación de datos y la participación del usuario optimizadas.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
source-git-commit: 2aa70e78764616f41fe64e324c017873cfba1d5b
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 16%

---

# Edge Delivery Services de AEM Forms

Optimice la creación de formularios y aumente las tasas de finalización con los Edge Delivery Services de AEM Forms de Adobe. Este servicio potente y componible le permite crear formularios de nivel empresarial con un rendimiento excepcional y un atractivo visual. AEM La priorización de la experiencia del usuario y los objetivos de su empresa es prioridad, lo que garantiza tiempos de carga increíblemente rápidos y mayores conversiones de formularios.

Puede utilizar el servicio para lo siguiente:

* **Cree experiencias de inscripción excepcionales**: cree experiencias de inscripción que se carguen y procesen rápidamente, incluso con conexiones a Internet lentas. Los tiempos de carga más rápidos y la experiencia de usuario optimizada contribuyen a tasas de finalización de formularios más altas y tasas de conversión mejoradas.

* **Cree experiencias de inscripción con las herramientas que elija**: aumente la eficacia de la creación mediante la desvinculación de fuentes de contenido. De forma predeterminada, puede utilizar ambas **creación basada en documentos** (Microsoft SharePoint o Google Drive) y **AEM creación de** (Editor de Forms adaptable). De este modo, puede trabajar con varios orígenes de contenido en el mismo formulario y utilizar sus herramientas de creación preferidas, como Microsoft Excel, Hojas de cálculo de Google o Editor de Forms adaptable.

* **Utilice un conjunto de herramientas fácil de desarrollar:** AEM Forms utiliza HTML sin formato, CSS moderno y JavaScript convencional para crear experiencias excepcionales sin la sobrecarga habitual. Cualquier desarrollador con conocimientos básicos de HTML, CSS y JS debe poder crear sus propios componentes y no tener que aprender ningún lenguaje o módulo específico. No es necesario canalizar ni esperar, proteja su código en Github y los cambios estarán activos. Además, no es necesario realizar ninguna canalización ni esperar, proteja el código en Github y los cambios se activarán.


## Información general sobre Edge Delivery Services AEM Forms {#edge-overview}

El diagrama siguiente ilustra cómo se puede editar contenido en Microsoft Excel o en Hojas de cálculo de Google (edición basada en documentos) y publicarlo en Edge Delivery Services. AEM También muestra el método de publicación de la mediante el Editor de Forms adaptable.

![Arquitectura de Edge Delivery](/help/edge/assets/AEM-forms-with-EDS-publishing.png)

Edge Delivery Services es un conjunto de servicios que admiten composición que permiten un alto grado de flexibilidad en la forma en que se crea contenido en su sitio web. Como se mencionó anteriormente, puede utilizar ambos [AEM administración de contenido de](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/getting-started/concepts.html?lang=es) con [AEM creación de](/help/implementing/universal-editor/introduction.md) así como [creación basada en documentos](https://www.aem.live/docs/authoring)

Por ejemplo, puede utilizar contenido directamente desde Microsoft Excel o Hojas de cálculo de Google. Esto significa que el contenido de esas fuentes puede convertirse en formularios en el sitio web. El nuevo contenido se añade al instante sin que sea necesario un proceso de reconstrucción.

Edge Delivery Services aprovecha GitHub para que los clientes puedan administrar e implementar código directamente desde su repositorio de GitHub. Por ejemplo, puede escribir formularios en Google Sheets o en Microsoft Excel y los componentes de los formularios se pueden desarrollar con CSS y JavaScript en GitHub. Cuando esté listo, puede utilizar la extensión del explorador de la barra de tareas para obtener una vista previa y publicar actualizaciones de contenido.

Los Edge Delivery Services de AEM Forms proporcionan un bloque de formularios denominado [Bloque de Forms adaptable](/help/edge/docs/forms/create-forms.md) para agregar un formulario al sitio de Edge Delivery Services.

### Características principales de los Edge Delivery Services de AEM Forms

AEM La creación basada en documentos es un conjunto básico de funciones y la creación de documentos, que desbloquea capacidades adicionales más allá de la creación basada en documentos, lo que le permite crear formularios más complejos e interactivos. En la tabla siguiente se destacan las funciones clave de ambos:

<!-- 

>[!BEGINTABS]

>[!TAB Document-based authoring]

Document-based authoring is a versatile option suitable for creating simple forms with essential functionalities. It allows you to integrate various input types like text fields, dropdown menus, and radio buttons, enabling you to collect user data effectively. It offers a basic version of rules to add dynamic behaviour to forms. Key features of Document-based authoring are: 

* **[HTML5-based Form Field components](/help/edge/docs/forms/form-components.md)**: AEM Forms Edge Delivery Services allow you to create user-friendly and interactive forms using form components based on HTML5 [input types](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types), <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">textarea</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">select</a>, and <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset</a>  elements. These components cater to different types of data collection and can be easily customized to fit your specific needs.  

* **Accessibility**: The fields in the form block are accessible. Each label is linked with its respective input element, and IDs are auto-generated for linking. Descriptions associated with fields are linked via the aria-describedby attribute. Keyboard navigation using the standard Tab/Shift + Tab keys is supported.

* **[Styling](/help/edge/docs/forms/style-theme-forms.md)**: Each form field has a fixed HTML structure that can be easily decorated using custom CSS or JavaScript files. Selectors for targeting fields in CSS and JS are provided based on type and name. You can easily create new selectors due to the standradized structure and style your form. 

* **Basic Rules**: Easily create logic that adjusts field visibility, validation, and behavior based on user input or predefined conditions. Rules offer a flexible and intuitive way to add intelligence to your forms, ensuring they adapt seamlessly based on user inputs.

* **Validations**: Before submission, the form is validated, and invalid fields are appropriately marked with error messages displayed to the user. Adaptive Forms Block support all the HTML form validation, supported by modern browsers, and provide additional validation mechanism like validation script, file size, file type, overall file size, and more. 

* **File Uploads**: You can add file attachment capabilities to your forms. Whether you need to gather documents, images, or other files from your users, file upload functionality serves you effortlessly. With custom handling options available, you can tailor the file upload process to suit your specific requirements.

* **reCAPTCHA**: Benefit from seamless integration of Google reCAPTCHA into your forms with our out-of-the-box (OOTB) support. Safeguard your forms against fraudulent activities, spam, and abuse, while maintaining a smooth and uninterrupted user experience. Adaptive Forms Block supports reCaptcha V3 and reCaptcha Enterprise. 

* **Send email notification on form submission**: Eliminate the hassle of manual follow-ups and ensure timely communication with our built-in email automation for form submissions. This integrated solution lets you effortlessly notify relevant parties, including sending form data, whenever someone fills out a form on your website. No need for complex configurations or additional tools – it's ready to use out of the box.

>[!TAB AEM Authoring]

AEM Authoring unlocks additional capabilities beyond the document-based authoring, empowering you to build more complex and interactive forms. In additon to the features of Document-based authoring, AEM authoring offers the following additional features:  

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

|                                           | Creación basada en documentos | AEM Creación de (editor de Forms adaptable) |
| ----------------------------------------- | ------------------------ | ------------------------------------ |
| **Funcionalidad de formulario** |                          |                                      |
| Componentes accesibles | ✓ | ✓ |
| Estructura de HTML estandarizada | ✓ | ✓ |
| Reglas y validación | ✓ | ✓ |
| Archivos adjuntos (carga de archivos) | ✓ | ✓ |
| Google reCAPTCHA | ✓ | ✓ |
| Componentes personalizados | ✓ | ✓ |
| Enviar al correo electrónico | ✓ | ✓ |
| **Funciones avanzadas** |                          |                                      |
| Reglas avanzadas con el editor de reglas visual |                          | ✓ |
| Extensibilidad del lado del servidor |                          | ✓ |
| Varias acciones de envío |                          | ✓ |
| **Diseño y administración de formularios** |                          |                                      |
| Editor de Forms adaptable para la edición WYSIWYG |                          | ✓ |
| **Integraciones** |                          |                                      |
| Documento de registro |                          | ✓ |
| Integrar con Adobe Sign |                          | ✓ |
| Integración con Adobe Analytics |                          | ✓ |
| Integración con Marketo |                          | ✓ |
| Integración con varias fuentes de datos |                          | ✓ |
| Varias acciones de envío |                          | ✓ |


## Empezar a crear formularios

* [Introducción: tutorial para desarrolladores](/help/edge/docs/forms/tutorial.md)
* [Crear un formulario con hojas de Google o Microsoft Excel](/help/edge/docs/forms/create-forms.md)
* [Envíe formularios directamente a las hojas de cálculo de Microsoft Excel o Google](/help/edge/docs/forms/submit-forms.md)
* [Cambiar la apariencia de los formularios](/help/edge/docs/forms/style-theme-forms.md)


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