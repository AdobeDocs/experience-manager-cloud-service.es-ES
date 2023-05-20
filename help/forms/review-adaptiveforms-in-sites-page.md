---
title: Crear y administrar revisiones de Forms adaptable incrustadas o creadas en la página de Sites
seo-title: Review is a mechanism that allows reviewer to perform different tasks for adaptive forms using Assign Task step
description: La revisión es un mecanismo que permite al revisor realizar diferentes tareas en los formularios adaptables mediante el paso Asignar tarea
feature: Adaptive Forms
hide: true
hidefromtoc: true
source-git-commit: daeb407e27b9f1d390fe40151ca16ec0196712e6
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 5%

---


# Paso para revisar Forms en la página del sitio {#review-step-forms-aem-sites-page}

Uso del [Asignar paso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html#assign-task-step) AEM del flujo de trabajo de la, el revisor revisa el formulario enviado y realiza una acción en él. Para revisar el formulario enviado mediante el paso Asignar tarea, siga estos pasos:

1. [AEM Creación de un flujo de trabajo de](#create-an-aem-workflow)
1. [Configurar la acción de envío del contenedor del formulario adaptable](#configure-submit-action)
1. [Enviar un formulario adaptable después de la revisión](#submit-af-after-review)

## AEM Creación de un flujo de trabajo de {#create-an-aem-workflow}

1. Abra la instancia de autor en el modo Edición.
1. Ir a **[!UICONTROL Herramientas]** >  **[!UICONTROL Flujo de trabajo]** >  **[!UICONTROL Modelos]** > **[!UICONTROL Crear]** > **[!UICONTROL Crear modelo]**
1. Especifique el Título del flujo de trabajo y añada **[Asignar tarea]** escalón
1. Tocar ![settings_icon](assets/settings_icon.png) en la barra de acciones. El **[!UICONTROL Asignar tarea]** se abre.
1. Abrir [!UICONTROL Formulario y documento] pestaña y abrir [!UICONTROL Rellenado previamente] y especifique:

   * Seleccionar archivo de datos de entrada mediante
   * Seleccionar archivos adjuntos de entrada usando

   ![Paso Revisar](/help/forms/assets/assigntask-review1.gif)

1. Abrir **[!UICONTROL Asignado]** pestaña y abrir [!UICONTROL Rellenado previamente] y especifique **[!UICONTROL Asignar opciones]**:

   ![Paso Revisar](/help/forms/assets/review-assignstep.png)

1. Haga clic en **[!UICONTROL Listo]** para guardar los cambios.

## Configurar la acción de envío {#configure-submit-action}

Ahora, configure la acción de envío de un componente Contenedor de formulario adaptable en la página de Sites:

1. Vaya a la página del sitio.
1. Tocar ![settings_icon](assets/settings_icon.png) de un contenedor de formulario adaptable. El **[!UICONTROL Contenedor de formulario adaptable]** se abre.
1. Abra el **[!UICONTROL Envío]** y especifique **[!UICONTROL Acción de envío]** hasta [AEM Invocar un flujo de trabajo de](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?lang=en#invoke-an-aem-workflow)

1. Clic [Listo] para guardar la configuración.

![submissiontab-reviewstep](/help/forms/assets/submissiontab-reviewstep.gif)

## Enviar un formulario adaptable después de la revisión {#submit-af-after-review}

Para revisar y confirmar el formulario adaptable enviado:

1. Ir a [!UICONTROL Herramientas] >  [!UICONTROL Flujo de trabajo] >  [!UICONTROL Instancias]
1. En la bandeja de entrada, puede ver que se está creando una instancia.
1. Seleccione la instancia y haga clic en [!UICONTROL Abrir].
1. Ahora puede ver el formulario enviado.

El revisor realiza diferentes acciones como:

* **Enviar**: el revisor completa el formulario y lo envía para un procesamiento posterior.
* **Guardar**: el revisor guarda el formulario en su estado actual sin enviarlo.
* **Restablecer**: el revisor borra los cambios realizados en el formulario y lo restaura a su estado original.
* **Delegar**: el revisor transfiere la propiedad del formulario a otra persona para que realice más acciones o realice revisiones.
