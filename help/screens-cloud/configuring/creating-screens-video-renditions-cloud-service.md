---
title: Creación de representaciones de vídeo en Screens as a Cloud Service
description: En esta página se describe cómo crear representaciones de vídeo en Screens as a Cloud Service.
exl-id: a9c46036-cd29-47fa-81d9-c865cf22c98a
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# Creación de representaciones de vídeo en Screens as a Cloud Service {#creating-screens-video-renditions}

## Introducción {#introduction}

En esta sección se describe cómo crear representaciones de vídeo utilizadas en reproductores de Screens.

>[!IMPORTANT]
>Los pasos resaltados en esta sección deben configurarse si planea utilizar vídeos en canales de Screens.

## Pasos para crear representaciones de vídeo en Screens as a Cloud Service {#steps-creating-screens-video-renditions}

Siga los pasos a continuación para crear representaciones de vídeo en Screens as a Cloud Service desde el proveedor de contenido de Screens:

1. Vaya al canal en el proveedor de contenido de Screens.

   >[!NOTE]
   >Consulte [Uso del proveedor de contenido de Screens](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=en#screens-content-provider) para obtener más información.

1. Haga clic en la sección Herramientas de la barra de navegación izquierda y haga clic en **Recursos** y haga clic en **Perfiles de procesamiento**.

   ![](/help/screens-cloud/assets/configure/screens-cp-3.png)

1. Haga clic en **Crear** para crear un nuevo perfil de procesamiento.

   ![](/help/screens-cloud/assets/configure/screens-video-2.png)

1. Introduzca la variable **Nombre**, como **ScreensProcessingProfile**.

   ![](/help/screens-cloud/assets/configure/screens-video-3.png)

1. Vaya a **Vídeo** para añadir una codificación de vídeo y haga clic en **Agregar nuevo**.

   ![](/help/screens-cloud/assets/configure/screens-video-4a.png)

1. Introduzca la variable **Nombre de codificación** como , **screens-fullhd** y **Velocidad de bits** como **2500**.

   ![](/help/screens-cloud/assets/configure/screens-video-4.png)

   >[!IMPORTANT]
   >Asegúrese de utilizar el nombre de codificación que empieza por &quot;screens-&quot;, solo se considerará que estas representaciones de vídeo reproducen la experiencia de vídeo en Screens as a Cloud Service. Introduzca la velocidad de bits que funciona para sus vídeos (2500 kbps para vídeo de 720 px y 5000 kbps para 1080 px).

   >[!NOTE]
   >Se pueden agregar varias representaciones de vídeo con anchura/altura/velocidad de bits variables para trabajar en los vídeos. Recuerde que los dispositivos Screens descargarán todas las representaciones de pantallas, aunque el dispositivo solo reproduzca la representación de vídeo.

1. Haga clic en **Guardar**.

1. Seleccione el perfil de procesamiento y haga clic en **Aplicar perfil a carpetas**.

   ![](/help/screens-cloud/assets/configure/screens-video-5.png)

1. Seleccione las carpetas en las que se guardan los vídeos de Screens y haga clic en **Aplicar**.

   ![](/help/screens-cloud/assets/configure/screens-video-6.png)

   >[!NOTE]
   >* Puede crear varios perfiles de procesamiento y aplicarlos a las carpetas correspondientes, de modo que los vídeos de esas carpetas obtengan las representaciones de vídeo específicas.
   >* Cuando se cargan vídeos a la carpeta donde se aplica el perfil de procesamiento, estos se procesan y se crean representaciones configuradas, que los dispositivos Screens utilizan para reproducir los vídeos.

