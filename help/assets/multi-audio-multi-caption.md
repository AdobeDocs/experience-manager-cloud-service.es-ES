---
title: Varios subtítulos y audio en Dynamic Media con vídeos de funciones de OpenAPI
description: Obtenga información sobre cómo añadir y administrar varias pistas de audio y subtítulos para recursos de vídeo en Dynamic Media con las funciones de OpenAPI en Adobe Experience Manager Assets.
role: User
badgeSaas: label="AEM Assets" type="Positive"
source-git-commit: 111fa1857261c71999088b2c061ae778115e5ef4
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 6%

---


# Varios subtítulos y audio en Dynamic Media con vídeos de funciones de OpenAPI {#multi-audio-captions-dynamic-media-with-openapi-capabilities}

[!DNL Adobe Experience Manager Assets] Dynamic Media con capacidades OpenAPI le permite agregar varias pistas de audio y archivos de subtítulos a los recursos de vídeo. Esta capacidad mejora la accesibilidad, admite experiencias de reproducción localizadas y mejora la entrega de vídeo para audiencias globales.

Estas características se administran directamente desde la pestaña **Pistas de subtítulos y audio** de la página de propiedades del recurso de vídeo.

>[!NOTE]
>
>La compatibilidad con varios subtítulos y audio en Dynamic Media con las capacidades de OpenAPI es una función de disponibilidad limitada. Puede habilitarlo creando un [ticket de asistencia](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html).

Todos los formatos de vídeo compatibles con Dynamic Media con funciones OpenAPI admiten varios subtítulos y pistas de audio.

## Antes de empezar {#before-you-begin}

Asegúrese de lo siguiente:

* El recurso de vídeo está disponible en [!DNL AEM Assets]
* Formato de audio admitido: `.mp3`
* Formato de rótulo admitido: `.vtt`

>[!NOTE]
>
>Dynamic Media con funciones de OpenAPI no requiere un perfil de vídeo. La ficha **Pistas de subtítulos y audio** está disponible para todos los recursos de vídeo de forma predeterminada.

## Añadir varias pistas de audio {#add-audio-tracks}

![Ficha Pistas de subtítulos y audio](/help/assets/assets/caption-audio-tracks1.png)

Para agregar pistas de audio a un vídeo:

1. Vaya al recurso de vídeo cargado.
2. Seleccione el recurso y haga clic en **Propiedades**.
3. Abra la ficha **Pistas de subtítulos y audio**.
4. Haga clic en **Cargar pistas de audio**.
5. Seleccione uno o más `.mp3` archivos.
6. Haga clic en el icono **Dibujar** junto al nombre del archivo de pista de audio.

En el cuadro de diálogo **Editar pista de audio**:

* **Nombre de archivo** - Nombre de archivo predeterminado derivado del archivo cargado.
* **Idioma** - Seleccione el idioma del audio.
* **Tipo** - Descripción original, estándar o de audio.
* **Etiqueta** - Nombre para mostrar mostrado en el selector de audio del reproductor.

![Cuadro de diálogo Pista de audio](/help/assets/assets/edit-audio1.png)

1. Haga clic en **Guardar**.
2. Si es necesario, repita la operación para pistas de audio adicionales.
3. Haga clic en **Guardar y cerrar**.

>[!NOTE]
>
>Cada etiqueta de pista de audio debe ser única.

## Añadir varios subtítulos {#add-captions}

![Ficha Pistas de subtítulos y audio](/help/assets/assets/caption-audio-tracks1.png)

Para agregar subtítulos:

1. Abra la página del vídeo **Propiedades**.
2. Abra la pestaña **Subtítulos y pistas de audio**.
3. Haga clic en **Crear pie de ilustración** > **Cargar archivos**.
4. Seleccione uno o más `.vtt` archivos.
5. Haga clic en el icono **Dibujar** junto al archivo de rótulo.

![Cuadro de diálogo Cargar pie de ilustración](/help/assets/assets/upload-caption.png)

En el cuadro de diálogo **Editar título**:

* **Nombre de archivo** - Nombre de archivo cargado predeterminado.
* **Idioma** - Idioma del pie de ilustración.
* **Tipo** - Subtítulo o pie de ilustración.
* **Etiqueta** - Nombre para mostrar mostrado en el selector de subtítulos del reproductor.

![Cuadro de diálogo Editar pie de ilustración](/help/assets/assets/edit-captions.png)

1. Haga clic en **Guardar**.
2. Haga clic en **Guardar y cerrar**.

>[!NOTE]
>
>No se admite la edición del texto de subtítulos. Actualice el archivo externamente y vuelva a cargarlo.

## Comportamiento de aprobación {#approval-behavior}

La aprobación depende del recurso de vídeo principal:

* Si se **aprobó**, los nuevos archivos se aprueban automáticamente después del procesamiento.
* Si no se aprueban, siguen el ciclo vital principal.

## Ver estado del ciclo vital del archivo {#status}

* **Aprobado** - Listo para la reproducción
* **Rechazado** - Archivo rechazado

## Definir pista de audio predeterminada {#set-default-audio}

De forma predeterminada, se utiliza el audio original.

1. Abrir **Subtítulos y pistas de audio**.

2. Seleccione la pista de audio.

3. Haga clic en **Establecer como predeterminado**.

   ![Establecer como acción predeterminada](/help/assets/assets/set-default.png)

4. Haga clic en **OK**.

5. Haga clic en **Guardar y cerrar**.

## Previsualizar audio y subtítulos {#preview-audio-captions}

Después del procesamiento:

1. Abra la previsualización de vídeo.

   ![Reproductor de vista previa de vídeo](/help/assets/assets/preview-caption-audio.png)

2. Usar controles del reproductor:

   * Cambiar pistas de audio
   * Habilitar subtítulos

## Descargar subtítulos o archivos de audio {#download-tracks}

1. Seleccione el pie de ilustración o el archivo de audio.

2. Haga clic en **Descargar**.

   ![Descargar acción de seguimiento](/help/assets/assets/download-caption.png)

3. Haga clic en **Descargar**.

El archivo seleccionado se descargará en el sistema local.

## Eliminar pie de ilustración o archivos de audio {#delete-tracks}

1. Seleccione el pie de ilustración o el archivo de audio.

2. Haga clic en **Eliminar**.

   ![Eliminar acción de seguimiento](/help/assets/assets/delete-caption.png)

3. Haga clic en **OK**.

No se puede eliminar el audio original extraído del vídeo.