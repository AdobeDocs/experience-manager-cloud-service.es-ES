---
title: Notas de la versión 2023.10.0 para Cloud Manager en Adobe Experience Manager as a Cloud Service
description: Estas son las notas de la versión 2023.10.0 para Cloud Manager en AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 661eac787439e6e696574a6973afa7e39eeb443e
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 18%

---


# Notas de la versión 2023.10.0 para Cloud Manager en Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta las notas de la versión 2023.10.0 para Cloud Manager en AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de Cloud Manager 2023.10.0 en AEM as a Cloud Service es el 5 de octubre de 2023. El próximo lanzamiento está planificado para el 2 de noviembre de 2023.

## Novedades {#what-is-new}

* [Ahora puede cancelar de forma segura una canalización](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#cancel) en los pasos validar y crear imagen.
* Mejoras en [indexación](/help/operations/indexing.md) han reducido la duración de la canalización al implementar nuevos índices.
   * Las mejoras varían según el perfil de contenido.
* Automático [actualizaciones para entornos de desarrollo](/help/implementing/cloud-manager/manage-environments.md#updating-environments) están habilitadas de forma predeterminada para los programas nuevos, lo que le ahorra el tiempo necesario para ejecutar las actualizaciones manualmente.
   * Esta actualización se implementará por fases.
* Con la versión de octubre de 2023 de Cloud Manager, las versiones de Java y Maven se actualizan mediante una implementación gradual.
   * Apache Maven se está actualizando a la versión 3.8.8.
   * Las versiones de Java se actualizan al Oracle JDK 8u371 y al Oracle JDK 11.0.20.
   * De forma predeterminada, la variable `JAVA_HOME` la variable de entorno se está actualizando a `/usr/lib/jvm/jdk1.8.0_371` que contiene el Oracle JDK 8u371.
   * Ver el documento [Entorno de compilación](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) para obtener más información.
   * [Consulte el aviso de OpenJDK](https://openjdk.org/groups/vulnerability/advisories/) para obtener más información sobre la seguridad y las correcciones de errores en estas actualizaciones de JDK.

## Programa de adopción temprana {#early-adoption}

Forme parte de nuestro programa de adopción anticipada y tenga la oportunidad de probar algunas de las próximas funciones.

### Permisos personalizados {#custom-permissions}

[Permisos personalizados de Cloud Manager](/help/implementing/cloud-manager/custom-permissions.md) le permite crear nuevos perfiles de permisos personalizados con permisos configurables para restringir el acceso a programas, canalizaciones y entornos para los usuarios de Cloud Manager.

si está interesado en probar esta nueva función y compartir sus comentarios, envíe un mensaje de correo electrónico a `Grp-CloudManager-custom-permissions@adobe.com` de su dirección de correo electrónico asociada a su Adobe ID.

### Restauración de contenido de autoservicio {#content-restore}

[Una nueva función de restauración de contenido de autoservicio](/help/operations/restore.md) ahora proporciona una restauración de copia de seguridad durante un máximo de siete días y está disponible para los usuarios que la adoptaron por primera vez con fines de evaluación, que incluye:

* Restauración de la copia de seguridad puntual de las 24 horas anteriores
* Restauraciones a tiempo fijo de hasta siete días

Si está interesado en probar esta nueva función y compartir sus comentarios, envíe un correo electrónico a `aemcs-restorefrombackup-adopter@adobe.com` de su correo electrónico asociado a su Adobe ID. Importante:

* El programa de los primeros en adoptarlo se limita únicamente a los entornos de desarrollo.
* La disponibilidad del programa de adopción anticipada de esta función es limitada.
* Esta función se utiliza para recuperar contenido eliminado accidentalmente y no está pensada para la recuperación ante desastres.

### Tablero de auditoría de experiencias {#experience-audit-dashboard}

[El panel de auditoría de experiencias de Cloud Manager](/help/implementing/cloud-manager/experience-audit-dashboard.md) incluye una vista de tendencias de las puntuaciones de rendimiento de la página, junto con perspectivas y recomendaciones para ayudarle a mejorarlas. La auditoría de experiencias se incluye como paso en la canalización de producción de Cloud Manager.

El tablero aprovecha Google Lighthouse, una herramienta automatizada de código abierto para mejorar la calidad de sus aplicaciones web. Puede ejecutarlo en cualquier página web, pública o que requiera autenticación. Tiene auditorías de rendimiento, accesibilidad, aplicaciones web progresivas, SEO y más.

¿Interesado en probar a conducir el nuevo tablero? Envíe un correo electrónico a `aem-lighthouse-pilot@adobe.com` a partir de su correo electrónico asociado con su Adobe ID y podemos ayudarle a empezar.
