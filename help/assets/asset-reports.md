---
title: Informes sobre uso y uso compartido
description: Informes sobre los recursos en [!DNL Adobe Experience Manager Assets] que ayudan a comprender el uso, la actividad y el uso compartido de los recursos digitales.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 3ee2e53268ea77949057ac18fcb4a8f8b1e01cb2
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 7%

---


# Informes del recurso {#asset-reports}

El sistema de informes de recursos permite evaluar la utilidad de la implementación [!DNL Adobe Experience Manager Assets]. Con [!DNL Assets], puede generar varios informes para sus recursos digitales. Los informes proporcionan información útil sobre el uso del sistema, la forma en que los usuarios interactúan con los recursos y los recursos que se descargan y comparten.

Utilice la información de los informes para derivar métricas de éxito clave y medir la adopción de [!DNL Assets] dentro de su empresa y por parte de los clientes.

El módulo de sistema de informes [!DNL Assets] utiliza [!DNL Sling] trabajos para procesar asincrónicamente solicitudes de informes de manera ordenada. Es escalable para repositorios grandes. El procesamiento asincrónico de informes aumenta la eficiencia y la velocidad con que se generan los informes.

La interfaz de administración de informes es intuitiva e incluye opciones y controles detallados para acceder a los informes archivados y a los estados de ejecución de los informes de vista (exitosos, fallidos y en cola).

Cuando se genera un informe, <!-- through an email (optional) and --> se le notifica mediante una notificación de bandeja de entrada. Puede vista, descargar o eliminar un informe desde la página con la lista de informes, donde se muestran todos los informes generados previamente.

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

1. En la interfaz [!DNL Experience Manager], haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Informes]**.

   ![Página Herramientas para navegar por el informe de recursos](assets/navigation.png)

1. En la página [!UICONTROL Informes de recursos], haga clic en **[!UICONTROL Crear]** desde la barra de herramientas.
1. En la página **[!UICONTROL Crear informe]**, elija el informe que desee crear y haga clic en **[!UICONTROL Siguiente]**.

   ![Seleccionar tipo de informe](assets/choose_report.png)

<!-- TBD: How do enable this in CS now? Is it done using some OSGi config now?
   >[!NOTE]
   >
   >Before you can generate an **[!UICONTROL Asset Downloaded]** report, ensure that the Asset Download service is enabled. From the web console (`https://[aem_server]:[port]/system/console/configMgr`), open the **[!UICONTROL Day CQ DAM Event Recorder]** configuration, and select the **[!UICONTROL Asset Downloaded (DOWNLOADED)]** option in Event Types if not already selected.
-->

>[!NOTE]
>
>De forma predeterminada, los fragmentos de contenido y los recursos compartidos de vínculos se incluyen en el informe Recurso [!UICONTROL Descargar]. Seleccione la opción adecuada para crear un informe de recursos compartidos de vínculos o para excluir fragmentos de contenido del informe de descarga.

>[!NOTE]
>
>El informe [!UICONTROL Descargar] muestra detalles de sólo los recursos que se descargan después de seleccionarse individualmente o que se descargan mediante Acción rápida. Sin embargo, no incluye los detalles de los recursos que se encuentran dentro de una carpeta descargada.

1. Configure los detalles del informe, como título, descripción, miniatura y ruta de carpeta, en el repositorio de CRX donde se almacena el informe. De forma predeterminada, la ruta de la carpeta es `/content/dam`. Puede especificar una ruta diferente.

   ![Página para agregar detalles del informe](assets/report_configuration.png)

   Elija el intervalo de fechas del informe.

   Puede elegir generar el informe ahora o en una fecha y hora futuras.

   >[!NOTE]
   >
   >Si decide programar el informe más adelante, asegúrese de especificar la fecha y la hora en los campos Fecha y Hora. Si no especifica ningún valor, el motor de informes lo trata como un informe que se va a generar instantáneamente.

   Los campos de configuración pueden diferir según el tipo de informe que cree. Por ejemplo: el informe **[!UICONTROL Uso del disco]** proporciona opciones para incluir representaciones de recursos al calcular el espacio en disco que utilizan los recursos. Puede optar por incluir o excluir recursos en subcarpetas para el cálculo del uso del disco.

   >[!NOTE]
   >
   >El informe **[!UICONTROL Uso del disco]** no incluye campos de intervalo de fechas porque solo indica el uso actual del espacio en disco.

   ![Página de detalles del informe Uso del disco](assets/disk_usage_configuration.png)

   Al crear el informe **[!UICONTROL Archivos]**, puede incluir o excluir subcarpetas. Sin embargo, no puede incluir representaciones de recursos para este informe.

   ![Página de detalles del informe Archivos](assets/files_report.png)

   El informe **[!UICONTROL Compartir vínculos]** muestra las direcciones URL de los recursos que se comparten con usuarios externos desde [!DNL Assets]. <!-- It includes email ids of the user who shared the assets, emails ids of users with which the assets are shared, share date, and expiration date for the link. --> Las columnas no se pueden personalizar.

   El informe **[!UICONTROL Uso compartido de vínculos]** no incluye opciones para subcarpetas y representaciones porque simplemente publica las direcciones URL compartidas que aparecen en `/var/dam/share`.

   ![Página de detalles del informe Uso compartido de vínculos](assets/link_share.png)

1. Haga clic en **[!UICONTROL Siguiente]** desde la barra de herramientas.

1. En la página **[!UICONTROL Configurar columnas]**, se seleccionan algunas columnas para que aparezcan en el informe de forma predeterminada. Puede seleccionar más columnas. Anule la selección de una columna seleccionada para excluirla del informe.

   ![Seleccionar o anular la selección de las columnas del informe](assets/configure_columns.png)

   Para mostrar un nombre de columna personalizado o una ruta de propiedad, configure las propiedades del binario de recursos en el nodo `jcr:content` en CRX. También puede agregarla mediante el selector de rutas de propiedad.

   ![Seleccionar o anular la selección de las columnas del informe](assets/custom_columns.png)

1. Haga clic en **[!UICONTROL Crear]** desde la barra de herramientas. Un mensaje notifica que se ha iniciado la generación de informes.
1. En la página [!UICONTROL Informes de recursos], el estado de generación de informes se basa en el estado actual del trabajo de informe, por ejemplo [!UICONTROL Éxito], [!UICONTROL Error], [!UICONTROL En cola] o [!UICONTROL Programado]. El mismo estado aparece en la bandeja de entrada de notificaciones.Para vista de la página del informe, haga clic en el vínculo del informe. Como alternativa, seleccione el informe y haga clic en **[!UICONTROL Vista]** en la barra de herramientas.

   ![Un informe generado](assets/report_page.png)

   Haga clic en **[!UICONTROL Descargar]** de la barra de herramientas para descargar el informe en formato CSV.

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

1. En [!DNL Manager interface], haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Informes]**.
1. En la página [!UICONTROL Informes de recursos], haga clic en **[!UICONTROL Crear]** desde la barra de herramientas.

1. En la página **[!UICONTROL Crear informe]**, elija el informe que desee crear y haga clic en **[!UICONTROL Siguiente]**.
1. Configure los detalles del informe, como título, descripción, miniatura, ruta de carpeta e intervalo de fechas, según corresponda.

1. Para mostrar una columna personalizada, especifique el nombre de la columna debajo de **[!UICONTROL Columnas personalizadas]**.

   ![Especificar el nombre de la columna personalizada del informe](assets/custom_columns-1.png)

1. Añada la ruta de la propiedad bajo el nodo `jcr:content` en CRXDE mediante el selector de rutas de propiedad. También puede escribir la ruta en el campo de ruta de la propiedad.

   ![Asignación de la ruta de la propiedad desde las rutas en jcr:content](assets/property_picker.png)

   Para agregar más columnas personalizadas, haga clic en **[!UICONTROL Añadir]** y repita los pasos 5 y 6.

1. Haga clic en **[!UICONTROL Crear]** desde la barra de herramientas. Un mensaje notifica que se ha iniciado la generación de informes.

<!-- TBD: How to configure purge now? Is it using OSGi configurations?

## Configure purging service {#configure-purging-service}

To remove reports that you no longer require, configure the DAM Report Purge service from the web console to purge existing reports based on their quantity and age.

1. Access the web console (configuration manager) from `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL DAM Report Purge Service]** configuration.
1. Specify the frequency (time interval) for the purging service in the `scheduler.expression.name` field. You can also configure the age and the quantity threshold for reports.
1. Save the changes.
-->

## Información, sugerencias y limitaciones para la resolución de problemas {#best-practices-and-limitations}

* Si el informe Uso de disco no se genera y utiliza [!DNL Dynamic Media], asegúrese de que todos los recursos se realicen correctamente. Para resolverlo, vuelva a procesar los recursos y, a continuación, vuelva a generar el informe.
