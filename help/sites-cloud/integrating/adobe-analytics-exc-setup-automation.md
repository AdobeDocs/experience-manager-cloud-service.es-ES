---
title: Integración de Adobe Analytics con la automatización de la configuración de Experience Cloud
description: La automatización de la configuración de Experience Cloud proporciona una forma sencilla y automatizada de integrar e instrumentar Experience Manager Sites con las Etiquetas de Experience Platform y Adobe Analytics mediante una sencilla interfaz de asistente de IU. Aprenda a utilizar la configuración automatizada con su propio sitio.
feature: Integration
role: Admin
exl-id: 351ead2c-7b0d-4bd9-a020-47516948d467
solution: Experience Manager Sites
source-git-commit: 4a3e65ef6a8aa08c8bc78db31f94272334994ac5
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 86%

---

# Integración de Adobe Analytics con la automatización de la configuración de Experience Cloud {#integrate-adobe-analytics-automation-setup}

>[!CAUTION]
>
>La funcionalidad de automatización de la configuración de Experience Cloud está en desuso.

La automatización de la configuración de Experience Cloud proporciona una forma sencilla y automatizada de integrar e instrumentar Experience Manager Sites con etiquetas de Experience Platform y Adobe Analytics mediante una sencilla interfaz de asistente de IU.

Nunca ha sido más sencillo integrar Adobe Analytics con AEM Sites. Con la automatización de la configuración de Experience Cloud, configure, integre e instrumente su sitio para capturar análisis de rendimiento y comprender cómo los clientes interactúan y se convierten, todo con solo unos pocos clics.

En este vídeo se explica cómo un sitio de AEM está integrado con etiquetas de Experience Platform y Analytics mediante la automatización de la configuración de Experience Cloud:

>[!VIDEO](https://video.tv.adobe.com/v/345372/?quality=12)

## Requisitos 

La configuración de automatización está diseñada para funcionar de forma predeterminada con un sitio de AEM creado mediante [Componentes principales de AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) con la [Capa de datos del cliente de Adobe](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html?lang=es) activada. Puede generar un nuevo sitio que tenga estas funciones activadas automáticamente mediante el [Tipo de archivo del proyecto de AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es) o creando un sitio con una [Plantilla de sitio](/help/journey-sites/quick-site/create-site.md).

## Requisitos previos {#prerequisites}

Antes de utilizar esta funcionalidad, es importante seguir estas instrucciones para asegurarse de que los servicios de requisitos previos se hayan configurado correctamente en su entorno:

1. Inicie sesión en Adobe Admin Console (https://adminconsole.adobe.com/).
1. Asegúrese de que el ID de organización de IMS correcto esté seleccionado en la esquina superior derecha.
1. Haga clic en la opción de navegación Productos.
1. Compruebe que Adobe Experience Manager as a Cloud Service esté aprovisionado para la organización IMS.
1. Compruebe que Adobe Analytics esté aprovisionado para la organización IMS.
1. Vaya a Cloud Manager (https://experience.adobe.com/cloud-manager).
1. Seleccione el programa apropiado.
1. Compruebe que Entorno sea de la última versión de Cloud Service (si no lo es, seleccione Actualizar en las opciones del menú).
1. Ejecute una canalización de pila completa en Cloud Manager.

El entorno debe estar listo para la automatización de la configuración de Experience Cloud.

## Cómo configurar

1. Vaya a **Sitios** y seleccione la raíz del sitio que desea integrar con Adobe Analytics.
1. Expanda el menú del carril lateral y seleccione **Análisis de configuración**.

   Se trata de una nueva opción del carril lateral que abre un panel que proporciona controles y el estado para la automatización de la configuración de Experience Cloud.
1. Seleccione el botón **Integrar Analytics**.
1. En el cuadro de diálogo resultante, proporcione un nombre para el **ID del grupo de informes**.

   Esta cadena se usa para crear un [ID del grupo de informes](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html?lang=es) en Adobe Analytics como almacén de datos para los datos de análisis del sitio de AEM seleccionado. La cadena proporcionada se añade con identificadores de entorno y de nivel para garantizar la exclusividad.

1. Actualice la página y el panel y seleccione **Comprobar estado de integración** para comprobar el estado de la automatización.

   La configuración de automatización se produce de forma asíncrona. **Comprobar estado de integración** mostrará el estado actual de la integración.

   * **En curso**: indica que el trabajo se está ejecutando.
   * **Integración finalizada**: indica que el trabajo ha completado la integración de Analytics y Etiquetas, la configuración de extensiones de Etiquetas y reglas de Etiquetas y la creación del nuevo grupo de informes en Adobe Analytics.
   * **Fallo**: indica que el trabajo automatizado no se pudo completar correctamente. Para comprobar los archivos de registro de este trabajo, haga clic en el vínculo Registros.

## Validación de la configuración de AEM

Una vez finalizada la automatización, confirme que su sitio está activando los eventos de Analytics.

1. Abra una página del sitio utilizando el **Editor de sitios**.
1. Utilice la opción **Ver tal y como aparece publicado** para cargar una versión publicada de la página.
1. Utilice las herramientas para desarrolladores del explorador para inspeccionar el tráfico de red y que las **Etiquetas** y `AppMeasurement.js` los archivos se están cargando.
1. Inspeccione la consola del explorador para ver que la capa de datos del cliente de Adobe activa y recopila los eventos de nivel de componente y página.

## Validación de la configuración de Analytics

A continuación, vaya a Adobe Analytics para ver los datos que llegan desde los eventos del sitio de AEM.

1. Vaya a Adobe Analytics en la misma organización de IMS que el sitio de AEM.
1. Cree un nuevo informe general para AEM Sites navegando a **Informes** > **Participación** > **Adobe Experience Manager** > **Información general sobre el rendimiento del sitio**.
1. Seleccione **Abrir informe**.
1. Seleccione el **ID del grupo de informes** que coincide con el nombre del grupo de informes utilizado en el ejercicio anterior.
1. Vea el flujo de datos de análisis en la nueva plantilla a lo largo del tiempo.

   >[!NOTE]
   >
   > Con una integración nueva, es posible que pasen unas horas antes de que el informe se rellene con datos.
