---
title: Panel de control de rendimiento de CDN
description: Comprenda cómo Cloud Manager evalúa el rendimiento de la red de entrega de contenido (CDN) y lo que puede aprender del tablero.
exl-id: ecd8c1ca-873f-4e73-ad73-b5f7561eb109
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 4%

---

# Panel de rendimiento de CDN {#cdn-performance}

Comprenda cómo Cloud Manager evalúa el rendimiento de la red de entrega de contenido (CDN) y lo que puede aprender del tablero.

## Información general {#overview}

Cada programa de Cloud Manager tiene un panel de rendimiento de CDN. Este panel presenta una puntuación general para el rendimiento de la CDN junto con tendencias, alertas y sugerencias para la mejora, según sea necesario.

![Panel de rendimiento de CDN](assets/cdn-performance-dashboard.png)

## Acceso al tablero {#accessing}

El panel CDN está disponible en la página de información general de cada programa.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, haga clic en el programa cuyo panel de CDN desee ver.

   ![Página de mis programas](assets/my-programs.png)

1. En la página **Resumen del programa** de tu programa, desplázate hacia abajo por debajo de las tarjetas de **Entornos** y **Canalizaciones** para ver la tarjeta de **Rendimiento**.

   ![Rendimiento](assets/cdn-performance-overview.png)

## Uso del tablero {#using}

El panel presenta una puntuación general para el rendimiento de la CDN junto con tendencias, alertas y sugerencias para la mejora, según sea necesario.

![Panel de rendimiento de CDN](assets/cdn-performance-dashboard.png)

Para obtener detalles sobre el rendimiento de su CDN y sugerencias sobre cómo mejorarlo, haga clic en **Ver tendencia**.

![Tendencia de rendimiento](assets/cdn-performance-trend.png)

Haga clic en **Ver** debajo del gráfico para cambiar el lapso de tiempo del gráfico.

Para obtener sugerencias sobre cómo mejorar el rendimiento de su CDN, seleccione la pestaña **Recommendations**.

![recomendaciones de CDN](assets/cdn-performance-recommendations.png)

Haga clic en comillas angulares junto a cualquier recomendación de la lista para ver detalles sobre los pasos que debe seguir para mejorar y la causa del problema.

## Definición de visita en caché {#cache-hit}

La proporción de visitas de caché mide cuántas solicitudes de contenido puede rellenar correctamente una caché en comparación con el número de solicitudes que recibe. Cuanto mayor sea la proporción de visitas de caché, mejor será el rendimiento de una CDN.

>[!TIP]
>
>Adobe recomienda que los usuarios busquen una proporción de visitas de caché del 99 %.

```text
Cache Hit Ratio = Cache Hits / (Hits + Misses + Passes + Other)
```

* **Visita**: se han solicitado datos de la caché y se han encontrado.
* **Faltante**: se han solicitado datos de la caché y no se han encontrado.
* **Paso**: se solicitan datos de la caché y se establece que no se almacenarán en caché estos datos en ningún caso.
* **Otro**: todas las solicitudes de datos de la caché que no coinciden con ningún otro caso.

Las métricas de caché se actualizan cada 24 horas.

>[!TIP]
>
>Para obtener más información sobre cómo Cloud Manager y la red de distribución de contenido (CDN) interactúan con Dispatcher, consulte [Almacenamiento en caché en AEM as a Cloud Service](/help/implementing/dispatcher/caching.md).
