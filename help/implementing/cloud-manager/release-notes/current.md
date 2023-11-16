---
title: Notas de la versión 2023.11.0 para Cloud Manager en Adobe Experience Manager as a Cloud Service
description: Estas son las notas de la versión 2023.11.0 para Cloud Manager en AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 4e2ea040ec14515525424b42f524601d34786cb8
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 13%

---


# Notas de la versión 2023.11.0 para Cloud Manager en Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta las notas de la versión 2023.11.0 para Cloud Manager en AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de Cloud Manager 2023.11.0 en AEM as a Cloud Service es el 14 de noviembre de 2023. La próxima versión está planificada para el 7 de diciembre de 2023.

## Novedades {#what-is-new}

* AEM La protección del cortafuegos de aplicaciones web-DDOS (WAF-DDOS) ya está disponible para su compra como parte de sus derechos as a Cloud Service y [se puede configurar en modo de autoservicio.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
* Especializado [canalizaciones de configuración](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) ahora están disponibles para configurar e implementar reglas de filtro de tráfico, incluidas las reglas WAF, en cuestión de minutos.
* [Al copiar contenido](/help/implementing/developing/tools/content-copy.md) desde un entorno superior a un entorno de desarrollo, ahora se muestra un mensaje que aconseja precaución al copiar grandes conjuntos de contenido, ya que los entornos de desarrollo tienen una capacidad limitada.
* [La página de detalles de ejecución de la canalización](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details) ahora mostrará todos los pasos de una ejecución de canalización con los que aún no se han iniciado atenuados.
* En ambos **[Actividad](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#activity)** y **[Canalizaciones](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#pipelines)** En algunas páginas, ahora está disponible un resumen de la ejecución de la canalización al hacer clic en una canalización con un estado en ejecución.
* Un nuevo **Duración** se ha añadido a la sección [página de detalles de canalización](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details) que incluye la duración promedio del paso de canalización en función de la tendencia histórica para ese programa.
* En el [página ejecución de canalización,](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#activity-window) los pasos finalizados ahora muestran la duración.
* Ejecuciones que [reutilizar artefactos de generación](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) ahora mostrará el vínculo a la ejecución que creó inicialmente esos artefactos.
* La opción para seleccionar **Errores importantes en las métricas** ahora se puede configurar para [canalizaciones de calidad de código](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) y también.


## Programa de adopción temprana {#early-adoption}

Forme parte de nuestro programa de adopción anticipada y tenga la oportunidad de probar algunas de las próximas funciones.

### Traer su propio GitHub {#byo-github}

Si usa GitHub para administrar sus repositorios, [Ahora puede validar código directamente dentro de sus repositorios de GitHub a través de Cloud Manager.](/help/implementing/cloud-manager/managing-code/byo-github.md) Esta integración elimina la necesidad de sincronizar el código de forma coherente con el repositorio de Adobe y le permite comprobar las solicitudes de extracción antes de combinarlas en las ramas principales.

Si está interesado en probar esta nueva función y compartir sus comentarios, envíe un correo electrónico a `Grp-CloudManager_BYOG@adobe.com` de su dirección de correo electrónico asociada a su Adobe ID.

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

## Problemas conocidos {#known-issues}

Hay un error conocido que evita [canalizaciones de configuración](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md##config-deployment-pipeline) de insertarse en producción.

Si la variable **Pausa antes de implementar en producción** se requiere para una canalización de configuración, la siguiente es la solución sugerida hasta que se resuelva el error.

1. Ejecutar la canalización.
1. Pruebe el código en el entorno de ensayo.
1. Cuando la implementación y la aprobación estén disponibles, haga clic en **Rechazar**.
1. Edite la canalización para deshabilitar el **Pausa antes de implementar en producción** opción.
1. Vuelva a ejecutar la canalización. Se volverá a ejecutar en el ensayo y después en la producción.
