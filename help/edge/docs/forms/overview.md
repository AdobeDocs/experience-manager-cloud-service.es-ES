---
title: Información general sobre Edge Delivery Services para AEM Forms
description: Cree y entregue formularios de alto rendimiento en Adobe Experience Manager Edge Delivery Services, con énfasis en el enfoque de creación del editor universal.
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: e1ead9342fadbdf82815f082d7194c9cdf6d799d
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 48%

---


# Edge Delivery Services para AEM Forms


Edge Delivery Services para AEM Forms es un conjunto de servicios que permiten un entorno de desarrollo rápido en el que los autores pueden actualizar, publicar e iniciar nuevos formularios con rapidez. Estos servicios ofrecen experiencias de formularios excepcionales y de gran impacto que fomentan la participación y las conversiones. Estas experiencias de formulario son fáciles de crear y desarrollar.

Estos servicios le permiten:

* **Crear experiencias de inscripción con las herramientas que elija:** aumente la eficacia de la creación desacoplando las fuentes de contenido. De forma predeterminada, puede utilizar la creación basada en documentos (Microsoft SharePoint o Google Drive) y la creación WYSIWYG (editor universal o editor de formularios adaptables). Puede trabajar con varias fuentes de contenido en el mismo sitio de formularios y utilizar sus herramientas de creación preferidas, como Microsoft Excel, Google Sheets, el editor universal o el editor de formularios adaptables.

* **Ofrecer experiencias excepcionales de inscripción digital:** ofrezca experiencias de inscripción digital que se carguen y procesen de forma rápida y continua para monitorizar el rendimiento de los formularios mediante la telemetría operativa. Los tiempos de carga más rápidos y la experiencia del usuario optimizada contribuyen a que las tasas de finalización y conversión de formularios sean más altas.

* **Utilice un conjunto de herramientas fácil de usar para el desarrollador:** Edge Delivery Services para AEM Forms 
utiliza HTML simples, CSS modernos y JavaScript convencionales para crear experiencias excepcionales, y evita la pronunciada curva de aprendizaje de una plataforma específica. Un desarrollador con habilidades básicas de desarrollo web puede personalizar y crear fácilmente componentes y experiencias de formularios. No es necesario esperar a que se ejecute una canalización, solo tiene que registrar el código en GitHub y los cambios estarán activos.

## Elección de un método de creación


Adobe Experience Manager (AEM) Edge Delivery Services (EDS) le permite ofrecer experiencias web increíblemente rápidas y escalables desde el perímetro de. En esta guía se explica **cómo crear y publicar formularios para esas experiencias**, con una jerarquía de recomendaciones clara:

1. **Editor universal (UE): la mejor opción para la mayoría de los equipos**
2. **Creación basada en documentos (documentos/hojas): ideal para formularios rápidos y sencillos**
3. **Creación de documentos (DA): se utiliza para incrustar formularios en páginas creadas por DA**

Al final, podrá elegir el método de creación adecuado, comprender las opciones de envío y seguir los pasos siguientes hacia formularios listos para la producción.





| Equipo y requisitos | Método recomendado | Por qué |
|--------------------|--------------------|-----|
| Los especialistas en marketing y los diseñadores necesitan un control visual, lógica condicional o integraciones de AEM | **Editor universal** | Arrastrar y soltar, reglas avanzadas, envíos a FSS o AEM Publish |
| Los autores de contenido ya trabajan en Word / Google Docs / Hojas; captura de datos sencilla para hoja de cálculo / correo electrónico | **Creación basada en documentos** | Herramientas familiares, la ruta más rápida para los formularios básicos |
| Páginas del sitio web creadas en **Creación de documentos (DA)** | **Incrustar** un formulario basado en UE o Doc en la página de DA | DA no crea formularios por sí mismo |


## Métodos de creación en detalle

### Editor universal

<span class="preview"> Esta es una característica previa al lanzamiento disponible a través de nuestro <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=es#new-features">canal previo al lanzamiento</a>. </span>

Universal Editor es una herramienta visual de creación de arrastrar y soltar para especialistas en marketing y diseñadores que combina velocidad con potencia de nivel empresarial:

* Edición de WYSIWYG en tiempo real y previsualizaciones de dispositivos.
* Integración directa con recursos de AEM, flujos de trabajo y el modelo de datos de formulario (FDM).
* Entrega perfecta a los desarrolladores de componentes personalizados en JS/CSS de vainilla.
* Editor de reglas avanzado para crear lógica compleja.
* Extensibilidad del lado del servidor para funcionalidades personalizadas.
* Experiencia de edición WYSIWYG para facilitar la creación y visualización de formularios.
* Funcionalidad de documento de registro para crear archivos a prueba de manipulaciones de los datos enviados.
* Integración con Adobe Sign para firmas electrónicas.
* Integración con Adobe Workfront Fusion para activar los escenarios de Adobe Workfront Fusion al enviar el formulario.
* Integración con varias fuentes de datos para rellenar previamente formularios y enviar datos.
* El modelo de datos de formulario sirve para definir la estructura de datos y las interacciones con varias fuentes de datos.
* Capacidad para elegir entre varias acciones de envío para administrar los envíos de formularios, incluido el envío de datos a Microsoft SharePoint, Microsoft OneDrive, Adobe Workfront Fusion, Salesforce, Microsoft Dynamics y muchas más fuentes de datos.
* Enviar mediante el servicio de envío de Forms (FSS) o las acciones de envío de publicación de AEM

> **Recomendación**: Inicie cada nuevo proyecto de formulario con el Editor universal a menos que su equipo esté 100 % centrado en documentos y el formulario sea muy básico.


### Creación basada en documentos (con Microsoft Docs o Google Sheets)

La creación basada en documentos es más adecuada para crear formularios sencillos y de baja complejidad con herramientas conocidas, como Microsoft Word, Google Docs o Hojas de cálculo de Google. Este método es ideal para equipos de contenido que requieren una forma rápida y directa de crear formularios.

* Componentes accesibles para una experiencia fácil de usar.
* Estructura del HTML estandarizada para un procesamiento coherente.
* Reglas y validaciones para garantizar la precisión de los datos.
* Opciones de archivo adjunto para recopilar información adicional.
* Integración de reCAPTCHA de Google para la protección contra spam.
* Capacidad para crear componentes de formularios personalizados para necesidades específicas.
* Envíe los datos del formulario directamente a Microsoft Excel o Google Sheets o a direcciones de correo electrónico.
* Supervise el rendimiento de los formularios mediante la telemetría operativa


### Incrustación de Forms en la creación de documentos (DA)

La creación de documentos (DA) está diseñada para crear contenido de página estructurado y no admite la creación de formularios nativos. Para agregar un formulario a una página creada por AD, puede crearlo con el **Editor universal** (recomendado) o la creación basada en documentos e incrustar el formulario en la página de creación de documentos.

## Publicación de Edge Delivery Services Forms {#edge-overview}

En el diagrama siguiente se ilustra cómo puede editar formularios en Microsoft Excel o Google Sheets (creación basada en documentos) y publicarlos en Edge Delivery Services. También muestra el método de publicación AEM mediante WYSIWYG Authoring (Universal Editor).

![Publicación en Edge Delivery Services y AEM](/help/edge/docs/forms/assets/AEM-forms-with-EDS-publishing.png)


<!-- 
## Feature Comparison

| Capability | Universal Editor | Document-Based | Document Authoring |
|------------|-----------------|----------------|--------------------|
| Visual drag-and-drop | ✅ | – | – |
| Advanced rules editor | ✅ | Limited | – |
| Attachments | ✅ | EA | – |
| reCAPTCHA Enterprise | ✅ | ✅ | Depends on embed |
| Submit to spreadsheet/email | ✅ (FSS) | ✅ (FSS) | Via embed |
| Submit to AEM workflows/FDM | ✅ | – | Via UE embed |
| Custom components (JS/CSS) | ✅ | ✅ | Via embed |
| Localization via Sites | ✅ | Manual | Via embed |

-->

## Siguientes pasos

1. **Empiece con el editor universal:** Consulte la [guía de introducción al editor universal](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) para comenzar a crear formularios.
1. **Usar la creación basada en documentos:** Para crear formularios con Microsoft Excel o Hojas de cálculo de Google, siga el [tutorial de creación basada en documentos](/help/edge/docs/forms/tutorial.md).
1. **Incrustar Forms en la creación de documentos:** Si está creando páginas en la creación de documentos, cree el formulario con el **Editor universal** (recomendado) o la creación basada en documentos e incruste el formulario en una [página de AD](https://www.aem.live/developer/da-tutorial).

Ya está listo para crear su primer formulario de alto rendimiento con AEM Edge Delivery Services.


<!-- 

## Start creating forms

* [Get started with Edge Delivery Services for AEM Forms](/help/edge/docs/forms/tutorial.md)
* [Create a form using Google Sheets or Microsoft Excel](/help/edge/docs/forms/create-forms.md)
* [Set up your Google Sheets or Microsoft Excel files to start accepting data​](/help/edge/docs/forms/submit-forms.md)
* [Publish your form and start collecting data](/help/edge/docs/forms/publish-forms.md)
* [Customize the look of your forms​](/help/edge/docs/forms/style-theme-forms.md)
* [Add repeatable sections to a form​](/help/edge/docs/forms/repeatable-forms.md)
* [Show a custom thank you message after form submission​](/help/edge/docs/forms/thank-you-page-form.md)
* [Adaptive Form Block components and their properties](/help/edge/docs/forms/form-components.md)
* [Real Use Monitoring](https://www.aem.live/developer/rum#authentication)

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