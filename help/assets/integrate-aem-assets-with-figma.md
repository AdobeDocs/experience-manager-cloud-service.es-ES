---
title: Integrar [!DNL AEM Assets] con [!DNL Figma].
description: Aprenda a integrar [!DNL AEM Assets] con [!DNL Figma] para acceder a los recursos de su organización y utilizarlos en el flujo de trabajo de  [!DNL Figma] diseño.
role: User
badgeSaas: label="AEM Assets" type="Positive" tooltip="(Se aplica a los AEM Assets)."
exl-id: 530561ca-497b-4331-a014-72c561e1ca84
source-git-commit: d37ebf94f617e8424799757c18037a73e97820b4
workflow-type: tm+mt
source-wordcount: '1520'
ht-degree: 4%

---


# Integrar [!DNL AEM Assets] con [!DNL Figma]{#integrate-aem-assets-with-figma}

[!DNL AEM Assets] se integra de forma nativa con [!DNL Figma], lo que permite a los diseñadores acceder directamente a los recursos almacenados en [!DNL AEM Assets] desde la interfaz de usuario de [!DNL Figma]. Puede colocar contenido administrado en [!DNL AEM Assets] en el lienzo [!DNL Figma] y, a continuación, guardar contenido nuevo o editado en el repositorio [!DNL AEM Assets].

## Antes de empezar{#prerequisites-for-aem-assets-and-figma-integration}

* La versión mínima de AEM requerida es `19149`.

* Debe tener licencias válidas de [!DNL AEM Assets] y [!DNL Figma] para integrar [!DNL AEM Assets] con [!DNL Figma].

## Formatos de archivo compatibles {#supported-file-formats-integration-figma}


* Para importar recursos de [!DNL AEM] en Figma, los formatos admitidos son recursos de imagen (JPEG, PNG), archivos de vídeo (MP4, MOV, WebM), archivos animados (GIF) y archivos vectoriales (SVG).
* Para exportar diseños de [!DNL Figma] a [!DNL AEM Assets], los formatos admitidos son **PNG**, **PDF**, **JPG**, **SVG**.

## Acceder A [!UICONTROL Conector De Assets De Adobe Experience Manager (AEM)]{#access-aem-assets-connector}

Ejecute los siguientes pasos para acceder a [!UICONTROL Adobe Experience Manager (AEM) Assets Connector]:

1. En la página de inicio de [!DNL Figma], haga clic en **[!UICONTROL Acciones]** en la barra de herramientas situada en la parte inferior del lienzo y busque [!DNL Adobe Experience Manager (AEM) Assets Connector] en la barra de búsqueda disponible en el cuadro de diálogo.
1. Seleccione [!DNL Adobe Experience Manager (AEM) Assets Connector] para mostrar el panel [!DNL Adobe Experience Manager (AEM) Assets Connector]. [Importe [!DNL AEM] recursos en su [!DNL Figma] lienzo](#import-aem-assets-into-figma-workflow) mediante este panel.   ![acciones](/help/assets/assets/actions-on-figma.png)
También puedes acceder a [[!DNL Adobe Experience Manager (AEM) Assets Connector]](https://www.figma.com/community/plugin/1512561378275712210/adobe-experience-manager-aem-assets-connector), disponible en la comunidad [!DNL Figma], hacer clic en **[!UICONTROL Abrir en...]**, seleccionar un archivo reciente o crear uno nuevo y hacer clic en **[!UICONTROL Ejecutar]** para acceder al panel [!DNL Adobe Experience Manager (AEM) Assets Connector].   ![plugin-page-on-figma-community](/help/assets/assets/plugin-page-on-figma-community.png)

>[!NOTE]
>
> [Póngase en contacto con el Soporte técnico de Adobe](https://helpx.adobe.com/es/contact.html) para obtener ayuda si ve un mensaje de **[!UICONTROL Error de red]** después de iniciar sesión en su entorno de [!DNL AEM].

## Importar [!DNL AEM] recursos al lienzo [!DNL Figma]{#import-aem-assets-into-figma-workflow}

[Acceda al [[!UICONTROL panel]](#access-aem-assets-connector) del conector Assets de Adobe Experience Manager (AEM)] dentro de su interfaz de diseño de [!DNL Figma] y haga lo siguiente:

1. Busque recursos en el panel [!UICONTROL Conector de Assets de Adobe Experience Manager (AEM)]. Para obtener más información, vea [usar el Asesor de contenido](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector#using-asset-selector).

1. Arrastre y suelte el recurso en el lienzo o selecciónelo y haga clic en **[!UICONTROL Seleccionar]** para llevar el recurso al lienzo.

1. Haga clic en ![tres puntos](/help/assets/assets/three-dots.svg) en la ruta de la carpeta para mostrar todas las carpetas principales y secundarias de la jerarquía actual. Seleccione una carpeta para desplazarse a esa ubicación.   ![tres puntos](/help/assets/assets/figma-v2-plugin.png)

1. [Opcional] Haga clic en **[!UICONTROL Buscar actualizaciones]**. Los recursos utilizados en el documento Figma actual se comparan con los recursos que existen en AEM. Las actualizaciones se muestran en una ventana independiente. Haga clic en **[!UICONTROL Actualizar]** para obtener el recurso actualizado de AEM en el documento de Figma.

Una vez que el diseño de Figma esté listo, puede [exportar el recurso al repositorio de AEM Assets](#export-figma-design-to-aem-assets-folder).

## Exportar recursos al repositorio [!DNL AEM Assets]{#export-figma-design-to-aem-assets-folder}

[Acceda al [[!UICONTROL panel]](#access-aem-assets-connector) del conector Assets de Adobe Experience Manager (AEM)] dentro de su interfaz de diseño de [!DNL Figma] y ejecute los siguientes pasos para exportar su diseño al repositorio de [!DNL AEM Assets]:

1. Vaya a la carpeta de destino donde desea guardar el diseño de [!DNL Figma]. Si ya se encuentra dentro de una carpeta, haga clic en Más opciones (![tres puntos](/help/assets/assets/three-dots.svg)) en la ruta de la carpeta para seleccionar una carpeta de destino diferente.
1. Opcional: agrupe los recursos en el lienzo para seleccionarlos como una sola unidad que cargar en la carpeta.
1. Haga clic en ![cargar archivo](/help/assets/assets/upload-icon.svg) **[!UICONTROL Cargar]** para mostrar el cuadro de diálogo **[!UICONTROL Cargar recurso]**.
1. En el cuadro de diálogo, seleccione **[!UICONTROL Elemento seleccionado]** o **[!UICONTROL Página]**, especifique un nombre de archivo o página, defina una configuración de exportación y haga clic en **[!UICONTROL Cargar]** para cargar el recurso seleccionado o todo el diseño en la carpeta de destino.

   La configuración de exportación incluye el formato de archivo, la escala y la calidad. Por ejemplo, si selecciona JPG como formato de archivo, también puede definir la escala y la calidad de la imagen. Del mismo modo, si selecciona PNG como formato de archivo, también puede definir la escala de la imagen.   ![cargar diseño figma](/help/assets/assets/upload-figma-design.png)


## Preguntas frecuentes {#frequently-asked-questions-aem-assets-figma-integration}

### ¿Qué permite hacer la integración de AEM Assets con Figma? {#aem-assets-figma-integration-overview}

La integración de AEM Assets con Figma permite a los diseñadores acceder directamente a los activos almacenados en Adobe Experience Manager desde la interfaz de usuario de Figma, sin cambiar entre herramientas. Los diseñadores pueden buscar e importar imágenes, vídeos, archivos animados y vectores desde los AEM Assets al lienzo Figma, y exportar diseños completados o editados al repositorio de AEM Assets en los formatos compatibles. La integración es nativa, y no requiere conectores de terceros más allá del conector de AEM Assets de Adobe Experience Manager disponible en la comunidad de Figma.

### ¿Cuáles son los requisitos previos para la integración de AEM Assets con Figma? {#aem-assets-figma-prerequisites}

La integración de AEM Assets con Figma requiere dos requisitos previos: una versión mínima de AEM de 19149 y licencias válidas tanto para AEM Assets como para Figma. Ambas condiciones deben cumplirse para poder acceder y utilizar el conector de AEM Assets de Adobe Experience Manager en Figma. Si aparece un mensaje de error de red tras iniciar sesión en el entorno de AEM durante la instalación, póngase en contacto con el soporte técnico de Adobe para obtener ayuda.

### ¿Cómo puedo acceder al conector de AEM Assets de Adobe Experience Manager en Figma? {#access-aem-assets-connector-figma}

El conector de AEM Assets de Adobe Experience Manager es accesible de dos formas desde Figma. En la página de inicio de Figma, haga clic en **Acciones** en la barra de herramientas situada en la parte inferior del lienzo, busque Conector de AEM Assets de Adobe Experience Manager en el cuadro de diálogo y selecciónelo para abrir el panel Conector. También puedes acceder al conector directamente desde la página de la comunidad Figma, hacer clic en **Abrir en**, seleccionar un archivo reciente o crear uno nuevo y hacer clic en **Ejecutar** para iniciar el panel conector.

### ¿Qué formatos de archivo se pueden importar desde AEM Assets a Figma? {#aem-assets-figma-import-formats}

Se admiten los siguientes formatos de archivo para importar AEM Assets a Figma: recursos de imagen en formatos JPEG y PNG, archivos de vídeo en formato MP4, MOV y WebM, archivos animados en formato GIF y archivos vectoriales en formato SVG. Assets en estos formatos se puede buscar dentro del panel Conector de AEM Assets de Adobe Experience Manager y colocarse directamente en el lienzo de Figma arrastrando y soltando o seleccionando el recurso y haciendo clic en Seleccionar.

### ¿Cómo se importa un recurso de AEM Assets a mi lienzo Figma? {#import-aem-assets-figma-canvas}

Para importar un recurso de AEM Assets a Figma, abra el panel Conector de AEM Assets de Adobe Experience Manager en la interfaz de diseño de Figma. Busque el recurso mediante el Asesor de contenido en el panel conector. Una vez que se encuentre el recurso, arrástrelo y suéltelo en el lienzo o selecciónelo y haga clic en **Seleccionar** para colocarlo en el lienzo. Para desplazarse por las carpetas dentro del repositorio, haga clic en el icono de tres puntos de la ruta de la carpeta para ver y navegar por las carpetas principales y secundarias de la jerarquía actual.

### ¿Cómo puedo comprobar si se han actualizado los AEM Assets utilizados en mi documento Figma? {#check-aem-assets-updates-figma}

El Conector de AEM Assets de Adobe Experience Manager en Figma incluye una opción **Comprobar actualizaciones** que compara los recursos que se utilizan actualmente en el documento Figma abierto con sus versiones en AEM Assets. Para usarlo, abra el panel conector y haga clic en **Buscar actualizaciones**. Todos los recursos que se hayan actualizado en AEM se muestran en una ventana independiente. Haga clic en **Actualizar** para extraer la última versión de cada recurso actualizado de AEM en el documento de Figma.

### ¿Qué formatos de archivo se admiten al exportar un diseño Figma a AEM Assets? {#figma-export-aem-assets-formats}

Al exportar un diseño de Figma al repositorio de AEM Assets, se admiten cuatro formatos de archivo: PNG, PDF, JPG y SVG. La configuración de exportación también permite definir ajustes adicionales en función del formato seleccionado: para las exportaciones JPG, se puede especificar la escala y la calidad de la imagen; para las exportaciones PNG, se puede definir la escala de la imagen. Estos ajustes se configuran en el cuadro de diálogo Cargar recurso durante el proceso de exportación.

### ¿Cómo se exporta un diseño Figma al repositorio de AEM Assets? {#export-figma-design-aem-assets}

Para exportar un diseño de Figma a AEM Assets, abra el panel Conector de AEM Assets de Adobe Experience Manager en Figma y vaya a la carpeta de destino en el repositorio de AEM Assets. Haga clic en el icono Cargar para abrir el cuadro de diálogo Cargar recurso. En el cuadro de diálogo, seleccione Elemento seleccionado para cargar un recurso específico o Página para cargar toda la página de diseño, especifique un nombre de archivo o página, defina la configuración de exportación, incluido el formato, la escala y la calidad, y haga clic en Cargar. El diseño se guarda en la carpeta de destino de los AEM Assets seleccionada.

### ¿Puedo agrupar recursos en Figma antes de exportarlos a AEM Assets? {#group-assets-figma-export-aem}

Los diseños de Figma se pueden agrupar en el lienzo antes de exportarlos al repositorio de AEM Assets. La agrupación de recursos permite seleccionarlos como una sola unidad y cargarlos juntos en la carpeta de destino en una operación. Después de agrupar, abra el panel Conector de AEM Assets de Adobe Experience Manager, vaya a la carpeta de destino, haga clic en Cargar, seleccione los elementos agrupados como el elemento seleccionado en el cuadro de diálogo Cargar recurso, configure los ajustes de exportación y haga clic en Cargar.

### ¿Cómo puedo navegar por las carpetas del repositorio de AEM Assets desde Figma? {#navigate-aem-folders-figma}

La navegación por carpetas dentro del repositorio de AEM Assets está disponible directamente dentro del panel Conector de AEM Assets de Adobe Experience Manager en Figma. Haga clic en el icono de tres puntos de la ruta de la carpeta para mostrar todas las carpetas principales y secundarias de la jerarquía actual. Seleccione cualquier carpeta de la lista para desplazarse a esa ubicación. Al exportar un diseño a una carpeta de destino diferente, haga clic en Más opciones en la ruta de la carpeta para seleccionar una carpeta alternativa dentro del repositorio de AEM Assets.


**Consulte también**

* [Traducir recursos](/help/assets/translate-assets.md)
* [API HTTP de recursos](/help/assets/mac-api-assets.md)
* [Formatos de archivo compatibles con recursos](/help/assets/file-format-support.md)
* [Buscar recursos](/help/assets/search-assets.md)
* [Recursos de red](/help/assets/use-assets-across-connected-assets-instances.md)
* [Informes de recurso](/help/assets/asset-reports.md)
* [Esquemas de metadatos](/help/assets/metadata-schemas.md)
* [Descarga de recursos](/help/assets/download-assets-from-aem.md)
* [Administración de metadatos](/help/assets/manage-metadata.md)
* [Administración de plantillas de Dynamic Media](/help/assets/dynamic-media/manage-dynamic-media-templates.md)
* [Administrar informes](/help/assets/manage-reports-assets-view.md)
* [Facetas de búsqueda](/help/assets/search-facets.md)
* [Administrar colecciones](/help/assets/manage-collections.md)
* [Importación masiva de metadatos](/help/assets/metadata-import-export.md)
* [Publicación de recursos en AEM y Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

