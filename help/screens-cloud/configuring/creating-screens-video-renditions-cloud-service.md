---
title: Creación de representaciones de vídeo de Screens en Screens como Cloud Service
description: En esta página se describe cómo crear representaciones de vídeo de Screens en Screens como Cloud Service.
source-git-commit: b8691bb77079eeb7efd141ce89c44c5a312262b3
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---


# Creación de representaciones de vídeo de Screens en Screens como Cloud Service {#creating-screens-video-renditions}

## Introducción {#introduction}

Esta guía describe cómo crear representaciones de vídeo utilizadas en reproductores de Screens.

>[!IMPORTANT]
>Los pasos resaltados en esta sección deben configurarse si planea utilizar vídeos en canales de Screens.

## Pasos para crear representaciones de vídeo de Screens en Screens como Cloud Service {#steps-creating-screens-video-renditions}

1. Vaya a los canales en la interfaz de usuario de Screens Cloud.
1. Haga clic en Adobe Experience Manager en la esquina superior izquierda para ir al Proveedor de contenido de Screens, es decir, AEM como Cloud Service.
1. Haga clic en la sección Herramientas en la navegación principal ahora, haga clic en &quot;Recursos&quot; y luego haga clic en &quot;Perfiles de procesamiento&quot;

1. Haga clic en &quot;Crear&quot; para crear un nuevo perfil de procesamiento
1. Proporcione un nombre como &quot;ScreensProcessingProfile&quot;.
1. Vaya a la pestaña Vídeo para añadir una codificación de vídeo y haga clic en Añadir nuevo .


   >[!IMPORTANT]
   >Asegúrese de utilizar el nombre de codificación que empieza por &quot;screens-&quot;, solo se considerará que estas representaciones de vídeo reproducen la experiencia de vídeo en Screens As a Cloud Service. Introduzca la velocidad de bits que se adapte a sus vídeos (2500 kbps para vídeo de 720 px y 5000 kbps para 1080 px)

   >[!NOTE]
   >Se pueden agregar varias representaciones de vídeo con distintos niveles de anchura, altura y velocidad de bits para adaptarlas a sus necesidades, pero recuerde que los dispositivos Screens descargarán todas las representaciones de vídeo de pantallas, aunque el dispositivo solo reproduzca vídeo.

1. Haga clic en Guardar

1. Seleccione el perfil de procesamiento y haga clic en &quot;Aplicar perfil a las carpetas&quot;

1. Seleccione las carpetas en las que se guardan los vídeos de Screens y haga clic en Aplicar

1. Puede crear varios perfiles de procesamiento y aplicarlos a las carpetas correspondientes, de modo que los vídeos de esas carpetas obtengan las representaciones de vídeo específicas

1. Al cargar cualquier vídeo en la carpeta donde se aplique el perfil de procesamiento, los vídeos se procesarán y se crearán representaciones configuradas, que los dispositivos Screens utilizarán para reproducir los vídeos.

