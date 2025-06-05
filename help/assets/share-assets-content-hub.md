---
title: Compartir Assets en  [!DNL the Content Hub]
description: Compartir Assets en  [!DNL the Content Hub]
role: User
exl-id: 5284d229-1596-40bf-aa5f-af4b6500ebdf
source-git-commit: 0e66b355d09e2fd2c4c8a5ddacc9b2d033b41bf2
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 17%

---

# Uso compartido de recursos en Content Hub {#search-assets-as-a-link}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime y Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integración de AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>New</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Extensibilidad de la IU</b></a>
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

Cree un vínculo a los recursos seleccionados para compartirlos con otros fácilmente. Como usuario autorizado de [!DNL Content Hub], seleccione uno o más recursos disponibles en su entorno de [!DNL Content Hub], genere un vínculo y envíelo a otros usuarios privados o públicos.

## Requisitos previos {#prerequisites}

[Usuarios de Content Hub](deploy-content-hub.md#onboard-content-hub-users) pueden crear un vínculo a los recursos seleccionados y compartirlo con otros usuarios.

## Compartir recursos {#share-assets}

Para compartir uno o más recursos con usuarios privados o públicos, ejecute los siguientes pasos:
1. Vaya a la página principal de [!DNL Content Hub], seleccione uno o varios recursos y haga clic en ![Compartir](/help/assets/assets/share.svg) **[!UICONTROL Compartir]** para mostrar un solo recurso seleccionado o una lista de varios recursos seleccionados en el cuadro de diálogo **[!UICONTROL Compartir recursos]**.
También puede seleccionar y compartir recursos disponibles en ![colecciones](/help/assets/assets/Smock_Collection_18_N.svg) **[!UICONTROL colecciones]**.
1. Vea un recurso o revise la lista de recursos disponibles en el cuadro de diálogo **[!UICONTROL Compartir recursos]**. Haga clic en ![anular la selección](/help/assets/assets/Close.svg) junto a un recurso para anular su selección en la lista.
1. Seleccione un **[!UICONTROL período de caducidad]** y haga clic en **[!UICONTROL Generar vínculo privado]** para generar un vínculo que compartir con usuarios privados. Los usuarios privados inician sesión en el entorno [!DNL Content Hub] para tener acceso a la página de recursos compartidos.
   ![vínculo privado y público](/help/assets/assets/private-and-public-link.png)
Habilite la opción **[!UICONTROL Vínculo público]**, seleccione un **[!UICONTROL período de caducidad]** y haga clic en **[!UICONTROL Generar vínculo público]** para generar un vínculo que compartir con usuarios públicos. Los usuarios públicos, como invitados, acceden a la página de recursos compartidos sin iniciar sesión en [!DNL Content Hub].
   ![vínculo privado y público](/help/assets/assets/public-and-private-link.png)

   >[!NOTE]
   > 
   > [Habilite el uso compartido de vínculos públicos desde la página de configuración](/help/assets/configure-content-hub-ui-options.md#enable-public-link-sharing) para mostrar la opción **[!UICONTROL Vínculo público]** en el cuadro de diálogo **[!UICONTROL Compartir recursos]**.

## Compartir un recurso desde su página de vista previa {#share-asset-from-preview-page}

Ejecute los siguientes pasos para compartir un recurso mientras lo previsualiza:

1. Vaya a la página principal de [!DNL Content Hub] y haga clic en la miniatura del recurso para obtener una vista previa del recurso y mostrar las opciones de menú en el panel derecho del cuadro de diálogo.
1. Seleccione ![share](/help/assets/assets/share.svg) para mostrar el panel **[!UICONTROL Share]**.
   ![compartir recurso al previsualizarlo](/help/assets/assets/share-assets-from-share-panel.png)
1. Siga el paso 3 de la sección [compartir recursos](#share-assets) para generar y compartir el vínculo de recursos (privados o públicos) desde este panel **[!UICONTROL Compartir]**.

## Acceso a los recursos compartidos {#access-shared-assets}

Acceda a la página de recursos compartidos a través del vínculo y haga lo siguiente:

* Seleccione uno o más recursos y haga clic en ![descargar](/help/assets/assets/download-icon.svg) **[!UICONTROL Descargar]** para seleccionar las representaciones **[!UICONTROL Original]**, **[!UICONTROL Estática]** o ambas entre las opciones de descarga disponibles.
  ![](/help/assets/assets/download-shared-assets.png)
* Haga clic en la miniatura del recurso para ver sus metadatos.
* En la página de recursos compartidos ([a los que se accede mediante un vínculo privado](#share-assets)), haga clic en una miniatura de recurso y seleccione ![descargar](/help/assets/assets/download-icon.svg) para seleccionar y ver las representaciones dinámicas disponibles del recurso en el panel **[!UICONTROL Descargar]** antes de seleccionarlas y descargarlas.
  ![](/help/assets/assets/download-renditions-shared-assets-page.png)





