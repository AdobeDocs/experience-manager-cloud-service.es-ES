---
title: Notas de la versión para Cloud Manager 2024.7.0 en Adobe Experience Manager as a Cloud Service
description: Estas son las notas de la versión para Cloud Manager 2024.7.0 en AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
role: Admin
source-git-commit: 12e19fe771c0b70ec471949944141f4d6858cbfd
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 62%

---


# Notas de la versión para Cloud Manager 2024.7.0 en Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta las notas de la versión 2024.7.0 para Cloud Manager en AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de Cloud Manager 2024.7.0 en AEM as a Cloud Service es el 18 de julio de 2024. La próxima versión está planificada para el 8 de agosto de 2024.

## Novedades {#what-is-new}

* La [canalización de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline) y la [canalización que no es de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline) activan **Cambios en Git** para iniciar la canalización en una confirmación y están disponibles para [repositorios privados.](/help/implementing/cloud-manager/managing-code/private-repositories.md)
   * Esto se implementará gradualmente y se completará a mediados de agosto.
* Al agregar un certificado DV administrado por Adobe [1}, ahora puede agregar un único certificado que cubre varios dominios, en lugar de crear un certificado para cada dominio.](/help/implementing/cloud-manager/managing-ssl-certifications/domain-validated-certificates.md)
* Ahora se pueden agregar a un programa soluciones que no tengan [regiones de publicación adicionales](/help/operations/additional-publish-regions.md) siempre que el programa tenga al menos una solución de Sites o Forms que se aplique a él.
* Las soluciones que no tienen [99,99% de SLA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla) ahora se pueden agregar a un programa siempre y cuando el programa tenga al menos una solución de Sites o Forms que se aplique a él.
* El [Panel de auditoría de experiencias](/help/implementing/cloud-manager/experience-audit-dashboard.md) se ha mejorado de varias maneras.
   * Las auditorías ahora se ejecutan en `.com` extremos a través de CDN, reemplazando el enfoque `.net` anterior.
      * Este cambio simula las experiencias de los usuarios reales de forma más precisa y le ayuda a tomar decisiones más informadas sobre la administración y la optimización de su sitio web.
   * Se han realizado varias mejoras en la IU de auditoría de experiencias, como las siguientes:
      * Se ha añadido una vista de tendencias de rendimiento, prácticas recomendadas, SEO y accesibilidad.
      * El vínculo Informe sin procesar de Lighthouse ahora está visible de forma más intuitiva, directamente en el panel de detalles de instantánea de análisis.
      * Se ha mejorado la sección de recomendaciones de Lighthouse.
   * La métrica PWA se eliminó de acuerdo con la versión 12.0.0 de Lighthouse, que eliminó esta métrica.
* AEM [El tipo de archivo del proyecto de](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es) se ha actualizado a [versión 49.](https://github.com/adobe/aem-project-archetype/tree/aem-project-archetype-49)

## Programa para primeros usuarios {#early-adoption}

Para tener la oportunidad de probar algunas de las próximas funciones, forme parte del programa de adopción anticipada de Adobe.

### Compatibilidad con Edge Delivery Services en Cloud Manager {#edge-delivery-services}

Si tiene licencia para Edge Delivery Services como parte de Adobe Experience Manager Sites, [ahora puede integrar su sitio con Edge Delivery Services directamente en Cloud Manager](/help/implementing/cloud-manager/edge-delivery-services.md) y ponerlo en marcha con una experiencia de autoservicio guiada.

Esto permite tener una experiencia unificada para todas las propiedades de AEM, lo que garantiza la coherencia con todos los flujos de trabajo críticos, incluida la administración de nombres de dominio, la administración de certificados SSL y las asignaciones de CDN.

Si le interesa probar esta nueva función y compartir sus comentarios, envíe un correo electrónico a `aemcs-cmedgedelsvs-program-adopter@adobe.com` desde su dirección de correo electrónico asociada a su Adobe ID. 

### Certificados validados por dominio (DV)

Cloud Manager ahora le permite [generar y administrar certificados SSL validados por dominio (DV) de autoservicio.](/help/implementing/cloud-manager/managing-ssl-certifications/domain-validated-certificates.md) Esto le proporciona la solución más rápida, sencilla y rentable para crear un sitio web seguro para su negocio en línea.

Si le interesa probar esta nueva función y compartir sus comentarios, envíe un correo electrónico a `Grp-aemcs-dv-dert-adopter@adobe.com` desde la dirección de correo electrónico asociada a su Adobe ID.

### Tablero de auditoría de experiencias {#experience-audit-dashboard}

[El tablero de auditoría de experiencias de Cloud Manager](/help/implementing/cloud-manager/experience-audit-dashboard.md) incluye una vista de tendencias de las puntuaciones de rendimiento de la página, junto con perspectivas y recomendaciones para ayudarle a mejorarlas. La auditoría de experiencias se incluye como paso en la canalización de producción de Cloud Manager.

El tablero utiliza Google Lighthouse, una herramienta automatizada de código abierto para mejorar la calidad de sus aplicaciones web. Puede ejecutarlo en cualquier página web, pública o que requiera autenticación. Tiene auditorías de rendimiento, accesibilidad, aplicaciones web progresivas, SEO y más.

¿Está interesado en probar el nuevo tablero? Para empezar, envíe un correo electrónico a `aem-lighthouse-pilot@adobe.com` desde su correo electrónico asociado a su Adobe ID.
