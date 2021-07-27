---
title: Creación de representaciones de vídeo de Screens en Screens como Cloud Service
description: En esta página se describe cómo crear representaciones de vídeo de Screens en Screens como Cloud Service.
source-git-commit: 0badd4209b35b4c8cdfa765a08b5d9db749f52b5
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---


# Creación de representaciones de vídeo de Screens en Screens como Cloud Service {#creating-screens-video-renditions}

## Introducción {#introduction}

Esta guía describe cómo crear representaciones de vídeo utilizadas en reproductores de Screens.

>[!IMPORTANT]
>Los pasos resaltados en esta sección deben configurarse si planea utilizar vídeos en canales de Screens.

## Pasos para crear representaciones de vídeo de Screens en Screens como Cloud Service {#steps-creating-screens-video-renditions}

1. Vaya al canal en el proveedor de contenido de Screens.

   >[!NOTE]
   >Consulte [Uso del proveedor de contenido de Screens](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=en#screens-content-provider) para obtener más información.

1. Haga clic en la sección Herramientas de la barra de navegación izquierda, haga clic en **Recursos** y, a continuación, haga clic en **Perfiles de procesamiento**.

   ![](/help/screens-cloud/assets/configure/screens-cp-3.png)

1. Haga clic en **Crear** para crear un nuevo perfil de procesamiento.

   ![](/help/screens-cloud/assets/configure/screens-video-2.png)

1. Introduzca el **Name**, como **ScreensProcessingProfile**.

   ![](/help/screens-cloud/assets/configure/screens-video-3.png)

1. Vaya a la pestaña **Video** para añadir una codificación de vídeo y haga clic en **Add New**.

   ![](/help/screens-cloud/assets/configure/screens-video-4a.png)

1. Introduzca el **Nombre de codificación** como , **screens-fullhd** y la **Velocidad de bits** como **2500**.

   ![](/help/screens-cloud/assets/configure/screens-video-4.png)

   >[!IMPORTANT]
   >Asegúrese de utilizar el nombre de codificación que empieza por &quot;screens-&quot;, solo se considerará que estas representaciones de vídeo reproducen la experiencia de vídeo en Screens como Cloud Service. Introduzca la velocidad de bits que funciona para sus vídeos (2500 kbps para vídeo de 720 px y 5000 kbps para 1080 px).

   >[!NOTE]
   >Se pueden agregar varias representaciones de vídeo con anchura/altura/velocidad de bits variables para trabajar en los vídeos. Recuerde que los dispositivos Screens descargarán todas las representaciones de pantallas, aunque el dispositivo solo reproduzca la representación de vídeo.

1. Haga clic en **Save**.

1. Seleccione el perfil de procesamiento y haga clic en **Aplicar perfil a las carpetas**.

   ![](/help/screens-cloud/assets/configure/screens-video-5.png)

1. Seleccione las carpetas en las que se guardan los vídeos de Screens y haga clic en **Aplicar**.

   ![](/help/screens-cloud/assets/configure/screens-video-6.png)

   >[!NOTE]
   >* Puede crear varios perfiles de procesamiento y aplicarlos a las carpetas correspondientes, de modo que los vídeos de esas carpetas obtengan las representaciones de vídeo específicas.
   >* Cuando se cargan vídeos a la carpeta donde se aplica el perfil de procesamiento, estos se procesan y se crean representaciones configuradas, que los dispositivos Screens utilizan para reproducir los vídeos.


