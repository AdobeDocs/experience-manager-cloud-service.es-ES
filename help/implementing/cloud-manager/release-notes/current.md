---
title: Notas de la versión 2023.9.0 para Cloud Manager en Adobe Experience Manager as a Cloud Service
description: Estas son las notas de la versión 2023.9.0 para Cloud Manager en AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 8bf2ffe8b1d3780f4ad3f6972fea4f8281945abb
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 23%

---


# Notas de la versión 2023.9.0 para Cloud Manager en Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta las notas de la versión 2023.9.0 para Cloud Manager en AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de Cloud Manager 2023.9.0 en AEM as a Cloud Service fue el 14 de septiembre de 2023. El próximo lanzamiento está programado para el 5 de octubre de 2023.

## Novedades {#what-is-new}

* Los registros de CDN, cuando están disponibles, se pueden descargar a través de la IU de Cloud Manager.
* Los usuarios ahora pueden optar por incluir las pruebas de auditoría de experiencias con tecnología Google LightHouse en canalizaciones full stack que no sean de producción.

## Programa de adopción temprana {#early-adoption}

Forme parte de nuestro programa de adopción anticipada y tenga la oportunidad de probar algunas de las próximas funciones.

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

## Correcciones de errores {#bug-fixes}

* Cuando se elimina un programa, también se elimina cualquier canalización asociada en ejecución, lo que garantiza que la canalización no se designe incorrectamente como estado de error.
* El botón Publicar finalización está desactivado e informa al usuario del motivo por el que una canalización está en curso.
* En ocasiones, cuando se &#39;completan&#39; todos los pasos de la ejecución de una canalización, el estado de la canalización se ve como &quot;en ejecución&quot;, lo que hace que parezca que está en un estado atascado. Ahora se ve como &#39;Completo&#39;.
