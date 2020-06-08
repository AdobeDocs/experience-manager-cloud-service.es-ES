---
title: Informes de Asset
description: En este artículo se describen varios informes sobre los recursos en Recursos AEM y cómo generar informes.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14
workflow-type: tm+mt
source-wordcount: '982'
ht-degree: 17%

---


# Informes del recurso {#asset-reports}

El sistema de informes de recursos es una herramienta clave para evaluar la utilidad de la implementación de Recursos Adobe Experience Manager (AEM). Con Recursos AEM, puede generar varios informes en torno a sus recursos digitales. Los informes proporcionan información útil sobre el uso del sistema, la forma en que los usuarios interactúan con los recursos y los recursos que se descargan y comparten.

Utilice la información de los informes para derivar métricas de éxito clave a fin de medir la adopción de Recursos AEM en su empresa y por parte de los clientes.

El marco de sistema de informes de AEM Assets aprovecha los trabajos de Sling para procesar de forma asincrónica las solicitudes de informes de forma ordenada. Es escalable para repositorios grandes. El procesamiento asincrónico de informes aumenta la eficiencia y la velocidad con que se generan los informes.

La interfaz de administración de informes es intuitiva e incluye opciones y controles detallados para acceder a los informes archivados y a los estados de ejecución de los informes de vista (exitosos, fallidos y en cola).

Cuando se genera un informe, se le notifica mediante <!-- through an email (optional) and --> una notificación de bandeja de entrada. Puede vista, descargar o eliminar un informe desde la página con la lista de informes, donde se muestran todos los informes generados previamente.

## Generar informes {#generate-reports}

Recursos AEM genera los siguientes informes estándar:

* Cargar
* Descargar
* Vencimiento
* Modificación
* Publicación
* Publicación de Brand Portal
* Uso del disco
* Archivos
* Vínculos compartidos

Los administradores de AEM pueden generar y personalizar fácilmente estos informes para su implementación. Un administrador puede seguir estos pasos para generar un informe:

1. Pulse o haga clic en el logotipo de AEM y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Informes]**.

   ![navegación](assets/navigation.png)

1. En la página Informes de recursos, toque o haga clic en **[!UICONTROL Crear]** desde la barra de herramientas.
1. En la página **[!UICONTROL Crear informe]** , elija el informe que desee crear y toque o haga clic en **[!UICONTROL Siguiente]**.

   ![select_report](assets/choose_report.png)

   >[!NOTE]
   >
   >Antes de generar un informe de **[!UICONTROL descarga de recursos]**, compruebe que el servicio de descarga de recursos está habilitado. En la consola web (`https://[aem_server]:[port]/system/console/configMgr`), abra la configuración del **[!UICONTROL grabador de eventos de CQ DAM de día]** y seleccione la opción **[!UICONTROL Recurso descargado (DESCARGADO)]** en Tipos de eventos si no está seleccionada.

   >[!NOTE]
   >
   >De forma predeterminada, los fragmentos de contenido y los recursos compartidos de vínculos se incluyen en el informe Descarga de recursos. Seleccione la opción adecuada para crear un informe de recursos compartidos de vínculos o para excluir fragmentos de contenido del informe de descarga.

1. Configure los detalles del informe, como título, descripción, miniatura y ruta de carpeta, en el repositorio de CRX donde se almacena el informe. De forma predeterminada, la ruta de la carpeta es */content/dam*. Puede especificar una ruta diferente.

   ![report_configuration](assets/report_configuration.png)

   Elija el intervalo de fechas del informe.

   Puede elegir generar el informe ahora o en una fecha y hora futuras.

   >[!NOTE]
   >
   >Si decide programar el informe en una fecha posterior, asegúrese de especificar la fecha y la hora en el campo Fecha y hora. Si no especifica ningún valor, el motor de informes lo trata como un informe que se va a generar instantáneamente.

   Los campos de configuración pueden diferir según el tipo de informe que cree.

   Por ejemplo: el informe Uso del **[!UICONTROL disco]** proporciona opciones para incluir representaciones de recursos al calcular el espacio en disco que utilizan los recursos. Puede optar por incluir o excluir recursos en subcarpetas para el cálculo del uso del disco.

   >[!NOTE]
   >
   >El informe **[!UICONTROL Uso del disco]** no incluye campos de intervalo de fechas porque solo indica el uso actual del espacio en disco.

   ![disk_usage_configuration](assets/disk_usage_configuration.png)

   Al crear el informe **[!UICONTROL Archivos]** , puede incluir o excluir subcarpetas. Sin embargo, no puede incluir representaciones de recursos para este informe.

   ![files_report](assets/files_report.png)

   El informe **[!UICONTROL Compartir vínculos]** muestra las direcciones URL de los recursos que se comparten con usuarios externos desde AEM Assets. <!-- It includes email ids of the user who shared the assets, emails ids of users with which the assets are shared, share date, and expiration date for the link. --> Las columnas no se pueden personalizar.

   El informe **[!UICONTROL Compartir vínculos]** no incluye opciones para subcarpetas y representaciones porque solo publica las direcciones URL compartidas que aparecen en */var/dam/share*.

   ![link_share](assets/link_share.png)

1. Toque o haga clic en **[!UICONTROL Siguiente]** en la barra de herramientas.

1. En la página **[!UICONTROL Configurar columnas]** , se seleccionan algunas columnas para que aparezcan en el informe de forma predeterminada. Puede seleccionar columnas adicionales. Anule la selección de una columna seleccionada para excluirla del informe.

   ![configure_columns](assets/configure_columns.png)

   Para mostrar un nombre de columna personalizado o una ruta de propiedad, configure las propiedades del binario de recursos en el nodo jcr:content en CRX. También puede agregarla mediante el selector de rutas de propiedad.

   ![custom_columns](assets/custom_columns.png)

1. Tap/click **[!UICONTROL Create]** from the toolbar. Un mensaje notifica que se ha iniciado la generación de informes.
1. En la página Informes de recursos, el estado de generación de informes se basa en el estado actual del trabajo del informe, por ejemplo, Éxito, Fallido, En cola o Programado. El mismo estado aparece en la bandeja de entrada de notificaciones.

   Para vista de la página del informe, toque o haga clic en el vínculo del informe. Como alternativa, seleccione el informe y toque o haga clic en el icono de Vista en la barra de herramientas.

   ![report_page](assets/report_page.png)

   Toque o haga clic en el icono Descargar de la barra de herramientas para descargar el informe en formato CSV.

## Añadir columnas personalizadas {#add-custom-columns}

Puede agregar columnas personalizadas a los siguientes informes para mostrar más datos según sus requisitos personalizados:

* Cargar
* Descargar
* Vencimiento
* Modificación
* Publicación
* Publicación de Brand Portal
* Archivos

1. Pulse o haga clic en el logotipo de AEM y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Informes]**.
1. En la página Informes de recursos, toque o haga clic en **[!UICONTROL Crear]** desde la barra de herramientas.

1. En la página **[!UICONTROL Crear informe]** , elija el informe que desee crear y toque o haga clic en **[!UICONTROL Siguiente]**.
1. Configure los detalles del informe, como título, descripción, miniatura, ruta de carpeta, intervalo de fechas, etc., según corresponda.

1. Para mostrar una columna personalizada, especifique el nombre de la columna debajo de **[!UICONTROL Columnas personalizadas]**.

   ![custom_columns-1](assets/custom_columns-1.png)

1. Añada la ruta de la propiedad bajo el `jcr:content` nodo en CRXDE mediante el selector de rutas de propiedad.

   ![property_picker](assets/property_picker.png)

   También puede escribir la ruta en el campo de ruta de la propiedad.

   ![property_path](assets/property_path.png)

   Para agregar más columnas personalizadas, toque o haga clic en **[!UICONTROL Añadir]** y repita los pasos 5 y 6.

1. Tap/click **[!UICONTROL Create]** from the toolbar. Un mensaje notifica que se ha iniciado la generación de informes.

## Configurar el servicio de depuración {#configure-purging-service}

Para eliminar los informes que ya no necesite, configure el servicio Depuración de informes DAM desde la consola web para purgar los informes existentes en función de su cantidad y antigüedad.

1. Acceda a la consola web (administrador de configuración) desde `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra la configuración del servicio **[!UICONTROL de depuración de informes]** DAM.
1. Especifique la frecuencia (intervalo de tiempo) del servicio de depuración en el `scheduler.expression.name` campo. También puede configurar la edad y el umbral de cantidad para los informes.
1. Guarde los cambios.
