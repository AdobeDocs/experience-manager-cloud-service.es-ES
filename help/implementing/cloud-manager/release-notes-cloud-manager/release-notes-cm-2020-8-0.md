---
title: Notas de la versión para Cloud Manager en AEM versión as a Cloud Service 2020.8.0
description: Notas de la versión para Cloud Manager en AEM versión as a Cloud Service 2020.8.0
feature: Release Information
exl-id: 70674e16-f9ba-4777-98fe-34161e90a481
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 1%

---

# Notas de la versión para Cloud Manager en Adobe Experience Manager as a Cloud Service 2020.8.0 {#release-notes}

Esta página describe las notas de la versión de Cloud Manager en AEM as a Cloud Service 2020.8.0.

## Fecha de la versión {#release-date}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2020.8.0 es el 6 de agosto de 2020.

## Novedades {#whats-new-cloud-manager}

* La auditoría de contenido es una función habilitada en las canalizaciones de producción de Cloud Manager Sites. La configuración de Canalización de producción para programas con Sitios ahora incluye una tercera pestaña denominada **Auditoría de contenido**. Cada vez que se ejecute un flujo de producción, se incluirá un nuevo paso de Auditoría de contenido en la canalización después de realizar pruebas funcionales personalizadas que evaluarán el sitio en relación con una serie de dimensiones, entre las que se incluyen rendimiento, SEO (Optimización de motores de búsqueda), accesibilidad, prácticas recomendadas y PWA (Aplicación web progresiva).


   >[!NOTE]
   >Desde entonces, se ha cambiado el nombre de Auditoría de contenido a Auditoría de experiencias.

   Consulte [Pruebas de auditoría de experiencias](/help/implementing/cloud-manager/experience-audit-testing.md) para obtener más información.

* Los entornos recién creados en los programas de Assets ahora se configurarán automáticamente con Smart Content Services.

* Los entornos en hibernación se pueden eliminar de la hibernación desde el **Información general** página.

* Capacidad para realizar comprobaciones de experiencias en páginas, con tecnología Google Lighthouse. Como parte de la canalización de Cloud Manager, se pueden comprobar y validar hasta 25 páginas con KPI de experiencia, y las puntuaciones se muestran en la interfaz de usuario de Cloud Manager.

### Corrección de errores {#bug-fixes-cm}

* Algunos complementos innecesarios y no deseados de SonarQube se estaban ejecutando como parte del análisis de calidad del código.

* En la página de ejecución de la canalización, el nombre de la rama tenía un formato incorrecto.

* En algunos casos, no se registró con éxito la finalización de las ejecuciones de canalización, lo que impidió nuevas ejecuciones de la canalización.

* Las ejecuciones de canalización ocasionalmente se obtienen *atascado* debido a problemas de comunicación interna.

* Al aprovisionar una nueva organización, a algunos usuarios con funciones administrativas distintas de los administradores del sistema se les daba acceso erróneamente a Cloud Manager.

* En ciertas condiciones, el trabajo de índices de actualización se inició varias veces en paralelo, lo que resultó en un error de implementación.

* La información sobre herramientas de las tarjetas de programa no era coherente.

* La interfaz de usuario permitía erróneamente que se intentaran realizar operaciones en un entorno mientras se eliminaba.

* Hubo una discordancia de color en el informe de Cloud Manager **Información general** página.

### Problemas conocidos {#known-issues-cm}

* Se incluyen páginas no válidas que llevan la puntuación media de auditoría de contenido por debajo de lo que deberían ser.

* La pestaña Auditoría de contenido muestra incorrectamente la dirección URL base utilizando el dominio de autor en lugar del dominio de publicación.

* Para activar el paso Auditoría de contenido, los usuarios deben editar la canalización y, opcionalmente, agregar páginas. Si no se agregan páginas, se auditará la página principal.
