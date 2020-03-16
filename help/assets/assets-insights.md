---
title: 'Información sobre Assets '
description: Descubra cómo la función de perspectivas de recursos le permite realizar un seguimiento de las clasificaciones de usuarios y las estadísticas de uso de las imágenes que se utilizan en sitios web de terceros, campañas de marketing y soluciones creativas de Adobe.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 6998ee5f3c1c1563427e8739998effe0eba867fc

---


# Información sobre Assets {#asset-insights}

Asset Insights rastrea las clasificaciones de usuarios y las estadísticas de uso de las imágenes que se utilizan en sitios web de terceros, campañas de marketing y soluciones creativas de Adobe. Ayuda a proporcionar perspectivas sobre el rendimiento y la popularidad de las imágenes.

Assets Insights captura los detalles de la actividad del usuario, como el número de veces que se califica, hace clic e imprime una imagen (el número de veces que se carga una imagen en el sitio web). Asigna puntuaciones a las imágenes en función de estas estadísticas. Puede utilizar las estadísticas de rendimiento y puntuaciones para seleccionar imágenes populares para incluirlas en catálogos, campañas de marketing, etc. Puede incluso formular políticas de archivado y renovación de licencias basadas en estas estadísticas.

Para que Assets Insights capture estadísticas de uso de imágenes de un sitio web, debe incluir el código incrustado de la imagen en el código del sitio web.

Para permitir que Asset Insights muestre las estadísticas de uso de los recursos, primero configure la función para recuperar datos de informes de Adobe Analytics. Para obtener más información, consulte [Configuración de perspectivas](#configure-asset-insights)de recursos.

>[!NOTE]
>
>Las perspectivas solo son compatibles y se proporcionan para imágenes.

## Ver estadísticas de una imagen {#viewing-statistics-for-an-image}

Puede ver las puntuaciones de perspectivas de recursos desde la página de metadatos.

1. En la interfaz de usuario de Recursos, seleccione la imagen y, a continuación, toque **[!UICONTROL Propiedades]** en la barra de herramientas.
1. En la página Propiedades, toque **[!UICONTROL Perspectivas]**.
1. Revise los detalles de uso del recurso en la ficha **[!UICONTROL Perspectivas]** . La sección **[!UICONTROL Puntuación]** describe el uso total de recursos y las recuperaciones de rendimiento de un recurso.

   La puntuación de uso describe la cantidad de veces que se utiliza el recurso en varias soluciones.

   La puntuación de **[!UICONTROL impresiones]** es el número de veces que el recurso se carga en el sitio web. El número que se muestra en **[!UICONTROL Clics]** es el número de veces que se hace clic en el recurso.

1. Revise la sección Estadísticas **[!UICONTROL de]** uso para saber de qué entidades formaba parte el recurso y qué soluciones creativas lo utilizaron recientemente. Cuanto mayor sea el uso, buenas serán las posibilidades de que el recurso sea popular entre los usuarios. Los datos de uso se muestran en los siguientes encabezados:

   * **[!UICONTROL Recurso]**: Número de veces que el recurso formaba parte de una colección o un recurso compuesto.
   * **[!UICONTROL Web y móvil]**: El número de veces que el recurso formaba parte de sitios web y aplicaciones.
   * **[!UICONTROL Social]**: El número de veces que el recurso se ha utilizado en soluciones como Adobe Social y Adobe Campaign.
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

1. Para obtener el código incrustado del recurso que incluye en los sitios web con el fin de obtener datos de rendimiento, toque o haga clic en **[!UICONTROL Obtener código]** incrustado debajo de la miniatura del recurso. <!-- For more information on how to include your Embed code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

   ![chlimage_1-98](assets/chlimage_1-98.png)

## Ver estadísticas agregadas de imágenes {#viewing-aggregate-statistics-for-images}

Puede ver las puntuaciones de todos los recursos de una carpeta simultáneamente mediante la **[!UICONTROL Vista de la información]**.

1. En la interfaz de usuario de Recursos, desplácese a la carpeta que contiene los recursos para los que desea ver perspectivas.
1. Toque o haga clic en el icono Diseño de la barra de herramientas y, a continuación, elija **[!UICONTROL Vista]** de perspectivas.
1. La página muestra las puntuaciones de uso de los recursos. Compare las clasificaciones de los distintos recursos y obtenga perspectivas.

## Programar trabajo en segundo plano {#scheduling-background-job}

Asset Insights obtiene datos de uso de recursos de los grupos de informes de Adobe Analytics de forma periódica. De forma predeterminada, Asset Insights ejecuta un trabajo en segundo plano cada 24 horas a las 2 de la madrugada para recuperar datos. Sin embargo, puede modificar tanto la frecuencia como la hora configurando el servicio Trabajo **[!UICONTROL de sincronización de informes de rendimiento de recursos de]** Adobe CQ DAM desde la consola web.

1. Pulse el logotipo de AEM y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.
1. Abra la configuración del servicio Trabajo **[!UICONTROL de sincronización de informes de rendimiento de recursos DAM de]** Adobe CQ.

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. Especifique la frecuencia del programador que desee y la hora de inicio del trabajo en la expresión del programador de propiedades. Guarde los cambios.

## Configurar perspectivas de recursos {#configure-asset-insights}

Recursos Adobe Experience Manager (AEM) obtiene datos de uso de los recursos de AEM utilizados por sitios web de terceros desde Adobe Analytics. Para habilitar Asset Insights para recuperar estos datos y generar perspectivas, primero configure la función para integrarla con Adobe Analytics.

>[!NOTE]
>
>Las perspectivas solo son compatibles y se proporcionan para imágenes.

1. En AEM, haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]**.

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. Haga clic en la tarjeta **[!UICONTROL Configuración de información]**.
1. En el asistente, seleccione un centro de datos y proporcione sus credenciales, incluido el nombre de su organización, el nombre de usuario y Shared Secret.

   ![Configuración de Adobe Analytics para perspectivas de recursos en AEM](assets/insights_config2.png)

   *Figura: Configuración de Adobe Analytics para perspectivas de recursos en AEM*

1. Pulse o haga clic en **[!UICONTROL Autenticar]**. Una vez que AEM haya autenticado sus credenciales, en la lista Grupo **[!UICONTROL de]** informes, elija un grupo de informes de Adobe Analytics desde el que desee que Asset Insights obtenga datos. Haga clic en **[!UICONTROL Agregar]**.
1. Una vez que AEM haya configurado el grupo de informes, toque **[!UICONTROL Listo]**.

### Rastreador de páginas {#page-tracker}

Después de configurar la cuenta de Adobe Analytics, se genera el código de rastreador de páginas. Para habilitar Assets Insights a fin de rastrear los recursos de AEM utilizados en sitios web de terceros, incluya el código del rastreador de páginas en el código del sitio web. Utilice la utilidad Rastreador de páginas de Recursos AEM para generar el código de seguimiento de páginas. <!--  For more information on how to include your Page Tracker code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

1. En AEM, haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]**.

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. En la página **[!UICONTROL Navegación]**, haga clic en la tarjeta **[!UICONTROL Rastreador de páginas de perspectivas]**.
1. Haga clic en **[!UICONTROL Descargar]** para descargar el código del rastreador de páginas.

<!--

## Using demo package for Asset Insights {#using-demo-package-for-asset-insights}

Using the demo package, you can enable Adobe Asset Insights to capture data from and generate insights for a sample web page.

1. Configure Asset Insights using the instructions in [Configure Asset Insights](#configure-asset-insights).
1. Download the sample AEM Assets package from below and install the package from CRXDE package manager.

   [Get File](assets/insightsdemo.zip)

1. Download the ZIP file containing the sample web page from below and extract on your local file system.

   [Get File](assets/demosite.zip)

1. Click the web page to open it in the web browser.

   >[!CAUTION]
   >
   >Web Page is configured to load asset from the localhost server . In case your server is running somewhere else change server address from localhost to server address in the HTML content of the web page.

   >[!NOTE]
   >
   >The external web page can be in AEM itself.

-->
