---
title: ¿Cómo se crean formularios en AEM?
description: Obtenga información sobre las distintas plataformas de creación de formularios disponibles en Adobe Experience Manager (AEM) y cómo elegir la correcta según sus requisitos.
feature: Edge Delivery Services, Adaptive Forms, Core Components
role: User, Developer
exl-id: bd9cb623-c272-4cdf-ad39-f97043f781a6
hide: true
hidefromToC: true
source-git-commit: 1662d1c9458f05c2e511514ce8a04247da90eaf3
workflow-type: ht
source-wordcount: '1075'
ht-degree: 100%

---

# ¿Cómo se crean formularios en Adobe Experience Manager (AEM)?

Adobe Experience Manager (AEM) proporciona una plataforma flexible para crear formularios atractivos, interactivos, dinámicos y adaptables. Ofrece una interfaz de usuario intuitiva y un conjunto completo de componentes predeterminados para crear y administrar formularios adaptables. Los formularios se pueden crear con o sin un modelo o esquema de formulario, según sus necesidades.

## Consideraciones clave a la hora de elegir una plataforma de creación

AEM ofrece varias opciones de creación de formularios para crear formularios interactivos y atractivos. Al seleccionar un entorno de creación de formularios, tenga en cuenta los siguientes factores:

| 📝 **Consideración** | 💡 **Qué preguntar** |
|----------------------|--------------------|
| **Experiencia del usuario** | ¿Quién creará los formularios: desarrolladores, usuarios empresariales o autores de contenido? |
| **Complejidad del formulario** | ¿El formulario necesita reglas avanzadas, secciones dinámicas o integraciones? |
| **Necesidades de reutilización** | ¿Se reutilizarán partes del formulario en diferentes formularios o proyectos? |
| **Flexibilidad de diseño** | ¿Necesita control total sobre el diseño, las temáticas y el estilo? |
| **Requisitos de integración** | ¿El formulario debe conectarse a modelos de datos, flujos de trabajo o sistemas externos? |
| **Facilidad de uso** | ¿La plataforma es intuitiva para el nivel de aptitud técnica de su equipo? |
| **Rendimiento y escalabilidad** | ¿Se utilizará el formulario a escala o en entornos de alto tráfico? |
| **Envío omnicanal** | ¿El formulario se utilizará en sitios web, aplicaciones móviles, quioscos o en varios canales? |
| **Flexibilidad de publicación** | ¿Dónde se publicarán los formularios en AEM, Edge Delivery o en aplicaciones personalizadas? |

## Información general sobre los métodos de creación de formularios en AEM

AEM admite varios métodos de creación, cada uno de los cuales se adapta a diferentes necesidades del usuario, niveles de aptitud técnica y destinos de publicación.

* [Componentes de base](/help/forms/create-adaptive-form-tutorial.md): utilice componentes de base para generar formularios tradicionales e interactivos. Son ideales para formularios que se integran con sistemas heredados o que dependen de flujos de trabajo establecidos desde hace mucho tiempo. Los formularios creados con componentes de base solo se pueden publicar en AEM y no son compatibles con Edge Delivery Services.

* [Componentes principales](/help/forms/creating-adaptive-form-core-components.md): utilice los componentes principales para crear formularios modernos, adaptables y escalables. Son reutilizables, accesibles y ofrecen un mejor rendimiento. Los formularios creados con componentes principales se puede publicar tanto en AEM como en Edge Delivery Services, lo que ofrece flexibilidad en todas las plataformas.

* [Formularios de Adobe Edge Delivery Services](/help/edge/docs/forms/overview.md): transforman la forma en que se crean, ejecutan y procesan los formularios. Al aprovechar Edge Delivery Services, las organizaciones pueden crear formularios digitales rápidos, seguros y de alta disponibilidad, mejorando la experiencia del usuario y la eficacia operativa con un entorno de desarrollo rápido. Puede crear formularios de Edge Delivery Services de las dos formas siguientes:
   * [Creación WYSIWYG](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md): utilice el editor universal para crear formularios visuales y de arrastrar y soltar, ideales para autores de contenido con conocimientos técnicos limitados. Los formularios creados con el editor universal se envían con Edge Delivery Services para un renderizado rápido y ligero.
   * [Creación basada en documentos](/help/edge/docs/forms/tutorial.md): utilice herramientas como Microsoft Excel o las Hojas de cálculo de Google para definir la estructura y el contenido del formulario. Este método es útil para los usuarios empresariales que prefieren la entrada basada en hoja de cálculo. Estos formularios se publican normalmente a través de Edge Delivery Services y son adecuados para casos de uso ligeros y de gran volumen.
* [Creación sin encabezado](https://experienceleague.adobe.com/es/docs/experience-manager-headless-adaptive-forms/using/tutorial/build-engaging-forms-using-core-components-and-headless-adaptive-forms-aem-forms-cloud-service): utilice las API para procesar formularios en formato JSON para cualquier front-end, por ejemplo, React, Angular, aplicaciones móviles o quioscos, sin depender de AEM. Actualmente, solo los componentes principales admiten el envío sin encabezado. Los formularios sin encabezado son ideales para casos de uso omnicanal, y se consumen independientemente del renderizado de las páginas de AEM, lo que los hace flexibles para implementaciones front-end personalizadas.

### Análisis comparativo de los métodos de creación de formularios de AEM

La siguiente tabla ofrece una comparación concisa de varios métodos de creación de formularios de AEM, destacando los enfoques, las características, las opciones de publicación y los casos de uso ideales para ayudarle a seleccionar el método más adecuado para sus necesidades.

| **Consideración** | **Componentes de base** | **Componentes principales** | **Editor universal (WYSIWYG)** | **Creación basada en documentos** | **Creación sin encabezado** |
|--------------------------|---------------------------------------------------------------------|------------------------------------------------------------------------|-------------------------------------------------------------------------|---------------------------------------------------------------------------|-------------------------------------------------------------------------|
| **Ideal para** | Mantener formularios y flujos de trabajo heredados en AEM | Formularios escalables y modernos con flujos de trabajo e integraciones complejos | Creación de formularios para sitios de Edge Delivery Services con requisitos complejos | Crear rápidamente prototipos para formularios básicos sin servicios avanzados de envío | Experiencias omnicanal en plataformas (web, móvil, quioscos, etc.) |
| **Experiencia del usuario** | Desarrolladores, autores de contenido | Desarrolladores, autores avanzados | Usuarios empresariales, autores de contenido | Usuarios empresariales | Desarrolladores |
| **Complejidad del formulario** | Formularios básicos | Formularios complejos con secciones dinámicas | Formularios complejos con acciones personalizadas | Formularios simples | Formularios muy complejos basados en la API |
| **Flexibilidad de diseño** | Limitado | Alto (personalización de CSS/JS) | Moderado (basado en las plantillas) | Limitado | Alto (control de marco de trabajo front-end) |
| **Capacidad de integración** | Flujos de trabajo básicos de AEM | Avanzados (modelos de datos, flujos de trabajo) | Integrado con sistemas externos | Básico (Google Sheets, Excel) | Control total mediante las API |
| **Método de publicación** | Solo AEM | AEM y Edge Delivery Services | Edge Delivery Services | Edge Delivery Services | Cualquier front-end a través de las API |
| **Rendimiento y SEO** | Estándar | Mejorados con respecto a los componentes base | Altas puntuaciones en Google Lighthouse para un renderizado más rápido y una mejor SEO | Altas puntuaciones en Google Lighthouse para un renderizado más rápido y una mejor SEO | Depende de la implementación |
| **Envío omnicanal** | Limitado | Moderado | Moderado | Limitado | Alto |

<!--
| **Form authoring methods** | **Key Approach** | **Features** | **Publishing Method** | **Use Cases** |
|-----------------------------|------------------|--------------|-----------------------|---------------|
| **Foundation Components** | Classic AEM authoring interface designed for standard web pages. | Includes basic components like text, images, tables, and charts. Limited reuse capabilities and primarily web-based. | Published on AEM only. | Best for maintaining legacy forms and workflows within AEM. |
| **Core Components** | Provides a modern, flexible approach with high customization capabilities. | Component-based authoring within AEM, offering high customization with CSS and JS. Built around accessibility guidelines and integrated with AEM Sites. | Published on AEM and Edge Delivery Services. | Suitable for scalable, modern forms with complex workflows and integrations. |
| **Universal Editor (WYSIWYG)** | Offers a WYSIWYG interface for intuitive form creation. | Forms are designed using an intuitive drag-and-drop interface. These forms inherit look and feel from the configured Edge Delivery Services GitHub repository for the corresponding form. | Published on Edge Delivery Services, achieving high Google Lighthouse scores for faster rendering and better SEO. | Ideal for creating forms for Edge Delivery Service sites and pages, especially scenarios involving complex forms, workflows, custom actions, or integrations with external systems. |
| **Document-based Authoring** | Uses familiar tools like Google Docs and Microsoft Office for form creation. | Forms are designed using spreadsheets, with data directly submitted to Google Sheets or Microsoft Excel. These forms are faster to create and deploy. No prior knowledge of AEM is required to develop custom components and styles for these forms. | Published on Edge Delivery Services, achieving high Google Lighthouse scores for faster rendering and better SEO. | Ideal for quick prototyping or basic forms where advanced submission services are not needed. Well-suited for surveys, registration, or feedback forms requiring data storage in spreadsheets. |
| **Headless Authoring** | Enables API-driven content creation for omnichannel delivery. | Full control via frontend frameworks, allowing content delivery across various platforms through APIs. | Can be integrated with any frontend via APIs. | Ideal for omnichannel experiences across platforms, suitable for web, mobile, kiosks, and more. |-->

### Comparación de características de los métodos de creación de formularios de AEM

En la siguiente tabla se ofrece una comparación detallada de las características clave de los distintos métodos de creación de formularios de AEM, lo que le ayudará a seleccionar el método más adecuado para sus necesidades.

| **Capacidad** | **Componentes de base** | **Componentes principales** | **Editor universal (WYSIWYG)** | **Creación basada en documentos** | **Creación sin encabezado** |
|-----------------------------------------|---------------------------|---------------------|-------------------------------|-----------------------------|------------------------|
| **Composición unificada con Sites** | ❌ | ✅ | ✅ | ❌ | ❌ |
| **Compatible con la incorporación de formularios** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **Reglas (comportamiento dinámico)** | Editor de reglas avanzadas con funciones personalizadas | Editor de reglas avanzadas con funciones personalizadas | Editor de reglas avanzadas con funciones personalizadas | Limitado: mostrar/ocultar, calcular valor, funciones personalizadas | Limitado: requiere implementación personalizada |
| **Compatible con los archivos adjuntos** | ✅ | ✅ | ✅ | ℹ   (Acceso anticipado) | ❌ |
| **Compatibilidad con CAPTCHA** | reCAPTCHA v2/Enterprise, hCaptcha (EA), Turnstile (EA) | reCAPTCHA v2/Enterprise, Captcha (EA) | reCAPTCHA Enterprise | reCAPTCHA Enterprise | Requiere una integración personalizada |
| **Características de envío** | Punto final REST, correo electrónico, modelo de datos de formulario (FDM), invocar flujo de trabajo de AEM, SharePoint, OneDrive, Azure Blob Storage, Power Automate, Workfront Fusion (EA) | Punto final REST, correo electrónico, modelo de datos de formulario (FDM), invocar flujo de trabajo de AEM, SharePoint, OneDrive, Azure Blob Storage, Power Automate, Workfront Fusion (EA) | Punto final REST, correo electrónico, modelo de datos de formulario (FDM), invocar flujo de trabajo de AEM, SharePoint, OneDrive, Azure Blob Storage, Power Automate, Workfront Fusion (EA) | Solo hoja de cálculo | Puntos finales de API personalizados |
| **Esquema de datos** | FDM, personalizado | FDM, personalizado | FDM, personalizado | Personalizado | Personalizado |
| **Relleno previo** | ✅ | ✅ | 💡 (a través del asistente) | ✅ | Implementación personalizada |
| **Fragmentos** | ✅ | ✅ | ✅ | ✅ | ❌ |
| **Editor de reglas visuales** | ✅ | ✅ | ✅ | ❌ | ❌ |
| **Localización** | ✅ | ✅ | 💡 (a través de Sites) | ℹ️ (Excel: manual, función de hojas de Google) | Implementación personalizada |
| **Esquema de datos (árbol de datos)** | ✅ | ✅ | 💡 (a través de la extensión de la IU) | ❌ | Implementación personalizada |
| **Compatible con plantillas** | ✅ | ✅ | Solo contenido inicial, sin directivas | ❌ | Implementación personalizada |
| **Portal** | ✅ | ✅ | ❌ | ❌ | ❌ |
| **Creación de DoR** | ✅ | ✅ | 💡 (a través de Derlina) | ❌ | ❌ |
| **Generación de DoR** | ✅ | ✅ | 💡 (Nuevo: FORMS-2475) | ❌ | ❌ |
| **Tema** | ✅ | ✅ | ℹ️ (a nivel de proyecto) | ℹ️ (a nivel de proyecto) | Implementación personalizada |
| **Componente personalizado** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **OOTB y funciones personalizadas** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **Referencia al fragmento** | ✅ | ❌ | ❌ | ❌ | ❌ |
| **Integración a Sign** | ✅ | ❌ | ❌ | ❌ | ❌ |
| **Compatibilidad con RTL** | ❌ | ✅ | 💡 | 💡 | Implementación personalizada |
| **Experimentación** | ❌ | ❌ | ✅ | ✅ | Implementación personalizada |
| **Administración de tareas mediante Workfront** | ❌ | ❌ | ✅ | ❌ | ❌ |
| **Extensión de la personalización** | ❌ | ❌ | 💡 | ❌ | Implementación personalizada |
| **Personalización del editor** | ❌ | ❌ | ✅ (a través de la extensión de la IU) | ❌ | Implementación personalizada |
| **Acción de envío** | ✅ | ✅ | ✅ | Solo hoja de cálculo | Implementación personalizada |


## Artículo relacionado

* [Creación basada en documentos mediante Microsoft Excel u Hojas de cálculo de Google](/help/edge/docs/forms/create-forms.md)
* [Editor universal para la creación de WYSIWYG](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring)
* [Creación de un formulario adaptable (componentes básicos)](/help/forms/creating-adaptive-form.md)
* [Creación de un formulario adaptable (componentes principales)](/help/forms/create-an-adaptive-form.md)
