---
title: Pruebas de auditoría de experiencias
description: Descubra cómo la auditoría de experiencias valida el proceso de implementación y ayuda a garantizar que los cambios implementados cumplan los estándares de línea de base para el rendimiento, la accesibilidad, las prácticas recomendadas y la SEO.
exl-id: 8d31bc9c-d38d-4d5b-b2ae-b758e02b7073
source-git-commit: 3ba5184275e539027728ed134c47f66fa4746d9a
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 56%

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

La auditoría de experiencias en Cloud Manager garantiza que la experiencia del usuario en el sitio sea de los más altos estándares.

Los resultados de la auditoría son informativos y permiten al administrador de implementación ver las puntuaciones y el cambio entre las puntuaciones actuales y anteriores. Esta perspectiva es importante para determinar si hay una regresión que se haya introducido con la implementación actual.

La auditoría de experiencias está equipada con Google Lighthouse, una herramienta de código abierto de Google.

>[!INFO]
>
>A partir del 31 de agosto de 2023, la auditoría de experiencias pasará a mostrar resultados específicos de la plataforma móvil. Las métricas de rendimiento de Mobile suelen registrar menos que las de los equipos de escritorio, por lo que debería anticipar un cambio en el rendimiento del informe después de este cambio.

## Disponibilidad {#availability}

La auditoría de experiencias está disponible para Cloud Manager:

* Canalizaciones de producción de Sites, de forma predeterminada.
* Canalizaciones de desarrollo front-end, opcionalmente.

Consulte la [Sección Configuración](#configuration) para obtener más información sobre cómo configurar la auditoría para los entornos opcionales.

## Configuración {#configuration}

La auditoría de experiencias está disponible de forma predeterminada para las canalizaciones de producción. Se puede habilitar de forma opcional para canalizaciones de desarrollo front-end. En todos los casos, debe definir qué rutas de contenido se evalúan durante la ejecución de la canalización.

Puede configurar qué páginas se incluyen en la auditoría de experiencias al configurar la canalización.

1. Según el tipo de canalización que desee configurar, siga las instrucciones para:

   * Añadir un nuevo [canalización de producción,](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) si desea definir las rutas que debe evaluar la auditoría.
   * Añadir un nuevo [canalización que no sea de producción,](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) si desea habilitar la auditoría en una canalización front-end o de full-stack de desarrollo.
   * O puedes [editar una canalización existente,](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) y actualizar las opciones existentes.

1. Si está agregando o editando una canalización que no es de producción para la que desea utilizar la auditoría de experiencias, debe seleccionar la **Auditoría de experiencias** de la casilla de verificación **Código fuente** pestaña.

   ![Habilitar la auditoría de experiencias](assets/experience-audit-enable.jpg)

   * Esto solo es necesario para canalizaciones que no sean de producción.
   * El **Auditoría de experiencias** aparece cuando se selecciona la casilla de verificación.

1. Tanto para las canalizaciones de producción como para las que no son de producción, debe definir las rutas que deben incluirse en la auditoría de experiencias en la **Auditoría de experiencias** pestaña.

   * Las rutas de página deben comenzar con `/` y son relativos al sitio.
   * Por ejemplo, si el sitio es `wknd.site` y desea incluir `https://wknd.site/us/en/about-us.html` en la auditoría de experiencias, introduzca la ruta `/us/en/about-us.html`.

   ![Definición de una ruta para la auditoría de experiencias](assets/experience-audit-add-page.png)

1. Haga clic o pulse **Agregar página** y la ruta se completa automáticamente con la dirección de su entorno y se agrega a la tabla de rutas.

   ![Guardar ruta de acceso a la tabla](assets/experience-audit-page-added.png)

1. Siga agregando rutas según sea necesario repitiendo los dos pasos anteriores.

   * Puede agregar un máximo de 25 rutas.
   * Si no define una ruta, la página principal del sitio se incluye en la auditoría de experiencias de forma predeterminada.

1. Haga clic en **Guardar** para guardar la canalización.

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

* **Valor positivo** : Las páginas han mejorado en la prueba seleccionada desde que se ejecutó la última canalización de producción.

* **Valor negativo** : las páginas han retrocedido en la prueba seleccionada desde que se ejecutó la última canalización de producción.

* **Sin cambios** : Las páginas tienen la misma puntuación desde que se ejecutó la última canalización de producción.

* **N/D**: No había ninguna puntuación disponible para comparar.

![Resultados de la auditoría de experiencias](/help/implementing/cloud-manager/assets/exp-audit-1.png)

### Puntuaciones a nivel de página {#page-level-scores}

Al profundizar en cualquiera de las pruebas, se dispone de una puntuación a nivel de página más detallada. Se puede ver la puntuación de las páginas individuales para la prueba específica junto con el cambio con respecto a la anterior.

Al hacer clic en los detalles de cualquier página individual se proporciona información sobre los elementos de la página que se evaluaron, así como las instrucciones para solucionar problemas si se detectan oportunidades de mejora.

![Puntuaciones a nivel de página](/help/implementing/cloud-manager/assets/exp-audit-2.png)
