---
title: Notas de la versión de Cloud Manager en AEM como Cloud Service, versión 2020.8.0
description: Notas de la versión de Cloud Manager en AEM como Cloud Service, versión 2020.8.0
translation-type: tm+mt
source-git-commit: ca690144a8254d5ffba354f0f96d9ef1c5202533
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 1%

---


# Notas de la versión de Cloud Manager en Adobe Experience Manager como Cloud Service 2020.8.0 {#release-notes}

Esta página describe las Notas de la versión de Cloud Manager en AEM como Cloud Service 2020.8.0.

## Fecha de la versión {#release-date}

La fecha de versión de Cloud Manager en AEM como Cloud Service 2020.8.0 es el 06 de agosto de 2020.

## Novedades {#whats-new-cloud-manager}

* La auditoría de contenido es una función habilitada en Cloud Manager Sites Producines. La configuración de la tubería de producción para programas con sitios ahora incluye una tercera ficha denominada **Auditoría de contenido**. Siempre que se ejecute un flujo de producción, se incluirá un nuevo paso de auditoría de contenido en la canalización después de realizar pruebas funcionales personalizadas que evaluarán el sitio en relación con una serie de dimensiones, entre las que se incluyen rendimiento, SEO (Optimización de motores de búsqueda), accesibilidad, prácticas recomendadas y PWA (Aplicación web progresiva).


   >[!NOTE]
   >La auditoría de contenido se ha cambiado a Auditoría de experiencias.

   Consulte [Prueba de auditoría de experiencias](/help/implementing/cloud-manager/experience-audit-testing.md) para obtener más detalles.

* Los entornos recién creados en programas de Recursos ahora se configurarán automáticamente con Smart Content Services.

* Los entornos hibernados se pueden deshibernar desde la página **Información general** del Administrador de nube.

* Capacidad para realizar comprobaciones de experiencias en páginas, con tecnología de Google Lighthouse. Como parte de la canalización de Cloud Manager, se pueden comprobar y validar hasta 25 páginas con KPI de experiencia, y las puntuaciones se muestran en la interfaz de usuario del Cloud Manager.

### Corrección de errores {#bug-fixes-cm}

* Algunos complementos innecesarios y no deseados de SonarQube se estaban ejecutando como parte de la exploración de calidad del código.

* En la página de ejecución de la canalización, el nombre de la ramificación tenía un formato incorrecto.

* En algunos casos, las ejecuciones de los trámites terminados no se registraban correctamente por haberse completado, lo que impedía la ejecución de los nuevos trámites.

* Las ejecuciones de tuberías ocasionalmente se *atascaran* debido a problemas de comunicación interna.

* Al aprovisionar una nueva organización, a algunos usuarios con funciones administrativas distintas de los administradores del sistema se les daba acceso erróneamente a Cloud Manager.

* En determinadas condiciones, el trabajo de índices de actualización se inició varias veces en paralelo, lo que resultó en un error de implementación.

* La información sobre herramientas de las tarjetas de programa no era coherente.

* La interfaz de usuario permitía erróneamente que las operaciones se intentaran en un entorno mientras se eliminaba.

* Hubo una discordancia de color en la página **Información general** del Administrador de nube.

### Problemas conocidos {#known-issues-cm}

* Se incluyen páginas no válidas que llevan la puntuación promedio de auditoría de contenido por debajo de lo que deberían ser.

* La ficha Auditoría de contenido muestra incorrectamente la dirección URL base utilizando el dominio de autor en lugar del dominio de publicación.

* Para activar el paso Auditoría de contenido, los usuarios deben editar la canalización y, opcionalmente, agregar páginas. Si no se agrega ninguna página, se auditará la página principal.