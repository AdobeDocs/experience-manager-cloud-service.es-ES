---
title: Formatos de archivo y tipos MIME admitidos por Experience Manager Assets como servicio de nube
description: Formatos de archivo y tipos MIME admitidos por Experience Manager Assets como servicio de nube.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0686acbc61b3902c6c926eaa6424828db0a6421a

---


# Assets supported file formats {#supported-file-formats}

Adobe Experience Manager como servicio de nube admite funciones básicas de gestor de contenido — almacenamiento, administración de metadatos en línea, creación de versiones, carga y descarga, etc. — para cualquier archivo binario, independientemente de su formato. Recursos Adobe Experience Manager admite una amplia gama de formatos de archivo y cada función de producto admite distintos formatos.

Además, Experience Manager Assets ofrece una compatibilidad ampliada para generar previsualizaciones y representaciones, así como para extraer metadatos y texto para la indexación de texto completo. Este apoyo ampliado se presta mediante [los microservicios](asset-microservices-configure-and-use.md)de activos.

La leyenda siguiente describe el nivel de asistencia.

| Nivel de asistencia | Descripción |
| ------------- | --------------------------- |
| ✓ | Compatible |
| * | Véanse las observaciones que figuran a continuación del cuadro |
| - | No aplicable |

## Conversión de recursos mediante microservicios de recursos {#asset-microservices-supported-formats}

Los aspectos más destacados incluyen:

* Formatos [de archivo clave de](#adobe-formats) Adobe producidos por aplicaciones y servicios de Adobe, incluidos Adobe Photoshop, Adobe InDesign, Adobe Illustrator, Adobe XD, Adobe Dimension y Adobe Acrobat o PDF.
* Formatos [de archivo de](#image-formats)imágenes clave.
* [Formatos](#camera-raw-formats) de archivo de Camera Raw para una amplia gama de cámaras, incluidas Canon, Nikon, Fujifilm, Olympus y otros fabricantes (con tecnología Adobe Camera Raw).
* Formatos [de](#document-formats)documento comunes, incluidos los formatos Microsoft Office y Open Documento.
* Amplia gama de formatos de [vídeo](#video-formats) y [audio.](#audio-formats)

Las columnas de las siguientes tablas proporcionan la siguiente información:

| Columna | Descripción |
| ------------ | --------------------------------------------------------------- |
| Formato | Formato de archivo (extensión de archivo) del binario original del recurso. |
| GIF | Formato GIF para la generación de representaciones. |
| JPEG | Formato JPEG para la generación de representaciones. |
| PNG | Formato PNG para la generación de representaciones. |
| Anchura/Altura | Compatibilidad para definir la anchura y la altura de una representación en píxeles. |

### Formatos de Adobe {#adobe-formats}

| Formato de archivo | GIF | JPEG | PNG | extracción de texto completo | Extracción de metadatos | Anchura/Altura |
| ----------- | -------- | -------- | -------- | ------------------- | ------------------- | ------------ |
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

\* Para INDD (archivos de InDesign), el tamaño de la representación viene determinado por la previsualización incrustada en el archivo INDD. Configure las preferencias en InDesign (**[!UICONTROL Preferencias > Administración de archivos > Guardar siempre imágenes de Previsualización con Documentos, Tamaño]** de Previsualización) para incrustar una representación más grande.

### Formatos de imagen {#image-formats}

| Formato de archivo | GIF | JPEG | PNG | Extracción de metadatos | Anchura/Altura |
| ----------- | -------- | -------- | -------- | ------------------- | ------------ |
| BMP | ✓ | ✓ | ✓ | - | ✓ |
| EPS | - | - | - | ✓ | - |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| SVG | - | - | - | ✓ | - |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |

### Formatos RAW de cámara {#camera-raw-formats}

| Formato de archivo | GIF | JPEG | PNG | Extracción de metadatos | Anchura/Altura |
| ----------- | -------- | -------- | -------- | ------------------- | ------------ |
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

### Formatos de Documento {#document-formats}

Los formatos de documento admitidos para las funciones de administración de recursos son los siguientes.

|  | GIF | JPEG | PNG | extracción de texto completo | Anchura/Altura | Gestión de metadatos | [Recursos conectados](use-assets-across-connected-assets-instances.md) |
| ---- | -------- | -------- | -------- | ------------------- | ------------ | ------------------- | ---------------- |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| DOC | - | - | - | - | - | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| PPT | - | - | - | - | - | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XLS | - | - | - | - | - | ✓ | ✓ |
| ODF | ✓ | ✓ | ✓ | ✓ | ✓ | - | - |
| OFG | ✓ | ✓ | ✓ | ✓ | ✓ | - | - |
| ODM | ✓ | ✓ | ✓ | ✓ | ✓ | - | - |
| ODP | ✓ | ✓ | ✓ | ✓ | ✓ | - | - |
| ODS | ✓ | ✓ | ✓ | ✓ | ✓ | - | - |
| ODT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| EPUB | - | - | - | ✓ | - | - | - |
| HTML | - | - | - | ✓ | - | ✓ | ✓ |
| PS | - | - | - | - | ✓ | - | - |
| RTF | - | - | - | ✓ | - | ✓ | ✓ |
| TXT | - | - | - | ✓ | - | ✓ | ✓ |
| XML | - | - | - | ✓ | - | - | - |

### Formatos de vídeo {#video-formats}

| Formato de archivo | GIF | JPEG | PNG | Extracción de metadatos | Anchura/Altura |
| ----------- | -------- | -------- | -------- | ------------------- | ------------ |
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

### Formatos de audio {#audio-formats}

Assets as a Cloud Service ofrece compatibilidad con la extracción de metadatos XMP para los formatos de audio AIF, ASF, M4A, MP3, WAV y WMA.

>[!MORELIKETHIS]
>
>* [Procesamiento de recursos mediante microservicios de recursos](asset-microservices-overview.md)

