---
title: ¿Cómo se crean formularios en AEM?
description: Obtenga información sobre las distintas plataformas de creación de formularios disponibles en Adobe Experience Manager (AEM) y cómo elegir la correcta según sus necesidades.
feature: Edge Delivery Services, Adaptive Forms, Core Components
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: f6c6b4c17482eb519fb0d4287704d775d0a5da00
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 12%

---


# ¿Cómo se crea Forms en Adobe Experience Manager (AEM)?

Adobe Experience Manager (AEM) proporciona una plataforma flexible para crear formularios atractivos, interactivos, dinámicos y adaptables. Ofrece una interfaz de usuario intuitiva y un completo conjunto de componentes predeterminados para crear y administrar Forms adaptable. Forms se puede crear con o sin un modelo o esquema de formulario, según sus necesidades.

## Consideraciones clave al elegir una plataforma de creación

AEM proporciona varias opciones de creación de formularios para crear formularios interactivos y atractivos. Al seleccionar un entorno de creación de formularios, tenga en cuenta los siguientes factores:

| ?? **Consideración** | ?? **Qué preguntar** |
|----------------------|--------------------|
| **Experiencia del usuario** | ¿Quién creará los formularios: desarrolladores, usuarios empresariales o autores de contenido? |
| **Complejidad de formulario** | ¿El formulario necesita reglas avanzadas, secciones dinámicas o integraciones? |
| **Necesidades de reutilización** | ¿Se reutilizarán partes del formulario en diferentes formularios o proyectos? |
| **Flexibilidad de diseño** | ¿Necesita control total sobre el diseño, las temáticas y el estilo? |
| **Requisitos de integración** | ¿El formulario debe conectarse a modelos de datos, flujos de trabajo o sistemas externos? |
| **Facilidad de uso** | ¿Es la plataforma intuitiva para el nivel de habilidad técnica de su equipo? |
| **Rendimiento y escalabilidad** | ¿Se utilizará el formulario a escala o en entornos de alto tráfico? |
| **Envío omnicanal** | ¿Se utilizará el formulario en sitios web, aplicaciones móviles, quioscos o en varios canales? |
| **Flexibilidad de publicación** | ¿Dónde se publicarán los formularios en AEM, Edge Delivery o aplicaciones personalizadas? |

## Información general sobre los métodos de creación de formularios en AEM

AEM admite varios métodos de creación, cada uno de los cuales se adapta a diferentes necesidades del usuario, niveles de aptitud técnica y destinos de publicación.

* [Componentes de base](/help/forms/create-adaptive-form-tutorial.md): use Componentes de base para generar formularios tradicionales e interactivos. Ideal para formularios que se integran con sistemas heredados o que dependen de flujos de trabajo establecidos desde hace mucho tiempo. Forms creado con componentes de base se puede publicar solo en AEM y no es compatible con Edge Delivery Services.

* [Componentes principales](/help/forms/creating-adaptive-form-core-components.md): use los componentes principales para crear formularios modernos, adaptables y escalables. Admiten reutilización, accesibilidad y un mejor rendimiento. Forms creado con componentes principales se puede publicar tanto en AEM como en Edge Delivery Services, lo que ofrece flexibilidad en todas las plataformas.

* [Edge Delivery Services Forms](/help/edge/docs/forms/overview.md): Edge Delivery Services Forms transforma la forma en que se crean, ejecutan y procesan los formularios. Al aprovechar Edge Delivery Services, las organizaciones pueden crear formularios digitales rápidos, seguros y de alta disponibilidad, mejorando la experiencia del usuario y la eficacia operativa con un entorno de desarrollo rápido. Puede crear el Forms de Edge Delivery Services de dos formas:
   * [Creación en WYSIWYG](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md): use el Editor universal para crear formularios visuales y de arrastrar y soltar, ideal para autores de contenido con conocimientos técnicos limitados. Los Forms creados con Universal Editor se entregan con Edge Delivery Services para una representación rápida y ligera.
   * [Creación basada en documentos](/help/edge/docs/forms/tutorial.md): utilice herramientas como Microsoft Excel o Hojas de cálculo de Google para definir la estructura y el contenido del formulario. Este método es útil para los usuarios empresariales que prefieren la entrada basada en hoja de cálculo. Estos formularios se publican normalmente a través de Edge Delivery Services y son adecuados para casos de uso ligeros y de gran volumen.
* [Creación sin encabezado](https://experienceleague.adobe.com/en/docs/experience-manager-headless-adaptive-forms/using/tutorial/build-engaging-forms-using-core-components-and-headless-adaptive-forms-aem-forms-cloud-service): Utilice API para procesar formularios como JSON para cualquier front-end, por ejemplo, React, Angular, aplicaciones móviles o quioscos, sin depender de AEM. Actualmente, solo los componentes principales admiten la entrega sin encabezado. Los formularios sin encabezado son ideales para casos de uso omnicanal y se consumen independientemente del procesamiento de páginas de AEM, lo que los hace flexibles para implementaciones front-end personalizadas.

### Análisis comparativo de los métodos de creación de formularios de AEM

&#x200B;La siguiente tabla ofrece una comparación concisa de varios métodos de creación de formularios de AEM, destacando los enfoques, las características, las opciones de publicación y los casos de uso ideales para ayudarle a seleccionar el método más adecuado para sus necesidades.

| **Consideración** | **Componentes de base** | **Componentes principales** | **Editor universal (WYSIWYG)** | **Creación basada en documentos** | **Creación sin encabezado** |
|--------------------------|---------------------------------------------------------------------|------------------------------------------------------------------------|-------------------------------------------------------------------------|---------------------------------------------------------------------------|-------------------------------------------------------------------------|
| **Ideal Para** | Mantener formularios y flujos de trabajo heredados en AEM | Formularios escalables y modernos con flujos de trabajo e integraciones complejos | Crear formularios para sitios de servicios de Edge Delivery con requisitos complejos | Creación rápida de prototipos para formularios básicos sin servicios avanzados de envío | Experiencias omnicanal en plataformas (web, móvil, quioscos, etc.) |
| **Experiencia del usuario** | Desarrolladores, autores de contenido | Desarrolladores, autores avanzados | Usuarios empresariales, autores de contenido | Usuarios empresariales | Desarrolladores |
| **Complejidad de formulario** | Formularios básicos | Formularios complejos con secciones dinámicas | Formularios complejos con acciones personalizadas | Formularios simples | Formularios muy complejos impulsados por API |
| **Flexibilidad de diseño** | Limitado | Alto (personalización de CSS/JS) | Moderar (según las plantillas) | Limitado | Alto (control de marco de front-end) |
| **Capacidad de integración** | Flujos de trabajo básicos de AEM | Avanzadas (modelos de datos, flujos de trabajo) | Integrado con sistemas externos | Básico (Google Sheets, Excel) | Control total mediante API |
| **Método de publicación** | Solo AEM | AEM y Edge Delivery Services | Edge Delivery Services | Edge Delivery Services | Cualquier front-end a través de API |
| **Rendimiento y SEO** | Estándar | Mejorado con respecto a los componentes base | Altas puntuaciones en Google Lighthouse para un procesamiento más rápido y una mejor SEO | Altas puntuaciones en Google Lighthouse para un procesamiento más rápido y una mejor SEO | Depende de la implementación |
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

La siguiente tabla proporciona una comparación detallada de las funciones clave de los distintos métodos de creación de formularios de AEM, lo que le ayudará a seleccionar el método más adecuado para sus necesidades&#x200B;

| **Capacidad** | **Componentes de base** | **Componentes principales** | **Editor universal (WYSIWYG)** | **Creación basada en documentos** | **Creación sin encabezado** |
|-----------------------------------------|---------------------------|---------------------|-------------------------------|-----------------------------|------------------------|
| **Composición unificada con sitios** | ❌ | ✅ | ✅ | ❌ | ❌ |
| **Compatibilidad con formularios incrustados** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **Reglas (comportamiento dinámico)** | Editor de reglas avanzadas con funciones personalizadas | Editor de reglas avanzadas con funciones personalizadas | Editor de reglas avanzadas con funciones personalizadas | Limitado: mostrar/ocultar, calcular valor, funciones personalizadas | Limitado: requiere implementación personalizada |
| **Compatibilidad con datos adjuntos** | ✅ | ✅ | ✅ | ℹ️ (Acceso anticipado) | ❌ |
| **Compatibilidad con CAPTCHA** | reCAPTCHA v2/Enterprise, Chcaptcha (EA), Torniquete (EA) | reCAPTCHA v2/Enterprise, Captcha (EA) | reCAPTCHA Enterprise | reCAPTCHA Enterprise | Requiere integración personalizada |
| **Características de envío** | Extremo REST, correo electrónico, modelo de datos de formulario (FDM), invocar flujo de trabajo de AEM, SharePoint, OneDrive, Azure Blob Storage, Power Automate, Workfront Fusion (EA) | Extremo REST, correo electrónico, modelo de datos de formulario (FDM), invocar flujo de trabajo de AEM, SharePoint, OneDrive, Azure Blob Storage, Power Automate, Workfront Fusion (EA) | Extremo REST, correo electrónico, modelo de datos de formulario (FDM), invocar flujo de trabajo de AEM, SharePoint, OneDrive, Azure Blob Storage, Power Automate, Workfront Fusion (EA) | Sólo hoja de cálculo | Extremos de API personalizados |
| **Esquema de datos** | FDM, personalizado | FDM, personalizado | FDM, personalizado | Personalizado | Personalizado |
| **Relleno previo** | ✅ | ✅ | ?? (a través del asistente) | ✅ | Implementación personalizada |
| **Fragmentos** | ✅ | ✅ | ✅ | ✅ | ❌ |
| **Editor visual de reglas** | ✅ | ✅ | ✅ | ❌ | ❌ |
| **Localización** | ✅ | ✅ | ?? (a través de Sites) | ℹ️ (Excel: manual, función de hojas de Google) | Implementación personalizada |
| **Esquema de datos (árbol de datos)** | ✅ | ✅ | ?? (a través de la extensión UI) | ❌ | Implementación personalizada |
| **Compatibilidad con plantillas** | ✅ | ✅ | Solo contenido inicial, sin política | ❌ | Implementación personalizada |
| **Portal** | ✅ | ✅ | ❌ | ❌ | ❌ |
| **Creación DoR** | ✅ | ✅ | ?? (vía Derlina) | ❌ | ❌ |
| **Generación DoR** | ✅ | ✅ | ?? (FORMS-2475 Nuevo) | ❌ | ❌ |
| **Tema** | ✅ | ✅ | ℹ️ (a nivel de proyecto) | ℹ️ (a nivel de proyecto) | Implementación personalizada |
| **Componente personalizado** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **OOTB y funciones personalizadas** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **Referencia al fragmento** | ✅ | ❌ | ❌ | ❌ | ❌ |
| **Integración de firma** | ✅ | ❌ | ❌ | ❌ | ❌ |
| **Compatibilidad con RTL** | ❌ | ✅ | ?? | ?? | Implementación personalizada |
| **Experimentación** | ❌ | ❌ | ✅ | ✅ | Implementación personalizada |
| **Administración de tareas mediante Workfront** | ❌ | ❌ | ✅ | ❌ | ❌ |
| **Extensión de Personalization** | ❌ | ❌ | ?? | ❌ | Implementación personalizada |
| **Personalización del editor** | ❌ | ❌ | ✅ (a través de la extensión de IU) | ❌ | Implementación personalizada |
| **Acción de envío** | ✅ | ✅ | ✅ | Sólo hoja de cálculo | Implementación personalizada |


## Artículo relacionado

* [Creación basada en documentos mediante Microsoft Excel u Hojas de cálculo de Google](/help/edge/docs/forms/create-forms.md)
* [Editor universal para la creación de WYSIWYG](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring)
* [Creación de un formulario adaptable (componentes básicos)](/help/forms/creating-adaptive-form.md)
* [Creación de un formulario adaptable (componentes principales)](/help/forms/create-an-adaptive-form.md)
