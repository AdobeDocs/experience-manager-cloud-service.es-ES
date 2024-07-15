---
title: Publicación de un canal en Screens as a Cloud Service
description: En esta página se describe cómo publicar un canal en Screens as a Cloud Service.
exl-id: a69086d2-777c-4a94-bd22-5c02f98bbedb
feature: Authoring Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 1%

---

# Publicación de canales en Screens as a Cloud Service {#publish-channel-screens-cloud}

## Introducción {#introduction}

Puede publicar contenido desde AEM Screens. La función Administrar publicación permite enviar actualizaciones de contenido del autor a la publicación del reproductor. Puede publicar o cancelar la publicación del contenido de todo el proyecto de AEM Screens o solo de uno de los canales, la ubicación, el reproductor o una aplicación.

>[!IMPORTANT]
>Después de crear el canal o los canales en el proyecto, es obligatorio publicar los canales para mostrar el canal o los canales en la vista de lista de inventario en el proveedor de servicios de AEM Screens.

## Objetivo {#objective}

Este documento le ayuda a comprender la publicación del contenido editado en el proveedor y reproductor de Screens Services. Después de leerlo, debe ser capaz de:

* saber cómo publicar un canal
* administrar publicación, en términos de ámbito

## Pasos para configurar Publish como canal {#publish-channel}

Siga los pasos a continuación para publicar el canal:

1. Desplácese y seleccione el canal de su proyecto, como **FirstDigitalExperience** —> **Canales** —> **LoopingChannelOne**.

   ![Seleccionar canal](/help/screens-cloud/assets/create-content/managepub-1.png)

1. Haga clic en **Administrar publicación** en la barra de acciones.

1. Seleccione **Action** como **Publish** y **Scheduling** como **Now** del **asistente para administrar publicación** y haga clic en **Next**.

   ![Seleccionar acción de Publish](/help/screens-cloud/assets/create-content/managepub-2.png)

   >[!NOTE]
   >Haga clic en **Incluir elementos secundarios** en la barra de acciones, desmarque todas las opciones para publicar todos los módulos del proyecto y haga clic en Agregar para publicar. De forma predeterminada, todas las casillas están marcadas y debe desmarcar manualmente las casillas para publicar todos los módulos del proyecto.

1. Después de seleccionar el canal en el asistente de **Administrar publicación**, haz clic en **Publish** para publicar el canal.

   ![Publish en el canal](/help/screens-cloud/assets/create-content/managepub-3.png)


## Siguientes pasos {#whats-next}

Ahora que ha publicado sus canales en el proyecto, debería continuar con su as a Cloud Service recorrido de Screens revisando el documento [Instalación y configuración de reproductores en Screens as a Cloud Service](/help/screens-cloud/managing-players-registration/installing-screens-cloud-player.md).
