---
title: Funciones de diseño de Forms adaptable
seo-title: Layout capabilities of Adaptive Forms
description: El diseño y los aspectos visuales de Adaptive Forms en varios dispositivos se rigen por la configuración de diseño. Comprenda los distintos diseños y cómo aplicarlos.
exl-id: e30c6ff9-692b-4415-8f14-b4ef616b2d12
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 1%

---

# Funciones de diseño de Forms adaptable {#layout-capabilities-of-adaptive-forms}

[!DNL Adobe Experience Manager] permite crear Forms adaptable fácil de usar que ofrezca experiencias dinámicas a los usuarios finales. La presentación del formulario controla cómo se muestran los elementos o los componentes en un formulario adaptable.

<!-- ## Prerequisite knowledge {#prerequisite-knowledge}

Before learning about the different layout capabilities of Adaptive Forms, read [Introduction to authoring forms](introduction-forms-authoring.md) to know more about Adaptive Forms. -->

## Tipos de diseños {#types-of-layouts}

Un formulario adaptable proporciona los siguientes tipos de diseños:

**[!UICONTROL Diseño de panel]** Controla cómo se muestran los elementos o componentes dentro de un panel en un dispositivo.

**[!UICONTROL Diseño móvil]** Controla la navegación de un formulario en un dispositivo móvil. Si el ancho del dispositivo es de 768 píxeles o más, el diseño se considera un diseño para móviles y se optimiza para un dispositivo móvil.

**[!UICONTROL Diseño de barra de herramientas]** Controla la colocación de los botones Acción en la barra de herramientas o la barra de herramientas del panel en un formulario.

Todos estos diseños de panel se definen en la `/libs/fd/af/layouts` ubicación.

Para cambiar la presentación de un formulario adaptable, utilice el modo de creación en [!DNL Experience Manager].

## [!UICONTROL Diseño de panel] {#panel-layout}

Un autor de formularios puede asociar una presentación a cada panel de un formulario adaptable, incluido el panel raíz.

Los diseños de panel están disponibles en `/libs/fd/af/layouts/panel` ubicación. Pulse el panel y seleccione ![cmppr1](assets/configure-icon.svg) para ver las propiedades del panel.

![Lista de diseños de panel para el panel raíz de un formulario adaptable](assets/layouts.png)

### [!UICONTROL Interactivo: todo en una página sin navegación] {#responsive-everything-on-one-page-without-navigation-br}

Utilice este diseño de panel para crear un diseño interactivo que se ajuste al tamaño de pantalla del dispositivo sin necesidad de navegación especializada.

Con este diseño, puede colocar varias **[!UICONTROL Formulario adaptable del panel]** componentes uno tras otro dentro del panel.

![Un formulario con presentación interactiva, tal como se ve en una pantalla pequeña](assets/responsive-layout.png)

### [!UICONTROL Asistente] {#wizard}

Utilice este diseño de panel para proporcionar navegación guiada dentro de un formulario. Por ejemplo, utilice esta presentación cuando desee capturar información obligatoria en un formulario y guiar a los usuarios paso a paso.

Utilice la variable **[!UICONTROL Formulario adaptable del panel]** para proporcionar navegación paso a paso dentro de un panel. Cuando se utiliza este diseño, el usuario solo pasa al siguiente paso una vez completado el paso actual

```javascript
window.guideBridge.validate([], this.panel.navigationContext.currentItem.somExpression)
```

![Un formulario con presentación de asistente](assets/wizard-layout2.png)

### [!UICONTROL Acordeón] {#layout-for-accordion-design}

Con este diseño, puede colocar la variable **[!UICONTROL Formulario adaptable del panel]** en un panel con navegación de estilo de acordeón. Con este diseño, también puede crear paneles repetibles. Los paneles repetibles permiten agregar o quitar paneles de forma dinámica según sea necesario. Puede definir el número mínimo y máximo de veces que se repite un panel. Además, el título del panel se puede determinar dinámicamente, en función de la información proporcionada en los elementos del panel.

La expresión de resumen se puede utilizar para mostrar los valores proporcionados por el usuario final en el título del panel minimizado.

![Paneles repetibles con diseño de acordeón en Forms adaptable](assets/accordion-layout.png)

### [!UICONTROL Presentación en fichas: las pestañas aparecen a la izquierda ]{#tabbed-layout-tabs-appear-on-the-left}

Con este diseño, puede colocar la variable **[!UICONTROL Formulario adaptable del panel]** en un panel con navegación por pestañas. Las pestañas se colocan a la izquierda del contenido del panel.

![En la presentación Tabulación, las pestañas aparecen a la izquierda](assets/tabs-on-left.png)

Pestañas que aparecen a la izquierda de un panel

### [!UICONTROL Presentación en fichas: las pestañas aparecen en la parte superior] {#tabbed-layout-tabs-appear-on-the-top}

Con este diseño, puede colocar la variable **[!UICONTROL Formulario adaptable del panel]** Componente de un panel con navegación por fichas. Las pestañas se colocan sobre el contenido del panel.

![Diseño en fichas en Adaptive Forms con pestañas en la parte superior](assets/tabs-on-top.png)

## Presentaciones móviles {#mobile-layouts}

Los diseños móviles permiten una navegación fácil de usar en los dispositivos móviles con pantallas relativamente más pequeñas. Los diseños móviles utilizan estilos con pestañas o de asistente para la navegación por formularios. La aplicación de un diseño para móvil proporciona una única presentación para todo el formulario.

Este diseño controla la navegación mediante una barra de navegación y un menú de navegación. La barra de navegación muestra **&lt;** y **>** para indicar **[!UICONTROL next]** y **[!UICONTROL previous]** pasos de navegación en el formulario.

Los diseños móviles están disponibles en `/libs/fd/af/layouts/mobile/` ubicación. De forma predeterminada, los siguientes diseños móviles están disponibles en Forms adaptable.

![Lista de diseños móviles en Forms adaptable](assets/mobile-navigation.png)

Seleccione el **[!UICONTROL Agregar elementos navegables de diseño interactivo al menú móvil]** para ver las opciones navegables disponibles para un panel en Diseño móvil. Las opciones navegables solo están visibles si selecciona **[!UICONTROL Interactivo]** diseño para un panel.

Cuando se utiliza una presentación móvil, el menú de formulario, para acceder a varios paneles de formulario, está disponible pulsando ![aem6forms_form_menu](assets/rail-icon.svg) icono.

### [!UICONTROL Presentación con títulos de panel en el encabezado del formulario] {#layout-with-panel-titles-in-the-form-header}

Este diseño, como su nombre indica, muestra los títulos de los paneles junto con el menú de navegación y la barra de navegación. Este diseño también incluye los iconos Siguiente y Anterior para la navegación.

![Presentaciones móviles con títulos de panel en los encabezados de formulario](assets/mobile-layout1.png)

### [!UICONTROL Presentación sin títulos de panel en el encabezado del formulario ]{#layout-without-panel-titles-in-the-form-header}

Este diseño, como su nombre indica, muestra únicamente el menú de navegación y la barra de navegación sin títulos de panel. Este diseño también incluye los iconos Siguiente y Anterior para la navegación.

![Presentaciones móviles sin títulos de panel en los encabezados de formulario](assets/mobile-layout2.png)

<!-- ## Toolbar layouts {#toolbar-layouts}

A Toolbar Layout controls positioning and display of any action buttons that you add to your Adaptive Forms. The layout can be added at a form level or at a panel level.

![A list of Toolbar Layouts in Adaptive Forms to control layout of buttons](assets/toolbar-layouts.png)

A list of Toolbar Layouts in Adaptive Forms

Toolbar layouts are available at `/libs/fd/af/layouts/toolbar` location. Adaptive Forms provide the following Toolbar Layouts, by default.

### [!UICONTROL Default layout for toolbar] {#default-layout-for-toolbar}

This layout is selected as the default layout when you add any action buttons in an Adaptive Form. Selecting this layout displays the same layout for both, desktop and mobile devices.

Also, you can add multiple toolbars containing action buttons configured with this layout. An action button is associated with a form control. You can configure the toolbars to be before or after a panel.

![Default view for toolbar](assets/toolbar_layout_default.png)

Default view for toolbar

### [!UICONTROL Mobile fixed layout for toolbar] {#mobile-fixed-layout-for-toolbar}

Select this layout to provide alternate layouts for desktop and mobile devices.

For the desktop layout, you can add Action buttons using some specific labels. Only one toolbar can be configured with this layout. If more than one toolbar is configured with this layout, there is an overlap for mobile devices and only one toolbar is visible. For example, you can have a toolbar at the bottom or the top of the form, or, after or before panels in the form.

For the Mobile layout, you can add action buttons using icons.

![Mobile fixed layout for toolbar](assets/toolbar_layout_mobile_fixed.png)

Mobile fixed layout for toolbar-->
