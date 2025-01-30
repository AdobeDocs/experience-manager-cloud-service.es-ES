---
Title: Authoring a Form
Description: This article provides information on various form authoring platforms, including the Universal Editor, document-based authoring, and Adaptive Forms editors (Core Components and Foundation Components).
Keywords: Universal Editor for WYSIWYG authoring, document-based authoring, Adaptive Forms editors, Adaptive Forms editors for Core Components authoring, Adaptive Forms editors for Foundation Components authoring
feature: Edge Delivery Services
Role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: bdc0e51a8b16df432f1f1aeabed11135fb8c8e0c
workflow-type: ht
source-wordcount: '877'
ht-degree: 100%

---


# Creación de un formulario

Adobe Experience Manager ofrece y admite varios editores para crear un formulario. Puede utilizar lo siguiente:
* Editor universal (para la creación de WYSIWYG)
* Microsoft Excel u Hojas de cálculo de Google (conocidas como Creación basada en documentos)
* Editores de formularios adaptables (para la creación basada en componentes principales o componentes de base)

**[imagen a añadir]**

## Editor universal (para la creación de WYSIWYG)

El editor universal es un editor visual versátil que ofrece una función WYSIWYG (what-you-see-is-what-you-get), lo que garantiza una experiencia de creación de formularios intuitiva. Se recomienda utilizar el editor universal para crear nuevos formularios, ya que ofrece un diseño moderno y fácil de usar, así como una interfaz práctica de arrastrar y soltar.

Para crear formularios con el editor universal, se utilizan las plantillas de Edge Delivery Services disponibles en el entorno de AEM. Estos formularios heredan la apariencia de las configuraciones del repositorio de GitHub de Edge Delivery Services. [Para habilitar la publicación de estos formularios en Edge Delivery Services, se ha establecido una conexión entre su entorno de AEM y el repositorio de GitHub de Edge Delivery Services](/help/edge/docs/forms/publishing-forms.md).

Para obtener más información sobre cómo crear con el editor universal, consulte el artículo [Creación de contenido con el editor universal.](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/sites/authoring/universal-editor/authoring)

## Microsoft Excel u Hojas de cálculo de Google (conocidas como Creación basada en documentos)

Puede crear los formularios utilizando la creación basada en documentos con archivos de Microsoft Excel o de Hojas de cálculo de Google, lo que le permite aprovechar los sólidos ecosistemas y las API de las Hojas de cálculo de Google, Microsoft Excel y Microsoft SharePoint. Este método es especialmente útil para crear formularios simples sin servicios de envío avanzados.

Para empezar a crear un formulario mediante Microsoft Excel u Hojas de cálculo de Google, [configure un proyecto de AEM usando el elemento repetitivo de AEM Forms](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) y clone el repositorio de GitHub correspondiente en su equipo local. AEM Forms Edge Delivery proporciona una característica denominada bloque de formularios adaptables, que simplifica el proceso de creación de formularios para capturar y almacenar datos. Para aprender a crear y publicar formularios utilizando el bloque de formularios adaptables en Edge Delivery Services, consulte [Crear un formulario](/help/edge/docs/forms/create-forms.md).

## Editores de formularios adaptables (para la creación basada en componentes principales o componentes de base)

Puede crear formularios atractivos, adaptables y dinámicos. El editor de formularios adaptables proporciona un asistente fácil de usar que le permite crear formularios adaptables rápidamente. El asistente para formularios incluye una sencilla navegación por pestañas, que permite seleccionar plantillas preconfiguradas para componentes básicos o principales, temáticas, modelos de datos y opciones de envío para crear un formulario de forma eficaz.

[La creación de formularios con componentes principales](/help/forms/creating-adaptive-form-core-components.md) le permite aprovechar componentes de captura de datos estandarizados que se pueden personalizar, lo que reduce el tiempo de desarrollo y los costes de mantenimiento de las experiencias de inscripción digital. Estos formularios se pueden publicar mediante el bloque de formularios adaptables en Edge Delivery Services o mediante la instancia de publicación de AEM.

[La creación de formularios con componentes de base](/help/forms/create-an-adaptive-form.md) usa componentes de captura de datos clásicos. Estos formularios solo se pueden publicar mediante la instancia de publicación de AEM.

También puede publicar formularios creados mediante editores de formularios adaptables en Edge Delivery Services estableciendo [conexión entre su entorno de AEM y el repositorio de GitHub de Edge Delivery Services](/help/edge/docs/forms/publishing-forms.md).

## ¿Cómo elegir entre varios tipos de creación de formularios?

En la siguiente tabla se describen las funciones y los casos de uso de cada editor de creación, lo que le ayuda a elegir el adecuado según sus necesidades y los envíos de formularios.

| **Editor de creación de formularios** | **Enfoque clave** | **Funciones** | **Método de publicación** | **Casos de uso** |
|--------|-----------|-------|-------|------------------------------------------------|
| **Creación basada en documentos** | Aprovecha herramientas conocidas como Google Docs y Microsoft Office para crear formularios. | Los formularios se han diseñado utilizando hojas de cálculo, con datos enviados directamente a las hojas de Google o a las hojas de Microsoft Excel. </br> </br>: Estos formularios son más rápidos de crear e implementar. No es necesario tener conocimientos previos de AEM para desarrollar componentes y estilos personalizados para estos formularios. | Estos formularios se publican en Edge Delivery Services y tienen una puntuación muy alta en Google Lighthouse. </br> </br> La puntuación más alta se traduce en un procesamiento más rápido y una mejor optimización de los motores de búsqueda. | Estos formularios son ideales para crear prototipos rápidos o formularios básicos en los que no se necesitan servicios de envío avanzados. </br> </br>: Estos formularios son adecuados para encuestas, formularios de registro o de comentarios que requieren almacenamiento de datos en hojas de cálculo. Estos formularios se publican en Edge Delivery Services |
| **Editor universal**  </br> </br> Si está creando un nuevo formulario, use el editor universal para crear formularios. | Ofrece una interfaz WYSIWYG para la creación intuitiva de formularios. | Los formularios se han diseñado mediante una interfaz intuitiva de arrastrar y soltar. </br> </br> Estos formularios toman prestada la apariencia del repositorio de GitHub de Edge Delivery Services configurado para el formulario correspondiente. | Estos formularios se publican en Edge Delivery Services y tienen una puntuación muy alta en Google Lighthouse. </br> </br> La puntuación más alta se traduce en un procesamiento más rápido y una mejor optimización de los motores de búsqueda. | Estos formularios son ideales para crear formularios para sitios y páginas de Edge Delivery Service. Son escenarios de formularios que implican formularios complejos, flujos de trabajo complejos, acciones personalizadas o integraciones con sistemas externos |
| **Editores de formularios adaptables** | Proporciona un enfoque basado en un asistente para iniciar rápidamente la creación de formularios utilizando plantillas, estilos y campos predefinidos. | Utilice estos editores para crear formularios basados en componentes principales o formularios basados en componentes de base. | Estos formularios se pueden publicar en Edge Delivery Services o a través de instancias de publicación de AEM. | Utilice estos editores para crear formularios basados en componentes principales o formularios basados en componentes de base. Son ideales para escenarios que implican formularios complejos, flujos de trabajo complejos, acciones personalizadas o integraciones con sistemas externos. |


>[!NOTE]
>
>
> Si encuentra que falta alguna función en el editor universal que antes estaba disponible en el editor de formularios adaptables, puede solicitarla enviando un correo electrónico a mailto:aem-forms-ea@adobe.com con su dirección de correo electrónico oficial.

## Artículo relacionado

* [Creación basada en documentos mediante Microsoft Excel u Hojas de cálculo de Google](/help/edge/docs/forms/create-forms.md)
* [Editor universal para la creación de WYSIWYG](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring)
* [Creación de un formulario adaptable (componentes básicos)](/help/forms/creating-adaptive-form.md)
* [Creación de un formulario adaptable (componentes principales)](/help/forms/create-an-adaptive-form.md)

## Consulte también

{{see-more-forms-eds}}