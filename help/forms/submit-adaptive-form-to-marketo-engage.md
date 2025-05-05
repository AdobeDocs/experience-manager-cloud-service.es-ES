---
Title: How to configure submit action to Marketo Engage for forms?
Description: Learn how to configure the submit action of Adaptive Form to send data to Marketo Engage.
Keywords: Submit data to Marketo engage, Configure submit action as Submit to Marketo Engage
Feature: Adaptive Forms, Form Data Model
Role: User, Developer
exl-id: 0683564b-1ac4-42b4-bc08-101c4fdef286
source-git-commit: e46c5afac945620cc44e9064956848acecc786bf
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 20%

---

# Configuración de la acción de envío a Marketo Engage para formularios existentes

<span class="preview"> La funcionalidad está disponible en el programa de primeros usuarios. Puede escribir a aem-forms-ea@adobe.com desde su ID de correo electrónico oficial para unirse al programa de primeros usuarios y solicitar acceso a esta funcionalidad. </span>

![Flujo de trabajo](/help/forms/assets/workflow-marketo-3.png)

El editor de Forms adaptable proporciona la acción de envío **Enviar al Marketo Engage** para enviar datos de Forms adaptables a Adobe Marketo Engage para su procesamiento. Puede configurar un formulario adaptable existente para enviar datos a [Adobe Marketo Engage](https://experienceleague.adobe.com/es/docs/marketo/using/home) en el envío.

Hay disponibles varias acciones de envío listas para usar para administrar los envíos de formularios. Puede obtener más información sobre estas opciones en el artículo [Acción de envío del formulario adaptable](/help/forms/configure-submit-actions-core-components.md).

## Consideración al configurar la acción de envío al Marketo Engage para el formulario

* Asegúrese de que el formulario adaptable esté configurado con la fuente de datos del Marketo Engage para enviar datos al Marketo Engage tras el envío del formulario. Sin embargo, puede cambiar la acción de envío a alternativas como, por ejemplo, **Enviar a OneDrive** o **Enviar a SharePoint**, aunque el formulario esté configurado con el esquema de datos de Marketo Engage.

## Requisito previo para configurar la acción de envío en el Marketo Engage para el formulario existente

Requisito previo para configurar la acción de envío para el Marketo Engage:

* Configure el origen de datos del Marketo Engage [para el formulario adaptable](/help/forms/use-marketo-engage-data-source-in-form.md) y enlace los elementos del formulario con los campos del Marketo Engage.

## Configuración de la acción de envío al Marketo Engage para los formularios existentes

>[!VIDEO](https://video.tv.adobe.com/v/3442866/submit-action-marketo-engage-marketo-aem-aem-forms-engage)

Puede configurar la acción de envío de un formulario adaptable para enviar datos a Adobe Marketo Engage. Para configurar la acción de envío en el Marketo Engage, realice los siguientes pasos:

1. Abra el formulario adaptable para editarlo.
2. Abra el árbol de contenido y seleccione **[!UICONTROL Contenedor de guía]**.
3. Haga clic en el icono de las ![Propiedades del contenedor del formulario adaptable](/help/forms/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable para configurar la acción de envío.
4. Abra la pestaña **[!UICONTROL Envío]** y seleccione una acción de envío como **Enviar al Marketo Engage**.
5. Haga clic en **[!UICONTROL Listo]**.

![Acción de envío de Marketo](/help/forms/assets/marketo-engage-submit-action.png){width=50%, height=50%}


Después de configurar la acción de envío para el formulario adaptable como **Enviar al Marketo Engage**, puede enviar datos a Adobe Marketo Engage para su procesamiento. Los datos se pueden utilizar para analizar y optimizar campañas de marketing, automatizar correos electrónicos de seguimiento y flujos de trabajo de déclencheur basados en los envíos de formularios.

## Preguntas más frecuentes (FAQ)

**Q: ¿Puede cambiar la acción de envío de los formularios configurados para conectarse al esquema del Marketo Engage?**
**A:** De forma predeterminada, la acción **Enviar a Marketo** está seleccionada cuando un formulario está configurado para conectarse con el esquema del Marketo Engage. Sin embargo, puede cambiar la acción de envío de los formularios si es necesario.

## Siguiente paso

También puede conectar un formulario adaptable con la [biblioteca de Munchkin](https://experienceleague.adobe.com/es/docs/marketo/using/product-docs/administration/setup/munchkin) para hacer un seguimiento del número de visitas, clics y envíos de formularios.

## Artículos relacionados

{{af-submit-action}}

## Consulte también

{{marketo-engage-see-also}}
