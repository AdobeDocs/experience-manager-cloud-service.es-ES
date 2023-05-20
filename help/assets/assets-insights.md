---
title: Assets Insights
description: Rastree las clasificaciones de los usuarios y las estadísticas de uso de las imágenes que se utilizan en sitios web de terceros, campañas de marketing y soluciones creativas de Adobe.
contentOwner: AG
feature: Asset Insights,Asset Reports
role: User,Leader
exl-id: e268453b-e7c0-4aa4-bd29-2686edb5f99a
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 9%

---

# Assets Insights {#asset-insights}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/asset-insights.html?lang=en) |
| AEM as a Cloud Service | Este artículo |

La funcionalidad de perspectivas de recursos le permite hacer un seguimiento de las clasificaciones de los usuarios y las estadísticas de uso de las imágenes que se utilizan en sitios web de terceros, campañas de marketing y soluciones creativas de Adobe. Ayuda a obtener información sobre el rendimiento y la popularidad de las imágenes.

Assets Insights captura los detalles de la actividad del usuario, como el número de veces que se clasifica, hace clic y genera impresiones una imagen (el número de veces que se carga una imagen en el sitio web). Asigna puntuaciones a las imágenes en función de estas estadísticas. Puede utilizar las puntuaciones y las estadísticas de rendimiento para seleccionar imágenes populares para incluirlas en catálogos, campañas de marketing, etc. Incluso puede formular políticas de archivado y renovación de licencias basadas en estas estadísticas.

Para que Assets Insights capture estadísticas de uso de imágenes de un sitio web, debe incluir el código incrustado de la imagen en el código del sitio web.

Para permitir que Assets Insights muestre las estadísticas de uso de los recursos, configure primero la función para recuperar los datos de informes de [!DNL Adobe Analytics]. Para obtener más información, consulte [Configurar perspectivas de recursos](#configure-asset-insights). Para utilizar esta función, compre [!DNL Adobe Analytics] licencia por separado.

>[!NOTE]
>
>Las perspectivas son compatibles y se proporcionan solo para imágenes.

## Visualización de estadísticas de una imagen {#viewing-statistics-for-an-image}

Puede ver las puntuaciones de Assets Insights desde la página de metadatos.

1. En la interfaz de usuario de Assets, seleccione la imagen y haga clic en **[!UICONTROL Propiedades]** en la barra de herramientas.
1. En la página Propiedades, haga clic en **[!UICONTROL Insights]**.
1. Revise los detalles de uso del recurso en la **[!UICONTROL Insights]** pestaña. El **[!UICONTROL Puntuación]** describe el uso total de recursos y las puntuaciones de rendimiento de un recurso

   La puntuación de uso describe el número de veces que el recurso se utiliza en varias soluciones.

   El **[!UICONTROL Impresiones]** la puntuación es el número de veces que el recurso se carga en el sitio web. El número mostrado debajo de **[!UICONTROL Clics]** es el número de veces que se hace clic en el recurso.

1. Revise la **[!UICONTROL Estadísticas de uso]** para saber de qué entidades formaba parte el recurso y qué soluciones creativas lo utilizaron recientemente. Cuanto mayor sea el uso, más buenas serán las probabilidades de que el recurso sea popular entre los usuarios. Los datos de uso se muestran bajo los siguientes encabezados:

   * **[!UICONTROL Recurso]**: el número de veces que el recurso formaba parte de una colección o de un recurso compuesto.
   * **[!UICONTROL Web y dispositivos móviles]**: El número de veces que el recurso formaba parte de sitios web y aplicaciones.
   * **[!UICONTROL Social]**: El número de veces que el recurso se utilizó en otras soluciones como una [!DNL Adobe Campaign].
   * **[!UICONTROL Correo electrónico]**: El número de veces que el recurso se utilizó en campañas de correo electrónico.

   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >Debido a que la función de perspectivas de recursos generalmente obtiene los datos de soluciones de [!DNL Adobe Analytics] de forma periódica, es posible que la sección Soluciones no muestre los datos más recientes. El período de tiempo para el que se muestran los datos depende de la programación de la operación de recuperación que ejecuta Assets Insights para recuperar datos de Analytics.

1. Para ver las estadísticas de rendimiento del recurso gráficamente durante un período de tiempo, seleccione el período en la sección **[!UICONTROL Estadísticas de rendimiento]**. Los detalles, incluidos los clics y las impresiones, se muestran como líneas de tendencia de un gráfico.

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >A diferencia de los datos de la sección Soluciones, la sección Estadísticas de rendimiento muestra los datos más recientes.

1. Para obtener el código incrustado del recurso que incluye en los sitios web para obtener datos de rendimiento, haga clic en **[!UICONTROL Obtener código incrustado]** debajo de la miniatura del recurso. <!-- For more information on how to include your Embed code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

   ![chlimage_1-98](assets/chlimage_1-98.png)

## Visualización de estadísticas acumuladas de imágenes {#viewing-aggregate-statistics-for-images}

Puede ver las puntuaciones de todos los recursos de una carpeta simultáneamente mediante la **[!UICONTROL Vista de la información]**.

1. En la interfaz de usuario de Assets, vaya a la carpeta que contiene los recursos para los que desea ver información.
1. Haga clic en **[!UICONTROL Diseño]** en la barra de herramientas y, a continuación, elija **[!UICONTROL Vista de perspectivas]**.
1. La página muestra las puntuaciones de uso de los recursos. Compare las clasificaciones de los distintos recursos y obtenga información.

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.

## Schedule background job {#scheduling-background-job}

Assets Insights fetches usage data for assets from Adobe Analytics report suites in a periodic manner. By default, Assets Insights runs a background job every 24 hours at 2 AM to the fetch data. However, you can modify both the frequency and the time by configuring the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service from the web console.

1. Click the [!DNL Experience Manager] logo, and go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Open the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service configuration.

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. Specify the desired scheduler frequency and the start time for the job in the property scheduler expression. Save the changes.
-->

## Configurar perspectivas de recursos {#configure-asset-insights}

[!DNL Experience Manager Assets] obtiene datos de uso de recursos digitales utilizados por sitios web de terceros de [!DNL Adobe Analytics]. Para permitir que Assets Insights recupere estos datos y genere perspectivas, configure primero la función para integrarla con [!DNL Adobe Analytics].

>[!NOTE]
>
>Las perspectivas solo son compatibles y se proporcionan para las imágenes.

1. Entrada [!DNL Experience Manager], haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]**.

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. Haga clic en la tarjeta **[!UICONTROL Configuración de información]**.

1. Para obtener la información de acceso al servicio web de Analytics, vaya a **[!UICONTROL Analytics]** > **[!UICONTROL Administrador]** > **[!UICONTROL Herramientas de administración]** > **[!UICONTROL Configuración de empresa]** > **[!UICONTROL Servicios web]** y copie el **[!UICONTROL Secreto compartido]** clave.

   En el asistente, seleccione la **[!UICONTROL Centro de datos]** y proporcione el nombre para mostrar del **[!UICONTROL Compañía]**, Servicios Web **[!UICONTROL Nombre de usuario]** y pegue el **[!UICONTROL Secreto compartido]** clave.

   Clic **[!UICONTROL Autenticar]**.

   ![Configuración de Adobe Analytics para las perspectivas de recursos en [!DNL Experience Manager]](assets/analytics-insight-config.png)

   *Figura: Configuración de Adobe Analytics para las perspectivas de recursos en[!DNL Experience Manager]*

1. Si la autenticación se realiza correctamente, los grupos de informes aparecen en la lista desplegable. Seleccione el Adobe Analytics **[!UICONTROL Grupo de informes]** de donde desee que Assets Insights recupere los datos. Clic **[!UICONTROL Añadir]**.

1. Después [!DNL Experience Manager] Para configurar el grupo de informes, haga clic en **[!UICONTROL Listo]**.

Para obtener más información, consulte [Servicios web de Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/admin/company-settings/web-services-admin.html#api-access-information).

### Rastreador de página {#page-tracker}

Después de configurar la cuenta de Adobe Analytics, se genera el código de seguimiento de página. Para permitir que Assets Insights rastree el [!DNL Experience Manager] Los recursos utilizados en sitios web de terceros incluyen el código de rastreador de páginas en el código del sitio web. Utilice la utilidad Rastreador de páginas de Assets para generar el código de rastreador de páginas. <!--  For more information on how to include your Page Tracker code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

1. Entrada [!DNL Experience Manager], haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]**.

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. En la página **[!UICONTROL Navegación]**, haga clic en la tarjeta **[!UICONTROL Rastreador de páginas de perspectivas]**.
1. Clic **[!UICONTROL Descargar]** para descargar el código de rastreador de página.

<!--
Add page tracker code, CQDOC-18045, 30/07/2021
-->
El siguiente fragmento de código de ejemplo muestra el código de seguimiento de página incluido en una página web de ejemplo:

```xml
 <head>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/sitecatalyst/appmeasurement.js"></script>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/foundation/assetinsights/pagetracker.js"></script>
            <script type="text/javascript">
                                assetAnalytics.attrTrackable = 'trackable';
                assetAnalytics.defaultTrackable = false;
                assetAnalytics.attrAssetID = 'aem-asset-id';
                assetAnalytics.assetImpressionPollInterval = 200; // interval in millis
                assetAnalytics.charsLimitForGET = 2000; // bytes
                assetAnalytics.dispatcher.init("assetstesting","abc.net","bee","list1","eVar3","event8","event7");
            </script>

 </head>
```



<!--

## Using demo package for Assets Insights {#using-demo-package-for-asset-insights}

Using the demo package, you can enable Adobe Assets Insights to capture data from and generate insights for a sample web page.

1. Configure Assets Insights using the instructions in [Configure Assets Insights](#configure-asset-insights).
1. Download the sample [!DNL Experience Manager Assets] package from below and install the package from CRXDE package manager.

   [Get File](assets/insightsdemo.zip)

1. Download the ZIP file containing the sample web page from below and extract on your local file system.

   [Get File](assets/demosite.zip)

1. Click the web page to open it in the web browser.

   >[!CAUTION]
   >
   >Web Page is configured to load asset from the localhost server . In case your server is running somewhere else change server address from localhost to server address in the HTML content of the web page.

   >[!NOTE]
   >
   >The external web page can be in [!DNL Experience Manager] itself.

-->

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
