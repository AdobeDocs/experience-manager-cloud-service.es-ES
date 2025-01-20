---
Title: Authoring a Form
Description: This article provides information on various form authoring platforms, including the Universal Editor, document-based authoring, and Adaptive Forms editors (Core Components and Foundation Components).
Keywords: Universal Editor for WYSIWYG authoring, document-based authoring, Adaptive Forms editors, Adaptive Forms editors for Core Components authoring, Adaptive Forms editors for Foundation Components authoring
feature: Edge Delivery Services
Role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: bdc0e51a8b16df432f1f1aeabed11135fb8c8e0c
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 2%

---


# Creación de un formulario

Adobe Experience Manager ofrece y admite varios editores para crear un formulario. Puede utilizar lo siguiente:
* Editor universal (para la creación de WYSIWYG)
* Hojas de cálculo de Microsoft Excel o Google (conocidas como Creación basada en documentos)
* Editores de Forms adaptables (para la creación basada en componentes principales o componentes de base)

**[imagen que se agregará]**

## Editor universal (para la creación de WYSIWYG)

El editor universal es un editor visual versátil que ofrece una función de lo que se ve es lo que se obtiene (WYSIWYG), lo que garantiza una experiencia de creación de formularios intuitiva. Se recomienda utilizar el Editor universal al crear nuevos formularios, ya que ofrece un diseño moderno y fácil de usar, así como una interfaz práctica de arrastrar y soltar.

Para crear formularios con el Editor universal, se utilizan las plantillas de Edge Delivery Services AEM disponibles en el entorno de la. Estos formularios heredan su aspecto de las configuraciones del repositorio de GitHub de los Edge Delivery Services. AEM [Para habilitar la publicación de estos formularios en Edge Delivery Services, se ha establecido una conexión entre el entorno de su y el repositorio de GitHub de los Edge Delivery Services](/help/edge/docs/forms/publishing-forms.md).

Para ver los pasos detallados sobre cómo crear contenido con el editor universal, consulte el artículo [Creación de contenido con el editor universal](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/universal-editor/authoring).

## Hojas de cálculo de Microsoft Excel o Google (conocidas como Creación basada en documentos)

Puede crear los formularios utilizando la creación basada en documentos con archivos de Microsoft Excel o Google Sheets, lo que le permite aprovechar los sólidos ecosistemas y API de Google Sheets, Microsoft Excel y Microsoft SharePoint. Este método es especialmente útil para crear formularios simples sin servicios de envío avanzados.

Para empezar a crear un formulario con Microsoft Excel o Hojas de cálculo de Google AEM, [configure un proyecto de con la plantilla de AEM Forms](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) y clone el repositorio de GitHub correspondiente en el equipo local. AEM Forms Edge Delivery proporciona una característica denominada bloque de Forms adaptable, que simplifica el proceso de creación de formularios para capturar y almacenar datos. Para aprender a crear y publicar formularios utilizando el bloque de Forms adaptable en Edge Delivery Services, consulte [Crear un formulario](/help/edge/docs/forms/create-forms.md).

## Editores de Forms adaptables (para la creación basada en componentes principales o componentes de base)

Puede crear formularios atractivos, interactivos y dinámicos. El editor de formularios adaptables proporciona un asistente fácil de usar que le permite crear Forms adaptable rápidamente. El asistente para formularios incluye una sencilla navegación por pestañas, que permite seleccionar plantillas preconfiguradas para componentes básicos o principales, temáticas, modelos de datos y opciones de envío para crear un formulario de forma eficaz.

La creación de [formularios con componentes principales](/help/forms/creating-adaptive-form-core-components.md) le permite aprovechar componentes de captura de datos estandarizados que se pueden personalizar, lo que reduce el tiempo de desarrollo y los costos de mantenimiento de las experiencias de inscripción digital. Estos formularios se pueden publicar mediante el Bloque de Forms adaptable en Edge Delivery Services AEM o a través de la instancia de Publish de la aplicación de la aplicación de la aplicación de seguridad de la aplicación de datos de.

[La creación de formularios con componentes de base](/help/forms/create-an-adaptive-form.md) usa componentes de captura de datos clásicos. AEM Estos formularios solo se pueden publicar mediante la instancia de Publish de la.

También puede publicar formularios creados con editores de Forms adaptables en Edge Delivery Services AEM estableciendo [conexión entre su entorno de y el repositorio de GitHub de los Edge Delivery Services](/help/edge/docs/forms/publishing-forms.md).

## ¿Cómo elegir entre varios tipos de creación de formularios?

En la siguiente tabla se describen las funciones y los casos de uso de cada editor de creación, lo que le ayuda a elegir el adecuado según sus necesidades y los envíos de formularios.

| **Editor de creación de formularios** | **Método clave** | **Características** | **Método de publicación** | **Casos de uso** |
|--------|-----------|-------|-------|------------------------------------------------|
| **Creación basada en documentos** | Aprovecha herramientas conocidas como Google Docs y Microsoft Office para crear formularios. | Forms está diseñado utilizando hojas de cálculo, con datos enviados directamente a las hojas de Google o a las hojas de Microsoft Excel. </br> </br>: estos formularios son más rápidos de crear e implementar. AEM No es necesario tener conocimientos previos de la documentación de para desarrollar componentes y estilos personalizados para estos formularios. | Estos formularios se publican en Edge Delivery Services y tienen una puntuación muy alta en Google Lighthouse. </br> </br> La puntuación más alta resulta en un procesamiento más rápido y una mejor SEO. | Estos formularios son ideales para crear prototipos rápidos o formularios básicos en los que no se necesitan servicios de envío avanzados. </br> </br>: estos formularios son adecuados para encuestas, formularios de registro o de comentarios que requieren almacenamiento de datos en hojas de cálculo. Estos formularios se publican en los servicios de Edge Delivery |
| **Editor universal** </br> </br> Si está creando un nuevo formulario, use el Editor universal para crear formularios. | Ofrece una interfaz de WYSIWYG para la creación intuitiva de formularios. | Forms está diseñado con una interfaz intuitiva de arrastrar y soltar. </br> </br>: estos formularios toman prestada la apariencia del repositorio de GitHub de los Edge Delivery Services configurados para el formulario correspondiente. | Estos formularios se publican en Edge Delivery Services y tienen una puntuación muy alta en Google Lighthouse. </br> </br> La puntuación más alta resulta en un procesamiento más rápido y una mejor SEO. | Estos formularios son ideales para crear formularios para sitios y páginas del servicio de Edge Delivery. Estos escenarios de formularios que implican formularios complejos, flujos de trabajo complejos, acciones personalizadas o integraciones con sistemas externos |
| **editores de Forms adaptables** | Proporciona un enfoque impulsado por un asistente para iniciar rápidamente la creación de formularios utilizando plantillas, estilos y campos predefinidos. | Utilice estos editores para crear formularios basados en componentes principales o en componentes de base. | Estos formularios se pueden publicar en Edge Delivery Services AEM o a través de instancias de Publish. | Utilice estos editores para crear formularios basados en componentes principales o en componentes de base. Ideal para escenarios que implican formularios complejos, flujos de trabajo complejos, acciones personalizadas o integraciones con sistemas externos. |


>[!NOTE]
>
>
> Si encuentra alguna función que falte en el editor universal y que anteriormente estuviera disponible en el editor de Forms adaptable, puede solicitarla enviando un correo electrónico a mailto:aem-forms-ea@adobe.com con su dirección de correo electrónico oficial.

## Artículo relacionado

* [Creación basada en documentos mediante Microsoft Excel o Hojas de cálculo de Google](/help/edge/docs/forms/create-forms.md)
* [Editor universal para la creación de WYSIWYG](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring)
* [Creación de un formulario adaptable (componentes básicos)](/help/forms/creating-adaptive-form.md)
* [Creación de un formulario adaptable (componentes principales)](/help/forms/create-an-adaptive-form.md)

## Ver también

{{see-more-forms-eds}}