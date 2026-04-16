---
title: Preparación para HIPAA para Adobe Experience Manager as a Cloud Service
description: Obtenga información acerca de la compatibilidad de Experience Manager as a Cloud Service con las regulaciones HIPAA y cómo cumplirlas al implementar un nuevo proyecto de AEM as a Cloud Service.
feature: Compliance
role: Admin, Architect, Developer, Leader
source-git-commit: 49721ac71bc2bde10eb5f25db58ee1b07c8a82e5
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 6%

---

# Preparación para HIPAA para Adobe Experience Manager as a Cloud Service {#hipaa-readiness-for-adobe-experience-manager-as-a-cloud-service}

>[!WARNING]
>
>El contenido de este documento no constituye asesoramiento jurídico y no está pensado para sustituirlo.
>
>Consulte al departamento legal de su empresa para obtener asesoramiento sobre las regulaciones de HIPAA.

>[!NOTE]
>
>Para obtener más información sobre la respuesta de Adobe a los problemas de privacidad y lo que esto supone para usted como cliente de Adobe, consulte:
>
>* [Productos y servicios de HIPAA y Adobe](https://www.adobe.com/trust/compliance/hipaa-hds/hipaa-ready.html) en el Centro de confianza de Adobe
>* [Centro de privacidad de Adobe](https://www.adobe.com/es/privacy.html)

Para Adobe Experience Manager (AEM) as a Cloud Service, Adobe proporciona documentación que le ayudará a comprender la preparación para la HIPAA. Puede ayudarle a cumplir con estas regulaciones.

## Ley de Portabilidad y Responsabilidad del Seguro de Salud (HIPAA) {#health-insurance-portability-and-accountability-act-hipaa}

### La Ley de Portabilidad y Responsabilidad del Seguro de Salud (HIPAA) {#the-health-insurance-portability-and-accountability-act-hipaa}

Las Reglas de Privacidad, Seguridad y Notificación de Infracciones de la HIPAA establecen protecciones importantes para la información de salud identificable individualmente conocida como Información de Salud Protegida (PHI).

En virtud de la HIPAA, una entidad cubierta es un proveedor de atención médica, un plan de salud o un centro de compensación de atención médica. Una asociada comercial es una entidad que brinda servicios a una entidad cubierta que implica el acceso a la PHI. Las Reglas de Privacidad y Seguridad de la HIPAA requieren que una entidad cubierta obtenga garantías por escrito de un socio comercial en forma de un Contrato de Socio Comercial (BAA, por sus siglas en inglés) que requiera que el asociado comercial salvaguarde la privacidad y seguridad de la PHI de la entidad cubierta.

### Proporcionar PHI a Adobe {#providing-phi-to-adobe}

Adobe actúa como socio comercial por sus servicios preparados para HIPAA, enumerados en [Preparación para HIPAA de los servicios en AEM as a Cloud Service](#hipaa-readiness-of-services-in-aem-as-a-cloud-service).

Los clientes que otorguen licencia a cualquier servicio compatible con HIPAA de Adobe para procesar la PHI **deben** tener la licencia correcta y una BAA firmada con Adobe.

>[!IMPORTANT]
>
>Los clientes no pueden crear, recibir, mantener o transmitir la PHI a través de productos y servicios de Adobe que no estén designados como Servicios preparados para HIPAA o sin la licencia adecuada para utilizar un Servicio compatible con HIPAA.

### Responsabilidades compartidas de HIPAA {#hipaa-shared-responsibilities}

Los servicios preparados para la HIPAA de Adobe se basan en un modelo de seguridad de responsabilidad compartida, que requiere que el cliente y Adobe asuman responsabilidades distintas para mantener la seguridad de la PHI. En este modelo de seguridad compartida, Adobe depende del cliente para utilizar y configurar los servicios compatibles con HIPAA y con HIPAA.

Para obtener más información sobre la ejecución de un BAA de Adobe para servicios preparados para HIPAA, póngase en contacto con su representante de ventas o administrador de éxito de clientes de Adobe.

>[!IMPORTANT]
>
>**Descargo de responsabilidad**:
>
>El cliente es responsable de su uso de los servicios preparados para HIPAA de Adobe y de garantizar que los servicios preparados para HIPAA de Adobe cumplan con sus requisitos de conformidad.

Para obtener más información, consulte [HIPAA y productos y servicios de Adobe](https://www.adobe.com/trust/compliance/hipaa-hds/hipaa-ready.html) en el Centro de confianza de Adobe.

## Terminología de HIPAA {#hipaa-terminology}

En la tabla siguiente se describe cómo se clasifican los servicios de AEM para el uso de HIPAA.

| Preparación para HIPAA | Descripción |
| --- | --- |
| Preparado para HIPAA | Diseñado para procesar la PHI cuando está configurado apropiadamente y se usa con una BAA. |
| No compatible con HIPAA | No está diseñado para procesar la PHI y no debe usarse en casos de uso relacionados con HIPAA. |

>[!NOTE]
>
>Las clasificaciones de preparación para la HIPAA se basan en la funcionalidad deseada de cada servicio y pueden cambiar con el tiempo.
>
>Los clientes deben consultar la documentación más actual y las condiciones contractuales aplicables al planificar las implementaciones relacionadas con HIPAA.

## Preparación de los servicios de HIPAA en AEM as a Cloud Service {#hipaa-readiness-of-services-in-aem-as-a-cloud-service}

La siguiente tabla describe qué servicios de AEM están preparados para HIPAA y qué servicios se pueden utilizar junto a ellos. Los servicios preparados para HIPAA requieren la compra de Seguridad extendida para atención médica, tal como se describe en [Requisitos adicionales](#additional-requirements).

| Producto/Funcionalidad | Servicio(s) | Preparación para HIPAA |
| --- | --- | --- |
| AEM Sites | AEM Sites, AEM Publish, Edge Delivery Services | Preparado para HIPAA |
| AEM Sites | Editor universal | No preparado para HIPAA<br>[1] Se puede agregar a un programa de seguridad ampliado cuando no se introduce ninguna PHI. |
| AEM Sites Optimizer | Sites Optimizer | No preparado para HIPAA<br>[1] Se puede agregar a un programa de seguridad ampliado cuando no se introduce ninguna PHI. |
| AEM Assets | AEM Assets | Preparado para HIPAA |
| AEM Assets | Content Hub | No preparado para HIPAA<br>[1] Se puede agregar a un programa de seguridad ampliado cuando no se introduce ninguna PHI. |
| AEM Assets | Brand Portal | No compatible con HIPAA |
| AEM Assets | API abierta de Dynamic Media | No preparado para HIPAA<br>[1] Se puede agregar a un programa de seguridad ampliado cuando no se introduce ninguna PHI. |
| AEM Assets | Dynamic Media Scene7 | No compatible con HIPAA |
| AEM Forms | AEM Forms, Servicio de fachada de autenticación, Servicio de utilidad de PDF | Preparado para HIPAA |
| AEM CIF | Commerce Integration Framework | No compatible con HIPAA |
| AEM Cloud Manager | AEM Cloud Manager, Release Orchestrator, Conmutadores de versiones, Validador de versiones | Preparado para HIPAA |
| AEM Cloud Manager | Distribución de software | No preparado para HIPAA<br>[1] Se puede agregar a un programa de seguridad ampliado cuando no se introduce ninguna PHI. |
|   |   |   |
| AEM Guides  | AEM Guides  | No compatible con HIPAA |
|   |   |   |
| LLM Optimizer | LLM Optimizer | No preparado para HIPAA<br>[1] Se puede agregar a un programa de seguridad ampliado cuando no se introduce ninguna PHI. |

>[!NOTE]
>
>[1]
>
>Para los servicios no preparados para HIPAA que se indican como pueden agregarse a un programa de seguridad extendida, los clientes deben asegurarse de que la PHI no se enrute a estos servicios ni se almacene en ellos.
>
>La introducción de la PHI en un servicio que no está preparado para HIPAA puede resultar en un incumplimiento.

### Requisitos adicionales {#additional-requirements}

[Los servicios enumerados](#hipaa-readiness-of-services-in-aem-as-a-cloud-service) como preparados para HIPAA requieren la compra de Seguridad ampliada para atención médica.

Cuando se adquiere la seguridad ampliada para atención sanitaria, existe el requisito de que:

* los productos seleccionados para ese programa están preparados para HIPAA (como se indica en la tabla),
* Se ha adquirido seguridad ampliada para atención médica para *cada* producto; esto garantiza suficientes créditos Cloud Manager,
* La seguridad ampliada para atención sanitaria se aplica en el momento de la creación del programa.

Si se cumplen los requisitos, se puede aplicar la seguridad ampliada para atención médica al crear el programa de AEM; consulte [Configuración](#setup) para obtener más información.

>[!NOTE]
>
>Para obtener más información sobre el aprovisionamiento y los precios, póngase en contacto con su representante de ventas.

## Entornos {#environments}

*Preparado para HIPAA* no se aplica a los entornos RDE (Entorno de Desarrollo Rápido), Dev o Stage, ya que la PHI no está permitida en estos entornos.

Esto significa que debe:

* utilizar datos ficticios para fines de desarrollo y prueba
* Procesar solo PHI de entornos de producción

La siguiente tabla muestra dónde se pueden admitir los tipos de entorno como preparados para HIPAA.

| | RDE | Desarrollador | Fase  | Prod |
| --- | --- | --- | --- | --- |
| Tipo de entorno  | No  | No  | No  | Sí  |

## Configuración {#setup}

Al [Crear programas de producción](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md), la ficha [Seguridad proporciona las opciones para activar la protección HIPAA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security).