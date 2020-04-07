---
title: Integración con Adobe Target
description: 'Integración con Adobe Target '
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14

---


# Integración con Adobe Target{#integrating-with-adobe-target}

Como parte de Adobe Marketing Cloud, [Adobe Destinatario](http://www.adobe.com/solutions/testing-targeting/testandtarget.html) le permite aumentar la relevancia del contenido mediante la determinación de objetivos y la medición en todos los canales. Los especialistas en marketing utilizan Adobe Destinatario para diseñar y ejecutar pruebas en línea, crear segmentos de audiencia sobre la marcha (según el comportamiento) y automatizar la segmentación del contenido y las experiencias en línea. AEM como servicio de nube ha adoptado el flujo de trabajo de segmentación que se utiliza en Adobe Destinatario Standard. Si utiliza Destinatario, estará familiarizado con el entorno de edición de segmentación en AEM como servicio de nube.

Integre sus sitios de AEM con Adobe Destinatario para personalizar el contenido de sus páginas:

* Implemente la segmentación de contenido.
* Utilice audiencias de Destinatario para crear experiencias personalizadas.
* Enviar datos de contexto a Destinatario cuando los visitantes interactúen con las páginas.
* Rastrear tasas de conversión.

>[!NOTE]
>
>Adobe Experience Manager como cliente de servicios en la nube que no tiene una cuenta de Destinatario existente, puede solicitar acceso a Destinatario Foundation Pack para Experience Cloud.  Foundation Pack proporciona un uso limitado del Destinatario por volumen.


Para realizar la integración con Destinatario, realice las siguientes tareas:

* [Realizar tareas](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/target-requirements.html)previas: Regístrese con Adobe Destinatario y configure determinados aspectos de la instancia de creación de AEM. La cuenta de Adobe Destinatario debe tener como mínimo permisos de **nivel de aprobador** . Además, debe proteger la configuración de actividad en el nodo de publicación para que los usuarios no puedan acceder a ella.

* Launch by Adobe es la herramienta de facto para instrumentar un sitio de AEM con funciones de Destinatario (bibliotecas JS). Por lo tanto, la integración de AEM como servicio de nube con Launch y Adobe Destinatario va de la mano (consulte los vínculos siguientes).

   * [Integración con Adobe Destinatario mediante Adobe I/O](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/integration-ims-adobe-io.html)
   * [Integrar Launch de Adobe](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
   * [Integración de AEM con Adobe Launch mediante Adobe I/O](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
   * [Información sobre la integración de AEM con Launch de Adobe, Analytics y Destinatario](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)

>[!NOTE]
>
>La configuración de IMS (cuentas técnicas) para Launch de Adobe está preconfigurada en AEM como un servicio de nube. Los usuarios no tienen que crear esta configuración.

1. [Configurar Actividades](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/activitylib.html): Asocie sus Actividades con la configuración de la nube de Destinatario.

>[!CAUTION]
>
>En AEM como servicio de nube, el agente de replicación que sincroniza Ofertas y Actividades de AEM con Adobe Destinatario está deshabilitado de forma predeterminada. Póngase en contacto con el equipo de asistencia [de](https://helpx.adobe.com/contact/enterprise-support.ec.html#experience-manager) Adobe si necesita volver a habilitar el agente de replicación.

>[!NOTE]
>
>Si está utilizando Destinatario con una configuración proxy personalizada, debe configurar ambas configuraciones proxy del cliente HTTP, ya que algunas funcionalidades de AEM están utilizando las API 3.x y otras las API 4.x:
>
>* 3.x está configurado con [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x está configurado con [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>



>[!CAUTION]
>
>You must secure the activity settings node **cq:ActivitySettings** on the publish instance so that it is inaccessible to normal users. El nodo de configuración de la actividad solo debe ser accesible para el servicio que administra la sincronización de actividades en Adobe Target.
>
>See [Prerequisites for Integrating with Adobe Target](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/target-requirements.html#securing-the-activity-settings-node) for detailed information.

Una vez completada la integración, puede [crear contenido](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/content-targeting-touch.html) de destino que envíe datos de visitante a Adobe Destinatario. Tenga en cuenta que los componentes de página requieren código específico para habilitar la segmentación de contenido. (Consulte [Desarrollo de contenido](https://docs.adobe.com/content/help/en/experience-manager-65/developing/personlization/target.html)de destino.

>[!NOTE]
>
>Cuando se destinatario un componente en el autor de AEM, el componente realiza una serie de llamadas del lado del servidor a Adobe Destinatario para registrar la campaña, configurar ofertas y recuperar segmentos de Adobe Destinatario (si están configurados). No se realizan llamadas del lado del servidor desde la publicación de AEM en Adobe Destinatario.

## Fuentes de información de fondo {#background-information-sources}

La integración de AEM como un servicio de nube con Adobe Destinatario requiere conocimientos sobre Adobe Destinatario, la administración de Actividades AEM y la administración de Audiencias AEM. Debe estar familiarizado con la siguiente información:

* Adobe Destinatario (consulte la documentación [de](https://marketing.adobe.com/resources/help/en_US/target/)Adobe Destinatario).
* Consola de Actividades AEM (consulte [Administración de Actividades](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/activitylib.html).
* Audiencias de AEM (consulte [Administración de Audiencias](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/managing-audiences.html).

>[!NOTE]
>
>Cuando se trabaja con Adobe Destinatario, el número máximo de artefactos permitidos dentro de una campaña es el siguiente:
>
>* 50 ubicaciones
>* 2.000 experiencias
>* 50 métricas
>* 50 segmentos de sistema de informes
>


