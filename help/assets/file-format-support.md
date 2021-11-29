---
title: Formatos de archivo compatibles y tipos MIME
description: Formatos de archivo y tipos MIME admitidos por [!DNL Experience Manager Assets] como [!DNL Cloud Service].
contentOwner: AG
feature: Asset Management,Renditions
role: User,Admin
exl-id: e848aa77-7829-4adc-8b88-0279791a4525
source-git-commit: 6c17b048631a7f61305ec4f0a4f84c4b0577aec0
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 9%

---

# [!DNL Assets] formatos de archivo compatibles {#supported-file-formats}

[!DNL Adobe Experience Manager] como [!DNL Cloud Service] admite capacidades básicas de administración de contenido (almacenamiento, administración de metadatos en línea, versiones, carga y descarga, etc.) para cualquier archivo binario, independientemente de su formato. [!DNL Adobe Experience Manager Assets] admite una amplia gama de formatos de archivo y cada función de producto tiene compatibilidad variada con distintos formatos.

Además, [!DNL Experience Manager Assets] proporciona compatibilidad ampliada para generar vistas previas y representaciones, y para extraer metadatos y texto para la indexación de texto completo. Esta compatibilidad ampliada se proporciona mediante [microservicios de recursos](asset-microservices-configure-and-use.md).

Los aspectos destacados de la conversión de recursos mediante los microservicios de recursos son:

* Clave [Formatos de archivo de Adobe](#adobe-formats) producidos por aplicaciones y servicios de Adobe, incluidos [!DNL Adobe Photoshop], [!DNL Adobe InDesign], [!DNL Adobe Illustrator], [!DNL Adobe XD], [!DNL Adobe Dimension]y [!DNL Adobe Acrobat] o PDF.
* Clave [formatos de archivo de imagen](#image-formats).
* [Formatos de archivo Camera Raw](#camera-raw-formats) para una amplia gama de cámaras, incluidas Canon, Nikon, Fujifilm, Olympus y otros fabricantes (con tecnología Adobe Camera Raw).
* Frecuentes [formatos de documento](#document-formats), incluidos los formatos Microsoft Office y Open Document.
* Amplia gama de formatos de [vídeo](#video-formats) y [audio.](#audio-formats)

La leyenda siguiente describe el nivel de compatibilidad con cada formato.

| Nivel de asistencia | Descripción |
| ------------- | --------------------------- |
| ✓ | Compatible |
| * | Véanse las observaciones que figuran a continuación del cuadro |
| - | No aplicable |

## formatos de Adobe {#adobe-formats}

| Formato del archivo | Generación de miniaturas | Extracción de texto completo | Extracción de metadatos | Anchura/Altura |
| ----------- | -------------------- | ------------------- | ------------------- | ------------ |
| AI | ✓ | - | ✓ | ✓ |
| COLLAGE | - | - | ✓ | - |
| DN | ✓ | - | ✓ | ✓ |
| IDEAS | - | - | ✓ | - |
| INDD | ✓ | - | ✓ | ✓ * |
| INDT | - | - | ✓ | - |
| PDF | ✓ | ✓ | ✓ | ✓ |
| PROTO | - | - | ✓ | - |
| PSB | ✓ | - | ✓ | ✓ |
| PSD | ✓ | - | ✓ | ✓ |
| XD | ✓ | - | ✓ | ✓ |

\* Para [!DNL Adobe InDesign] archivos (INDD), el tamaño de la representación viene determinado por la previsualización incrustada en el archivo INDD. Configure las preferencias en [!DNL InDesign] (**[!UICONTROL Preferencias > Administración de archivos > Guardar siempre imágenes de vista previa con documentos, Tamaño de vista previa]**) para incrustar una representación más grande.

## Formatos de imagen {#image-formats}

| Formato del archivo | Generación de miniaturas | Extracción de metadatos | Anchura/Altura | Recortar |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | ✓ | - | ✓ | ✓ |
| EPS | - | ✓ | - | - |
| GIF | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ |
| RGB | ✓ | ✓ | ✓ | ✓ |
| RGBA | ✓ | ✓ | ✓ | ✓ |
| SGI | ✓ | ✓ | ✓ | ✓ |
| SVG | ✓ | - | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | - |

## Formatos de imagen en [!DNL Dynamic Media] {#image-support-dynamic-media}

| Formato | Cargar (formato de entrada) | Crear ajuste preestablecido de imagen (formato de salida) | Vista previa de la representación dinámica | Entregar representación dinámica | Descargar representación dinámica |
| ------- | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| BMP | ✓ | - | - | - | - |
| EPS | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| PICT | ✓ | - | - | - | - |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| PSD } | ✓ | - | - | - | - |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |

✓ La imagen combinada se extrae del archivo PSD. Es una imagen generada por [!DNL Adobe Photoshop] y se incluye en el archivo PSD. Dependiendo de la configuración, la imagen combinada puede ser o no la imagen real.

Los siguientes subtipos de formatos de archivo de imagen de trama no son compatibles con [!DNL Dynamic Media]:

* Los archivos PNG que tienen un tamaño de fragmento IDAT tienen un tamaño bueno de más de 100 MB.
* Archivos PSB.
* Los archivos PSD con un espacio de color distinto de CMYK, RGB, escala de grises o mapa de bits no son compatibles. Los espacios de color DuoTone, Lab e Indexed no son compatibles.
* archivos PSD con una profundidad buena superior a 16.
* archivos TIFF que tienen datos de coma flotante.
* Archivos TIFF que tienen espacio de color Lab.

## Formatos 3D {#support-3d-formats}

Se admiten los siguientes formatos 3D.

Consulte también [Uso de recursos 3D en Dynamic Media](/help/assets/dynamic-media/assets-3d.md).

| Formato | Almacenamiento | Versiones | Flujo de trabajo | Publicación | Control de acceso | Vista previa de miniatura | Vista previa 3D | Entrega de Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ | - | ✓ | ✓ | - | - |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ | - | ✓ | - | ✓ | - |
| OBJ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| USDz | ✓ | ✓ | ✓ | ✓ | ✓ | - | - | ✓ |

## [!DNL Camera RAW] formatos {#camera-raw-formats}

| Formato del archivo | Generación de miniaturas | Extracción de metadatos | Anchura/Altura |
| ----------- | -------------------- | ------------------- | ------------ |
| 3FR | ✓ | ✓ | ✓ |
| ARW | ✓ | ✓ | ✓ |
| CR2 | ✓ | ✓ | ✓ |
| CR3 | ✓ | ✓ | ✓ |
| CRW | ✓ | ✓ | ✓ |
| DCR | ✓ | ✓ | ✓ |
| DNG | ✓ | ✓ | ✓ |
| ERF | ✓ | ✓ | ✓ |
| FFF | ✓ | ✓ | ✓ |
| RGPD | ✓ | ✓ | ✓ |
| IIQ | ✓ | ✓ | ✓ |
| KDC | ✓ | ✓ | ✓ |
| MEF | ✓ | ✓ | ✓ |
| MFW | ✓ | ✓ | ✓ |
| MOS | ✓ | ✓ | ✓ |
| MRW | ✓ | ✓ | ✓ |
| NEF | ✓ | ✓ | ✓ |
| NRW | ✓ | ✓ | ✓ |
| ORF | ✓ | ✓ | ✓ |
| PEF | ✓ | ✓ | ✓ |
| RAF | ✓ | ✓ | ✓ |
| RAW | ✓ | ✓ | ✓ |
| RW2 | ✓ | ✓ | ✓ |
| RWL | ✓ | ✓ | ✓ |
| SRF | ✓ | ✓ | ✓ |
| SRW | ✓ | ✓ | ✓ |
| X3F | ✓ | ✓ | ✓ |

## Formatos de documento {#document-formats}

Los formatos de documento admitidos para las funciones de administración de recursos son los siguientes.

| Formato del archivo | Generación de miniaturas | Extracción de texto completo | Anchura/Altura | Gestión de metadatos | [Recursos conectados](use-assets-across-connected-assets-instances.md) |
| ----------- | -------------------- | ------------------- | ------------ | ------------------- | ---------------- |
| DOC | - | - | - | ✓ | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ |
| ePub | - | ✓ | - | - | - |
| HTML | - | ✓ | - | ✓ | ✓ |
| ODF | ✓ | ✓ | ✓ | - | - |
| ODM | ✓ | ✓ | ✓ | - | - |
| ODP | ✓ | ✓ | ✓ | - | - |
| ODS | ✓ | ✓ | ✓ | - | - |
| ODT | ✓ | ✓ | ✓ | ✓ | ✓ |
| OFG | ✓ | ✓ | ✓ | - | - |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ |
| PPT | - | - | - | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ |
| PS | - | - | ✓ | - | - |
| RTF | - | ✓ | - | ✓ | ✓ |
| TXT | ✓ | ✓ | - | ✓ | ✓ |
| XLS | - | - | - | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | - | ✓ | - | - | - |

## Formatos de documento en [!DNL Dynamic Media] {#document-support-dynamic-media}

| Formato | Cargar (formato de entrada) | Crear ajuste preestablecido de imagen (formato de salida) | Vista previa de la representación dinámica | Entregar representación dinámica | Descargar representación dinámica |
| ------ | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| AI | ✓ | - | - | - | - |
| INDD | ✓ | - | - | - | - |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ |

## Formatos de vídeo {#video-formats}

| Formato del archivo | Generación de miniaturas | Extracción de metadatos | Anchura/Altura |
| ----------- | -------------------- | ------------------- | ------------ |
| 3G2 | - | ✓ | - |
| 3GP | - | ✓ | - |
| AVI | ✓ | ✓ | ✓ |
| DIVX | ✓ | - | ✓ |
| F4V | ✓ | ✓ | ✓ |
| FLV | ✓ | ✓ | ✓ |
| M2T | ✓ | - | ✓ |
| M2TS | ✓ | - | ✓ |
| M2V | ✓ | - | ✓ |
| M4V | ✓ | ✓ | ✓ |
| MKV | ✓ | - | ✓ |
| MOV | ✓ | ✓ | ✓ |
| MP4 | ✓ | ✓ | ✓ |
| MPEG | ✓ | ✓ | ✓ |
| MPG | ✓ | ✓ | ✓ |
| MTS | ✓ | - | ✓ |
| MXF | ✓ | - | ✓ |
| OGV | ✓ | - | ✓ |
| QT | ✓ | - | ✓ |
| R3D | - | ✓ | ✓ |
| SWF | ✓ | - | ✓ |
| WebM | ✓ | - | ✓ |
| WMV | ✓ | ✓ | ✓ |

## Formatos de vídeo en [!DNL Dynamic Media] para la transcodificación {#video-dynamic-media-transcoding}

| Extensión de archivo de vídeo | Contenedor | Códecs de vídeo recomendados | Códecs de vídeo no compatibles |
| --- | --- | --- | --- |
| AVI | Intercalación A/V | XVID, DIVX, HDV, MiniDV (DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3 (IV30), MJPEG, Microsoft Video 1 (MS-CRAM) |
| FLV, F4V | Flash de Adobe | H264/AVC, Flix VP6, H263, Sorenson | SWF (archivos de animación vectoriales) |
| M4V | Apple iTunes | H264/AVC | - |
| MKV | Matroska | H264/AVC | - |
| MOV, QT | QuickTime de Apple | H264/AVC, Apple ProRes422 HQ, XDCAM de Sony, DVCAM de Sony, HDV, Panasonic DVCPro, Apple DV (DV25), Apple PhotoJPEG, Sorenson, Avid DNxHD, Avid AVR | Apple Intermedio, animación de Apple |
| MP4 | MPEG-4 | H264/AVC (todos los perfiles) | - |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 | - |
| MXF |  | Formato Media eXchange.<br>Apple ProRes422 | - |
| OGV, OGG | Ogg | Theora, VP3, Dirac | - |
| WebM | WebM | Google VP8 | - |
| WMV | Windows Media 9 | WMV3 (v9), WMV2 (v8), WMV1 (v7), GoToMeeting (G2M2, G2M3, G2M4) | Pantalla de Microsoft (MSS2), Microsoft Photo Story (WVP2) |

## Formatos de audio {#audio-formats}

[!DNL Assets] como [!DNL Cloud Service] proporciona compatibilidad con la extracción de metadatos XMP para los formatos de audio AIF, ASF, M4A, MP3, WAV y WMA.

## Formatos de entrada compatibles para la transcripción de audio y vídeo {#audio-video-transcription-formats}

* FLV (con códecs H.264 y AAC) (.flv)
* MXF (.mxf)
* MPEG2-PS, MPEG2-TS, 3GP (.ts, .ps, .3gp, .3gpp, .mpg)
* Vídeo de Windows Media (WMV)/ASF (.wmv, .asf)
* AVI (sin comprimir 8 bits/10 bits) (.avi)
* MP4 (.mp4, .m4a, .m4v)
* Grabación de vídeo digital de Microsoft (DVR-MS) (.dvr-ms)
* Matroska/WebM (.mkv)
* WAVE/WAV (.wav)
* QuickTime (.mov)

## Sugerencias y limitaciones {#limitations-and-tips}

* Actualmente, el límite de tamaño de archivo para la extracción de metadatos es de aproximadamente 15 GB. Al cargar recursos muy grandes, a veces se produce un error en la operación de extracción de metadatos.

>[!MORELIKETHIS]
>
>* [Procesamiento de recursos mediante microservicios de recursos](asset-microservices-overview.md)
>* [Formatos de archivo compatibles para el etiquetado inteligente de recursos basados en texto](/help/assets/smart-tags.md#smart-tags-supported-file-formats)

