---
title: Representaciones de vídeo
description: Representaciones de vídeo
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Video renditions {#video-renditions}

Recursos Adobe Experience Manager (AEM) genera representaciones de vídeo para recursos de vídeo de varios formatos, incluidos OGG, FLV, etc.

Recursos AEM admite representaciones estáticas y dinámicas (representaciones con codificación DM) para recursos multimedia.

Las representaciones estáticas se generan de forma nativa utilizando FFMPEG (instalado y disponible en la ruta del sistema) y se almacenan en el repositorio de contenido.

Las representaciones con codificación DM se almacenan en el servidor proxy y se sirven en tiempo de ejecución.

Los recursos de AEM admiten la reproducción de estas representaciones en el lado del cliente.

Para ver las representaciones de un recurso de vídeo concreto, abra su página de recursos y toque el icono de navegación global. A continuación, seleccione **[!UICONTROL Representaciones]** en la lista.

La lista de representaciones de vídeo se muestra en el panel **[!UICONTROL Representaciones]** .

Para configurar el servidor proxy para las representaciones con codificación DM, configure los servicios de Dynamic Media Cloud.

<!-- To generate video renditions with desired parameters, [create a corresponding video profile](video-profiles.md). -->

Después de configurar el servidor proxy y crear perfiles de vídeo, puede incluir este ajuste preestablecido de vídeo en un perfil de procesamiento y aplicar el perfil de procesamiento a una carpeta.

>[!NOTE]
>
>La reproducción de audio no funciona con archivos OGG y WAV en Internet Explorer 11. Se muestra un error &quot;Origen no válido&quot; en la página de detalles del recurso para los recursos con la extensión OGG o WAV. En MS Edge y iPad, los archivos OGG no se reproducen y generan un error de formato no admitido.