---
title: Crear un formulario adaptable basado en componentes principales mediante plantillas de formulario XFA
description: Aprenda a crear un formulario adaptable mediante  [!DNL Experience Manager Forms] plantillas de formulario XFA o archivos XDP.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
exl-id: f3c9b798-8b20-4674-9b96-a3a0b143d947
source-git-commit: 8d43f28e62a865b6b990678544e0d9589f17722a
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 19%

---

# Crear un formulario adaptable (componentes principales) basado en plantillas de formulario XFA

<span class="preview"> La funcionalidad está disponible en el programa de primeros usuarios. Puede escribir a aem-forms-ea@adobe.com desde su ID de correo electrónico oficial para unirse al programa de primeros usuarios y solicitar acceso a esta funcionalidad. </span>

AEM as a Cloud Service proporciona a los usuarios la opción de crear Forms adaptable basado en componentes principales mediante plantillas de formulario XFA (XML Forms Architecture) o archivos `*.XDP` (XML Data Package). Esta función permite a los usuarios ahorrar tiempo migrando campos de plantilla de formulario XFA o archivos XDP directamente a Forms adaptable.

Puede cambiar el propósito de la plantilla de formulario XFA o de los archivos XDP para crear Forms adaptable basado en componentes principales. Para cambiar el propósito, cargue y asocie una plantilla de formulario XFA o archivos XDP con un formulario adaptable. Los elementos de la plantilla de formulario XFA o los archivos XDP están disponibles para su uso en el buscador de contenido durante la creación de formularios adaptables. Desde el buscador de contenido, puede arrastrar y soltar los elementos de la plantilla de formulario en el formulario.

## Ventajas de crear formularios basados en plantillas de formulario XFA o archivos XDP

Algunas de las ventajas de crear formularios basados en plantillas de formulario XFA o archivos XDP son:

* **Ahorro de tiempo**: puede reutilizar rápidamente las plantillas de formulario XFA existentes (archivos XDP) sin necesidad de volver a crear la estructura del formulario, lo que ahorra tiempo y esfuerzo durante el proceso de creación.
* **Migración sin esfuerzo**: Si ya tiene plantillas de formulario XFA en uso, esta opción proporciona una ruta de migración sencilla a Forms adaptable, lo que le permite aprovechar las ventajas de los componentes principales modernos de AEM sin perder los datos y la lógica de formulario existentes.
* **Experiencia del usuario mejorada**: Los Forms adaptables son más adaptables y personalizables que los formularios XFA. Al realizar la transición a un Forms adaptable, puede garantizar una experiencia más fácil de usar en diferentes dispositivos y tamaños de pantalla.
* **Integración mejorada**: el Forms adaptable se integra mejor con otras características, como flujos de trabajo, enlaces de datos y envíos de formularios, lo que permite flujos de trabajo más suaves y una mejor administración general de los formularios.

## Requisitos previos

Para crear un formulario adaptable basado en componentes principales que utilicen plantillas de formulario XFA o archivos XDP, es necesario lo siguiente:

* Instale la última versión para habilitar los componentes principales adaptables de Forms para su entorno de AEM Cloud Service.
* Se recomienda estar familiarizado con las siguientes áreas:
   * Crear un formulario adaptable
   * XFA (arquitectura de formularios en XML)

## Crear un formulario adaptable mediante plantillas de formulario XFA o archivos XDP

Siga estos pasos para crear un formulario adaptable mediante plantillas de formulario XFA o XDP:

1. Inicie sesión en la instancia de autor de [!DNL Experience Manager Forms].
1. Introduzca sus credenciales en la página de inicio de sesión de Experience Manager. Cuando haya iniciado sesión, en la esquina superior izquierda, seleccione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.

   ![Forms y documentos](/help/forms/assets/create-fdm.png)

1. Seleccione **[!UICONTROL Crear]** > **[!UICONTROL Forms adaptable]**.

   ![Crear formulario adaptable](/help/forms/assets/create-af.png)

   Se abre el asistente de creación de formularios.
1. En la pestaña **Source**, seleccione una plantilla basada en componentes principales.

   ![Seleccionar plantilla](/help/forms/assets/select-template.png)

   Al seleccionar una plantilla, se seleccionan automáticamente un tema y una acción de envío especificados en la plantilla, y se habilita el botón **[!UICONTROL Crear]**.

   ![Seleccionar tema](/help/forms/assets/select-form-theme.png)

1. Seleccione **[!UICONTROL Crear]**. Aparecerá un cuadro de diálogo para especificar el título, el nombre y la ubicación para guardar el formulario adaptable.
1. Especifique su título, nombre y ubicación.
1. Seleccione **[!UICONTROL Crear]**.
   ![Proporcionar nombre y título](/help/forms/assets/create-form.png)

   Se crea un formulario adaptable que se abre en el editor de formularios adaptables. El editor muestra el contenido disponible en la plantilla.
1. Seleccione ![Información de página](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL Abrir propiedades]**.

   ![Abrir propiedades](/help/forms/assets/form-properties.png)

   Se abre la página Propiedades del formulario.
1. Vaya a la pestaña **[!UICONTROL Modelo de formulario]** y elija **Plantillas de formulario**.
1. Seleccione el archivo .xdp en la lista desplegable.

   ![Seleccionar archivo XDP](/help/forms/assets/select-xdp-file.png)

   Aparece un cuadro de diálogo de advertencia en la pantalla. Haga clic en **Aceptar** para continuar.

   ![Cuadro de diálogo de advertencia](/help/forms/assets/fdm-warning.png)

1. Seleccione **[!UICONTROL Guardar y cerrar]** para guardar las propiedades.

   >[!NOTE]
   >
   > Después de seleccionar **Plantillas de formulario** en la ficha Modelo de formulario **3&rbrace;, no se puede cambiar.**


Se crea un formulario adaptable que se abre en el editor de formularios adaptables. El editor muestra el contenido disponible en la plantilla.  En función del tipo de formulario adaptable, los elementos del formulario presentes en la plantilla de formulario XFA asociada se muestran en la pestaña **[!UICONTROL Objetos del modelo de datos]** del **[!UICONTROL Explorador de contenido]** de la barra lateral. También puede arrastrar y soltar estos elementos para crear su formulario adaptable.

>[!NOTE]
>
> Puede deshabilitar los scripts para los campos de formulario XDP mediante la barra de herramientas del panel del campo agregado. Cree lógicas para los campos agregados usando el [Editor visual de reglas](/help/forms/rule-editor-core-components.md).

