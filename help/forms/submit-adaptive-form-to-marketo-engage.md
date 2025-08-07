---
Title: How to configure submit action to Marketo Engage for forms?
Description: Learn how to configure the submit action of Adaptive Form to send data to Marketo Engage.
Keywords: Submit data to Marketo engage, Configure submit action as Submit to Marketo Engage
Feature: Adaptive Forms, Form Data Model
Role: User, Developer
exl-id: 0683564b-1ac4-42b4-bc08-101c4fdef286
source-git-commit: dabf8029577c5fb6bb5eebdbf10d77f3d4d95a5d
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 15%

---

# Configuración de la acción de envío a Marketo Engage para formularios existentes

<span class="preview"> La funcionalidad está disponible en el programa de primeros usuarios. Puede escribir a aem-forms-ea@adobe.com desde su ID de correo electrónico oficial para unirse al programa de primeros usuarios y solicitar acceso a esta funcionalidad. </span>

![Flujo de trabajo](/help/forms/assets/workflow-marketo-3.png)

El editor de Forms adaptable proporciona la acción de envío **Enviar a Marketo Engage** para enviar datos de Forms adaptables a Adobe Marketo Engage para su procesamiento. Puede configurar un formulario adaptable existente para enviar datos a [Adobe Marketo Engage](https://experienceleague.adobe.com/es/docs/marketo/using/home) en el envío.

Hay disponibles varias acciones de envío listas para usar para administrar los envíos de formularios. Puede obtener más información sobre estas opciones en el artículo [Acción de envío del formulario adaptable](/help/forms/configure-submit-actions-core-components.md).

## Consideración al configurar la acción de envío en Marketo Engage para el formulario

* Asegúrese de que el formulario adaptable está configurado con la fuente de datos de Marketo Engage para enviar datos a Marketo Engage al enviar el formulario. Sin embargo, puede cambiar la acción de envío por alternativas, por ejemplo, **Enviar a OneDrive** o **Enviar a SharePoint**, incluso si el formulario está configurado con el esquema de datos de Marketo Engage.

## Requisito previo para configurar la acción de envío en Marketo Engage para el formulario existente

Requisito previo para configurar la acción de envío en Marketo Engage:

* Configure la fuente de datos [Marketo Engage para el formulario adaptable](/help/forms/use-marketo-engage-data-source-in-form.md) y enlace los elementos del formulario con los campos de Marketo Engage.

## Configurar la acción de envío en Marketo Engage para los formularios existentes

>[!VIDEO](https://video.tv.adobe.com/v/3442866/submit-action-marketo-engage-marketo-aem-aem-forms-engage)

<span> Este vídeo solo es aplicable a los componentes principales. Para componentes UE/Foundation, consulte el artículo.</span>


>[!BEGINTABS]

>[!TAB Componente Base]

Puede configurar la acción de envío de un formulario adaptable basado en componentes de base para enviar datos a Adobe Marketo Engage. Para configurar la acción de envío en Marketo Engage, realice los siguientes pasos:

1. Inicie sesión en la instancia de autor de [!DNL Experience Manager Forms].
1. Abra el formulario adaptable para editarlo y vaya a la sección **[!UICONTROL Envío]** de las propiedades del contenedor del formulario adaptable y seleccione una acción de envío como **Enviar a Marketo Engage**.
1. Haga clic en **[!UICONTROL Listo]**.

![Acción de envío de Marketo](/help/forms/assets/marketo-engage-submit-action-af.png){width=50%, height=50%}

Después de configurar la acción de envío para el formulario adaptable como **Enviar a Marketo Engage**, puede enviar datos a Adobe Marketo Engage para su procesamiento. Los datos se pueden utilizar para analizar y optimizar campañas de marketing, automatizar correos electrónicos de seguimiento y flujos de trabajo de déclencheur basados en los envíos de formularios.

>[!TAB Componente principal]

Puede configurar la acción de envío de un formulario adaptable basado en componentes principales para enviar datos a Adobe Marketo Engage. Para configurar la acción de envío en Marketo Engage, realice los siguientes pasos:

1. Abra el formulario adaptable para editarlo.
1. Abra el árbol de contenido y seleccione **[!UICONTROL Contenedor de guía]**.
1. Haga clic en el icono de las ![Propiedades del contenedor del formulario adaptable](/help/forms/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable para configurar la acción de envío.
1. Abra la pestaña **[!UICONTROL Envío]** y seleccione una acción de envío como **Enviar a Marketo Engage**.
1. Haga clic en **[!UICONTROL Listo]**.

![Acción de envío de Marketo](/help/forms/assets/marketo-engage-submit-action.png){width=50%, height=50%}

Después de configurar la acción de envío para el formulario adaptable como **Enviar a Marketo Engage**, puede enviar datos a Adobe Marketo Engage para su procesamiento. Los datos se pueden utilizar para analizar y optimizar campañas de marketing, automatizar correos electrónicos de seguimiento y flujos de trabajo de déclencheur basados en los envíos de formularios.

>[!TAB Editor universal]

Puede configurar la acción de envío de un formulario adaptable creado en el Editor universal para enviar datos a Adobe Marketo Engage. Para configurar la acción de envío en Marketo Engage, realice los siguientes pasos:

1. Abra el formulario adaptable para editarlo.
1. Haga clic en la extensión **Editar propiedades del formulario** en el editor.
Aparecerá el cuadro de diálogo **Propiedades del formulario**.

   >[!NOTE]
   >
   > * Si no ve el icono **Editar propiedades de formulario** en la interfaz de Universal Editor, habilite la extensión **Editar propiedades de formulario** en Extension Manager.
   > * Consulte el artículo [Aspectos destacados de las funciones de Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) para obtener información sobre cómo habilitar o deshabilitar extensiones en el editor universal.

1. Haga clic en la pestaña **Envío** y seleccione la acción de envío **[!UICONTROL Enviar a Marketo Engage]**.

   ![Acción de envío de Marketo](/help/forms/assets/marketo-engage-submit-action-ue.png)

1. Haga clic en **[!UICONTROL Guardar y cerrar]**.

Después de configurar la acción de envío para el formulario adaptable como **Enviar a Marketo Engage**, puede enviar datos a Adobe Marketo Engage para su procesamiento. Los datos se pueden utilizar para analizar y optimizar campañas de marketing, automatizar correos electrónicos de seguimiento y flujos de trabajo de déclencheur basados en los envíos de formularios.

>[!ENDTABS]

## Preguntas más frecuentes (FAQ)

**Q: ¿Puede cambiar la acción de envío de los formularios configurados para conectarse al esquema de Marketo Engage?**
**A:** De forma predeterminada, la acción **Enviar a Marketo** está seleccionada cuando un formulario está configurado para conectarse con el esquema de Marketo Engage. Sin embargo, puede cambiar la acción de envío de los formularios si es necesario.

## Siguiente paso

También puede conectar un formulario adaptable con la [biblioteca de Munchkin](https://experienceleague.adobe.com/es/docs/marketo/using/product-docs/administration/setup/munchkin) para hacer un seguimiento del número de visitas, clics y envíos de formularios.

## Artículos relacionados

{{af-submit-action}}

## Véase también

{{marketo-engage-see-also}}
