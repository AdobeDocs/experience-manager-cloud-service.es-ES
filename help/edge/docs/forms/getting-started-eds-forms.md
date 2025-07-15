---
title: Introducción a Forms en AEM Edge Delivery Services
description: Aprenda a crear y entregar formularios de alto rendimiento en Adobe Experience Manager Edge Delivery Services, con énfasis en el enfoque de creación del Editor universal.
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: e1ead9342fadbdf82815f082d7194c9cdf6d799d
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 1%

---


# Introducción a Forms en AEM Edge Delivery Services

<span class="preview"> Esta es una característica previa al lanzamiento disponible a través de nuestro <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=es#new-features">canal previo al lanzamiento</a>. </span>

Adobe Experience Manager (AEM) Edge Delivery Services (EDS) le permite ofrecer experiencias web increíblemente rápidas y escalables desde el perímetro de. En esta guía se explica **cómo crear y publicar formularios para esas experiencias**, con una jerarquía de recomendaciones clara:

1. **Editor universal (UE): la mejor opción para la mayoría de los equipos**
2. **Creación basada en documentos (documentos/hojas): ideal para formularios rápidos y sencillos**
3. **Creación de documentos (DA): se utiliza para incrustar formularios en páginas creadas por DA**

Al final, podrá elegir el método de creación adecuado, comprender las opciones de envío y seguir los pasos siguientes hacia formularios listos para la producción.



## Elección de un método de creación

| Equipo y requisitos | Método recomendado | Por qué |
|--------------------|--------------------|-----|
| Los especialistas en marketing y los diseñadores necesitan un control visual, lógica condicional o integraciones de AEM | **Editor universal** | Arrastrar y soltar, reglas avanzadas, envíos a FSS o AEM Publish |
| Los autores de contenido ya trabajan en Word / Google Docs / Hojas; captura de datos sencilla para hoja de cálculo / correo electrónico | **Creación basada en documentos** | Herramientas familiares, la ruta más rápida para los formularios básicos |
| Páginas del sitio web creadas en **Creación de documentos (DA)** | **Incrustar** un formulario basado en UE o Doc en la página de DA | DA no crea formularios por sí mismo |


## Métodos de creación en detalle

### Editor universal

Universal Editor es una herramienta visual de creación de arrastrar y soltar para especialistas en marketing y diseñadores que combina velocidad con potencia de nivel empresarial:

* Edición de WYSIWYG en tiempo real y previsualizaciones de dispositivos.
* Reglas avanzadas e IU de validación: no se requiere código.
* Integración directa con recursos de AEM, flujos de trabajo y el modelo de datos de formulario (FDM).
* Entrega perfecta a los desarrolladores de componentes personalizados en JS/CSS de vainilla.
* Objetivos de envío flexibles: empiece con el **Servicio de envío de Forms (FSS)** o cambie a **Acciones de envío de publicación de AEM** a medida que sus necesidades aumenten.

> **Recomendación**: Inicie cada nuevo proyecto de formulario con el Editor universal a menos que su equipo esté 100 % centrado en documentos y el formulario sea muy básico.


### Creación basada en documentos (documentos/hojas)

La creación basada en documentos es más adecuada para crear formularios sencillos y de baja complejidad con herramientas conocidas, como Microsoft Word, Google Docs o Hojas de cálculo de Google. Este método es ideal para equipos de contenido que requieren una forma rápida y directa de crear formularios.

* Defina campos de formulario dentro de una tabla (Documentos) o como filas (Hojas).
* Admite validación de campos básica y Google reCAPTCHA para la protección contra spam.
* Los envíos de formularios se administran exclusivamente a través del servicio de envío de Forms.
* Publicación instantánea: cualquier cambio realizado en el documento de origen se refleja inmediatamente en el sitio sin requerir una canalización de implementación.


### Incrustación de Forms en la creación de documentos (DA)

La creación de documentos (DA) está diseñada para crear contenido de página estructurado y no admite la creación de formularios nativos. Para agregar un formulario a una página creada por DA, siga estos pasos:

1. Cree el formulario con el **Editor universal** (recomendado) o la creación basada en documentos.
2. Publique el formulario para generar una dirección URL única (por ejemplo, `/forms/contact-us`).
3. En la página de DA, inserte un bloque **Incrustar formulario** y especifique la dirección URL del formulario publicado.

<!-- 
## Feature Comparison

| Capability | Universal Editor | Document-Based | Document Authoring |
|------------|-----------------|----------------|--------------------|
| Visual drag-and-drop | ✅ | – | – |
| Advanced rules editor | ✅ | Limited | – |
| Attachments | ✅ | EA | – |
| reCAPTCHA Enterprise | ✅ | ✅ | Depends on embed |
| Submit to spreadsheet/email | ✅ (FSS) | ✅ (FSS) | Via embed |
| Submit to AEM workflows/FDM | ✅ | – | Via UE embed |
| Custom components (JS/CSS) | ✅ | ✅ | Via embed |
| Localization via Sites | ✅ | Manual | Via embed |

-->

## Siguientes pasos

1. **Empiece con el editor universal:** Consulte la [guía de introducción al editor universal](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) para comenzar a crear formularios.
2. **Configurar envío de formularios:** Seleccione y configure su método de envío preferido. Consulte [Servicio de envío de Forms](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md) o Acciones de envío de publicación de AEM para obtener instrucciones de configuración.
3. **Aplicar prácticas recomendadas:** Revise [prácticas recomendadas de diseño de formularios](/help/edge/docs/forms/universal-editor/best-practices-eds-forms.md) para garantizar la accesibilidad y el rendimiento.
4. **Usar la creación basada en documentos:** Para crear formularios con Microsoft Excel o Hojas de cálculo de Google, siga el [tutorial de creación basada en documentos](/help/edge/docs/forms/tutorial.md).
5. **Incrustar Forms en la creación de documentos:** Si está creando páginas en la creación de documentos, consulte el [tutorial de DA](https://www.aem.live/developer/da-tutorial) para obtener instrucciones sobre cómo incrustar formularios publicados.

> **Ya está listo para crear su primer formulario de alto rendimiento con AEM Edge Delivery Services.**