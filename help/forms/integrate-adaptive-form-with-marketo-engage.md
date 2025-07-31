---
Title: How to integrate Marketo Engage with AEM Forms using Form wizard?
Description: Learn how to integrate your Marketo Engage instance with AEM Forms using form wizard.
Keywords: How to connect a Marketo instance with form? , Connect a form to Marketo, Integrate a form with Marketo Engage, Integrate an Adaptive Form with a Marketo instance.
Feature: Adaptive Forms, Form Data Model
Role: User, Developer
exl-id: 1fcba628-ffd8-416a-a8b5-76b35d4aabd4
source-git-commit: ce4646d8db1870f8ec85faddeb4e0a6a04f4c46e
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 23%

---

# Integración de un formulario adaptable con Marketo Engage

<span class="preview"> La funcionalidad está disponible en el programa de primeros usuarios. Puede escribir a aem-forms-ea@adobe.com desde su ID de correo electrónico oficial para unirse al programa de primeros usuarios y solicitar acceso a esta funcionalidad. </span>

![Flujo de trabajo](/help/forms/assets/workflow-marketo-4.png)

Después de crear la configuración del servicio en la nube para integrar Marketo Engage con AEM Forms, puede configurar un formulario adaptable para integrarlo con [Adobe Marketo Engage](https://experienceleague.adobe.com/en/docs/marketo/using/home).

Puede conectar Marketo Engage a un formulario adaptable mediante el asistente de formularios, que simplifica el proceso de configuración y le guía en cada paso. Incluye la selección de plantillas, estilos y campos de datos, así como la configuración de la asignación de datos para garantizar que el formulario esté listo para comunicarse con Marketo Engage una vez creado. Con el asistente de formularios, también puede configurar el formulario adaptable para enviar datos directamente a Adobe Marketo Engage tras el envío.

## Consideración para configurar la fuente de datos de Marketo Engage para formularios

Al configurar la fuente de datos de Marketo Engage para los formularios, hay que tener en cuenta lo siguiente:

* No es posible conectar Edge Delivery Services Forms con Marketo Engage.

## Requisito previo para conectar Marketo Engage con formularios

Requisito previo para conectar Marketo Engage con formularios:

* Cree [la configuración del servicio en la nube para integrar Marketo Engage con formularios](/help/forms/integrate-form-to-marketo-engage.md).

## Configuración del nuevo formulario adaptable para integrarlo con Marketo Engage

>[!VIDEO](https://video.tv.adobe.com/v/3442867/marketo-aem-marketo-engage-engage-aem-forms)

>[!BEGINTABS]

>[!TAB Componente Base]

Para configurar un nuevo formulario adaptable basado en componentes de base para integrarlo con Marketo Engage, realice los siguientes pasos:

1. Seleccione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.

   ![Seleccionar Forms y documentos](/help/forms/assets/select-forms.png)

1. Seleccione **[!UICONTROL Crear]** > **[!UICONTROL Formularios adaptables]**. Se abre el asistente para la creación de formularios.

   ![Seleccionar AF](/help/forms/assets/select-create-forms.png)

1. En la ficha **[!UICONTROL Source]**, seleccione una plantilla

   ![Seleccionar plantillas](/help/forms/assets/select-template-af1.png)

1. En **[!UICONTROL Estilo]**, seleccione el tema.

   ![Seleccionar tema](/help/forms/assets/select-form-theme-af1.png)
1. En la ficha **[!UICONTROL Datos]**, seleccione un modelo de datos como **Marketo Engage**.
1. Seleccione **[!UICONTROL Configuración de nube]** de la lista desplegable que aparece en el panel derecho de la pantalla.
De forma predeterminada, aparecen todos los campos de la configuración asociada. El asistente ofrece la comodidad de permitirle elegir selectivamente qué campos se deben incluir en el formulario adaptable mediante el uso de casillas de verificación.

   ![Seleccionar modelo de datos](/help/forms/assets/select-marketo-data-af1.png)

1. En la ficha **[!UICONTROL Envío]**, seleccione la acción de envío como **[!UICONTROL Enviar a Marketo]**.

   Cuando selecciona el modelo de datos como **Marketo Engage**, la acción de envío como **Enviar a Marketo** se selecciona automáticamente. Puede seleccionar una acción de envío diferente en la ficha **[!UICONTROL Envío]**. La pestaña **[!UICONTROL Envío]** muestra todas las acciones de envío disponibles.

   ![Enviar a Marketo Engage](/help/forms/assets/select-marketo-engage.png)

1. Seleccione **[!UICONTROL Crear]**. Especifique el título, el nombre y la ubicación para guardar el formulario adaptable.

   ![Crear formulario](/help/forms/assets/create-marketo-form.png)

1. Seleccione **[!UICONTROL Crear]**.

El formulario adaptable ahora está configurado para conectarse con la instancia de Marketo Engage. También puede editar las propiedades del formulario adaptable para cambiar su configuración asociada

>[!TAB Componente principal]

Para configurar un nuevo formulario adaptable basado en componentes principales para integrarlo con Marketo Engage, realice los siguientes pasos:

1. Seleccione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.

   ![Seleccionar Forms y documentos](/help/forms/assets/select-forms.png)

1. Seleccione **[!UICONTROL Crear]** > **[!UICONTROL Formularios adaptables]**. Se abre el asistente para la creación de formularios.

   ![Seleccionar AF](/help/forms/assets/select-create-forms.png)

1. En la ficha **[!UICONTROL Source]**, seleccione una plantilla

   ![Seleccionar plantillas](/help/forms/assets/select-template.png)

1. En **[!UICONTROL Estilo]**, seleccione el tema.

   ![Seleccionar tema](/help/forms/assets/select-form-theme.png)


1. En la ficha **[!UICONTROL Datos]**, seleccione un modelo de datos como **Marketo Engage**.

1. Seleccione **[!UICONTROL Configuración de nube]** de la lista desplegable que aparece en el panel derecho de la pantalla.
De forma predeterminada, aparecen todos los campos de la configuración asociada. El asistente ofrece la comodidad de permitirle elegir selectivamente qué campos se deben incluir en el formulario adaptable mediante el uso de casillas de verificación.

   ![Seleccionar modelo de datos](/help/forms/assets/select-marketo-data.png)

1. En la ficha **[!UICONTROL Envío]**, seleccione la acción de envío como **[!UICONTROL Enviar a Marketo]**.

   Cuando selecciona el modelo de datos como **Marketo Engage**, la acción de envío como **Enviar a Marketo** se selecciona automáticamente. Puede seleccionar una acción de envío diferente en la ficha **[!UICONTROL Envío]**. La pestaña **[!UICONTROL Envío]** muestra todas las acciones de envío disponibles.

   ![Enviar a Marketo Engage](/help/forms/assets/select-marketo-engage.png)

1. Seleccione **[!UICONTROL Crear]**. Especifique el título, el nombre y la ubicación para guardar el formulario adaptable.

   ![Crear formulario](/help/forms/assets/create-marketo-form.png)

1. Seleccione **[!UICONTROL Crear]**.

El formulario adaptable ahora está configurado para conectarse con la instancia de Marketo Engage. También puede editar las propiedades del formulario adaptable para cambiar su configuración asociada.

>[!TAB Editor universal]

Para configurar el nuevo formulario adaptable creado en el Editor universal para integrarlo con Marketo Engage, realice los siguientes pasos:

1. Seleccione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.

   ![Seleccionar Forms y documentos](/help/forms/assets/select-forms.png)

1. Seleccione **[!UICONTROL Crear]** > **[!UICONTROL Formularios adaptables]**. Se abre el asistente para la creación de formularios.

   ![Seleccionar AF](/help/forms/assets/select-create-forms.png)

1. En la ficha **[!UICONTROL Source]**, seleccione una plantilla

   ![Seleccionar plantillas](/help/forms/assets/select-template-ue.png)

1. En la ficha **[!UICONTROL Datos]**, seleccione un modelo de datos como **Marketo Engage**.

1. Seleccione **[!UICONTROL Configuración de nube]** de la lista desplegable que aparece en el panel derecho de la pantalla.
De forma predeterminada, aparecen todos los campos de la configuración asociada. El asistente ofrece la comodidad de permitirle elegir selectivamente qué campos se deben incluir en el formulario adaptable mediante el uso de casillas de verificación.

   ![Seleccionar modelo de datos](/help/forms/assets/select-marketo-data-ue.png)

1. En la ficha **[!UICONTROL Envío]**, seleccione la acción de envío como **[!UICONTROL Enviar a Marketo]**.

   Cuando selecciona el modelo de datos como **Marketo Engage**, la acción de envío como **Enviar a Marketo** se selecciona automáticamente. Puede seleccionar una acción de envío diferente en la ficha **[!UICONTROL Envío]**. La pestaña **[!UICONTROL Envío]** muestra todas las acciones de envío disponibles.

   ![Enviar a Marketo Engage](/help/forms/assets/select-marketo-engage-ue.png)

1. Seleccione **[!UICONTROL Crear]**. Especifique el título, el nombre y la ubicación para guardar el formulario adaptable.

   ![Crear formulario](/help/forms/assets/create-marketo-form.png)

1. Seleccione **[!UICONTROL Crear]**.

El formulario adaptable ahora está configurado para conectarse con la instancia de Marketo Engage. También puede editar las propiedades del formulario adaptable para cambiar su configuración asociada.

>[!ENDTABS]

## Preguntas más frecuentes (FAQ)

**Q: ¿Puede cambiar la acción de envío de los formularios configurados para conectarse al esquema de Marketo Engage?**
**A:** De forma predeterminada, la acción **Enviar a Marketo** está seleccionada cuando un formulario está configurado para conectarse con el esquema de Marketo Engage. Sin embargo, puede cambiar la acción de envío de los formularios si es necesario.


**P: ¿Qué sucede cuando cambia el conector del formulario?**\
**R:** Si cambia el conector del formulario, los enlaces existentes dejarán de ser válidos.

**P: ¿Cuáles son las tres operaciones disponibles en Invocar servicio del Editor de reglas para los formularios integrados con Marketo Engage?**\
**P:** Las tres operaciones predeterminadas disponibles en **Invocar servicio** para los formularios integrados con Marketo Engage son:

* Sincronizar posible cliente
* Obtener posible cliente por el ID
* Obtener posible cliente por el tipo de filtro

## Siguiente paso

También puede conectar un formulario adaptable con la [biblioteca de Munchkin](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/setup/munchkin) para hacer un seguimiento del número de visitas, clics y envíos de formularios.

## Artículos relacionados

{{af-submit-action}}

## Véase también

{{marketo-engage-see-also}}
