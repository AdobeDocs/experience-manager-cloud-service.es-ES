---
title: Integrar [!DNL AEM Assets] con [!DNL Figma].
description: Aprenda a integrar [!DNL AEM Assets] con [!DNL Figma] para acceder a los recursos de su organización y utilizarlos en el flujo de trabajo de  [!DNL Figma] diseño.
hide: false
role: User
source-git-commit: 25434ebc76096055940d8d85640b28ce4db36d3a
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 10%

---


# Integrar [!DNL AEM Assets] con [!DNL Figma]{#integrate-aem-assets-with-figma}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime y Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integración de AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>New</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Extensibilidad de la IU</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar Dynamic Media Prime y Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Prácticas recomendadas de búsqueda</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Prácticas recomendadas de metadatos</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Centro de contenido</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funciones de OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentación de desarrollador de AEM Assets</b></a>
        </td>
    </tr>
</table>

[!DNL AEM Assets] se integra de forma nativa con [!DNL Figma], lo que permite a los diseñadores acceder directamente a los recursos almacenados en [!DNL AEM Assets] desde la interfaz de usuario de [!DNL Figma]. Puede colocar contenido administrado en [!DNL AEM Assets] en el lienzo [!DNL Figma] y, a continuación, guardar contenido nuevo o editado en el repositorio [!DNL AEM Assets].

## Antes de empezar{#prerequisites-for-aem-assets-and-figma-integration}

* La versión mínima de AEM requerida es `19149`.

* Debe tener licencias válidas de [!DNL AEM Assets] y [!DNL Figma] para integrar [!DNL AEM Assets] con [!DNL Figma].

## Acceder A [!UICONTROL Conector De Assets De Adobe Experience Manager (AEM)]{#access-aem-assets-connector}

Ejecute los siguientes pasos para acceder a [!UICONTROL Adobe Experience Manager (AEM) Assets Connector]:

1. En la página de inicio de [!DNL Figma], haga clic en **[!UICONTROL Acciones]** en la barra de herramientas situada en la parte inferior del lienzo y busque [!DNL Adobe Experience Manager (AEM) Assets Connector] en la barra de búsqueda disponible en el cuadro de diálogo.
1. Seleccione [!DNL Adobe Experience Manager (AEM) Assets Connector] para mostrar el panel [!DNL Adobe Experience Manager (AEM) Assets Connector]. [Importe [!DNL AEM] recursos en su [!DNL Figma] lienzo](#import-aem-assets-into-figma-workflow) mediante este panel.
   ![acciones](/help/assets/assets/actions-on-figma.png)
También puedes acceder a [[!DNL Adobe Experience Manager (AEM) Assets Connector]](https://www.figma.com/community/plugin/1512561378275712210/adobe-experience-manager-aem-assets-connector), disponible en la comunidad [!DNL Figma], hacer clic en **[!UICONTROL Abrir en...]**, seleccionar un archivo reciente o crear uno nuevo y hacer clic en **[!UICONTROL Ejecutar]** para acceder al panel [!DNL Adobe Experience Manager (AEM) Assets Connector].
   ![plugin-page-on-figma-community](/help/assets/assets/plugin-page-on-figma-community.png)

>[!NOTE]
>
> [Póngase en contacto con el Soporte técnico de Adobe](https://helpx.adobe.com/es/contact.html) para obtener ayuda si ve un mensaje de **[!UICONTROL Error de red]** después de iniciar sesión en su entorno de [!DNL AEM].

## Importar [!DNL AEM] recursos al lienzo [!DNL Figma]{#import-aem-assets-into-figma-workflow}

[Acceda al [[!UICONTROL panel]](#access-aem-assets-connector) del conector Assets de Adobe Experience Manager (AEM)] dentro de su interfaz de diseño de [!DNL Figma] y haga lo siguiente:

1. Busque recursos en el panel [!UICONTROL Conector de Assets de Adobe Experience Manager (AEM)]. Para obtener más información, consulte [uso del Selector de recursos](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector#using-asset-selector).

1. Arrastre y suelte el recurso en el lienzo o selecciónelo y haga clic en **[!UICONTROL Seleccionar]** para llevar el recurso al lienzo.

1. Haga clic en ![tres puntos](/help/assets/assets/three-dots.svg) en la ruta de la carpeta para mostrar todas las carpetas principales y secundarias de la jerarquía actual. Seleccione una carpeta para desplazarse a esa ubicación.
   ![tres puntos](/help/assets/assets/assets-folder-structure.png)

Una vez que el diseño de Figma esté listo, puede [exportar el recurso al repositorio de AEM Assets](#export-figma-design-to-aem-assets-folder).

## Exportar recursos al repositorio [!DNL AEM Assets]{#export-figma-design-to-aem-assets-folder}

[Acceda al [[!UICONTROL panel]](#access-aem-assets-connector) del conector Assets de Adobe Experience Manager (AEM)] dentro de su interfaz de diseño de [!DNL Figma] y ejecute los siguientes pasos para exportar su diseño al repositorio de [!DNL AEM Assets]:

1. Vaya a la carpeta de destino donde desea guardar el diseño de [!DNL Figma]. Si ya se encuentra dentro de una carpeta, haga clic en Más opciones (![tres puntos](/help/assets/assets/three-dots.svg)) en la ruta de la carpeta para seleccionar una carpeta de destino diferente.
1. Opcional: agrupe los recursos en el lienzo para seleccionarlos como una sola unidad que cargar en la carpeta.
1. Haga clic en ![cargar archivo](/help/assets/assets/upload-icon.svg) **[!UICONTROL Cargar]** para mostrar el cuadro de diálogo **[!UICONTROL Cargar recurso]**.
1. En el cuadro de diálogo, especifique un nombre de archivo, elija un formato de archivo, seleccione **[!UICONTROL Elemento seleccionado]** o **[!UICONTROL Página]** y haga clic en **[!UICONTROL Cargar]** para cargar el recurso seleccionado o todo el diseño en la carpeta de destino.
   ![cargar diseño figma](/help/assets/assets/upload-figma-design.png)

## Puntos importantes que debe tener en cuenta{#Limitations-of-using-aem-assets-into-figma}

Esta integración tiene actualmente las siguientes limitaciones:

* Para importar [!DNL AEM] recursos en Figma, los formatos admitidos son **JPEG**, **PNG**.
* Para exportar diseños de [!DNL Figma] a [!DNL AEM Assets], los formatos admitidos son **PNG**, **PDF**, **JPG**, **SVG**.



