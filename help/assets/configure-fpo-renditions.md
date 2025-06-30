---
title: Generar representaciones solo para ubicación para Adobe InDesign
description: Genere representaciones de FPO (solo para ubicación) de recursos nuevos y existentes mediante el flujo de trabajo de Experience Manager Assets y ImageMagick.
contentOwner: Vishabh Gupta
role: Admin
feature: Renditions
exl-id: 869c1c34-6287-4d62-bb7a-aa4df580ac0e
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 10%

---

# Generar representaciones solo para ubicación para Adobe InDesign {#fpo-renditions}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/assets/administer/configure-fpo-renditions) |
| AEM as a Cloud Service | Este artículo |

Al colocar recursos de gran tamaño de Experience Manager en documentos de Adobe InDesign, un profesional creativo debe esperar un tiempo considerable después de [colocar un recurso](https://helpx.adobe.com/es/indesign/using/placing-graphics.html). Mientras tanto, se bloquea al usuario el uso de InDesign. Esto interrumpe el flujo creativo y afecta negativamente a la experiencia del usuario. Adobe permite colocar temporalmente representaciones de pequeño tamaño en documentos de InDesign para empezar. Cuando se requiere la salida final, por ejemplo, para los flujos de trabajo de impresión y publicación, los recursos originales de resolución completa reemplazan la representación temporal en segundo plano. Esta actualización asíncrona en segundo plano acelera el proceso de diseño para mejorar la productividad y no obstaculiza el proceso creativo.

Assets proporciona representaciones que se utilizan para ubicación solamente (FPO). Estas representaciones de FPO tienen un tamaño de archivo pequeño, pero son de la misma proporción de aspecto. Si una representación de FPO no está disponible para un recurso, Adobe InDesign utiliza el recurso original en su lugar. Este mecanismo de reserva garantiza que el flujo de trabajo creativo se desarrolle sin interrupciones.

Experience Manager as a Cloud Service ofrece funciones de procesamiento de recursos nativas de la nube para generar las representaciones de FPO. Utilice los microservicios de recursos para generar representaciones. Puede configurar la generación de representaciones de los recursos recién cargados y de los recursos que existen en Experience Manager.

A continuación se indican los pasos para generar representaciones de FPO:

1. [Crear un perfil de procesamiento](#create-processing-profile).

1. Configure Experience Manager para que use este perfil para [procesar nuevos recursos](#generate-renditions-of-new-assets).
1. Use los perfiles para [procesar los recursos existentes](#generate-renditions-of-existing-assets).

## Crear un perfil de procesamiento {#create-processing-profile}

Para generar representaciones de FPO, cree un **[!UICONTROL Perfil de procesamiento]**. Los perfiles utilizan microservicios de recursos nativos de la nube para el procesamiento. Para obtener instrucciones, consulte [crear perfiles de procesamiento para microservicios de recursos](asset-microservices-configure-and-use.md).

Seleccione **[!UICONTROL Crear representación FPO]** para generar la representación FPO. De manera opcional, haga clic en **[!UICONTROL Agregar nuevo]** para agregar otra configuración de representación al mismo perfil.

![create-processing-profile-fpo-renditions](assets/create-processing-profile-fpo-renditions.png)

## Generar representaciones de nuevos recursos {#generate-renditions-of-new-assets}

Para generar representaciones FPO de nuevos recursos, aplique el **[!UICONTROL Perfil de procesamiento]** a la carpeta en las propiedades de la carpeta. En la página Propiedades de una carpeta, haga clic en la ficha **[!UICONTROL Procesamiento de recursos]**, seleccione el **[!UICONTROL perfil de FPO]** como **[!UICONTROL Perfil de procesamiento]** y guarde los cambios. Todos los recursos nuevos cargados en la carpeta se procesan mediante este perfil.

![add-fpo-rendition](assets/add-fpo-rendition.png)


## Generar representaciones de recursos existentes {#generate-renditions-of-existing-assets}

Para generar representaciones, seleccione los recursos y siga estos pasos.

![fpo-existing-asset-reprocess](assets/fpo-existing-asset-reprocess.gif)


## Ver representaciones de FPO {#view-fpo-renditions}

Puede comprobar que las representaciones de FPO generadas una vez finalizado el flujo de trabajo. En la interfaz de usuario de Experience Manager Assets, haga clic en el recurso para abrir una vista previa grande. Abra el carril izquierdo y seleccione **[!UICONTROL Representaciones]**. También puede usar el método abreviado de teclado `Alt + 3` cuando la vista previa esté abierta.

Haga clic en **[!UICONTROL Representación de FPO]** para cargar su vista previa. De forma opcional, puede hacer clic con el botón derecho en la representación y guardarla en el sistema de archivos. Compruebe las representaciones disponibles en el carril izquierdo.

![lista_de_representación](assets/list-renditions.png)

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
* [Publicación de recursos en AEM y Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)