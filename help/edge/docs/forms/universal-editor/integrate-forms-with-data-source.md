---
title: Crear un modelo de datos de formulario (FDM) para un formulario en el editor universal
description: Aprenda a crear formularios basados en un modelo de datos de formulario (FDM). Generar y editar datos de ejemplo para objetos de modelo de datos en el modelo de datos de formulario (FDM).
feature: Edge Delivery Services, Form Data Model
role: Admin, User
hide: true
hidefromtoc: true
source-git-commit: e2259e542df5a12748705af901d073e4486292c4
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 11%

---


# Integrar formularios con el modelo de datos de formulario en el editor universal

La integración de formularios con un modelo de datos de formulario (FDM) en el editor universal permite utilizar diversas fuentes de datos back-end para crear un modelo de datos de formulario (FDM). Puede utilizar el modelo de datos de formulario (FDM) como esquema en varios flujos de trabajo de formulario. Configure las fuentes de datos y cree un modelo de datos de formulario (FDM) basado en los objetos y servicios de modelo de datos disponibles en las fuentes de datos.

## Consideración

* Actualmente no se admite el servicio de rellenado previo para formularios en el editor universal.

## Requisitos previos

Antes de configurar el formulario con el modelo de datos de formulario en el editor universal, asegúrese de completar los siguientes pasos:

* [Configurar Source de datos](/help/forms/configure-data-sources.md): configure el origen de datos para conectar el formulario a los datos del servidor.
* [Crear modelo de datos de formulario (FDM)](/help/forms/create-form-data-models.md): cree un modelo de datos con objetos y servicios de datos de la fuente de datos configurada.
* [Configurar objetos y servicios del modelo de datos](/help/forms/work-with-form-data-model.md): asigne los objetos y servicios del modelo de datos para garantizar un flujo de datos fluido entre el formulario y el origen de datos.

## Crear Forms con el modelo de datos de formulario en el editor universal

En el editor universal, puede crear lo siguiente:
* [Formulario basado en esquemas](#schema-based-form): un formulario basado en esquemas utiliza un origen de datos configurado durante la creación del formulario en la ficha **Datos**, que enlaza automáticamente los datos a los campos del formulario.
* [Formulario no basado en esquema](#non-schema-based-form): Un formulario no basado en esquema requiere que agregue manualmente un origen de datos y enlace cada campo del árbol de contenido.

![Tipos de formulario en el editor universal](/help/edge/docs/forms/universal-editor/assets/form-types.png){width="50%" align="center" height="50%"}

Estos métodos le proporcionan la flexibilidad para conectar modelos de datos con formularios basados en sus necesidades.

### Formulario basado en esquemas

Cuando se crea un formulario basado en esquemas, se configura automáticamente con una fuente de datos y los campos del formulario ya están vinculados a los datos a través de enlaces de datos. Para crear un formulario basado en esquemas mediante el asistente para la creación de formularios, realice los siguientes pasos:

1. Inicie sesión en la instancia de autor de [!DNL Experience Manager Forms].
2. Introduzca sus credenciales en la página de inicio de sesión de Experience Manager. Cuando haya iniciado sesión, en la esquina superior izquierda, seleccione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.
3. Seleccione **[!UICONTROL Crear]** > **[!UICONTROL Formularios adaptables]**. Se abre el asistente. En la ficha **Source**, seleccione una plantilla:

   ![Plantilla de Edge Delivery Services](/help/edge/assets/create-eds-forms.png)

   Al seleccionar una plantilla basada en Edge Delivery Services, se habilita el botón **[!UICONTROL Crear]**. Puede ir a las pestañas **[!UICONTROL Source de datos]** o **[!UICONTROL Envío]** para seleccionar un origen de datos o una acción de envío.

4. En la ficha **Datos**, puede seleccionar uno de los siguientes modelos de datos:

   * **Modelo de datos de formulario (FDM)**: integre objetos y servicios de modelo de datos de fuentes de datos en su formulario. Elija Modelo de datos de formulario (FDM) si el formulario requiere leer y escribir datos de varias fuentes.

   * **Esquema JSON**: integre el formulario con un sistema backend al asociar un esquema JSON que define la estructura de datos. Permite añadir contenido dinámico mediante los elementos de esquema.

     Por ejemplo, seleccione el modelo de datos de formulario creado denominado Modelo de datos de formulario para mascotas.

     ![Seleccionar modelo de datos de formulario](/help/edge/docs/forms/universal-editor/assets/select-petstore-form-data-model.png)


     De forma predeterminada, todos los campos del esquema JSON o del modelo de datos de formulario (FDM) asociado se seleccionan automáticamente y se convierten en los componentes de formulario correspondientes, lo que simplifica el proceso de creación. El asistente también le permite elegir selectivamente qué campos incluir en el formulario mediante casillas de verificación.

5. Haga clic en **[!UICONTROL Crear]** y aparecerá el asistente **Crear formulario**.
6. Especifique **Name** y **Title**.
7. Especifique la **URL de GitHub**. Por ejemplo, si el repositorio de GitHub se llama `edsforms` y se encuentra en la cuenta `wkndforms`, la dirección URL es:
   `https://github.com/wkndforms/edsforms`
8. Haga clic en **[!UICONTROL Crear]**.

   ![Crear formulario basado en esquema](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form.png)

   Tan pronto como haga clic en **[!UICONTROL Crear]**, el formulario se abrirá en el editor universal para la creación.

   ![crear el formulario](/help/edge/docs/forms/universal-editor/assets/schema-based-form-in-ue.png)

   El formulario se crea utilizando los elementos de datos de la fuente de datos asociada, con los campos de formulario que tienen enlaces de datos preconfigurados.

   ![Enlace Automático De Datos](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

   Ahora puede agregar y [configurar la acción de envío](/help/edge/docs/forms/universal-editor/submit-action.md) para su formulario.

### Formulario no basado en esquemas

Cuando se crea un formulario no basado en esquemas, no se configura ninguna fuente de datos. Puede editar las propiedades del formulario más adelante para agregar una fuente de datos y configurar manualmente los enlaces de datos para los campos del formulario. Siga estos pasos para editar las propiedades del formulario y agregar una fuente de datos:

1. Inicie sesión en la instancia de autor de [!DNL Experience Manager Forms].
1. Introduzca sus credenciales en la página de inicio de sesión de Experience Manager. Cuando haya iniciado sesión, en la esquina superior izquierda, seleccione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.
1. Seleccione el formulario para el que desea agregar una fuente de datos y haga clic en **[!UICONTROL Propiedades]**.
   ![Abrir propiedades de formulario](/help/edge/docs/forms/universal-editor/assets/non-schema-based-edit-properties.png)

   Se abren las propiedades del formulario.
1. Haga clic para abrir la ficha **Modelo de formulario** y en el menú desplegable **Seleccionar de**. Puede seleccionar una de las siguientes opciones:

   * **Modelo de datos de formulario (FDM)**: cree el formulario con un modelo de datos de formulario.
   * **Conector**: cree el formulario con el origen de datos de Adobe Marketo.
   * **Esquema**: cree el formulario con un esquema JSON cargado en AEM Forms.
   * **Ninguno**: cree el formulario desde cero sin usar ningún modelo de formulario.

     Por ejemplo, seleccione el Modelo de datos de formulario (FDM)

     ![Seleccionar ficha de modelo de formulario](/help/edge/docs/forms/universal-editor/assets/select-form-model.png)

1. Seleccione el modelo de datos de formulario (FDM) creado en la lista desplegable. Por ejemplo, seleccione el modelo de datos de formulario creado denominado Modelo de datos de formulario para mascotas de la lista desplegable.

   ![Seleccionar FDM](/help/edge/docs/forms/universal-editor/assets/select-fdm.png)

   Al seleccionar el Modelo de datos de formulario (FDM), aparecerá el cuadro de diálogo de advertencia. Haga clic en **Aceptar** para cerrar el cuadro de diálogo.

   ![Asistente para modelo de formulario](/help/edge/docs/forms/universal-editor/assets/form-model-wizard.png)

1. Haga clic en **[!UICONTROL Guardar y cerrar]**.
1. Abra el formulario para editarlo. El formulario se abrirá en el Editor universal para la creación.

   ![Creación de formularios no basada en esquemas](/help/edge/docs/forms/universal-editor/assets/non-schema-form-authoring.png)

   Los elementos de formulario presentes en el modelo de datos de formulario (FDM) asociado se muestran en la pestaña **[!UICONTROL Fuente de datos]** del **[!UICONTROL Explorador de contenido]** en el **Panel de propiedades**.

   ![Source de datos de formulario](/help/edge/docs/forms/universal-editor/assets/non-schema-data-source.png)

1. Seleccione los elementos de datos de la ficha **[!UICONTROL Origen de datos]** y haga clic en **[!UICONTROL Agregar]**.

   ![Agregar elementos de datos](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-element.png)

   También puede arrastrar y soltar estos elementos para crear su formulario adaptable. Al hacer clic en **[!UICONTROL Agregar]**, los elementos seleccionados de la ficha **[!UICONTROL Fuente de datos]** se agregan al formulario y aparece una marca de verificación delante de los elementos agregados.

   ![Generar formulario](/help/edge/docs/forms/universal-editor/assets/non-schema-form.png)

   También puede agregar manualmente enlaces de datos a un elemento de formulario especificándolo en las propiedades **Bind Reference** del elemento de formulario.
Por ejemplo, vamos a agregar una referencia de enlace de datos al cuadro de texto **Nombre del animal doméstico** que ya está presente en el formulario:

   ![Agregar manualmente datos que enlazan para un campo de formulario](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-binding.png)

   Ahora puede agregar y [configurar la acción de envío](/help/edge/docs/forms/universal-editor/submit-action.md) para su formulario.

## Consulte también

{{universal-editor-see-also}}
