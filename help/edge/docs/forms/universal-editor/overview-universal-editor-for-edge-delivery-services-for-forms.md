---
title: Editor universal de Edge Delivery Services para formularios
description: Utilice el editor universal de Edge Delivery Services para formularios y crear formularios adaptables.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: d711e0d1-a2fc-4aa6-af87-6e77a7bc5d2e
source-git-commit: 9ef4c5638c2275052ce69406f54dda3ea188b0ef
workflow-type: ht
source-wordcount: '1012'
ht-degree: 100%

---


# Editor universal de Edge Delivery Services para formularios

<span class="preview"> Es una función de la versión preliminar y se puede acceder a ella a través de nuestro <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=es#new-features">canal de versiones preliminares</a>. </span>

El editor universal revoluciona la creación de formularios para Adobe Edge Delivery Services al ofrecer una interfaz WYSIWYG (What You See Is What You Get - Lo que se ve es lo que se obtiene) sencilla, visual e intuitiva. Diseñado para creadores de contenido y autores de formularios, elimina la complejidad de los procesos tradicionales de creación de formularios, lo que lo hace accesible incluso para usuarios no técnicos.

Con el editor universal, puede diseñar con rapidez formularios interactivos y adaptables mediante componentes creados previamente, como campos de texto, casillas de verificación y botones de opción. Su sólido conjunto de funciones admite reglas dinámicas, integración de datos fluida y personalización avanzada, lo que garantiza que cada formulario se adapte a sus necesidades.

Tanto si gestiona un renderizado ligero del lado del cliente, garantiza la compatibilidad entre exploradores o cumple con estrictos estándares de accesibilidad, el editor universal ofrece una solución optimizada para crear y administrar formularios.

![Editor universal](/help/edge/docs/forms/universal-editor/assets/universal-editor.png){width=80%, align-center}

## Funciones principales del editor universal de Edge Delivery Services para formularios



| ![Interfaz WYSIWYG](/help/edge/docs/forms/universal-editor/assets/generate-forms.svg) | ![Editor de reglas](/help/edge/docs/forms/universal-editor/assets/rule-editor.svg) | ![Acciones de envío](/help/edge/docs/forms/universal-editor/assets/submit-actions.svg) |
|:-------------:|:-------------:|:-------------:|
| [**Interfaz WYSIWYG**](/help/edge/docs/forms/universal-editor/universal-editor-user-interface.md) | [**Editor de reglas**](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md) | [**Acciones de envío**](/help/edge/docs/forms/universal-editor/submit-action.md) |
| El editor universal proporciona una interfaz de WYSIWYG para el diseño de formularios con una biblioteca de componentes prediseñada, diseño interactivo, creación con plantillas y modificaciones de campos en tiempo real. | El editor de reglas permite a los usuarios crear interacciones de formulario dinámicas mediante reglas impulsadas por eventos, validación instantánea y administración de errores a través de JavaScript y JSON ligeros. | Las acciones de envío admiten la integración back-end, la lógica de envío condicional, los extremos seguros y los preprocesadores, lo que optimiza los flujos de trabajo de envío. |

| ![Publicación/cancelación de la publicación](/help/edge/docs/forms/universal-editor/assets/publish-unpublish.svg) | ![Modo adaptable](/help/edge/docs/forms/universal-editor/assets/responsive.svg) | ![Componentes personalizados](/help/edge/docs/forms/universal-editor/assets/custom-components.svg) |
|:-------------:|:-------------:|:-------------:|
| [**Publicación/cancelación de la publicación**](/help/edge/docs/forms/universal-editor/publish-forms.md) | [**Modo adaptable**](/help/edge/docs/forms/universal-editor/responsive-layout.md) | [**Componentes personalizados**](/help/edge/docs/forms/universal-editor/create-custom-component.md) |
| Controle fácilmente la visibilidad de los formularios: publíquelos o cancele su publicación directamente desde el editor con solo unos clics. | Diseñe formularios que se adapten sin problemas a todos los dispositivos (equipos de escritorio, tabletas y dispositivos móviles). Utilice el modo interactivo para previsualizar y probar formularios para varios tamaños de pantalla. | Los componentes personalizados permiten a los desarrolladores ampliar las capacidades de los formularios creando elementos únicos adaptados a casos de uso organizativos específicos. |

| ![Estilo](/help/edge/docs/forms/universal-editor/assets/personalization.svg) | ![Servicios de rellenado previo](/help/edge/docs/forms/universal-editor/assets/prefill-services.svg) | ![Pruebas A/B](/help/edge/docs/forms/universal-editor/assets/experimentation-ab-testing.svg) |
|:-------------:|:-------------:|:-------------:|
| [**Estilo**](/help/edge/docs/forms/universal-editor/style-theme-forms.md) | **Servicios de rellenado previo** (próximamente) | [**Pruebas A/B**](https://github.com/adobe/aem-experimentation/blob/main/documentation/experiments.md) |
| Aplicar estilo con CSS permite a los desarrolladores personalizar el aspecto de los elementos del formulario y crear un diseño visualmente atractivo que se ajuste a la estética del sitio web. | Los servicios de rellenado previo completan de forma automática los campos de formulario con datos de usuario relevantes de varias fuentes, lo que reduce la entrada manual y mejora la experiencia del usuario. | Las pruebas A/B permiten a las organizaciones experimentar con diferentes diseños de formulario, diseños y características para identificar las variantes de mejor rendimiento. |

| ![Análisis y seguimiento](/help/edge/docs/forms/universal-editor/assets/analyticsandtracking.svg) | ![Fragmentos de formulario](/help/edge/docs/forms/universal-editor/assets/form-fragments.svg) | ![Enlace de datos](/help/edge/docs/forms/universal-editor/assets/data-binding.svg) |
|:-------------:|:-------------:|:-------------:|
| [**Análisis y seguimiento**](https://www.aem.live/developer/martech-integration) | **Fragmentos de formulario** (próximamente) | [**Enlace de datos**](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md) |
| Obtenga información sobre el comportamiento del usuario, las interacciones de formularios y las tasas de envío con análisis y seguimiento integrados para permitir la optimización de formularios basada en datos. | Los fragmentos de formulario habilitan la reutilización al permitir que las secciones utilizadas comúnmente se creen una vez y se reutilicen en varios formularios, lo que garantiza la coherencia y reduce el esfuerzo de mantenimiento. | El enlace de datos permite conexiones directas entre campos de formulario y fuentes de datos back-end, lo que admite actualizaciones en tiempo real y una asignación de datos avanzada. |

| ![CAPTCHA](/help/edge/docs/forms/universal-editor/assets/captcha.svg) | ![Incorporación de formularios](/help/edge/docs/forms/universal-editor/assets/embedding-forms.svg) | ![Configuración de agradecimiento](/help/edge/docs/forms/universal-editor/assets/thank-you.svg) |
|:-------------:|:-------------:|:-------------:|
| [**CAPTCHA**](/help/edge/docs/forms/universal-editor/recaptcha-forms.md) | **Incorporación de formularios** (próximamente) | [**Configuración de agradecimiento**](/help/edge/docs/forms/universal-editor/submit-action.md#show-a-custom-thank-you-message-on-adaptive-form-submission-submit-action-message-ue) |
| Utilice reCAPTCHA para proteger los formularios de bots automatizados, lo que garantiza una recopilación de datos segura y fiable. | Incruste formularios directamente en las páginas de Sites de Edge Delivery Services mediante el componente incrustado integrado del editor universal. | Personalice con facilidad el mensaje de confirmación o la página que se muestra a los usuarios después de enviar correctamente el formulario. |


<!-- ![Universal Editor](/help/edge/docs/forms/universal-editor/assets/generate-forms.svg)  **WYSIWYG interface for Form creation**: Universal Editor provides a WYSIWYG interface for form design. It provides pre-built component library, responsive design support, and template-based form creation. You can instantly add or remove form fields and modify field properties (like label, data binding, validation). You can also plugin custom form components to Universal Editor.


* **Rule editor**: The rule editor stands out as a powerful mechanism for creating sophisticated form interactions. It supports event-driven rules, instant validation, and error handling through lightweight JavaScript and JSON-based definitions. This allows developers to implement complex form logic, such as conditional field visibility, automatic calculations, and dynamic form behaviour without extensive coding.

* **Submit actions**: Submit Actions enable form submission workflows. These actions provide comprehensive backend integration options, supporting protocols like REST API. The system allows you configure data pre-processors for automatic data transformation, conditional submission logic based on form field values, and secure endpoint connections. Organizations can define complex submission rules that validate data, and manage form responses with granular control.

* **Pre-fill services:** Pre-fill Services enhance user experience by intelligently populating form fields with relevant data. These services connect to various data sources, including user profiles, browser local storage, and external databases. The mechanism supports dynamic data population, enabling automatic completion of form fields based on contextual information. Users benefit from reduced manual data entry, while administrators gain flexibility in configuring pre-fill rules across different form types and scenarios. The pre-fill functionality adapts to different authentication methods, including session-based approaches and token-based systems, ensuring both convenience and security.

* **Data binding capabilities**: Data binding in the Universal Editor enables direct, dynamic connections between form fields and backend data sources. This feature allows real-time synchronization of form data, supporting complex data mapping scenarios. The system supports transforming form inputs into structured database records with minimal configuration. Advanced mapping supports nested data structures, allowing complex form designs to interact seamlessly with intricate data models.

* **Internationalization/localization capabilities**: Internationalization support ensures global accessibility, with multi-language rendering, right-to-left language compatibility, and locale-specific formatting.

* **Analytics and tracking mechanisms**: The built-in analytics and tracking mechanisms provide comprehensive insights into form interactions, submission rates, and user behavior, enabling continuous optimization of form design and performance. 

* **Experimentation (A/B Testing)**: The Universal Editor supports experimentation by allowing organizations to run A/B tests on form designs to identify the best-performing layouts or features.

* **Task Management via Adobe Workfront**: Integration with Adobe Workfront allows teams to manage tasks related to form creation and maintenance, ensuring streamlined collaboration and efficient workflows.

* **Editor Customization via UI Extension**: Developers can extend the functionality of the Universal Editor through UI extensions, enabling tailored solutions that fit specific organizational needs. -->

## Componentes de formulario generados previamente

El editor universal proporciona los siguientes componentes listos para usar de forma predeterminada:

<table>
  <thead>
    <tr>
      <th></th> 
      <th>Componentes de formulario</th>
      <th>Descripción</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="22"><img src="/help/edge/docs/forms/universal-editor/assets/adaptive-forms-components.png" alt="Componentes de formulario" style="width: 100%;"></td> 
      <td><b>Acordeón</b></td>
      <td>Estructura de panel contraíble para organizar el contenido.</td>
    </tr>
    <tr>
      <td><b>Botón</b></td>
      <td>Añade elementos interactivos para acciones como navegación o lógica personalizada.</td>
    </tr>
    <tr>
      <td><b>Captcha</b></td>
      <td>Evita el correo no deseado al exigir a los usuarios que completen una tarea de verificación humana mediante Google reCaptcha o HCaptcha.</td>
    </tr>
    <tr>
      <td><b>Casilla de verificación</b></td>
      <td>Permite a los usuarios configurar una casilla de verificación.</td>
    </tr>
    <tr>
      <td><b>Grupo de casillas de verificación</b></td>
      <td>Permite a los usuarios seleccionar varias opciones de un grupo.</td>
    </tr>
    <tr>
      <td><b>Selector de fecha</b></td>
      <td>Permite a los usuarios seleccionar una fecha mediante una interfaz de calendario.</td>
    </tr>
    <tr>
      <td><b>Listas desplegables</b></td>
      <td>Ofrece opciones de selección única o múltiple de una lista predefinida.</td>
    </tr>
    <tr>
      <td><b>Correo electrónico</b></td>
      <td>Registra direcciones de correo electrónico con validación básica de formato.</td>
    </tr>
    <tr>
      <td><b>Archivo adjunto</b></td>
      <td>Permite cargar documentos, imágenes u otros tipos de archivos.</td>
    </tr>
    <tr>
      <td><b>Fragmentos de formulario</b></td>
      <td>Componentes de formulario reutilizables para secciones como campos de dirección o detalles de contacto.</td>
    </tr>
    <tr>
      <td><b>Imagen</b></td>
      <td>Admite la carga y visualización de imágenes en formularios.</td>
    </tr>
    <tr>
      <td><b>Modal</b></td>
      <td>Muestra un cuadro de diálogo emergente, que suele utilizarse para alertas, información adicional o confirmación.</td>
    </tr>
    <tr>
      <td><b>Campo numérico</b></td>
      <td>Registra la entrada numérica, lo que permite validar números o intervalos.</td>
    </tr>
    <tr>
      <td><b>Panel</b></td>
      <td>Organiza secciones de formulario con paneles expansibles/contraíbles.</td>
    </tr>
    <tr>
      <td><b>Botones de opción</b></td>
      <td>Habilita la selección de opción única de un grupo de opciones.</td>
    </tr>
    <tr>
      <td><b>Clasificación</b></td>
      <td>Permite a los usuarios proporcionar una clasificación basada en estrellas.</td>
    </tr>
    <tr>
      <td><b>Botón Restablecer</b></td>
      <td>Restablece los campos del formulario a su estado predeterminado.</td>
    </tr>
    <tr>
      <td><b>Botón Enviar</b></td>
      <td>Activa el envío de formularios e inicia flujos de trabajo definidos.</td>
    </tr>
    <tr>
      <td><b>Campo de número de teléfono</b></td>
      <td>Registra los números de teléfono con formato basado en el país.</td>
    </tr>
    <tr>
      <td><b>Texto</b></td>
      <td>Proporciona una sección dedicada para mostrar los términos legales y recopilar el acuerdo del usuario a través de las casillas de verificación.</td>
    </tr>
    <tr>
      <td><b>Campo de texto</b></td>
      <td>Captura la entrada de una sola línea, como nombres o direcciones de correo electrónico.</td>
    </tr>
    <tr>
      <td><b>Asistente</b></td>
      <td>Guía a los usuarios paso a paso a través de un proceso de formulario de varias partes.</td>
    </tr>
  </tbody>
</table>

<!-- * Footer: Adds a footer section for consistent design or additional information.
* Form Container: Wraps all form elements and manages overall form properties.
* Header: Adds a header section for form titles, branding, or instructions.-->
<!-- * 
* Prefillable Fields: Automatically populates form fields with data from predefined sources such as user profiles or APIs. 

* Switches/Toggle Buttons: Provides binary on/off choices for user input.


* Title: Adds a text-based heading or label to improve form clarity and organization.


In-addtion to pre-built form components, the Universal editor also provides support for:

* **Embedding Forms in Another Webpage**: The Universal Editor supports embedding forms directly into Edge Deliver Services Sites pages. This can be done using the embed component provided out of the box.

* **Validation Messages**: Validation messages provide real-time feedback to users when they enter incorrect or incomplete data. Features include:
    * Dynamic Error Display: Instantly alerts users to errors, such as invalid email addresses or missing required fields.
    * Customizable Messages: Allows form authors to define user-friendly error texts.
    * Rule-Based Validation: Supports advanced validation logic, such as checking dependencies between fields or implementing conditional rules.

* **Hidden Fields**: Hidden fields store data invisibly within the form, often for backend processing or prefilled values. Use cases include:
    * Passing contextual information (e.g., user ID or session data) to the backend without displaying it to users.
    * Capturing metadata like timestamps or tracking IDs.
    * Hidden fields are not visible to end-users but can be prefilled, updated dynamically, or used in workflows.

* **Custom Components**: Custom components allow developers to extend the functionality of forms by creating specialized or third-party integrations. Features include:
    * Flexibility: Developers can design unique form elements tailored to specific use cases.
    * Third-Party Integration: Embed widgets or tools like payment gateways, analytics trackers, or AI-driven input fields.
    * Seamless Compatibility: Custom components can integrate with the Universal Editor's drag-and-drop interface and existing features like data binding or validation.

* **Thank you Configuration**: Customize the acknowledgment message or page shown after form submission.
-->


## Incorporación

<span class="preview"> Es una función de la versión preliminar y se puede acceder a ella a través de nuestro <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=es#new-features">canal de versiones preliminares</a>. </span>

## Preguntas frecuentes

**P: ¿Quién puede utilizar el editor universal?**
El editor universal está diseñado para una audiencia amplia que incluye:

* Creadores de contenido que deseen crear formularios visualmente atractivos.
* Desarrolladores que necesitan funcionalidades avanzadas de personalización e integración.
* Organizaciones que buscan soluciones de formularios escalables, seguras y compatibles.

**P: ¿Puedo integrar formularios creados con el editor universal en mis sistemas existentes?**
Por supuesto. El editor universal admite el enlace de datos sin problemas con sistemas back-end, lo que permite actualizaciones en tiempo real y asignación de datos avanzada. También se integra con herramientas como Adobe Workfront para la administración de tareas y admite extremos seguros para los flujos de trabajo de envío de datos.

**P: ¿es posible personalizar los componentes del formulario?**
Sí, el editor universal permite a los desarrolladores crear componentes personalizados adaptados a necesidades organizativas específicas. Además, puede ampliar la funcionalidad del editor mediante extensiones de interfaz de usuario y flujos de trabajo personalizados.

**P: ¿Cómo administra la accesibilidad el editor universal?**
El editor universal está diseñado con un estricto cumplimiento de los estándares de accesibilidad, incluidas las WCAG (Directrices de accesibilidad al contenido web). Esto garantiza que las personas con discapacidad puedan utilizar los formularios, lo que proporciona una experiencia inclusiva.

**P: ¿Qué tipo de análisis puedo obtener de los formularios?**
El editor universal incluye herramientas de seguimiento y análisis integradas para monitorizar las interacciones del usuario, las tasas de envío de formularios y las métricas de conversión. Estas perspectivas ayudan a optimizar los formularios para obtener un mejor rendimiento.


## Empezar a crear formularios

{{universal-editor-see-also}}

