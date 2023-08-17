---
title: Pruebas de auditoría de experiencias
description: Descubra cómo la auditoría de experiencias valida el proceso de implementación y ayuda a garantizar que los cambios implementados cumplan los estándares de línea de base para el rendimiento, la accesibilidad, las prácticas recomendadas y la SEO.
exl-id: 8d31bc9c-d38d-4d5b-b2ae-b758e02b7073
source-git-commit: e9f205a506fb2d2b7f5e634b353b112bf077058a
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 85%

---


# Pruebas de auditoría de experiencias {#experience-audit-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_expaudittesting"
>title="Pruebas de auditoría de experiencias"
>abstract="Descubra cómo la auditoría de experiencias valida el proceso de implementación y ayuda a garantizar que los cambios implementados cumplan los estándares de línea de base para el rendimiento, la accesibilidad, las prácticas recomendadas y la SEO."

Descubra cómo la auditoría de experiencias valida el proceso de implementación y ayuda a garantizar que los cambios implementados cumplan los estándares de línea de base para el rendimiento, la accesibilidad, las prácticas recomendadas y la SEO.

## Información general {#overview}

La auditoría de experiencia es una característica disponible en las canalizaciones de producción de Cloud Manager Sites que valida el proceso de implementación y que ayuda a garantizar que los cambios implementados:

1. Cumplan los estándares de línea de base para el rendimiento, la accesibilidad, las prácticas recomendadas, la SEO (optimización de motores de búsqueda) y la PWA (aplicación web progresiva).

1. No introduzcan regresiones.

La auditoría de experiencias en Cloud Manager garantiza que la experiencia del usuario final en el sitio sea de los más altos estándares.

Los resultados de la auditoría son informativos y permiten al administrador de implementación ver las puntuaciones y el cambio entre las puntuaciones actuales y anteriores. Esta perspectiva es valiosa para determinar si hay una regresión que se introdujo con la implementación actual.

La auditoría de experiencias está equipada con Google Lighthouse, una herramienta de código abierto de Google y está habilitada en todas las canalizaciones de producción de Cloud Manager.

>[!INFO]
>
>A partir del 28 de agosto de 2023, la auditoría de experiencias pasará a mostrar resultados específicos de la plataforma móvil. Tenga en cuenta que las métricas de rendimiento móviles suelen registrarse por debajo de las del escritorio, por lo que debe anticipar un cambio en el rendimiento del informe después de este cambio.

>[!TIP]
>
>Puede configurar qué páginas se incluyen en la Auditoría de experiencias al [configurar la canalización](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#full-stack-code).

## Comprender los resultados de la auditoría de experiencias {#understanding-experience-audit-results}

La auditoría de experiencias proporciona resultados de prueba agregados y detallados a nivel de página a través de la [página de ejecución de canalizaciones de producción](/help/implementing/cloud-manager/deploy-code.md).

* Las métricas agregadas miden las puntuaciones medias en las páginas que fueron auditadas para el rendimiento, la accesibilidad, las prácticas recomendadas y la SEO (optimización del motor de búsqueda).
* Las puntuaciones a nivel de página individuales también están disponibles mediante “explorar en profundidad”.
* Los detalles de las puntuaciones están disponibles para ver los resultados de las pruebas individuales, y también hay instrucciones sobre cómo remediar cualquier problema que se haya identificado.
* En Cloud Manager existe un historial de los resultados de la prueba para determinar si los cambios que se introducen en la canalización incluyen alguna regresión de la ejecución anterior.

### Puntuaciones agregadas {#aggregate-scores}

La puntuación a nivel agregado toma la puntuación media de las páginas incluidas en la ejecución. El cambio a nivel agregado representa la puntuación media de las páginas en la ejecución actual comparada con la media de las puntuaciones de la ejecución anterior, incluso si la colección de páginas configuradas para incluirse se ha cambiado entre ejecuciones.

Hay una puntuación a nivel agregado para cada tipo de prueba, como rendimiento, accesibilidad, SEO y prácticas recomendadas.

La métrica de cambios puede tener uno de los siguientes valores.

* **Valor positivo**: Las páginas han mejorado en la prueba seleccionada desde la última ejecución de la canalización de producción.

* **Valor negativo**: Las páginas han retrocedido en la prueba seleccionada desde que se ejecutó la última canalización de producción.

* **Sin cambio**: Las páginas tienen la misma puntuación desde que se ejecutó la última canalización de producción.

* **N/D**: No había ninguna puntuación disponible para comparar.

![Resultados de la auditoría de experiencias](/help/implementing/cloud-manager/assets/exp-audit-1.png)

### Puntuaciones a nivel de página {#page-level-scores}

Al profundizar en cualquiera de las pruebas, se dispone de una puntuación a nivel de página más detallada. Se puede ver la puntuación de las páginas individuales para la prueba específica junto con el cambio con respecto a la anterior.

Al hacer clic en los detalles de cualquier página individual se proporciona información sobre los elementos de la página que se evaluaron y se proporcionan instrucciones para solucionar problemas si se detectan oportunidades de mejora.

![Puntuaciones a nivel de página](/help/implementing/cloud-manager/assets/exp-audit-2.png)
