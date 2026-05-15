---
title: Aplicar recortes inteligentes de vídeo a vídeos aprobados
description: Dynamic Media con funciones OpenAPI le permiten generar automáticamente salidas de recorte inteligente de vídeo para recursos de vídeo aprobados en Adobe Experience Manager (AEM).
role: Admin, User
badgeSaas: label="AEM Assets" type="Positive" tooltip="(Se aplica a los AEM Assets)."
exl-id: video-smartcrop-dmwoapi
source-git-commit: c2b849ef25afd0809891a822a99ddd3059bf1919
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 2%

---


# Aplicar recortes inteligentes de vídeo a vídeos aprobados {#apply-video-smart-crops-dmwoapi}

[!DNL Dynamic Media with OpenAPI capabilities] le permite generar automáticamente salidas de recorte inteligente de vídeo para los recursos de vídeo en [!DNL Adobe Experience Manager (AEM)]. Los recortes inteligentes de vídeo analizan el contenido de vídeo y ajustan el marco de forma dinámica para mantener al sujeto clave enfocado en diferentes relaciones de aspecto y dispositivos.

Los recortes inteligentes de vídeo se generan automáticamente cuando la función está habilitada y se aprueba el recurso de vídeo

## Antes de empezar {#prerequisites-for-video-smart-crops}

Asegúrese de que dispone de:

* Acceso a [!DNL AEM Assets as a Cloud Service].
* Permite editar esquemas de metadatos.
* Dynamic Media con las funcionalidades de OpenAPI habilitadas para su entorno.
* Recursos de vídeo que se pueden marcar como **[!UICONTROL Aprobado]**.

## Activar recortes inteligentes de vídeo para vídeos {#enable-video-smart-crops}

Para habilitar los recortes inteligentes de vídeo, configure el esquema de metadatos utilizado para los recursos de vídeo:

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de metadatos]**.
2. Abra el esquema de metadatos aplicable (por ejemplo, **default**).
3. Seleccione el formulario **Vídeo** y haga clic en **[!UICONTROL Editar]**.
4. Agregue un nuevo **[!UICONTROL campo desplegable]** y configure lo siguiente:

   * **Etiqueta de campo**: Crear recortes inteligentes de vídeo
   * **Asignar a propiedad**: `./jcr:content/dam:applyVideoSmartCrop`

5. Añada los siguientes valores manualmente:

   * Sí → verdadero
   * No hay → falso

6. Guarde el esquema.

La opción **Crear cultivos inteligentes de vídeo** ya está disponible en el formulario de metadatos de recursos de vídeo.

<!--
broken link
![Create Video Smartcrops field](/help/assets/assets/video-smartcrop-metadata-field.png)
-->

## Aplicar recortes inteligentes de vídeo a vídeos aprobados {#apply-video-smart-crops}

Puede aplicar recortes inteligentes de vídeo a los recursos de vídeo si habilita el campo de metadatos y aprueba el recurso.

Ejecute los siguientes pasos:

1. En [!DNL Assets View], seleccione **[!UICONTROL Assets]** y navegue hasta su carpeta.
2. Seleccione el recurso de vídeo.
3. Haga clic en **[!UICONTROL Detalles]**.
4. En el panel de metadatos, busque **[!UICONTROL Crear cultivos inteligentes de vídeo]**.
5. Establezca el valor en **Yes** y, a continuación, haga clic en **[!UICONTROL Guardar]**.
6. Establezca el estado del recurso en **[!UICONTROL Aprobado]**.

Una vez aprobado el recurso, las salidas de recorte inteligente de vídeo se generan automáticamente.

## Ver salidas de recorte inteligente de vídeo {#view-video-smart-crops}

Una vez generados los recortes inteligentes de vídeo:

* Las salidas están disponibles durante la reproducción de vídeo.
* El visualizador de Dynamic Media selecciona automáticamente el recorte más adecuado en función del dispositivo y la relación de aspecto.
* La reproducción de vídeo se ajusta dinámicamente para mantener el sujeto clave enfocado.

## Usar vídeos recortados inteligentes de vídeo {#use-video-smart-crops}

Puede utilizar salidas de recorte inteligente de vídeo dondequiera que se envíe el recurso de vídeo, como:

* Páginas web
* Aplicaciones
* Reproductores de vídeo integrados

El visor aplica automáticamente el recorte inteligente adecuado durante la reproducción.

>[!NOTE]
>
>* Los recortes inteligentes de vídeo solo se generan para **Recursos de vídeo aprobados**.
>* Asegúrese de que el campo **Crear cultivos inteligentes de vídeo** esté establecido en **Sí** antes de aprobar el recurso.
>* Los recortes inteligentes de vídeo no modifican el recurso original. El recorte se aplica de forma dinámica durante la reproducción.