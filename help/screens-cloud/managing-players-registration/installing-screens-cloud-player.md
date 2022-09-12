---
title: Instalación y configuración de reproductores en Screens as a Cloud Service
description: En esta página se describe cómo instalar y configurar reproductores en Screens as a Cloud Service.
exl-id: a022738a-c543-4629-a244-f70fa294fe7f
source-git-commit: 3367977496d3edad0f6f1e27e98eac95c791e870
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 1%

---

# Instalación y configuración de reproductores en Screens as a Cloud Service {#installing-players-screens-cloud}

En esta sección se describe cómo instalar reproductores de AEM Screens que están registrados en instancias de AEM locales. Además, debe realizar un restablecimiento de fábrica del reproductor existente y, a continuación, registrar el nuevo reproductor con AEM Screens as a Cloud Service.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo configurar su reproductor antes de registrar los reproductores. Después de leer, debe ser capaz de entender:

* donde instalar los reproductores desde
* cómo actualizar el reproductor al modo de nube

## Pasos para establecer el reproductor en modo de nube {#cloud-mode-setup}

Una vez descargado el último reproductor de [Descargas del reproductor de AEM Screens](https://download.macromedia.com/screens/), ya está listo para actualizar el reproductor al modo de nube.

Siga los pasos a continuación para actualizar el reproductor:

1. Abra el reproductor AEM Screens.

   >[!NOTE]
   >Puede elegir probar con dispositivos de hardware dedicados o con una extensión web en su propio reproductor.

1. Haga clic en el **Configuración** y haga clic en **A fábrica** botón debajo de **Restablecer** .

   ![imagen](/help/screens-cloud/assets/player/installplayer-2.png)

1. Haga clic en **Confirmar** para restablecer el reproductor.

1. De nuevo desde el **Configuración** y haga clic en **Cambiar al modo de nube** botón debajo de **Alternar modo de ejecución** .

   ![imagen](/help/screens-cloud/assets/player/installplayer-1.png)

1. Haga clic en **Confirmar** que se indica al cambiar al modo de nube, anulará el registro del reproductor.

## Monitorización de reproducción básica {#playback-monitoring}

El reproductor informa de varias métricas de reproducción con cada `ping` que toma el valor predeterminado 30 segundos. En función de estas métricas, podemos detectar varios casos extremos, como experiencia atascada, pantalla en blanco y problemas de programación. Esto nos permite comprender y solucionar problemas en el dispositivo y, por lo tanto, acelera la investigación y las medidas correctivas con usted.

La monitorización de reproducción básica en un reproductor AEM Screens permite:

* Monitorice de forma remota si un reproductor reproduce contenido correctamente.

* Mejore la reacción a pantallas en blanco o experiencias rotas en el campo .

* Reduce el riesgo de mostrar una experiencia rota al usuario final.

### Explicación de las propiedades {#understand-properties}

Las siguientes propiedades se incluyen en cada `ping`:

| Propiedad | Descripción |
|---|---|
| id {string} | el identificador del reproductor |
| activeChannel {string} | ruta de canal en reproducción o nulo si no hay nada programado |
| activeElements {string} | cadena separada por comas, elementos visibles actualmente en todos los canales de secuencias de reproducción (varios en caso de un diseño de varias zonas) |
| isDefaultContent {boolean} | true si el canal de reproducción se considera un canal predeterminado o de reserva (es decir, tiene prioridad 1 y no hay programación) |
| hasContentChanged {boolean} | true si el contenido ha cambiado en los últimos 5 minutos, false en caso contrario |
| lastContentChange {string} | marca de tiempo del último cambio de contenido |

>[!NOTE]
>De forma opcional, se puede activar una propiedad más avanzada desde las preferencias del reproductor (Activar monitorización de reproducción), es decir:
>|Propiedad|Descripción|
>|—|—|
>|isContentRendering {boolean}|true si la GPU puede confirmar que está reproduciendo contenido real (basado en el análisis de píxeles)|

### Restricciones     {#limitations}

A continuación se enumeran algunas limitaciones de la monitorización de reproducción básica:

* El reproductor informa de su propio estado de reproducción al servidor, por lo que requiere una conexión activa.

* La variable `isContentRendering` que comprueba que la GPU consume demasiados recursos como para habilitarla de forma predeterminada y requiere la inclusión explícita de las preferencias del reproductor. Se recomienda no utilizarlo junto con los vídeos en producción.

* Esta función solo se admite para canales de secuencia y aún no cubre el caso de uso de canales interactivos (SPA).

* Las métricas aún no están completamente expuestas a nuestros clientes, por lo que estamos trabajando duro en habilitar un mecanismo de alerta e informes similar al panel en un futuro próximo.

## Siguientes pasos {#whats-next}

Ahora que ha instalado y configurado el reproductor en el modo de nube, debe continuar con el recorrido as a Cloud Service de Screens revisando el documento, [Registro de reproductores en Screens as a Cloud Service](/help/screens-cloud/managing-players-registration/registering-players-screens-cloud.md) del proveedor de servicios de Screens.
