---
title: Aptitud para la creación de formularios
description: Obtenga información acerca de las habilidades de creación de formularios de Experience Production Agent y cómo utilizar el lenguaje natural para crear formularios desde cero.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: d5b7a8343551c5880b40c692266f33a1864f9d2b
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---


# Aptitud de creación de formularios {#form-creation-skill}

La aptitud para la creación de formularios es una capacidad de Experience Production Agent que está diseñada para desarrollar formularios utilizando indicadores de lenguaje natural. Esta aptitud genera automáticamente la estructura de formulario y los tipos de campo adecuados. La aptitud se muestra a través del asistente de IA.

Algunas de las ventajas clave de la aptitud para la creación de formularios son las siguientes:

* **Desarrollo acelerado de formularios**: cree formularios rápidamente con
comandos sencillos de lenguaje natural, lo que elimina la necesidad de aprender interfaces de producto tradicionales.
* **Experiencias coherentes y sin marca**: Cree formularios que sigan las directrices de estilo, plantillas y marca de su organización utilizando plantillas y estilos aprobados.
* **Reducir la barrera técnica**: permite a los usuarios empresariales crear formularios fácilmente, sin necesidad de tener conocimientos técnicos avanzados o profundos sobre el producto.

## Capacidades {#capabilitiess}

* **Crear un nuevo formulario con solicitud de texto sin formato**: puede crear experiencias de formulario sin marca enviando sus requisitos en un idioma sin formato.

* **Importar un PDF o una imagen y convertirla en un formulario**: puede importar y transformar imágenes existentes o documentos de PDF en formularios. El agente analiza el contenido cargado para detectar tipos de campos, conservar diseños y mejorar los formularios con una lógica de validación y diseño adaptable. Los formatos admitidos son Acroforms, PDF XFA, PDF planos, imágenes (JPG, PNG) y fotografías de formularios dibujados a mano.

  Cuando utilice cualquiera de las funciones anteriores, se le pedirá que elija el tipo de formulario que desea crear, especifique una plantilla de formulario adaptable basada en los componentes principales o una plantilla de formulario adaptable basada en Edge Delivery Services, y que indique la ruta preferida para guardar el formulario. Si está creando un formulario basado en Edge Delivery Services, también puede especificar la dirección URL de GitHub del repositorio.


### Ejemplos de peticiones de datos {#sample-prompts}

* *Crear un formulario para la colección de comentarios con campos de nombre, correo electrónico y mensaje*
* *Cree un formulario de comentarios para clientes con una clasificación de productos (de 1 a 5 estrellas), un campo de comentarios y un correo electrónico opcional*
* *Cree un formulario de contacto con los campos nombre, correo electrónico, asunto, lista desplegable y mensaje*
* *Cree un formulario de registro con información personal, preferencias de cuenta y aceptación de términos*
* *Cree un formulario de solicitud de tarjeta de crédito importando el archivo PDF disponible en &#39;https://[aem-author-url]/path/to/pdf/file*
* *Crear un formulario de comentarios usando la repetidor en &#39;<https://github.com/wkndforms/wesecure>&#39;*

## Próximos pasos {#refine-with-forms-experience-builder}

Después de crear la estructura del formulario inicial mediante el Asistente de IA, puede utilizar la extensión de creación de Forms para lo siguiente:

* **Actualizar formularios**: agregue o modifique campos, ajuste tipos de campos y actualice el estilo según sea necesario mediante el editor visual.

* **Actualizar diseño**: reorganice secciones, grupos o campos, ajuste el espaciado y modifique la jerarquía visual para mejorar la facilidad de uso y garantizar que el formulario sea claro e intuitivo para su audiencia.

* **Agregar lógica empresarial**: cree lógica condicional, muestre u oculte reglas, dependencias de campo y defina reglas de validación.

* **Configurar envío**: configure dónde se envían los datos del formulario, incluida la configuración de notificaciones por correo electrónico, integraciones con flujos de trabajo o conexiones a sistemas externos.

Para obtener más información, consulte [Documentación de Forms Experience Builder](/help/forms/experience-builder/product-overview.md).

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
