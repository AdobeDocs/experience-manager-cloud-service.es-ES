---
title: Formatos de archivo y tipos MIME admitidos
description: Formatos de archivo y tipos MIME admitidos por  [!DNL Experience Manager Assets] as a [!DNL Cloud Service].
contentOwner: AG
feature: Asset Management, Renditions
role: User, Admin
exl-id: e848aa77-7829-4adc-8b88-0279791a4525
source-git-commit: 0129bf13301a208b777b61f65623222cdf2b4b18
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 10%

---

# [!DNL Assets] formatos de archivo compatibles {#supported-file-formats}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] admite funciones básicas de administración de contenido (almacenamiento, administración de metadatos en línea, versiones, carga y descarga, etc.) para cualquier archivo binario, independientemente de su formato. [!DNL Adobe Experience Manager Assets] admite una amplia gama de formatos de archivo y cada característica del producto tiene compatibilidad variada con diferentes formatos.

Además, [!DNL Experience Manager Assets] proporciona compatibilidad ampliada para generar vistas previas y representaciones, así como para extraer metadatos y texto para la indización de texto completo. Esta compatibilidad ampliada se proporciona mediante [microservicios de recursos](asset-microservices-configure-and-use.md).

Los aspectos destacados de la conversión de recursos mediante microservicios de recursos son:

* Los [formatos de archivo Adobe](#adobe-formats) clave producidos por aplicaciones y servicios de Adobe, incluidos [!DNL Adobe Photoshop], [!DNL Adobe InDesign], [!DNL Adobe Illustrator], [!DNL Adobe XD], [!DNL Adobe Dimension] y [!DNL Adobe Acrobat] o PDF.
* Clave [formatos de archivo de imagen](#image-formats).
* [Formatos de archivo Camera Raw](#camera-raw-formats) para una amplia gama de cámaras, entre ellas Canon, Nikon, Fujifilm, Olympus y otros fabricantes (con tecnología Adobe Camera Raw).
* [formatos de documento comunes](#document-formats), incluidos los formatos Microsoft® Office y Open Document.
* Amplio rango de formatos de [vídeo](#video-formats) y [audio](#audio-formats).

La siguiente leyenda describe el nivel de compatibilidad con cada formato.

| Niveles de soporte | Descripción |
| ------------- | --------------------------- |
| ✓ | Compatible |
| * | Véanse las observaciones que figuran debajo del cuadro |
| - | No aplicable |

>[!IMPORTANT]
>
>[!DNL Adobe Experience Manager Assets] solo admite los formatos de archivo enumerados en este artículo.
>>Algunas funciones pueden parecer compatibles con otros formatos, pero estos formatos no son compatibles oficialmente. Los resultados pueden ser incoherentes y es posible que las funciones no funcionen según lo esperado.
>>Para garantizar resultados coherentes y fiables, utilice únicamente los formatos admitidos.

## Formatos de Adobe {#adobe-formats}

| Formato del archivo | Generación de miniaturas | Extracción de texto completo | Extracción de metadatos | Anchura/Altura |
| ----------- | -------------------- | ------------------- | ------------------- | ------------ |
| IA | ✓ | - | ✓ | ✓ |
| COLLAGE | - | - | ✓ | - |
| DN | ✓ | - | ✓ | ✓ |
| SBSAR | ✓ | - | ✓ | ✓ |
| IDEAS | - | - | ✓ | - |
| INDD | ✓ | - | ✓ | ✓ * |
| INDT | - | - | ✓ | - |
| PDF | ✓ | ✓ | ✓ | ✓ |
| PROTO | - | - | ✓ | - |
| PSB | ✓ | - | ✓ | ✓ |
| PSD | ✓ | - | ✓ | ✓ |
| XD | ✓ | - | ✓ | ✓ |

\* Para [!DNL Adobe InDesign] archivos (INDD), el tamaño de las representaciones viene determinado por la vista previa incrustada en el archivo INDD. Configure las preferencias en [!DNL InDesign] (**[!UICONTROL Preferencias > Administración de archivos > Guardar siempre imágenes de vista previa con documentos, Tamaño de vista previa]**) para que pueda incrustar representaciones más grandes.

## Formatos de imagen {#image-formats}

| Formato del archivo | Generación de miniaturas | Extracción de metadatos | Anchura/Altura | Recortar |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | ✓ | - | ✓ | ✓ |
| EPS | ✓ | ✓ | - | - |
| GIF | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ |
| RGB | ✓ | ✓ | ✓ | ✓ |
| RGBA | ✓ | ✓ | ✓ | ✓ |
| SGI™ | ✓ | ✓ | ✓ | ✓ |
| SVG | ✓ | - | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | - |
| WebP | ✓ | ✓ | ✓ | ✓ |

## Formatos 3D {#support-3d-formats}

Se admiten los siguientes formatos 3D.

Consulte también [Trabajo con recursos 3D en Dynamic Media](/help/assets/dynamic-media/assets-3d.md).

| Formato | Almacenamiento | Versiones | Flujo de trabajo | Publicación | Control de acceso | Vista previa de miniaturas | Previsualización 3D | Entrega de Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ | - | ✓ | ✓ | - | - |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ | - | ✓ | - | ✓ | - |
| OBJ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| FBX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | - |
| 3DS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | - |
| USDz | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ |
| SBSAR | ✓ | ✓ | ✓ | - | ✓ | ✓ | - | - |

## [!DNL Camera Raw] formatos {#camera-raw-formats}

| Formato del archivo | Generación de miniaturas | Extracción de metadatos | Anchura/Altura |
| ----------- | -------------------- | ------------------- | ------------ |
| 3FR | ✓ | ✓ | ✓ |
| ARW | ✓ | ✓ | ✓ |
| CR2 | ✓ | ✓ | ✓ |
| CR3 | ✓ | ✓ | ✓ |
| TRIPULACIÓN | ✓ | ✓ | ✓ |
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
| CRUDO | ✓ | ✓ | ✓ |
| RW2 | ✓ | ✓ | ✓ |
| RWL | ✓ | ✓ | ✓ |
| SRF | ✓ | ✓ | ✓ |
| SRW | ✓ | ✓ | ✓ |
| X3F | ✓ | ✓ | ✓ |

## Formatos de documento {#document-formats}

Los formatos de documento admitidos para las funciones de administración de recursos son los siguientes.

| Formato del archivo | Generación de miniaturas | Extracción de texto completo | Anchura/Altura | Administración de metadatos | [Recursos conectados](use-assets-across-connected-assets-instances.md) | Vista previa completa del documento |
| ----------- | -------------------- | ------------------- | ------------ | ------------------- | ---------------- |--------|
| DOC | - | - | - | ✓ | ✓ | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| EPUB | - | ✓ | - | - | - | - |
| HTML | - | ✓ | - | ✓ | ✓ | - |
| ODF | ✓ | ✓ | ✓ | - | - | - |
| ODM | ✓ | ✓ | ✓ | - | - | - |
| ODP | ✓ | ✓ | ✓ | - | - | - |
| ODS | ✓ | ✓ | ✓ | - | - | - |
| PUNTO | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| OFG | ✓ | ✓ | ✓ | - | - | - |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| PPT | - | - | - | ✓ | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| PS | - | - | ✓ | - | - | - |
| RTF | - | ✓ | - | ✓ | ✓ | ✓ |
| TXT | ✓ | ✓ | - | ✓ | ✓ | ✓ |
| XLS | - | - | - | ✓ | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | - | ✓ | - | - | - | - |

## Formatos de vídeo {#video-formats}

| Formato del archivo | Generación de miniaturas | Extracción de metadatos | Anchura/Altura | Vista previa | Salida |
| ----------- | -------------------- | ------------------- | ------------ | ------- | ------- |
| 3G2 | - | ✓ | - | - | - |
| 3GP | - | ✓ | - | - | - |
| AVI | ✓ | ✓ | ✓ | ✓ | - |
| DIVX | ✓ | - | ✓ | ✓ | - |
| F4V | ✓ | ✓ | ✓ | ✓ | - |
| FLV | ✓ | ✓ | ✓ | ✓ | - |
| M2T | ✓ | - | ✓ | ✓ | - |
| M2TS | ✓ | - | ✓ | ✓ | - |
| M2V | ✓ | - | ✓ | ✓ | - |
| M4V | ✓ | ✓ | ✓ | ✓ | - |
| MKV | ✓ | - | ✓ | ✓ | - |
| MOV | ✓ | ✓ | ✓ | ✓ | - |
| MP4 | ✓ | ✓ | ✓ | ✓ | ✓ |
| MPEG | ✓ | ✓ | ✓ | ✓ | - |
| MPG | ✓ | ✓ | ✓ | ✓ | - |
| MTS | ✓ | - | ✓ | ✓ | - |
| MXF | ✓ | - | ✓ | ✓ | - |
| OGV | ✓ | - | ✓ | ✓ | - |
| QT | ✓ | - | ✓ | ✓ | - |
| R3D | - | ✓ | ✓ | ✓ | - |
| SWF | ✓ | - | ✓ | ✓ | - |
| WebM | ✓ | - | ✓ | ✓ | ✓ |
| WMV | ✓ | ✓ | ✓ | ✓ | - |

## Formatos de audio {#audio-formats}

[!DNL Assets] as a [!DNL Cloud Service] proporciona compatibilidad de extracción de metadatos de XMP para los formatos de audio AIF, ASF, M4A, MP3, WAV y WMA.

## Formatos de entrada compatibles para la transcripción de audio y vídeo {#audio-video-transcription-formats}

* FLV (con códecs H.264 y AAC) (.flv)
* MXF (.mxf)
* MPEG2-PS, MPEG2-TS, 3GP (.ts, .ps, .3gp, .3gpp, .mpg)
* Vídeo de Windows Media (WMV)/ASF (.wmv, .asf)
* AVI (sin comprimir 8/10 bits) (.avi)
* MP4 (.mp4, .m4a, .m4v)
* Microsoft® Digital Video Recording (DVR-MS) (.dvr-ms)
* Matroska/WebM (.mkv)
* WAVE/WAV (.wav)
* QuickTime (.mov)

## Sugerencias y limitaciones {#limitations-and-tips}

* Actualmente, el límite de tamaño de archivo para la extracción de metadatos es de aproximadamente 15 GB. Al cargar recursos grandes, a veces la operación de extracción de metadatos falla.

## Dynamic Media: Formatos de vídeo de entrada compatibles para la transcodificación {#video-dynamic-media-transcoding}

| Extensión de archivo de vídeo | Contenedor | Códecs de vídeo recomendados | Códecs de vídeo no compatibles |
| --- | --- | --- | --- |
| AVI | Entrelazado A/V | XVID, DIVX, HDV, MiniDV (DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3 (IV30), MJPEG, Microsoft® Video 1 (MS-CRAM) |
| FLV, F4V | Flash Adobe | H264/AVC, Flix VP6, H263, Sorenson | SWF (archivos de animación vectorial) |
| M4V | Apple iTunes | H264/AVC | − |
| MKV | Matroska | H264/AVC | − |
| MOV, QT | Apple QuickTime | H264/AVC, Apple ProRes422 y HQ, Sony XDCAM, Sony DVCAM, HDV, Panasonic DVCPro, Apple DV (DV25), Apple PhotoJPEG, Sorenson, Avid DNxHD, Avid AVR | Apple Intermediate, Apple Animation |
| MP4 | MPEG-4 | H264/AVC (todos los perfiles) | − |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 | − |
| ‡ MXF | MXF | XDCAM de Sony, MPEG-2, MPEG-4, Panasonic DVCPro | − |
| OGV, OGG | OGG | Theora, VP3, Dirac | − |
| WebM | WebM | Google VP8 | − |
| WMV | Windows Media 9 | WMV3 (v9), WMV2 (v8), WMV1 (v7), GoToMeeting (G2M2, G2M3, G2M4) | Pantalla Microsoft® (MSS2), Microsoft® Photo Story (WVP2) |

‡ Este formato de vídeo aún no es compatible con vídeos interactivos de Dynamic Media ni con anotaciones de Experience Manager Assets.

## Dynamic Media: formatos de documento compatibles {#document-support-dynamic-media}

| Formato | Cargar (formato de entrada) | Crear ajuste preestablecido de imagen (formato de salida) | Previsualizar representación dinámica | Ofrecer representación dinámica | Descargar representación dinámica |
| ------ | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| IA | ✓ | - | - | - | - |
| INDD | ✓ | - | - | - | - |
| PDF (consulte la nota más abajo) | ✓ | ✓ | ✓ | ✓ | ✓ |

>[!NOTE]
>
>En el caso de los PDF seguros, solo se admite la carga.

## Dynamic Media: Formatos de imagen rasterizada compatibles {#image-support-dynamic-media}

| Formato | Cargar (formato de entrada) | Crear ajuste preestablecido de imagen (formato de salida) | Previsualizar representación dinámica | Ofrecer representación dinámica | Descargar representación dinámica | Establecer tipos compatibles con este formato |
|---|:---:|:---:|:---:|:---:|:---:| --- |
| AVIF | − | − | − | ✓ | − | − |
| BMP | ✓ | − | − | − | − | [Imagen](/help/assets/dynamic-media/image-sets.md), [Medios mixtos](/help/assets/dynamic-media/mixed-media-sets.md) y [Giro](/help/assets/dynamic-media/spin-sets.md) |
| [EPS](/help/assets/dynamic-media/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| HEIC | − | − | − | ✓ | − | − |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | [Imagen](/help/assets/dynamic-media/image-sets.md), [Medios mixtos](/help/assets/dynamic-media/mixed-media-sets.md) y [Giro](/help/assets/dynamic-media/spin-sets.md) |
| PICT | ✓ | − | − | − | − | − |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | [Imagen](/help/assets/dynamic-media/image-sets.md), [Medios mixtos](/help/assets/dynamic-media/mixed-media-sets.md) y [Giro](/help/assets/dynamic-media/spin-sets.md) |
| PSD ‡ | ✓ | − | − | − | − | − |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ | [Imagen](/help/assets/dynamic-media/image-sets.md), [Medios mixtos](/help/assets/dynamic-media/mixed-media-sets.md) y [Giro](/help/assets/dynamic-media/spin-sets.md) |
| WEBP | − | − | − | ✓ | − | − |

<!-- AVIF, HEIC, and WebP added to table above on March 4, 2024 based on CQDOC-21294 -->

‡ La imagen combinada se extrae del archivo PSD. Es una imagen generada por [!DNL Adobe Photoshop] y que se incluye en el archivo PSD. Según la configuración, la imagen combinada puede ser o no la imagen real.

## Dynamic Media: formatos de imagen rasterizada no compatibles {#unsupported-raster-image-formats-dm}

Los siguientes subtipos de formatos de archivo de imagen rasterizada que *no* son compatibles con [!DNL Dynamic Media]:

* Archivos PNG con un tamaño de fragmento IDAT superior a 100 MB.
* Archivos PSB.
* Los archivos PSD con un espacio de color distinto de CMYK, RGB, escala de grises o mapa de bits no son compatibles. No se admiten los espacios de color DuoTone, Lab e Indexed.
* Archivos PSD con una profundidad de bits superior a 16.
* Archivos TIFF que tienen datos de punto flotante.
* Archivos TIFF que tienen espacio de color Lab.

## Dynamic Media: formatos de archivo 3D compatibles {#support-3d-formats-dynamic-media}

Ver también [formatos 3D compatibles](/help/assets/file-format-support.md#support-3d-formats)

| Extensión de archivo 3D | Formato del archivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmisión binaria GL | model/gltf-binary | Incluye los materiales y las texturas como un solo recurso. |
| OBJ | Archivo de objeto 3D WaveFront | application/x-tgif | |
| STL | Estereolitografía | application/vnd.ms-pki.stl | |
| USDZ | Universal Scene Description Archivo zip | model/vnd.usdz+zip | *Compatibilidad con la ingesta y generación de miniaturas; aún no se admiten vistas previas 3D.* USDZ es un formato 3D que Safari o iOS pueden ver de forma nativa. |

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de recursos](mac-api-assets.md)
* [Buscar recursos](search-assets.md)
* [Recursos de red](use-assets-across-connected-assets-instances.md)
* [Informes de recurso](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)
* [Publicación de recursos en AEM y Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Procesamiento de recursos mediante microservicios de recursos](asset-microservices-overview.md).
>* [Formatos de archivo compatibles con el etiquetado inteligente de recursos basados en texto](/help/assets/smart-tags.md#smart-tags-supported-file-formats)
