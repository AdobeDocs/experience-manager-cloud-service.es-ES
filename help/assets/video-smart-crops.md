---
title: Aplicar recortes inteligentes de vídeo a vídeos aprobados
description: Dynamic Media con funciones OpenAPI le permite generar salidas de recorte inteligente de vídeo para recursos de vídeo en Adobe Experience Manager (AEM).
role: Admin, User
badgeSaas: label="AEM Assets" type="Positive" tooltip="Se aplica a los AEM Assets."
source-git-commit: 30037f08d5caeab878b6cf89b936308d16ae3e8d
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 3%

---

# Aplicar recortes inteligentes de vídeo a vídeos aprobados {#apply-video-smart-crops-dmwoapi}

[!DNL Dynamic Media with OpenAPI capabilities] le permite generar salidas de recorte inteligente de vídeo para los recursos de vídeo en [!DNL Adobe Experience Manager (AEM)].

Los recortes inteligentes de vídeo analizan el contenido de vídeo y ajustan el marco de forma dinámica para mantener al sujeto clave enfocado en diferentes relaciones de aspecto y dispositivos.

Para utilizar esta función, configure el esquema de metadatos para los recursos de vídeo. Una vez activado, los usuarios pueden aplicar recortes inteligentes de vídeo actualizando los metadatos del recurso y aprobándolo.

## Antes de empezar {#prerequisites-for-video-smart-crops}

Asegúrese de que dispone de:

* Acceso a [!DNL AEM Assets as a Cloud Service].
* Permite editar esquemas de metadatos.
* Dynamic Media con las funcionalidades de OpenAPI habilitadas para su entorno.
* Recursos de vídeo disponibles en AEM Assets.

## Activar recortes inteligentes de vídeo para vídeos (administrador) {#enable-video-smart-crops}

Para habilitar los recortes inteligentes de vídeo, configure el esquema de metadatos utilizado para los recursos de vídeo.

Ejecute los siguientes pasos:

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de metadatos]**.
1. Abra el esquema de metadatos aplicado a los recursos de vídeo y haga clic en **[!UICONTROL Editar]**.
1. En el Editor de esquemas de metadatos, seleccione la ficha **[!UICONTROL Vídeo]**.
1. Desde la sección **[!UICONTROL Generar formulario]**, arrastre el componente **[!UICONTROL Desplegable]** al formulario.

   ![Se agregó el campo Crear recorte inteligente de vídeo al esquema de metadatos](/help/assets/assets/metadata-schema-form.png)

1. Seleccione el campo recién agregado y configure lo siguiente en el panel **[!UICONTROL Configuración]**:

   * **Etiqueta de campo**: especifique una etiqueta de campo de su elección.
   * **Asignar a propiedad**: `./jcr:content/dam:applyVideoSmartCrop`

1. En la sección **[!UICONTROL Opciones]**, agregue los siguientes valores:

   * Sí → verdadero
   * No hay → falso

   ![Configurar el campo Crear cultivos inteligentes de vídeo](/help/assets/assets/edit-setting1.png)

1. Haga clic en **[!UICONTROL Guardar]**.

>[!NOTE]
>
>Si el esquema de metadatos `dm_video` se usa en su entorno, asegúrese de que la misma configuración también se aplique al esquema `dm_video`. Esto garantiza un comportamiento coherente de los recortes inteligentes de vídeo en todos los tipos de esquemas de vídeo.

## Aplicar recortes inteligentes de vídeo a vídeos aprobados {#apply-video-smart-crops}

Puede aplicar recortes inteligentes de vídeo a los recursos de vídeo si habilita el campo de metadatos y aprueba el recurso.

Ejecute los siguientes pasos:

1. En [!DNL Assets View], seleccione **[!UICONTROL Assets]** y navegue hasta su carpeta.
1. Seleccione el recurso de vídeo.
1. Haga clic en **[!UICONTROL Propiedades]**.
1. En el panel de metadatos, establezca **[!UICONTROL Crear cultivos inteligentes de vídeo]** en **Sí**, actualice el estado del recurso a **[!UICONTROL Aprobado]** y haga clic en **[!UICONTROL Guardar]**.

   ![Recurso de vídeo aprobado con Video Smartcrop habilitado](/help/assets/assets/assets-create-video-smartcrops1.png)

Se muestra un mensaje de confirmación después de que las propiedades se actualicen correctamente.

## Ver salidas de recorte inteligente de vídeo {#view-video-smart-crops}

Una vez generados los recortes inteligentes de vídeo, incluya el parámetro `mode=smartcrop` en la solicitud de entrega de vídeo del extremo `/play` para procesarlos.

* Los recortes inteligentes de vídeo se aplican de forma dinámica durante la reproducción cuando se utiliza el parámetro `mode=smartcrop`.
* El visualizador de Dynamic Media selecciona automáticamente el recorte más adecuado en función del dispositivo y la relación de aspecto.
* La reproducción de vídeo se ajusta dinámicamente para mantener el sujeto clave enfocado.
