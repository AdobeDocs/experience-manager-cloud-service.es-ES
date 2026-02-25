---
title: Trabajo de creación de formularios
description: Obtenga información sobre el trabajo de creación de formularios de Brand Experience Agent y cómo utilizar el lenguaje natural para crear formularios desde cero.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: 24ad5f36-405b-4ea2-9819-de6aea856a7a
source-git-commit: 71e3770a7a26b8d3144717513f3ec1c997b3b435
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---


# Trabajo de creación de formularios {#form-creation-job}

El trabajo de creación de formularios es una funcionalidad de [Brand Experience Agent](/help/ai-in-aem/agents/brand-experience/overview.md) que está diseñada para desarrollar formularios utilizando indicaciones en lenguaje natural. Este trabajo genera automáticamente la estructura de formulario y los tipos de campo adecuados. El trabajo se muestra mediante el Asistente de IA.

Algunas de las ventajas clave del trabajo de creación de formularios son:

* **Desarrollo acelerado de formularios**: cree formularios rápidamente utilizando comandos sencillos de lenguaje natural, lo que elimina la necesidad de aprender interfaces de productos tradicionales.
* **Experiencias coherentes y sin marca**: Cree formularios que sigan las directrices de estilo, plantillas y marca de su organización utilizando plantillas y estilos aprobados.
* **Reducir la barrera técnica**: permita a los usuarios empresariales crear formularios fácilmente, sin necesidad de tener conocimientos técnicos avanzados o una amplia experiencia en el producto.

## Capacidades {#capabilities}

* **Crear un nuevo formulario con solicitud de texto sin formato**: puede crear un formulario enviando los requisitos en un idioma sin formato. La aptitud genera automáticamente la estructura de formulario, los tipos de campo y las experiencias en la marca adecuados en función de la descripción del idioma natural y la plantilla especificada. Esta capacidad acelera la creación de formularios a la vez que garantiza que se mantengan los estándares de conformidad y marca.

* **Importar un documento de PDF y convertirlo en formulario**: puede importar y transformar documentos de PDF existentes en formularios. La aptitud analiza el contenido cargado para detectar tipos de campo, conservar diseños y mejorar los formularios con una lógica de validación y diseño adaptable, a la vez que garantiza que se mantengan los estándares de conformidad y marca.

Cuando utilice cualquiera de estas funciones, se le pedirá que elija el tipo de formulario que desea crear. Especifique una plantilla de formulario adaptable basada en componentes principales o una plantilla de formulario adaptable basada en Edge Delivery Services e indique la ruta preferida para guardar el formulario. Si está creando un formulario basado en Edge Delivery Services, también puede especificar la dirección URL de GitHub del repositorio.


### Indicadores de ejemplo {#sample-prompts}

* *Crear un formulario para la colección de comentarios con campos de nombre, correo electrónico y mensaje*
* *Cree un formulario de comentarios para clientes con una clasificación de productos (de 1 a 5 estrellas), un campo de comentarios y un correo electrónico opcional*
* *Cree un formulario de contacto con los campos nombre, correo electrónico, asunto, lista desplegable y mensaje*
* *Cree un formulario de registro con información personal, preferencias de cuenta y aceptación de términos*
* *Cree un formulario de solicitud de tarjeta de crédito importando el archivo PDF disponible en`https://[aem-author-url]/path/to/pdf/file`*
* *Cree un formulario de comentarios usando la repetidor en`https://github.com/wkndforms/wesecure`*

## Acotamiento del formulario {#refine-with-forms-experience-builder}

Después de crear la estructura del formulario inicial con el Asistente para IA, puede utilizar Forms Experience Builder para lo siguiente:

* **Actualizar formularios**: agregue o modifique campos, ajuste tipos de campos y actualice el estilo según sea necesario mediante el editor visual.

* **Actualizar diseño**: reorganice secciones, grupos o campos, ajuste el espaciado y modifique la jerarquía visual para mejorar la facilidad de uso y garantizar que el formulario sea claro e intuitivo para su audiencia.

* **Agregar lógica empresarial**: cree lógica condicional, muestre u oculte reglas, dependencias de campo y defina reglas de validación.

* **Configurar envío**: configure dónde se envían los datos del formulario, incluida la configuración de notificaciones por correo electrónico, integraciones con flujos de trabajo o conexiones a sistemas externos.

Para obtener más información, consulte [Documentación de Forms Experience Builder.](/help/forms/experience-builder/product-overview.md)


## Activación {#activation}

Para habilitar el trabajo de creación de formularios para su organización, la activación debe iniciarse mediante Adobe. Inicie el proceso poniéndose en contacto mediante:

* Correo electrónico: `experience-production-agent@adobe.com`
* O bien, póngase en contacto con el equipo de cuenta de Adobe designado.

Cuando contacte con, asegúrese de proporcionar su ID de organización de AEM as a Cloud Service.

<!-- 
#### Import and convert {#import-and-convert}

Transform existing documents into interactive digital forms. The agent analyzes uploaded content to detect field types, preserve layouts, and enhance forms with responsive design and validation logic. Supported formats include Acroforms, XFA PDFs, flat PDFs, images (JPG, PNG), and hand-drawn form photographs.

>[!VIDEO](https://video.tv.adobe.com/v/3474042)

**Prompt examples:**

* *Convert the attached PDF file to an adaptive form*
* *Transform this scanned form image into an interactive digital form*
* *Import the employee onboarding PDF and create an editable form*
* *Convert this paper form photograph into a digital form with validation*
-->

<!-- 
### Embed an existing form to a sites page {#embed-existing-form}

The form creation skill enables seamless integration of existing forms into any sites page through natural language commands. Rather than manually locating, copying, and embedding form components, users can simply specify which form to add and where to place it. The agent handles the technical implementation, ensuring proper rendering and functionality.

>[!VIDEO](https://video.tv.adobe.com/v/PLACEHOLDER)

**Prompt examples:**

* *Embed the contact form to the homepage*
* *Add the existing customer feedback form to the support page*
* *Insert the newsletter signup form into the footer section*
* *Place the registration form on /content/site/signup*
* *Add form "contact-us-2024" to the current page*
-->

<!-- 
### Build and add a form to an existing sites page {#build-and-add-form}

The form creation skill combines form creation and site integration in a single conversational workflow. Users can describe the form they need and specify where to add it, and the agent creates the form and embeds it into the specified page automatically. This eliminates the traditional multi-step process of creating a form separately and then manually adding it to a page.

>[!VIDEO](https://video.tv.adobe.com/v/PLACEHOLDER)

**Prompt examples:**

* *Create a newsletter signup form with email field and add it to the footer*
* *Build a quick contact form with name, email, and message, then add it to /content/about-us*
* *Add a feedback form with rating stars and comment field to this page*
* *Create a simple survey form with 5 questions and embed it on the customer portal homepage*
* *Build an event registration form with name, email, and date selection, then add it to /content/events/conference-2025*
-->
