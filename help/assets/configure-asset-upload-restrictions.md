---
title: Configurar restricciones de carga de recursos
description: Configure Adobe Experience Manager Assets para restringir el tipo de recursos que los usuarios pueden cargar en función del tipo MIME. Ayuda a evitar cargas accidentales de archivos malintencionados y formatos no deseados.
exl-id: 094c31f3-f2e9-4b44-9995-c76fb78ca458
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 8%

---

# Configurar restricciones de carga de recursos {#configure-asset-upload-restrictions}

Puede configurar Adobe Experience Manager Assets para restringir el tipo de recursos que los usuarios pueden cargar en función del tipo MIME.

>[!IMPORTANT]
>
>De forma predeterminada, Experience Manager Assets permite a los usuarios cargar recursos de todos los tipos MIME. Sin embargo, puede configurar los ajustes para restringir a los usuarios la carga de archivos de tipos MIME específicos únicamente.

## Requisitos previos {#prerequisites-asset-upload-restrictions}

Debe tener privilegios de administrador para configurar las restricciones de carga de recursos.

## Aplicar restricciones para cargas de recursos {#apply-restrictions-asset-uploadsssssss}

Para configurar [!DNL Experience Manager] para restringir a los usuarios la carga de archivos de tipos MIME específicos:

1. Vaya a **[!UICONTROL Herramientas > Recursos > Configuraciones de recursos]**.

1. Clic **[!UICONTROL Restricciones de carga]**.

1. Clic **[!UICONTROL Añadir]** para definir los tipos MIME permitidos.

1. Especifique el tipo MIME en el cuadro de texto. Puede hacer clic en **[!UICONTROL Añadir]** de nuevo para especificar más tipos MIME permitidos. También puede hacer clic en ![icono eliminar](assets/delete-icon.svg) para eliminar cualquier tipo MIME de la lista.

1. Haga clic en **[!UICONTROL Guardar]**.

**Ejemplo 1: Permitir la carga de todas las imágenes y archivos del PDF en Experience Manager Assets**

Para permitir la carga de imágenes en todos los formatos y archivos de PDF en Experience Manager Assets, realice la siguiente configuración:

![Restricciones de carga de recursos](assets/asset-upload-restrictions.png)

`image/*` ya que el tipo MIME permite la carga de imágenes en todos los formatos. `application/pdf` ya que el tipo MIME permite cargar archivos del PDF en Experience Manager Assets.

Si intenta cargar un archivo que no está incluido en la lista de tipos MIME permitidos, Experience Manager Assets muestra el siguiente mensaje de error:

![Archivos restringidos](assets/asset-upload-restricted-files.png)

`Screen Recording 2022-08-31 at 3.36.09 PM.mov` hace referencia a un nombre de archivo que no está incluido en los tipos MIME permitidos.

**Ejemplo 2: Permitir la carga de formatos de imagen específicos en Experience Manager Assets**

Para agregar formatos de imagen específicos a los tipos MIME permitidos y restringir la carga de todos los demás formatos de recurso, haga la siguiente configuración:

![Restricciones de recursos](assets/asset-restrictions.png)

Según la configuración que se muestra en la imagen, puede cargar imágenes en los formatos .JPG, .PNG y .GIF a Experience Manager Assets.

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de Recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con Assets](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos conectados](use-assets-across-connected-assets-instances.md)
* [Informes de Asset](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)
