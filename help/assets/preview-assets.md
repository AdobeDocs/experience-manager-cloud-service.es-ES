---
title: Previsualice los recursos antes de utilizarlos en las páginas de AEM Sites
description: Dynamic Media con funciones de OpenAPI le permite previsualizar recursos en páginas de vista previa de sitios de Adobe Experience Manager (AEM). Esta vista previa de recursos permite al usuario y a las partes interesadas revisar y validar las actualizaciones de los recursos antes de publicar las páginas de creación (con recursos actualizados) para uso público.
role: Admin, User
exl-id: 6f071ca9-0f84-45fc-a6b3-047cca9d5e65
source-git-commit: 3f3e091d09b94418fc2cda0bd3b3ce950555b7a9
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 0%

---


# Previsualice los recursos antes de utilizarlos en páginas de AEM Sites {#asset-preview-using-Dynamic-Media-with-OpenAPI-capabilities}

[!DNL Dynamic Media with OpenAPI capabilities] le permite obtener una vista previa de los recursos disponibles en las páginas de creación de [!DNL Adobe Experience Manager (AEM) Sites] antes de ponerlos a disposición del público. La vista previa de recursos está disponible en el nivel de creación y vista previa del sitio.

Para [obtener una vista previa de los recursos en las páginas de vista previa de AEM Sites](#asset-preview-on-sites-pages-using-Dynamic-Media-with-OpenAPI-capabilities), actualice las páginas de creación del sitio agregando los recursos de los que desee obtener una vista previa o reemplazando los existentes disponibles en la página de sitios activa. Publique las páginas de autor actualizadas en el nivel de vista previa para generar una URL de vista previa.

Comparta la página de vista previa con las partes interesadas para recopilar comentarios sobre la calidad visual y la alineación contextual de los recursos actualizados. Refine los recursos en función de los comentarios. Cree y administre varias versiones del recurso durante el ciclo de revisión.

Una vez finalizados los recursos para uso público, actualícelos en las páginas de creación y publique las páginas en el nivel de publicación para acceso público.

## Antes de empezar{#prerequisites-for-previewing-assets-using-Dynamic-Media-with-OpenAPI-capabilities}

Asegúrese de que dispone de:

* Acceso a [!DNL AEM Assets as a Cloud Service].
* Permiso para editar la propiedad Status de los recursos.
* [Se ha agregado el valor [!UICONTROL Vista previa] a la propiedad de metadatos [!UICONTROL  Status] disponible en la pestaña [!UICONTROL Básico]](/help/assets/metadata-assets-view.md#edit-metadata-forms) del formulario de metadatos aplicado a la carpeta que contiene los recursos que se van a previsualizar.
  ![Agregar opción de vista previa](/help/assets/assets/metedata-form-preview.png)
* Clave para generar el token de vista previa. [Póngase en contacto con el soporte técnico de Adobe](https://helpx.adobe.com/in/contact.html) y envíe una solicitud para la clave.

## Vista previa de recursos en la página de vista previa de sitios {#asset-preview-on-sites-pages-using-Dynamic-Media-with-OpenAPI-capabilities}

Puede obtener una vista previa de los nuevos recursos o recursos que ya están aprobados. Los recursos aprobados solo se muestran en las páginas activas de Sites.

Ejecute los siguientes pasos para establecer el estado del recurso para obtener una vista previa en [!DNL Assets View] y, a continuación, publique la página de creación de sitios en el nivel de vista previa para generar una URL de vista previa de la página:

1. Establezca el estado del recurso en **[!UICONTROL Vista previa]** mediante la ejecución de los siguientes pasos:

   1. En [!DNL Assets View], seleccione **[!UICONTROL Assets]** y navegue hasta su carpeta.
   1. Seleccione el recurso que desea previsualizar.
   1. Haga clic en **[!UICONTROL Detalles]**.
   1. En el [!UICONTROL Panel de información], establezca **[!UICONTROL Estado]** en **[!UICONTROL Vista previa]** y, a continuación, haga clic en **[!UICONTROL Guardar]**.
      ![Vista previa](/help/assets/assets/preview-boat-at-bay.png)

1. Vaya a la página de creación de Sites. Ejecute los pasos de [Acceder a recursos remotos en la sección Editor de páginas de AEM](/help/assets/integrate-remote-approved-assets-with-sites.md#access-remote-assets-in-aem-page-editor) para usar el panel Selector de recursos y seleccionar el recurso que ha establecido recientemente como Vista previa (estado).

   >[!NOTE]
   >
   > El Selector de recursos muestra los recursos con la actualización de estado más reciente establecida como Aprobado o Vista previa.

1. Publique la página en el nivel de vista previa con la opción **[!UICONTROL Administrar publicación]**. Ejecute los pasos de la sección [Publicación de contenido para vista previa](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/sites-console/previewing-content) para publicar la página en el nivel de vista previa. Después de la publicación, genere una URL de vista previa de su página. La página Vista previa muestra los recursos (con las actualizaciones de estado más recientes) de la página Sites.

Comparta esta URL de vista previa con las partes interesadas para revisarla y recibir comentarios. Asegúrese de que las partes interesadas tengan acceso a la página de vista previa. Consulte [Acceso al servicio de vista previa](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments#access-preview-service) para obtener información sobre cómo proporcionar acceso a las páginas de vista previa.

>[!NOTE]
>
>El componente principal [Image V3](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/wcm-components/image#version-and-compatibility) admite la versión de vista previa de los recursos de forma predeterminada. Al seleccionar una versión de vista previa de un recurso (recurso con estado de vista previa) mediante el panel [Selector de recursos](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/asset-selector-upload), el componente Image V3 lo procesa automáticamente en el nivel de vista previa (una versión de vista previa en la página de creación de Sites).

Después de finalizar la versión del recurso, [publique sus páginas en el nivel de publicación](#publish-your-pages-to-publish-tier) para el consumo público.

## Publicar sus páginas con recursos aprobados para uso público{#publish-your-pages-to-publish-tier}

Después de finalizar la versión del recurso para uso público, establezca el estado del recurso en **[!UICONTROL Aprobado]**. A continuación, publique las páginas en el nivel de publicación. Siga estos pasos para publicar las páginas:

1. Siga el paso 1 de la sección [Vista previa de recursos en la página de vista previa de sus sitios](#asset-preview-on-sites-pages-using-Dynamic-Media-with-OpenAPI-capabilities) anterior para cambiar el estado del recurso a **[!UICONTROL Aprobado]**.
1. Vaya a la página de creación de Sites y publíquelo en [!DNL Publish tier]. Publique las páginas ejecutando los pasos de [Publicación desde la sección Editor de páginas](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/page-editor/publishing#publishing-from-the-page-editor).
También puede seguir los pasos de [Publicación de páginas desde la sección Consola de sitios](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/sites-console/publishing-pages#publishing-from-the-sites-console) para publicar la página desde la consola del sitio.

   >[!NOTE]
   >
   > Solo los recursos aprobados se pueden entregar en el nivel de publicación. Apruebe los recursos antes de publicar la página en el nivel Publicar para uso público.

   ![La página se ha publicado](/help/assets/assets/the-page-has-been-publushed.png)
Se muestra un mensaje de confirmación **[!UICONTROL La página se ha publicado]** después de la publicación correcta. Navegue hasta la página publicada en el nivel de publicación para confirmar que las actualizaciones estén activas y que el contenido se muestre según lo esperado.
