---
title: Notas de la versión para Cloud Manager 2024.9.0 en Adobe Experience Manager as a Cloud Service
description: Obtenga información sobre las notas de la versión para Cloud Manager 2024.9.0 en AEM as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 610ae004b6da2f7fc0dae2baa613cb363fe9fb00
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 83%

---

# Notas de la versión para Cloud Manager 2024.9.0 en Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta las notas de la versión 2024.9.0 para Cloud Manager en AEM as a Cloud Service.

>[!NOTE]
>
>Consulte las [notas de la versión actuales de Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de Cloud Manager 2024.9.0 en AEM as a Cloud Service es el 5 de septiembre de 2024. La próxima versión está planificada para el 3 de octubre de 2024.

## Novedades {#what-is-new}

* **Tablero de auditoría de experiencias:**

  El [tablero mejorado de auditoría de experiencias](/help/implementing/cloud-manager/experience-audit-dashboard.md) de Adobe Cloud Manager, con tecnología Google Lighthouse, proporciona información sobre la calidad y el rendimiento de AEM Sites mediante la evaluación de los elementos vitales de la web, la optimización de los motores de búsqueda y las métricas de accesibilidad. Ayuda a los usuarios a identificar áreas de mejora al ofrecer recomendaciones procesables, lo que permite a los equipos mejorar la experiencia del usuario, los tiempos de carga de las páginas y el cumplimiento del sitio. Este tablero simplifica la monitorización de las métricas esenciales del sitio y garantiza que las aplicaciones de AEM cumplan con los estándares de alto rendimiento y accesibilidad.

* **Certificados de validación de dominio administrados y generados por Adobe:**

  Cloud Manager ahora le permite [generar y administrar certificados SSL DV (validados por dominio) de autoservicio de Adobe](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md). Esto le proporciona la solución más rápida, sencilla y rentable para crear un sitio web seguro para su organización o empresa en línea. <!-- CMGR-52403 -->

  >[!NOTE]
  >
  >Los clientes de [Content Hub](/help/assets/product-overview.md) tienen planeado recibir esta función por fases como parte de un despliegue gradual.

* **Compatibilidad con Edge Delivery Services en Cloud Manager:**

  Si tienes una licencia de Edge Delivery Services como parte de AEM Sites, [ahora puedes incorporar tu sitio con Edge Delivery Services directamente a través de Cloud Manager](/help/implementing/cloud-manager/edge-delivery-services.md). Esta función permite una experiencia de autoservicio guiada en el lanzamiento. AEM También unifica los flujos de trabajo esenciales, como la administración de nombres de dominio, los certificados SSL y las asignaciones de CDN en todas las propiedades de AEM, lo que garantiza la coherencia y la eficacia. <!-- CMGR-49859 -->

  >[!NOTE]
  >
  >Los clientes de [Content Hub](/help/assets/product-overview.md) tienen planeado recibir esta función por fases como parte de un despliegue gradual.

* Los clientes que utilizan repositorios de GitHub ahora tienen la capacidad de crear y utilizar canalizaciones de configuración de nivel web. <!--( KEEP IN? SP: YES CMGR-59046 and Slack https://cq-dev.slack.com/archives/C07LFP5BZ2L/p1725407057847379 ) -->

<!--
## Early adoption program {#early-adoption}

For a chance to test some upcoming features, be a part of Adobe's early adoption program. -->


## Corrección de errores

* La paginación de la vista de tabla de certificados SSL ahora funciona según lo esperado. <!-- (CMGR-60804 - [UI] Pagination doesn't work for ssl certificates) -->
* Se promocionó una versión incorrecta del artefacto al usar el botón **Promocionar versión** desde una ejecución. <!-- ( KEEP IN? SP: YES CMGR-59519 and Slack https://cq-dev.slack.com/archives/C07LFPN2R08/p1725408253474129 ) -->

<!-- * Slack message says next release? SP: REMOVE (Leave in for now) SSL Certificates table in Cloud Manager now enables pagination in the user experience. ( https://jira.corp.adobe.com/browse/CMGR-61041 and Slack https://cq-dev.slack.com/archives/C07LFRE9QJU/p1725408553760009 ) --<>
