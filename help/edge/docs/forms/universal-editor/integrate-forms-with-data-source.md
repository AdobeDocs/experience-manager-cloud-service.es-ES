---
title: ¿Cómo se integra el modelo de datos de formulario (FDM) para un formulario en el editor universal?
description: Aprenda a crear formularios basados en un modelo de datos de formulario (FDM). Genere y edite datos de muestra para objetos del modelo de datos en el modelo de datos de formulario (FDM).
feature: Edge Delivery Services, Form Data Model
role: Admin, User
exl-id: 9ce51223-57d0-47d8-8868-84b37d4e8e3e
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 33%

---


# Integrar Forms con el modelo de datos de formulario (FDM)

Conecte los formularios a fuentes de datos back-end mediante FDM para habilitar los flujos de trabajo de enlace, validación y envío de datos.

## Requisitos previos

Complete estos pasos antes de integrar FDM con sus formularios:

1. **[Configurar datos de Source](/help/forms/configure-data-sources.md)**: configurar conexiones back-end
2. **[Crear modelo de datos de formulario](/help/forms/create-form-data-models.md)**: defina la estructura y los servicios de datos
3. **[Configurar objetos del modelo de datos](/help/forms/work-with-form-data-model.md)**: Asignar relaciones de datos

## Consideraciones

Si no ve el icono **Fuentes de datos** en su interfaz del editor universal o la propiedad **Referencia de enlace** en el panel de propiedades de la derecha, habilite la extensión **Fuente de datos** en **Extension Manager**.

![Captura de pantalla de la interfaz de Extension Manager del editor universal que muestra las extensiones disponibles, incluida la extensión de fuentes de datos que se puede habilitar para la integración de formularios](/help/edge/docs/forms/universal-editor/assets/extension-manager.png)

Consulte el artículo [Características destacadas de las funciones de Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) para obtener información sobre cómo habilitar y deshabilitar las extensiones del editor universal.

## Elija su tipo de formulario

El editor universal admite dos métodos de creación de formularios:

| Aspecto | Formulario basado en esquema | Formulario no basado en esquema |
|--------|-------------------|----------------------|
| **Complejidad de la instalación** | Simple (enlace automático) | Manual (enlace campo a campo) |
| **Caso práctico** | Nuevos formularios con estructura de datos definida | Formularios existentes o requisitos flexibles |
| **Fuente de datos** | Necesario durante la creación | Se puede agregar más tarde |
| **Enlace** | Enlace automático de campos | Enlace manual por campo |

![Tipos de formulario del editor universal](/help/edge/docs/forms/universal-editor/assets/form-types.png){width="50%" align="center" height="50%"}

## Formulario basado en esquema

Los formularios basados en esquemas configuran automáticamente fuentes de datos y enlazan campos de formulario a datos. Este método es ideal para formularios nuevos con estructuras de datos bien definidas.

### Crear formulario basado en esquemas

1. **Acceder a la consola de Forms**
   - Inicie sesión en la instancia de autor de [!DNL Experience Manager Forms]
   - Vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms y documentos]**

2. **Iniciar la creación de formularios**
   - Seleccione **[!UICONTROL Crear]** > **[!UICONTROL Forms adaptable]**
   - Elegir una plantilla de Edge Delivery Services
   - Haga clic en **[!UICONTROL Crear]** cuando esté habilitado

   ![Plantilla de Edge Delivery Services](/help/edge/assets/create-eds-forms.png)

3. **Configurar modelo de datos**
   - Vaya a la ficha **Datos**
   - Seleccione **Modelo de datos de formulario (FDM)** para varias fuentes de datos o **Esquema JSON** para un solo sistema backend
   - Elija el FDM creado (por ejemplo, modelo de datos de formulario para mascotas)

   ![Seleccionar modelo de datos de formulario](/help/edge/docs/forms/universal-editor/assets/select-petstore-form-data-model.png)

4. **Completar la configuración del formulario**
   - Escriba **Name** y **Title**
   - Especifique **URL de GitHub** (por ejemplo, `https://github.com/wkndforms/edsforms`)
   - Haga clic en **[!UICONTROL Crear]**

   ![Crear formulario basado en esquema](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form.png)

### Verificar formulario basado en esquemas

El formulario se abrirá en el Editor universal con enlaces de datos preconfigurados:

![Captura de pantalla del editor universal que muestra un formulario basado en un esquema con campos de formulario previamente rellenados y el explorador de contenido que muestra los elementos de fuente de datos disponibles](/help/edge/docs/forms/universal-editor/assets/schema-based-form-in-ue.png)

![Enlace de datos automáticos](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

## Formulario no basado en esquema

Los formularios que no son de esquema requieren una configuración manual de la fuente de datos y un enlace de campo. Este método ofrece flexibilidad para los formularios existentes o para los requisitos complejos.

### Crear formulario no basado en esquemas

1. **Propiedades de formulario de acceso**
   - Inicie sesión en la instancia de autor de [!DNL Experience Manager Forms]
   - Vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms y documentos]**
   - Seleccione el formulario y haga clic en **[!UICONTROL Propiedades]**

   ![Abrir propiedades del formulario](/help/edge/docs/forms/universal-editor/assets/non-schema-based-edit-properties.png)

2. **Configurar modelo de formulario**
   - Abra la ficha **Modelo de formulario**
   - Seleccione **Modelo de datos de formulario (FDM)** de la lista desplegable **Seleccionar de**
   - Elija el FDM de la lista

   ![Seleccionar pestaña Modelo de formulario](/help/edge/docs/forms/universal-editor/assets/select-form-model.png)

   ![Seleccionar FDM](/help/edge/docs/forms/universal-editor/assets/select-fdm.png)

3. **Confirmar configuración**
   - Haga clic en **Aceptar** en el cuadro de diálogo de advertencia
   - Haga clic en **[!UICONTROL Guardar y cerrar]**

   ![Asistente para modelo de formulario](/help/edge/docs/forms/universal-editor/assets/form-model-wizard.png)

### Añadir elementos de datos

1. **Abrir formulario para edición**
   - El formulario se abrirá en el editor universal

   ![Creación de formulario no basado en esquema](/help/edge/docs/forms/universal-editor/assets/non-schema-form-authoring.png)

2. **Elementos de Source de datos de acceso**
   - Vaya a la ficha **[!UICONTROL Fuente de datos]** en el **[!UICONTROL Explorador de contenido]**
   - Ver los elementos de datos disponibles de su FDM

   ![Fuente de datos del formulario](/help/edge/docs/forms/universal-editor/assets/non-schema-data-source.png)

3. **Agregar elementos al formulario**
   - Seleccione elementos de datos y haga clic en **[!UICONTROL Agregar]**
   - O bien, arrastre y suelte los elementos para crear el formulario

   ![Añadir elementos de datos](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-element.png)

   ![Captura de pantalla que muestra el editor universal con un formulario sin esquema que se crea al arrastrar y soltar elementos de datos de la pestaña Fuente de datos en la estructura del formulario](/help/edge/docs/forms/universal-editor/assets/non-schema-form.png)

### Añadir enlace de datos manual

Para los campos de formulario existentes, agregue el enlace de datos a través de la propiedad **Referencia de enlace**:

1. **Abrir propiedades de campo**
   - Seleccione el campo de formulario para el enlace
   - Abra su panel de propiedades

2. **Configurar referencia de enlace**
   - Ir a la propiedad **Bind Reference**
   - Haz clic en el icono **Examinar**

   ![Añadir manualmente el enlace de datos para un campo de formulario](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-binding.png)

3. **Seleccionar elemento de datos**
   - Elija del árbol de fuentes de datos en el asistente **Seleccionar una referencia de enlace**
   - Seleccione el elemento de datos deseado y haga clic en **Seleccionar**

   ![seleccionar referencia de enlace de datos](/help/edge/docs/forms/universal-editor/assets/select-bind-reference.png)

   ![seleccionar elemento de datos](/help/edge/docs/forms/universal-editor/assets/select-data-element.png)

4. **Verificar enlace**
   - El campo de formulario ahora se enlaza al elemento de datos
   - El enlace aparece en la propiedad **Bind Reference**

   ![Enlace de datos automáticos](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

## Verificar integración

Después de completar la integración:

1. **Probar enlace de datos**: compruebe que los campos de formulario muestran datos correctos
2. **Validar envíos**: Asegúrese de guardar los datos en los orígenes configurados
3. **Control de errores de comprobación**: prueba con escenarios de datos no válidos

## Próximos pasos

Configure [acciones de envío](/help/edge/docs/forms/universal-editor/submit-action.md) para completar el flujo de trabajo del formulario.
