---
title: Creación de representaciones de vídeo en Screens as a Cloud Service
description: En esta página se describe cómo crear representaciones de vídeo en Screens as a Cloud Service.
exl-id: a9c46036-cd29-47fa-81d9-c865cf22c98a
feature: Administering Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---

# Creación de representaciones de vídeo en Screens as a Cloud Service {#creating-screens-video-renditions}

## Introducción {#introduction}

En esta sección se describe cómo crear representaciones de vídeo utilizadas en reproductores de Screens.

>[!IMPORTANT]
>Los pasos resaltados en esta sección deben estar configurados si planea utilizar vídeos en canales de Screens.

## Pasos para crear representaciones de vídeo en Screens as a Cloud Service {#steps-creating-screens-video-renditions}

Siga los pasos a continuación para crear representaciones de vídeo en Screens as a Cloud Service desde el proveedor de contenido de Screens:

1. Vaya al canal en el proveedor de contenido de Screens.

   >[!NOTE]
   >Consulte [Uso del proveedor de contenido de Screens](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=es#screens-content-provider) para obtener más información.

1. Haga clic en la sección Herramientas de la barra de navegación izquierda, haga clic en **Assets** y, a continuación, haga clic en **Perfiles de procesamiento**.

   ![Perfiles de procesamiento de clic](/help/screens-cloud/assets/configure/screens-cp-3.png)

1. Haga clic en **Crear** para crear un perfil de procesamiento.

   ![Haga clic en Crear](/help/screens-cloud/assets/configure/screens-video-2.png)

1. Escriba **Name**, como **ScreensProcessingProfile**.

   ![Cuadro de diálogo Perfil de procesamiento que muestra el campo Nombre resaltado.](/help/screens-cloud/assets/configure/screens-video-3.png)

1. Vaya a la pestaña **Vídeo** para poder agregar una codificación de vídeo y, a continuación, haga clic en **Agregar nuevo**.

   ![Cuadro de diálogo Perfil de procesamiento que muestra el botón Agregar nuevo resaltado.](/help/screens-cloud/assets/configure/screens-video-4a.png)

1. Escriba el **Nombre de codificación** como , **screens-fullhd** y la **Velocidad de bits** como **2500**.

   ![Cuadro de diálogo Perfil de procesamiento que muestra el botón Guardar resaltado.](/help/screens-cloud/assets/configure/screens-video-4.png)

   >[!IMPORTANT]
   >Utilice el nombre de codificación que comienza con &quot;screens-&quot;. Solo se considera que estas representaciones de vídeo reproducen la experiencia de vídeo en Screens as a Cloud Service. Introduzca la velocidad de bits de funcionamiento de los vídeos (2500 kbps para vídeo de 720 px y 5000 kbps para vídeo de 1080 px).

   >[!NOTE]
   >Se pueden agregar varias representaciones de vídeo con diferentes anchura, altura y velocidad de bits para trabajar con los vídeos. Los dispositivos Screens descargan todas las pantallas y representaciones, aunque el dispositivo solo reproduzca representaciones de vídeo.

1. Haga clic en **Guardar**.

1. Seleccione el perfil de procesamiento y haga clic en **Aplicar perfil a las carpetas**.

   ![Aplicar perfil a la carpeta](/help/screens-cloud/assets/configure/screens-video-5.png)

1. Seleccione las carpetas donde se guardan los vídeos de Screens y haga clic en **Aplicar**.

   ![Haga clic en Aplicar](/help/screens-cloud/assets/configure/screens-video-6.png)

   >[!NOTE]
   >
   >* Puede crear varios perfiles de procesamiento y aplicarlos a las carpetas correspondientes, de modo que los vídeos de esas carpetas obtengan las representaciones de vídeo específicas.
   >* Al cargar vídeos en la carpeta en la que se aplica un perfil de procesamiento, estos se procesan. Se crean representaciones configuradas que los dispositivos Screens utilizan para reproducir los vídeos.
