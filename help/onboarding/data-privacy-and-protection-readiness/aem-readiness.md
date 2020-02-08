---
title: 'Regulaciones de protección de datos y privacidad de datos: Adobe Experience Manager como preparación para el servicio en la nube'
description: 'Obtenga información sobre la compatibilidad de Adobe Experience Manager como servicio de nube para las distintas normativas de protección de datos y privacidad de datos; incluyendo el Reglamento General de Protección de Datos de la UE (RGPD), la Ley de Privacidad del Consumidor de California y cómo cumplir al implementar un nuevo proyecto de AEM como servicio de nube. '
translation-type: tm+mt
source-git-commit: 2b7ee2b7b0ce351ed48aeb2f3135c947eafe7247

---


# Adobe Experience Manager como preparación para servicios en la nube para la protección de datos y las regulaciones de privacidad de datos {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>El contenido de este documento no constituye asesoramiento jurídico y no se pretende sustituir al asesoramiento jurídico.
>
>Consulte con el departamento legal de su empresa para obtener asesoramiento acerca de las normas de protección de datos y privacidad de datos.

>[!NOTE]
>
>Para obtener más información sobre la respuesta de Adobe a los problemas de privacidad y lo que esto significa para usted como cliente de Adobe, consulte el Centro [de privacidad de](https://www.adobe.com/privacy.html)Adobe.

Adobe proporciona documentación y procedimientos (con API cuando están disponibles), para que el administrador de privacidad del cliente o el administrador de AEM puedan gestionar las solicitudes de protección de datos y privacidad de datos y ayudar a nuestros clientes a cumplir con estas normativas. Los procedimientos documentados permitirán a los clientes ejecutar las solicitudes reglamentarias manualmente o llamando a las API, cuando estén disponibles, desde un portal o servicio externo.

>[!CAUTION]
>
>Los detalles documentados aquí están restringidos a Adobe Experience Manager como servicio de nube.
>
>Los datos de otro servicio a petición de Adobe, junto con las solicitudes de privacidad relacionadas, requerirán que se realicen acciones en ese servicio.
>
>Para obtener más información, consulte el Centro [de privacidad de](https://www.adobe.com/privacy.html)Adobe.

## Introducción {#introduction}

Las instancias de Adobe Experience Manager como servicio de nube y las aplicaciones que se ejecutan en ellos son propiedad de nuestros clientes y son operadas por ellos.

En consecuencia, las regulaciones de protección de datos, como el RGPD, la CCPA y otras, son en gran medida responsabilidad de los clientes.

Como breve introducción, las regulaciones para la protección y la privacidad de los datos incluyen nuevas normas que deben ir seguidas de las funciones de:

* Entidades comerciales (CCPA) y/o controladores de datos (RGPD)

* Proveedores de servicios (CCPA) y/o procesadores de datos (RGPD)

Las principales disposiciones de esos reglamentos son las siguientes:

1. Definición ampliada de datos personales para incluir todos los ID únicos; como en datos identificables directa e indirectamente.

2. Reforzar los requisitos de consentimiento.

3. Se ha aumentado el enfoque en los derechos de eliminación (Eliminación de datos).

4. Exclusión de la venta de datos.

Para Adobe Experience Manager como servicio de nube:

* Las instancias, y las aplicaciones que se ejecutan en ellas, son propiedad del cliente y son operadas por él.

   * Esto significa efectivamente que el cliente administra las funciones reglamentarias, incluidas las entidades comerciales y el proveedor de servicios, el controlador de datos y el procesador de datos, entre otras.

   * Adobe Experience Platform Privacy Service no formará parte del flujo de trabajo para AEM, como se ilustra en el diagrama siguiente.

* AEM incluye documentación y procedimientos para que el administrador de privacidad del cliente y/o el administrador de AEM ejecuten las solicitudes de regulación de privacidad; manualmente o a través de API, cuando esté disponible.

* No se ha agregado ningún servicio ni interfaz de usuario nuevos.

   * En su lugar, los procedimientos y las API están documentados para su uso por las UI/portales del cliente que gestionan solicitudes de regulación de privacidad.

* AEM no incluirá ninguna herramienta lista para usar para admitir el flujo de trabajo de las solicitudes de privacidad.

   * Adobe proporcionará documentación y procedimientos para el administrador de privacidad del cliente y/o el administrador de AEM, permitiéndoles ejecutar manualmente las solicitudes relacionadas con las normativas de privacidad.

Adobe proporciona procedimientos para gestionar solicitudes de privacidad relacionadas con Access, Delete y Opt-Out para Adobe Experience Manager como un servicio de nube. En algunos casos, hay API disponibles que se pueden llamar desde un portal desarrollado por el cliente o desde scripts para ayudar con la automatización.

El diagrama siguiente ilustra el aspecto que podría tener un flujo de trabajo de solicitud de privacidad (ilustrado con Adobe Experience Manager 6.5):

![Protección de datos y privacidad](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager como servicio de nube y preparación para la regulación {#aem-as-a-cloud-service-and-regulatory-readiness}

Consulte las secciones siguientes para obtener documentación normativa sobre las áreas de producto de AEM como un servicio en la nube.

## Adobe Experience Manager como base de servicios en la nube {#aem-foundation}

Consulte [AEM Foundation Readiness for Data Protection and Data Privacy Regulation](/help/onboarding/data-privacy-and-protection-readiness/foundation-readiness.md).

## Adobe Experience Manager como sitios de servicios en la nube {#aem-sites}

Consulte Preparación de los sitios [AEM para la protección de datos y Regulaciones de privacidad de datos.](/help/onboarding/data-privacy-and-protection-readiness/sites-readiness.md)

## Adobe Experience Manager como integración de servicios en la nube con Adobe Target y Adobe Analytics {#aem-integration-with-adobe-target-adobe-analytics}

Estas integraciones de Adobe Experience Manager como servicio de nube se realizan con servicios preparados para la protección de datos y la privacidad (por ejemplo, GDPR). No se almacenan datos personales de Adobe Target o Adobe Analytics en AEM en relación con las integraciones.
Para obtener más información, consulte:

* [Adobe Target: Información general de privacidad](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/privacy.html)

* [Flujo de trabajo de privacidad de datos de Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)
