---
title: Cómo configurar la página de redireccionamiento
description: Obtenga información sobre cómo se puede redirigir a los usuarios a una página web que los autores de formularios pueden configurar al crear el formulario.
feature: Adaptive Forms, Foundation Components
role: User, Developer
level: Intermediate
exl-id: e4dc01d2-7c89-4bd8-af0a-1d2df4676a9a
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 100%

---

# Configuración de la página de redireccionamiento {#configuring-redirect-page}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-redirect-page.html?lang=es) |
| AEM as a Cloud Service | Este artículo |

Los autores de formularios pueden configurar una página para cada formulario, a la cual se redirigirá a los usuarios una vez enviado.

1. En el modo de edición, seleccione un componente y, a continuación, pulse ![field-level](assets/select_parent_icon.svg) > **[!UICONTROL Contenedor de formulario adaptable]** y haga clic en ![cmppr](assets/configure-icon.svg).

1. En la barra lateral, haga clic en **[!UICONTROL Envío]**.

1. Proporcione la URL de la página de redireccionamiento en **[!UICONTROL URL/ruta de redireccionamiento]** en la sección **[!UICONTROL Envío]**.
1. De forma opcional, en Acción de envío, puede configurar el parámetro que se pasará a la página de redireccionamiento para la acción Enviar a extremo REST.

   ![Configuración de la página de redireccionamiento](assets/redirect-url.png)

   Configuración de la página de redireccionamiento

Los autores de formularios pueden utilizar los siguientes parámetros, los cuales se pasan a la página de agradecimiento. Los parámetros `status` y `owner` se pasan para todas las acciones de envío disponibles. Además de estos dos parámetros, se pasan algunos parámetros adicionales para las siguientes acciones de envío:

* **[!UICONTROL Enviar a extremo REST]**: se pasan los parámetros añadidos para la asignación de campos en uso a parámetros. Los parámetros `status` y `owner` no se pasan en esta acción de envío. Para obtener más información, consulte [Configuración de la acción de envío Enviar a extremo REST](configuring-submit-actions.md).

>[!MORELIKETHIS]
>
>* [Configurar una página de redireccionamiento o un mensaje de agradecimiento](/help/forms/configure-redirect-page-or-thank-you-message.md)
