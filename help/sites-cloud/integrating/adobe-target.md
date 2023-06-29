---
title: Integración con Adobe Target
description: Integración con Adobe Target
exl-id: 2b4cf35e-2b75-4303-8d09-f6644ad99274
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 72%

---

# Integración con Adobe Target{#integrating-with-adobe-target}

Como parte de Adobe Experience Cloud, [Adobe Target](https://business.adobe.com/products/target/adobe-target.html) le permite aumentar la relevancia del contenido mediante el direccionamiento y efectuando mediciones en todos los canales. Los especialistas en marketing utilizan Adobe Target para diseñar y ejecutar pruebas en línea, crear segmentos de audiencia sobre la marcha (basados en el comportamiento) y automatizar el direccionamiento del contenido y las experiencias en línea. AEM as a Cloud Service ha adoptado el flujo de trabajo de direccionamiento que se utiliza en Adobe Target Standard. AEM Si utiliza Target, estará familiarizado con el entorno de edición de direccionamiento en el as a Cloud Service de la.

AEM Integre los sitios de la con Adobe Target para poder personalizar el contenido de sus páginas:

* Implemente la segmentación de contenido.
* Utilice las audiencias de Target para crear experiencias personalizadas.
* Envíe datos de contexto a Target cuando los visitantes interactúen con las páginas.
* Rastree las tasas de conversión.

>[!NOTE]
>
>Los clientes que no tengan una cuenta de Target existente pueden solicitar acceso a Target Foundation Pack para Experience Cloud. Foundation Pack proporciona un uso limitado del volumen de Target.


Para integrarse con Target, realice las siguientes tareas:

* [Realizar tareas previas](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-requirements.html?lang=es): regístrese en Adobe Target y configure ciertos aspectos de la instancia de autor de AEM. La cuenta de Adobe Target debe tener permisos de nivel de **aprobador** como mínimo. Además, debe proteger la configuración de actividad en el nodo de publicación para que los usuarios no puedan acceder a ella.

* Experience Platform Launch es la herramienta para instrumentar un sitio AEM con capacidades de Target (bibliotecas JS). Por lo tanto, la integración de AEM as a Cloud Service con Launch y Adobe Target se realiza de forma conjunta (consulte los vínculos a continuación).

   * [Integración con Adobe Target mediante Adobe I/O](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/integration-target-ims.html)
   * [Integrar Experience Platform Launch](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/overview.html)
   * [AEM Integración de la con Adobe Launch mediante el Adobe I/O](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/overview.html?lang=en)
   * [Explicación de la integración de AEM con Experience Platform Launch, Analytics y Target](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/overview.html)

>[!NOTE]
>
>La configuración de IMS (cuentas técnicas) para Experience Platform Launch está preconfigurada en AEM as a Cloud Service. Los usuarios no tienen que crear esta configuración.

1. [Configurar actividades](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/activitylib.html?lang=es): asocie sus actividades a la configuración de nube de Target.

>[!CAUTION]
>
>En AEM as a Cloud Service, el agente de replicación que sincroniza Ofertas y actividades de AEM a Adobe Target está deshabilitado de forma predeterminada. Póngase en contacto con [Compatibilidad con Adobe](https://experienceleague.adobe.com/?support-solution=General&amp;lang=es#support) si debe volver a activar el agente de replicación.

>[!NOTE]
>
>AEM Si utiliza Target con una configuración proxy personalizada, debe configurar ambas configuraciones proxy del cliente HTTP, ya que algunas funcionalidades de los utilizan las API 3.x y otras las API 4.x:
>
>* 3.x está configurado con [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x está configurado con [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>

>[!CAUTION]
>
>Proteja el nodo de configuración de la actividad **cq:ActivitySettings** en la instancia de publicación, para que los usuarios normales no puedan acceder a ella. El nodo de configuración de la actividad solo debe ser accesible para el servicio que administra la sincronización de actividades en Adobe Target.
>
>Consulte [Requisitos previos para la integración con Adobe Target](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-requirements.html?lang=es#securing-the-activity-settings-node) para obtener información detallada.

Cuando se complete la integración, puede [crear contenido de destino](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/content-targeting-touch.html?lang=es) para enviar datos sobre visitantes a Adobe Target. Los componentes de página requieren un código específico para habilitar la segmentación de contenido. (Consulte [Desarrollo de contenido de destino](https://experienceleague.adobe.com/docs/experience-manager-65/developing/personlization/target.html?lang=es)).

>[!NOTE]
>
>Cuando se marca un componente como objetivo en el autor AEM, este realiza una serie de llamadas del lado del servidor a Adobe Target para registrar la campaña, configurar ofertas y recuperar segmentos de Adobe Target (si están configurados). No se realizan llamadas del lado del servidor desde publicaciones de AEM a Adobe Target.

## Fuentes de información de fondo {#background-information-sources}

La integración de AEM as a Cloud Service con Adobe Target requiere conocimientos de Adobe Target, gestión de AEM Activities y gestión de AEM Audiences. Debe estar familiarizado con la siguiente información:

* Adobe Target (consulte la [documentación de Adobe Target](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=es)).
* Consola de AEM Activities (consulte [Administración de actividades](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/activitylib.html?lang=es)).
* AEM Audiences (consulte [Administración de audiencias](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/managing-audiences.html?lang=es)).

>[!NOTE]
>
>Al trabajar con Adobe Target, el siguiente número de artefactos es el máximo permitido dentro de una campaña:
>
>* 50 ubicaciones
>* 2000 experiencias
>* 50 métricas
>* 50 segmentos de creación de informes
