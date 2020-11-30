---
title: 'Normas de protección de datos y privacidad de datos: Adobe Experience Manager como Cloud Service listo'
description: 'Obtenga información sobre Adobe Experience Manager como Cloud Service de soporte para las distintas normas de protección de datos y privacidad de datos; incluyendo el Reglamento General de Protección de Datos de la UE (RGPD), la Ley de Privacidad del Consumidor de California y cómo cumplir con la implementación de un nuevo AEM como proyecto Cloud Service. '
translation-type: tm+mt
source-git-commit: 2b7ee2b7b0ce351ed48aeb2f3135c947eafe7247
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 2%

---


# Adobe Experience Manager como Cloud Service listo para la protección de datos y las regulaciones de privacidad de datos {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>El contenido del presente documento no constituye asesoramiento jurídico y no sustituye al asesoramiento jurídico.
>
>Consulte con el departamento legal de su compañía para obtener asesoramiento sobre las normas de protección de datos y privacidad de datos.

>[!NOTE]
>
>Para obtener más información sobre la respuesta del Adobe a los problemas de privacidad y lo que esto significa para usted como cliente de Adobe, consulte el Centro de privacidad del [Adobe](https://www.adobe.com/privacy.html).

Adobe proporciona documentación y procedimientos (con API cuando están disponibles), para que el administrador de privacidad del cliente o AEM administrador se encargue de la protección de datos y las solicitudes de privacidad de datos y ayude a nuestros clientes a cumplir con estas normativas. Los procedimientos documentados permitirán a los clientes ejecutar las solicitudes reglamentarias manualmente o llamando a las API, cuando estén disponibles, desde un portal o servicio externo.

>[!CAUTION]
>
>Los detalles documentados aquí están restringidos a Adobe Experience Manager como Cloud Service.
>
>Los datos de otro servicio a petición de Adobe, junto con las solicitudes de privacidad relacionadas, requerirán que se realicen acciones en ese servicio.
>
>Para obtener más información, consulte el Centro [de privacidad de](https://www.adobe.com/privacy.html)Adobe.

## Introducción {#introduction}

Las instancias de Adobe Experience Manager como Cloud Service, y las aplicaciones que se ejecutan en ellas, son propiedad de nuestros clientes y son operadas por ellos.

En consecuencia, las regulaciones de protección de datos, como el RGPD, la CCPA y otras, son en gran medida responsabilidad de los clientes.

Como breve introducción, las regulaciones para la protección y la privacidad de los datos incluyen nuevas normas que deben ir seguidas de las funciones de:

* Entidades comerciales (CCPA) y/o controladores de datos (RGPD)

* proveedores de servicio (CCPA) y/o procesadores de datos (RGPD)

Las principales disposiciones de esos reglamentos son las siguientes:

1. Definición ampliada de datos personales para incluir todos los ID únicos; como en datos identificables directa e indirectamente.

2. Reforzar los requisitos de consentimiento.

3. Se ha aumentado el enfoque en los derechos de eliminación (Eliminación de datos).

4. Exclusión de la venta de datos.

Para Adobe Experience Manager como Cloud Service:

* Las instancias, y las aplicaciones que se ejecutan en ellas, son propiedad del cliente y son operadas por él.

   * Esto significa que el cliente gestiona las funciones reglamentarias, incluidas las entidades comerciales y el Proveedor de servicio, el controlador de datos y el procesador de datos, entre otras.

   * El Adobe Experience Platform Privacy Service no formará parte del flujo de trabajo para AEM, como se ilustra en el diagrama siguiente.

* AEM incluye documentación y procedimientos para que el administrador de privacidad del cliente y/o AEM administrador ejecuten las solicitudes de regulación de privacidad; manualmente o a través de API, cuando esté disponible.

* No se ha agregado ningún servicio ni interfaz de usuario nuevos.

   * En su lugar, los procedimientos y las API están documentados para su uso por las UI/portales del cliente que gestionan solicitudes de regulación de privacidad.

* No AEM ninguna herramienta lista para usar para admitir el flujo de trabajo de las solicitudes de privacidad.

   * Adobe proporcionará documentación y procedimientos para el administrador de privacidad del cliente y/o AEM administrador, permitiéndole ejecutar manualmente las solicitudes relacionadas con las normativas de privacidad.

Adobe proporciona procedimientos para gestionar las solicitudes de privacidad relacionadas con Access, Delete y Opt-Out para Adobe Experience Manager como Cloud Service. En algunos casos, hay API disponibles que se pueden llamar desde un portal desarrollado por el cliente o desde scripts para ayudar con la automatización.

El diagrama siguiente ilustra el aspecto que podría tener un flujo de trabajo de solicitud de privacidad (ilustrado con Adobe Experience Manager 6.5):

![Protección de datos y privacidad](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager como Cloud Service y listo para la regulación {#aem-as-a-cloud-service-and-regulatory-readiness}

Consulte las secciones a continuación para obtener documentación reglamentaria sobre las áreas de producto de AEM como Cloud Service.

## Adobe Experience Manager as a Cloud Service Foundation {#aem-foundation}

See [AEM Foundation Readiness for Data Protection and Data Privacy Regulations](/help/onboarding/data-privacy-and-protection-readiness/foundation-readiness.md).

## Sitios de Adobe Experience Manager as a Cloud Service {#aem-sites}

See [AEM Sites Readiness for Data Protection and Data Privacy Regulations.](/help/onboarding/data-privacy-and-protection-readiness/sites-readiness.md)

## Adobe Experience Manager como Cloud Service integrado con Adobe Target y Adobe Analytics {#aem-integration-with-adobe-target-adobe-analytics}

Estas integraciones de Adobe Experience Manager como Cloud Service están con servicios listos para protección de datos y privacidad (por ejemplo, RGPD). No se almacenan datos personales de Adobe Target o Adobe Analytics en AEM en relación con las integraciones.
Para obtener más información, consulte:

* [Adobe Target: Información general de privacidad](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/privacy.html)

* [Flujo de trabajo de privacidad de datos de Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)
