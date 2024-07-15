---
title: Instalación y configuración de reproductores en Screens as a Cloud Service
description: En esta página se describe cómo instalar y configurar reproductores en Screens as a Cloud Service.
exl-id: a022738a-c543-4629-a244-f70fa294fe7f
feature: Developing Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 1%

---

# Instalación y configuración de reproductores en Screens as a Cloud Service {#installing-players-screens-cloud}

En esta sección se describe cómo instalar reproductores de AEM Screens AEM registrados en instancias de on-premise. Además, debe hacer un restablecimiento de fábrica del reproductor existente y luego registrar el nuevo reproductor contra AEM Screens as a Cloud Service.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo configurar el reproductor antes de registrarlo. Después de leer, debería poder comprender lo siguiente:

* desde dónde instalar los reproductores
* Actualizar el reproductor al modo de nube

## Pasos para establecer el reproductor en modo de nube {#cloud-mode-setup}

Después de descargar el reproductor más reciente de [Descargas del reproductor AEM Screens](https://download.macromedia.com/screens/), ya puede actualizar el reproductor al modo de nube.

Siga los pasos a continuación para actualizar el reproductor:

1. Abra el reproductor de AEM Screens.

   >[!NOTE]
   >Puede elegir realizar pruebas con dispositivos de hardware dedicados o con una extensión web en su propio reproductor.

1. Haga clic en la ficha **Configuración** y luego en el botón **Para usar la fábrica** en la opción **Restablecer**.

   ![imagen](/help/screens-cloud/assets/player/installplayer-2.png)

1. Haz clic en **Confirmar** para restablecer el reproductor.

1. Vuelva a la pestaña **Configuración** y haga clic en el botón **Cambiar al modo de nube** en la opción **Alternar modo de ejecución**.

   ![imagen](/help/screens-cloud/assets/player/installplayer-1.png)

1. Haga clic en **Confirmar** que le avise cuando se cambie al modo de nube para anular el registro del reproductor.

## Monitorización de reproducción básica {#playback-monitoring}

El reproductor informa de varias métricas de reproducción con cada `ping` cuyo valor predeterminado es de 30 segundos. En función de estas métricas, el Adobe puede detectar varios casos extremos, como experiencias atascadas, pantallas en blanco y problemas de programación. Esta detección nos permite comprender y solucionar problemas en el dispositivo y, por lo tanto, acelera una investigación y medidas correctivas con usted.

La monitorización de la reproducción básica en un reproductor AEM Screens nos permite:

* Monitorice de forma remota si un reproductor está reproduciendo el contenido correctamente.

* Mejore la reacción a pantallas en blanco o experiencias rotas en el campo.

* Reduce el riesgo de mostrar una experiencia rota al usuario.

### Explicación de propiedades {#understand-properties}

En cada `ping` se incluyen las siguientes propiedades:

| Propiedad | Descripción |
|---|---|
| id {string} | el identificador del reproductor |
| activeChannel {string} | ruta de canal en reproducción, o nulo si no hay nada programado |
| activeElements {string} | cadena separada por comas, elementos visibles actualmente en todos los canales de secuencia de reproducción (varios si había un diseño de varias zonas) |
| isDefaultContent {boolean} | true si el canal de reproducción se considera un canal predeterminado o de reserva (es decir, tiene prioridad 1 y no hay programación) |
| hasContentChanged {boolean} | true si el contenido ha cambiado en los últimos 5 minutos, false en caso contrario |
| lastContentChange {string} | marca de tiempo del último cambio de contenido |

>[!NOTE]
>De forma opcional, puede activar una propiedad más avanzada desde las preferencias del reproductor (Activar monitorización de reproducción):
>|Propiedad|Descripción|
>|—|—|
>|isContentRendering {boolean}|true si la GPU puede confirmar que está reproduciendo contenido real (según el análisis de píxeles)|

### Limitaciones {#limitations}

A continuación se enumeran algunas limitaciones de la monitorización básica de la reproducción:

* El reproductor informa de su propio estado de reproducción al servidor, por lo que requiere una conexión activa.

* La propiedad `isContentRendering` que comprueba la GPU consume demasiados recursos para habilitarse de forma predeterminada y requiere la inclusión explícita en las preferencias del reproductor. Se recomienda no utilizarlo con vídeos en producción.

* SPA Esta función solo se admite para canales de secuencia y aún no cubre el caso de uso de canales interactivos ().

* Las métricas aún no están completamente expuestas a los clientes; Adobe está trabajando en la activación del mecanismo de creación de informes y alertas de tipo panel próximamente.

## Siguientes pasos {#whats-next}

Ahora que ha instalado y configurado el reproductor en el modo de nube, continúe con el as a Cloud Service recorrido de Screens. Consulte [Registro de reproductores en Screens as a Cloud Service](/help/screens-cloud/managing-players-registration/registering-players-screens-cloud.md) del proveedor de servicios de Screens.
