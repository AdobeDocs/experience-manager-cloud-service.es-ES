---
title: Formatos de archivo y tipos MIME admitidos por Experience Manager Assets como servicio de nube
description: Formatos de archivo y tipos MIME admitidos por Experience Manager Assets como servicio de nube.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 2830c1cb2a9a0c06e6f8a4a765420706f5ceb093
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 9%

---


# Assets supported file formats {#supported-file-formats}

Adobe Experience Manager como servicio de nube admite funciones básicas de gestor de contenido — almacenamiento, administración de metadatos en línea, creación de versiones, carga y descarga, etc. — para cualquier archivo binario, independientemente de su formato. Recursos Adobe Experience Manager admite una amplia gama de formatos de archivo y cada función de producto admite distintos formatos.

Además, Experience Manager Assets ofrece una compatibilidad ampliada para generar previsualizaciones y representaciones, así como para extraer metadatos y texto para la indexación de texto completo. Este apoyo ampliado se presta mediante [los microservicios](asset-microservices-configure-and-use.md)de activos.

Los aspectos destacados de la conversión de recursos mediante los microservicios de recursos son:

* Formatos [de archivo clave de](#adobe-formats) Adobe producidos por aplicaciones y servicios de Adobe, incluidos Adobe Photoshop, Adobe InDesign, Adobe Illustrator, Adobe XD, Adobe Dimension y Adobe Acrobat o PDF.
* Formatos [de archivo de](#image-formats)imágenes clave.
* [Formatos](#camera-raw-formats) de archivo de Camera Raw para una amplia gama de cámaras, incluidas Canon, Nikon, Fujifilm, Olympus y otros fabricantes (con tecnología Adobe Camera Raw).
* Formatos [de](#document-formats)documento comunes, incluidos los formatos Microsoft Office y Open Documento.
* Amplia gama de formatos de [vídeo](#video-formats) y [audio.](#audio-formats)

La leyenda siguiente describe el nivel de asistencia.

| Nivel de asistencia | Descripción |
| ------------- | --------------------------- |
| ✓ | Compatible |
| * | Véanse las observaciones que figuran a continuación del cuadro |
| - | No aplicable |

## Formatos de Adobe {#adobe-formats}

| Formato de archivo | Generación de miniaturas | extracción de texto completo | Extracción de metadatos | Anchura/Altura |
| ----------- | -------------------- | ------------------- | ------------------- | ------------ |
| AI | ✓ | - | ✓ | ✓ |
| COLLAGE | - | - | ✓ | - |
| DN | ✓ |  | ✓ | ✓ |
| IDEAS | - | - | ✓ | - |
| INDD | ✓ | - | ✓ | ✓ * |
| INDT | - | - | ✓ | - |
| PDF | ✓ | ✓ | ✓ | ✓ |
| PROTO | - | - | ✓ | - |
| PSB | ✓ | - | ✓ | ✓ |
| PSD | ✓ | - | ✓ | ✓ |
| XD | ✓ | - | ✓ | ✓ |

\* Para [!DNL Adobe InDesign] archivos (INDD), el tamaño de la representación viene determinado por la previsualización incrustada en el archivo INDD. Configure las preferencias en [!DNL InDesign] (**[!UICONTROL Preferencias > Administración de archivos > Guardar siempre imágenes de Previsualización con Documentos, Tamaño]** de Previsualización) para incrustar una representación más grande.

## Formatos de imagen {#image-formats}

| Formato de archivo | Generación de miniaturas | Extracción de metadatos | Anchura/Altura | Recortar |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | ✓ | - | ✓ | ✓ |
| EPS | - | ✓ | - | - |
| GIF | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ |
| SVG | - | ✓ | - | - |
| TIFF | ✓ | ✓ | ✓ | - |

## Formatos de imagen en [!DNL Dynamic Media] {#image-support-dynamic-media}

| Formato | Cargar (formato de entrada) | Creación de ajustes preestablecidos de imagen (formato de salida) | Representación dinámica de Previsualización | Entregar representación dinámica | Descargar representación dinámica |
| ------- | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | - | - | - | - |
| PSD* | ✓ | - | - | - | - |
| EPS | ✓ | ✓ | ✓ | ✓ | ✓ |
| PICT | ✓ | - | - | - | - |

† La imagen combinada se extrae del archivo PSD. Es una imagen generada por [!DNL Adobe Photoshop] y incluida en el archivo PSD. Según la configuración, la imagen combinada puede ser o no la imagen real.

Los siguientes subtipos de formatos de archivo de imagen rasterizada que no se admiten en [!DNL Dynamic Media]:

* Archivos PNG con un tamaño de fragmento IDAT bueno de 100 MB.
* Archivos PSB.
* Los archivos PSD con un espacio de color distinto de CMYK, RGB, escala de grises o mapa de bits no son compatibles. No se admiten los espacios de color DuoTone, Lab e Indexed.
* Archivos PSD con una profundidad buena de 16.
* Archivos TIFF que tienen datos de coma flotante.
* Archivos TIFF que tienen espacio de color Lab.

## [!DNL Camera RAW] formatos {#camera-raw-formats}

| Formato de archivo | Generación de miniaturas | Extracción de metadatos | Anchura/Altura |
| ----------- | -------------------- | ------------------- | ------------ |
| 3FR | ✓ | ✓ | ✓ |
| ARW | ✓ | ✓ | ✓ |
| CR2 | ✓ | ✓ | ✓ |
| CR3 | ✓ | ✓ | ✓ |
| CRW | ✓ | ✓ | ✓ |
| DCR | ✓ | ✓ | ✓ |
| DNG | ✓ | ✓ | ✓ |
| FEDER | ✓ | ✓ | ✓ |
| FFF | ✓ | ✓ | ✓ |
| GPR | ✓ | ✓ | ✓ |
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

## Formatos de Documento {#document-formats}

Los formatos de documento admitidos para las funciones de administración de recursos son los siguientes.

| Formato de archivo | Generación de miniaturas | extracción de texto completo | Anchura/Altura | Gestión de metadatos | [Recursos conectados](use-assets-across-connected-assets-instances.md) |
| ----------- | -------------------- | ------------------- | ------------ | ------------------- | ---------------- |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ |
| DOC | - | - | - | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ |
| PPT | - | - | - | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ |
| XLS | - | - | - | ✓ | ✓ |
| ODF | ✓ | ✓ | ✓ | - | - |
| OFG | ✓ | ✓ | ✓ | - | - |
| ODM | ✓ | ✓ | ✓ | - | - |
| ODP | ✓ | ✓ | ✓ | - | - |
| ODS | ✓ | ✓ | ✓ | - | - |
| ODT | ✓ | ✓ | ✓ | ✓ | ✓ |
| EPUB | - | ✓ | - | - | - |
| HTML | - | ✓ | - | ✓ | ✓ |
| PS | - | - | ✓ | - | - |
| RTF | - | ✓ | - | ✓ | ✓ |
| TXT | - | ✓ | - | ✓ | ✓ |
| XML | - | ✓ | - | - | - |

## Formatos de Documento en [!DNL Dynamic Media] {#document-support-dynamic-media}

| Formato | Cargar (formato de entrada) | Creación de ajustes preestablecidos de imagen (formato de salida) | Representación dinámica de Previsualización | Entregar representación dinámica | Descargar representación dinámica |
| ------ | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| AI | ✓ | - | - | - | - |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ |
| INDD | ✓ | - | - | - | - |

## Formatos de vídeo {#video-formats}

| Formato de archivo | Generación de miniaturas | Extracción de metadatos | Anchura/Altura |
| ----------- | -------------------- | ------------------- | ------------ |
| 3G2 | - | ✓ | - |
| 3GP | - | ✓ | - |
| AVI | ✓ | ✓ | ✓ |
| DIVX | ✓ |  | ✓ |
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
| OGV | ✓ | - | ✓ |
| QT | ✓ | - | ✓ |
| R3D | ✓ | - | ✓ |
| SWF | ✓ | - | ✓ |
| WEBM | ✓ | - | ✓ |
| WMV | ✓ | ✓ | ✓ |

## Formatos de vídeo para [!DNL Dynamic Media] transcodificación {#video-dynamic-media-transcoding}

| Extensión de archivo de vídeo | Contenedor | Códecs de vídeo recomendados | Códecs de vídeo no compatibles |
|------------------------|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| MP4 | MPEG-4 | H264/AVC (todos los perfiles) |  |
| MOV, QT | Apple QuickTime | H264/AVC, Apple ProRes422 y HQ, XDCAM de Sony, DVCAM de Sony, HDV, Panasonic DVCPro, Apple DV (DV25), Apple PhotoJPEG, Sorenson, Avid DNxHD, Avid AVR | Apple Intermediate, animación de Apple |
| FLV, F4V | Adobe Flash | H264/AVC, Flix VP6, H263, Sorenson | SWF (archivos de animación vectorial) |
| WMV | Windows Media 9 | WMV3 (v9), WMV2 (v8), WMV1 (v7), GoToMeeting (G2M2, G2M3, G2M4) | Microsoft Screen (MSS2), Microsoft Photo Story (WVP2) |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 |  |
| M4V | Apple iTunes | H264/AVC |  |
| AVI | Intercalación A/V | XVID, DIVX, HDV, MiniDV (DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3 (IV30), MJPEG, Microsoft Video 1 (MS-CRAM) |
| WebM | WebM | Google VP8 |  |
| OGV, OGG | Ogg | Theora, VP3, Dirac |  |
| MXF | MXF | Sony XDCAM, MPEG-2, MPEG-4, Panasonic DVCPro |  |
| MTS | AVCHD | H264/AVC |  |
| MKV | Matroska | H264/AVC |  |
| R3D, RM | Vídeo rojo sin formato | MJPEG 2000 |  |
| RAM, RM | RealVideo | No admitido | Real G2 (RV20), Real 8 (RV30), Real 10 (RV40) |
| FLAC | Flac nativo | Códec de audio sin pérdida gratuito |  |
| MJ2 | Motion JPEG 2000 | Códec Motion JPEG 2000 |  |

## Formatos de audio {#audio-formats}

Assets as a Cloud Service ofrece compatibilidad con la extracción de metadatos XMP para los formatos de audio AIF, ASF, M4A, MP3, WAV y WMA.

>[!MORELIKETHIS]
>
>* [Procesamiento de recursos mediante microservicios de recursos](asset-microservices-overview.md)

