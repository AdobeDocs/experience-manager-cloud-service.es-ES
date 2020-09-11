---
title: Cambios importantes en AEM Commerce as a Cloud Service
description: Cambios importantes en AEM Commerce as a Cloud Service en comparación con Adobe Experience Manager 6.5.
translation-type: tm+mt
source-git-commit: ed81d08d9775f61c0ab1e305710ac7ecf29d4229
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 94%

---


# Cambios importantes en AEM Commerce as a Cloud Service {#notable-changes}

Adobe Experience Manager as a Cloud Service ofrece muchas nuevas funciones y posibilidades para gestionar sus Proyectos AEM. Este documento destaca las importantes diferencias entre las capacidades del Commerce Integration Framework (CIF) para el servicio on-premise, el servicio administrado por Adobe y Experience Manager as a Cloud Service. Para ver otros cambios, consulte los [cambios genéricos a Experience Manager as a Cloud Service](/help/release-notes/aem-cloud-changes.md).

Las principales diferencias con respecto al Experience Manager 6.5 se encuentran en los siguientes ámbitos:
* [Compatibilidad con CIF clásico](#cif-classic)
* [Implementación de las herramientas de creación del CIF](#cif-tools)
* [Cambio del servicio administrado por Adobe on-premise](#moving-cif-cs)

## Compatibilidad con CIF clásico/Quickstart en Experience Manager as a Cloud Service {#cif-classic}

Commerce Integration Framework clásico, que incluía un importador de productos para importar y almacenar catálogos de productos en Experience Manager, ya no está disponible en Experience Manager as a Cloud Service. Experience Manager as a Cloud Service no admite el uso del CIF clásico y los proyectos que utilicen CIF clásico tendrán que reemplazar la implementación del CIF clásico con la versión admitida, como se describe en el [CIF en Experience Manager as a Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/commerce/architecture/magento.html#overview)

## Implementación del CIF {#deployment}

A continuación se muestran los diferentes modelos de implementación del Commerce Integration Framework para las distintas ofertas de AEM:

|  | AEM on-premise | Managed Services de AEM | AEM Cloud Service |
|-------------     |-----------|-----------|-----------|
| Cómo implementar las herramientas de creación del CIF para el back-end Magento | [Consulte el conector del CIF](https://github.com/adobe/commerce-cif-connector/blob/master/README.md) compatible con AEM 6.5 | [Consulte el conector del CIF](https://github.com/adobe/commerce-cif-connector/blob/master/README.md) compatible con AEM 6.5 | AEM as a Cloud Service debe aprovisionarse con el complemento CIF. Póngase en contacto con su representante de ventas para obtener más información. |
| Cómo implementar el [proyecto Venia con el CIF](https://github.com/adobe/aem-cif-guides-venia) | Instalación del paquete en AEM | Implementación realizada mediante [Cloud Manager](https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) | El proyecto se ha trasladado al [repositorio de Git de Cloud Manager](https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html) y la implementación se ha realizado mediante [Cloud Manager](https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-service/implementing/deploying/overview.html). |

>[!NOTE]
>
>Para obtener documentación adicional sobre cómo utilizar CIF con AEM servicio administrado o AEM in situ, consulte [Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)

>[!Note]
>
>La versión de CIF clásico/Quickstart de Commerce Integration Framework puede utilizarse como oferta en AEM on-premise para casos de uso muy limitados. Sin embargo, esta no es la solución recomendada.

## Traslado a AEM Commerce as a Cloud Service desde on-premise y Managed Services {#moving-cif-cs}

Los clientes que pasan de una instalación on-premise o de Managed Services de AEM a AEM as a Cloud Service deben realizar algunos ajustes menores en el proyecto AEM.

El primer ajuste, como se ha descrito anteriormente, es necesario para el conector del CIF. El conector del CIF se sustituye por el complemento CIF que se implementa mediante Adobe. Por lo tanto, no instale el conector del CIF en AEM as a Cloud Service. Además, no se admite el uso con el SDK local de AEM Cloud, Adobe también proporciona el complemento CIF para el [desarrollo local](develop.md).

En segundo lugar, comprenda la [estructura del proyecto AEM](https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) y las características de AEM as a Cloud Service. Adapte la configuración del proyecto al diseño de AEM as a Cloud Service.
Las principales diferencias son las siguientes:

* El paquete OSGI del cliente de GraphQL ya **no debe** incluirse en el proyecto AEM; se implementa mediante el complemento CIF
* Las configuraciones OSGI para el cliente de GraphQL y el servicio de datos Graphql ya **no deben** incluirse en el proyecto AEM.

>[!TIP]
>
>Consulte el proyecto de la [Tienda de referencia de Venia de AEM](https://github.com/adobe/aem-cif-guides-venia) en GitHub. Este proyecto proporciona perfiles Maven para AEM as a Cloud Service e instalaciones on-premise que tienen en cuenta las diferentes condiciones del marco de trabajo.
