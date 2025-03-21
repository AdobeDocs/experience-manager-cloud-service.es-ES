---
title: Compartir Assets en  [!DNL the Content Hub]
description: Compartir Assets en  [!DNL the Content Hub]
role: User
exl-id: 5284d229-1596-40bf-aa5f-af4b6500ebdf
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 11%

---

# Uso compartido de recursos en Content Hub {#search-assets-as-a-link}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime y Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> integración de <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>extensibilidad de la interfaz de usuario</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar Dynamic Media Prime y Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Prácticas recomendadas de búsqueda</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Prácticas recomendadas de metadatos</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Centro de contenido</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funciones de OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentación de desarrollador de AEM Assets</b></a>
        </td>
    </tr>
</table>

![Compartir recursos con la imagen del titular](assets/share-assets-banner.png)

>[!AVAILABILITY]
>
>La guía del centro de contenido ya está disponible en formato de PDF. Descargue la guía completa y utilice el Asistente de IA de Adobe Acrobat para responder sus consultas.
>
>[!BADGE Guía del centro de contenido en PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

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
