---
title: Notas de la versión para Cloud Manager 2024.6.0 en Adobe Experience Manager as a Cloud Service
description: Estas son las notas de la versión para Cloud Manager 2024.6.0 en AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
role: Admin
source-git-commit: 8eaf2b70734cec1fedace64d74059ee161785b39
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 100%

---


# Notas de la versión para Cloud Manager 2024.6.0 en Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta las notas de la versión 2024.6.0 para Cloud Manager en AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de Cloud Manager versión 2024.6.0 en AEM as a Cloud Service fue el 6 de junio de 2024. La próxima versión está planificada para el 11 de julio de 2024.

## Novedades {#what-is-new}

* Ahora puede [usar sus propios repositorios de GitHub](/help/implementing/cloud-manager/managing-code/private-repositories.md) como fuentes para canalizaciones de pila completa y de front-end.
   * Además, puede aprovechar los repositorios de GitHub con [submódulos de Git](/help/implementing/cloud-manager/managing-code/git-submodules.md), lo que le proporciona un control mejorado sobre las canalizaciones generadas automáticamente que se utilizan para validar las solicitudes de extracción y le permite definir los comportamientos para las métricas cruciales durante la fase de análisis de código.
   * [También tiene la opción](/help/implementing/cloud-manager/managing-code/github-check-config.md) de conservar el historial de informes en GitHub, asignar un nombre a la canalización y definir variables de canalización que se adapten a sus necesidades.
* La [Restauración del contenido de autoservicio](/help/operations/restore.md) proporciona restauración de copia de seguridad durante un máximo de siete días y ofrece las siguientes funciones:
   * Restauración de copias de seguridad puntuales de las 24 horas anteriores
   * Restauraciones a hora fija durante un máximo de siete días
* Se han añadido [nuevas reglas de OakPal](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-ui-content-package) al análisis de calidad del código de Cloud Manager.
   * Cada nueva regla añadida a partir de junio de 2024 es un cambio permanente.
   * Se le insta a abordar estos cambios lo antes posible, ya que las nuevas reglas harán que las canalizaciones fallen a partir de la versión de agosto de 2024 de Cloud Manager.

## Programa para primeros usuarios {#early-adoption}

Para tener la oportunidad de probar algunas de las próximas funciones, forme parte del programa de adopción anticipada de Adobe.

### Compatibilidad con Edge Delivery Services en Cloud Manager {#edge-delivery-services}

Si tiene licencia para Edge Delivery Services como parte de Adobe Experience Manager Sites, [ahora puede integrar su sitio con Edge Delivery Services directamente en Cloud Manager](/help/implementing/cloud-manager/edge-delivery-services.md) y ponerlo en marcha con una experiencia de autoservicio guiada.

Esto permite tener una experiencia unificada para todas las propiedades de AEM, lo que garantiza la coherencia con todos los flujos de trabajo críticos, incluida la administración de nombres de dominio, la administración de certificados SSL y las asignaciones de CDN.

Si le interesa probar esta nueva función y compartir sus comentarios, envíe un correo electrónico a `aemcs-cmedgedelsvs-program-adopter@adobe.com` desde su dirección de correo electrónico asociada a su Adobe ID. 

### Certificados validados por dominio (DV)

Cloud Manager ahora le permite [generar y administrar certificados SSL validados por dominio (DV) de autoservicio.](/help/implementing/cloud-manager/managing-ssl-certifications/domain-validated-certificates.md) Esto le proporciona la solución más rápida, sencilla y rentable para crear un sitio web seguro para su negocio en línea.

Si le interesa probar esta nueva función y compartir sus comentarios, envíe un correo electrónico a `Grp-aemcs-dv-dert-adopter@adobe.com` desde la dirección de correo electrónico asociada a su Adobe ID.

<!-- RICK: REMOVED THIS SECTION AS PER EMAIL REQUEST TO DL-AEM-DOCS FROM SHWETA DUA, WEDNESDAY, JUNE 12, 2024 ### Client-Side Collection via Real Use Monitoring (RUM) {#rum}

You can leverage the [Real Use Monitoring (RUM) Data Service](/help/implementing/cloud-manager/content-requests.md#cliendside-collection) to enable client-side collection for AEM as a Cloud Service.

Real Use Monitoring (RUM) Data Service offers a more precise reflection of user interactions, ensuring a reliable measure of website engagement. It is a great opportunity to gain advanced insights into your page performance. This is beneficial for customers who use either Adobe-managed CDN or non-Adobe managed CDN. For customers using a non-Adobe managed CDN, automated traffic reporting can now be enabled for them, thus removing the need to share any traffic report with Adobe.

If you are interested in testing this new feature and sharing your feedback, please send an email to `aemcs-rum-adopter@adobe.com` from the email address associated with your Adobe ID. Please include the domain name for production, stage, and dev environments in your email.  Availability of the early adopter program of this feature is limited.-->

### Tablero de auditoría de experiencias {#experience-audit-dashboard}

[El tablero de auditoría de experiencias de Cloud Manager](/help/implementing/cloud-manager/experience-audit-dashboard.md) incluye una vista de tendencias de las puntuaciones de rendimiento de la página, junto con perspectivas y recomendaciones para ayudarle a mejorarlas. La auditoría de experiencias se incluye como paso en la canalización de producción de Cloud Manager.

El tablero utiliza Google Lighthouse, una herramienta automatizada de código abierto para mejorar la calidad de sus aplicaciones web. Puede ejecutarlo en cualquier página web, pública o que requiera autenticación. Tiene auditorías de rendimiento, accesibilidad, aplicaciones web progresivas, SEO y más.

¿Está interesado en probar el nuevo tablero? Para empezar, envíe un correo electrónico a `aem-lighthouse-pilot@adobe.com` desde su correo electrónico asociado a su Adobe ID.
