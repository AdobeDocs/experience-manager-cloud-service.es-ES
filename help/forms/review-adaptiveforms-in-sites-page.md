---
title: Creación y administración de revisiones de Forms adaptable incrustadas o creadas en la página Sitios
seo-title: Review is a mechanism that allows reviewer to perform different tasks for adaptive forms using Assign Task step
description: Revisar es un mecanismo que permite al revisor realizar distintas tareas para formularios adaptables mediante el paso Asignar tarea
feature: Adaptive Forms
hide: true
hidefromtoc: true
source-git-commit: daeb407e27b9f1d390fe40151ca16ec0196712e6
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 5%

---


# Revise el paso de Forms en la página del sitio {#review-step-forms-aem-sites-page}

Al usar la variable [Asignar paso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html#assign-task-step) del flujo de trabajo AEM, el revisor revisa el formulario enviado y realiza una acción sobre él. Para revisar el formulario enviado mediante el paso Asignar tarea , siga estos pasos:

1. [Creación de un flujo de trabajo AEM](#create-an-aem-workflow)
1. [Configurar la acción de envío del contenedor de formularios adaptables](#configure-submit-action)
1. [Enviar un formulario adaptable después de la revisión](#submit-af-after-review)

## Creación de un flujo de trabajo AEM {#create-an-aem-workflow}

1. Abra la instancia de autor en modo de edición.
1. Vaya a **[!UICONTROL Herramientas]** >  **[!UICONTROL Flujo de trabajo]** >  **[!UICONTROL Modelos]** > **[!UICONTROL Crear]** > **[!UICONTROL Crear modelo]**
1. Especifique el título del flujo de trabajo y añada la variable **[Asignar tarea]** step
1. Toque ![settings_icon](assets/settings_icon.png) en la barra de acciones. La variable **[!UICONTROL Asignar tarea]** se abre.
1. Apertura [!UICONTROL Formulario y documento] y abrir [!UICONTROL Rellenado previamente] y especifique:

   * Seleccionar archivo de datos de entrada mediante
   * Seleccionar archivos adjuntos de entrada usando

   ![Revisar paso](/help/forms/assets/assigntask-review1.gif)

1. Apertura **[!UICONTROL Usuario asignado]** y abrir [!UICONTROL Rellenado previamente] y especifique **[!UICONTROL Asignar opciones]**:

   ![Revisar paso](/help/forms/assets/review-assignstep.png)

1. Haga clic en **[!UICONTROL Listo]** para guardar los cambios.

## Configurar la acción de envío {#configure-submit-action}

Ahora, configure la acción Enviar de un componente Contenedor de formulario adaptable en la página del sitio :

1. Vaya a la página del sitio.
1. Toque ![settings_icon](assets/settings_icon.png) de un contenedor de formulario adaptable. La variable **[!UICONTROL Contenedor de formulario adaptable]** se abre.
1. Abra el **[!UICONTROL Envío]** y especifique **[!UICONTROL Enviar acción]** a [Invocar un flujo de trabajo AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?lang=en#invoke-an-aem-workflow)

1. Haga clic en [Listo] para guardar la configuración.

![sumisión, ficha, revisor, paso](/help/forms/assets/submissiontab-reviewstep.gif)

## Enviar un formulario adaptable después de la revisión {#submit-af-after-review}

Para revisar y confirmar el formulario adaptable presentado:

1. Vaya a [!UICONTROL Herramientas] >  [!UICONTROL Flujo de trabajo] >  [!UICONTROL Instancias]
1. En la Bandeja de entrada, puede ver que se está creando una instancia.
1. Seleccione la instancia y haga clic en [!UICONTROL Apertura].
1. Ahora puede ver el formulario enviado.

El revisor realiza diferentes acciones como:

* **Submit**: El revisor completa el formulario y lo envía para su procesamiento posterior.
* **Guardar**: El revisor guarda el formulario en su estado actual sin enviarlo.
* **Restablecer**: El revisor borra los cambios realizados en el formulario y lo restaura a su estado original.
* **Delegar**: El revisor transfiere la propiedad del formulario a otra persona para que la adopte medidas o las revise.
