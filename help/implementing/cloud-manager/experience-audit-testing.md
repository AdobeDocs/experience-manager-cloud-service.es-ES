---
title: Pruebas de auditoría de experiencias
description: Descubra cómo Experience Audit valida el proceso de implementación y ayuda a garantizar que los cambios implementados cumplan los estándares de línea de base para rendimiento, accesibilidad, prácticas recomendadas y SEO.
exl-id: 8d31bc9c-d38d-4d5b-b2ae-b758e02b7073
source-git-commit: 15de47e28e804fd84434d5e8e5d2fe8fe6797241
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 1%

---


# Pruebas de auditoría de experiencias {#experience-audit-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_expaudittesting"
>title="Pruebas de auditoría de experiencias"
>abstract="Descubra cómo Experience Audit valida el proceso de implementación y ayuda a garantizar que los cambios implementados cumplan los estándares de línea de base para rendimiento, accesibilidad, prácticas recomendadas y SEO."

Descubra cómo Experience Audit valida el proceso de implementación y ayuda a garantizar que los cambios implementados cumplan los estándares de línea de base para rendimiento, accesibilidad, prácticas recomendadas y SEO.

## Información general {#overview}

La auditoría de experiencia es una función disponible en las canalizaciones de producción de Cloud Manager Sites que valida el proceso de implementación y que ayuda a garantizar que los cambios implementados:

1. Cumplir los estándares de línea de base para rendimiento, accesibilidad, prácticas recomendadas, SEO (Optimización de motores de búsqueda) y PWA (Aplicación web progresiva).

1. No introduzca regresiones.

Auditar experiencias en Cloud Manager garantiza que la experiencia del usuario final en el sitio sea de los más altos estándares.

Los resultados de la auditoría son informativos y permiten al administrador de implementación ver las puntuaciones y el cambio entre las puntuaciones actual y anterior. Esta perspectiva es valiosa para determinar si hay una regresión que se introducirá con la implementación actual.

Experience Audit está equipado con Google Lighthouse, una herramienta de código abierto de Google, y está habilitada en todas las canalizaciones de producción de Cloud Manager.

## Comprender los resultados de la auditoría de experiencias {#understanding-experience-audit-results}

La auditoría de experiencias proporciona resultados de prueba agregados y detallados en el nivel de página a través del [página de ejecución de canalización de producción .](/help/implementing/cloud-manager/deploy-code.md)

* Las métricas agregadas miden las puntuaciones promedio en las páginas que fueron auditadas para rendimiento, accesibilidad, prácticas recomendadas, SEO (Optimización del motor de búsqueda).
* Las puntuaciones de nivel de página individuales también están disponibles mediante desglose.
* Los detalles de las puntuaciones están disponibles para ver los resultados de las pruebas individuales, así como instrucciones sobre cómo remediar cualquier problema que se haya identificado.
* En Cloud Manager persiste un historial de los resultados de la prueba para determinar si los cambios que se introducen en la canalización incluyen alguna regresión de la ejecución anterior.

### Puntuaciones agregadas {#aggregate-scores}

La puntuación de nivel agregado toma la puntuación promedio de las páginas incluidas en la ejecución. El cambio en el nivel de agregado representa la puntuación media de las páginas en la ejecución actual comparada con la media de las puntuaciones de la ejecución anterior, incluso si la colección de páginas configuradas para incluirse se ha cambiado entre ejecuciones.

Hay una puntuación de nivel agregado para cada tipo de prueba, como rendimiento, accesibilidad, SEO y prácticas recomendadas.

La métrica de cambios puede tener uno de los siguientes valores.

* **Valor positivo** - Las páginas han mejorado en la prueba seleccionada desde la última ejecución de la canalización de producción.

* **Valor negativo** : las páginas han retrocedido en la prueba seleccionada desde que se ejecutó la última canalización de producción.

* **Sin cambio** - Las páginas tienen la misma puntuación desde que se ejecutó la última canalización de producción.

* **N/D** - No había ninguna puntuación disponible para comparar.

![Resultados de la auditoría de experiencias](/help/implementing/cloud-manager/assets/exp-audit-1.png)


### Puntuaciones de nivel de página {#page-level-scores}

Al profundizar en cualquiera de las pruebas, se dispone de una puntuación de nivel de página más detallada. Se puede ver la puntuación de las páginas individuales para la prueba específica junto con el cambio con respecto a la anterior.

Al hacer clic en los detalles de cualquier página individual se proporciona información sobre los elementos de la página que se evaluaron, así como instrucciones para solucionar problemas si se detectan oportunidades de mejora.

![Puntuaciones en el nivel de página](/help/implementing/cloud-manager/assets/exp-audit-2.png)
