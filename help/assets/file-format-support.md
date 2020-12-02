---
title: Formatos de archivo y tipos MIME admitidos
description: Formatos de archivo y tipos MIME admitidos por [!DNL Experience Manager Assets] como Cloud Service.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 7e5ea5ccf0110d1fb55449c9c1933aff6aba0065
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 10%

---


# [!DNL Assets] formatos de archivo admitidos  {#supported-file-formats}

[!DNL Adobe Experience Manager] como Cloud Service admite funciones básicas de gestor de contenido: almacenamiento, administración de metadatos en línea, creación de versiones, carga y descarga, etc. — para cualquier archivo binario, independientemente de su formato. [!DNL Adobe Experience Manager Assets] admite una amplia gama de formatos de archivo y cada función de producto admite distintos formatos.

Además, [!DNL Experience Manager Assets] proporciona soporte ampliado para generar previsualizaciones y representaciones y extraer metadatos y texto para indexar texto completo. Este soporte ampliado se proporciona mediante [microservicios de recursos](asset-microservices-configure-and-use.md).

Los aspectos destacados de la conversión de recursos mediante los microservicios de recursos son:

* Formatos de archivo clave [Adobe](#adobe-formats) producidos por aplicaciones y servicios de Adobe, incluidos [!DNL Adobe Photoshop], [!DNL Adobe InDesign], [!DNL Adobe Illustrator], [!DNL Adobe XD], [!DNL Adobe Dimension] y [!DNL Adobe Acrobat] o PDF.
* Formatos de archivo de imágenes [clave](#image-formats).
* [Camera Raw ](#camera-raw-formats) formatos de archivo para una amplia gama de cámaras, incluyendo Canon, Nikon, Fujifilm, Olympus y otros fabricantes (con tecnología Adobe Camera Raw).
* Formatos comunes de [documento](#document-formats), incluidos los formatos de Microsoft Office y Documento abierto.
* Amplia gama de formatos de [vídeo](#video-formats) y [audio.](#audio-formats)

La leyenda siguiente describe el nivel de asistencia.

| Nivel de asistencia | Descripción |
| ------------- | --------------------------- |
| xib | Compatible |
| * | Véanse las observaciones que figuran a continuación del cuadro |
| - | No aplicable |

## Formatos de Adobe {#adobe-formats}

| Formato de archivo | Generación de miniaturas | Extracción de texto completo | Extracción de metadatos | Anchura/Altura |
| ----------- | -------------------- | ------------------- | ------------------- | ------------ |
| AI | xib | - | xib | xib |
| COLLAGE | - | - | xib | - |
| DN | xib | - | xib | xib |
| IDEAS | - | - | xib | - |
| INDD | xib | - | xib | xib |
| INDT | - | - | xib | - |
| PDF | xib | xib | xib | xib |
| PROTO | - | - | xib | - |
| PSB | xib | - | xib | xib |
| PSD | xib | - | xib | xib |
| XD | xib | - | xib | xib |

\* Para archivos [!DNL Adobe InDesign] (INDD), el tamaño de la representación viene determinado por la previsualización incrustada en el archivo INDD. Configure las preferencias en [!DNL InDesign] (**[!UICONTROL Preferencias > Administración de archivos > Guardar siempre imágenes de Previsualización con Documentos, Tamaño de Previsualización]**) para incrustar una representación más grande.

## Formatos de imagen {#image-formats}

| Formato de archivo | Generación de miniaturas | Extracción de metadatos | Anchura/Altura | Recortar |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | xib | - | xib | xib |
| EPS | - | xib | - | - |
| GIF | xib | xib | xib | xib |
| JPEG | xib | xib | xib | xib |
| PNG | xib | xib | xib | xib |
| TIFF | xib | xib | xib | - |
| SVG | xib | - | xib | xib |
| SGI | xib | xib | xib | xib |
| RGB | xib | xib | xib | xib |
| RGBA | xib | xib | xib | xib |

## Formatos de imagen en [!DNL Dynamic Media] {#image-support-dynamic-media}

| Formato | Cargar (formato de entrada) | Creación de ajustes preestablecidos de imagen (formato de salida) | Representación dinámica de previsualización | Entregar representación dinámica | Descargar representación dinámica |
| ------- | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| PNG | xib | xib | xib | xib | xib |
| GIF | xib | xib | xib | xib | xib |
| TIFF | xib | xib | xib | xib | xib |
| JPEG | xib | xib | xib | xib | xib |
| BMP | xib | - | - | - | - |
| PSD   answer | xib | - | - | - | - |
| EPS | xib | xib | xib | xib | xib |
| PICT | xib | - | - | - | - |

† La imagen combinada se extrae del archivo PSD. Es una imagen generada por [!DNL Adobe Photoshop] y que se incluye en el archivo PSD. Según la configuración, la imagen combinada puede ser o no la imagen real.

Los siguientes subtipos de formatos de archivo de imagen rasterizada que no se admiten en [!DNL Dynamic Media]:

* Archivos PNG con un tamaño de fragmento IDAT bueno de 100 MB.
* Archivos PSB.
* Los archivos PSD con un espacio de color distinto de CMYK, RGB, escala de grises o mapa de bits no son compatibles. No se admiten los espacios de color DuoTone, Lab e Indexed.
* Archivos PSD con una profundidad buena de 16.
* Archivos TIFF que tienen datos de coma flotante.
* Archivos TIFF que tienen espacio de color Lab.

## Formatos 3D {#support-3d-formats}

Se admite la siguiente lista de formatos 3D.

Consulte también [Uso de recursos 3D en Dynamic Media.](/help/assets/dynamic-media/assets-3d.md)

| Formato | Almacenamiento | Versiones | Flujo de trabajo | Publicación | Control de acceso | Previsualización de miniaturas | previsualización 3D | Envío de Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | xib | xib | xib | - | xib | xib | - | - |
| gLB | xib | xib | xib | xib | xib | - | xib | xib |
| gLTF | xib | xib | xib | - | xib | - | xib | - |
| OBJ | xib | xib | xib | xib | xib | - | xib | xib |
| STL | xib | xib | xib | xib | xib | - | xib | xib |
| USDz | xib | xib | xib | xib | xib | - | - | xib |

## [!DNL Camera RAW] formatos  {#camera-raw-formats}

| Formato de archivo | Generación de miniaturas | Extracción de metadatos | Anchura/Altura |
| ----------- | -------------------- | ------------------- | ------------ |
| 3FR | xib | xib | xib |
| ARW | xib | xib | xib |
| CR2 | xib | xib | xib |
| CR3 | xib | xib | xib |
| CRW | xib | xib | xib |
| DCR | xib | xib | xib |
| DNG | xib | xib | xib |
| FEDER | xib | xib | xib |
| FFF | xib | xib | xib |
| GPR | xib | xib | xib |
| IIQ | xib | xib | xib |
| KDC | xib | xib | xib |
| MEF | xib | xib | xib |
| MFW | xib | xib | xib |
| MOS | xib | xib | xib |
| MRW | xib | xib | xib |
| NEF | xib | xib | xib |
| NRW | xib | xib | xib |
| ORF | xib | xib | xib |
| PEF | xib | xib | xib |
| RAF | xib | xib | xib |
| RAW | xib | xib | xib |
| RW2 | xib | xib | xib |
| RWL | xib | xib | xib |
| SRF | xib | xib | xib |
| SRW | xib | xib | xib |
| X3F | xib | xib | xib |

## Formatos de documento {#document-formats}

Los formatos de documento admitidos para las funciones de administración de recursos son los siguientes.

| Formato de archivo | Generación de miniaturas | Extracción de texto completo | Anchura/Altura | Gestión de metadatos | [Recursos conectados](use-assets-across-connected-assets-instances.md) |
| ----------- | -------------------- | ------------------- | ------------ | ------------------- | ---------------- |
| PDF | xib | xib | xib | xib | xib |
| DOCX | xib | xib | xib | xib | xib |
| DOC | - | - | - | xib | xib |
| PPTX | xib | xib | xib | xib | xib |
| PPT | - | - | - | xib | xib |
| XLSX | xib | xib | xib | xib | xib |
| XLS | - | - | - | xib | xib |
| ODF | xib | xib | xib | - | - |
| OFG | xib | xib | xib | - | - |
| ODM | xib | xib | xib | - | - |
| ODP | xib | xib | xib | - | - |
| ODS | xib | xib | xib | - | - |
| ODT | xib | xib | xib | xib | xib |
| EPUB | - | xib | - | - | - |
| HTML | - | xib | - | xib | xib |
| PS | - | - | xib | - | - |
| RTF | - | xib | - | xib | xib |
| TXT | - | xib | - | xib | xib |
| XML | - | xib | - | - | - |

## Formatos de documento en [!DNL Dynamic Media] {#document-support-dynamic-media}

| Formato | Cargar (formato de entrada) | Creación de ajustes preestablecidos de imagen (formato de salida) | Representación dinámica de previsualización | Entregar representación dinámica | Descargar representación dinámica |
| ------ | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| AI | xib | - | - | - | - |
| PDF | xib | xib | xib | xib | xib |
| INDD | xib | - | - | - | - |

## Formatos de vídeo {#video-formats}

| Formato de archivo | Generación de miniaturas | Extracción de metadatos | Anchura/Altura |
| ----------- | -------------------- | ------------------- | ------------ |
| 3G2 | - | xib | - |
| 3GP | - | xib | - |
| AVI | xib | xib | xib |
| DIVX | xib | - | xib |
| F4V | xib | xib | xib |
| FLV | xib | xib | xib |
| M2T | xib | - | xib |
| M2TS | xib | - | xib |
| M2V | xib | - | xib |
| M4V | xib | xib | xib |
| MKV | xib | - | xib |
| MOV | xib | xib | xib |
| MP4 | xib | xib | xib |
| MPEG | xib | xib | xib |
| MPG | xib | xib | xib |
| MTS | xib | - | xib |
| OGV | xib | - | xib |
| QT | xib | - | xib |
| R3D | - | xib | xib |
| SWF | xib | - | xib |
| WebM | xib | - | xib |
| WMV | xib | xib | xib |

## Formatos de vídeo en [!DNL Dynamic Media] para la transcodificación {#video-dynamic-media-transcoding}

| Extensión de archivo de vídeo | Contenedor | Códecs de vídeo recomendados | Códecs de vídeo no compatibles |
|------------------------|--------------------|--------|-------|
| MP4 | MPEG-4 | H264/AVC (todos los perfiles) | - |
| MOV, QT | Apple QuickTime | H264/AVC, Apple ProRes422 y HQ, XDCAM de Sony, DVCAM de Sony, HDV, Panasonic DVCPro, Apple DV (DV25), Apple PhotoJPEG, Sorenson, Avid DNxHD, Avid AVR | Apple Intermediate, animación de Apple |
| FLV, F4V | Flash Adobe | H264/AVC, Flix VP6, H263, Sorenson | SWF (archivos de animación vectorial) |
| WMV | Windows Media 9 | WMV3 (v9), WMV2 (v8), WMV1 (v7), GoToMeeting (G2M2, G2M3, G2M4) | Microsoft Screen (MSS2), Microsoft Photo Story (WVP2) |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 | - |
| M4V | Apple iTunes | H264/AVC | - |
| AVI | Intercalación A/V | XVID, DIVX, HDV, MiniDV (DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3 (IV30), MJPEG, Microsoft Video 1 (MS-CRAM) |
| WebM | WebM | Google VP8 | - |
| OGV, OGG | Ogg | Theora, VP3, Dirac | - |
| MXF | MXF | Sony XDCAM, MPEG-2, MPEG-4, Panasonic DVCPro | - |
| MTS | AVCHD | H264/AVC | - |
| MKV | Matroska | H264/AVC | - |
| R3D, RM | Vídeo rojo sin formato | MJPEG 2000 | - |
| RAM, RM | RealVideo | No admitido | Real G2 (RV20), Real 8 (RV30), Real 10 (RV40) |
| FLAC | Flac nativo | Códec de audio sin pérdida gratuito | - |
| MJ2 | Motion JPEG 2000 | Códec Motion JPEG 2000 | - |

## Formatos de audio {#audio-formats}

[!DNL Assets] como Cloud Service proporciona compatibilidad con la extracción de metadatos XMP para los formatos de audio AIF, ASF, M4A, MP3, WAV y WMA.

>[!MORELIKETHIS]
>
>* [Procesamiento de recursos mediante microservicios de recursos](asset-microservices-overview.md)

