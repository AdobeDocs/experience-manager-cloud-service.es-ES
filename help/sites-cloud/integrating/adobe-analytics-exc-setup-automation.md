---
title: Integración de Adobe Analytics con la automatización de la configuración de Experience Cloud
description: La automatización de la configuración de Experience Cloud proporciona una forma sencilla y automatizada de integrar e instrumentar Experience Manager Sites con Experience Platform Launch y Adobe Analytics mediante una sencilla interfaz de asistente de IU. Aprenda a utilizar la configuración automatizada con su propio sitio.
feature: Administering
role: Admin
hide: true
hidefromtoc: true
index: false
exl-id: 351ead2c-7b0d-4bd9-a020-47516948d467
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: ht
source-wordcount: '639'
ht-degree: 100%

---

# Integración de Adobe Analytics con la automatización de la configuración de Experience Cloud {#integrate-adobe-analytics-automation-setup}

>[!CAUTION]
>
> Esta funcionalidad se encuentra actualmente en versión beta interna. La versión de Target se publicará en el primer trimestre de 2022.

La automatización de la configuración de Experience Cloud proporciona una forma sencilla y automatizada de integrar e instrumentar Experience Manager Sites con Experience Platform Launch y Adobe Analytics mediante una sencilla interfaz de asistente de IU.

Nunca ha sido más sencillo integrar Adobe Analytics con AEM Sites. Con la automatización de la configuración de Experience Cloud, configure, integre e instrumente su sitio para capturar análisis de rendimiento y comprender cómo los clientes interactúan y se convierten, todo con solo unos pocos clics.

En este vídeo se explica cómo un sitio de AEM está integrado con Experience Platform Launch y Analytics mediante la automatización de la configuración de Experience Cloud:

>[!VIDEO](https://video.tv.adobe.com/v/339605/?quality=12)

## Requisitos 

La configuración de automatización está diseñada para funcionar de forma predeterminada con un sitio de AEM creado mediante [Componentes principales de AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) con la [Capa de datos del cliente de Adobe](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html?lang=es) activada. Puede generar un nuevo sitio que tenga estas funciones activadas automáticamente mediante el [Tipo de archivo del proyecto de AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es) o creando un sitio con una [Plantilla de sitio](/help/journey-sites/quick-site/create-site.md).

## Cómo configurar

1. Vaya a **Sitios** y seleccione la raíz del sitio que desea integrar con Adobe Analytics.
1. Expanda el menú del carril lateral y pulse **Configurar Analytics**.

   Esta es una nueva opción del carril lateral que abrirá un panel que proporcionará controles y el estado para la automatización de la configuración de Experience Cloud.
1. Pulse el botón **Integrar Analytics**.
1. En el cuadro de diálogo resultante, proporcione un nombre para el **ID del grupo de informes**.

   Esta cadena se utilizará para crear un nuevo [ID del grupo de informes](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html?lang=es) en Adobe Analytics como almacén de datos para los datos del análisis del sitio de AEM seleccionado. La cadena proporcionada se añadirá con identificadores de entorno y de nivel para garantizar la exclusividad.

1. Actualice la página y el panel y pulse **Comprobar estado de integración** para comprobar el estado de la automatización.

   La configuración de automatización se produce de forma asíncrona. **Comprobar estado de integración** mostrará el estado actual de la integración.

   * **En curso**: indica que el trabajo se está ejecutando.
   * **Integración finalizada**: indica que el trabajo ha completado la integración de Analytics y Launch, la configuración de extensiones de Launch y reglas de Launch y la creación del nuevo grupo de informes en Adobe Analytics.
   * **Fallo**: indica que el trabajo automatizado no se pudo completar correctamente. Para comprobar los archivos de registro de este trabajo, haga clic en el vínculo Registros.

## Validación de la configuración de AEM

Una vez finalizada la automatización, confirme que su sitio está activando los eventos de Analytics.

1. Abra una página del sitio utilizando el **Editor de sitios**.
1. Utilice la opción **Ver tal y como aparece publicado** para cargar una versión publicada de la página.
1. Utilice las herramientas para desarrolladores del explorador para inspeccionar el tráfico de red y que **Launch** y `AppMeasurement.js` los archivos se están cargando.
1. Inspeccione la consola del explorador para ver que la capa de datos del cliente de Adobe activa y recopila los eventos de nivel de componente y página.

## Validación de la configuración de Analytics

A continuación, vaya a Adobe Analytics para ver los datos que llegan desde los eventos del sitio de AEM.

1. Vaya a Adobe Analytics en la misma organización de IMS que el sitio de AEM.
1. Cree un nuevo informe general para AEM Sites navegando a **Informes** > **Participación** > **Adobe Experience Manager** > **Información general sobre el rendimiento del sitio**.
1. Pulse **Abrir informe**.
1. Seleccione el **ID del grupo de informes** que coincide con el nombre del grupo de informes utilizado en el ejercicio anterior.
1. Vea el flujo de datos de análisis en la nueva plantilla a lo largo del tiempo.

   >[!NOTE]
   >
   > Con una integración nueva, es posible que pasen unas horas antes de que el informe se rellene con datos.
