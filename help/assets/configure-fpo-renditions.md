---
title: Generar representaciones solo para ubicación para Adobe InDesign
description: Genere representaciones FPO de recursos nuevos y existentes mediante el flujo de trabajo de Experience Manager Assets y ImageMagick.
contentOwner: Vishabh Gupta
role: Admin
feature: Renditions
exl-id: 869c1c34-6287-4d62-bb7a-aa4df580ac0e
source-git-commit: f0e9fe0bdf35cc001860974be1fa2a7d90f7a3a9
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 7%

---

# Generar representaciones solo para ubicación para Adobe InDesign {#fpo-renditions}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/configure-fpo-renditions.html?lang=en) |
| AEM as a Cloud Service | Este artículo |

Cuando se colocan recursos de gran tamaño de Experience Manager en documentos de Adobe InDesign, un profesional creativo debe esperar un tiempo considerable después de enviarlos [colocar un recurso](https://helpx.adobe.com/indesign/using/placing-graphics.html). Mientras tanto, se bloquea al usuario el uso del InDesign. Esto interrumpe el flujo creativo y afecta negativamente a la experiencia del usuario. El Adobe permite colocar temporalmente representaciones de pequeño tamaño en documentos de InDesign para empezar. Cuando se requiere la salida final, por ejemplo, para los flujos de trabajo de impresión y publicación, los recursos originales de resolución completa reemplazan la representación temporal en segundo plano. Esta actualización asíncrona en segundo plano acelera el proceso de diseño para mejorar la productividad y no obstaculiza el proceso creativo.

Assets proporciona representaciones que se utilizan para la ubicación solamente (FPO). Estas representaciones de FPO tienen un tamaño de archivo pequeño, pero son de la misma proporción de aspecto. Si una representación de FPO no está disponible para un recurso, Adobe InDesign utiliza el recurso original en su lugar. Este mecanismo de reserva garantiza que el flujo de trabajo creativo se desarrolle sin interrupciones.

Experience Manager as a Cloud Service ofrece funciones de procesamiento de recursos nativas de la nube para generar las representaciones de FPO. Utilice los microservicios de recursos para generar representaciones. Puede configurar la generación de representaciones de los recursos recién cargados y de los recursos que existen en Experience Manager.

A continuación se indican los pasos para generar representaciones de FPO:

1. [Creación de un perfil de procesamiento](#create-processing-profile).

1. Configure el Experience Manager para que utilice este perfil [procesar nuevos recursos](#generate-renditions-of-new-assets).
1. Utilice los perfiles para lo siguiente [procesar recursos existentes](#generate-renditions-of-existing-assets).

## Crear un perfil de procesamiento {#create-processing-profile}

Para generar representaciones de FPO, cree un **[!UICONTROL Perfil de procesamiento]**. Los perfiles utilizan microservicios de recursos nativos de la nube para el procesamiento. Para obtener instrucciones, consulte [creación de perfiles de procesamiento para microservicios de recursos](asset-microservices-configure-and-use.md).

Seleccionar **[!UICONTROL Crear representación de FPO]** para generar la representación de FPO. Si lo desea, haga clic en **[!UICONTROL Añadir nuevo]** para agregar otra configuración de representación al mismo perfil.

![create-processing-profile-fpo-renditions](assets/create-processing-profile-fpo-renditions.png)

## Generar representaciones de nuevos recursos {#generate-renditions-of-new-assets}

Para generar representaciones FPO de nuevos recursos, aplique la variable **[!UICONTROL Perfil de procesamiento]** a la carpeta en las propiedades de la carpeta. En la página Propiedades de una carpeta, haga clic en **[!UICONTROL Procesamiento de recursos]** , seleccione la pestaña **[!UICONTROL Perfil de FPO]** as a **[!UICONTROL Perfil de procesamiento]** y guarde los cambios. Todos los recursos nuevos cargados en la carpeta se procesan mediante este perfil.

![add-fpo-rendition](assets/add-fpo-rendition.png)


## Generar representaciones de recursos existentes {#generate-renditions-of-existing-assets}

Para generar representaciones, seleccione los recursos y siga estos pasos.

![fpo-existing-asset-reprocess](assets/fpo-existing-asset-reprocess.gif)


## Ver representaciones de FPO {#view-fpo-renditions}

Puede comprobar las representaciones de FPO generadas una vez finalizado el flujo de trabajo. En la interfaz de usuario de Experience Manager Assets, haga clic en el recurso para abrir una vista previa grande. Abra el carril izquierdo y seleccione **[!UICONTROL Representaciones]**. También puede utilizar el método abreviado de teclado `Alt + 3` cuando la previsualización está abierta.

Clic **[!UICONTROL Representación de FPO]** para cargar su previsualización. De forma opcional, puede hacer clic con el botón derecho en la representación y guardarla en el sistema de archivos. Compruebe las representaciones disponibles en el carril izquierdo.

![rendition_list](assets/list-renditions.png)

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con recursos](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos de red](use-assets-across-connected-assets-instances.md)
* [Informes de recurso](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)
