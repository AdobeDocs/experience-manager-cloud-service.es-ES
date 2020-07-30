---
title: 'Integración con Adobe Analytics '
description: 'Integración con Adobe Analytics '
translation-type: tm+mt
source-git-commit: ec747361935b94a729cdd5b6712aee6d3ce1b8a2
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 14%

---


# Integración con Adobe Analytics{#integrating-with-adobe-analytics}

La integración de Adobe Analytics y AEM como Cloud Service le permite rastrear la actividad de su página web:

* Una configuración de Adobe Analytics permite AEM autenticarse con Adobe Analytics.
* Un marco identifica los datos que se envían al grupo de informes de Adobe Analytics.

Los datos incluyen datos de página y usuario, por ejemplo:

* datos que AEM los componentes recopilan
* clics en vínculos
* información de uso de vídeo
* el número de visitas a la página desde Adobe Analytics

Las páginas que se enumeran a continuación pueden ayudarle a configurar la integración. Cabe señalar que el Launch by Adobe es la herramienta de hecho para instrumentar un sitio AEM con capacidades de Analytics (bibliotecas JS). Por lo tanto, la integración de AEM como Cloud Service con Launch y Adobe Analytics va de la mano.

* [Conexión a Adobe Analytics y creación de marcos](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-connect.html) : tenga en cuenta que los &quot;marcos de Analytics&quot; son heredados en AEM y que su creación no funciona en AEM como Cloud Service porque requiere la IU clásica. En su lugar, se debe utilizar el Launch by Adobe, tanto para la asignación de variables como para la implementación de bibliotecas JS en páginas.
* [Integrar Launch by Adobe](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
* [Integrar AEM con el lanzamiento de Adobe mediante E/S de Adobe](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
* [AEM integración con Launch by Adobe, Analytics y Destinatario](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)
* [Configuración del seguimiento de vínculos para Adobe Analytics](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-link.html)
* [Asignación de datos de componentes con propiedades de Adobe Analytics](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-mapping.html)
* [Configuración del seguimiento de videos para Adobe Analytics](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-video.html)
* [Clasificaciones de Adobes](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-classifications.html)

>[!CAUTION]
>
>Adobe Experience Manager como cliente Cloud Service que no tiene una cuenta Analytics existente, puede solicitar acceso a Analytics Foundation Pack para Experience Cloud.  Este paquete de Foundation proporciona un uso limitado por volumen de Analytics.

>[!NOTE]
>
>La configuración de IMS (cuentas técnicas) para Launch by Adobe está preconfigurada en AEM como Cloud Service. Los usuarios no tienen que crear esta configuración.

## Información adicional {#further-information}

Consulte:

* [Ampliación de la integración](https://docs.adobe.com/content/help/en/experience-manager-65/developing/extending-aem/extending-analytics/extending-analytics.html) de Adobe Analytics para obtener información sobre el desarrollo de componentes que recopilan datos de usuario y la personalización del marco de trabajo de Adobe Analytics. Tenga en cuenta que los &quot;marcos de Analytics&quot; son heredados en AEM y su creación no funciona en AEM como Cloud Service porque requiere la IU clásica. En su lugar, se debe utilizar el Launch by Adobe, tanto para la asignación de variables como para la implementación de bibliotecas JS en páginas.
* El artículo de la base de conocimientos, Integración con [Adobe Analytics: solución de problemas](https://helpx.adobe.com/experience-manager/kb/sitecatalystintegrationtroubleshooting.html), para obtener información sobre la solución de problemas de la integración con Adobe Analytics.

>[!NOTE]
>
>Si utiliza Adobe Analytics con una configuración proxy personalizada, debe [configurar dos paquetes](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/configuring-osgi.html) OSGi (por ejemplo, con la consola web) necesarios para las configuraciones proxy del cliente **HTTP de Apache**. Ambas son necesarias, ya que algunas funcionalidades de AEM utilizan las API 3.x, mientras que otras utilizan las API 4.x. Configurar:
>
>* **Day Commons HTTP Client 3.1** para configurar la API 3.x;
   >  por ejemplo, [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
   >
   >
* **Configuración** proxy de componentes HTTP de Apache para configurar la API 4.x;
   >  por ejemplo, [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>


