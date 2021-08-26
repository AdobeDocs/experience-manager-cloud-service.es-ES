---
title: Instalación y configuración de reproductores en Screens as a Cloud Service
description: En esta página se describe cómo instalar y configurar reproductores en Screens como Cloud Service.
source-git-commit: 6afb71803ae24bed2d5d5662a7cdd4af5637e329
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 1%

---


# Instalación y configuración de reproductores en Screens as a Cloud Service {#installing-players-screens-cloud}

En esta sección se describe cómo instalar reproductores de AEM Screens que están registrados en instancias de AEM locales. Además, debe realizar un restablecimiento de fábrica del reproductor existente y, a continuación, registrar el nuevo reproductor en AEM Screens como Cloud Service.

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

1. Haga clic en la pestaña **Configuration** y haga clic en el botón **To Factory** en la opción **Reset**.

   ![image](/help/screens-cloud/assets/player/installplayer-2.png)

1. Haga clic en **Confirm** para reiniciar el reproductor.

1. De nuevo, en la pestaña **Configuration** y haga clic en el botón **Change to Cloud Mode** en la opción **Toggle Runmode**.

   ![image](/help/screens-cloud/assets/player/installplayer-1.png)

1. Haga clic en **Confirm** que se muestra al cambiar al modo de nube, se anulará el registro del reproductor.

## Monitorización de reproducción básica {#playback-monitoring}

El reproductor informa de varias métricas de reproducción con cada `ping` cuyo valor predeterminado es de 30 segundos. En función de las métricas, puede detectar varios casos extremos, como experiencia atascada, pantalla en blanco y problemas de programación. Esto le permite comprender y solucionar problemas en el dispositivo y, por lo tanto, agiliza la investigación y las medidas correctivas.

La monitorización de reproducción básica en un reproductor AEM Screens le permite:

* Monitorice de forma remota si un reproductor está reproduciendo contenido correctamente

* Mejore la reacción a pantallas en blanco o experiencias rotas en el campo

* Disminuya el riesgo de mostrar una experiencia rota al usuario final

### Explicación de las propiedades {#understand-properties}

En cada `ping` se incluyen las siguientes propiedades:

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


## Siguientes pasos {#whats-next}

Ahora que ha instalado y configurado el reproductor en el modo de nube, debe continuar con el recorrido Screens como Cloud Service revisando el documento [Registro de reproductores en Screens como Cloud Service](/help/screens-cloud/managing-players-registration/registering-players-screens-cloud.md) del proveedor de servicios de Screens.