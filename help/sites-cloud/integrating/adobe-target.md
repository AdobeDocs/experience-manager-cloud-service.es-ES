---
title: Integración con Adobe Target
description: 'Integración con Adobe Target '
translation-type: tm+mt
source-git-commit: bffc335fdafe6bf12a66bcd2f7aacf029fce567e
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 4%

---


# Integración con Adobe Target{#integrating-with-adobe-target}

Como parte de Adobe Marketing Cloud, [Adobe Target](http://www.adobe.com/solutions/testing-targeting/testandtarget.html) le permite aumentar la relevancia del contenido mediante la determinación de objetivos y la medición en todos los canales. Los especialistas en marketing utilizan Adobe Target para diseñar y ejecutar pruebas en línea, crear segmentos de audiencia sobre la marcha (basados en el comportamiento) y automatizar la determinación de objetivos de contenido y experiencias en línea. AEM como Cloud Service ha adoptado el flujo de trabajo de segmentación que se utiliza en Adobe Target Standard. Si utiliza Destinatario, estará familiarizado con el entorno de edición de segmentación en AEM como Cloud Service.

Integre sus sitios AEM con Adobe Target para personalizar el contenido de sus páginas:

* Implemente la segmentación de contenido.
* Utilice audiencias de Destinatario para crear experiencias personalizadas.
* Enviar datos de contexto a Destinatario cuando los visitantes interactúen con las páginas.
* Rastrear tasas de conversión.

>[!NOTE]
>
>Adobe Experience Manager, como cliente Cloud Service que no tiene una cuenta de Destinatario existente, puede solicitar acceso al Destinatario Foundation Pack para Experience Cloud.  Foundation Pack proporciona un uso limitado del Destinatario por volumen.


Para realizar la integración con Destinatario, realice las siguientes tareas:

* [Realizar tareas](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/target-requirements.html) previas: Regístrese con Adobe Target y configure determinados aspectos de la instancia de creación de AEM. Su cuenta de Adobe Target debe tener **permisos de nivel de aprobador** como mínimo. Además, debe proteger la configuración de actividad en el nodo de publicación para que los usuarios no puedan acceder a ella.

* Launch by Adobe es la herramienta de facto para instrumentar un sitio AEM con capacidades de Destinatario (bibliotecas JS). Por lo tanto, la integración de AEM como Cloud Service con Launch y Adobe Target va de la mano (vea los vínculos a continuación).

   * [Integración con Adobe Target mediante Adobe I/O](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/integration-ims-adobe-io.html)
   * [Integrar Launch by Adobe](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
   * [Integrar AEM con el lanzamiento de Adobe mediante Adobe I/O](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
   * [AEM integración con Launch by Adobe, Analytics y Destinatario](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)

>[!NOTE]
>
>La configuración de IMS (cuentas técnicas) para Launch by Adobe está preconfigurada en AEM como Cloud Service. Los usuarios no tienen que crear esta configuración.

1. [Configurar Actividades](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/activitylib.html): Asocie sus Actividades con la configuración de la nube de Destinatario.

>[!CAUTION]
>
>En AEM como Cloud Service, el agente de replicación que sincroniza Ofertas y Actividades de AEM a Adobe Target está deshabilitado de forma predeterminada. Póngase en contacto con el equipo de [Soporte de Adobe](https://helpx.adobe.com/contact/enterprise-support.ec.html#experience-manager) si necesita volver a habilitar el agente de replicación.

>[!NOTE]
>
>Si utiliza Destinatario con una configuración proxy personalizada, debe configurar ambas configuraciones proxy del cliente HTTP, ya que algunas funcionalidades de AEM utilizan las API 3.x y otras las API 4.x:
>
>* 3.x está configurado con [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x está configurado con [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>



>[!CAUTION]
>
>Debe proteger el nodo de configuración de actividad **cq:ActivitySettings** en la instancia de publicación para que los usuarios normales no puedan acceder a él. El nodo de configuración de la actividad solo debe ser accesible para el servicio que administra la sincronización de actividades en Adobe Target.
>
>Consulte [Requisitos previos para la integración con Adobe Target](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/target-requirements.html#securing-the-activity-settings-node) para obtener información detallada.

Una vez completada la integración, puede [crear contenido de destino](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/content-targeting-touch.html) que envíe datos de visitante a Adobe Target. Tenga en cuenta que los componentes de página requieren código específico para habilitar la segmentación de contenido. (Consulte [Desarrollo para contenido de objetivo](https://docs.adobe.com/content/help/en/experience-manager-65/developing/personlization/target.html).

>[!NOTE]
>
>Cuando se destinatario un componente en AEM autor, el componente realiza una serie de llamadas del lado del servidor a Adobe Target para registrar la campaña, configurar ofertas y recuperar segmentos de Adobe Target (si están configurados). No se realizan llamadas del lado del servidor desde AEM publicación en Adobe Target.

## Fuentes de información de fondo {#background-information-sources}

La integración de AEM como Cloud Service con Adobe Target requiere conocimientos de Adobe Target, administración de Actividades de AEM y administración de Audiencias de AEM. Debe estar familiarizado con la siguiente información:

* Adobe Target (consulte la [documentación de Adobe Target](https://docs.adobe.com/content/help/en/target/using/target-home.html)).
* Consola de Actividades AEM (consulte [Administración de Actividades](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/activitylib.html).
* audiencias AEM (Consulte [Administración de Audiencias](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/managing-audiences.html).

>[!NOTE]
>
>Al trabajar con Adobe Target, se muestra el número máximo de artefactos permitidos dentro de una campaña:
>
>* 50 ubicaciones
>* 2.000 experiencias
>* 50 métricas
>* 50 segmentos de sistema de informes

>


