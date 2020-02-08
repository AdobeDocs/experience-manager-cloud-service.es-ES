---
title: Problemas conocidos
description: Notas de la versión específicas de los problemas conocidos con Adobe Experience Manager como servicio de nube
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# Problemas conocidos {#known-issues}

Este artículo enumera los problemas conocidos de Adobe Experience Manager como una oferta de servicio de nube. La lista se revisa y actualiza con cada versión continua de Experience Manager.

[Póngase en contacto con la asistencia](https://helpx.adobe.com/support/experience-manager.html) para obtener más información sobre los problemas conocidos.

<!-- 
## Platform {#platform}

## Sites {#sites}
-->

## Recursos {#assets}

<!-- Jira label: assets-cloud-known-issues -->

Algunos problemas conocidos son:

* **Esquema** de metadatos: La utilidad de clasificación de recursos puede provocar un error de compilación JSP. Una solución consiste en quitar el componente de clasificación de recursos del esquema de metadatos. <!-- CQ-4282865 -->

Algunas limitaciones de la funcionalidad Recursos son:

* Con AEM Assets como servicio de nube, la funcionalidad Recursos conectados funciona cuando AEM 6.5 Sites se implementa en AMS.

### Próximas capacidades de Recursos {#upcoming-assets-capabilities}

Se espera que algunas funciones de Recursos Adobe Experience Manager que dependen de las capacidades básicas, que aún no están disponibles en Experience Manager como arquitectura de implementación de Cloud Service, se habiliten en una etapa posterior:

* La publicación en Brand Portal no está habilitada en este momento. Puede ampliar e implementar la implementación de [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) para casos de uso de distribución de recursos.
* La funcionalidad de etiquetado inteligente mejorada que aprovecha los servicios de AI de Adobe I/O no está disponible por ahora.
* Capacidades no habilitadas en este momento debido a la dependencia de las API de Commerce Integration Framework:
   * Modelos de flujo de trabajo de sesión fotográfica.
   * La ficha Información del producto de la interfaz de usuario de las propiedades del recurso no está rellenada.
* Capacidades no habilitadas en este momento debido a la dependencia de la integración de InDesign Server:
   * Plantillas de recursos y catálogos de recursos.
   * Vista previa de varios archivos de InDesign.

>[!MORELIKETHIS]
>
>* [Principales cambios en AEM](aem-cloud-changes.md)
>* [Funciones obsoletas y eliminadas](deprecated-removed-features.md)
>* [Notas de versión](home.md)

