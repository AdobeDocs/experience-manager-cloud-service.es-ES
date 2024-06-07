---
title: Notas de la versión para Cloud Manager 2024.6.0 en Adobe Experience Manager as a Cloud Service
description: Estas son las notas de la versión para Cloud Manager 2024.6.0 en AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
role: Admin
source-git-commit: 5644e6f433b18408780e13057ba469e7c4926f78
workflow-type: ht
source-wordcount: '702'
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

* Ahora puede [utilizar sus propios repositorios de GitHub](/help/implementing/cloud-manager/managing-code/private-repositories.md) como fuentes para canalizaciones de pila completa y de front-end.
   * Además, puede aprovechar los repositorios de GitHub con [submódulos git,](/help/implementing/cloud-manager/managing-code/git-submodules.md) que le proporcionan un mayor control sobre las canalizaciones generadas automáticamente que se utilizan para la validación de las solicitudes de extracción y le permiten definir comportamientos para métricas cruciales durante la fase de análisis del código.
   * [También tiene la opción](/help/implementing/cloud-manager/managing-code/github-check-config.md) de conservar el historial de informes en GitHub, asignar un nombre a la canalización y definir variables de canalización que se adapten a sus necesidades.
* La [Restauración del contenido de autoservicio](/help/operations/restore.md) proporciona restauración de copia de seguridad durante un máximo de siete días y ofrece las siguientes funciones:
   * Restauración de copias de seguridad puntuales de las 24 horas anteriores
   * Restauraciones a hora fija durante un máximo de siete días
* Se han añadido [nuevas reglas de OakPal](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-ui-content-package) al análisis de calidad del código de Cloud Manager.
   * Cada nueva regla añadida a partir de junio de 2024 es un cambio permanente.
   * Le instamos a que solucione estos problemas lo antes posible, ya que estas nuevas reglas provocarán fallos en las canalizaciones a partir de la versión de agosto de 2024 de Cloud Manager.

## Programa para primeros usuarios {#early-adoption}

Para tener la oportunidad de probar algunas de las próximas funciones, forme parte del programa de adopción anticipada de Adobe.

### Compatibilidad con Edge Delivery Services en Cloud Manager {#edge-delivery-services}

Si tiene licencia para Edge Delivery Services como parte de Adobe Experience Manager Sites, [ahora puede integrar su sitio con Edge Delivery Services directamente en Cloud Manager](/help/implementing/cloud-manager/edge-delivery-services.md) y ponerlo en marcha con una experiencia de autoservicio guiada.

Esto permite tener una experiencia unificada para todas las propiedades de AEM, lo que garantiza la coherencia con todos los flujos de trabajo críticos, incluida la administración de nombres de dominio, la administración de certificados SSL y las asignaciones de CDN.

Si le interesa probar esta nueva función y compartir sus comentarios, envíe un correo electrónico a `aemcs-cmedgedelsvs-program-adopter@adobe.com` desde su dirección de correo electrónico asociada a su Adobe ID. 

### Certificados validados por dominio (DV)

Cloud Manager ahora le permite [generar y administrar certificados SSL validados por dominio (DV) de autoservicio.](/help/implementing/cloud-manager/managing-ssl-certifications/domain-validated-certificates.md) Esto le proporciona la solución más rápida, sencilla y rentable para crear un sitio web seguro para su negocio en línea.

Si le interesa probar esta nueva función y compartir sus comentarios, envíe un correo electrónico a `Grp-aemcs-dv-dert-adopter@adobe.com` desde la dirección de correo electrónico asociada a su Adobe ID.

### Colección del lado del cliente mediante Monitorización del usuario real (RUM) {#rum}

Puede aprovechar [Servicio de datos de Monitorización del usuario real (RUM)](/help/implementing/cloud-manager/content-requests.md#cliendside-collection) para habilitar la recopilación del lado del cliente para el uso de AEM as a Cloud Service.

El servicio de datos de Monitorización del usuario real (RUM) ofrece un reflejo más preciso de las interacciones del usuario, lo que garantiza una medida fiable de la participación en el sitio web. Es una gran oportunidad para obtener perspectivas avanzadas sobre el rendimiento de su página. Esto resulta beneficioso para los clientes que utilizan CDN administrada por Adobe o CDN no administrada por Adobe. Para los clientes que utilizan una CDN no administrada por Adobe, ahora se pueden habilitar los informes de tráfico automatizados para ellos, lo que elimina la necesidad de compartir cualquier informe de tráfico con Adobe.

Si le interesa probar esta nueva funcionalidad y compartir sus comentarios, envíe un correo electrónico a `aemcs-rum-adopter@adobe.com` desde su dirección de correo electrónico asociada a su Adobe ID. Incluya el nombre de dominio para los entornos de producción, fase y desarrollo en su correo electrónico.  La disponibilidad del programa para primeros usuarios de esta funcionalidad es limitada.

### Tablero de auditoría de experiencias {#experience-audit-dashboard}

[El tablero de auditoría de experiencias de Cloud Manager](/help/implementing/cloud-manager/experience-audit-dashboard.md) incluye una vista de tendencias de las puntuaciones de rendimiento de la página, junto con perspectivas y recomendaciones para ayudarle a mejorarlas. La auditoría de experiencias se incluye como paso en la canalización de producción de Cloud Manager.

El tablero utiliza Google Lighthouse, una herramienta automatizada de código abierto para mejorar la calidad de sus aplicaciones web. Puede ejecutarlo en cualquier página web, pública o que requiera autenticación. Tiene auditorías de rendimiento, accesibilidad, aplicaciones web progresivas, SEO y más.

¿Está interesado en probar el nuevo tablero? Para empezar, envíe un correo electrónico a `aem-lighthouse-pilot@adobe.com` desde su correo electrónico asociado a su Adobe ID.
