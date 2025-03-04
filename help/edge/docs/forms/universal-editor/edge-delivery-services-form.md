---
Title: How Edge Delivery Services Forms work?
Description: This article provides information on how Edge Delivery Services Forms work. It also provides information on various form authoring platforms, including the Universal Editor and document-based authoring.
Keywords: Universal Editor for WYSIWYG authoring, document-based authoring, Working of Edge Delivery Services Forms, How Edge Delivery Services Forms work?
feature: Edge Delivery Services
Role: User, Developer
hide: true
hidefromtoc: true
exl-id: db58ce85-139a-4cc1-8e18-73da76357299
source-git-commit: bb01a76ae2bfd78ae648e91545f34f20fabebd10
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 100%

---


# Formularios de Edge Delivery Services

Los formularios de Adobe Edge Delivery Services transforman la forma en que se crean, ejecutan y procesan los formularios. Al aprovechar Edge Delivery Services, las organizaciones pueden crear formularios digitales rápidos, seguros y de alta disponibilidad, mejorando la experiencia del usuario y la eficacia operativa con un entorno de desarrollo rápido. Con los formularios de Edge Delivery Services, puede impulsar las conversiones, reducir los costes y acelerar el envío de contenido.

## Ventajas de los formularios de Edge Delivery Services

* **Creación más rápida de formularios**: cree formularios de alto rendimiento con una puntuación perfecta de Lighthouse y supervise continuamente su rendimiento real mediante la monitorización de usuarios reales (RUM).

* **Proceso de creación optimizado**: administre fácilmente el contenido de múltiples fuentes para obtener mayor flexibilidad. De forma predeterminada, puede crear formularios utilizando WYSIWYG y la creación basada en documentos, lo que permite una integración perfecta de varios formatos de contenido.

* **Facilidad de uso para usuarios no técnicos**: Edge Delivery Services permite a los usuarios no programadores administrar y publicar fácilmente formularios sin necesidad de tener amplios conocimientos de programación.

* **Mejor experiencia del usuario**: garantice tiempos de carga rápidos e interacciones fluidas, proporcionando a los usuarios tiempos de espera mínimos y una experiencia intuitiva de cumplimentación de formularios.

* **Ejecución sin servidor**: Edge Delivery Services permite la ejecución sin servidor de la lógica del formulario. Esto incluye:

   * **Validación del lado del cliente**: la validación de campos de formulario se produce en el lado del cliente, lo que reduce los retrasos de ida y vuelta.

   * **Rellenado previo y personalización**: el rellenado previo de los datos del formulario se administra en el lado del cliente para una experiencia de usuario perfecta.

   * **Procesamiento de envíos**: los envíos de formularios se validan y se reenvían de forma segura sin un servidor central

## ¿Cómo funcionan los formularios de Edge Delivery Services?

Los usuarios pueden crear formularios de Edge Delivery Services con herramientas de creación basadas en documentos como Google Drive, SharePoint o el editor universal (creación de WYSIWYG), a la vez que aprovechan el estilo, el comportamiento y los componentes básicos disponibles en el repositorio de GitHub. Una vez creados, los formularios de Edge Delivery Services pueden enviar datos a cualquier plataforma mediante el servicio de envío de formularios.

![Funcionamiento de los formularios de Edge Delivery Services](/help/edge/docs/forms/assets/eds-forms-working.png)

### Componentes clave de los formularios de Edge Delivery Services

Los componentes clave de los formularios de Edge Delivery Services son:

* **Repositorio de GitHub**: el repositorio de GitHub sirve como modelo para crear formularios de Edge Delivery Services. Los formularios aprovechan el estilo y la funcionalidad básicos del repositorio y permiten a los usuarios añadir personalizaciones y componentes personalizados a los formularios de Edge Delivery Services.

* **Creación de formularios**: los formularios de Edge Delivery Services admiten dos tipos de creación: WYSIWYG y la creación basada en documentos. La creación basada en documentos permite a los usuarios crear formularios utilizando herramientas conocidas como Google Docs y Microsoft Office. La creación de WYSIWYG permite a los usuarios diseñar formularios de forma visual mediante el editor universal, lo que facilita a los usuarios sin conocimientos técnicos la creación y administración de formularios. Universal Editor ofrece una experiencia de creación de formularios intuitiva y proporciona acceso a numerosas funciones de formulario.

* **Servicio de envío de formularios**: El servicio de envío de formularios le permite almacenar datos de los envíos de formularios en cualquier plataforma, como OneDrive, SharePoint o Hojas de cálculo de Google, lo que facilita el acceso y la administración de los datos de formulario en su sistema preferido.

## Creación de un formulario

Adobe Experience Manager ofrece y admite varios editores para crear un formulario. Puede utilizar lo siguiente:
* [Editor universal (para la creación de WYSIWYG)](#universal-editor-for-wysiwyg-authoring)
* [Microsoft Excel u Hojas de cálculo de Google (conocidas como Creación basada en documentos)](#microsoft-excel-or-google-sheets-known-as-document-based-authoring)

### Editor universal (para la creación de WYSIWYG)

El editor universal es un editor visual versátil que ofrece una función WYSIWYG (what-you-see-is-what-you-get), lo que garantiza una experiencia de creación de formularios intuitiva. Se recomienda utilizar el editor universal para crear nuevos formularios, ya que ofrece un diseño moderno y fácil de usar, así como una interfaz práctica de arrastrar y soltar.

Para crear formularios con el editor universal, se utilizan las plantillas de Edge Delivery Services disponibles en el entorno de AEM. Estos formularios heredan la apariencia de las configuraciones del repositorio de GitHub de Edge Delivery Services. [Para habilitar la publicación de estos formularios en Edge Delivery Services, se ha establecido una conexión entre su entorno de AEM y el repositorio de GitHub de Edge Delivery Services](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md).

Para obtener más información sobre cómo crear con el editor universal, consulte el artículo [Creación de contenido con el editor universal.](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/sites/authoring/universal-editor/authoring)

### Microsoft Excel u Hojas de cálculo de Google (conocidas como Creación basada en documentos)

Puede crear los formularios utilizando la creación basada en documentos con archivos de Microsoft Excel o de Hojas de cálculo de Google, lo que le permite aprovechar los sólidos ecosistemas y las API de las Hojas de cálculo de Google, Microsoft Excel y Microsoft SharePoint. Este método es especialmente útil para crear formularios simples sin servicios de envío avanzados.

Para empezar a crear un formulario mediante Microsoft Excel u Hojas de cálculo de Google, [configure un proyecto de AEM usando el elemento repetitivo de AEM Forms](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) y clone el repositorio de GitHub correspondiente en su equipo local. AEM Forms Edge Delivery proporciona una característica denominada bloque de formularios adaptables, que simplifica el proceso de creación de formularios para capturar y almacenar datos. Para aprender a crear y publicar formularios utilizando el bloque de formularios adaptables en Edge Delivery Services, consulte [Crear un formulario](/help/edge/docs/forms/create-forms.md).

<!--
## Adaptive Forms editors (for Core Components or foundation components based authoring)

You can author forms that are engaging, responsive and dynamic. The Adaptive Form editor provides a user-friendly wizard that allows you to quickly create Adaptive Forms. The form wizard features easy tab navigation, enabling you to select pre-configured templates for foundation or core components, themes, data models, and submission options to create a form efficiently. 

[Authoring forms with Core Components](/help/forms/creating-adaptive-form-core-components.md) allows you to leverage standardized data capture components that can be customized, reducing development time and lowering maintenance costs for digital enrollment experiences. These forms can be published using the Adaptive Forms Block on Edge Delivery Services or through the AEM Publish instance. 

[Authoring forms with Foundation Components](/help/forms/create-an-adaptive-form.md) uses classic data capture components. These forms can only be published using the AEM Publish instance. 

You can also publish forms created using Adaptive Forms Editors on Edge Delivery Services by establishing [connection between your AEM environment and the Edge Delivery Services GitHub repository](/help/edge/docs/forms/publishing-forms.md).


| **Adaptive Forms editors** | Provides a wizard-driven approach to quickly start forms authoring using templates, styling, and predefined fields. | Use these editors to create Core Components based forms or Foundation Components based forms. | These forms can be published on Edge Delivery Services or via AEM Publish instances.  | Use these editors to create Core Components based forms or Foundation Components based forms. Ideal for scenarios involving complex forms, complex workflows, custom actions, or integrations with external systems. |  



## Types of Publishing for Edge Delivery Services Forms

You can publish Edge Delivery Services Forms on one of the following:

* **Edge Delivery Services Form Submission**: Edge Delivery Services Form Submissions ensure that form interactions, including submission and data processing, are handled efficiently and securely. This enables a faster and more reliable user experience, particularly during high traffic periods. By processing form submissions at the edge, Edge Delivery Services minimizes the reliance on a centralized server.

* **AEM Publish instance**: The AEM Forms server offers a publish instance that manages the forms and related assets available to end users.
-->

### ¿Cómo elegir entre varios tipos de creación de formularios?

En la siguiente tabla se describen las funciones y los casos de uso de cada editor de creación, lo que le ayuda a elegir el adecuado según sus necesidades y los envíos de formularios.

| **Editor de creación de formularios** | **Enfoque clave** | **Funciones** | **Método de publicación** | **Casos de uso** |
|--------|-----------|-------|-------|------------------------------------------------|
| **Creación basada en documentos** | Aprovecha herramientas conocidas como Google Docs y Microsoft Office para crear formularios. | Los formularios se han diseñado utilizando hojas de cálculo, con datos enviados directamente a las hojas de Google o a las hojas de Microsoft Excel. </br> </br>: Estos formularios son más rápidos de crear e implementar. No es necesario tener conocimientos previos de AEM para desarrollar componentes y estilos personalizados para estos formularios. | Estos formularios se publican en Edge Delivery Services y tienen una puntuación muy alta en Google Lighthouse. </br> </br> La puntuación más alta se traduce en un procesamiento más rápido y una mejor optimización de los motores de búsqueda. | Estos formularios son ideales para crear prototipos rápidos o formularios básicos en los que no se necesitan servicios de envío avanzados. </br> </br>: Estos formularios son adecuados para encuestas, formularios de registro o de comentarios que requieren almacenamiento de datos en hojas de cálculo. Estos formularios se publican en Edge Delivery Services |
| **Editor universal**  </br> </br> Si está creando un nuevo formulario, use el editor universal para crear formularios. | Ofrece una interfaz WYSIWYG para la creación intuitiva de formularios. | Los formularios se han diseñado mediante una interfaz intuitiva de arrastrar y soltar. </br> </br> Estos formularios toman prestada la apariencia del repositorio de GitHub de Edge Delivery Services configurado para el formulario correspondiente. | Estos formularios se publican en Edge Delivery Services y tienen una puntuación muy alta en Google Lighthouse. </br> </br> La puntuación más alta se traduce en un procesamiento más rápido y una mejor optimización de los motores de búsqueda. | Estos formularios son ideales para crear formularios para sitios y páginas de Edge Delivery Service. Son escenarios de formularios que implican formularios complejos, flujos de trabajo complejos, acciones personalizadas o integraciones con sistemas externos |

>[!NOTE]
>
>
> Si encuentra que falta alguna función en el editor universal que antes estaba disponible en el editor de formularios adaptables, puede solicitarla enviando un correo electrónico a mailto:aem-forms-ea@adobe.com con su dirección de correo electrónico oficial.

## Véase también

{{see-more-forms-eds}}
