---
title: Informes sobre el uso y uso compartido de los recursos digitales.
description: Informes sobre los recursos [!DNL Adobe Experience Manager Assets] que le ayudan a comprender el uso, la actividad y el uso compartido de los recursos digitales.
contentOwner: AG
translation-type: tm+mt
source-git-commit: ab9a3bfa3536e25243e9752f9f034e31a57e136c
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 11%

---


# Informes del recurso {#asset-reports}

El sistema de informes de recursos permite evaluar la utilidad de la [!DNL Adobe Experience Manager Assets] implementación. Con [!DNL Assets], puede generar varios informes para sus recursos digitales. Los informes proporcionan información útil sobre el uso del sistema, la forma en que los usuarios interactúan con los recursos y los recursos que se descargan y comparten.

Utilice la información de los informes para derivar métricas de éxito clave y medir la adopción de [!DNL Assets] las mismas en su empresa y por los clientes.

El marco de trabajo de [!DNL Assets] sistema de informes utiliza [!DNL Sling] trabajos para procesar de forma asíncrona las solicitudes de informes de manera ordenada. Es escalable para repositorios grandes. El procesamiento asincrónico de informes aumenta la eficiencia y la velocidad con que se generan los informes.

La interfaz de administración de informes es intuitiva e incluye opciones y controles detallados para acceder a los informes archivados y a los estados de ejecución de los informes de vista (exitosos, fallidos y en cola).

Cuando se genera un informe, se le notifica mediante <!-- through an email (optional) and --> una notificación de bandeja de entrada. Puede vista, descargar o eliminar un informe desde la página con la lista de informes, donde se muestran todos los informes generados previamente.

## Generar informes {#generate-reports}

[!DNL Experience Manager Assets] genera los siguientes informes estándar:

* Cargar
* Descargar
* Vencimiento
* Modificación
* Publicación
* [!DNL Brand Portal] instancias de publicación
* Uso del disco
* Archivos
* Vínculos compartidos

[!DNL Adobe Experience Manager] los administradores pueden generar y personalizar fácilmente estos informes para su implementación. Un administrador puede seguir estos pasos para generar un informe:

1. En [!DNL Experience Manager] la interfaz, haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Informes]**.

   ![Página Herramientas para navegar por el informe de recursos](assets/navigation.png)

1. En la página Informes [!UICONTROL de] recursos, haga clic en **[!UICONTROL Crear]** en la barra de herramientas.
1. En la página **[!UICONTROL Crear informe]** , elija el informe que desee crear y haga clic en **[!UICONTROL Siguiente]**.

   ![Seleccionar tipo de informe](assets/choose_report.png)

   >[!NOTE]
   >
   >Antes de generar un informe de **[!UICONTROL descarga de recursos]**, compruebe que el servicio de descarga de recursos está habilitado. En la consola web (`https://[aem_server]:[port]/system/console/configMgr`), abra la configuración del **[!UICONTROL grabador de eventos de CQ DAM de día]** y seleccione la opción **[!UICONTROL Recurso descargado (DESCARGADO)]** en Tipos de eventos si no está seleccionada.

   >[!NOTE]
   >
   >De forma predeterminada, los fragmentos de contenido y los recursos compartidos de vínculos se incluyen en el informe de [!UICONTROL descarga] de recursos. Seleccione la opción adecuada para crear un informe de recursos compartidos de vínculos o para excluir fragmentos de contenido del informe de descarga.

   >[!NOTE]
   >
   >El informe [!UICONTROL Descargar] muestra detalles de solo los recursos que se descargan tras seleccionarlos individualmente o que se descargan mediante Acción rápida. Sin embargo, no incluye los detalles de los recursos que se encuentran dentro de una carpeta descargada.

1. Configure los detalles del informe, como título, descripción, miniatura y ruta de carpeta, en el repositorio de CRX donde se almacena el informe. De forma predeterminada, la ruta de la carpeta es `/content/dam`. Puede especificar una ruta diferente.

   ![Página para agregar detalles del informe](assets/report_configuration.png)

   Elija el intervalo de fechas del informe.

   Puede elegir generar el informe ahora o en una fecha y hora futuras.

   >[!NOTE]
   >
   >Si decide programar el informe más adelante, asegúrese de especificar la fecha y la hora en los campos Fecha y Hora. Si no especifica ningún valor, el motor de informes lo trata como un informe que se va a generar instantáneamente.

   Los campos de configuración pueden diferir según el tipo de informe que cree. Por ejemplo: el informe Uso del **[!UICONTROL disco]** proporciona opciones para incluir representaciones de recursos al calcular el espacio en disco que utilizan los recursos. Puede optar por incluir o excluir recursos en subcarpetas para el cálculo del uso del disco.

   >[!NOTE]
   >
   >El informe **[!UICONTROL Uso del disco]** no incluye campos de intervalo de fechas porque solo indica el uso actual del espacio en disco.

   ![Página de detalles del informe Uso del disco](assets/disk_usage_configuration.png)

   Al crear el informe **[!UICONTROL Archivos]** , puede incluir o excluir subcarpetas. Sin embargo, no puede incluir representaciones de recursos para este informe.

   ![Página de detalles del informe Archivos](assets/files_report.png)

   El informe **[!UICONTROL Compartir vínculos]** muestra las direcciones URL de los recursos que se comparten con usuarios externos desde [!DNL Assets]. <!-- It includes email ids of the user who shared the assets, emails ids of users with which the assets are shared, share date, and expiration date for the link. --> Las columnas no se pueden personalizar.

   The **[!UICONTROL Link Share]** report, does not include options for sub-folders and renditions because it merely publishes the shared URLs that appear under `/var/dam/share`.

   ![Página de detalles del informe Uso compartido de vínculos](assets/link_share.png)

1. Click **[!UICONTROL Next]** from the toolbar.

1. En la página **[!UICONTROL Configurar columnas]** , se seleccionan algunas columnas para que aparezcan en el informe de forma predeterminada. Puede seleccionar más columnas. Anule la selección de una columna seleccionada para excluirla del informe.

   ![Seleccionar o anular la selección de las columnas del informe](assets/configure_columns.png)

   Para mostrar un nombre de columna personalizado o una ruta de propiedad, configure las propiedades del binario de recursos bajo el `jcr:content` nodo en CRX. También puede agregarla mediante el selector de rutas de propiedad.

   ![Seleccionar o anular la selección de las columnas del informe](assets/custom_columns.png)

1. Click **[!UICONTROL Create]** from the toolbar. Un mensaje notifica que se ha iniciado la generación de informes.
1. En la página Informes [!UICONTROL de] recursos, el estado de generación de informes se basa en el estado actual del trabajo de informe, por ejemplo, [!UICONTROL Éxito], [!UICONTROL Error], [!UICONTROL En cola]o [!UICONTROL Programado]. El mismo estado aparece en la bandeja de entrada de notificaciones.Para vista de la página del informe, haga clic en el vínculo del informe. Como alternativa, seleccione el informe y haga clic en **[!UICONTROL Vista]** en la barra de herramientas.

   ![Un informe generado](assets/report_page.png)

   Haga clic en **[!UICONTROL Descargar]** desde la barra de herramientas para descargar el informe en formato CSV.

## Añadir columnas personalizadas {#add-custom-columns}

Puede agregar columnas personalizadas a los siguientes informes para mostrar más datos según sus requisitos personalizados:

* Cargar
* Descargar
* Vencimiento
* Modificación
* Publicación
* [!DNL Brand Portal] instancias de publicación
* Archivos

Para agregar columnas personalizadas a estos informes, siga estos pasos:

1. En la [!DNL Manager interface], haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Informes]**.
1. En la página Informes [!UICONTROL de] recursos, haga clic en **[!UICONTROL Crear]** en la barra de herramientas.

1. En la página **[!UICONTROL Crear informe]** , elija el informe que desee crear y haga clic en **[!UICONTROL Siguiente]**.
1. Configure los detalles del informe, como título, descripción, miniatura, ruta de carpeta e intervalo de fechas, según corresponda.

1. Para mostrar una columna personalizada, especifique el nombre de la columna debajo de **[!UICONTROL Columnas personalizadas]**.

   ![Especificar el nombre de la columna personalizada del informe](assets/custom_columns-1.png)

1. Añada la ruta de la propiedad bajo el `jcr:content` nodo en CRXDE mediante el selector de rutas de propiedad. También puede escribir la ruta en el campo de ruta de la propiedad.

   ![Asignación de la ruta de la propiedad desde las rutas en jcr:content](assets/property_picker.png)

   Para agregar más columnas personalizadas, haga clic en **[!UICONTROL Añadir]** y repita los pasos 5 y 6.

1. Click **[!UICONTROL Create]** from the toolbar. Un mensaje notifica que se ha iniciado la generación de informes.

## Configurar el servicio de depuración {#configure-purging-service}

Para eliminar los informes que ya no necesite, configure el servicio Depuración de informes DAM desde la consola web para purgar los informes existentes en función de su cantidad y antigüedad.

1. Acceda a la consola web (administrador de configuración) desde `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra la configuración del servicio **[!UICONTROL de depuración de informes]** DAM.
1. Especifique la frecuencia (intervalo de tiempo) del servicio de depuración en el `scheduler.expression.name` campo. También puede configurar la edad y el umbral de cantidad para los informes.
1. Guarde los cambios.
