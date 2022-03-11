---
title: Información general de Live Copy
description: Obtenga información sobre los conceptos básicos de la consola de información general de Live Copy para comprender rápidamente el estado de las Live Copies y sincronizar el contenido.
feature: Multi Site Manager
role: Admin
exl-id: 3ef7fbce-10a1-4b21-8486-d3c3706e537c
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 2%

---

# Información general de Live Copy {#live-copy-overview-console}

La variable **Información general de Live Copy** console le permite:

* Ver/administrar la herencia en un sitio.
   * Ver el árbol de modelo y la estructura correspondiente de Live Copy, junto con su estado de herencia
   * Cambiar el estado de herencia, como suspender y reanudar
   * Ver propiedades de modelo y Live Copy
* Realice acciones de despliegue.

## Información general sobre la apertura de Live Copy {#opening-the-live-copy-overview}

Puede abrir la Información general de Live Copy desde:

* [Panel lateral Referencias de una página de modelo (consola Sitios)](#opening-live-copy-overview-references-for-a-blueprint-page)
* [Propiedades de una página de modelo](#opening-live-copy-overview-properties-of-a-blueprint-page)

### Referencias a una página de modelo {#references-to-a-blueprint-page}

La variable **Información general de Live Copy** se puede abrir desde el **Referencias** panel lateral del **Sitios** consola:

1. En el **Sitios** consola, [vaya a la página de modelo y selecciónela.](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)
1. Abra el **[Referencias](/help/sites-cloud/authoring/getting-started/basic-handling.md#references)** carril y seleccione **Live Copies**.

   ![Live Copy desde el carril de referencias](../assets/live-copy-references.png)

   >[!TIP]
   >
   >También puede abrir primero las referencias y, a continuación, seleccionar el modelo.

1. Select **Información general de Live Copy** para mostrar y utilizar la descripción general de todas las Live Copies relacionadas con el modelo seleccionado.
1. Uso **Cerrar** para salir y volver al **Sitios** consola.

### Propiedades de una página de modelo {#properties-of-a-blueprint-page}

La variable **Información general de Live Copy** se puede abrir al ver las propiedades de una página de modelo:

1. Apertura **Propiedades** para la página de modelo adecuada.
1. Abra el **Modelo** pestaña : **Información general de Live Copy** se mostrará en la barra de herramientas superior:

   ![Ficha Propiedades del modelo](../assets/live-copy-blueprint-tab.png)

1. Select **Información general de Live Copy** para mostrar y utilizar la descripción general de todas las Live Copies relacionadas con el modelo actual.

1. Uso **Cerrar** para salir y volver al **Sitios** consola.

## Información general sobre el uso de Live Copy {#using-the-live-copy-overview}

La variable **Información general de Live Copy** proporciona información general sobre el estado de las Live Copies relacionadas con la página seleccionada.

![Ventana Información general de Live Copy](../assets/live-copy-overview.png)

Un despliegue depende de las acciones de sincronización definidas en la configuración específica del despliegue. Algunas acciones dependen de las modificaciones del contenido. Sin embargo, también hay muchas acciones que no dependen de las modificaciones del contenido, sino que dependen de eventos como la activación de páginas. Estos eventos no modifican el contenido, pero sí las propiedades internas relacionadas con el contenido.

Los campos de estado también dependen de las acciones de sincronización definidas en la configuración de lanzamiento específica e indican si ha habido alguna acción de este tipo en el modelo o en Live Copy desde la última implementación correcta. Un campo de estado solo reflejará las acciones de la configuración específica del despliegue. Si nunca se ha realizado una implementación correcta en una Live Copy, el estado siempre se mostrará actualizado.

Por ejemplo, una configuración de lanzamiento se define como `targetActivate`. Por lo tanto, el despliegue dependerá únicamente de los eventos de activación. El campo de estado solo indica si se ha producido algún evento de activación desde la última vez que se implementó correctamente.

La variable **Información general de Live Copy** también se puede utilizar para realizar acciones en Live Copy:

1. Abra el **Información general de Live Copy**.
1. Seleccione el modelo necesario o la página Live Copy y la barra de herramientas se actualizará para mostrar las acciones disponibles. La variable [acciones](overview.md#terms-used) disponible dependen de si selecciona un [modelo](#actions-for-a-blueprint-page) o [Live Copy](#actions-for-a-live-copy-page) página.

### Acciones para una página de modelo {#actions-for-a-blueprint-page}

Cuando selecciona una página de modelo, están disponibles las siguientes acciones:

![Acciones de información general de Live Copy para un modelo](../assets/live-copy-overview-actions-blueprint.png)

* **Editar** - Abra la página de modelo para editarla.
* **[Despliegue](overview.md#rollout-and-synchronize)** - Realice un despliegue para insertar los cambios del origen en Live Copy.

### Acciones para una página de Live Copy {#actions-for-a-live-copy-page}

Cuando selecciona una página de Live Copy, están disponibles las siguientes acciones:

![Acciones de información general de Live Copy para una Live Copy](../assets/live-copy-overview-actions.png)

* **Editar** - Abra la página Live Copy para editarla.
* **[Estado de la relación](#relationship-status)** - Vea información sobre el estado y la herencia.
* **[Sincronizar](overview.md#rollout-and-synchronize)** - Sincronice una Live Copy para extraer cambios del origen a Live Copy.
* **[Restablecer](creating-live-copies.md#resetting-a-live-copy-page)** - Restablezca una página de Live Copy para eliminar todas las cancelaciones de herencia y devuelva la página al mismo estado que la página de origen.
* **[Suspender](overview.md#suspending-and-cancelling-inheritance-and-synchronization)** - Desactiva temporalmente la relación activa entre una Live Copy y su página de modelo.
* **[Reanudar](creating-live-copies.md#resuming-inheritance-for-a-page)** - Reanudar le permite restablecer una relación suspendida.
* **[Desasociar](overview.md#detaching-a-live-copy)** : elimina de forma permanente la relación activa entre una Live Copy y su página de modelo.

## Estado de la relación {#relationship-status}

La variable **Estado de la relación** tiene dos fichas que proporcionan una amplia gama de funciones.

* [Estado de la relación](#relationship-status-tab)
* [Live Copy   ](#live-copy-tab)

### Estado de la relación {#relationship-status-tab}

Esta pestaña proporciona información detallada sobre el estado de la relación entre el modelo y Live Copy.

![Ficha Estado de relación](../assets/live-copy-relationship-status.png)

### Live Copy    {#live-copy-tab}

Esta pestaña le permite ver y editar la configuración de Live Copy.

![Ficha Live Copy](../assets/live-copy-relationship-status-live-copy.png)
