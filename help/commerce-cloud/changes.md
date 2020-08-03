---
title: Cambios notables en AEM comercio como Cloud Service
description: Cambios notables en AEM comercio como Cloud Service en comparación con el Adobe Experience Manager 6.5.
translation-type: tm+mt
source-git-commit: df6f679b70a7cc70e4f76612c0a72a31443cd1b8
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 6%

---


# Notable changes to AEM Commerce as a Cloud Service {#notable-changes}

Adobe Experience Manager como Cloud Service trae muchas nuevas características y posibilidades para administrar sus proyectos AEM. Este documento destaca las importantes diferencias entre las capacidades de Commerce Integration Framework (CIF) para el servicio local, el servicio administrado por Adobe y el Experience Manager como Cloud Service. Para ver otros cambios, consulte los [cambios genéricos a Experience Manager como Cloud Service](/help/release-notes/aem-cloud-changes.md).

Las principales diferencias con respecto al Experience Manager 6.5 se encuentran en los siguientes ámbitos:
* [Compatibilidad con CIF Classic](#cif-classic)
* [Implementación de las herramientas de creación de CIF](#cif-tools)
* [Cambio del servicio administrado in situ y Adobe](#moving-cif-cs)

## Compatibilidad con CIF Classic/Quickstart en Experience Manager como Cloud Service {#cif-classic}

El marco de integración de comercio clásico, que incluía un importador de productos para importar y almacenar catálogos de productos en Experience Manager, ya no está disponible en Experience Manager como Cloud Service. El Experience Manager no admite el uso de CIF clásico como Cloud Service y los proyectos que utilicen CIF clásico tendrán que reemplazar la implementación de CIF clásico con la versión admitida, como se describe en [CIF on Experience Manager como Cloud Service](https://git.corp.adobe.com/AdobeDocs/experience-manager-cloud-service.en/blob/cif/help/commerce-cloud/architecture.md)

## Implementación del CIF {#deployment}

A continuación se muestran los diferentes modelos de implementación de Commerce Integration Framework para las distintas ofertas de AEM:

|  | AEM in situ | AEM Managed Services | Cloud Service AEM |
|-------------     |-----------|-----------|-----------|
| Cómo implementar las herramientas de creación de CIF para el servidor Magento | [Consulte Conector](https://github.com/adobe/commerce-cif-connector/blob/master/README.md) CIF compatible con AEM 6.5 | [Consulte Conector](https://github.com/adobe/commerce-cif-connector/blob/master/README.md) CIF compatible con AEM 6.5 | AEM como Cloud Service debe aprovisionarse con un complemento CIF. Póngase en contacto con su representante de ventas para obtener más información |
| Cómo implementar el proyecto [CIF Venia](https://github.com/adobe/aem-cif-guides-venia) | AEM instalación del paquete | Implementación realizada mediante [Cloud Manager](https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) | El proyecto se ha trasladado al repositorio [Git de](https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html) Cloud Manager y la implementación se ha realizado mediante [Cloud Manager](https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-service/implementing/deploying/overview.html) |

>[!Note]
>
>La versión CIF Classic/Quickstart de Commerce Integration Framework puede utilizarse en AEM oferta in situ para casos de uso muy limitados. Sin embargo, esta no es la solución recomendada.

## Pasar a AEM comercio como Cloud Service desde On-premise y Managed Services {#moving-cif-cs}

Los clientes que pasan de una instalación in situ o de Managed Services AEM a AEM como Cloud Service deben realizar algunos ajustes menores en el proyecto AEM.

El primer ajuste, como se ha descrito anteriormente, es necesario para el conector CIF. El conector CIF se sustituye por el complemento CIF que se implementa mediante Adobe. Por lo tanto, no instale el conector CIF en AEM como Cloud Service. Además, no se admite el uso con el SDK local de AEM Cloud, Adobe también proporciona el complemento CIF para el desarrollo [](develop.md)local.

En segundo lugar, comprenda la [AEM estructura](https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) del proyecto y las características de AEM como Cloud Service. Adapte la configuración del proyecto a la AEM como diseño de Cloud Service.
Las principales diferencias son:

* El paquete OSGI del cliente GraphQL ya no **debe** incluirse en el proyecto de AEM; se implementa mediante el complemento CIF
* Las configuraciones OSGI para el cliente GraphQL y el servicio de datos Graphql ya no **deben** incluirse en el proyecto AEM

>[!TConsejo]
>
>Consulte el [AEM proyecto de la Tienda](https://github.com/adobe/aem-cif-guides-venia) de referencia Venia en GitHub. Este proyecto proporciona perfiles Maven para AEM como Cloud Service e instalaciones locales que tienen en cuenta las diferentes condiciones del marco.
