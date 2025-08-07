---
title: Introducción a los formularios en AEM Edge Delivery Services
description: Aprenda a crear y suministrar formularios de alto rendimiento en Adobe Experience Manager Edge Delivery Services, con énfasis en el enfoque de creación con el editor universal.
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: ccfb85da187e828b5f7e8b1a8bae3f483209368d
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 100%

---


# Introducción a los formularios en AEM Edge Delivery Services

<!--<span class="preview"> This is a pre-release feature available through our <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features">pre-release channel</a>. </span>-->

Adobe Experience Manager (AEM) Edge Delivery Services (EDS) le permite ofrecer experiencias web increíblemente rápidas y escalables desde el principio. En esta guía se explica **cómo crear y publicar formularios para esas experiencias**, con una jerarquía de recomendaciones clara:

1. **Editor universal (UE): la mejor opción para la mayoría de los equipos**
2. **Creación basada en documentos (documentos/hojas): ideal para formularios rápidos y sencillos**
3. **Creación de documentos (DA): se utiliza para incrustar formularios en páginas creadas por DA**

Al final, podrá elegir el método de creación adecuado, comprender las opciones de envío y seguir los próximos pasos para obtener formularios listos para la producción.



## Elección de un método de creación

| Equipo y requisito | Método recomendado | ¿Por qué? |
|--------------------|--------------------|-----|
| Los expertos en marketing y los diseñadores necesitan un control visual, lógica condicional o integraciones de AEM | **Editor universal** | Arrastrar y soltar, reglas avanzadas, envíos a FSS o AEM Publish |
| Los autores de contenido ya trabajan en Word / GoogleDocs / Sheets; captura sencilla de datos en hojas de cálculo/por correo electrónico | **Creación basada en documentos** | Herramientas familiares, la ruta más rápida para los formularios básicos |
| Páginas del sitio web basadas en la **creación de documentos (DA)** | **Incrustar** un formulario basado en el editor universal o documentos en la página de DA | La DA no crea formularios por sí misma |


## Métodos de creación detallados

### Editor universal

El editor universal es una herramienta visual de creación de tipo arrastrar y soltar para expertos en marketing y diseñadores que combina velocidad con potencia de nivel empresarial:

- Edición de WYSIWYG en tiempo real y previsualizaciones de dispositivos.
- Reglas avanzadas e IU de validación: no se requiere código.
- Integración directa con recursos de AEM, flujos de trabajo y el modelo de datos de formulario (FDM).
- Entrega perfecta a los desarrolladores de componentes personalizados en JS/CSS sin modificaciones.
- Objetivos de envío flexibles: empiece con el **servicio de envío de formularios (FSS)** o cambie a las **acciones de envío de AEM Publish** a medida que sus necesidades aumenten.

> **Recomendación**: inicie cada nuevo proyecto de formulario con el editor universal a menos que su equipo esté 100 % centrado en los documentos y el formulario sea muy básico.


### Creación basada en documentos (Docs/Sheets)

La creación basada en documentos es ideal para crear formularios sencillos y poco complejos con herramientas conocidas, como Microsoft Word, Google Docs o Google Sheets. Este método es ideal para los equipos de contenido que necesitan una forma rápida y directa de crear formularios.

- Defina campos de formulario dentro de una tabla (Docs) o como filas (Sheets).
- Admite la validación de campos básica y Google reCAPTCHA para la protección contra spam.
- Los envíos de formularios se administran exclusivamente a través del servicio de envío de formularios.
- Publicación instantánea: cualquier cambio realizado en el documento de origen se refleja inmediatamente en el sitio sin requerir una canalización de implementación.


### Incorporación de formularios en la creación de documentos (DA)

La creación de documentos (DA) está diseñada para crear contenido de página estructurado y no admite la creación de formularios nativos. Para añadir un formulario a una página creada por DA, siga estos pasos:

1. Cree el formulario con el **editor universal** (recomendado) o mediante la creación basada en documentos.
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

## Próximos pasos

1. **Empiece con el editor universal:** consulte la [guía de introducción al editor universal](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) para comenzar a crear formularios.
2. **Configure el envío de formularios:** seleccione y configure su método de envío preferido. Consulte el [servicio de envío de formularios](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md) o las acciones de envío de AEM Publish para obtener instrucciones de configuración.
3. **Aplique las prácticas recomendadas:** revise las [prácticas recomendadas de diseño de formularios](/help/edge/docs/forms/universal-editor/best-practices-eds-forms.md) para garantizar la accesibilidad y el rendimiento.
4. **Utilice la creación basada en documentos:** para crear formularios con Microsoft Excel o Google Sheets, siga el [tutorial de creación basada en documentos](/help/edge/docs/forms/tutorial.md).
5. **Incruste formularios en la creación de documentos:** si va a crear páginas en la creación de documentos, consulte el [tutorial de DA](https://www.aem.live/developer/da-tutorial) para obtener instrucciones sobre cómo incrustar formularios publicados.

> **Ya está listo para crear su primer formulario de alto rendimiento con AEM Edge Delivery Services.**