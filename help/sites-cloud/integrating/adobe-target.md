---
title: Integración con Adobe Target
description: 'Integración con Adobe Target '
translation-type: tm+mt
source-git-commit: 5a7f2d603952b2c5f92363888efedb482d8efea3

---


# Integración con Adobe Target{#integrating-with-adobe-target}

Como parte de Adobe Marketing Cloud, [Adobe Target](http://www.adobe.com/solutions/testing-targeting/testandtarget.html) le permite aumentar la relevancia del contenido mediante la determinación de objetivos y la medición en todos los canales. Los especialistas en marketing utilizan Adobe Target para diseñar y ejecutar pruebas en línea, crear segmentos de audiencia sobre la marcha (según el comportamiento) y automatizar la segmentación del contenido y las experiencias en línea. AEM como servicio de nube ha adoptado el flujo de trabajo de segmentación que se utiliza en Adobe Target Standard. Si usa Target, estará familiarizado con el entorno de edición de segmentación en AEM como un servicio de nube.

Integre sus sitios de AEM con Adobe Target para personalizar el contenido de sus páginas:

* Implemente la segmentación de contenido.
* Utilice las audiencias de Target para crear experiencias personalizadas.
* Envíe datos de contexto a Target cuando los visitantes interactúen con sus páginas.
* Rastree las tasas de conversión.

>[!NOTE]
>
>Adobe Experience Manager como cliente de servicios en la nube que no tiene una cuenta de Target existente, puede solicitar acceso a Target Foundation Pack para Experience Cloud.  Foundation Pack proporciona un uso limitado del volumen de Target.


Para realizar la integración con Target, realice las siguientes tareas:

* [Realizar tareas](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/target-requirements.html)previas: Regístrese con Adobe Target y configure determinados aspectos de la instancia de creación de AEM. La cuenta de Adobe Target debe tener permisos de **nivel de aprobador** como mínimo. Además, debe proteger la configuración de la actividad en el nodo de publicación para que los usuarios no puedan acceder a ella.

* Launch de Adobe es la herramienta de facto para instrumentar un sitio de AEM con capacidades de Target (bibliotecas JS). Por lo tanto, la integración de AEM como servicio de nube con Launch y Adobe Target va de la mano (consulte los vínculos siguientes).

   * [Integración con Adobe Target mediante Adobe I/O](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/integration-ims-adobe-io.html)
   * [Integrar Launch de Adobe](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
   * [Integración de AEM con Adobe Launch mediante Adobe I/O](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
   * [Información sobre la integración de AEM con Launch de Adobe, Analytics y Target](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)

>[!NOTE]
>
>La configuración de IMS (cuentas técnicas) para Launch de Adobe está preconfigurada en AEM como un servicio de nube. Los usuarios no tienen que crear esta configuración.

1. [Configurar actividades](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/activitylib.html): Asocie sus actividades a la configuración de la nube de Target.

>[!CAUTION]
>
>&quot;En AEM como servicio de nube, el agente de replicación que sincroniza ofertas y actividades de AEM con Adobe Target está deshabilitado de forma predeterminada. Póngase en contacto con el servicio de asistencia técnica [de](https://helpx.adobe.com/contact/enterprise-support.ec.html#target) Adobe si necesita volver a habilitar el agente de replicación&quot;.

>[!NOTE]
>
>Si está utilizando Target con una configuración proxy personalizada, debe configurar ambas configuraciones proxy del cliente HTTP, ya que algunas funcionalidades de AEM están utilizando las API 3.x y otras, las API 4.x:
>
>* 3.x está configurado con [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x está configurado con [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>



>[!CAUTION]
>
>You must secure the activity settings node **cq:ActivitySettings** on the publish instance so that it is inaccessible to normal users. El nodo de configuración de la actividad solo debe ser accesible para el servicio que administra la sincronización de actividades en Adobe Target.
>
>See [Prerequisites for Integrating with Adobe Target](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/target-requirements.html#securing-the-activity-settings-node) for detailed information.

Una vez completada la integración, puede [crear contenido](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/content-targeting-touch.html) de destino que envíe datos de visitantes a Adobe Target. Tenga en cuenta que los componentes de página requieren código específico para habilitar la segmentación de contenido. (Consulte [Desarrollo de contenido](https://docs.adobe.com/content/help/en/experience-manager-65/developing/personlization/target.html)de destino.

>[!NOTE]
>
>Cuando se dirige a un componente en un autor de AEM, el componente realiza una serie de llamadas del lado del servidor a Adobe Target para registrar la campaña, configurar ofertas y recuperar segmentos de Adobe Target (si están configurados). No se realiza ninguna llamada al servidor desde la publicación de AEM en Adobe Target.

## Fuentes de información de fondo {#background-information-sources}

La integración de AEM como un servicio de nube con Adobe Target requiere conocimientos sobre Adobe Target, la gestión de actividades de AEM y la gestión de audiencias de AEM. Debe estar familiarizado con la siguiente información:

* Adobe Target (consulte la documentación [de](https://marketing.adobe.com/resources/help/en_US/target/)Adobe Target).
* Consola de actividades de AEM (consulte [Administración de actividades](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/activitylib.html).
* Audiencias AEM (consulte [Administración de audiencias](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/managing-audiences.html).

>[!NOTE]
>
>Al trabajar con Adobe Target, se muestra el número máximo de artefactos permitidos en una campaña:
>
>* 50 ubicaciones
>* 2.000 experiencias
>* 50 métricas
>* 50 segmentos de informes
>


