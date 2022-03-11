---
title: 'Integración con Adobe Analytics '
description: 'Integración con Adobe Analytics '
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 12%

---


# Integración con Adobe Analytics{#integrating-with-adobe-analytics}

La integración de Adobe Analytics y AEM as a Cloud Service permite rastrear la actividad de la página web:

* Una configuración de Adobe Analytics permite AEM autenticarse con Adobe Analytics.
* Un marco identifica los datos que se envían al grupo de informes de Adobe Analytics.

Los datos incluyen datos de páginas y usuarios, por ejemplo:

* datos que recopilan los componentes de AEM
* clics en vínculos
* información de uso de vídeo
* el número de visitas a la página desde Adobe Analytics

Las páginas enumeradas a continuación pueden ayudarle a configurar la integración. Tenga en cuenta que Launch by Adobe es la herramienta de facto para instrumentar un sitio AEM con capacidades de Analytics (bibliotecas JS). Por lo tanto, la integración AEM as a Cloud Service con Launch y Adobe Analytics va de la mano.

* [Conexión a Adobe Analytics y creación de módulos](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-connect.html) : Tenga en cuenta que los &quot;marcos de Analytics&quot; son heredados en AEM y su creación no funciona en AEM as a Cloud Service porque requiere la IU clásica. En su lugar, se debe usar el Launch by Adobe para la asignación de variables y para la implementación de bibliotecas JS en páginas.
* [Integrar Launch by Adobe](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
* [Integración de AEM con Adobe Launch mediante Adobe I/O](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
* [AEM integración con Launch by Adobe, Analytics y Target](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)
* [Configuración del seguimiento de vínculos para Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-link.html)
* [Asignación de datos de componente con propiedades de Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-mapping.html)
* [Configuración del seguimiento de vídeo para Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-video.html)
* [Clasificaciones de Adobe](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-classifications.html)

>[!CAUTION]
>
>Los clientes de Adobe Experience Manager as a Cloud Service que no tengan una cuenta de Analytics existente, pueden solicitar acceso a Analytics Foundation Pack para Experience Cloud.  Este Foundation Pack proporciona un uso limitado del volumen de Analytics.

>[!NOTE]
>
>La configuración de IMS (cuentas técnicas) para Launch by Adobe está preconfigurada en AEM as a Cloud Service. Los usuarios no tienen que crear esta configuración.

## Información adicional {#further-information}

Consulte:

* [Ampliación de la integración con Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-analytics/extending-analytics.html) para obtener información sobre el desarrollo de componentes que recopilan datos de usuario y la personalización del marco de Adobe Analytics. Tenga en cuenta que los &quot;marcos de Analytics&quot; son heredados en AEM y su creación no funciona en AEM as a Cloud Service porque requiere la IU clásica. En su lugar, se debe usar el Launch by Adobe para la asignación de variables y para la implementación de bibliotecas JS en páginas.
* El artículo de la base de conocimiento, [Integración de Adobe Analytics: solución de problemas](https://helpx.adobe.com/experience-manager/kb/sitecatalystintegrationtroubleshooting.html), para obtener información sobre la solución de problemas de la integración de Adobe Analytics.

>[!NOTE]
>
>Si utiliza Adobe Analytics con una configuración proxy personalizada, debe [configurar dos paquetes](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-osgi.html) OSGi (por ejemplo, con la consola web) necesarios para las configuraciones proxy del cliente **HTTP de Apache**. Ambas son necesarias, ya que algunas funcionalidades de AEM utilizan las API 3.x, mientras que otras utilizan las API 4.x. Configuración:
>
>* **Day Commons HTTP Client 3.1** para configurar la API 3.x;
   >  por ejemplo, [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>
>* **Configuración proxy de componentes HTTP de Apache** para configurar la API 4.x;
   >  por ejemplo, [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>

