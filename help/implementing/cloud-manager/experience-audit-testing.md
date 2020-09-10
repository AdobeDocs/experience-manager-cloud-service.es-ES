---
title: Prueba de auditoría de experiencias - Cloud Services
description: Prueba de auditoría de experiencias - Cloud Services
translation-type: tm+mt
source-git-commit: 28ba5412190560b21b27068832ba05cfff24c079
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---


# Prueba de auditoría de experiencias {#experience-audit-testing}

Experience Audit es una función disponible en los canales de producción de Cloud Manager Sites, con tecnología de Google Lighthouse, una herramienta de código abierto de Google. Esta función está habilitada en todas las canalizaciones de producción de Cloud Manager.

Valida el proceso de implementación y ayuda a garantizar que los cambios implementados:

1. Cumplir los estándares de referencia para rendimiento, accesibilidad, optimizaciones, SEO (Optimización de motores de búsqueda) y PWA (Aplicación web progresiva).

1. No incluya regresiones en estas dimensiones.

La auditoría de experiencias en Cloud Manager garantiza que la experiencia digital de los usuarios finales en el sitio se pueda mantener con los estándares más altos. Los resultados son informativos y permiten al usuario ver las puntuaciones y el cambio entre la puntuación actual y la anterior. Esta perspectiva es valiosa para determinar si existe una regresión que se introducirá con la implementación actual.

## Explicación de los resultados de la auditoría de experiencias {#understanding-experience-audit-results}

La auditoría de experiencias proporciona resultados de prueba acumulados y detallados a nivel de página a través de la página de ejecución de la tubería de producción.

* Las métricas de nivel acumulado miden la puntuación promedio en las páginas que fueron auditadas por rendimiento, accesibilidad, optimizaciones, SEO (Optimización de motores de búsqueda).
   >[!NOTE]
   >La puntuación de la aplicación web progresiva (PWA) no se incluye en la puntuación de resumen y solo se mostrará en la pantalla de detalles del informe a nivel de página.
* Las puntuaciones de nivel de página individuales también están disponibles mediante el desglose.
* Los detalles de las puntuaciones están disponibles para ver cuáles son los resultados de las pruebas individuales, junto con la guía sobre cómo solucionar cualquier problema que se identificó durante la auditoría de contenido.
* Dentro del Administrador de nube se conserva un historial de los resultados de la prueba para que los clientes puedan ver si los cambios que se introducen en la ejecución de la canalización incluyen alguna regresión de la ejecución anterior.

### Puntuaciones acumuladas {#aggregate-scores}

Hay una puntuación de nivel acumulada para cada tipo de prueba, como rendimiento, accesibilidad, SEO y prácticas recomendadas.
>[!NOTE]
>La puntuación de la aplicación web progresiva (PWA) no se incluye en la puntuación de resumen y solo se mostrará en la pantalla de detalles del informe a nivel de página.

La puntuación de nivel acumulado toma la puntuación media de las páginas incluidas en la ejecución. El cambio en el nivel acumulado representa la puntuación media de las páginas en la ejecución actual en comparación con la media de las puntuaciones de la ejecución anterior, incluso si la colección de páginas configuradas para incluirse se ha modificado entre ejecuciones.

El valor de la métrica Cambio puede ser uno de los siguientes:

* **Valor** positivo: las páginas han mejorado en la prueba seleccionada desde la última ejecución de la canalización de producción

* **Valor** negativo: las páginas han retrocedido en la prueba seleccionada desde la última ejecución de la canalización de producción

* **Sin cambios** : las páginas tienen el mismo puntaje desde la última ejecución del flujo de producción

* **N/D** : no había ninguna puntuación anterior disponible para comparar

   ![](/help/implementing/cloud-manager/assets/exp-audit-1.png)


### Puntuaciones de nivel de página {#page-level-scores}

Al explorar en profundidad cualquiera de las pruebas, se puede ver una puntuación de nivel de página más detallada. El usuario podrá ver cómo las páginas individuales se clasificaron para la prueba específica junto con el cambio de la hora anterior en que se ejecutó la prueba.

Al hacer clic en los detalles de cualquier página individual se proporcionará información sobre los elementos de la página que se evaluaron y una guía para solucionar problemas si se detectan oportunidades de mejora. Los detalles de las pruebas y las directrices asociadas son proporcionados por Google Lighthouse.

![](/help/implementing/cloud-manager/assets/exp-audit-2.png)

