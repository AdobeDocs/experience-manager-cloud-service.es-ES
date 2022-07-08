---
title: 'Integración con Adobe Analytics '
description: 'Integración con Adobe Analytics '
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: ht
source-wordcount: '545'
ht-degree: 100%

---


# Integración con Adobe Analytics{#integrating-with-adobe-analytics}

La integración de Adobe Analytics y AEM as a Cloud Service permite rastrear la actividad de la página web:

* Una configuración de Adobe Analytics permite a AEM autenticarse con Adobe Analytics.
* Un marco de trabajo identifica los datos que se envían al grupo de informes de Adobe Analytics.

Los datos incluyen datos de páginas y usuarios, por ejemplo:

* datos que recopilan los componentes de AEM
* clics en vínculos
* información de uso de vídeo
* número de visitas a la página desde Adobe Analytics

Las páginas que se nombran a continuación pueden ayudarle a configurar la integración. Tenga en cuenta que Launch by Adobe es la herramienta de facto para dotar a un sitio de AEM de las capacidades de Analytics (bibliotecas JS). Por lo tanto, la integración de AEM as a Cloud Service con Launch y Adobe Analytics va de la mano.

* [Conexión a Adobe Analytics y creación de marcos de trabajo](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-connect.html?lang=es): tenga en cuenta que los “marcos de trabajo de Analytics” son heredados en AEM y su creación no funciona en AEM as a Cloud Service porque requiere la IU clásica. En su lugar, se debe usar Launch by Adobe para la asignación de variables y para la implementación de bibliotecas JS en páginas.
* [Integración de Launch by Adobe](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand?lang=es)
* [Integración de AEM con Adobe Launch mediante Adobe I/O](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html?lang=es)
* [Explicación de la integración de AEM con Launch by Adobe, Analytics y Target](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html?lang=es)
* [Configuración de Seguimiento de vínculos para Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-link.html?lang=es)
* [Asignación de datos de componente con propiedades de Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-mapping.html?lang=es)
* [Configuración del seguimiento de vídeo para Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-video.html?lang=es)
* [Clasificaciones de Adobe](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-classifications.html?lang=es)

>[!CAUTION]
>
>Los clientes de Adobe Experience Manager as a Cloud Service que no tengan cuenta de Analytics pueden solicitar acceso al paquete Analytics Foundation para Experience Cloud.  Este paquete Foundation proporciona un volumen de uso limitado de Analytics.

>[!NOTE]
>
>La configuración de IMS (cuentas técnicas) para Launch by Adobe está preconfigurada en AEM as a Cloud Service. Los usuarios no tienen que crear esta configuración.

## Información adicional {#further-information}

Consulte:

* [Ampliación de la integración con Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-analytics/extending-analytics.html?lang=es) para obtener información acerca del desarrollo de componentes que recopilan datos de usuario y la personalización del marco de trabajo de Adobe Analytics. Tenga en cuenta que los “marcos de trabajo de Analytics” son heredados en AEM y su creación no funciona en AEM as a Cloud Service porque requiere la IU clásica. En su lugar, se debe usar Launch by Adobe para la asignación de variables y para la implementación de bibliotecas JS en páginas.
* El artículo de la base de conocimiento, [Integración de Adobe Analytics: solución de problemas](https://helpx.adobe.com/es/experience-manager/kb/sitecatalystintegrationtroubleshooting.html), para obtener información acerca de la solución de problemas de la integración de Adobe Analytics.

>[!NOTE]
>
>Si utiliza Adobe Analytics con una configuración proxy personalizada, debe [configurar dos paquetes](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-osgi.html?lang=es) OSGi (por ejemplo, con la consola web) necesarios para las configuraciones proxy del cliente **HTTP de Apache**. Ambas son necesarias, ya que algunas funcionalidades de AEM utilizan las API 3.x, mientras que otras utilizan las API 4.x. Configuración de:
>
>* **Cliente HTTP 3.1 de Day Commons** para configurar la API 3.x;
   >  por ejemplo, [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>
>* **Configuración proxy de componentes HTTP de Apache** para configurar la API 4.x;
   >  por ejemplo, [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>

