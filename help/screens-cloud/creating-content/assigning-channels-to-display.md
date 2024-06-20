---
title: Asignación de canales a una pantalla en Pantallas as a Cloud Service
description: En esta página se describe cómo asignar un canal a una visualización en Pantallas as a Cloud Service.
exl-id: ba001c18-7b05-4ae2-aa7f-9ebb320fedd0
feature: Authoring Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 2%

---

# Asignación de canales a una pantalla en Pantallas as a Cloud Service {#assign-channel-displays-screens-cloud}

Una vez completada la configuración del proyecto, debe asignar el canal a una pantalla para ver el contenido.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo asignar un canal a una pantalla, una vez que la pantalla está lista y ha agregado contenido al canal y lo ha publicado. Después de leerlo, debería saber cómo asignar un canal a una visualización desde el proveedor de servicios de Screens.

## Requisitos previos {#prerequisites}

Antes de realizar los pasos siguientes para asignar un canal a una pantalla, debe haber terminado el aprendizaje:

* Creación y administración de pantallas
* Creación y administración de canales

## Pasos para asignar un canal a una pantalla {#assign-channel-to-display}

Siga los pasos a continuación para asignar un canal a una visualización:

1. Vaya al proveedor de servicios de Screens y seleccione **Visualizaciones** en el panel de navegación izquierdo.

1. Clic **Asignar canal** a la pantalla.

   ![imagen](/help/screens-cloud/assets/display/assignchannel-1.png)

1. Rellene los campos siguientes desde **Asignar un canal** Cuadro de diálogo.

   ![imagen](/help/screens-cloud/assets/display/assignchannel-2.png)

   1. Seleccione el nombre del canal en la lista desplegable.
   1. Elija la prioridad.

      >[!NOTE]
      >La prioridad se usa para ordenar las asignaciones en caso de que varias coincidan con los criterios de reproducción. El que tiene el valor más alto siempre tiene prioridad sobre los valores más bajos. Por ejemplo, si hay dos canales, A y B. A tiene una prioridad de 1 y B tiene una prioridad de 2. A continuación, se muestra el canal B, ya que tiene una prioridad mayor que A.

   1. Seleccione la fecha de inicio y la fecha de finalización desde **Activation**.

1. Clic **+ Agregar periodicidad** para añadir una programación de periodicidad para el canal.

   ![imagen](/help/screens-cloud/assets/create-content/recurrence-1.png)

   >[!NOTE]
   >Puede agregar varias programaciones recurrentes al canal. Las programaciones de periodicidad introducen DayParting, que permite establecer una programación global con varios canales ejecutándose a horas específicas del día y reutilizar esa configuración para todas las pantallas a la vez.

   Puede establecer las siguientes opciones:

   * **Nombre**: Título de la programación de periodicidad.
   * **Repetir**: Seleccione si la programación se ejecuta diariamente, semanalmente, mensualmente o anualmente.
   * **Inicio**: la hora de inicio de la programación.
   * **Fin**: la hora de finalización de la programación. Puede establecerlo por tiempo o duración.
   * **Hora**: la programación finaliza a una hora especificada.
   * **Duración**: la programación se ejecuta durante un período de tiempo determinado en horas o minutos.

1. Haga clic en **Crear**. Puede ver que hay un canal asignado para esa visualización, como se muestra en la figura siguiente.

   ![imagen](/help/screens-cloud/assets/display/assignchannel-3.png)


## Siguientes pasos {#whats-next}

Ahora que ha asignado el canal a una pantalla, debe continuar con el recorrido as a Cloud Service de Screens revisando el documento a continuación [AEM as a Cloud Service Instalación y configuración del reproductor de Screens para su uso en](/help/screens-cloud/managing-players-registration/installing-screens-cloud-player.md).
