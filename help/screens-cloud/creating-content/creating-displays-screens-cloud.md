---
title: Creación y administración de pantallas en Screens as a Cloud Service
description: En esta página se describe cómo crear y administrar pantallas en Screens as a Cloud Service.
exl-id: 0f9faa4b-b50e-40f8-a8ed-280f8bd0a9b8
feature: Authoring Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 3%

---

# Creación y administración de pantallas en Screens as a Cloud Service {#create-displays-screens-cloud}

Una vez publicado el canal, es hora de crear la visualización en el proveedor de servicios de Screens.

Una pantalla es una agrupación virtual de pantallas que normalmente se colocan una al lado de la otra. La pantalla suele ser permanente con respecto a una instalación. Este contenido de objeto es con lo que los autores trabajan y siempre se refieren como visualización lógica en lugar de sus partes de contador físicas.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo crear y administrar pantallas en el proveedor de servicios de Screens. Después de leer, debería haber logrado lo siguiente:

* Obtenga información sobre cómo crear y eliminar pantallas
* Obtenga información sobre cómo organizar las pantallas en carpetas

## Pasos para crear una pantalla {#create-display}

Siga los pasos a continuación para crear la visualización desde el proveedor de servicios de Screens:

1. Vaya al proveedor de servicios de Screens desde la instancia de AEM Cloud Service.
1. Seleccione **Pantallas** en el panel de navegación izquierdo y haga clic en **Crear** en la esquina superior derecha de la pantalla.

   ![imagen](/help/screens-cloud/assets/display/disp-1.png)

1. Seleccione **Mostrar** en la barra de acciones.

   ![imagen](/help/screens-cloud/assets/display/disp-2.png)

1. Escriba el título como **LoopingChannelDisplay** en **Display Name** y haga clic en **Crear**.

   ![imagen](/help/screens-cloud/assets/display/disp3.png)

1. La pantalla con el título **LoopingChannelDisplay** ahora estará visible en la lista de visualización.

   ![imagen](/help/screens-cloud/assets/display/disp-4.png)

### Eliminación de una visualización {#deleting-display}

Puede eliminar una visualización del proveedor de servicios de Screens.

Seleccione la pantalla y haga clic en **Eliminar** desde la parte inferior del panel, como se muestra en la figura siguiente.

![imagen](/help/screens-cloud/assets/display/disp-5.png)

## Pasos para organizar las pantallas en carpetas {#organize-display}

## Cómo alternar el carril de la carpeta {#toggle-rail}

Puede cambiar el carril de la carpeta para que no muestre todas las carpetas a carpetas específicas:

1. Navegue hasta la vista de inventario de pantallas haciendo clic en el botón resaltado a continuación:

   ![imagen](/help/screens-cloud/assets/display/display-inventory.png)

1. Se muestra el carril lateral de la carpeta.

   ![imagen](/help/screens-cloud/assets/display/toggle-rail.png)

1. Seleccione **Ocultar carpetas** para cerrarlo de nuevo.

## Cómo crear una carpeta {#create-folder}

Puede crear carpetas para organizar mejor las pantallas.

1. Navegue hasta la vista de inventario de pantallas.
1. Asegúrese de que no está actualmente en una carpeta y vea lo siguiente:

   ![imagen](/help/screens-cloud/assets/display/verify-view.png)

   Nota: **Todas las pantallas** deben estar seleccionadas en el carril lateral de la carpeta y la navegación por la ruta de exploración solo debe mostrar **Pantallas**.

1. Haga clic en el botón &quot;Crear&quot; en la parte superior derecha y seleccione la opción **Carpeta**.

   ![imagen](/help/screens-cloud/assets/display/Createfolder.png)

1. Rellene el título de la nueva carpeta y haga clic en **Crear**.

   ![imagen](/help/screens-cloud/assets/display/Createfolder2.png)

## Cómo crear una carpeta anidada {#nested-folder}

1. Navegue hasta la vista de inventario de pantallas.

1. Seleccione la carpeta principal que desee en el carril lateral de la carpeta o en la vista de inventario.
1. Compruebe que la carpeta principal deseada está seleccionada.

   ![imagen](/help/screens-cloud/assets/display/Nestedview.png)

   * La carpeta debe estar seleccionada en el carril lateral de la carpeta.
   * La navegación de ruta de exploración debería mostrar el nombre de la carpeta actual junto a **Pantallas**.

1. Haga clic en **Crear** en la parte superior derecha y seleccione la opción **Carpeta**.

   ![imagen](/help/screens-cloud/assets/display/Createfolder.png)

1. Rellene el título de la nueva carpeta y haga clic en **Crear**.

   ![imagen](/help/screens-cloud/assets/display/Createfolder2.png)

## Cómo mover contenido a una carpeta nueva {#move-folder}

Puede mover contenido a sus nuevas carpetas para organizar mejor las pantallas.

1. Navegue hasta la vista de inventario de pantallas.

1. Seleccione la carpeta principal que desee en el carril lateral de la carpeta o en la vista de inventario.

1. Compruebe que ha seleccionado la carpeta principal deseada.

![imagen](/help/screens-cloud/assets/display/movetofolder.png)

**Nota**: la carpeta debe estar seleccionada en el carril lateral de la carpeta. Además, la exploración de la ruta de exploración debe mostrar el nombre de la carpeta actual junto a **Pantallas**.

## Eliminación de contenido de una carpeta {#delete-folder}

Se puede acceder a todas las operaciones de carpeta a través de la barra de acciones de selección en la vista de inventario.

1. Vaya a la carpeta principal o selecciónela en el carril lateral.

1. En la vista de inventario, seleccione la carpeta secundaria que desee eliminar y asegúrese de que esté vacía.

1. Haga clic en la acción **Eliminar** en la barra de acciones de selección. La acción se desactiva si la carpeta no está vacía.


## Siguientes pasos {#whats-next}

Ahora que ha aprendido a crear y administrar pantallas para su proyecto, debe continuar con su as a Cloud Service recorrido de Screens revisando el documento [Asignación de canales a una pantalla en Screens as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/create-content/assigning-channels-to-display.html?lang=es).
