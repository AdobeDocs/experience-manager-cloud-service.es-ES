---
title: Cómo configurar una página de redireccionamiento o un mensaje de agradecimiento
description: Obtenga información sobre cómo se puede redirigir a los usuarios a una página web que los autores de formularios pueden configurar al crear el formulario o cómo se puede mostrar a los usuarios un mensaje de agradecimiento.
feature: Adaptive Forms, Edge Delivery Services
role: User
level: Intermediate
source-git-commit: 1be7bafc1d93a65a81eeb2f7e86cac33cde7aa35
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 50%

---

# Configurar redireccionamiento o mensaje de agradecimiento

En los formularios creados con el Editor universal, los autores de formularios pueden configurar lo que sucede después de que un usuario envía un formulario. Puede mostrar un mensaje de agradecimiento o redirigir al usuario a una página web específica mediante la pestaña Envío en la extensión Editar propiedades del formulario.

Puede configurar el mensaje de agradecimiento o redirigir las direcciones URL de los formularios creados en el editor universal mediante la ficha **Envío** de la extensión **Propiedades de formulario de AEM**.

## Requisitos previos

Puede configurar la acción de envío para los formularios creados en el editor universal mediante la pestaña **Envío** de la extensión **Editar propiedades del formulario**.

![Icono de propiedades de formulario](/help/forms/assets/ue-form-properties-icon.png)

![Propiedades de formulario de editor universal](/help/forms/assets/ue-form-properties.png)

>[!NOTE]
>
>* Si no ve el icono **Propiedades del formulario** en su interfaz de Universal Editor, habilite la extensión **Editar propiedades del formulario** en Extension Manager.
>* Consulte el artículo [Aspectos destacados de las funciones de Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) para obtener información sobre cómo habilitar o deshabilitar extensiones en el editor universal.

## ¿Cómo configurar el redireccionamiento o el mensaje de agradecimiento?

Al enviar un formulario, puede redirigir al usuario a otra página web o mostrar un mensaje.

Para configurar la página de redireccionamiento o el mensaje de agradecimiento:

1. Abra el formulario adaptable para editarlo.
1. Abra el árbol de contenido y seleccione **[!UICONTROL Contenedor de guía]**.
1. Haga clic en el icono de las ![Propiedades del contenedor del formulario adaptable](/help/forms/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable para configurar modelos de datos.
1. Abra la pestaña **[!UICONTROL Entrega]**. Se muestran las opciones para configurar una página de redireccionamiento o un mensaje:

   ![Cuadro de diálogo de envío del contenedor de guía para configurar una página de redirección o un mensaje](/help/forms/assets/adaptive-forms-core-components-redirect-page-or-thank-you-message.png)

**Configurar URL de redireccionamiento**

* Para configurar una URL de redireccionamiento, por ejemplo, en la opción Enviar, seleccione la **[!UICONTROL Opción Redirigir a URL]** y proporcione una dirección absoluta, una URL de redireccionamiento o una ruta relativa de una página de AEM Sites.

![redireccionamiento](/help/edge/docs/forms/universal-editor/assets/redirect-ue.png)

**Configurar mensaje de agradecimiento**

* Para configurar un mensaje personalizado o de agradecimiento, seleccione la opción de **[!UICONTROL Mostrar mensaje]** y proporcione un mensaje en el cuadro Contenido del mensaje. Es un cuadro de texto enriquecido, puede utilizar la opción de pantalla completa para ver todos los elementos de texto enriquecido disponibles.

![gracias](/help/edge/docs/forms/universal-editor/assets/thankyou-ue.png)

Los autores de formularios pueden configurar una página para cada formulario, a la cual se redirigirá a los usuarios una vez enviado.
