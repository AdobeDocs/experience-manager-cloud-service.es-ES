---
title: ¿Cómo enviar un formulario adaptable para revisión?  ¿Cómo administrar las revisiones de un formulario adaptable de AEM?
description: Revisar es un mecanismo que permite al revisor realizar distintas tareas para formularios adaptables mediante el paso Asignar tarea.
feature: Adaptive Forms
hide: true
hidefromtoc: true
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 100%

---


# Creación y administración de revisiones para un formulario adaptable {#review-step-forms-aem-sites-page}

Al usar el [paso Asignar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?lang=es#assign-task-step) del flujo de trabajo de AEM, el revisor revisa el formulario enviado y realiza una acción sobre él. Para revisar el formulario enviado mediante el paso Asignar tarea, siga estos pasos:

1. [Crear un flujo de trabajo de AEM](#create-an-aem-workflow)
1. [Configurar la acción de envío del contenedor del formulario adaptable](#configure-submit-action)
1. [Enviar un formulario adaptable después de la revisión](#submit-af-after-review)

## Crear un flujo de trabajo de AEM {#create-an-aem-workflow}

1. Abra la instancia de autor en modo de edición.
1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** >  **[!UICONTROL Modelos]** > **[!UICONTROL Crear]** > **[!UICONTROL Crear modelo]**
1. Especifique el Título del flujo de trabajo y añada el paso **[Asignar tarea]**
1. Seleccione ![settings_icon](assets/settings_icon.png) en la barra de acciones. Se abre el cuadro de diálogo **[!UICONTROL Asignar tarea]**.
1. Abra la pestaña [!UICONTROL Formulario y documento] y abra la lista desplegable [!UICONTROL Rellenado previamente] y especifique:

   * Seleccionar archivo de datos de entrada mediante
   * Seleccionar archivos adjuntos de entrada usando

   ![Revisar paso](/help/forms/assets/assigntask-review1.gif)

1. Abra la pestaña **[!UICONTROL Usuario asignado]** y abra la lista desplegable [!UICONTROL Rellenado previamente] y especifique **[!UICONTROL Asignar opciones]**:

   ![Revisar paso](/help/forms/assets/review-assignstep.png)

1. Haga clic en **[!UICONTROL Listo]** para guardar los cambios.

## Configurar la acción de envío {#configure-submit-action}

Ahora, configure la acción Enviar de un componente Contenedor de formulario adaptable en la página del sitio :

1. Vaya a la página del sitio.
1. Seleccione ![settings_icon](assets/settings_icon.png) de un contenedor de formulario adaptable. Se abre el cuadro de diálogo **[!UICONTROL Contenedor de formulario adaptable]**.
1. Abra la pestaña **[!UICONTROL Envío]** y especifique **[!UICONTROL Enviar acción]** para [Invocar un flujo de trabajo de AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?lang=es#invoke-an-aem-workflow)

1. Haga clic en [Listo] para guardar los cambios.

![submissiontab-reviewstep](/help/forms/assets/submissiontab-reviewstep.gif)

## Enviar un formulario adaptable después de la revisión {#submit-af-after-review}

Para revisar y confirmar el formulario adaptable presentado:

1. Vaya a [!UICONTROL Herramientas] > [!UICONTROL Flujo de trabajo] > [!UICONTROL Instancias]
1. En la Bandeja de entrada, puede ver que se está creando una instancia.
1. Seleccione la instancia y haga clic en [!UICONTROL Abrir].
1. Ahora puede ver el formulario enviado.

El revisor realiza diferentes acciones como:

* **Enviar**: El revisor completa el formulario y lo envía para su procesamiento posterior.
* **Guardar**: El revisor guarda el formulario en su estado actual sin enviarlo.
* **Restablecer**: El revisor borra los cambios realizados en el formulario y lo restaura a su estado original.
* **Delegar**: El revisor transfiere la propiedad del formulario a otra persona para que adopte medidas o las revise.
