---
title: ¿Cómo se integra el modelo de datos de formulario para un formulario en el editor universal?
description: Aprenda a crear formularios para Edge Delivery Services basados en un modelo de datos de formulario (form data model, FDM). Genere y edite datos de muestra para objetos del modelo de datos en el FDM.
feature: Edge Delivery Services, Form Data Model
role: Admin, User
exl-id: 9ce51223-57d0-47d8-8868-84b37d4e8e3e
source-git-commit: cfff846e594b39aa38ffbd3ef80cce1a72749245
workflow-type: ht
source-wordcount: '716'
ht-degree: 100%

---


# Integración de los formularios con el modelo de datos de formulario (FDM)

Conecte los formularios a fuentes de datos back-end con el FDM para habilitar los flujos de trabajo de enlace, validación y envío de datos.

## Requisitos previos

Complete estos pasos antes de integrar el FDM con sus formularios:

1. **[Configurar la fuente de datos](/help/forms/configure-data-sources.md)**: configure las conexiones back-end.
2. **[Crear modelo de datos de formulario](/help/forms/create-form-data-models.md)**: definir la estructura y los servicios de datos
3. **[Configurar objetos del modelo de datos](/help/forms/work-with-form-data-model.md)**: asignar relaciones de datos

## Consideraciones

Si no ve el icono **Fuentes de datos** en su interfaz del editor universal o la propiedad **Referencia de enlace** en el panel de propiedades de la derecha, habilite la extensión **Fuente de datos** en **Extension Manager**.

![Captura de pantalla de la interfaz de Extension Manager del editor universal que muestra las extensiones disponibles, incluida la extensión de fuentes de datos que se puede habilitar para la integración de formularios](/help/edge/docs/forms/universal-editor/assets/extension-manager.png)

Consulte el artículo [Características destacadas de las funciones de Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) para obtener información sobre cómo habilitar y deshabilitar las extensiones del editor universal.

## Elección de su tipo de formulario

El editor universal admite dos métodos de creación de formularios:

| Aspecto | Formulario basado en esquema | Formulario no basado en esquema |
|--------|-------------------|----------------------|
| **Complejidad de la instalación** | Simple (enlace automático) | Manual (enlace campo a campo) |
| **Caso práctico** | Nuevos formularios con estructura de datos definida | Formularios existentes o requisitos flexibles |
| **Fuente de datos** | Necesario durante la creación | Se puede añadir más tarde |
| **Enlace** | Enlace automático de campos | Enlace manual por campo |

![Tipos de formulario del editor universal](/help/edge/docs/forms/universal-editor/assets/form-types.png){width="50%" align="center" height="50%"}

## Formulario basado en esquema

Los formularios basados en esquemas configuran automáticamente fuentes de datos y enlazan campos de formulario a datos. Este método es ideal para formularios nuevos con estructuras de datos bien definidas.

### Creación de un formulario basado en esquemas

1. **Acceder a la consola de formularios**
   - Inicie sesión en la instancia de autor de [!DNL Experience Manager Forms]
   - Vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.

2. **Iniciar la creación de formularios**
   - Seleccione **[!UICONTROL Crear]** > **[!UICONTROL Formularios adaptables]**
   - Elegir una plantilla de Edge Delivery Services
   - Haga clic en **[!UICONTROL Crear]** cuando esté habilitado

   ![Plantilla de Edge Delivery Services](/help/edge/assets/create-eds-forms.png)

3. **Configurar modelo de datos**
   - Vaya a la pestaña **Datos**
   - Seleccione **Modelo de datos de formulario (FDM)** para varias fuentes de datos o **Esquema JSON** para un solo sistema back-end
   - Elija el FDM creado (por ejemplo, modelo de datos de formulario para mascotas)

   ![Seleccionar el modelo de datos de formulario](/help/edge/docs/forms/universal-editor/assets/select-petstore-form-data-model.png)

4. **Completar la configuración del formulario**
   - Escriba **Nombre** y **Título**
   - Especifique la información en **URL de GitHub** (por ejemplo, `https://github.com/wkndforms/edsforms`)
   - Haga clic en **[!UICONTROL Crear]**

   ![Crear formulario basado en esquema](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form.png)

### Verificar formulario basado en esquemas

El formulario se abrirá en el Editor universal con enlaces de datos preconfigurados:

![Captura de pantalla del editor universal que muestra un formulario basado en un esquema con campos de formulario previamente rellenados y el explorador de contenido que muestra los elementos de fuente de datos disponibles](/help/edge/docs/forms/universal-editor/assets/schema-based-form-in-ue.png)

![Enlace de datos automáticos](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

## Formulario no basado en esquema

Los formularios que no son de esquema requieren una configuración manual de la fuente de datos y un enlace de campo. Este método ofrece flexibilidad para los formularios existentes o para los requisitos complejos.

### Creación de un formulario no basado en esquema

1. **Acceso a las propiedades del formulario**
   - Inicie sesión en la instancia de autor de [!DNL Experience Manager Forms]. 
   - Vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**
   - Seleccione su formulario y haga clic en **[!UICONTROL Propiedades]**

   ![Abrir propiedades del formulario](/help/edge/docs/forms/universal-editor/assets/non-schema-based-edit-properties.png)

2. **Configurar modelo de formulario**
   - Abrir la ficha **Modelo de formulario**
   - Seleccione **Modelo de datos de formulario (FDM)** en la lista desplegable **Seleccionar de**
   - Elija su FDM en la lista

   ![Seleccionar pestaña Modelo de formulario](/help/edge/docs/forms/universal-editor/assets/select-form-model.png)

   ![Seleccionar FDM](/help/edge/docs/forms/universal-editor/assets/select-fdm.png)

3. **Confirma configuración**
   - Haga clic en **Aceptar** en el cuadro de diálogo de advertencia
   - Haga clic en **[!UICONTROL Guardar y cerrar]**

   ![Asistente para modelo de formulario](/help/edge/docs/forms/universal-editor/assets/form-model-wizard.png)

### Añadir elementos de datos

1. **Abrir el formulario para editarlo**
   - El formulario se abrirá en el editor universal

   ![Creación de formulario no basado en esquema](/help/edge/docs/forms/universal-editor/assets/non-schema-form-authoring.png)

2. **Elementos de fuente de datos de acceso**
   - Vaya a la pestaña **[!UICONTROL Fuente de datos]** en el **[!UICONTROL Explorador de contenido]**
   - Ver los elementos de datos disponibles de su FDM

   ![Fuente de datos del formulario](/help/edge/docs/forms/universal-editor/assets/non-schema-data-source.png)

3. **Añada elementos al formulario**
   - Seleccione elementos de datos y haga clic en **[!UICONTROL Añadir]**
   - O bien, arrastre y suelte los elementos para crear el formulario

   ![Añadir elementos de datos](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-element.png)

   ![Captura de pantalla que muestra el editor universal con un formulario sin esquema que se crea al arrastrar y soltar elementos de datos de la pestaña Fuente de datos en la estructura del formulario](/help/edge/docs/forms/universal-editor/assets/non-schema-form.png)

### Añadir enlace de datos manual

Para los campos de formulario existentes, añadir el enlace de datos a través de la propiedad **Referencia de enlace**:

1. **Propiedades del campo de formulario**
   - Seleccione el campo de formulario para el enlace
   - Abra su panel de propiedades

2. **Configurar la referencia de enlace**
   - Vaya a la propiedad **Referencia de enlace**
   - Haga clic en el icono **Examinar**

   ![Añadir manualmente el enlace de datos para un campo de formulario](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-binding.png)

3. **Seleccionar elemento de datos**
   - Elija en el árbol de fuentes de datos en el asistente **Seleccionar una referencia de enlace**.
   - Seleccione el elemento de datos que desee y haga clic en **Seleccionar**

   ![seleccionar referencia de enlace de datos](/help/edge/docs/forms/universal-editor/assets/select-bind-reference.png)

   ![seleccionar elemento de datos](/help/edge/docs/forms/universal-editor/assets/select-data-element.png)

4. **Verificar enlace**
   - El campo de formulario ahora se enlaza al elemento de datos
   - El enlace aparece en la propiedad **Referencia de enlace**

   ![Enlace de datos automáticos](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

## Verificar integración

Después de completar la integración:

1. **Probar enlace de datos**: compruebe que los campos de formulario muestran datos correctos
2. **Validar envíos**: asegúrese de guardar los datos en los orígenes configurados
3. **Control de errores de comprobación**: pruebe con escenarios de datos no válidos

## Próximos pasos

Configure [acciones de envío](/help/edge/docs/forms/universal-editor/submit-action.md) para completar el flujo de trabajo del formulario.
