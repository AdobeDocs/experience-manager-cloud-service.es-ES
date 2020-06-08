---
title: Integración con Adobe Analytics
description: 'Integración con Adobe Analytics '
translation-type: tm+mt
source-git-commit: 6754693da488b0bc44a71aa9f0402fc1308b703a
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 14%

---


# Integración con Adobe Analytics{#integrating-with-adobe-analytics}

La integración de Adobe Analytics y AEM como un servicio de nube le permite realizar un seguimiento de la actividad de su página web:

* Una configuración de Adobe Analytics permite que AEM se autentique con Adobe Analytics.
* Un marco identifica los datos que se envían al grupo de informes de Adobe Analytics.

Los datos incluyen datos de página y usuario, por ejemplo:

* datos que recopilan los componentes de AEM
* clics en vínculos
* información de uso de vídeo
* el número de visitas de página de Adobe Analytics

Las páginas que se enumeran a continuación pueden ayudarle a configurar la integración. Cabe destacar que Launch by Adobe es la herramienta de facto para instrumentar un sitio de AEM con capacidades de Analytics (bibliotecas JS). Por lo tanto, la integración de AEM como servicio de nube con Launch y Adobe Analytics va de la mano.

* [Conexión a Adobe Analytics y creación de marcos](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-connect.html) : tenga en cuenta que los &quot;marcos de Analytics&quot; son heredados en AEM y que su creación no funciona en AEM como un servicio de nube porque requiere la IU clásica. En su lugar, se debe utilizar el lanzamiento de Adobe, tanto para la asignación de variables como para la implementación de bibliotecas JS en páginas.
* [Integrar Launch de Adobe](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
* [Integración de AEM con Adobe Launch mediante Adobe I/O](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
* [Información sobre la integración de AEM con Launch de Adobe, Analytics y Destinatario](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)
* [Configuración del seguimiento de vínculos para Adobe Analytics](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-link.html)
* [Asignación de datos de componentes con propiedades de Adobe Analytics](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-mapping.html)
* [Configuración del seguimiento de vídeo para Adobe Analytics](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-video.html)
* [Clasificaciones de Adobe](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-classifications.html)

>[!CAUTION]
>
>Adobe Experience Manager como cliente de Cloud Service que no tiene una cuenta de Analytics existente, puede solicitar acceso a Analytics Foundation Pack para Experience Cloud.  Este paquete de Foundation proporciona un uso limitado del volumen de Analytics.

>[!NOTE]
>
>La configuración de IMS (cuentas técnicas) para Launch de Adobe está preconfigurada en AEM como un servicio de nube. Los usuarios no tienen que crear esta configuración.

## Información adicional {#further-information}

Consulte:

* [Ampliación de la integración](https://docs.adobe.com/content/help/en/experience-manager-65/developing/extending-aem/extending-analytics/extending-analytics.html) de Adobe Analytics para obtener información sobre el desarrollo de componentes que recopilan datos de usuario y la personalización del marco de trabajo de Adobe Analytics. Tenga en cuenta que los &quot;marcos de Analytics&quot; son heredados en AEM y su creación no funciona en AEM como un servicio de nube porque requiere la IU clásica. En su lugar, se debe utilizar el lanzamiento de Adobe, tanto para la asignación de variables como para la implementación de bibliotecas JS en páginas.
* El artículo de la base de conocimientos, Integración de [Adobe Analytics: solución de problemas](https://helpx.adobe.com/experience-manager/kb/sitecatalystintegrationtroubleshooting.html), para obtener información sobre la solución de problemas de la integración de Adobe Analytics.

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


