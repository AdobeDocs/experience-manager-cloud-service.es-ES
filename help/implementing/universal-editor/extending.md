---
title: Ampliación del editor universal
description: Obtenga información acerca de las distintas opciones para ampliar las capacidades del editor universal y satisfacer las necesidades de los autores de contenido.
feature: Developing
role: Admin, Developer
exl-id: 2f487fa5-57a7-477a-ad68-590e6cc12f4e
source-git-commit: 9adf2bc4f9f25ee7fc0a39b0f1a3ae9e45fce7d2
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 100%

---

# Ampliación del editor universal {#extending}

Obtenga información acerca de las distintas opciones para ampliar las capacidades del editor universal y satisfacer las necesidades de los autores de contenido.

>[!TIP]
>
>El editor universal también ofrece varias [opciones de personalización](/help/implementing/universal-editor/customizing.md) que le permiten satisfacer mejor las necesidades de su proyecto.

## Extensiones {#extensions}

Como servicio de Adobe Experience Cloud, la IU del editor universal se puede ampliar con App Builder y Experience Manager. Adobe ofrece muchas extensiones listas para usarse disponibles a través de [Extension Manager](https://experience.adobe.com/aem/extension-manager) que puede usar para su proyecto.

* **[Extensión de administración de varios sitios de AEM (MSM)](/help/sites-cloud/authoring/universal-editor/authoring.md#inheritance)**: interrumpa o restablezca la herencia en el nivel de componente
* **[Extensión de propiedades de la página de AEM](/help/sites-cloud/authoring/universal-editor/authoring.md#page-properties)**: acceda a la ventana de propiedades de la página desde el editor universal
* **[Extensión de administración de sitios de AEM](/help/sites-cloud/authoring/universal-editor/authoring.md#sites-console)**: abra la consola de Sites en la ubicación de la página en el editor universal
* **[Extensión de bloqueo de página de AEM](/help/sites-cloud/authoring/universal-editor/authoring.md#locking-pages)**: vea y cambie el estado del bloqueo de página desde el editor universal
* **[Extensión de flujos de trabajo de AEM](/help/sites-cloud/authoring/universal-editor/authoring.md#workflows)**: inicie flujos de trabajo en la página y contenido de página desde el editor universal
* **[Generar variaciones](/help/generative-ai/generate-variations-integrated-editor.md)**: use la inteligencia artificial generativa (IA) para crear variaciones para el contenido directamente en el panel de propiedades.
* **[Selector de productos de AEM para el editor universal](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/ue-product-picker/)**: integre datos de Adobe Commerce seleccionando o eliminando datos de productos del editor.
* **[Borradores de contenido del editor universal](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/universal-editor-content-drafts/)**: cree, edite y administre varios borradores de contenido.
* **[Selector de recursos configurable](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/)**: habilite la selección de recursos desde repositorios que no sean los utilizados por la página editada.
* **Editor de reglas de Forms**: añada comportamientos dinámicos a los campos de AEM Forms visualmente, sin codificación.
* **[Exportar fragmentos de contenido a Adobe Target](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/exporting-content-fragment-to-adobe-target/)**: exporte los fragmentos de contenido, creados en Adobe Experience Manager as a Cloud Service, a Adobe Target para usarlos como ofertas en actividades de Target, para probarlos y para personalizar experiencias a escala.
* **[Flujos de trabajo de fragmentos de contenido](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/content-fragments-workflows/)**: inicie un flujo de trabajo de AEM para los fragmentos de contenido seleccionados.

Para obtener información acerca de cómo habilitar estas extensiones, [consulte la documentación de Extension Manager.](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)

## Ampliación de la IU {#extending-ui}

Las extensiones de IU del editor universal son aplicaciones JavaScript creadas con Adobe App Builder. Con estas mismas herramientas, también puede añadir sus propios botones y acciones al menú de encabezado y al panel de propiedades, así como crear sus propios eventos para el editor universal.

Si desea explorar las posibilidades de crear sus propias extensiones, consulte los siguientes recursos:

1. [Extensibilidad de la IU](https://developer.adobe.com/uix/docs/): esta es la documentación para desarrolladores para la extensión de la IU.
1. [Guías de extensibilidad de la IU](https://developer.adobe.com/uix/docs/guides/): instrucciones paso a paso sobre cómo desarrollar su propia extensión
1. [Puntos de extensión de la IU del editor universal](https://developer.adobe.com/uix/docs/services/aem-universal-editor/): documentación del punto de extensión específico del editor universal

>[!TIP]
>
>Si prefiere aprender con el ejemplo, consulte el [tutorial de extensibilidad de la IU de AEM](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/developing/extensibility/ui/overview). Aunque se centra en ampliar la consola de fragmentos de contenido, los conceptos para implementar una extensión de IU en el editor universal son los mismos.

[Con Extension Manager en AEM Sites](https://developer.adobe.com/uix/docs/extension-manager/), puede habilitar o deshabilitar las extensiones por instancia, tener acceso a las extensiones de origen de Adobe, incluidas las del editor universal, y mucho más.

## Puntos de extensión {#extension-points}

Además de la extensibilidad de la IU, el editor universal ofrece muchos otros puntos de extensión flexibles para permitir la integración perfecta de los requisitos empresariales personalizados.

* **[Bloques](https://www.aem.live/developer/block-collection)**: con un formato JSON simple, los proyectos pueden ajustar los bloques y las funciones UE disponibles para la creación de contenido.
* **[Interfaz de usuario personalizada](#extending-ui)**: las extensiones pueden mostrar la IU necesaria en paneles laterales o cuadros de diálogo modales.
* **[Eventos](/help/implementing/universal-editor/events-universal-editor.md)**: las extensiones reciben eventos sobre las acciones y selecciones del autor en la página para responder de forma adecuada.
