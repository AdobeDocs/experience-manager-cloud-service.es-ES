---
title: ¿Cómo se integra el modelo de datos de formulario (FDM) para un formulario en el editor universal?
description: Aprenda a crear formularios basados en un modelo de datos de formulario (FDM). Genere y edite datos de muestra para objetos del modelo de datos en el modelo de datos de formulario (FDM).
feature: Edge Delivery Services, Form Data Model
role: Admin, User
exl-id: 9ce51223-57d0-47d8-8868-84b37d4e8e3e
source-git-commit: e1ead9342fadbdf82815f082d7194c9cdf6d799d
workflow-type: tm+mt
source-wordcount: '1271'
ht-degree: 94%

---

# Integración de formularios con el modelo de datos de formulario en el editor universal

La integración de formularios con un modelo de datos de formulario (FDM) en el editor universal permite utilizar diversas fuentes de datos back-end para crear un modelo de datos de formulario (FDM). Puede utilizar el modelo de datos de formulario (FDM) como esquema en varios flujos de trabajo de formulario. Configure las fuentes de datos y cree un modelo de datos de formulario (FDM) basado en los objetos y servicios de modelo de datos disponibles en las fuentes de datos. 

## Consideraciones

* Si no ve el icono **Fuentes de datos** en su interfaz del editor universal o la propiedad **Referencia de enlace** en el panel de propiedades de la derecha, habilite la extensión **Fuente de datos** en **Extension Manager**.

  ![Captura de pantalla de la interfaz de Extension Manager del editor universal que muestra las extensiones disponibles, incluida la extensión de fuentes de datos que se puede habilitar para la integración de formularios](/help/edge/docs/forms/universal-editor/assets/extension-manager.png)

  Consulte el artículo [Características destacadas de las funciones de Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) para obtener información sobre cómo habilitar y deshabilitar las extensiones del editor universal.

* Actualmente no se admite el servicio de rellenado previo para formularios en el editor universal.

## Requisitos previos

Antes de configurar el formulario con el modelo de datos de formulario en el editor universal, asegúrese de completar los siguientes pasos:

* [Configuración de la fuente de datos](/help/forms/configure-data-sources.md): configure la fuente de datos para conectar el formulario a los datos de back-end.
* [Creación de un modelo de datos de formulario (FDM)](/help/forms/create-form-data-models.md): cree un modelo de datos mediante objetos y servicios de datos de la fuente de datos configurada.
* [Configuración de objetos y servicios de modelo de datos](/help/forms/work-with-form-data-model.md): asigne los objetos y servicios de modelo de datos para garantizar un flujo de datos fluido entre el formulario y la fuente de datos.

## Creación de formularios con el modelo de datos de formulario en el editor universal

En el editor universal, puede crear lo siguiente:

* [Formulario basado en esquema](#schema-based-form): un formulario basado en un esquema utiliza una fuente de datos configurada durante la creación del formulario en la pestaña **Datos**, que enlaza automáticamente los datos a los campos del formulario.
* [Formulario no basado en esquema](#non-schema-based-form): un formulario no basado en un esquema requiere que se añada manualmente una fuente de datos y se enlace cada campo del árbol de contenido.

![Tipos de formulario del editor universal](/help/edge/docs/forms/universal-editor/assets/form-types.png){width="50%" align="center" height="50%"}

Estos métodos le ofrecen la posibilidad de conectar modelos de datos con formularios basados en sus necesidades.

### Formulario basado en esquema

Cuando se crea un formulario basado en un esquema, se configura automáticamente con una fuente de datos y los campos del formulario ya están vinculados a los datos a través de enlaces de datos. Para crear un formulario basado en esquema mediante el asistente para la creación de formularios, realice los siguientes pasos:

1. Inicie sesión en la instancia de autor de [!DNL Experience Manager Forms].
1. Introduzca sus credenciales en la página de inicio de sesión de Experience Manager. Cuando haya iniciado sesión, en la esquina superior izquierda, seleccione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.
1. Seleccione **[!UICONTROL Crear]** > **[!UICONTROL Formularios adaptables]**. Se abre el asistente. En la pestaña **Fuente**, seleccione una plantilla:

   ![Plantilla de Edge Delivery Services](/help/edge/assets/create-eds-forms.png)

   Al seleccionar una plantilla basada en Edge Delivery Services, se habilita el botón **[!UICONTROL Crear]**. Puede ir a las pestañas **[!UICONTROL Fuente de datos]** o **[!UICONTROL Envío]** para seleccionar una fuente de datos o acción de envío.

1. En la pestaña **Datos**, puede seleccionar uno de los siguientes modelos de datos:

   * **Modelo de datos de formulario (FDM)**: integre objetos y servicios de modelo de datos desde las fuentes de datos en su formulario. Elija Modelo de datos de formulario (FDM) si el formulario requiere leer y escribir datos de varias fuentes.

   * **Esquema JSON**: integre su formulario con un sistema back-end asociando un esquema JSON que defina la estructura de datos. Le permite añadir contenido dinámico mediante los elementos de esquema.

     Por ejemplo, seleccione el modelo de datos de formulario creado denominado Modelo de datos de formulario Pet.

     ![Seleccionar modelo de datos de formulario](/help/edge/docs/forms/universal-editor/assets/select-petstore-form-data-model.png)


     De forma predeterminada, todos los campos del esquema JSON asociado o Modelo de datos de formulario (FDM) se seleccionan automáticamente y se convierten en los correspondientes componentes, lo que simplifica el proceso de creación. El asistente también le permite elegir selectivamente qué campos incluir en el formulario mediante casillas de verificación.

1. Haga clic en **[!UICONTROL Crear]** y aparece el asistente **Crear formulario**.
1. Especifique el **Nombre** y **Título**.
1. Especifique la **URL de GitHub**. Por ejemplo, si el repositorio de GitHub se llama `edsforms` y está ubicado en la cuenta `wkndforms`, la URL es la siguiente:
   `https://github.com/wkndforms/edsforms`
1. Haga clic en **[!UICONTROL Crear]**.

   ![Crear formulario basado en esquema](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form.png)

   Tan pronto como haga clic en **[!UICONTROL Crear]**, el formulario se abre en el editor universal para la creación.

   ![Captura de pantalla del editor universal que muestra un formulario basado en esquema con campos de formulario previamente rellenados y el explorador de contenido que muestra los elementos de origen de datos disponibles](/help/edge/docs/forms/universal-editor/assets/schema-based-form-in-ue.png)

   El formulario se crea utilizando los elementos de datos de la fuente de datos asociada, con los campos de formulario que tienen enlaces de datos preconfigurados.

   ![Enlace de datos automáticos](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

   Ahora puede añadir y [configurar la acción de envío](/help/edge/docs/forms/universal-editor/submit-action.md) para su formulario.

### Formulario no basado en esquema

Cuando se crea un formulario no basado en un esquema, no se configura ninguna fuente de datos. Puede editar las propiedades del formulario más adelante para añadir una fuente de datos y configurar manualmente enlaces de datos para los campos del formulario. Siga estos pasos para editar las propiedades del formulario y añadir una fuente de datos:

1. Inicie sesión en la instancia de autor de [!DNL Experience Manager Forms].
1. Introduzca sus credenciales en la página de inicio de sesión de Experience Manager. Cuando haya iniciado sesión, en la esquina superior izquierda, seleccione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.
1. Seleccione el formulario para el que desea añadir una fuente de datos y haga clic en **[!UICONTROL Propiedades]**.
   ![Abrir propiedades del formulario](/help/edge/docs/forms/universal-editor/assets/non-schema-based-edit-properties.png)

   Se abren las propiedades del formulario.
1. Haga clic para abrir la pestaña **Modelo de formulario** y en el menú desplegable **Seleccionar de**. Puede seleccionar una de las siguientes opciones:

   * **Modelo de datos de formulario (FDM)**: cree el formulario mediante un modelo de datos de formulario.
   * **Conector**: cree el formulario mediante la fuente de datos de Adobe Marketo.
   * **Esquema**: cree el formulario mediante un esquema JSON cargado en AEM Forms.
   * **Ninguno**: cree el fragmento desde cero sin usar ningún modelo de formulario.

     Por ejemplo, seleccione el modelo de datos de formulario (FDM)

     ![Seleccionar pestaña Modelo de formulario](/help/edge/docs/forms/universal-editor/assets/select-form-model.png)

1. Seleccione el modelo de datos de formulario (FDM) creado en la lista desplegable. Por ejemplo, seleccione el modelo de datos de formulario creado denominado Modelo de datos de formulario Pet en la lista desplegable.

   ![Seleccionar FDM](/help/edge/docs/forms/universal-editor/assets/select-fdm.png)

   Al seleccionar el Modelo de datos de formulario (FDM), aparecerá el cuadro de diálogo de advertencia. Haga clic en **Aceptar** para cerrar el cuadro de diálogo.

   ![Asistente para modelo de formulario](/help/edge/docs/forms/universal-editor/assets/form-model-wizard.png)

1. Haga clic en **[!UICONTROL Guardar y cerrar]**.
1. Abra el formulario para editarlo. El formulario se abrirá en el editor universal para la creación.

   ![Creación de formulario no basado en esquema](/help/edge/docs/forms/universal-editor/assets/non-schema-form-authoring.png)

   Los elementos del formulario presentes en el modelo de datos de formulario (FDM) asociado se muestran en la pestaña **[!UICONTROL Fuente de datos]** del **[!UICONTROL Explorador de contenido]** en el **Panel de propiedades**.

   ![Fuente de datos del formulario](/help/edge/docs/forms/universal-editor/assets/non-schema-data-source.png)

1. Seleccione los elementos de datos en la pestaña **[!UICONTROL Fuente de datos]** y haga clic en **[!UICONTROL Añadir]**.

   ![Añadir elementos de datos](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-element.png)

   También puede arrastrar y soltar estos elementos para crear su formulario adaptable. Al hacer clic en **[!UICONTROL Añadir]**, los elementos seleccionados en la pestaña **[!UICONTROL Fuente de datos]** se añaden al formulario y aparece una marca de verificación delante de los elementos añadidos.

   ![Captura de pantalla que muestra el editor universal con un formulario sin esquema que se está creando al arrastrar y soltar elementos de datos de la pestaña Data Source en la estructura del formulario](/help/edge/docs/forms/universal-editor/assets/non-schema-form.png)

Puede añadir un enlace de datos a un campo de formulario seleccionándolo en la propiedad **Referencia de enlace**. Por ejemplo, vamos a añadir una referencia de enlace de datos al cuadro de texto **Id** que ya está presente en el formulario.
Para seleccionar el enlace de datos para el campo de formulario del árbol de fuentes de datos, realice los siguientes pasos:

1. Abra las propiedades del campo de formulario para el que desea añadir la referencia de enlace de datos.
1. Vaya a la propiedad **Referencia de enlace** y haga clic en el icono **Examinar**.

   ![Añadir manualmente el enlace de datos para un campo de formulario](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-binding.png)

1. Elija la referencia de enlace de datos del árbol de fuentes de datos en el asistente **Seleccionar una referencia de enlace**.

   ![seleccionar referencia de enlace de datos](/help/edge/docs/forms/universal-editor/assets/select-bind-reference.png)

1. Seleccione el elemento de datos del árbol de fuente de datos que desea enlazar al campo de formulario y haga clic en **Seleccionar**.

   ![seleccionar elemento de datos](/help/edge/docs/forms/universal-editor/assets/select-data-element.png)

   El campo de formulario se enlaza al elemento de datos y aparece en la propiedad **Referencia de enlace**.

   ![Enlace de datos automáticos](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

   También puede editar manualmente la propiedad **Referencia de enlace** para el campo del formulario.

Ahora puede añadir y [configurar la acción de envío](/help/edge/docs/forms/universal-editor/submit-action.md) para su formulario.

## Véase también

{{universal-editor-see-also}}
