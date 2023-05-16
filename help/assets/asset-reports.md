---
title: Informes sobre uso y uso compartido
description: Informes sobre sus recursos en [!DNL Adobe Experience Manager Assets] que le ayudan a comprender el uso, la actividad y el uso compartido de sus recursos digitales.
contentOwner: AG
feature: Asset Reports,Asset Management
role: Admin,User
exl-id: ef617b01-0019-4379-8d58-c03215d7e28f
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 9%

---

# Informes de Asset {#asset-reports}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/asset-reports.html?lang=en) |
| AEM as a Cloud Service | Este artículo |

Los informes de recursos le permiten evaluar la utilidad de su [!DNL Adobe Experience Manager Assets] implementación. con [!DNL Assets], puede generar varios informes para los recursos digitales. Los informes proporcionan información útil sobre el uso del sistema, cómo interactúan los usuarios con los recursos y cuáles son <!-- downloaded and --> compartido.

Utilice la información de los informes para derivar métricas de éxito clave para medir la adopción de [!DNL Assets] en su empresa y por clientes.

La variable [!DNL Assets] uso del marco de informes [!DNL Sling] trabajos para procesar de forma asíncrona solicitudes de informes de forma ordenada. Es escalable para repositorios grandes. El procesamiento asincrónico de informes aumenta la eficacia y la velocidad con que se generan los informes.

La interfaz de administración de informes es intuitiva e incluye opciones y controles detallados para acceder a informes archivados y ver estados de ejecución de informes (éxito, error y cola).

Cuando se genera un informe, se le notifica mediante <!-- through an email (optional) and --> una notificación de la bandeja de entrada. Puede ver, descargar o eliminar un informe desde la página de lista de informes, donde se muestran todos los informes generados anteriormente.

## Generar informes {#generate-reports}

[!DNL Experience Manager Assets] genera los siguientes informes estándar:

* Cargar
* Descargar
* Vencimiento
* Modificación
* Publicación
* [!DNL Brand Portal] publicación
* Uso del disco
* Archivos
* Vínculos compartidos

<!-- Removed download report.
* Upload
* Download
* Expiration
* Modification
* Publish
* [!DNL Brand Portal] publish
* Disk Usage
* Files
* Link Share
-->

[!DNL Adobe Experience Manager] los administradores pueden generar y personalizar fácilmente estos informes para su implementación. Un administrador puede seguir estos pasos para generar un informe:

1. En [!DNL Experience Manager] interfaz, haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Informes]**.

   ![Página Herramientas para navegar por el informe Recursos](assets/navigation.png)

1. En el [!UICONTROL Informes de recursos] página, haga clic en **[!UICONTROL Crear]** en la barra de herramientas.
1. En el **[!UICONTROL Crear informe]** , elija el informe que desea crear y haga clic en **[!UICONTROL Siguiente]**.

   ![Seleccionar tipo de informe](assets/choose_report.png)

1. Configure los detalles del informe, como título, descripción, miniatura y ruta de carpeta. De forma predeterminada, la ruta de la carpeta es `/content/dam`. Puede especificar una ruta diferente para ejecutar el informe en una carpeta específica.

   ![Página para agregar detalles del informe](assets/report_configuration.png)

   Elija el intervalo de fechas del informe. Puede elegir generar el informe ahora o en una fecha y hora futuras.

   >[!NOTE]
   >
   >Si decide programar el informe más adelante, asegúrese de especificar la fecha y la hora en los campos Fecha y Hora. Si no especifica ningún valor, el motor de informes lo considera un informe que se generará al instante.

   Los campos de configuración pueden variar según el tipo de informe que cree. Por ejemplo, la variable **[!UICONTROL Uso del disco]** proporciona opciones para incluir representaciones de recursos al calcular el espacio en disco utilizado por los recursos. Puede elegir incluir o excluir recursos en subcarpetas para el cálculo del uso del disco.

   >[!NOTE]
   >
   >El informe **[!UICONTROL Uso del disco]** no incluye campos de intervalo de fechas porque solo indica el uso actual del espacio en disco.

   ![Página Detalles del informe Uso del disco](assets/disk_usage_configuration.png)

   Al crear la variable **[!UICONTROL Archivos]** , puede incluir o excluir subcarpetas. Sin embargo, no puede incluir representaciones de recursos para este informe.

   ![Página de detalles del informe Archivos](assets/files_report.png)

   El informe **[!UICONTROL Compartir vínculos]** muestra las direcciones URL de los recursos que se comparten con usuarios externos desde [!DNL Assets]. <!-- It includes email ids of the user who shared the assets, emails ids of users with which the assets are shared, share date, and expiration date for the link. --> Las columnas no se pueden personalizar.

   La variable **[!UICONTROL Compartir vínculos]** no incluye opciones para subcarpetas y representaciones porque solo publica las direcciones URL compartidas que aparecen en `/var/dam/share`.

   ![Página de detalles del informe Compartir vínculos](assets/link_share.png)

1. Haga clic en **[!UICONTROL Siguiente]** en la barra de herramientas.

1. En el **[!UICONTROL Configurar columnas]** , algunas columnas están seleccionadas para aparecer en el informe de forma predeterminada. Puede seleccionar más columnas. Cancelar la selección de una columna para excluirla en el informe.

   ![Seleccionar o cancelar la selección de columnas de informes](assets/configure_columns.png)

   Para mostrar un nombre de columna personalizado o una ruta de propiedad, configure las propiedades del binario de recursos en la sección `jcr:content` en CRX. También puede agregarlo mediante el selector de rutas de propiedad.

   ![Seleccionar o cancelar la selección de columnas de informes](assets/custom_columns.png)

1. Haga clic en **[!UICONTROL Crear]** en la barra de herramientas. Un mensaje notifica que se ha iniciado la generación del informe.
1. En el [!UICONTROL Informes de recursos] , el estado de generación de informes se basa en el estado actual del trabajo del informe, por ejemplo [!UICONTROL Correcto], [!UICONTROL Error], [!UICONTROL En cola]o [!UICONTROL Programado]. El mismo estado aparece en la bandeja de entrada de notificaciones. Para ver la página del informe, haga clic en el vínculo del informe. También puede seleccionar el informe y hacer clic en **[!UICONTROL Ver]** en la barra de herramientas.

   ![Un informe generado](assets/report_page.png)

   Haga clic en **[!UICONTROL Descargar]** en la barra de herramientas para descargar el informe en formato CSV.

   >[!NOTE]
   >
   >Puede generar informes basados en los eventos generados durante los últimos 360 días. Experience Manager retiene los datos de ID de usuario durante 30 días.

## Agregar columnas personalizadas a informes {#add-custom-columns}

Puede agregar columnas personalizadas a los siguientes informes para mostrar más datos según sus necesidades personalizadas:

<!-- Remove download report.
* Upload
* Download
* Expiration
* Modification
* Publish
* [!DNL Brand Portal] publish
* Files
-->

* Cargar
* Vencimiento
* Modificación
* Publicación
* [!DNL Brand Portal] publicación
* Archivos

Para agregar columnas personalizadas a estos informes, siga estos pasos:

1. En el [!DNL Manager interface], haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Informes]**.
1. En el [!UICONTROL Informes de recursos] página, haga clic en **[!UICONTROL Crear]** en la barra de herramientas.

1. En el **[!UICONTROL Crear informe]** , elija un informe para crear. Haga clic en **[!UICONTROL Siguiente]**.

1. Configure los detalles del informe, como título, descripción, miniatura, ruta de carpeta e intervalo de fechas, según corresponda. Haga clic en **[!UICONTROL Siguiente]**.

1. Seleccione la información aplicable de la lista de **[!UICONTROL Columnas predeterminadas]**. Para mostrar una columna personalizada, especifique el nombre de la columna debajo de **[!UICONTROL Columnas personalizadas]**.

   ![Especificar el nombre de la columna personalizada del informe](assets/custom_columns-1.png)

1. Añada la ruta de la propiedad en la sección `jcr:content` en CRXDE usando el selector de rutas de propiedad. También puede escribir la ruta en el campo de ruta de la propiedad.

   ![Asignación de la ruta de la propiedad desde las rutas en jcr:content](assets/property_picker.png)

   Para agregar más columnas personalizadas, haga clic en **[!UICONTROL Agregar]** y repita los pasos anteriores.

1. Haga clic en **[!UICONTROL Crear]** en la barra de herramientas. Un mensaje notifica que se ha iniciado la generación del informe.

<!-- TBD: How to configure purge now? Is it using OSGi configurations?

## Configure purging service {#configure-purging-service}

To remove reports that you no longer require, configure the DAM Report Purge service from the web console to purge existing reports based on their quantity and age.

1. Access the web console (configuration manager) from `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL DAM Report Purge Service]** configuration.
1. Specify the frequency (time interval) for the purging service in the `scheduler.expression.name` field. You can also configure the age and the quantity threshold for reports.
1. Save the changes.
-->

## Información sobre resolución de problemas {#tips-troubleshoot}

* Si la variable [!UICONTROL Informe de uso del disco] no genera y si está utilizando [!DNL Dynamic Media], asegúrese de que todos los recursos se procesan correctamente. Para resolverlo, vuelva a procesar los recursos y vuelva a generar el informe.

<!-- These notes were present in generate report section above. Removing commented text from in between the instructions to preserve the numbering of the ordered list.

TBD: How do enable this in CS now? Is it done using some OSGi config now?
   >[!NOTE]
   >
   >Before you can generate an **[!UICONTROL Asset Downloaded]** report, ensure that the Asset Download service is enabled. From the web console (`https://[aem_server]:[port]/system/console/configMgr`), open the **[!UICONTROL Day CQ DAM Event Recorder]** configuration, and select the **[!UICONTROL Asset Downloaded (DOWNLOADED)]** option in Event Types if not already selected.
-->

<!-- Removed download report.
   >[!NOTE]
   >
   >By default, the Content Fragments and link shares are included in the asset [!UICONTROL Download] report. Select the appropriate option to create a report of link shares or to exclude Content Fragments from the download report.

   >[!NOTE]
   >
   >The [!UICONTROL Download] report displays details of only those assets which are downloaded after selecting individually or are downloaded using Quick Action. However, it does not include the details of the assets that are inside a downloaded folder.
-->

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de Recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con Assets](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos conectados](use-assets-across-connected-assets-instances.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)
