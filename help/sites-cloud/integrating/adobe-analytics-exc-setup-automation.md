---
title: Integración de Adobe Analytics con la automatización de la configuración del Experience Cloud
description: La automatización de la configuración del Experience Cloud proporciona una forma sencilla y automatizada de integrar e instrumentar Experience Manager Sites con Experience Platform Launch y Adobe Analytics mediante una sencilla interfaz de asistente de IU. Aprenda a utilizar la configuración automatizada con su propio sitio.
feature: Administering
role: Admin
hide: true
hidefromtoc: true
index: false
exl-id: 351ead2c-7b0d-4bd9-a020-47516948d467
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# Integración de Adobe Analytics con la automatización de la configuración del Experience Cloud {#integrate-adobe-analytics-automation-setup}

>[!CAUTION]
>
> Esta funcionalidad se encuentra actualmente en versión beta interna. La versión de Target se publicará en el primer trimestre de 2022.

La automatización de la configuración del Experience Cloud proporciona una forma sencilla y automatizada de integrar e instrumentar Experience Manager Sites con Experience Platform Launch y Adobe Analytics mediante una sencilla interfaz de asistente de IU.

Nunca ha sido más sencillo integrar Adobe Analytics con AEM Sites. Con la automatización de la configuración de Experience Cloud, configure, integre e instrumente su sitio para capturar análisis de rendimiento para comprender cómo los clientes están atrayendo y convirtiendo, todo se ajusta con solo unos pocos clics.

En este vídeo se explica cómo un sitio AEM está integrado con Experience Platform Launch y Analytics mediante la automatización de la configuración del Experience Cloud:

>[!VIDEO](https://video.tv.adobe.com/v/339605/?quality=12)

## Requisitos

La configuración de automatización está diseñada para funcionar de forma predeterminada con un sitio AEM creado mediante [Componentes principales AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) con la variable [Capa de datos del cliente de Adobe](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html) activada. Puede generar un nuevo sitio que tenga estas funciones activadas automáticamente mediante la variable [Tipo de archivo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) o creando un sitio con un [Plantilla del sitio](/help/journey-sites/quick-site/create-site.md).

## Cómo configurar

1. Vaya a **Sitios** y seleccione la raíz del sitio que desea integrar con Adobe Analytics.
1. Expanda el menú del carril lateral y pulse **Configuración de Analytics**.

   Esta es una nueva opción del carril lateral que abrirá un panel que proporcionará controles y estado para la automatización de la configuración del Experience Cloud.
1. Toque . **Integrar Analytics** botón.
1. En el cuadro de diálogo resultante, proporcione un nombre para la variable **ID del grupo de informes**.

   Esta cadena se utilizará para crear una [ID del grupo de informes](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html?lang=en) en Adobe Analytics como almacén de datos para los datos de análisis del sitio AEM seleccionado. La cadena proporcionada se añadirá con identificadores de entorno y de nivel para garantizar la exclusividad.

1. Actualice la página y el panel y pulse **Comprobar estado de integración** para comprobar el estado de la automatización.

   La configuración de automatización se produce de forma asíncrona. La variable **Comprobar estado de integración** mostrará el estado actual de la integración.

   * **En curso** - indica que el trabajo se está ejecutando.
   * **Integración finalizada** : indica que el trabajo ha completado la integración de Analytics y Launch, la configuración de extensiones de Launch y reglas de Launch y la creación del nuevo grupo de informes en Adobe Analytics.
   * **Fallo** : indica que el trabajo automatizado no se pudo completar correctamente. Para comprobar los archivos de registro de este trabajo, haga clic en el vínculo Logs .

## Validar AEM configuración

Una vez finalizada la automatización, confirme que su sitio está activando los eventos de Analytics.

1. Abra una página del sitio utilizando la **Editor de sitios**.
1. Utilice la variable **Ver tal y como aparece publicado** para cargar una versión publicada de la página.
1. Utilice las herramientas para desarrolladores del navegador para inspeccionar el tráfico de red y que **Launch** y `AppMeasurement.js` los archivos se están cargando.
1. Inspect utiliza la consola del explorador para ver que la capa de datos del cliente de Adobe activa y recopila los eventos de nivel de componente y página.

## Validar la configuración de Analytics

A continuación, vaya a Adobe Analytics para ver los datos que llegan desde los eventos del sitio AEM.

1. Vaya a Adobe Analytics en la misma organización de IMS que AEM sitio.
1. Cree un nuevo informe general para que AEM Sites navegue a **Informes** > **Participación** > **Adobe Experience Manager** > **Información general sobre el rendimiento del sitio**.
1. Toque **Abrir informe**.
1. Seleccione el **ID del grupo de informes** que coincide con el nombre del grupo de informes utilizado en el ejercicio anterior.
1. Vea el flujo de datos de análisis en la nueva plantilla a lo largo del tiempo.

   >[!NOTE]
   >
   > Con una nueva integración, es posible que pasen unas horas antes de que el informe se rellene con datos.
