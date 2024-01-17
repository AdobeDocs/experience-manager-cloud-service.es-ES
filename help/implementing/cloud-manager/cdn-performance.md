---
title: Tablero de rendimiento de CDN
description: Comprenda cómo Cloud Manager evalúa el rendimiento de la red de entrega de contenido (CDN) y lo que puede aprender del tablero.
source-git-commit: 0d60c19638707262dab7f290f84fa873b694bc22
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 3%

---


# Tablero de rendimiento de CDN {#cdn-performance}

Comprenda cómo Cloud Manager evalúa el rendimiento de la red de entrega de contenido (CDN) y lo que puede aprender del tablero.

## Información general {#overview}

Cada programa de Cloud Manager tiene un panel de rendimiento de CDN. Este panel presenta una puntuación general para el rendimiento de la CDN junto con tendencias, alertas y sugerencias para la mejora, según sea necesario.

![Panel de rendimiento de CDN](assets/cdn-performance-dashboard.png)

## Acceso al panel {#accessing}

El panel CDN está disponible en la página de información general de cada programa.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En el **[Mis programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** , pulse o haga clic en el programa cuyo panel CDN desee ver.

   ![Página Mis programas](assets/my-programs.png)

1. En el **Resumen del programa** de su programa, desplácese hacia abajo por debajo de la **Entornos** y **Canalizaciones** para ver las **Rendimiento** Tarjeta de.

   ![Rendimiento](assets/cdn-performance-overview.png)

## Uso del panel {#using}

El panel presenta una puntuación general para el rendimiento de la CDN junto con tendencias, alertas y sugerencias para la mejora, según sea necesario.

![Panel de rendimiento de CDN](assets/cdn-performance-dashboard.png)

Para obtener más información sobre el rendimiento de su CDN, así como sugerencias sobre cómo mejorarlo, toque o haga clic en **Ver tendencia**.

![Tendencia de rendimiento](assets/cdn-performance-trend.png)

Haga clic o pulse **Ver** debajo del gráfico para cambiar el lapso de tiempo del gráfico.

Para obtener sugerencias sobre cómo mejorar el rendimiento de la CDN, seleccione la **Recommendations** pestaña.

![Recomendaciones de CDN](assets/cdn-performance-recommendations.png)

Toque o haga clic en las comillas angulares junto a cualquier recomendación de la lista para ver detalles acerca de los pasos que debe seguir para mejorar y la causa del problema.

## Definición de visita en caché {#cache-hit}

La proporción de visitas de caché mide cuántas solicitudes de contenido puede rellenar correctamente una caché en comparación con el número de solicitudes que recibe. Cuanto mayor sea la proporción de visitas de caché, mejor será el rendimiento de una CDN.

>[!TIP]
>
>El Adobe recomienda que los usuarios busquen una proporción de visitas de caché del 99 %.

```text
Cache Hit Ratio = Cache Hits / (Hits + Misses + Passes + Other)
```

* **Visita** : se solicitan los datos de la caché y se encuentran.
* **Señorita** - Se solicitan datos de la caché y no se encuentran.
* **Aprobado** - Se solicitan datos de la caché y se establece que no se almacenarán en caché estos datos en ningún caso.
* **Otros** : Todas las solicitudes de datos de la caché que no coinciden con ningún otro caso.

Las métricas de caché se actualizan cada 24 horas.

>[!TIP]
>
>Para obtener más información sobre cómo Cloud Manager y la CDN interactúan con Dispatcher, consulte el documento [AEM Almacenamiento en caché en as a Cloud Service de.](/help/implementing/dispatcher/caching.md)
