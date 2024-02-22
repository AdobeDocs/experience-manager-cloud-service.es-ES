---
title: Notas de la versión 2024.2.0 para Cloud Manager en Adobe Experience Manager as a Cloud Service
description: Estas son las notas de la versión para Cloud Manager 2024.2.0 en AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 4a41de9da557be562bb2ff5773c7954f76a9acc7
workflow-type: ht
source-wordcount: '725'
ht-degree: 100%

---


# Notas de la versión 2024.2.0 para Cloud Manager en Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta las notas de la versión 2024.2.0 para Cloud Manager en AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de la versión 2024.2.0 de Cloud Manager en AEM as a Cloud Service es el 15 de febrero de 2024. La próxima versión está planificada para el 16 de marzo de 2024.

## Novedades {#what-is-new}

* Cloud Manager ahora admite la gestión de autoservicio de [variables de canalización](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) a través de la IU de Cloud Manager.
* A partir de ahora, [el servicio de vista previa](/help/implementing/cloud-manager/manage-environments.md#access-preview-sevice) se habilitará en los entornos creados antes de que se implementara la función del servicio de vista previa.
* Los [permisos personalizados de Cloud Manager](/help/implementing/cloud-manager/custom-permissions.md) le permiten crear perfiles de permisos personalizados con permisos configurables para restringir el acceso a programas, canalizaciones y entornos para los usuarios de Cloud Manager.
   * Esta función comenzó a implementarse de manera gradual con la [versión de diciembre de 2023](/help/implementing/cloud-manager/release-notes/2023/2023-12-0.md) y se completará el 20 de febrero de 2024.
* En todos los entornos nuevos, los nombres del [ perfil de producto del entorno](/help/onboarding/aem-cs-team-product-profiles.md) tendrán un formato más fácil de usar basado en una combinación de descripción de perfil, tipo de entorno, número y número de programa.
* [El entorno de compilación](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) se ha actualizado a la versión 3.9.4 de Maven y a las versiones de JDK jdk-11.0.22 y jdk1.8.0_401.

## Programa para primeros usuarios {#early-adoption}

Para tener la oportunidad de probar algunas de las próximas funciones, forme parte del programa de adopción anticipada de Adobe.

### Colección del lado del cliente mediante Monitorización del usuario real (RUM) {#rum}

Puede aprovechar [Servicio de datos de Monitorización del usuario real (RUM)](/help/implementing/cloud-manager/content-requests.md#cliendside-collection) para habilitar la recopilación del lado del cliente para el uso de AEM as a Cloud Service.

El servicio de datos de Monitorización del usuario real (RUM) ofrece un reflejo más preciso de las interacciones del usuario, lo que garantiza una medida fiable de la participación en el sitio web. Es una gran oportunidad para obtener perspectivas avanzadas sobre el rendimiento de su página. Esto resulta beneficioso para los clientes que utilizan CDN administrada por Adobe o CDN no administrada por Adobe. Para los clientes que utilizan una CDN no administrada por Adobe, ahora se pueden habilitar los informes de tráfico automatizados para ellos, lo que elimina la necesidad de compartir cualquier informe de tráfico con Adobe.

Si le interesa probar esta nueva funcionalidad y compartir sus comentarios, envíe un correo electrónico a `aemcs-rum-adopter@adobe.com` desde su dirección de correo electrónico asociada a su Adobe ID. Incluya el nombre de dominio para los entornos de producción, fase y desarrollo en su correo electrónico.  La disponibilidad del programa para primeros usuarios de esta funcionalidad es limitada.

### Traer su propio GitHub {#byo-github}

Si utiliza GitHub para administrar sus repositorios, [ahora puede validar códigos directamente dentro de sus repositorios de GitHub a través de Cloud Manager.](/help/implementing/cloud-manager/managing-code/byo-github.md)Esta integración elimina la necesidad de sincronizar el código de forma coherente con el repositorio de Adobe y le permite comprobar las solicitudes de extracción antes de combinarlas en las ramas principales. Esta funcionalidad es exclusiva de GitHub público. La compatibilidad con GitHub autoalojado no está disponible.

Si le interesa probar esta nueva funcionalidad y compartir sus comentarios, envíe un correo electrónico a `Grp-CloudManager_BYOG@adobe.com` desde su dirección de correo electrónico asociada a su Adobe ID.

### Restauración de contenido de autoservicio {#content-restore}

[Una nueva funcionalidad de restauración de contenido de autoservicio](/help/operations/restore.md) ahora proporciona una restauración de copia de seguridad durante siete días y está disponible para los primeros usuarios para la evaluación:

* Restauración de copias de seguridad puntuales de las 24 horas anteriores
* Restauraciones a hora fija durante un máximo de siete días

Si le interesa probar esta nueva funcionalidad y compartir sus comentarios, envíe un correo electrónico a `aemcs-restorefrombackup-adopter@adobe.com` desde su correo electrónico asociado a su Adobe ID.

* El programa para primeros usuarios se limita únicamente a los entornos de desarrollo.
* La disponibilidad del programa para primeros usuarios de esta funcionalidad es limitada.
* Esta funcionalidad se utiliza para recuperar contenido eliminado accidentalmente y no está pensada para la recuperación ante desastres.

### Tablero de auditoría de experiencias {#experience-audit-dashboard}

[El tablero de auditoría de experiencias de Cloud Manager](/help/implementing/cloud-manager/experience-audit-dashboard.md) incluye una vista de tendencias de las puntuaciones de rendimiento de la página, junto con perspectivas y recomendaciones para ayudarle a mejorarlas. La auditoría de experiencias se incluye como paso en la canalización de producción de Cloud Manager.

El tablero utiliza Google Lighthouse, una herramienta automatizada de código abierto para mejorar la calidad de sus aplicaciones web. Puede ejecutarlo en cualquier página web, pública o que requiera autenticación. Tiene auditorías de rendimiento, accesibilidad, aplicaciones web progresivas, SEO y más.

¿Está interesado en probar el nuevo tablero? Para empezar, envíe un correo electrónico a `aem-lighthouse-pilot@adobe.com` desde su correo electrónico asociado a su Adobe ID.

## Correcciones de errores {#bug-fixes}

* El JDK de los contenedores de la versión se ha actualizado a una versión que soluciona [JDK-8313765.](https://bugs.openjdk.org/browse/JDK-8313765)
