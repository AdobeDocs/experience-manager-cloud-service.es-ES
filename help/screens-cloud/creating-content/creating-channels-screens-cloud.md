---
title: Creación y administración de canales en Screens as a Cloud Service
description: En esta página se describe cómo crear y administrar canales en Screens as a Cloud Service.
exl-id: 3b0bae7a-4a45-485a-ab04-604510ff6578
source-git-commit: 9db22dca0fd6debaff0d93e1958e59536efabad8
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 4%

---

# Creación y administración de un canal en Screens as a Cloud Service {#creating-channels-screens-cloud}

Una vez creado un proyecto de AEM Screens, debe crear los canales.
***Canales***, muestra una secuencia de contenido (imágenes y vídeos), un sitio web o una aplicación de una sola página.

## Objetivo {#objective}

Este documento le ayuda a comprender la creación y administración de canales para su proyecto de AEM Screens en el proveedor de contenido de Screens. Después de leer debe:

* comprender cómo crear canales para el proveedor de contenido de Screens
* administrar y editar contenido en los canales
* programación de activación para sus canales

## Pasos para crear un nuevo canal de secuencia en Screens as a Cloud Service {#create-new-channel}

>[!NOTE]
>**Requisitos previos**
>Antes de iniciar esta sección de la Guía, consulte [Creación y administración de proyectos en Screens as a Cloud Service](/help/screens-cloud/creating-content/creating-projects-screens-cloud.md).

Siga los pasos a continuación para crear un nuevo canal de secuencia en Screens as a Cloud Service:

1. Vaya al proveedor de contenido de Screens.

1. Vaya al proyecto de AEM Screens, como *FirstDigitalExperience*.

1. Seleccione el **Canales** de su proyecto, como **FirstDigitalExperience** —> **Canales** y haga clic en **Crear** de la barra de acciones.

   ![](/help/screens-cloud/assets/create-content/channel-create1.png)

1. Seleccione la plantilla como, por ejemplo, **Canal de secuencia** de la variable **Crear** asistente y haga clic en **Siguiente**.

   ![](/help/screens-cloud/assets/create-content/channel-create2.png)
   >[!NOTE]
   > La variable **Crear** proporciona diferentes tipos de plantillas al crear un canal. Consulte la sección [Plantillas disponibles](#available-templates) en Crear asistente para obtener más información.

1. Introduzca el nombre del canal de secuencia, como, por ejemplo, **BucleChannelOne** y haga clic en **Crear**.

   ![](/help/screens-cloud/assets/create-content/channel-create3.png)

   Ahora verá un **BucleChannelOne** en la carpeta Canales de su proyecto de AEM Screens.

   Una vez creado el canal, ahora puede añadir contenido al canal. Consulte [Adición de contenido a un canal](#add-content) para aprender a añadir recursos (imágenes/vídeos) al canal.

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
   >Haga clic en **Vista previa** para obtener una vista previa del contenido del canal.
   >![](/help/screens-cloud/assets/create-content/edit-channelpreview.png)

## Plantillas disponibles en el Asistente de creación {#available-templates}

Las siguientes plantillas están disponibles mientras se usa la variable **Crear** asistente de canales:

| Plantillas disponibles | Descripción |
|--- |--- |
| Carpeta de canales | Permite crear una carpeta para almacenar la colección de canales. |
| Canal de secuencia | Permite crear un canal que reproduzca los componentes de forma secuencial (uno por uno en una presentación con diapositivas). |
| Canal de pantalla dividida de barras L izquierda o derecha | Permite a los autores de contenido ver diferentes tipos de recursos en zonas de tamaño adecuado. |

## Usar detalles de asignación predeterminados para canales {#default-channels}

Esta capacidad le permite definir una programación de activación predeterminada para un canal y utilizarla de forma predeterminada para cada asignación para una pantalla. Esto proporciona un método para que no sea necesario repetir la engorrosa definición de la programación.

### Crear detalles de asignación predeterminados para un canal {#create-default}

1. Vaya a la página de detalles del canal que desea configurar.
1. Busque la variable **Detalles de asignación predeterminados** en la página.

   ![image](/help/screens-cloud/assets/display/Assignment1.png)

1. Haga clic en **Definir detalles predeterminados**.
1. Configure los detalles de asignación predeterminados, incluidas las fechas de prioridad, inicio y finalización, así como los patrones de periodicidad del canal, y haga clic en **Asignar**.

   ![image](/help/screens-cloud/assets/display/Assignments2.png)

1. Observe que los detalles de la asignación se muestran en el **Detalles de asignación predeterminados** mosaico:

   ![image](/help/screens-cloud/assets/display/Assignments3.png)

Este mosaico muestra la siguiente información:
* Prioridad predeterminada del canal en la pantalla.
* Fechas de inicio y finalización de la activación cuando el canal está programado para reproducirse.
* Vista sintética de la recurrencia (por hora/diario/semanal/mensual/anual, así como el nombre dado a esa recurrencia).

### Usar los detalles de asignación predeterminados al asignar a una pantalla {#default-display}

Los canales con detalles de asignación predeterminados se pueden asignar a muestra de la misma manera que los canales normales, con la opción añadida para aprovechar los detalles de asignación predeterminados en lugar de definir manualmente los personalizados cada vez.

1. Vaya a la página de detalles de visualización a la que desee asignar el canal y haga clic en el botón **Asignar canal**.
también puede seleccionar la visualización que desee en la vista de inventario y hacer clic en el botón **Asignar canal**.
1. Se abre el cuadro de diálogo de asignación de canal.

   ![image](/help/screens-cloud/assets/display/Assignments4.png)

1. Seleccione el canal que desee y que tenga los detalles de asignación predeterminados en el selector de canales.
1. Observe los cambios en el cuadro de diálogo de asignación de canal para que pueda elegir los detalles de asignación predeterminados o seleccionar los personalizados:

   ![image](/help/screens-cloud/assets/display/Assignments5.png)

1. Haga clic en **Asignar** para finalizar la asignación, o haga clic en **Definir detalles de asignación personalizados** si prefiere anular los valores predeterminados con otros valores en el contexto de esa visualización en particular.

   ![image](/help/screens-cloud/assets/display/Assignments6.png)

1. Observe que **Canales asignados** el mosaico se actualiza con la nueva asignación:

   ![image](/help/screens-cloud/assets/display/Assignments7.png)

1. Tenga en cuenta que los canales tendrán un icono diferente en función de si están utilizando programas personalizados (icono del reloj) o heredando los detalles predeterminados (icono del reloj del mundo), y al hacer clic en ellos se mostrarán los detalles de la programación.
1. Tenga en cuenta también que las acciones disponibles para cada tipo diferirán.

   ![image](/help/screens-cloud/assets/display/Assignments8.png)

**Nota:** Una asignación de canal que aprovecha los detalles de asignación predeterminados no se puede editar en el contexto de la visualización.

* Si necesita cambiarla a una asignación personalizada, primero deberá eliminarla y luego agregarla usando la variable **Definir detalles de asignación personalizados** .
* Si necesita cambiar las propiedades de los detalles de asignación predeterminados, tendrá que hacerlo directamente desde la página de detalles del canal.

### Eliminar los detalles de asignación predeterminados de un canal {#remove-display}

1. Vaya a la página de detalles del canal en el que desea eliminar los detalles de asignación predeterminados.
1. Busque la variable **Detalles de asignación predeterminados** mosaico en la página
1. Haga clic en el **Eliminar predeterminado**.

   ![image](/help/screens-cloud/assets/display/Assignments9.png)

1. Se mostrará un cuadro de diálogo de confirmación y los detalles coincidirán con una de las siguientes condiciones:
   **a.** El canal no se utiliza en ninguna pantalla.

   ![image](/help/screens-cloud/assets/display/Assignments10.png)

**b.** El canal se utiliza en una sola pantalla.

![image](/help/screens-cloud/assets/display/Assignment11.png)

**c.** El canal se utiliza en varias pantallas.

![image](/help/screens-cloud/assets/display/Assignments12.png)

1. Haga clic en el *Eliminar* para validar el cambio.

**Nota:** Al eliminar los detalles de asignación predeterminados de un canal, se eliminarán las asignaciones coincidentes de todas las pantallas que lo utilizaban.
Como consecuencia, esto puede llevar a pantallas en blanco si no hay contenido alternativo que reproducir en esas pantallas.

## Siguientes pasos {#whats-next}

Ahora que ha configurado un canal de AEM Screens en el proyecto, debe publicar el canal. Consulte [Canales de publicación en Screens as a Cloud Service](manage-publish.md) antes de administrar sus reproductores desde el proveedor de servicios de Screens.
