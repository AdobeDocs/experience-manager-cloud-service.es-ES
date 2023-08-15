---
title: Administración de canalizaciones
description: Obtenga información sobre cómo administrar las canalizaciones existentes, como editarlas, ejecutarlas y eliminarlas.
index: true
exl-id: 4aff5a84-134a-43fa-8de8-8d564f4edd16
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 97%

---

# Administración de canalizaciones {#managing-pipelines}

Obtenga información sobre cómo administrar las canalizaciones existentes, como editarlas, ejecutarlas y eliminarlas.

## Tarjeta de canalización {#pipeline-card}

La tarjeta **Canalizaciones** de la página **Información general del programa** en Cloud Manager le ofrece una descripción general de todas sus canalizaciones y de su estado actual.

![Tarjeta de canalización en Cloud Manager](/help/implementing/cloud-manager/assets/configure-pipeline/pipelines-card.png)

Al hacer clic en el botón de los tres puntos situado junto a cada canalización, puede realizar las siguientes acciones.

* [Ejecutar la canalización](#running-pipelines)
* [Editar la canalización](#editing-pipelines)
* [Eliminar la canalización](#deleting-pipelines)
* [Ver detalles](#view-details)

En la parte inferior de la lista de canalizaciones, tiene opciones generales.

* **Agregar**: [Agrega una nueva canalización de producción](configuring-production-pipelines.md) o [una nueva canalización que no sea de producción](configuring-non-production-pipelines.md)
* **Mostrar todo**: Lleva al usuario a la pantalla Canalizaciones para ver todas las canalizaciones en una tabla más detallada.
* **Acceder a la info del repositorio**: Muestra la información necesaria para acceder al repositorio de Git de Cloud Manager
* **Más información**: Navega hasta los recursos de documentación de canalización de CI/CD.

## Ejecutar canalizaciones {#running-pipelines}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Navegue hasta la tarjeta **Canalizaciones** de la página **Información general del programa** y haga clic en el botón de los tres puntos situado junto a la canalización que ejecute, seleccione **Ejecutar** del menú.

1. La ejecución de la canalización comienza y se indica con la columna **Estado**.

Para ver los detalles de la ejecución, vuelva a hacer clic en el botón de los tres puntos y seleccione **[Ver detalles.](#view-details)**

Según el tipo de canalización, puede cancelar la ejecución si hace clic de nuevo en el botón de los tres puntos y selecciona **Cancelar**.

## Editar canalizaciones {#editing-pipelines}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Navegue hasta la tarjeta **Canalizaciones** de la página **Información general del programa**, haga clic en el botón de los tres puntos situado junto a la canalización que desee editar y, a continuación, seleccione **Editar** del menú.

1. El cuadro de diálogo **Editar canalización de producción** o **Editar canalización que no sea de producción** se mostrará y le permitirá editar los mismos detalles introducidos al crear la canalización.

   * Consulte las siguientes páginas para obtener más información sobre todos los campos y las opciones de configuración disponibles para las canalizaciones.
      * [Configurar canalizaciones de producción](configuring-production-pipelines.md)
      * [Configurar canalizaciones que no sean de producción](configuring-non-production-pipelines.md)

1. Haga clic en **Actualizar** cuando haya terminado de editar la canalización.

>[!NOTE]
>
>No se puede editar una canalización en ejecución.

## Eliminar canalizaciones {#deleting-pipelines}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Navegue hasta la tarjeta **Canalizaciones** de la página **Información general del programa** y haga clic en el botón de los tres puntos situado junto a la canalización que ejecute, seleccione **Eliminar** del menú.

>[!NOTE]
>
>No se puede eliminar una canalización en ejecución.

## Ver detalles {#view-details}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Navegue hasta la tarjeta **Canalizaciones** de la página **Información general del programa** y haga clic en el botón de los tres puntos situado junto a la canalización que ejecute, seleccione **Ver detalles** del menú.

1. Se le redirigirá a la página de detalles de la canalización en ejecución.

![Detalles de canalización](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-running-details.png)

Desde aquí puede ver el estado de los distintos pasos de la canalización y recuperar los registros de generación con fines diagnósticos. Consulte el documento [Implementar el código](/help/implementing/cloud-manager/deploy-code.md) para obtener más información.

>[!NOTE]
>
>Solo puede ver los detalles de una canalización que se esté ejecutando o que se haya ejecutado al menos una vez.
