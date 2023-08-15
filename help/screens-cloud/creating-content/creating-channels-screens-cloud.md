---
title: Creación y administración de canales en Screens as a Cloud Service
description: En esta página se describe cómo crear y administrar canales en Pantallas as a Cloud Service.
exl-id: 3b0bae7a-4a45-485a-ab04-604510ff6578
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 2%

---

# Creación y administración de un canal en Screens as a Cloud Service {#creating-channels-screens-cloud}

Una vez creado un proyecto de AEM Screens, debe crear canales.
***Canales***, mostrar una secuencia de contenido (imágenes y vídeos), un sitio web o una aplicación de una sola página.

## Objetivo {#objective}

Este documento le ayuda a comprender la creación y administración de canales para su proyecto de AEM Screens en el proveedor de contenido de Screens. Después de leerlo, debe hacer lo siguiente:

* Obtenga información sobre cómo crear canales para el proveedor de contenido de Screens
* administrar y editar contenido en sus canales
* programación de activación de sus canales

## Pasos para crear un nuevo canal de secuencia en Screens as a Cloud Service {#create-new-channel}

>[!NOTE]
>**Requisitos previos**
>Antes de comenzar esta sección de la Guía, revise lo siguiente [Creación y administración de proyectos en Pantallas as a Cloud Service](/help/screens-cloud/creating-content/creating-projects-screens-cloud.md).

Siga los pasos a continuación para crear un nuevo canal de secuencia en Pantallas as a Cloud Service:

1. Vaya al proveedor de contenido de Screens.

1. Vaya al proyecto de AEM Screens, como *FirstDigitalExperience*.

1. Seleccione el **Canales** carpeta del proyecto, como **FirstDigitalExperience** —> **Canales** y haga clic en **Crear** de la barra de acciones.

   ![channel-create1](/help/screens-cloud/assets/create-content/channel-create1.png)

1. Seleccione la plantilla, como, **Canal de secuencia** desde el **Crear** asistente y haga clic en **Siguiente**.

   ![channel-create2](/help/screens-cloud/assets/create-content/channel-create2.png)

   >[!NOTE]
   > El **Crear** El asistente proporciona diferentes tipos de plantillas al crear un canal. Consulte [Plantillas disponibles](#available-templates) en el Asistente de creación para obtener más información.

1. Introduzca el nombre del canal de secuencia, como, **BucleCanalUno** y haga clic en **Crear**.

   ![channel-create3](/help/screens-cloud/assets/create-content/channel-create3.png)

   Ahora verá una etiqueta **BucleCanalUno** en la carpeta Canales del proyecto de AEM Screens.

   Una vez creado el canal, ahora puede añadir contenido al canal. Consulte [Adición de contenido a un canal](#add-content) para obtener información sobre cómo añadir recursos (imágenes/vídeos) a su canal.

## Administración de un canal {#managing-channels}

Puede editar, ver las propiedades y el panel, copiar, previsualizar y eliminar un canal.

Navegue hasta el canal del proyecto y seleccione el canal, como se muestra en la figura siguiente. Ahora puede seleccionar las opciones, como editar el canal, ver propiedades, previsualizar contenido, administrar la publicación o eliminar el canal de la barra de acciones.

![channelprop1](/help/screens-cloud/assets/create-content/channelprop1.png)

### Adición de contenido a un canal {#add-content}

Para añadir o editar contenido en un canal, siga los pasos a continuación:

1. Seleccione el canal que desee editar, como se muestra en la figura siguiente. Haga clic en **Editar** desde la esquina superior izquierda de la barra de acciones para abrir el editor.

   ![edit-channel1](/help/screens-cloud/assets/create-content/edit-channel1.png)

1. El editor permite agregar recursos o componentes al canal que desee publicar.

1. Arrastre y suelte los recursos desde el panel lateral izquierdo y agréguelos al editor.

   ![edit-channel2](/help/screens-cloud/assets/create-content/edit-channel2.png)

   >[!NOTE]
   >Haga clic en **Previsualizar** para obtener una vista previa del contenido del canal.
   >![edit-channelpreview](/help/screens-cloud/assets/create-content/edit-channelpreview.png)

## Plantillas disponibles en el asistente de creación {#available-templates}

Las siguientes plantillas están disponibles mientras se utiliza la variable **Crear** asistente de canal:

| Plantillas disponibles | Descripción |
|--- |--- |
| Carpeta de canales | Permite crear una carpeta para almacenar una colección de canales. |
| Canal de secuencia | Permite crear un canal que reproduce los componentes secuencialmente (uno a uno en una presentación de diapositivas). |
| Canal de pantalla dividida de barra en L izquierda o derecha | Permite a los autores de contenido ver diferentes tipos de recursos en zonas de tamaño adecuado. |

## Usar los detalles de asignación predeterminados para los canales {#default-channels}

Esta capacidad permite definir una programación de activación predeterminada para un canal y utilizarla de forma predeterminada para cada asignación de una visualización. Esto proporciona un método para que no sea necesario repetir la engorrosa definición de programación.

### Crear detalles de asignación predeterminados para un canal {#create-default}

1. Vaya a la página de detalles del canal que desee configurar.
1. Busque el **Detalles de asignación predeterminados** mosaico en la página.

   ![imagen](/help/screens-cloud/assets/display/Assignment1.png)

1. Clic **Establecer detalles predeterminados**.
1. Configure los detalles de asignación predeterminados, incluidas las fechas de inicio y finalización y los patrones de periodicidad del canal, y haga clic en **Asignar**.

   ![imagen](/help/screens-cloud/assets/display/Assignments2.png)

1. Observe que los detalles de la asignación se muestran en la **Detalles de asignación predeterminados** mosaico:

   ![imagen](/help/screens-cloud/assets/display/Assignments3.png)

Este mosaico muestra la siguiente información:
* Prioridad predeterminada del canal en la visualización.
* Las fechas de inicio y finalización de la activación indican cuándo está programado que se reproduzca el canal.
* Vista sintética de la recurrencia (por hora/diario/semanal/mensual/anual y nombre dado a esa recurrencia).

### Utilizar los detalles de asignación predeterminados al asignar a una pantalla {#default-display}

Los canales con detalles de asignación predeterminados se pueden asignar a y muestran de la misma manera que los canales normales, con la opción añadida de utilizar los detalles de asignación predeterminados en lugar de definir manualmente los personalizados cada vez.

1. Vaya a la página de detalles de visualización a la que desee asignar el canal y haga clic en **Asignar canal**.
también puede seleccionar la visualización que desee en la vista de inventario y hacer clic en **Asignar canal**.
1. Se abrirá el cuadro de diálogo Asignación de canal.

   ![imagen](/help/screens-cloud/assets/display/Assignments4.png)

1. Seleccione el canal que tenga los detalles de asignación predeterminados en el selector de canales.
1. Observe los cambios del cuadro de diálogo de asignación de canal para permitirle elegir los detalles de asignación predeterminados o seleccionar los personalizados:

   ![imagen](/help/screens-cloud/assets/display/Assignments5.png)

1. Clic **Asignar** para finalizar la asignación, o haga clic en **Establecer detalles de asignación personalizados** si prefiere anular los valores predeterminados con otros valores en el contexto de esa visualización en particular.

   ![imagen](/help/screens-cloud/assets/display/Assignments6.png)

1. Observe el **Canales asignados** el mosaico se actualiza con la nueva asignación:

   ![imagen](/help/screens-cloud/assets/display/Assignments7.png)

1. Observe que los canales tienen un icono diferente en función de si utilizan programaciones personalizadas (icono del reloj) o heredan los detalles predeterminados (icono del reloj mundial) y al hacer clic en ellos se muestran los detalles de la programación.
1. Fíjese también en que las acciones disponibles para cada tipo serán diferentes.

   ![imagen](/help/screens-cloud/assets/display/Assignments8.png)

**Nota:** Una asignación de canal que utilice los detalles de asignación predeterminados no se podrá editar en el contexto de la visualización.

* Si debe cambiarla a una asignación personalizada, primero elimínela y, a continuación, agréguela de nuevo mediante el **Establecer detalles de asignación personalizados** opción.
* Si debe cambiar las propiedades de los detalles de asignación predeterminados, hágalo directamente desde la página de detalles del canal.

### Quitar los detalles de asignación predeterminados de un canal {#remove-display}

1. Vaya a la página de detalles del canal en el que desee eliminar los detalles de asignación predeterminados.
1. Busque el **Detalles de asignación predeterminados** mosaico en la página
1. Haga clic en **Quitar predeterminado**.

   ![imagen](/help/screens-cloud/assets/display/Assignments9.png)

1. Se muestra un cuadro de diálogo de confirmación y los detalles coinciden con una de las siguientes condiciones:
   **a.** El canal no se utiliza en ninguna visualización.

   ![imagen](/help/screens-cloud/assets/display/Assignments10.png)

**b.** El canal se utiliza en una sola pantalla.

![imagen](/help/screens-cloud/assets/display/Assignment11.png)

**c.** El canal se utiliza en varias pantallas.

![imagen](/help/screens-cloud/assets/display/Assignments12.png)

1. Haga clic en *Eliminar* para validar el cambio.

**Nota:** Si se eliminan los detalles de asignación predeterminados de un canal, se eliminarán las asignaciones coincidentes en todas las pantallas que lo utilizaban.
Como consecuencia, esto puede generar pantallas en blanco si no hay contenido alternativo para reproducir en esas pantallas.

## Siguientes pasos {#whats-next}

Ahora que ha configurado un canal de AEM Screens en el proyecto, debe publicar el canal. Consulte [Publicación de canales en Screens as a Cloud Service](manage-publish.md) antes de administrar los reproductores desde el proveedor de servicios de Screens.
