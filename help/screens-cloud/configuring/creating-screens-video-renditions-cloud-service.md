---
title: Creación de representaciones de vídeo en Screens as a Cloud Service
description: En esta página se describe cómo crear representaciones de vídeo en Pantallas as a Cloud Service.
exl-id: a9c46036-cd29-47fa-81d9-c865cf22c98a
source-git-commit: cf1e2717342ca4e00780428d6ccf264bd8eca371
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 1%

---

# Creación de representaciones de vídeo en Screens as a Cloud Service {#creating-screens-video-renditions}

## Introducción {#introduction}

En esta sección se describe cómo crear representaciones de vídeo utilizadas en reproductores de Screens.

>[!IMPORTANT]
>Los pasos resaltados en esta sección deben estar configurados si planea utilizar vídeos en canales de Screens.

## Pasos para crear representaciones de vídeo en Screens as a Cloud Service {#steps-creating-screens-video-renditions}

Siga los pasos a continuación para crear representaciones de vídeo en Pantallas as a Cloud Service desde el proveedor de contenido de Pantallas:

1. Vaya al canal en el proveedor de contenido de Screens.

   >[!NOTE]
   >Consulte [Uso del proveedor de contenido de Screens](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=en#screens-content-provider) para obtener más información.

1. Haga clic en la sección Herramientas de la barra de navegación izquierda y haga clic en **Assets** y luego haga clic en **Perfiles de procesamiento**.

   ![Haga clic en Perfiles de procesamiento](/help/screens-cloud/assets/configure/screens-cp-3.png)

1. Haga clic en **Crear** para crear un nuevo perfil de procesamiento.

   ![Haga clic en Crear](/help/screens-cloud/assets/configure/screens-video-2.png)

1. Introduzca el **Nombre**, como **ScreensProcessingProfile**.

   ![](/help/screens-cloud/assets/configure/screens-video-3.png)

1. Vaya a **Vídeo** para añadir una codificación de vídeo y hacer clic en **Añadir nuevo**.

   ![](/help/screens-cloud/assets/configure/screens-video-4a.png)

1. Introduzca el **Nombre de codificación** como , **screens-fullhd** y el **Velocidad de bits** as **2500**.

   ![](/help/screens-cloud/assets/configure/screens-video-4.png)

   >[!IMPORTANT]
   >Asegúrese de utilizar el nombre de codificación que comienza con &quot;screens-&quot;, solo se considera que estas representaciones de vídeo reproducen la experiencia de vídeo en Screens as a Cloud Service. Introduzca la velocidad de bits que funciona para sus vídeos (2500 kbps para vídeo de 720 px y 5000 kbps para 1080 px).

   >[!NOTE]
   >Se pueden agregar varias representaciones de vídeo con diferentes anchura, altura y velocidad de bits para trabajar con los vídeos. Los dispositivos de Screens descargan todas las pantallas y representaciones, aunque el dispositivo solo reproduzca vídeo.

1. Haga clic en **Guardar**.

1. Seleccione el perfil de procesamiento y haga clic en **Aplicar perfil a las carpetas**.

   ![Aplicar perfil a la carpeta](/help/screens-cloud/assets/configure/screens-video-5.png)

1. Seleccione las carpetas donde se guardan los vídeos de Screens y haga clic en **Aplicar**.

   ![Haga clic en Aplicar](/help/screens-cloud/assets/configure/screens-video-6.png)

   >[!NOTE]
   >* Puede crear varios perfiles de procesamiento y aplicarlos a las carpetas correspondientes, de modo que los vídeos de esas carpetas obtengan las representaciones de vídeo específicas.
   >* Al cargar vídeos en la carpeta en la que se aplica el perfil de procesamiento, se procesan y se crean representaciones configuradas de los vídeos, que los dispositivos de Screens utilizan también para reproducir los vídeos.
