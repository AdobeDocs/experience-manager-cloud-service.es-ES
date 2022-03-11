---
title: Asignación de canales a una visualización en Screens as a Cloud Service
description: En esta página se describe cómo asignar un canal a una pantalla de Screens as a Cloud Service.
exl-id: ba001c18-7b05-4ae2-aa7f-9ebb320fedd0
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 19%

---

# Asignación de canales a una visualización en Screens as a Cloud Service {#assign-channel-displays-screens-cloud}

Una vez completada la configuración del proyecto, debe asignar el canal a una pantalla para ver el contenido.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo asignar un canal a una pantalla, una vez que la pantalla esté lista y haya añadido contenido al canal y lo haya publicado. Después de leer, debe poder comprender cómo asignar un canal a una pantalla del proveedor de servicios de Screens.

## Requisitos previos {#prerequisites}

Antes de realizar los pasos siguientes para asignar un canal a una pantalla, debe haber terminado de aprender:

* Crear y administrar visualizaciones
* Crear y administrar canales

## Pasos para asignar un canal a una pantalla {#assign-channel-to-display}

Siga los pasos a continuación para asignar un canal a una visualización:

1. Vaya al proveedor de servicios de Screens y seleccione **Visualizaciones** del panel de navegación izquierdo.

1. Haga clic en **Asignar canal** a la visualización.

   ![image](/help/screens-cloud/assets/display/assignchannel-1.png)

1. Rellene los campos siguientes desde **Asignar un canal** para abrir el Navegador.

   ![image](/help/screens-cloud/assets/display/assignchannel-2.png)

   1. Seleccione el nombre del canal en la lista desplegable.
   1. Elija la prioridad .

      >[!NOTE]
      >La prioridad se utiliza para solicitar las asignaciones en caso de que varias de ellas coincidan con los criterios de reproducción. Aquel elemento que tenga el valor más alto siempre tendrá prioridad sobre otros valores más bajos. Por ejemplo, si hay dos canales A y B, y A tiene una prioridad de 1 y B tiene una prioridad de 2, se muestra el canal B ya que tiene mayor prioridad que A.
   1. Seleccione la fecha de inicio y la de finalización desde **Activation**.

1. Haga clic en **+ Añadir recurrencia** para agregar una programación de periodicidad para el canal.

   ![image](/help/screens-cloud/assets/create-content/recurrence-1.png)

   >[!NOTE]
   >Puede agregar varias programaciones recurrentes al canal. Las programaciones de periodicidad introducen DayParting, que permite establecer una programación global con varios canales que se ejecutan en momentos específicos del día, y reutilizar esa configuración para todas las visualizaciones a la vez.

   Puede establecer las siguientes opciones:

   * **Nombre**: Título de la programación de periodicidad.
   * **Repetir**: Elija si la programación se ejecuta diariamente, semanalmente, mensualmente o anualmente.
   * **Inicio**: La hora de inicio de la programación.
   * **Fin**: La hora de finalización de la programación. Puede configurarlo por tiempo o duración.
   * **Tiempo**: La programación finalizará a una hora especificada.
   * **Duración**: La programación se ejecuta durante un tiempo determinado en horas o minutos.

1. Haga clic en **Crear** y ahora verá el que un canal está asignado para esa pantalla, como se muestra en la figura siguiente.

   ![image](/help/screens-cloud/assets/display/assignchannel-3.png)


## Siguientes pasos {#whats-next}

Ahora que ha asignado el canal a una pantalla, debe continuar con el recorrido as a Cloud Service de Screens revisando el documento [Instalación y configuración de Screens Player para AEM as a Cloud Service](/help/screens-cloud/managing-players-registration/installing-screens-cloud-player.md).
