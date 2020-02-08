---
title: Formatos de archivo y tipos MIME admitidos por Experience Manager Assets como servicio de nube
description: Formatos de archivo y tipos MIME admitidos por Experience Manager Assets como servicio de nube.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 776b089a322cc4f86fdcb9ddf1c3cc207fc85d39

---


# Formatos de archivo compatibles con los recursos {#supported-file-formats}

Adobe Experience Manager como servicio de nube admite funciones básicas de administración de contenido (almacenamiento, administración de metadatos en línea, creación de versiones, carga y descarga, etc.) para cualquier archivo binario, independientemente de su formato. Además, para los formatos de archivo más utilizados, como imagen, propiedad de Adobe, documento y vídeo, proporciona una mayor compatibilidad para generar vistas previas y representaciones y extraer metadatos y texto para indexar texto completo. Este apoyo ampliado se presta mediante [los microservicios](asset-microservices-configure-and-use.md)de activos.

Algunos aspectos destacados de los formatos de archivo con compatibilidad ampliada son:

* Formatos [de archivo clave de](#adobe-formats) Adobe producidos por aplicaciones y servicios de Adobe, incluidos Adobe Photoshop, InDesign, Illustrator, XD, Dimension y Acrobat/PDF.
* Formatos de archivo de [imágenes clave](#image-formats)
* [Formatos](#camera-raw-formats) de archivo RAW de cámara para una amplia gama de cámaras, incluidas Canon, Nikon, Fujifilm, Olympus y otros fabricantes (con tecnología Adobe Camera Raw)
* Formatos [comunes de](#document-formats)documento, incluidos los formatos [Microsoft Office](#microsoft-office-formats) (Word, Excel, PowerPoint) y [Open Document](#opendocument-formats)
* Amplia gama de formatos de [vídeo](#video-formats) y [audio](#audio-formats)

## Leyenda para obtener información detallada sobre asistencia {#legend-for-detailed-support-information}

La leyenda siguiente describe el nivel de compatibilidad con una función:

| Nivel de asistencia | Descripción |
| ------------------------------------------------------------ | --------------------------- |
| ✓ | Admitido |
| * | Véanse las observaciones que figuran a continuación del cuadro |
| - | No aplicable |

Las columnas de las tablas de soporte proporcionan la siguiente información:

| Columna | Descripción |
| ------------ | --------------------------------------------------------------- |
| Formato | Formato de archivo (extensión de archivo) del binario original del recurso |
| GIF | Formato GIF para la generación de representaciones |
| JPEG | Formato JPEG para la generación de representaciones |
| PNG | Formato PNG para la generación de representaciones |
| XMP | Extracción de metadatos del binario original |
| TXT | Extracción de texto del documento para indexar |
| Anchura/Altura | Compatibilidad para definir la anchura y la altura de una representación (píxeles) |

<!-- Adding this checkmark icon ✓ does not look good in table. The icon's shade and size has to be toned down for good readability and less clutter.
@gklebus: I suggest using a checkmark character, either U+2713 ✓ CHECK MARK or U+2714 ✔ HEAVY CHECK MARK
-->

## Formatos de Adobe {#adobe-formats}

| Formato de archivo | GIF | JPEG | PNG | TXT | XMP | Anchura/Altura |
| ----------- | --- | ---- | --- | --- | --- | ------------ |
| AI | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| COLLAGE | - | - | - | - | ✓ | - |
| DN | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| IDEAS | - | - | - | - | ✓ | - |
| INDD | ✓ | ✓ | ✓ | - | ✓ | ✓* |
| INDT | - | - | - | - | ✓ | - |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| PROTO | - | - | - | - | ✓ | - |
| PSB | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| PSD | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| XD | ✓ | ✓ | ✓ | - | ✓ | ✓ |

\* Para INDD (archivos de InDesign), el tamaño de la representación viene determinado por la vista previa incrustada en el archivo INDD. Configure las preferencias en InDesign (**[!UICONTROL Preferencias > Administración de archivos > Guardar siempre imágenes de vista previa con documentos, Tamaño]** de vista previa) para incrustar una representación más grande.

## Formatos de imagen {#image-formats}

| Formato de archivo | GIF | JPEG | PNG | XMP | Anchura/Altura |
| ----------- | --- | ---- | --- | --- | ------------ |
| BMP | ✓ | ✓ | ✓ | - | ✓ |
| EPS | - | - | - | ✓ | - |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| SVG | - | - | - | ✓ | - |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |


## Formatos RAW de cámara {#camera-raw-formats}

| Formato de archivo | GIF | JPEG | PNG | XMP | Anchura/Altura |
| ----------- | --- | ---- | --- | --- | ------------ |
| 3FR | ✓ | ✓ | ✓ | ✓ | ✓ |
| ARW | ✓ | ✓ | ✓ | ✓ | ✓ |
| CR2 | ✓ | ✓ | ✓ | ✓ | ✓ |
| CR3 | ✓ | ✓ | ✓ | ✓ | ✓ |
| CRW | ✓ | ✓ | ✓ | ✓ | ✓ |
| DCR | ✓ | ✓ | ✓ | ✓ | ✓ |
| DNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| FEDER | ✓ | ✓ | ✓ | ✓ | ✓ |
| FFF | ✓ | ✓ | ✓ | ✓ | ✓ |
| GPR | ✓ | ✓ | ✓ | ✓ | ✓ |
| IIQ | ✓ | ✓ | ✓ | ✓ | ✓ |
| KDC | ✓ | ✓ | ✓ | ✓ | ✓ |
| MEF | ✓ | ✓ | ✓ | ✓ | ✓ |
| MFW | ✓ | ✓ | ✓ | ✓ | ✓ |
| MOS | ✓ | ✓ | ✓ | ✓ | ✓ |
| MRW | ✓ | ✓ | ✓ | ✓ | ✓ |
| NEF | ✓ | ✓ | ✓ | ✓ | ✓ |
| NRW | ✓ | ✓ | ✓ | ✓ | ✓ |
| ORF | ✓ | ✓ | ✓ | ✓ | ✓ |
| PEF | ✓ | ✓ | ✓ | ✓ | ✓ |
| RAF | ✓ | ✓ | ✓ | ✓ | ✓ |
| RAW | ✓ | ✓ | ✓ | ✓ | ✓ |
| RW2 | ✓ | ✓ | ✓ | ✓ | ✓ |
| RWL | ✓ | ✓ | ✓ | ✓ | ✓ |
| SRF | ✓ | ✓ | ✓ | ✓ | ✓ |
| SRW | ✓ | ✓ | ✓ | ✓ | ✓ |
| X3F | ✓ | ✓ | ✓ | ✓ | ✓ |

## Formatos de documento {#document-formats}

| Formato de archivo | TXT | XMP |
| ----------- | --- | --- |
| EPUB | ✓ | - |
| HTML | ✓ | - |
| PS | - | ✓ |
| RTF | ✓ | - |
| TEXTO | ✓ | - |
| XML | ✓ | - |

## Formatos de Microsoft Office {#microsoft-office-formats}

| Formato de archivo | GIF | JPEG | PNG | TEXTO | Anchura/Altura |
| ----------- | --- | ---- | --- | ---- | ------------ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ |

## Formatos OpenDocument {#opendocument-formats}

| Formato de archivo | GIF | JPEG | PNG | TEXTO | Altura |
| ----------- | --- | ---- | --- | ---- | ------ |
| ODF | ✓ | ✓ | ✓ | ✓ | ✓ |
| OFG | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODM | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODP | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODS | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODT | ✓ | ✓ | ✓ | ✓ | ✓ |

## Formatos de vídeo {#video-formats}

| Formato de archivo | GIF | JPEG | PNG | XMP | Anchura/Altura |
| ----------- | --- | ---- | --- | --- | ------------ |
| 3G2 | - | - | - | ✓ | - |
| 3GP | - | - | - | ✓ | - |
| AVI | ✓ | ✓ | ✓ | ✓ | ✓ |
| DIVX | ✓ | ✓ | ✓ |  | ✓ |
| F4V | ✓ | ✓ | ✓ | ✓ | ✓ |
| FLV | ✓ | ✓ | ✓ | ✓ | ✓ |
| M2T | ✓ | ✓ | ✓ | - | ✓ |
| M2TS | ✓ | ✓ | ✓ | - | ✓ |
| M2V | ✓ | ✓ | ✓ | - | ✓ |
| M4V | ✓ | ✓ | ✓ | ✓ | ✓ |
| MKV | ✓ | ✓ | ✓ | - | ✓ |
| MOV | ✓ | ✓ | ✓ | ✓ | ✓ |
| MP4 | ✓ | ✓ | ✓ | ✓ | ✓ |
| MPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| MPG | ✓ | ✓ | ✓ | ✓ | ✓ |
| MTS | ✓ | ✓ | ✓ | - | ✓ |
| OGV | ✓ | ✓ | ✓ | - | ✓ |
| QT | ✓ | ✓ | ✓ | - | ✓ |
| R3D | ✓ | ✓ | ✓ | - | ✓ |
| SWF | ✓ | ✓ | ✓ | - | ✓ |
| WEBM | ✓ | ✓ | ✓ | - | ✓ |
| WMV | ✓ | ✓ | ✓ | ✓ | ✓ |

## Formatos de audio {#audio-formats}

Assets as a Cloud Service ofrece compatibilidad con XMP para estos formatos de audio: AIF, ASF, M4A, MP3, WAV y WMA.

<!-- TBD: Some items from https://helpx.adobe.com/experience-manager/6-5/assets/using/assets-formats.html#SupportedinputvideoformatsforDynamicMediatranscoding may be applicable.

Bring more parity with https://helpx.adobe.com/experience-manager/6-5/assets/using/assets-formats.html#SupportedMIMEtypes.
https://helpx.adobe.com/experience-manager/6-5/assets/using/assets-formats.html#Supportedmultimediaformats
-->

>[!MORELIKETHIS]
>
>* [Procesamiento de recursos mediante microservicios de recursos](asset-microservices-overview.md)

