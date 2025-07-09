---
title: Información general sobre Edge Delivery Services para AEM Forms
description: Edge Delivery Services para AEM Forms está diseñado para ofrecer un rendimiento máximo, lo que le permite visualizar el futuro de la recopilación de datos y la participación del usuario optimizadas.
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: bca160763fdd1e96f1350ac74eb76ff7c26ac00b
workflow-type: tm+mt
source-wordcount: '1874'
ht-degree: 7%

---


# Introducción a Forms en AEM Edge Delivery Services

<span class="preview"> Esta es una función previa al lanzamiento y se puede acceder a esta en el [canal previo al lanzamiento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=es#new-features). </span>

Esta guía le ayuda a comprender e implementar formularios mediante Adobe Experience Manager (AEM) Edge Delivery Services (EDS). Tanto si está creando un formulario de contacto simple como una herramienta de recopilación de datos compleja, esta página le muestra las opciones.

## Explicación de Forms en Edge Delivery Services

Edge Delivery Services es la solución moderna de Adobe para ofrecer contenido web, incluidos formularios, con un rendimiento y una agilidad excepcionales. Con Edge Delivery Services para los formularios, puede:

* **Ofrecer experiencias más rápidas:** Forms se carga increíblemente rápido porque se proporcionan desde una red global de servidores Edge (CDN) cerca de sus usuarios. Esto mejora la satisfacción del usuario y puede aumentar las tasas de finalización del formulario.
* **Actualizar Forms más fácilmente:** El enfoque de Edge Delivery Services a menudo permite ciclos de desarrollo y actualizaciones de contenido más rápidos, para que pueda adaptar los formularios rápidamente.
* **Crear un Forms moderno y adaptable:** Cree formularios con un aspecto impecable y que funcionen sin problemas en cualquier dispositivo.
* **Aproveche la escalabilidad y la fiabilidad:** sus formularios serán tan sólidos y escalables como la infraestructura perimetral subyacente.

Esta guía:

* Explicar las diferentes formas de crear formularios (de autor) para los sitios de Edge Delivery.
* Muestra cómo configurar lo que sucede después de que un usuario envía un formulario (acciones de envío).
* Ayudarle a elegir los mejores métodos para sus necesidades específicas y habilidades de equipo.
* Proporcionar diagramas arquitectónicos y prácticas recomendadas.

## Términos clave que debe conocer

* **Edge Delivery Services (EDS):** La arquitectura de Adobe que ofrece el mejor rendimiento para entregar contenido de AEM a través de CDN. También conocido como Proyecto Franklin.
* **AEM Forms:** solución de Adobe para crear, administrar y procesar formularios.
* **Editor universal (UE):** Un editor visual de WYSIWYG para contenido de AEM, incluidos formularios.
* **Creación basada en documentos:** Creación de formularios con Microsoft Word o Google Docs/Sheets.
* **Creación de documentos (DA):** Servicio alojado en Adobe para la creación de contenido (incluidas páginas que pueden alojar formularios) para Edge Delivery Services.
* **Servicio de envío de Forms (FSS):** Servicio de Adobe que simplifica el envío de datos de formulario a hojas de cálculo o correo electrónico.
* **Instancia de publicación de AEM:** El entorno de AEM activo que puede procesar envíos de formularios complejos.
* **CORS (Intercambio de recursos de origen cruzado):** Característica de seguridad del explorador que necesita configuración al incrustar formularios de dominios diferentes.
* **CDN (red de distribución de contenido):** Red de servidores que entrega contenido web rápidamente a los usuarios en función de su ubicación geográfica.


**Diagrama conceptual de la interacción de formularios Edge Delivery Services**

<!--  
```mermaid
graph LR
    User[User on Device] >|Interacts| EdgeForm[Edge-Delivered Form Page]
    EdgeForm >|Loads Instantly| CDN[CDN Edge Server]
    CDN >|Serves Content| User
    EdgeForm >|Submits Data| Backend[Backend Processing - e.g. Forms Submission Service / AEM Publish]
    style User fill:#f9f,stroke:#333,stroke-width:2px
    style EdgeForm fill:#ccf,stroke:#333,stroke-width:2px
    style CDN fill:#9cf,stroke:#333,stroke-width:2px
    style Backend fill:#fca,stroke:#333,stroke-width:2px
``` -->

![Interacción de formulario](/help/forms/assets/eds-form-interaction.png)
Este diagrama muestra un usuario que interactúa con un formulario enviado rápidamente a través de una CDN. Los datos que envían se gestionan mediante un sistema backend.

## ¿Cómo funciona Forms en Edge?

Con EDS, el contenido del sitio web (incluida la estructura de los formularios) puede proceder de varias fuentes, como AEM as a Cloud Service, SharePoint, Google Drive o el servicio de creación de documentos (DA). Este contenido se publica en una CDN global. Cuando un usuario visita su sitio, el contenido se sirve directamente desde el servidor perimetral de CDN más cercano, lo que garantiza la máxima velocidad.

<!--*   **Where AEM Forms Fit In**
    Forms in an EDS architecture are designed to be:
    *   **Fast Loading:** Form structures are often simple HTML rendered client-side.
    *   **Decoupled:** The visual part of the form (frontend) is separate from where the data goes after submission (backend).
    *   **Flexible to Create:** You have different tools to build your forms.
    *   **Configurable for Submission:** You can send data to simple services or powerful AEM backends.-->

**Arquitectura de Edge Delivery Services simplificada con Forms**

<!--
```mermaid
    graph TD
        UserStart[<img src='https://img.icons8.com/ios-filled/50/000000/user.png' width='30' /> User on Device] >|Interacts| EdgeForm[Edge-Delivered Form Page]
        EdgeForm >|Loads Instantly| CDN[CDN Edge Server]
        CDN >|Serves Content| UserEnd[<img src='https://img.icons8.com/ios-filled/50/000000/user.png' width='30' /> User on Device]
        EdgeForm >|Submits Data| Backend[Backend Processing - Form Submission Service / AEM Publish]

        style UserStart fill:#f9f,stroke:#333,stroke-width:2px
        style UserEnd fill:#f9f,stroke:#333,stroke-width:2px
        style EdgeForm fill:#ccf,stroke:#333,stroke-width:2px
        style CDN fill:#9cf,stroke:#333,stroke-width:2px
        style Backend fill:#fca,stroke:#333,stroke-width:2px
``` -->

![Arquitectura](/help/forms/assets/eds-simplified-architecture.png)
Este diagrama muestra el recorrido: los formularios se definen en un sistema de creación, se publican en el perímetro, se proporcionan a los usuarios y los datos enviados se procesan mediante un servidor.

## Elección del método de creación de formularios

Existen tres formas principales de crear formularios para los sitios de Edge Delivery Services. Su elección dependerá de las habilidades de su equipo, la complejidad del formulario y las necesidades de su proyecto.

### ¿Qué enfoque de creación es adecuado para usted?

Utilice este árbol de decisión para ayudarle a elegir:

**Árbol de decisiones de creación de formularios**
<!--    
```mermaid
    graph TD
        A{Start: I need to create a form for an Edge Delivery Services site} > B{What are my team's primary content creation tools & skills?}
        B -- "We mainly use Word / Google Docs / Sheets" > C{How complex is the form and where does the data need to go?}
        B -- "We use AEM and prefer visual tools (Marketers or Designers)" > D[Use Universal Editor - WYSIWYG]
        B -- "Our site content is managed in Document Authoring (DA)" > E[Use Document Authoring - Embed Forms]
        C -- "Simple to moderate form, data to a spreadsheet or email" > F[Use Document-Based Authoring]
        C -- "More complex logic or needs AEM backend integration" > D
        E > G[Create form using Document-Based Authoring or Universal Editor, then embed in your DA page]

        style A fill:#f9f,stroke:#333,stroke-width:2px
        style F fill:#ccf,stroke:#333,stroke-width:2px
        style D fill:#ccf,stroke:#333,stroke-width:2px
        style G fill:#ccf,stroke:#333,stroke-width:2px
``` -->

![Seleccionar la plataforma correcta](/help/forms/assets/eds-authoring-selection.png)

Este árbol de decisión le ayuda a seleccionar un método de creación basado en las necesidades de su equipo y del formulario.

### Crear Forms con documentos (Word/Google Docs)

Este método es ideal para [crear formularios rápidamente si su equipo se siente cómodo con Microsoft Word o Google Docs/Sheets](/help/edge/docs/forms/create-forms.md).

**Cómo funciona: de documento a formulario web**

Los campos, etiquetas y tipos del formulario se definen directamente en un documento de Word o en una hoja de Google mediante un formato de tabla especial o un &quot;bloque de formulario&quot;. Al publicar este documento, Edge Delivery Services lo convierte automáticamente en un formulario de HTML compatible con la Web con el que los usuarios pueden interactuar en el sitio.

**Funciones y capacidades**

* Crear en herramientas familiares: Word, Google Docs, Hojas de cálculo de Google.
* Definir campos: entradas de texto, correo electrónico, listas desplegables, casillas de verificación, botones de opción y áreas de texto.
* Agregar etiquetas, marcadores de posición y mensajes de ayuda.
* Establecer reglas de validación básicas: campos obligatorios, formato de correo electrónico.
* Integre reCAPTCHA para la protección contra spam.
* Permitir la carga de archivos.
* Publicar al instante: Los cambios en el documento se reflejan rápidamente en el sitio activo.
* Ampliar con código personalizado: los usuarios avanzados pueden agregar componentes de formulario personalizados y estilo a través de GitHub.

**Consideraciones**

* Su equipo utiliza con regularidad Word o Google Docs/Sheets para el contenido.
* Debe crear formularios simples o moderadamente complejos rápidamente.
* Desea enviar datos de formulario directamente a una hoja de cálculo o a una dirección de correo electrónico con una configuración mínima.

**Funcionamiento De Los Envíos (Principalmente Servicio De Envío De Forms)**

Forms creó de esta manera, normalmente [envía sus datos al servicio de envío de AEM Forms](/help/forms/forms-submission-service.md). Lo configurará (a menudo en el propio documento de origen) para enviar datos a una hoja de Google, a un archivo de Excel en OneDrive/SharePoint o como correo electrónico.

**Concepto de creación basado en documentos**
<!--    
```mermaid
    graph LR
        subgraph Authoring["You define your form in a Google Sheet or Word Document"]
        Sheet[Spreadsheet or Document with field definitions:\nField Name - Type - Label\nemail - email - Email Address\nmessage - textarea - Your Message]
    end

        Sheet >|Edge Delivery Services automatically converts it| JSON[Internal Form Definition as JSON]
    JSON >|A 'Form Block' on your page renders it as| HTMLForm[Live HTML Form on Your Website]

        style Sheet fill:#e6ffe6,stroke:#333
        style JSON fill:#e6e6ff,stroke:#333
        style HTMLForm fill:#ffe6e6,stroke:#333
```-->

![Basado en documento](/help/forms/assets/eds-doc-based.png)
Este diagrama muestra cómo un formulario definido en un documento se convierte en un formulario web activo.

### Forms visualmente con el editor universal

El [Editor universal](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) ofrece una interfaz moderna de arrastrar y soltar para crear formularios directamente en el explorador web.

**Cómo funciona: Arrastrar y soltar el formulario**

Utilice una interfaz visual para arrastrar componentes de formulario (como campos de entrada, botones y listas desplegables) a la página. A continuación, puede configurar las propiedades de cada componente (etiquetas, validación, etc.) mediante un panel de propiedades. El editor universal muestra una vista previa en tiempo real del formulario.

**Funciones y capacidades**

* Creación visual de formularios con una biblioteca de componentes generados previamente.
* Configure la validación en tiempo real y la lógica empresarial (por ejemplo, mostrar u ocultar campos basados en selecciones).
* Consulte vistas previas en directo para diferentes dispositivos (escritorio, móvil).
* Integre con funciones de AEM como fragmentos de contenido, flujos de trabajo de AEM y permisos de usuario.
* Utilice el &quot;Experience Builder&quot; para obtener asistencia de IA para crear o editar formularios mediante indicaciones.

**Consideraciones**

* Debe crear formularios complejos con lógica condicional, paneles de varios pasos o personalización.
* Su equipo (por ejemplo, especialistas en marketing o usuarios empresariales) prefiere las herramientas visuales.
* Necesita una integración sólida con AEM as a Cloud Service para el control, los flujos de trabajo o el uso de recursos de AEM en los formularios.

**Cómo funcionan los envíos (servicio de envío de Forms o publicación de AEM)**

Forms creado con el editor universal puede:

* Use el [servicio de envío de Forms](/help/forms/forms-submission-service.md) sencillo (para enviar datos a hojas de cálculo o correo electrónico).
* Envíe datos a su instancia de publicación de AEM para un procesamiento más avanzado (como iniciar un flujo de trabajo de AEM, utilizar el modelo de datos de formulario o integrarse con otros sistemas empresariales).

**Concepto de editor universal**

<!--    
```mermaid
    graph TD
    subgraph UE_Interface["Universal Editor Interface in your Browser"]
        Toolbar[Editor Toolbar and Asset Finder]
        Canvas[Your Page with the Form Being Built]
        ComponentPalette[Available Form Components:\nInput / Dropdown / Button\nDrag and drop]
        PropertiesPanel[Configure Selected Component:\nLabel / Validation / Rules]
    end
    ComponentPalette >|Drag & Drop onto| Canvas
    Canvas >|Select a component to edit its| PropertiesPanel
    UE_Interface >|Creates| RenderedForm[Live Form on Your Website]

    style UE_Interface fill:#f0f8ff,stroke:#333
    style RenderedForm fill:#ffe6e6,stroke:#333
```-->

![Editor universal](/help/forms/assets/eds-ue-based.png)

Este diagrama muestra las partes principales del editor universal que se utilizan para la creación de formularios.

### Uso de Forms con la creación de documentos (DA)

[Creación de documentos (DA)](https://www.aem.live/developer/da-tutorial) es un servicio hospedado en Adobe para crear y administrar el contenido del sitio web principal (páginas, artículos) que se enviará a través de Edge Delivery Services. Es una alternativa al uso de SharePoint o Google Drive para el contenido de origen de Edge Delivery Services.

**Explicación de la creación de documentos (DA) para el contenido de Edge Delivery Services**

La creación de documentos proporciona un entorno de creación de nivel empresarial mediante el sistema de diseño de Adobe (Spectrum) y el modelo de documento de AEM (Blocks, Sections). Está diseñado para la gestión de contenido estructurado para EDS.

**Cómo Gestiona DA Forms (Incrustación, No La Creación Directa)**

El DA en sí **no es una herramienta para crear formularios desde cero**. En su lugar, usa DA para crear sus páginas web y luego *incrustar* formularios (creados mediante la creación basada en documentos o el editor universal) en esas páginas creadas por DA.

**Pasos para incrustar Forms en las páginas de DA**

1. **Cree su formulario:** Cree su formulario mediante:
   * Creación basada en documentos (Word/Google Docs)
   * Editor universal

1. **Publicar su formulario:** Asegúrese de que este formulario se publica y se puede acceder a él a través de su propia URL de Edge Delivery (por ejemplo, `https://your-eds-project.hlx.page/forms/contact-us`).
1. **Cree su página en DA:** Cree o edite la página en la creación de documentos en la que desea que aparezca el formulario.
1. **Incrustar el formulario:** Use un &quot;bloque&quot; o componente específico dentro de su página de DA para hacer referencia al formulario e incrustarlo desde su dirección URL. La página de DA recuperará y mostrará este formulario creado externamente.

**Creación de documentos con formulario incrustado**
<!--
```mermaid
    graph TD
    subgraph FormCreation["1. Create Form using other methods"]
        UE_Form[Universal Editor Form] >|Published to| FormLocation[Form lives at its own Edge Delivery Services URL:\nfor example: /forms/my-contact-form]
        DocBased_Form[Document-Based Form] >|Published to| FormLocation
    end

    subgraph DA_Content["2. Author Page in Document Authoring"]
        DAPage[Your Web Page Authored in DA\nExample: /main-site/landing-page]
        EmbedBlock[On DA Page, add 'Embed Form' Block\nPoints to /forms/my-contact-form]
    end

    DAPage > EmbedBlock
    User[User visits your DA Page] > DAPage
    EmbedBlock >|DA Page fetches and displays| FormLocation[The Form appears on your DA Page]

    style FormCreation fill:#e6ffe6,stroke:#333
    style DA_Content fill:#ffe6cc,stroke:#333
    style FormLocation fill:#ccf,stroke:#333
```-->

![Creación de documentos](/help/forms/assets/eds-da-based.png)

Este diagrama muestra que primero debe crear un formulario con UE o Docs y luego incrustarlo en una página que haya creado en Document Authoring.


### Comparación de opciones de creación

| Criterios | Creación basada en documentos | Editor universal (WYSIWYG) | Forms en la creación de documentos (DA) |
|----------------------------------|---------------------------------------|-----------------------------------------|-------------------------------------------|
| **Herramienta de creación principal** | Word/Google Docs/Hojas | Explorador (AEM Universal Editor) | N/D (los Forms están *incrustados*) |
| **Nivel de habilidad del equipo** | Familiarizado con los editores de documentos | Cómoda con las herramientas web visuales | Utiliza DA para el contenido de la página |
| **Complejidad típica del formulario** | De simple a moderado | De moderado a complejo, categoría empresarial | Depende del formulario incrustado |
| **Opción de envío 1 (simple)** | Servicio de envío de Forms (a hoja/correo electrónico) | Servicio de envío de Forms (a hoja/correo electrónico) | Sigue la configuración del formulario incrustado |
| **Opción de envío 2 (avanzada)** | N/D | Publicación de AEM (flujo de trabajo, FDM, etc.) | Sigue la configuración del formulario incrustado |
| **Integración back-end de AEM** | Mínimo | Alto (con envío de publicación de AEM) | Indirectamente, mediante el formulario de editor universal incrustado |
| **Mejor Para...** | Creación rápida de formularios sencillos por equipos de contenido, captura rápida de datos. | Especialistas en marketing, usuarios empresariales que necesiten control visual, formularios complejos o una integración AEM profunda. | Sitios donde el contenido principal se administra en DAM y que requieren formularios de otras fuentes. |

**Árbol de decisiones mejorado**
<!--
```mermaid
    graph TD
    A{Start Here: I need a form on my Edge Delivery Services Site} > B{What's my team's main authoring tool & skill for form content?};
    B -- "Word/Google Docs" > C{How complex is the form & data destination?};
    C -- "Simple form, data to Sheet/Email" > Sol1[CHOOSE: Document-Based Authoring + Forms Submission Service];
    C -- "Needs more logic OR AEM backend\nlike Workflow or FDM" > Sol2[CONSIDER: Can Universal Editor meet this need better?];

    B -- "AEM User / Visual Editor needed\nMarketer or Designer" > D{Where does the form data need to go?};
    D -- "Simple - to Sheet/Email" > Sol3[CHOOSE: Universal Editor + Forms Submission Service];
    D -- "Advanced - AEM Workflow, FDM,\n3rd Party via AEM" > Sol4[CHOOSE: Universal Editor + AEM Publish Submissions\nRequires additional setup];

    B -- "Our main site content is in Document Authoring (DA)" > Sol5[STRATEGY: Author form using Sol1, Sol2, Sol3 or Sol4 first\nTHEN embed that form into your DA page];

    A > F{Will this form be embedded or fetched from another site or domain?};
    F -- "Yes" > G[IMPORTANT: Configure CORS on the site hosting the form.\nEnsure any form JavaScript blocks are available where the form is displayed];

    style Sol1 fill:#90ee90,stroke:#333
    style Sol2 fill:#fffacd,stroke:#333
    style Sol3 fill:#90ee90,stroke:#333
    style Sol4 fill:#90ee90,stroke:#333
    style Sol5 fill:#add8e6,stroke:#333
    style G fill:#ffb6c1,stroke:#333
```-->

![Árbol de decisiones](/help/forms/assets/eds-enhanced-decision.png)

## Comparación de características de los métodos de creación

En la siguiente tabla se ofrece una comparación detallada de las características clave de los distintos métodos de creación de formularios de AEM, lo que le ayudará a seleccionar el método más adecuado para sus necesidades.

| **Capacidad** | **Editor universal (WYSIWYG)** | **Creación basada en documentos** | **Creación de documentos (DA)** |
|-----------------------------------------|-------------------------------|-----------------------------|-----------------------------|
| **Composición unificada con Sites** | ✅ |                              | ✅ (con formularios incrustados) |
| **Compatible con la incorporación de formularios** | ✅ | ✅ | ✅ (incrustado desde el editor universal o documentos) |
| **Reglas (comportamiento dinámico)** | Editor de reglas avanzadas con funciones personalizadas | Limitado: mostrar/ocultar, calcular valor, funciones personalizadas | Depende del formulario incrustado |
| **Compatible con los archivos adjuntos** | ✅ | ℹ️ (Acceso rápido) | Depende del formulario incrustado |
| **Compatibilidad con CAPTCHA** | reCAPTCHA Enterprise | reCAPTCHA Enterprise | Depende del formulario incrustado |
| **Características de envío** | REST, correo electrónico, FDM, flujo de trabajo, SharePoint, OneDrive, Azure Blob, Power Automate, Workfront Fusion (EA) | Sólo hoja de cálculo | Sigue la configuración del formulario incrustado |
| **Esquema de datos** | FDM, personalizado | Personalizado | Basado en formulario incrustado |
| **Relleno previo** | 💡 (a través del asistente) | ✅ | Depende del formulario incrustado |
| **Fragmentos** | ✅ | ✅ | Depende del formulario incrustado |
| **Editor de reglas visuales** | ✅ |                              |                              |
| **Localización** | 💡 (a través de Sites) | ℹ️ (Manual de Excel/Hojas) | Depende del formulario incrustado |
| **Esquema de datos (árbol de datos)** | 💡 (a través de la extensión de IU) |                              |                              |
| **Compatible con plantillas** | Solo contenido inicial |                              |                              |
| **Portal** |                               |                              |                              |
| **Tema** | ℹ️ (a nivel de proyecto) | ℹ️ (a nivel de proyecto) | ℹ️ (basado en el sitio de alojamiento) |
| **Componente personalizado** | ✅ | ✅ | ✅ (si el componente incrustado lo admite) |
| **OOTB y funciones personalizadas** | ✅ | ✅ | ✅ (en formulario incrustado) |
| **Referencia al fragmento** |                               |                              |                              |
| **Integración de Sign** |                               |                              |                              |
| **Experimentación** | ✅ | ✅ | Depende del contexto incrustado |
| **Administración de tareas mediante Workfront** | ✅ |                              |                              |
| **Extensión de la personalización** | 💡 |                              |                              |
| **Personalización del editor** | ✅ (a través de la extensión de IU) |                              |                              |
| **Acción de envío** | ✅ | Sólo hoja de cálculo | Basado en formulario incrustado |

<!--

## Best Practices for Creating Forms

Building great forms goes beyond just the technology. Here's how to ensure your forms are user-friendly and achieve their goals:

* **Designing User-Friendly and Accessible Forms**

  *   **Use Clear, Visible Labels:** Every form field needs a `<label>`. Don't rely only on placeholder text (text inside the input field), as it disappears when users type and is bad for accessibility.
        *   *Good:* `<label for="email">Email Address:</label> <input type="email" id="email" placeholder="you@example.com">`
        *   *Bad:* `<input type="email" placeholder="Email Address">`
  *   **Keep it Simple:** Use standard HTML input types (`<input type="date">`, `<input type="tel">`) where possible. They often have better mobile support and accessibility than complex custom widgets.
  *   **Logical Order and Grouping:** Arrange fields in a way that makes sense to the user. Group related fields together using `<fieldset>` and `<legend>`.
  *   **Provide Clear Instructions:** For any fields that might be confusing, offer concise help text or tooltips.
  *   **Keyboard Navigation:** Ensure users can navigate through your entire form using only the keyboard (Tab, Shift+Tab, Enter, Spacebar).
  *   **Error Handling:** Make errors obvious and easy to correct. Display error messages next to the relevant field and explain what needs to be fixed.

* **Ensuring Your Forms Load Quickly and Are Visible**

  *   **Place Forms Prominently:** If a form is important, make sure users can see it easily without too much scrolling ("above the fold" if possible). Adobe's research shows many forms get low interaction because they are hidden.
  *   **Optimize Assets:** Keep any custom JavaScript or CSS for your forms as small as possible to ensure fast load times. Edge Delivery Services helps with the base page load, but heavy form scripts can still slow things down.

* **Handling User Data Responsibly**
  *   **Ask Only What You Need:** The less Personal Identifiable Information (PII) you ask for, the better. Every field is a potential reason for a user to abandon the form.
  *   **Be Transparent:** Clearly explain *why* you need certain information and *how it will be used*. Link to your privacy policy. This builds trust.

* **Improving User Experience: Captcha Alternatives**

  * **Rethink Visible Captchas:** Those "type the wavy text" or "click all the traffic lights" tests can be very frustrating for users, especially those with disabilities, and often lead to high drop-off rates.

*   **Consider Alternatives:**
    *   **Honeypot Fields:** Add a hidden field that only bots would fill out. If it has data, the submission is likely spam.
    *   **Time-Based Checks:** Measure how quickly a form is submitted. Submissions that are too fast are often bots.
    *   **Invisible reCAPTCHA (v3):** This Google service analyzes user behavior in the background and only presents a challenge if the user seems suspicious. This is often a much better user experience.

**Form Design Do's and Don'ts**

```mermaid
    graph LR
subgraph GoodFormUX [Do ✅ - For Better Forms]
    direction LR
    ClearLabels[Use Visible <label> Tags for All Fields]
    SimpleInputs[Prefer Standard HTML Input Types]
    KeyboardNav[Ensure Full Keyboard Navigation]
    ClearErrors[Show Clear, Actionable Error Messages]
    MinimalPII[Ask Only for Necessary Information]
    TransparentUse[Explain How Data is Used - Privacy Info]
    InvisibleCaptcha[Use Invisible or Behavioral CAPTCHA]
    ProminentPlacement[Make Form Easy to Find on Page]
end

subgraph BadFormUX [Don't ❌ - Avoid These]
    direction LR
    PlaceholderOnly[Only Use Placeholder Text for Labels]
    ComplexWidgets[Use Overly Complex Custom Widgets]
    PoorErrors[Vague or Missing Error Messages]
    ExcessivePII[Request Excessive Personal Data]
    VisibleHardCaptcha[Use Hard-to-Solve Visible CAPTCHAs]
    HiddenForm[Hide the Form Deep in the Page]
end

style GoodFormUX fill:#e6ffe6,stroke:#333
style BadFormUX fill:#ffe6e6,stroke:#333
```

## Quick Decision Guide: Choosing the Right Form Strategy

Let's bring it all together to help you decide on the best approach for your forms.

*   **Matching Form Features to Your Project Goals**
    *   **For speed and simplicity with basic data capture (to spreadsheets/email):** Document-Based Authoring with the Forms Submission Service is often your fastest route.
    *   **For visually rich forms with potential for AEM backend integration:** Universal Editor is your tool. You can start with the Forms Submission Service for simple needs and scale to full AEM Publish submissions for complex workflows.
    *   **If your site content is managed in Document Authoring (DA):** You'll create forms using one of the above methods and then embed them into your DA pages. The submission logic will be tied to how the original embedded form was configured.-->

Para aprovechar lo que ha aprendido, así es como puede avanzar:

[Elija su estrategia de envío](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md) y decida si su proyecto requiere la simplicidad del servicio de envío de Forms (ideal para la salida de hoja de cálculo/correo electrónico) o la flexibilidad y la integración back-end que ofrecen las acciones de envío de publicación de AEM.

Consulte el artículo [Prácticas recomendadas para crear Forms](/help/edge/docs/forms/universal-editor/best-pratices-eds-forms.md) para aprender a diseñar formularios eficaces, accesibles y fáciles de usar.

## Siguientes pasos

Esta guía proporciona información general sobre el uso de formularios con AEM Edge Delivery Services. Para obtener instrucciones paso a paso más detalladas sobre configuraciones específicas, consulte la documentación oficial de Adobe Experience Manager:

* [Creación basada en documentos con Edge Delivery Services Forms](/help/edge/docs/forms/tutorial.md)
* [Editor universal con Edge Delivery Services Forms](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [Creación de documentos (DA) e incrustación de contenido](https://www.aem.live/developer/da-tutorial)
* [Servicio de envío de AEM Forms](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)


<!-- 
# Edge Delivery Services for AEM Forms
 

Edge Delivery Services for AEM Forms is a composable set of services that enables a rapid development environment where authors can update, publish, and launch new forms rapidly. These services deliver exceptional and high impact forms experiences that drive engagement and conversions. These forms experiences are easy to author and develop.

These services enable you to:

* **Create enrolment experiences with tools of your choice:** Increase authoring efficiency by decoupling content sources. Out of the box you can use Document-based Authoring (Microsoft SharePoint or Google Drive), WYSIWYG Authoring (Universal Editor or Adaptive Forms Editor). You can work with multiple content sources on the same forms site and use your preferred authoring tools, such as Microsoft Excel, Google Sheets, Universal Editor, or Adaptive Forms Editor.

* **Deliver exceptional Digital Enrolment experiences:** Deliver Digital Enrolment experiences that load and render quickly and continuously monitor your forms performance through Operational Telemetry. Faster loading times and optimized user experience contribute to higher form completion and conversion rates. 

* **Use developer friendly toolset:** Edge Delivery Services for AEM Forms
 uses plain HTML, modern CSS, and vanilla JavaScript to create exceptional experiences, avoiding the steep learning curve of a specific framework. A developer with basic web development skills can customize and easily build form components and experiences. There is no need to wait for a pipeline to run, just check-in your code into GitHub and your changes are live.

## Edge Delivery Services for AEM Forms Overview {#edge-overview}

Edge Delivery Services for AEM Forms allows for a high degree of flexibility in how you author forms on your website. You can author content and forms with [WYSIWYG Authoring](/help/forms/creating-adaptive-form-core-components.md) as well as [Document-based Authoring](/help/edge/docs/forms/create-forms.md). Edge Delivery Services for AEM Forms
 provide a forms block, known as [Adaptive Forms Block](/help/edge/docs/forms/create-forms.md) to add a form to your Edge Delivery Services site.

For example, you author forms directly in Microsoft Excel or Google Sheets and these spreadsheets are transformed into forms for your website. Any new form or form content, such as a new form field, is instantly available on your website without requiring a rebuild process.

The following diagram illustrates how you can edit forms in Microsoft Excel or Google Sheets (Document-based Authoring) and publish to Edge Delivery Services. It also shows the AEM publishing method using the WYSIWYG Authoring (Universal Editor or Adaptive Forms Editor).

![Publish to Edge Delivery Services and AEM](/help/edge/docs/forms/assets/AEM-forms-with-EDS-publishing.png)

Edge Delivery Services for AEM Forms uses GitHub so customers can manage and deploy code directly from their GitHub repository. For example, you can write forms in either [Google Sheets](/help/edge/docs/forms/create-forms.md) or [Microsoft Excel](/help/edge/docs/forms/create-forms.md) and the components of your forms can be developed by using CSS and JavaScript in a GitHub repository.

When your forms are ready, you can use the [AEM Sidekick](/help/edge/docs/forms/tutorial.md#preview-and-publish-your-content), a chrome browser extension, to preview and publish content updates.

![Install AEM SideKick](/help/edge/assets/aem-sidekick-preview-publish-forms.png)

The choice between the [Document-based Authoring ](#document-based-authoring-features) and [WYSIWYG Authoring](#wysiwyg-authoring-features) depends on your specific requirements:

* For simple forms that just collect basic information with a few fields (think contact us forms, lead generation forms, or service request forms), and where you need quick data connectivity using a spreadsheet, the [Document-based Authoring](#document-based-authoring-features) is a good fit. You can build these forms like you would build a document in Google Sheets or Microsoft Excel. 

* For complex forms, like forms requiring multiple panels, complex rules and business logic, data manipulation, integration with external systems, or streamlined workflows using AEM features, then [WYSIWYG Authoring](#wysiwyg-authoring-features) is a better option. 


### Key Features of Document-based Authoring and WYSIWYG Authoring

Document-based Authoring offers a basic set of features and WYSIWYG Authoring unlocks additional capabilities beyond the Document-based Authoring, empowering you to build more complex and interactive forms. The key features of both Document-based Authoring and WYSIWYG Authoring are:

#### Document-based Authoring features

Document-based Authoring  allows you to create forms using familiar tools like Microsoft Excel or Google Sheets. These forms offer the following functionalities:

* Accessible components for a user-friendly experience.
* Standardized HTML structure for consistent rendering.
* Rules and validations to ensure data accuracy.
* File attachment options for collecting additional information.
* Google reCAPTCHA integration for spam protection.
* Ability to create custom form components for specific needs.
* Submit form data directly to Microsoft Excel or Google Sheets or email addresses.
* Monitor your forms performance through Operational Telemetry

#### WYSIWYG Authoring features

WYSIWYG Authoring provides WYSIWYG interfaces (Universal Editor and Adaptive Forms Editor) for building forms and offers all the capabilities of Document-based Authoring, plus a wide range of additional features:

* Advanced rules editor for creating complex logic.
* Server-side extensibility for custom functionalities.
* WYSIWYG editing experience for easy form creation and visualization.
* Document of record functionality to create tamper-proof archives of submitted data.
* Integration with Adobe Sign for electronic signatures.
* Integration with Adobe Workfront Fusion to triggering Adobe Workfront Fusion scenarios upon form submission.
* Integration with various data sources for pre-populating forms and submitting data.
* Form Data Model (FDM) for defining data structure and interactions with various data sources.
* Ability to choose from multiple submit actions for handling form submissions, including submitting data to Microsoft SharePoint, Microsoft OneDrive, Adobe Workfront Fusion, Salesforce, Microsoft Dynamics, many more data sources.

The all above features are also available via Adaptive Forms Editor. 

In essence, WYSIWYG Authoring (Universal Editor and [Adaptive Forms Editor](/help/forms/creating-adaptive-form-core-components.md)) builds upon the foundation of [Document-based Authoring](/help/edge/docs/forms/create-forms.md), providing a more advanced toolkit for creating and managing complex forms. 

>[!NOTE]
>
>
> The WYSIWYG Authoring capability is available under the early-adopter program. If you are interested, send a quick email from your work address to aem-forms-ea@adobe.com to request access to the capability.

### Edge Delivery Services for AEM Forms

: Authoring, Publishing, and Submission of Forms  

The following diagrams illustrate the process of creating, publishing, and submitting forms using Document-based Authoring and WYSIWYG Authoring.

![Document-based Authoring](/help/edge/assets/document-based-authoring-workflow.png)

![WYSIWYG Authoring](/help/edge/assets/wysiwyg-authoring-workflow.png)

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
            <img src="/help/edge/assets/smock_devices_18_n.svg" alt="Create a form using Edge Delivery Services forms" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Create a form using Google Sheets or Microsoft Excel</b>
        </a>
        <p>Create forms that load and render quickly and automatically reflows on mobile devices.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="Submit form" alt="Use Form Fragments in an Edge Delivery Services Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Submit form to spreadsheet</b>
        </a>
        <p>Submit forms directly to your Microsoft Excel or Google Sheets.</p>
    </div>
     <div class="card-container">
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="Apply styles or themes to an Edge Delivery Services form" style="border-radius: 5px;"> </b>
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
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="Translate an Edge Delivery Services Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Translate a form</b>
        </a>
        <p>Extend the reach of your forms while keeping costs in check.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/repeatable-forms.md">  
            <img src="/help/edge/assets/smock_addto_18_n.svg" alt="Add repeatable sections to an Edge Delivery Services Form" style="border-radius: 5px;"> </b>
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
            <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="Use reCAPTCHA in an Edge Delivery Services Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Use reCAPTCHA</b>
        </a>
        <p>Use OOTB reCAPTCHA integration for robust spam and bot protection.</p>
    </div>


</div>


</br>


-->
