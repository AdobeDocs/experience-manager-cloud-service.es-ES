---
title: Administración de canalizaciones
description: Obtenga información sobre cómo administrar las canalizaciones existentes, como editarlas, ejecutarlas y eliminarlas.
index: true
exl-id: 4aff5a84-134a-43fa-8de8-8d564f4edd16
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 46%

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

## Ventana Canalizaciones {#pipelines}

El **Canalizaciones** La ventana muestra una lista completa de todas las canalizaciones para el programa seleccionado. Esto resulta útil, ya que presenta información más completa que la disponible en el [Tarjeta de canalización.](#pipeline-card)

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Desde el **Resumen del programa** página, toque o haga clic en **Canalizaciones** para cambiar a la pestaña **Canalizaciones** ventana.

1. Aquí puede ver una lista de todas las canalizaciones para el programa, así como iniciar y detener la ejecución de la canalización como lo haría en el **Tarjeta de canalizaciones**.

Si se está ejecutando una canalización, pase el ratón sobre su **Estado** La columna revelará detalles sobre la ejecución.

![Detalles de ejecución de canalización](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-status.png)

Toque o haga clic **Ver detalles** le llevará a la [detalles de la ejecución de la canalización.](#view-details)

## Ventana de actividad {#activity}

El **Actividades** La ventana muestra una lista completa de todas las ejecuciones de canalizaciones para el programa seleccionado.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Desde el **Resumen del programa** página, toque o haga clic en **Actividad** para cambiar a la pestaña **Actividad** ventana.

1. Aquí puede ver una lista de todas las ejecuciones de canalización del programa, incluidas las ejecuciones actuales e históricas.

Si se está ejecutando una canalización, pase el ratón sobre su **Estado** La columna revelará detalles sobre la ejecución.

![Detalles de ejecución de canalización](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-activity.png)

Toque o haga clic **Ver detalles** le llevará a la [detalles de la ejecución de la canalización.](#view-details)

## Ejecutar canalizaciones {#running-pipelines}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a **Canalizaciones** de la tarjeta de **Resumen del programa** y haga clic en el botón de los tres puntos situado junto a la canalización que ejecute, seleccione **Ejecutar** en el menú.

1. La ejecución de la canalización comienza y se indica con la columna **Estado**.

Para ver los detalles de la ejecución, vuelva a hacer clic en el botón de los tres puntos y seleccione **[Ver detalles.](#view-details)**

Según el tipo de canalización, puede cancelar la ejecución si hace clic de nuevo en el botón de los tres puntos y selecciona **Cancelar**.

## Editar canalizaciones {#editing-pipelines}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a **Canalizaciones** de la tarjeta de **Resumen del programa** y haga clic en el botón de los tres puntos situado junto a la canalización que desee editar y, a continuación, seleccione **Editar** en el menú.

1. El cuadro de diálogo **Editar canalización de producción** o **Editar canalización que no sea de producción** se mostrará y le permitirá editar los mismos detalles introducidos al crear la canalización.

   * Consulte las siguientes páginas para obtener más información sobre todos los campos y las opciones de configuración disponibles para las canalizaciones.
      * [Configurar canalizaciones de producción](configuring-production-pipelines.md)
      * [Configurar canalizaciones que no sean de producción](configuring-non-production-pipelines.md)

1. Clic **Actualizar** una vez que haya terminado de editar la canalización.

>[!NOTE]
>
>No se puede editar una canalización en ejecución.

## Eliminar canalizaciones {#deleting-pipelines}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a **Canalizaciones** de la tarjeta de **Resumen del programa** y haga clic en el botón de los tres puntos situado junto a la canalización que ejecute, seleccione **Eliminar** en el menú.

>[!NOTE]
>
>No se puede eliminar una canalización en ejecución.

## Ver detalles de canalización {#view-details}

Puede ver los detalles de una canalización para ver el estado y los registros de su última ejecución.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a **Canalizaciones** de la tarjeta de **Resumen del programa** y haga clic en el botón de los tres puntos situado junto a la canalización que ejecute, seleccione **Ver detalles** en el menú.

1. Se le redirigirá a la página de detalles de la canalización en ejecución.

![Detalles de canalización](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-running-details.png)

Desde aquí puede ver el estado de los distintos pasos de la canalización y recuperar los registros de generación con fines diagnósticos. Ver el documento [Implementar el código](/help/implementing/cloud-manager/deploy-code.md) para obtener más información sobre la implementación del código y la ejecución de pruebas.

Todos los pasos de la ejecución de una canalización se muestran con los que aún no se han iniciado atenuados. Los pasos finalizados muestran su duración.

Una vez completado el paso de una canalización, se presenta un resumen.

![Resumen del paso](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-step.png)

Haga clic o pulse en **Ver detalles** vínculo para mostrar el **Duración** sección. Esto incluye la duración promedio de la canalización en función de la tendencia histórica para ese programa.

![Duración](/help/implementing/cloud-manager/assets/configure-pipeline/duration.png)

>[!NOTE]
>
>Solo puede ver los detalles de una canalización que se esté ejecutando o que se haya ejecutado al menos una vez.

## Cancelar canalizaciones {#cancel}

Si una canalización se encuentra en la fase de validación o compilación de imagen, puede cancelar de forma segura la ejecución de la canalización.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. En la página de información general del programa, haga clic en el botón de los tres puntos de la canalización que desee cancelar en el **Canalizaciones** Tarjeta de.

   ![Cancelar una canalización](/help/implementing/cloud-manager/assets/cancel-pipeline.png)

1. Haga clic o pulse **Cancelar**.

También puede cancelar una canalización desde la página de detalles de la canalización.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a **Canalizaciones** de la pestaña **Resumen del programa** y toque o haga clic en la canalización que desee cancelar.

1. Se le redirigirá a la página de detalles de la canalización en ejecución.

   ![Cancelar detalles de canalización](/help/implementing/cloud-manager/assets/cancel-pipeline-details.png)

1. Haga clic o pulse **Cancelar**.
