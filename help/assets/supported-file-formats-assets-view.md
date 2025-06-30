---
title: Formatos de archivo compatibles
description: Formatos de archivo compatibles con los distintos casos de uso de [!DNL Assets view]
role: User, Leader, Admin, Architect, Developer
contentOwner: AG
exl-id: 5936ace2-318e-4888-9ad4-23e6f6bfb857
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 100%

---

# Compatibilidad de formatos de archivo en [!DNL Assets view] {#file-format-support}

[!DNL Assets view] admite una amplia gama de formatos de archivo y cada funcionalidad tiene compatibilidad variada con distintos tipos de archivo.

* ![icono de tipo de archivo de imagen](assets/image-icon.svg) Imágenes: JPG, PNG, GIF, TIFF y otros
* ![icono de tipo Creative Cloud](assets/creative-cloud-files.svg) Archivos de Creative Cloud: PSD, IA e INDD
* ![icono de tipo cámara](assets/camera-icon.svg) Archivos de Camera Raw: CR2/CR3, NEF, SRW/SRF y otros
* ![icono de tipo de archivo de documento](assets/document-icon.svg) Documentos: DOCX, PDF, PPTX y XLSX
* ![icono de tipo de archivo de vídeo](assets/video-icon.svg) Vídeos: MP4

[!DNL Assets view] admite cualquier formato de archivo binario con servicios básicos como, por ejemplo, almacenamiento, carga, copia, movimiento, eliminación y adición de metadatos.

[!DNL Assets view] también admite archivos RAW de cámara de una amplia gama de fabricantes líderes de cámaras, incluidos Canon (CR2/CR3), Nikon (NEF), Sony (SRW/SRF), Fujifilm (RAF), Olympus (ORF) y otros, con tecnología Adobe Camera Raw.

Los distintos tipos de archivo tienen diferentes grados de compatibilidad con los casos de uso y las funciones, como se describe a continuación. Utilice la leyenda para comprender el nivel de compatibilidad.

| Nivel de soporte | Descripción |
|-------------------|-------------------------|
| ✓ | Compatible |
| ✓ ‡ | Compatible con condiciones |
| − | No aplicable |

## Adición, carga y visualización de recursos {#support-to-upload-view}

<!-- TBD: For AEM, AI files require the PDF option to be selected when saving the AI file.
-->

| Tipo de recurso | [Examinar](/help/assets/navigate-assets-view.md) | Copiar | [Cargar](/help/assets/add-delete-assets-view.md) | Crear | [Eliminar](/help/assets/add-delete-assets-view.md#delete-assets) | Detalles | Zoom de imagen | [Vistos recientemente](/help/assets/navigate-assets-view.md) |
|-------------------|----------|----------|----------|----------|----------|-------------------|------------|-----------------|
| Rasterización de imágenes | ✓ | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| Archivos RAW | ✓ | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| Carpetas | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | − | − |
| Vídeos MP4 | ✓ | ✓ | ✓ | − | ✓ | ✓ ‡ | − | ✓ |
| PDF | ✓ | ✓ | ✓ | − | ✓ | ✓ | − | ✓ |
| PSD, PSB, IA e INDD | ✓ | ✓ | ✓ | − | ✓ | ✓ ‡ | − | ✓ |
| Otros archivos binarios | ✓ | ✓ | ✓ | − | ✓ | ✓ | − | ✓ |

<!-- Hiding CC Libraries (considered beta) as per PM feedback.
| CC Libraries  | &#10003; | &minus;  | &#10003; | &#10003; | &#10003; | &#10003; | &minus;    | &minus;         |
-->

## Búsqueda, utilización y edición de recursos {#support-to-search-use-edit}

| Tipo de recurso | [Descargar](/help/assets/manage-organize-assets-view.md#download) | Arrastrar y colocar | [Editor de imágenes](/help/assets/edit-images-assets-view.md) | [Buscar](/help/assets/search-assets-view.md) | [Etiquetas inteligentes](/help/assets/metadata-assets-view.md#tags) | [Cambiar nombre](/help/assets/manage-organize-assets-view.md) | [Versiones](/help/assets/manage-organize-assets-view.md#versions-of-assets) |
|---------------|----------|---------------|--------------|----------|------------|----------|----------|
| Rasterización de imágenes | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Archivos RAW | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ | ✓ |
| Carpetas | ✓ | ✓ | − | ✓ | − | ✓ | ✓ |
| Vídeos | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| Bibliotecas CC | − | − | − | − | − | ✓ | ✓ |
| PDF | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| PSD y PSB | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| IA e INDD | ✓ | ✓ | − | ✓ | − | ✓ | ✓ |
| Otros archivos binarios | ✓ | ✓ | − | ✓ | − | ✓ | ✓ |


## Revisión de recursos y colaboración {#support-to-review-collaborate}

| Tipo de recurso | Anotar | Comentar | Crear tareas y revisar |
|---------------|----------|----------|-------------------------|
| Rasterización de imágenes | ✓ | ✓ | ✓ |
| Archivos RAW | ✓ | ✓ | ✓ |
| Carpetas | − | − | − |
| Vídeos | − | ✓ | ✓ |
| Bibliotecas CC | − | − | − |
| PDF | − | ✓ | ✓ |
| PSD, PSB, IA e INDD | − | ✓ | ✓ |
| Otros archivos binarios | − | ✓ | ✓ |
| DOC | − | ✓ | ✓ |
| DOCX | − | ✓ | ✓ |
| PPT | − | ✓ | ✓ |
| PPTX | − | ✓ | ✓ |
| XLS | − | ✓ | ✓ |
| XLSX | − | ✓ | ✓ |
| TXT | − | ✓ | ✓ |
| RTF | − | ✓ | ✓ |

## Otras tareas de administración de recursos {#support-to-manage-assets}

| Tipo de recurso | [Metadatos](/help/assets/metadata-assets-view.md) | [Representaciones](/help/assets/add-delete-assets-view.md#renditions) | [Papelera](/help/assets/add-delete-assets-view.md#delete-assets) | Copiar | Mover |
|---------------|-------------------|------------|----------|----------|----------|
| Rasterización de imágenes | ✓ | ✓ | ✓ | ✓ | ✓ |
| Archivos RAW | ✓ | ✓ | ✓ | ✓ | ✓ |
| Carpetas | ✓ | − | ✓ | ✓ | ✓ |
| Vídeos | ✓ | − | ✓ | ✓ | ✓ |
| Bibliotecas CC | ✓ | − | − | − | − |
| PDF | ✓ | − | ✓ | ✓ | ✓ |
| IA e INDD | ✓ | − | ✓ | ✓ | ✓ |
| PSD y PSB | ✓ | ✓ | ✓ | ✓ | ✓ |
| Otros archivos binarios | ✓ | − | ✓ | ✓ | ✓ |

Los usuarios de [!DNL Adobe Asset Link] pueden cargar y registrar archivos (cargar una nueva versión) en el repositorio de [!DNL Assets view] desde las aplicaciones de escritorio de [!DNL Adobe Creative Cloud] admitidas.

<!-- TBD: Saving the template table separately for later use.
| Asset type    | Features |
|---------------|----------|
| Raster images |          |
| Folders       |          |
| Videos        |          |
| CC Libraries  |          |
| PDF files     |          |
| PSD, PSB           |          |
| AI            |          |
| INDD          |          |

>[!MORELIKETHIS]
>
>* []()
-->

## Siguientes pasos {#next-steps}

* Realice comentarios del producto mediante la opción [!UICONTROL Comentarios] disponible en la interfaz de usuario de la vista Recursos

* Proporcione comentarios sobre la documentación usando [!UICONTROL Editar esta página] ![editar la página](assets/do-not-localize/edit-page.png) o [!UICONTROL Registrar una incidencia] ![crear una incidencia de GitHub](assets/do-not-localize/github-issue.png), disponibles en la barra lateral derecha

* Contacto con el [Servicio de atención al cliente](https://experienceleague.adobe.com/es?support-solution=General#support)
