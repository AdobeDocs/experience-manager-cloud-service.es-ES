---
title: 'Pruebas de auditoría de experiencias: Cloud Services'
description: 'Pruebas de auditoría de experiencias: Cloud Services'
exl-id: 8d31bc9c-d38d-4d5b-b2ae-b758e02b7073
translation-type: tm+mt
source-git-commit: f6c700f82bc5a1a3edf05911a29a6e4d32dd3f72
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# Prueba de auditoría de experiencias {#experience-audit-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_expaudittesting"
>title="Pruebas de auditoría de experiencias"
>abstract="Experience Audit es una función disponible en las canalizaciones de producción de Cloud Manager Sites, con tecnología de Google Lighthouse, una herramienta de código abierto de Google. Esta función está habilitada en todas las canalizaciones de producción de Cloud Manager."

Experience Audit es una función disponible en las canalizaciones de producción de Cloud Manager Sites, con tecnología de Google Lighthouse, una herramienta de código abierto de Google. Esta función está habilitada en todas las canalizaciones de producción de Cloud Manager.

Valida el proceso de implementación y ayuda a garantizar que los cambios implementados:

1. Cumplir los estándares de línea de base para rendimiento, accesibilidad, prácticas recomendadas, SEO (Optimización de motores de búsqueda) y PWA (Aplicación web progresiva).

1. No incluya regresiones en estas dimensiones.

Experience Audit en Cloud Manager garantiza que la experiencia digital de los usuarios finales en el sitio se pueda mantener con los estándares más altos. Los resultados son informativos y permiten al usuario ver las puntuaciones y el cambio entre las puntuaciones actual y anterior. Esta perspectiva es valiosa para determinar si hay una regresión que se introducirá con la implementación actual.

## Explicación de los resultados de auditoría de experiencias {#understanding-experience-audit-results}

La auditoría de experiencias proporciona resultados de prueba agregados y detallados a nivel de página a través de la página de ejecución de la canalización de producción .

* Las métricas de nivel agregado miden la puntuación promedio en las páginas auditadas para rendimiento, accesibilidad, prácticas recomendadas, SEO (Optimización del motor de búsqueda).
   >[!NOTE]
   >La puntuación de aplicación web progresiva (PWA) no se incluye en la puntuación de resumen y solo se muestra en la pantalla de detalles del informe a nivel de página.
* Las puntuaciones de nivel de página individuales también están disponibles mediante desglose.
* Se dispone de detalles de las puntuaciones para ver cuáles son los resultados de las pruebas individuales, así como directrices sobre cómo remediar cualquier problema que se identificara durante la auditoría de experiencias.
* En Cloud Manager persiste un historial de los resultados de la prueba, de modo que los clientes puedan ver si los cambios que se introducen en la ejecución de la canalización incluyen alguna regresión de la ejecución anterior.

### Puntuaciones agregadas {#aggregate-scores}

Hay una puntuación de nivel agregado para cada tipo de prueba, como rendimiento, accesibilidad, SEO y prácticas recomendadas.
>[!NOTE]
>La puntuación de aplicación web progresiva (PWA) no se incluye en la puntuación de resumen y solo se muestra en la pantalla de detalles del informe a nivel de página.

La puntuación de nivel agregado toma la puntuación promedio de las páginas incluidas en la ejecución. El cambio en el nivel de agregado representa la puntuación media de las páginas en la ejecución actual comparada con la media de las puntuaciones de la ejecución anterior, incluso si la colección de páginas configuradas para incluirse se ha cambiado entre ejecuciones.

El valor de la métrica Cambio puede ser uno de los siguientes:

* **Valor positivo** : las páginas han mejorado en la prueba seleccionada desde la última ejecución de la canalización de producción.

* **Valor negativo** : las páginas han retrocedido en la prueba seleccionada desde la última ejecución de la canalización de producción.

* **Sin cambios** : las páginas tienen la misma puntuación desde la última ejecución de la canalización de producción

* **N/A** : no había ninguna puntuación anterior disponible para comparar

   ![](/help/implementing/cloud-manager/assets/exp-audit-1.png)


### Puntuaciones de nivel de página {#page-level-scores}

Al profundizar en cualquiera de las pruebas, se puede ver una puntuación de nivel de página más detallada. El usuario podrá ver cómo clasificaron las páginas individuales para la prueba específica junto con el cambio de la hora anterior en que se ejecutó la prueba.

Al hacer clic en los detalles de cualquier página individual se proporcionará información sobre los elementos de la página que se evaluaron y directrices para solucionar problemas si se detectan oportunidades de mejora. Google Lighthouse proporciona los detalles de las pruebas y las directrices asociadas.

![](/help/implementing/cloud-manager/assets/exp-audit-2.png)
