---
title: 'Información sobre Assets '
description: Descubra cómo la función de perspectivas de recursos le permite realizar un seguimiento de las clasificaciones de usuarios y las estadísticas de uso de las imágenes que se utilizan en sitios web de terceros, campañas de marketing y soluciones creativas de Adobe.
contentOwner: AG
translation-type: tm+mt
source-git-commit: ce22a7ba95942881b90a4f3f22d89bcd35b5e559
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Información sobre Assets {#asset-insights}

Asset Insights rastrea las clasificaciones de usuarios y las estadísticas de uso de las imágenes que se utilizan en sitios web de terceros, campañas de marketing y soluciones creativas de Adobe. Ayuda a proporcionar perspectivas sobre el rendimiento y la popularidad de las imágenes.

Assets Insights captura los detalles de la actividad del usuario, como el número de veces que se califica, hace clic e imprime una imagen (el número de veces que se carga una imagen en el sitio web). Asigna puntuaciones a las imágenes en función de estas estadísticas. Puede utilizar las estadísticas de rendimiento y puntuaciones para seleccionar imágenes populares para incluirlas en catálogos, campañas de marketing, etc. Puede incluso formular políticas de archivado y renovación de licencias basadas en estas estadísticas.

Para que Assets Insights capture estadísticas de uso de imágenes de un sitio web, debe incluir el código incrustado de la imagen en el código del sitio web.

Para permitir que Asset Insights muestre las estadísticas de uso de los recursos, primero configure la función para recuperar datos de sistema de informes de Adobe Analytics. Para obtener más información, consulte [Configuración de perspectivas de recursos](#configure-asset-insights).

>[!NOTE]
>
>Las perspectivas solo son compatibles y se proporcionan para imágenes.

## Estadísticas de vista para una imagen {#viewing-statistics-for-an-image}

Puede realizar la vista de las puntuaciones de perspectivas de recursos desde la página de metadatos.

1. En la interfaz de usuario de Recursos (IU), seleccione la imagen y, a continuación, toque **[!UICONTROL Propiedades]** en la barra de herramientas.
1. En la página Propiedades, toque **[!UICONTROL Perspectivas]**.
1. Revise los detalles de uso del recurso en la ficha **[!UICONTROL Perspectivas]**. La sección **[!UICONTROL Puntuación]** describe el uso total de los recursos y las recuperaciones de rendimiento de un recurso.

   La puntuación de uso describe la cantidad de veces que se utiliza el recurso en varias soluciones.

   La puntuación **[!UICONTROL Impresiones]** es el número de veces que el recurso se carga en el sitio Web. El número que se muestra en **[!UICONTROL Clics]** es el número de veces que se hace clic en el recurso.

1. Revise la sección **[!UICONTROL Estadísticas de uso]** para saber de qué entidades formaba parte el recurso y qué soluciones creativas lo utilizaron recientemente. Cuanto mayor sea el uso, buenas serán las posibilidades de que el recurso sea popular entre los usuarios. Los datos de uso se muestran en los siguientes encabezados:

   * **[!UICONTROL Recurso]**: Número de veces que el recurso formaba parte de una colección o un recurso compuesto.
   * **[!UICONTROL Web y móvil]**: El número de veces que el recurso formaba parte de sitios web y aplicaciones.
   * **[!UICONTROL Social]**: El número de veces que se ha utilizado el recurso en soluciones como Adobe Social y Adobe Campaign.
   * **[!UICONTROL Correo electrónico]**: El número de veces que el recurso se ha utilizado en campañas de correo electrónico.

   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >Debido a que la función de perspectivas de recursos generalmente recopila los datos de soluciones de Adobe Analytics de forma periódica, es posible que la sección Soluciones no muestre los datos más recientes. El período de tiempo durante el cual se muestran los datos depende de la programación de la operación de recuperación que se ejecuta Asset Insights para recuperar datos de Analytics.

1. Para ver las estadísticas de rendimiento del recurso gráficamente durante un período de tiempo, seleccione el período en la sección **[!UICONTROL Estadísticas de rendimiento]**. Los detalles, incluidos los clics y las impresiones, se muestran como líneas de tendencia de un gráfico.

   ![climage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >A diferencia de los datos de la sección Soluciones, la sección Estadísticas de rendimiento muestra los datos más recientes.

1. Para obtener el código incrustado del recurso que incluye en los sitios web con el fin de obtener datos de rendimiento, toque o haga clic en **[!UICONTROL Obtener código incrustado]** debajo de la miniatura del recurso. <!-- For more information on how to include your Embed code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

   ![chlimage_1-98](assets/chlimage_1-98.png)

## Estadísticas acumuladas de vista para imágenes {#viewing-aggregate-statistics-for-images}

Puede ver las puntuaciones de todos los recursos de una carpeta simultáneamente mediante la **[!UICONTROL Vista de la información]**.

1. En la interfaz de usuario de Recursos, desplácese a la carpeta que contenga los recursos para los que desee realizar la vista.
1. Toque o haga clic en el icono Diseño de la barra de herramientas y, a continuación, elija **[!UICONTROL Vista de perspectivas]**.
1. La página muestra las puntuaciones de uso de los recursos. Compare las clasificaciones de los distintos recursos y obtenga perspectivas.

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.

## Schedule background job {#scheduling-background-job}

Asset Insights fetches usage data for assets from Adobe Analytics report suites in a periodic manner. By default, Asset Insights runs a background job every 24 hours at 2 AM to the fetch data. However, you can modify both the frequency and the time by configuring the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service from the web console.

1. Click the [!DNL Experience Manager] logo, and go to **[!UICONTROL Tools]** &gt; **[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.
1. Open the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service configuration.

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. Specify the desired scheduler frequency and the start time for the job in the property scheduler expression. Save the changes.
-->

## Configurar perspectivas de recursos {#configure-asset-insights}

[!DNL Experience Manager Assets] recoge datos de uso de recursos digitales utilizados por sitios web de terceros desde  [!DNL Adobe Analytics]. Para habilitar Asset Insights para recuperar estos datos y generar perspectivas, primero configure la función para integrarla con [!DNL Adobe Analytics].

>[!NOTE]
>
>Las perspectivas solo son compatibles y se proporcionan para imágenes.

1. En [!DNL Experience Manager], haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]**.

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. Haga clic en la tarjeta **[!UICONTROL Configuración de información]**.
1. En el asistente, seleccione un centro de datos y proporcione sus credenciales, incluido el nombre de su organización, el nombre de usuario y Shared Secret.

   ![Configurar Adobe Analytics para Assets Insights en  [!DNL Experience Manager]](assets/insights_config2.png)

   *Figura: Configurar Adobe Analytics para Assets Insights en[!DNL Experience Manager]*

1. Pulse o haga clic en **[!UICONTROL Autenticar]**. Después de que [!DNL Experience Manager] autentique las credenciales, en la lista **[!UICONTROL Grupo de informes]**, elija un grupo de informes de Adobe Analytics desde donde desee que Asset Insights recopile los datos. Haga clic en **[!UICONTROL Agregar]**.
1. Después de que [!DNL Experience Manager] configure el grupo de informes, toque **[!UICONTROL Listo]**.

### Rastreador de páginas {#page-tracker}

Después de configurar la cuenta de Adobe Analytics, se genera el código Rastreador de páginas. Para permitir que Assets Insights rastree los [!DNL Experience Manager] recursos utilizados en sitios web de terceros, incluya el código del rastreador de páginas en el código del sitio web. Utilice la utilidad Rastreador de páginas en Recursos para generar el código de rastreador de páginas. <!--  For more information on how to include your Page Tracker code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

1. En [!DNL Experience Manager], haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]**.

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. En la página **[!UICONTROL Navegación]**, haga clic en la tarjeta **[!UICONTROL Rastreador de páginas de perspectivas]**.
1. Haga clic en **[!UICONTROL Descargar]** para descargar el código del rastreador de páginas.

<!--

## Using demo package for Asset Insights {#using-demo-package-for-asset-insights}

Using the demo package, you can enable Adobe Asset Insights to capture data from and generate insights for a sample web page.

1. Configure Asset Insights using the instructions in [Configure Asset Insights](#configure-asset-insights).
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
