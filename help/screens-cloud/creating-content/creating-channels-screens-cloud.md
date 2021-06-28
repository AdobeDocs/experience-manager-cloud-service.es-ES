---
title: Creación y administración de canales en Screens as a Cloud Service
description: En esta página se describe cómo crear y administrar canales en Screens como Cloud Service.
source-git-commit: b9b27c09b1f4a1799a8c974dfb846295664be998
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 7%

---


# Creación y administración de canales en Screens as a Cloud Service {#creating-channels-screens-cloud}

Una vez creado un proyecto de AEM Screens, debe crear los canales.
***Los canales*** muestran una secuencia de contenido (imágenes y vídeos), un sitio web o una aplicación de una sola página.

## Objetivo {#objective}

Este documento le ayuda a comprender la creación y administración de canales para su proyecto de AEM Screens en el proveedor de contenido de Screens. Después de leer debe:

* comprender cómo crear canales para el proveedor de contenido de Screens
* administrar y editar contenido en los canales

## Pasos para crear un nuevo canal de secuencia en Screens como Cloud Service {#create-new-channel}

>[!NOTE]
>**Requisitos previos**
>Antes de iniciar esta sección de la Guía, revise [Creación y administración de proyectos en Screens como Cloud Service](/help/screens-cloud/creating-content/creating-projects-screens-cloud.md).

Siga los pasos a continuación para crear un nuevo canal de secuencia en Screens as a Cloud Service:

1. Vaya al proveedor de contenido de Screens.

1. Vaya al proyecto de AEM Screens, como *FirstDigitalExperience*.

1. Seleccione la carpeta **Channels** de su proyecto, como **FirstDigitalExperience** —> **Channels** y haga clic en **Crear** en la barra de acciones.

   ![](/help/screens-cloud/assets/create-content/channel-create1.png)

1. Seleccione la plantilla, como **Sequence Channel** en el asistente **Create** y haga clic en **Next**.

   ![](/help/screens-cloud/assets/create-content/channel-create2.png)
   >[!NOTE]
   > El asistente **Crear** proporciona diferentes tipos de plantillas al crear un canal. Consulte la sección [Plantillas disponibles](#available-templates) en el Asistente de creación para obtener más información.

1. Introduzca el nombre del canal de la secuencia, como **LoopingChannelOne** y haga clic en **Create**.

   ![](/help/screens-cloud/assets/create-content/channel-create3.png)

   Ahora verá **LoopingChannelOne** en la carpeta Canales de su proyecto de AEM Screens.

   Una vez creado el canal, ahora puede añadir contenido al canal. Consulte [Adición de contenido a un canal](#add-content) para obtener información sobre cómo añadir recursos (imágenes/vídeos) al canal.

## Administración de un canal {#managing-channels}

Puede editar, ver las propiedades y el panel, y copiar, acceder a la vista previa y eliminar un canal.

Vaya al canal del proyecto y seleccione el canal, como se muestra en la figura siguiente. Ahora puede seleccionar las opciones, como editar el canal, ver las propiedades, previsualizar el contenido, administrar la publicación o eliminar el canal de la barra de acciones.

![](/help/screens-cloud/assets/create-content/channelprop1.png)

### Adición de contenido a un canal {#add-content}

Para añadir o editar contenido en un canal, siga los pasos que se indican a continuación:

1. Seleccione el canal que desee editar, como se muestra en la figura siguiente. Haga clic en **Editar** en la esquina superior izquierda de la barra de acciones para abrir el editor.

   ![](/help/screens-cloud/assets/create-content/edit-channel1.png)

1. El editor le permite añadir recursos o componentes al canal que desea publicar.

1. Arrastre y suelte los recursos del panel izquierdo y agréguelos al editor.

   ![](/help/screens-cloud/assets/create-content/edit-channel2.png)

   >[!NOTE]
   >Haga clic en **Preview** para previsualizar el contenido del canal.
   >![](/help/screens-cloud/assets/create-content/edit-channelpreview.png)

## Plantillas disponibles en el Asistente de creación {#available-templates}

Las siguientes plantillas están disponibles mientras se utiliza el asistente de canal **Create**:

| Plantillas disponibles | Descripción |
|--- |--- |
| Carpeta de canales | Permite crear una carpeta para almacenar la colección de canales. |
| Canal de secuencia | Permite crear un canal que reproduzca los componentes de forma secuencial (uno por uno en una presentación con diapositivas). |
| Canal de pantalla dividida de barras L izquierda o derecha | Permite a los autores de contenido ver diferentes tipos de recursos en zonas de tamaño adecuado. |


## Siguientes pasos {#whats-next}

Ahora que ha configurado un canal de AEM Screens en el proyecto, debe publicar el canal. Consulte [Publicación de canales en Screens como Cloud Service](/help/screens-cloud/creating-content/manage-publish.md) antes de administrar los reproductores desde el proveedor de servicios de Screens.