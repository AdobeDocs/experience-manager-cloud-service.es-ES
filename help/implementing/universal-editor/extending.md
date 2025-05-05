---
title: Ampliación del editor universal
description: Obtenga información acerca de las distintas opciones para ampliar las capacidades del Editor universal para satisfacer las necesidades de los autores de contenido.
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 0cab4a807be4aa402667feddb6a948f0d2db371f
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---


# Ampliación del editor universal {#extending}

Obtenga información acerca de las distintas opciones para ampliar las capacidades del Editor universal para satisfacer las necesidades de los autores de contenido.

>[!TIP]
>
>El editor universal también ofrece varias [opciones de personalización](/help/implementing/universal-editor/customizing.md) que le permiten satisfacer mejor sus necesidades de proyecto.

## Extensiones  {#extensions}

Como servicio de Adobe Experience Cloud, la interfaz de usuario del editor universal se puede ampliar con App Builder y Experience Manager. Adobe ofrece muchas extensiones listas para su uso que puede utilizar para su proyecto.

* **[Selector de productos AEM para el editor universal](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/ue-product-picker/)**: integre datos de Adobe Commerce seleccionando o eliminando datos de productos del editor.
* **[Borradores de contenido de editor universal](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/universal-editor-content-drafts/)**: cree, edite y administre varios borradores de contenido.
* **[Selector de recursos configurable](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/)**: habilite la selección de recursos desde repositorios que no sean los utilizados por la página editada.
* **Editor de reglas de Forms**: agregue el comportamiento dinámico a los campos de AEM Forms visualmente, sin codificación.
* **[Exportar fragmentos de contenido a Adobe Target](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/exporting-content-fragment-to-adobe-target/)**: exporte los fragmentos de contenido, creados en Adobe Experience Manager as a Cloud Service a Adobe Target para usarlos como ofertas en actividades de Target, para probar y personalizar experiencias a escala.
* **[Flujos de trabajo de fragmentos de contenido](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/content-fragments-workflows/)**: inicie un flujo de trabajo de AEM para los fragmentos de contenido seleccionados.

## Ampliación de la IU {#extending-ui}

Las extensiones de IU del editor universal son aplicaciones de JavaScript creadas con Adobe App Builder. Con estas mismas herramientas, también puede agregar sus propios botones y acciones al menú de encabezado y al panel de propiedades, así como crear sus propios eventos para el editor universal.

Si desea explorar las posibilidades de crear sus propias extensiones, consulte los siguientes recursos:

1. [Extensibilidad de la interfaz de usuario](https://developer.adobe.com/uix/docs/): esta es la documentación para desarrolladores para la extensión de la interfaz de usuario.
1. [Guías de extensibilidad de la IU](https://developer.adobe.com/uix/docs/guides/): instrucciones paso a paso sobre cómo desarrollar su propia extensión
1. [Puntos de extensión de la interfaz de usuario del editor universal](https://developer.adobe.com/uix/docs/services/aem-universal-editor/): documentación del punto de extensión específico del editor universal

>[!TIP]
>
>Si prefiere aprender con el ejemplo, consulte el [tutorial de extensibilidad de la IU de AEM](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/developing/extensibility/ui/overview). Aunque se centra en ampliar la consola de fragmentos de contenido, los conceptos para implementar una extensión de interfaz de usuario en el editor universal son los mismos.

[Con Extension Manager en AEM Sites](https://developer.adobe.com/uix/docs/extension-manager/), puede habilitar o deshabilitar las extensiones por instancia, tener acceso a las extensiones de origen de Adobe, incluidas las del editor universal, y mucho más.

## Puntos de extensión {#extension-points}

Además de la extensibilidad de la interfaz de usuario, el editor universal ofrece muchos otros puntos de extensión flexibles para permitir la integración perfecta de los requisitos empresariales personalizados.

* **[Bloques](/help/edge/developer/block-collection.md)**: en formato JSON simple, los proyectos pueden ajustar los bloques y las características de uso disponibles para la creación de contenido.
* **[Interfaz de usuario personalizada](#extending-ui)**: las extensiones pueden mostrar la interfaz de usuario necesaria en paneles laterales o cuadros de diálogo modales.
* **[Eventos](/help/implementing/universal-editor/events.md)**: las extensiones reciben eventos sobre las acciones y selecciones del autor en la página para responder correctamente.
