---
title: Información general sobre Edge Delivery Services para AEM Forms
description: Aprenda a utilizar Edge Delivery Services para crear y entregar formularios de alto rendimiento con AEM Forms, lo que permite un desarrollo rápido y una recopilación de datos optimizada.
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: 1ddf97f56e5a9b7c95959da47a748f5a6d128e43
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 8%

---


# Edge Delivery Services para AEM Forms


Edge Delivery Services para AEM Forms es un conjunto de servicios que permiten un entorno de desarrollo rápido en el que los autores pueden actualizar, publicar e iniciar nuevos formularios con rapidez. Estos servicios ofrecen experiencias de formularios excepcionales y de gran impacto que fomentan la participación y las conversiones. Estas experiencias de formulario son fáciles de crear y desarrollar.

* **Experiencias más rápidas:** Forms se entrega desde una red de distribución de contenido (CDN) global, lo que garantiza que se cargue rápidamente para los usuarios.
* **Desarrollo rápido:** Un proceso de desarrollo optimizado permite actualizaciones más rápidas. Los cambios se pueden publicar sin esperar compilaciones de canalización largas.
* **Creación flexible:** Elija entre varias herramientas para crear formularios, incluida la creación basada en documentos (Microsoft Word, Google Docs/Hojas) o un editor visual de WYSIWYG (Editor universal).

## Funcionamiento

Con Edge Delivery Services, la estructura y el contenido del formulario pueden residir en fuentes como AEM as a Cloud Service, Microsoft SharePoint o Google Drive. Este contenido se publica en una CDN global. Cuando un usuario visita su sitio, el formulario se proporciona directamente desde el servidor perimetral de CDN más cercano para obtener un rendimiento óptimo.

![Diagrama de arquitectura simplificado que muestra las fuentes de contenido, una CDN y el usuario.](/help/forms/assets/eds-simplified-architecture.png)
**Arquitectura de Edge Delivery Services simplificada con Forms**

Los datos enviados por los usuarios se pueden enviar a varios destinos, desde una sencilla hoja de cálculo hasta un potente back-end de AEM para un procesamiento posterior.

## Elección de un método de creación

Existen varias formas de crear formularios para los sitios de Edge Delivery Services. El mejor método depende de las habilidades del equipo, la complejidad del formulario y los requisitos del proyecto.

![Árbol de decisiones para elegir un método de creación de formularios.](/help/forms/assets/eds-authoring-selection.png)
**Árbol de decisiones de creación de formularios**

### Creación basada en documentos

Este método le permite [crear formularios utilizando Microsoft Word o Google Docs/Sheets](/help/edge/docs/forms/create-forms.md). Los campos de formulario, las etiquetas y los tipos se definen en un documento utilizando un formato de tabla específico. Edge Delivery Services convierte este documento en un formulario interactivo de HTML.

**Características:**

* Crear en herramientas conocidas: Word, Google Docs o Hojas de cálculo de Google.
* Defina campos como entradas de texto, correo electrónico, listas desplegables, casillas de verificación y botones de opción.
* Establezca reglas de validación básicas, como campos obligatorios.
* Integre Google reCAPTCHA para la protección contra spam.
* Compatibilidad con cargas de archivos.
* Envíe datos directamente a una hoja de cálculo o dirección de correo electrónico.
* Amplíe con código personalizado mediante GitHub para obtener componentes y estilos avanzados.

**Mejor para:**

* Equipos que utilizan principalmente editores de documentos para la creación de contenido.
* Crear rápidamente formularios simples o moderadamente complejos.
* Recopilación de datos sencilla en una hoja de cálculo o un correo electrónico.

Los envíos de formularios basados en documentos los administra normalmente [AEM Forms Submission Service](/help/forms/forms-submission-service.md), que enruta los datos a una hoja de cálculo o dirección de correo electrónico configuradas.

### Creación del Editor universal

El editor universal [proporciona una interfaz moderna de WYSIWYG](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) para crear formularios con una experiencia de arrastrar y soltar.

**Características:**

* Crear formularios visuales y de arrastrar y soltar con una biblioteca de componentes generados previamente.
* Configure la validación en tiempo real y la lógica empresarial compleja (por ejemplo, mostrar/ocultar campos basados en selecciones de usuarios).
* Vista previa en directo para diferentes dispositivos.
* Integración profunda con funciones de AEM as a Cloud Service como fragmentos de contenido, flujos de trabajo de AEM y permisos de usuario.
* Creación y edición de formularios con asistencia de IA a través de Experience Builder.

**Mejor para:**

* Crear formularios complejos con lógica condicional, paneles de varios pasos o personalización.
* Equipos (por ejemplo, especialistas en marketing o usuarios empresariales) que prefieren las herramientas visuales.
* Proyectos que requieren una integración sólida con el back-end de AEM para el procesamiento de datos y flujos de trabajo.

Forms creado con el editor universal puede usar el [servicio de envío de Forms](/help/forms/forms-submission-service.md) o configurarse para usar [las acciones de envío proporcionadas como OOTB para la administración avanzada de datos](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md), como enviar datos a un flujo de trabajo de AEM, a un extremo REST o a una base de datos.

### Incrustar Forms en páginas de creación de documentos

[Creación de documentos (DA)](https://www.aem.live/developer/da-tutorial) es un servicio hospedado en Adobe para administrar el contenido del sitio web de Edge Delivery Services. Aunque DA no es una herramienta de creación de formularios en sí, puede utilizarla para crear páginas web e incrustar formularios creados con otros métodos.

**Cómo funciona:**

1. **Crear el formulario:** Cree el formulario mediante la creación basada en documentos o el Editor universal.
2. **Publicar el formulario:** Asegúrese de que se publica el formulario y de que se puede obtener acceso a él desde su propia dirección URL.
3. **Incrustar en DA:** En la página de creación de documentos, agregue un bloque que haga referencia a la dirección URL del formulario para incrustarlo.

Este método es para equipos que utilizan la creación de documentos como su sistema de administración de contenido principal para sitios de Edge Delivery Services.

## Comparación de métodos de creación

| Criterios | Creación basada en documentos | Editor universal (WYSIWYG) | Forms en la creación de documentos (DA) |
|----------------------------------|---------------------------------------|-----------------------------------------|-------------------------------------------|
| **Herramienta de creación principal** | Word/Google Docs/Hojas | Explorador (AEM Universal Editor) | N/D (los Forms están *incrustados*) |
| **Nivel de habilidad del equipo** | Familiarizado con los editores de documentos | Cómoda con las herramientas web visuales | Utiliza DA para el contenido de la página |
| **Complejidad típica del formulario** | De simple a moderado | De moderado a complejo, categoría empresarial | Depende del formulario incrustado |
| **Opciones de envío** | Servicio de envío de Forms (a hoja/correo electrónico) | Servicio de envío de Forms, publicación de AEM (flujo de trabajo, modelo de datos de formulario, integraciones de terceros) | Sigue la configuración del formulario incrustado |
| **Integración back-end de AEM** | Mínimo | Alto (con envío de publicación de AEM) | Indirectamente, mediante el formulario de editor universal incrustado |
| **Mejor Para...** | Creación rápida de formularios sencillos por equipos de contenido, captura rápida de datos. | Los especialistas en marketing y los usuarios empresariales que necesitan control visual, formularios complejos o una integración AEM profunda. | Sitios donde el contenido principal se administra en DAM. |

<!-- 
## Detailed Feature Comparison

| **Capability**                        | **Universal Editor (WYSIWYG)** | **Document-based Authoring** | **Document Authoring (DA)** |
|-----------------------------------------|-------------------------------|-----------------------------|-----------------------------|
| **Unified Composition with Sites**    | ✅                            |                              | ✅ (with embedded forms)     |
| **Embedding Form Support**            | ✅                            | ✅                          | ✅ (embed from Universal Editor or Docs)   |
| **Rules (Dynamic Behavior)**          | Advanced rules editor with custom functions | Limited: Show/hide, compute value, custom functions | Depends on embedded form     |
| **Attachment Support**                | ✅                            | ℹ️ (Early Access)           | Depends on embedded form     |
| **CAPTCHA Support**                   | reCAPTCHA Enterprise          | reCAPTCHA Enterprise       | Depends on embedded form     |
| **Submission Features**               | REST, Email, FDM, Workflow, SharePoint, OneDrive, Azure Blob, Power Automate, Workfront Fusion (EA) | Only Spreadsheet            | Follows embedded form's setup |
| **Data Schema**                       | FDM, Custom                   | Custom                      | Based on embedded form       |
| **Pre-fill**                          | 💡 (via Wizard)               | ✅                          | Depends on embedded form     |
| **Fragments**                         | ✅                            | ✅                          | Depends on embedded form     |
| **Visual Rule Editor**                | ✅                            |                              |                              |
| **Localization**                      | 💡 (via Sites)                | ℹ️ (Excel/Sheets manual)    | Depends on embedded form     |
| **Template Support**                  | Only Initial Content          |                              |                              |
| **Theme**                             | ℹ️ (at project level)         | ℹ️ (at project level)        | ℹ️ (based on hosting site)    |
| **Custom Component**                  | ✅                            | ✅                          | ✅ (if embedded component supports it) |
| **Experimentation**                   | ✅                            | ✅                          | Depends on embed context     |
| **Submit Action**                     | ✅                            | Only Spreadsheet            | Based on embedded form       |
-->



## Siguientes pasos

* [Crear un formulario con creación basada en documentos](/help/edge/docs/forms/tutorial.md)
* [Obtenga información acerca del Editor universal para Forms](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [Configurar acciones de envío de formularios](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)
* [Más información acerca de la creación de documentos (DA)](https://www.aem.live/developer/da-tutorial)
