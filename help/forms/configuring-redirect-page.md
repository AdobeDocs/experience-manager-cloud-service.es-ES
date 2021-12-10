---
title: ¿Cómo configurar una página de redireccionamiento?
description: Descubra cómo se puede redirigir a los usuarios a una página web que los autores de formularios puedan configurar al crear el formulario.
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: e4dc01d2-7c89-4bd8-af0a-1d2df4676a9a
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# Configuración de la página de redireccionamiento {#configuring-redirect-page}

Los autores de formularios pueden configurar una página para cada formulario, a la que se redirige a los usuarios después de enviar el formulario.

1. En el modo de edición, seleccione un componente y haga clic en ![nivel de campo](assets/select_parent_icon.svg) > **[!UICONTROL Contenedor de formulario adaptable]** y, a continuación, haga clic en ![cmppr](assets/configure-icon.svg).

1. En la barra lateral, haga clic en **[!UICONTROL Envío]**.

1. Proporcione la dirección URL de la página de redirección en **[!UICONTROL Dirección URL/ruta de redireccionamiento]** en el **[!UICONTROL Envío]** para obtener más información.
1. De forma opcional, en Enviar acción, para la acción de extremo Enviar a REST, puede configurar el parámetro que se pasará a la página de redirección.

   ![Redirigir la configuración de la página](assets/redirect-url.png)

   Redirigir la configuración de la página

Los autores de formularios pueden utilizar los siguientes parámetros que se pasan a la página de agradecimiento. Para todas las acciones de envío disponibles, `status` y `owner` se pasan. Además de estos dos parámetros, se pasan algunos parámetros adicionales para las siguientes acciones de envío:

* **[!UICONTROL Enviar al extremo REST]**: Se pasan los parámetros añadidos para la asignación de parámetros en el campo a . `status` y `owner` no se pasan en esta acción de envío. Para obtener más información, consulte [Configuración de la acción de envío de extremo de Enviar a REST](configuring-submit-actions.md).
