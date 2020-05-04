---
title: Formatos de archivo y tipos MIME admitidos por Experience Manager Assets como servicio de nube
description: Formatos de archivo y tipos MIME admitidos por Experience Manager Assets como servicio de nube.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 2e73a9bba91f15702bdeb1d57e87b688360661bd

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

### Formatos de Adobe {#adobe-formats}

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

\* Para INDD (archivos de InDesign), el tamaño de la representación viene determinado por la previsualización incrustada en el archivo INDD. Configure las preferencias en InDesign (**[!UICONTROL Preferencias > Administración de archivos > Guardar siempre imágenes de Previsualización con Documentos, Tamaño]** de Previsualización) para incrustar una representación más grande.

### Formatos de imagen {#image-formats}

| Formato de archivo | Generación de miniaturas | Extracción de metadatos | Anchura/Altura | Recortar |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | ✓ | - | ✓ | ✓ |
| EPS | - | ✓ | - | - |
| GIF | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ |
| SVG | - | ✓ | - | - |
| TIFF | ✓ | ✓ | ✓ | - |

### Formatos RAW de cámara {#camera-raw-formats}

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

### Formatos de Documento {#document-formats}

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

### Formatos de vídeo {#video-formats}

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

### Formatos de audio {#audio-formats}

Assets as a Cloud Service ofrece compatibilidad con la extracción de metadatos XMP para los formatos de audio AIF, ASF, M4A, MP3, WAV y WMA.

>[!MORELIKETHIS]
>
>* [Procesamiento de recursos mediante microservicios de recursos](asset-microservices-overview.md)

