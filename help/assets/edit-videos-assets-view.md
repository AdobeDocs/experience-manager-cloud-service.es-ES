---
title: Edición de vídeos
description: Editar vídeos con [!DNL Adobe Express] opciones de y guardar vídeos actualizados como versiones de.
role: User
exl-id: 42b25935-e2ff-444f-97c8-b4ed56f3ef9e
source-git-commit: 79e72f967673010b936bd0464a2fcf0a1c068e69
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 18%

---

# Edición de vídeos en [!DNL Assets view] {#edit-videos}

Crear variaciones de contenido de vídeo es fácil para los usuarios de Assets con el [!DNL Adobe Express] acciones rápidas para vídeo. Acciones rápidas en [!DNL Assets view] equipado con [!DNL Adobe Express] proporciona opciones de edición de vídeo fáciles de usar, como recorte de vídeo, cambio de tamaño de vídeo, recorte de vídeo y conversión de vídeo a GIF.

Para editar un vídeo, vaya a los detalles del vídeo y haga clic en [!UICONTROL Editar vídeo]. También puede seleccionar el recurso, hacer clic en Detalles y luego hacer clic en ![tijera](assets/do-not-localize/cut.svg) disponible en el panel derecho. Después de editar un vídeo, puede guardarlo como una nueva versión o como un nuevo recurso.

## Requisitos previos {#prerequisites}

Derechos de acceso [!DNL Adobe Express] y al menos un entorno dentro de AEM Assets. El entorno puede ser cualquiera de los repositorios de [!DNL Assets as a Cloud Service] o [!DNL Assets view].

## Editar vídeos con el Adobe Express {#edit-video-using-express}

Transformar un vídeo en un tamaño y una orientación perfectos es fácil gracias al uso de funciones integradas [!DNL Adobe Express] acciones rápidas.

### Recortar vídeo {#crop-video-using-express}

Puede eliminar partes no deseadas del vídeo si utiliza funciones integradas [!DNL Adobe Express] acciones rápidas. Para ello, ejecute los pasos a continuación:

1. Seleccione un vídeo y haga clic en **[!UICONTROL Editar]**.
2. Clic **[!UICONTROL Recortar vídeo]** de las acciones rápidas disponibles en el panel izquierdo.
3. Arrastre los controladores de las esquinas del vídeo para crear el recorte deseado; o elija entre los tamaños de pantalla existentes según desee.
4. Puede optar por silenciar o reactivar el vídeo.
5. Haga clic en **[!UICONTROL Aplicar]**.
   ![recortar vídeo con Adobe Express](assets/adobe-express-crop-video.png)

   El vídeo recortado está disponible para descargar. Puede guardar el recurso editado como una nueva versión del mismo recurso o guardarlo como un nuevo recurso. ![Guardar vídeo con Adobe Express](assets/adobe-express-save-video.png)

### Cambiar tamaño de vídeo {#resize-video-using-express}

El contenido final de vídeo en DAM suele necesitar un cambio de tamaño para su distribución en canales específicos. [!DNL Assets view] le permite cambiar fácilmente el tamaño del vídeo para adaptarlo a las dimensiones requeridas por los canales sociales comunes y también puede cambiar el tamaño para obtener resoluciones personalizadas. Para cambiar el tamaño del vídeo mediante [!DNL Assets view], ejecute los pasos siguientes:

1. Seleccione un vídeo y haga clic en **[!UICONTROL Editar]**.
2. Clic **[!UICONTROL Cambiar tamaño de vídeo]** de las acciones rápidas disponibles en el panel izquierdo.
3. Seleccione las dimensiones adecuadas de la plataforma de medios sociales en **[!UICONTROL Cambiar tamaño para]** lista desplegable. También puede arrastrar los controladores de las esquinas del vídeo para crear el recorte deseado.
4. Escale el vídeo, si es necesario, utilizando **[!UICONTROL Escala de vídeo]** field.
5. Puede optar por silenciar o reactivar el vídeo.
6. Haga clic en **[!UICONTROL Aplicar]** para que tengan efecto los cambios.
   ![Redimensionado de vídeo con Adobe Express](assets/adobe-express-resize-video.png)

El vídeo que ha cambiado de tamaño está disponible para descargar. Puede guardar el recurso editado como una nueva versión del mismo recurso o guardarlo como uno nuevo.

### Recortar vídeo {#trim-video-using-express}

Si necesita utilizar un clip de un vídeo más grande, puede utilizar el **[!UICONTROL Recortar vídeo]** para seleccionar y recortar una sección del vídeo. Siga estos pasos:

1. Seleccione un vídeo y haga clic en **[!UICONTROL Editar]**.
2. Clic **[!UICONTROL Recortar vídeo]** de las acciones rápidas disponibles en el panel izquierdo.
3. Especifique la hora de inicio y finalización del vídeo para recortar una parte concreta. También puede arrastrar los controladores de las esquinas del vídeo para crear el recorte deseado.
4. Seleccione las dimensiones adecuadas de la **[!UICONTROL Tamaño]** lista desplegable.
5. Puede optar por silenciar o reactivar el vídeo.
6. Haga clic en **[!UICONTROL Aplicar]** para que tengan efecto los cambios.
   ![Redimensionado de vídeo con Adobe Express](assets/adobe-express-trim-video.png)

El vídeo recortado está disponible para descargar. Puede guardar el recurso editado como una nueva versión del mismo recurso o guardarlo como uno nuevo.

### Convertir vídeo en GIF {#convert-mp4-to-gif-using-express}

Puede convertir rápidamente un vídeo MP4 a un formato de GIF mediante el Adobe Express. Ejecute los siguientes pasos:

1. Seleccione un vídeo y haga clic en **[!UICONTROL Editar]**.
2. Clic **[!UICONTROL Convertir en GIF]** de las acciones rápidas disponibles en el panel izquierdo.
3. Seleccione el tamaño de archivo adecuado en función de la calidad deseada. Además, elija la orientación horizontal, vertical o cuadrada.
4. Arrastre los controladores de las esquinas del vídeo para crear el recorte deseado.
5. Haga clic en **[!UICONTROL Aplicar]**.

   ![Convertir vídeo en GIF con Adobe Express](assets/adobe-express-convert-video-to-gif.png)

El vídeo está disponible en formato GIF para su descarga. Puede guardar el recurso editado como una nueva versión del mismo recurso o guardarlo como uno nuevo.

## Restricciones {#limitations-video-adobe-express}

* Solo se admiten vídeos en formato MP4 para su edición.

* El tamaño máximo de archivo de origen admitido es de 1 GB.

* Los vídeos compatibles tienen más de 46 píxeles y menos de 3840 píxeles en cualquier lado.

* Los exploradores web admitidos son Google Chrome, Firefox, Safari y Edge.

* La funcionalidad no se puede abrir en un modo incógnito de un explorador web.

### Siguientes pasos {#next-steps}

* Realice comentarios del producto mediante la opción [!UICONTROL Comentarios] disponible en la interfaz de usuario de la vista Recursos

* Proporcione comentarios sobre la documentación usando [!UICONTROL Editar esta página] ![editar la página](assets/do-not-localize/edit-page.png) o [!UICONTROL Registrar una incidencia] ![crear una incidencia de GitHub](assets/do-not-localize/github-issue.png), disponibles en la barra lateral derecha

* Contacto con el [Servicio de atención al cliente](https://experienceleague.adobe.com/?support-solution=General#support)

>[!MORELIKETHIS]
>
>* [Editar imágenes en la vista Recursos](edit-images-assets-view.md)
>* [Previsualización de un recurso](navigate-assets-view.md)
