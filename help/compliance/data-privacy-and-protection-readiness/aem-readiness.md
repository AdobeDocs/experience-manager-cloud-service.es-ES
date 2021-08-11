---
title: 'Reglamentos de protección de datos y privacidad de datos: preparación de Adobe Experience Manager as a Cloud Service'
description: Obtenga información sobre la compatibilidad de Adobe Experience Manager como Cloud Service con las distintas normas de protección de datos y privacidad de datos; incluido el Reglamento General de Protección de Datos (RGPD) de la UE, la Ley de Privacidad del Consumidor de California y cómo cumplir al implementar un nuevo proyecto de AEM como Cloud Service.
exl-id: 5dfa353b-84c5-4b07-bfcd-b03c2d361553
source-git-commit: e9c1ec6807f86ab00f89ef292a89a0c8efdf802b
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 2%

---

# Adobe Experience Manager como Cloud Service listo para la protección de datos y las normas de privacidad de datos {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>El contenido de este documento no constituye asesoramiento jurídico y no está pensado para sustituir el asesoramiento jurídico.
>
>Consulte con el departamento legal de su empresa para obtener asesoramiento sobre la protección de datos y las normas de privacidad de datos.

>[!NOTE]
>
>Para obtener más información sobre la respuesta del Adobe a los problemas de privacidad y lo que esto supone para usted como cliente de Adobe, consulte [Centro de privacidad de Adobe](https://www.adobe.com/privacy.html).

Adobe proporciona documentación y procedimientos (con API cuando están disponibles), para que el administrador de privacidad del cliente o AEM administrador gestione las solicitudes de protección de datos y privacidad de datos y ayude a nuestros clientes a cumplir con estas regulaciones. Los procedimientos documentados permitirán a los clientes ejecutar las solicitudes reglamentarias manualmente o llamando a las API, si están disponibles, desde un portal o servicio externo.

>[!CAUTION]
>
>Los detalles documentados aquí están restringidos a Adobe Experience Manager como Cloud Service.
>
>Los datos de otro servicio bajo demanda de Adobe, junto con cualquier solicitud de privacidad relacionada, requerirán que se realicen acciones en ese servicio.
>
>Para obtener más información, consulte [Centro de privacidad del Adobe](https://www.adobe.com/privacy.html).

## Introducción {#introduction}

Las instancias de Adobe Experience Manager como Cloud Service, y las aplicaciones que se ejecutan en ellas, son propiedad de nuestros clientes y son operadas por ellos.

Como consecuencia, las regulaciones de protección de datos, como el RGPD, la CCPA y otras, son en gran medida responsabilidad de los clientes.

Como introducción muy breve, las regulaciones para la privacidad y protección de datos incluyen nuevas reglas a las que deben seguir las funciones de:

* Entidades comerciales (CCPA) y/o controladores de datos (RGPD)

* Proveedores de servicios (CCPA) y/o procesadores de datos (RGPD)

Las principales disposiciones de esos reglamentos son las siguientes:

1. Definición ampliada de datos personales para incluir todos los ID únicos; como en datos directa e indirectamente identificables.

2. Fortalecimiento de los requisitos de consentimiento.

3. Mayor atención a los derechos de eliminación (eliminación de datos).

4. Exclusión de la venta de datos.

Para Adobe Experience Manager as a Cloud Service:

* Las instancias, y las aplicaciones que se ejecutan en ellas, son propiedad del cliente y las gestiona.

   * Esto significa que el cliente gestiona las funciones regulatorias, incluidas las Entidades del negocio y el proveedor de servicios, el controlador de datos y el procesador de datos, entre otras.

   * Adobe Experience Platform Privacy Service no formará parte del flujo de trabajo para AEM, como se ilustra en el diagrama siguiente.

* AEM incluye documentación y procedimientos para el administrador de privacidad del cliente o AEM administrador para ejecutar las solicitudes de regulación de privacidad; manualmente o a través de API, cuando esté disponible.

* No se ha agregado ningún servicio ni interfaz de usuario nuevos.

   * En su lugar, los procedimientos y las API están documentados para su uso por las IU o portales de los clientes que administran solicitudes de regulación de la privacidad.

* AEM incluirá ninguna herramienta predeterminada para admitir el flujo de trabajo de solicitudes de privacidad.

   * Adobe proporcionará documentación y procedimientos para el administrador de privacidad o AEM del cliente, lo que les permitirá ejecutar manualmente las solicitudes relacionadas con las normas de privacidad.

Adobe proporciona procedimientos para gestionar solicitudes de privacidad relacionadas con Acceso, Eliminación y Exclusión para Adobe Experience Manager como Cloud Service. En algunos casos, hay API disponibles a las que se puede llamar desde un portal o scripts desarrollados por el cliente para ayudar con la automatización.

El diagrama siguiente ilustra el aspecto que podría tener un flujo de trabajo de solicitud de privacidad (ilustrado con Adobe Experience Manager 6.5):

![Protección de datos y privacidad](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager como Cloud Service y preparación para la regulación {#aem-as-a-cloud-service-and-regulatory-readiness}

Consulte las secciones siguientes para obtener documentación reglamentaria sobre áreas de producto de AEM como Cloud Service.

## Adobe Experience Manager as a Cloud Service Foundation {#aem-foundation}

Consulte [Preparación de base AEM para la protección de datos y las normas de privacidad de datos](/help/compliance/data-privacy-and-protection-readiness/foundation-readiness.md).

## Sitios de Adobe Experience Manager as a Cloud Service {#aem-sites}

Consulte [Preparación de AEM Sites para la protección de datos y las normas de privacidad de datos.](/help/compliance/data-privacy-and-protection-readiness/sites-readiness.md)

## Integración de Adobe Experience Manager as a Cloud Service con Adobe Target y Adobe Analytics {#aem-integration-with-adobe-target-adobe-analytics}

Estas integraciones de Adobe Experience Manager as a Cloud Service se realizan con servicios preparados para la protección de datos y la privacidad (por ejemplo, RGPD). No se almacenan datos personales de Adobe Target o Adobe Analytics en AEM en relación con las integraciones.
Para obtener más información, consulte:

* [Adobe Target: Información general de privacidad](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/privacy.html)

* [Flujo de trabajo de privacidad de datos de Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-workflow.html)
