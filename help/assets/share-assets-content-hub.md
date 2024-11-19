---
title: Compartir Assets en  [!DNL the Content Hub]
description: Compartir Assets en  [!DNL the Content Hub]
role: User
exl-id: 5284d229-1596-40bf-aa5f-af4b6500ebdf
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 6%

---

# Uso compartido de recursos en Content Hub {#search-assets-as-a-link}

| [Prácticas recomendadas de búsqueda](/help/assets/search-best-practices.md) | [Prácticas recomendadas de metadatos](/help/assets/metadata-best-practices.md) | [Centro de contenido](/help/assets/product-overview.md) | [Dynamic Media con funciones de OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentación de desarrollador de AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![Compartir recursos con la imagen del titular](assets/share-assets-banner.png)

>[!AVAILABILITY]
>
>La guía de Content Hub ya está disponible en formato de PDF. Descargue toda la guía y utilice Adobe Acrobat AI Assistant para responder a sus consultas.
>
>[!BADGE PDF de guía de Content Hub]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Compartir recursos a través de un vínculo es una manera cómoda de poner los recursos a disposición de [!DNL the Content Hub] usuarios. La funcionalidad permite a los usuarios autorizados acceder y descargar los recursos compartidos con ellos. Al descargar recursos desde un vínculo compartido, [!DNL the Content Hub] utiliza un servicio asincrónico que ofrece una descarga más rápida e ininterrumpida.

## Requisitos previos {#prerequisites}

[Usuarios de Content Hub](deploy-content-hub.md#onboard-content-hub-users) pueden realizar las acciones mencionadas en este artículo.

## Compartir un solo recurso {#share-a-single-asset}

Puede compartir un solo recurso ejecutando los siguientes pasos:

1. Seleccione un recurso y haga clic en el icono ![compartir icono](assets/share.svg) para compartir un recurso.

   ![Compartiendo un solo recurso](assets/sharing-single-asset.png)

1. Utilice el campo **[!UICONTROL Caducidad]** para especificar una fecha de vencimiento para el vínculo. Seleccione una de las opciones disponibles, como, 24 horas, 1 semana, 30 días, 90 días, 1 año o especifique una fecha personalizada.

1. Haga clic en **[!UICONTROL Copiar vínculo compartido]**. A continuación, puede compartir el vínculo copiado con el destinatario.

## Compartir varios recursos {#share-multiple-assets}

[!DNL The Content Hub] le permite compartir varios recursos mediante un vínculo compartido. Ejecute los siguientes pasos:

1. Seleccione los recursos que debe compartir con el destinatario autorizado. Puede seleccionar varios recursos uno por uno o hacer clic en **[!UICONTROL Seleccionar todo]** para seleccionar todos los recursos disponibles a la vez. La opción **[!UICONTROL Seleccionar todo]** solo se muestra al seleccionar al menos un recurso.

1. Haga clic en el icono ![compartir icono](assets/share.svg).

   ![Compartir varios recursos](assets/sharing-multiple-assets.png)

1. En la sección Vista previa, también puede eliminar recursos según sus necesidades. Utilice el campo **[!UICONTROL Caducidad]** para especificar una fecha de vencimiento para el vínculo. Seleccione una de las opciones disponibles, como, 24 horas, 1 semana, 30 días, 90 días, 1 año o especifique una fecha personalizada.

1. Haga clic en **[!UICONTROL Copiar vínculo compartido]**. A continuación, puede compartir el vínculo copiado con el destinatario.

## Previsualización y uso compartido de recursos {#preview-assets}

Puede obtener una vista previa del aspecto de un recurso digital que va a compartir antes de compartirlo con un destinatario del vínculo. Haga clic en el recurso que necesita previsualizar. [!DNL Content Hub] muestra la [vista detallada del recurso](asset-properties-content-hub.md).

Haga clic en el icono ![compartir icono](assets/share.svg) para compartir un recurso. Utilice el campo **[!UICONTROL Caducidad]** para especificar una fecha de vencimiento para el vínculo. Seleccione una de las opciones disponibles, como, 24 horas, 1 semana, 30 días, 90 días, 1 año o especifique una fecha personalizada. Haga clic en **[!UICONTROL Copiar vínculo compartido]**. A continuación, puede compartir el vínculo copiado con el destinatario.

![Vista previa de recursos en Content Hub](assets/preview-assets-content-hub.png)

## Acceso a los recursos compartidos {#access-shared-assets}

Después de compartir el vínculo de los recursos, los destinatarios autorizados pueden hacer clic en él para obtener una vista previa de los recursos compartidos o descargarlos en un explorador web.

Haga clic en el vínculo compartido y en el icono de descarga disponible en la tarjeta de recursos para descargar un recurso.  También puede seleccionar varios recursos y hacer clic en **[!UICONTROL Descargar]**. <!--You can either download original assets or Original+Renditions of an asset.--> [!DNL The Content Hub] descarga cada recurso uno por uno en el sistema de archivos local.

![Vínculos compartidos de acceso](assets/content-hub-access-shared-links.png)
