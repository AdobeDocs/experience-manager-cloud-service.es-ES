---
title: 'Información sobre Assets '
description: Rastree las clasificaciones de usuarios y las estadísticas de uso de las imágenes que se utilizan en sitios web de terceros, campañas de marketing y las soluciones creativas del Adobe.
contentOwner: AG
feature: Información sobre Assets, Informes de Asset
role: Business Practitioner
exl-id: e268453b-e7c0-4aa4-bd29-2686edb5f99a
translation-type: tm+mt
source-git-commit: a42138cd009a85a92e74d98dd808578014361e1d
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 8%

---

# Información sobre Assets {#asset-insights}

Asset Insights realiza un seguimiento de las clasificaciones de usuarios y las estadísticas de uso de las imágenes que se usan en sitios web de terceros, campañas de marketing y soluciones creativas de Adobe. Ayuda a proporcionar perspectivas sobre el rendimiento y la popularidad de las imágenes.

Assets Insights captura los detalles de actividad del usuario, como el número de veces que se clasifica, se hace clic en una imagen y las impresiones (el número de veces que se carga una imagen en el sitio web). Asigna puntuaciones a las imágenes según estas estadísticas. Puede utilizar las puntuaciones y las estadísticas de rendimiento para seleccionar imágenes populares para incluirlas en catálogos, campañas de marketing, etc. Incluso puede formular políticas de archivado y renovación de licencias basadas en estas estadísticas.

Para que Assets Insights capture las estadísticas de uso de las imágenes de un sitio web, debe incluir el código incrustado de la imagen en el código del sitio web.

Para que Asset Insights pueda mostrar las estadísticas de uso de los recursos, configure primero la función para recuperar datos de informes de Adobe Analytics. Para obtener más información, consulte [Configuración de Asset Insights](#configure-asset-insights).

>[!NOTE]
>
>Las perspectivas solo se admiten y se proporcionan para imágenes.

## Ver estadísticas de una imagen {#viewing-statistics-for-an-image}

Puede ver las puntuaciones de Asset Insights desde la página de metadatos.

1. En la interfaz de usuario (IU) de Assets, seleccione la imagen y, a continuación, pulse **[!UICONTROL Propiedades]** en la barra de herramientas.
1. En la página Propiedades, pulse **[!UICONTROL Perspectivas]**.
1. Revise los detalles de uso del recurso en la pestaña **[!UICONTROL Insights]**. La sección **[!UICONTROL Puntuación]** describe el uso total de los recursos y las puntuaciones de rendimiento de un recurso.

   La puntuación de uso describe la cantidad de veces que se utiliza el recurso en varias soluciones.

   La puntuación **[!UICONTROL Impresiones]** es el número de veces que el recurso se carga en el sitio web. El número mostrado en **[!UICONTROL Clicks]** es el número de veces que se hace clic en el recurso.

1. Revise la sección **[!UICONTROL Estadísticas de uso]** para saber de qué entidades formaba parte el recurso y qué soluciones creativas lo utilizaron recientemente. Cuanto mayor sea el uso, buenas serán las posibilidades de que el recurso sea popular entre los usuarios. Los datos de uso se muestran en los siguientes encabezados:

   * **[!UICONTROL Recurso]**: El número de veces que el recurso formaba parte de una colección o un recurso compuesto.
   * **[!UICONTROL Web y dispositivos móviles]**: El número de veces que el recurso formaba parte de sitios web y aplicaciones.
   * **[!UICONTROL Social]**: El número de veces que se usó el recurso en soluciones como Adobe Social y Adobe Campaign.
   * **[!UICONTROL Correo electrónico]**: Número de veces que el recurso se ha utilizado en campañas de correo electrónico.

   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >Debido a que la función Asset Insights generalmente recupera los datos de Soluciones de Adobe Analytics de forma periódica, es posible que la sección Soluciones no muestre los datos más recientes. El período de tiempo durante el cual se muestran los datos depende de la programación de la operación de recuperación que Asset Insights ejecuta para recuperar datos de Analytics.

1. Para ver las estadísticas de rendimiento del recurso gráficamente durante un período de tiempo, seleccione el período en la sección **[!UICONTROL Estadísticas de rendimiento]**. Los detalles, incluidos los clics y las impresiones, se muestran como líneas de tendencia de un gráfico.

   ![Chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >A diferencia de los datos de la sección Soluciones , la sección Estadísticas de rendimiento muestra los datos más recientes.

1. Para obtener el código incrustado del recurso que incluye en los sitios web para obtener datos de rendimiento, pulse o haga clic en **[!UICONTROL Obtener código incrustado]** debajo de la miniatura del recurso. <!-- For more information on how to include your Embed code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

   ![imagen_1-98](assets/chlimage_1-98.png)

## Ver estadísticas agregadas para imágenes {#viewing-aggregate-statistics-for-images}

Puede ver las puntuaciones de todos los recursos de una carpeta simultáneamente mediante la **[!UICONTROL Vista de la información]**.

1. En la interfaz de usuario de Assets, vaya a la carpeta que contiene los recursos para los que desea ver información.
1. Pulse o haga clic en el icono Diseño de la barra de herramientas y, a continuación, elija **[!UICONTROL Vista de perspectivas]**.
1. La página muestra las puntuaciones de uso de los recursos. Compare las clasificaciones de los distintos recursos y extraiga perspectivas.

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.

## Schedule background job {#scheduling-background-job}

Asset Insights fetches usage data for assets from Adobe Analytics report suites in a periodic manner. By default, Asset Insights runs a background job every 24 hours at 2 AM to the fetch data. However, you can modify both the frequency and the time by configuring the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service from the web console.

1. Click the [!DNL Experience Manager] logo, and go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Open the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service configuration.

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. Specify the desired scheduler frequency and the start time for the job in the property scheduler expression. Save the changes.
-->

## Configurar Asset Insights {#configure-asset-insights}

[!DNL Experience Manager Assets] recupera los datos de uso relacionados con los recursos digitales utilizados por sitios web de terceros desde  [!DNL Adobe Analytics]. Para permitir que Asset Insights recupere estos datos y genere perspectivas, configure primero la función para integrarla con [!DNL Adobe Analytics].

>[!NOTE]
>
>Las perspectivas solo se admiten y se proporcionan para imágenes.

1. En [!DNL Experience Manager], haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]**.

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. Haga clic en la tarjeta **[!UICONTROL Configuración de información]**.
1. En el asistente, seleccione un centro de datos y proporcione sus credenciales, incluidos el nombre de su organización, el nombre de usuario y el secreto compartido.

   ![Configuración de Adobe Analytics para Assets Insights en  [!DNL Experience Manager]](assets/insights_config2.png)

   *Figura: Configuración de Adobe Analytics para Assets Insights en[!DNL Experience Manager]*

1. Pulse o haga clic en **[!UICONTROL Autenticar]**. Después de que [!DNL Experience Manager] autentique sus credenciales, en la lista **[!UICONTROL Grupo de informes]**, elija un grupo de informes de Adobe Analytics desde el que desea que Asset Insights recupere datos. Haga clic en **[!UICONTROL Agregar]**.
1. Después de que [!DNL Experience Manager] configure el grupo de informes, pulse **[!UICONTROL Listo]**.

### Rastreador de páginas {#page-tracker}

Después de configurar la cuenta de Adobe Analytics, se genera el código Rastreador de páginas . Para permitir que Assets Insights rastree los [!DNL Experience Manager] recursos utilizados en sitios web de terceros, incluya el código del rastreador de páginas en el código del sitio web. Utilice la utilidad Rastreador de páginas de Assets para generar el código de seguimiento de páginas. <!--  For more information on how to include your Page Tracker code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

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
