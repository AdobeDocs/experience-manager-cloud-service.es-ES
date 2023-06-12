---
title: Cómo configurar una página de redireccionamiento o un mensaje de agradecimiento
description: Descubra cómo se puede mostrar a los usuarios un mensaje de agradecimiento o cómo se les puede redirigir a una página web que los autores de formularios pueden configurar al crear el formulario.
feature: Adaptive Forms
role: User
level: Intermediate
source-git-commit: b104c7ddd102b3600384bf7472b166131e334c35
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 12%

---


# Configurar la página de redireccionamiento {#configuring-redirect-page}

Al presentar una solicitud [Formulario adaptable basado en componentes principales](creating-adaptive-form-core-components.md), puede redirigir al usuario a otra página web o mostrar un mensaje. Para configurar la página de redireccionamiento o el mensaje de agradecimiento:

1. Abra el formulario adaptable para editarlo.
1. Abra el árbol de contenido y seleccione **[!UICONTROL Contenedor de guía]**.
1. Haga clic en las propiedades del contenedor del formulario adaptable ![Propiedades del contenedor del formulario adaptable](/help/forms/assets/configure-icon.svg) icono. Se abre el cuadro de diálogo Contenedor de formulario adaptable para configurar modelos de datos.
1. Abra el **[!UICONTROL Envío]** pestaña. Se muestran las opciones para configurar una página de redireccionamiento o un mensaje:

   ![Cuadro de diálogo de envío del contenedor de guía para configurar una página de redirección o un mensaje](/help/forms/assets/adaptive-forms-core-components-redirect-page-or-thank-you-message.png)

   * Para configurar una URL de redireccionamiento, por ejemplo, en la opción Enviar, seleccione **[!UICONTROL Opción Redirigir a URL]** y proporcione una dirección absoluta, una URL de redireccionamiento o una ruta relativa de una página de AEM Sites.

   * Para configurar un mensaje personalizado o de agradecimiento, seleccione la **[!UICONTROL Mostrar mensaje]** y proporcione un mensaje en el cuadro Contenido del mensaje. Es un cuadro de texto enriquecido, puede utilizar la opción de pantalla completa para ver todos los elementos de texto enriquecido disponibles.

Los autores de formularios pueden configurar una página para cada formulario, a la cual se redirigirá a los usuarios una vez enviado.

**Relacionado**

* [Configuración de la página de redireccionamiento (Foundation Forms)](configuring-redirect-page.md)
