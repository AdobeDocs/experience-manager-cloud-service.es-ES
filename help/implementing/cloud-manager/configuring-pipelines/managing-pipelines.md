---
title: Administración de canalizaciones
description: Obtenga información sobre cómo administrar las canalizaciones existentes, como editarlas, ejecutarlas y eliminarlas.
index: true
exl-id: 4aff5a84-134a-43fa-8de8-8d564f4edd16
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 500e1b78fb9688601848fc17f312fc23be83bcb0
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 70%

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

## Ventana de canalizaciones {#pipelines}

La ventana **Canalizaciones** muestra una lista completa de todas las canalizaciones para el programa seleccionado. Esto resulta útil, ya que presenta información más completa que la disponible en la [Tarjeta de canalizaciones](#pipeline-card).

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.

1. En la página **Resumen del programa**, seleccione la pestaña **Canalizaciones** para cambiar a la ventana **Canalizaciones**.

1. Aquí puede ver una lista de todas las canalizaciones para el programa, así como iniciar y detener la ejecución de la canalización como lo haría en la **Tarjeta de canalizaciones**.

Si se está ejecutando una canalización, al hacer clic en el icono de información en la columna **Estado** se muestran detalles sobre la ejecución.

![Detalles de ejecución de canalización](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-status.png)

Hacer clic en **Ver detalles** le llevará a los [detalles de la ejecución de la canalización](#view-details).

También puede hacer clic en el botón de los tres puntos de la canalización para realizar acciones adicionales apropiadas para el estado de la canalización, como [editarla](#editing-pipelines) o [cancelar la ejecución](#cancel).

![Acciones de canalización](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-actions.png)

## Ventana de actividad {#activity}

La ventana **Activity** muestra una lista completa de todas las ejecuciones de canalizaciones para el programa seleccionado, así como otros eventos de programa importantes.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. En la página **Información general del programa**, seleccione la pestaña **Actividad** para cambiar a la ventana **Actividad**.

1. Aquí puede ver una lista de todas las ejecuciones de canalización del programa, incluidas las ejecuciones actuales e históricas.

Si se está ejecutando una canalización, al hacer clic en el icono de información en la columna **Estado** se mostrarán los detalles sobre la ejecución.

![Detalles de ejecución de canalización](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-activity.png)

Al tocar o hacer clic en la fila que representa la ejecución de la canalización, se le dirigirán [detalles de la ejecución de la canalización](#view-details).

También puede hacer clic en el botón de los tres puntos para realizar más acciones en la ejecución de la canalización, como ver sus detalles o descargar el registro, que le lleva a la [página de detalles de la canalización](#view-details).

![Acciones de ejecución de canalización](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-execution-actions.png)

## Ejecutar canalizaciones {#running-pipelines}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Navegue hasta la tarjeta **Canalizaciones** de la página **Información general del programa** y haga clic en el botón de los tres puntos situado junto a la canalización que ejecute, seleccione **Ejecutar** en el menú.

1. La ejecución de la canalización comienza y se indica con la columna **Estado**.

Para ver los detalles de la ejecución, vuelva a hacer clic en el botón de los tres puntos y seleccione **[Ver detalles](#view-details)**.

Según el tipo de canalización, puede cancelar la ejecución si hace clic de nuevo en el botón de los tres puntos y selecciona **Cancelar**.

## Edición de una canalización {#editing-pipelines}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a la tarjeta **Canalizaciones** de la página **Resumen del programa** y haga clic en el botón de puntos suspensivos situado junto a la canalización que quiere editar y seleccione **Editar** en el menú.

1. El cuadro de diálogo **Editar canalización de producción** o **Editar canalización que no sea de producción** se mostrará y le permitirá editar los mismos detalles introducidos al crear la canalización.

   * Consulte las siguientes páginas para obtener más información sobre los campos y las opciones de configuración disponibles para las canalizaciones.
      * [Configurar canalizaciones de producción](configuring-production-pipelines.md)
      * [Configurar canalizaciones que no sean de producción](configuring-non-production-pipelines.md)

1. Haga clic en **Actualizar** una vez que haya terminado de editar la canalización.

>[!NOTE]
>
>No se puede editar una canalización en ejecución.

>[!NOTE]
>
>Las canalizaciones de configuración de nivel web no son compatibles con los repositorios privados. Consulte [Agregar un repositorio privado en Cloud Manager](/help/implementing/cloud-manager/managing-code/private-repositories.md) para obtener detalles y la lista completa de limitaciones.

## Eliminar canalizaciones {#deleting-pipelines}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a la tarjeta **Canalizaciones** de la página **Resumen del programa** y haga clic en el botón de puntos suspensivos situado junto a la canalización que ejecuta. Seleccione **Eliminar** en el menú.

>[!NOTE]
>
>No se puede eliminar una canalización en ejecución.

## Ver detalles de canalización {#view-details}

Puede ver los detalles de una canalización para ver el estado y los registros de su última ejecución.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a la tarjeta **Canalizaciones** de la página **Resumen del programa** y haga clic en el botón de puntos suspensivos situado junto a la canalización que ejecuta. Seleccione **Ver detalles** en el menú.

1. Se le redirigirá a la página de detalles de la canalización en ejecución.

![Detalles de canalización](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-running-details.png)

Desde aquí puede ver el estado de los distintos pasos de la canalización y recuperar los registros de generación con fines diagnósticos. Consulte el documento [Implementación del código](/help/implementing/cloud-manager/deploy-code.md) para obtener más información sobre la implementación del código y la ejecución de pruebas.

Todos los pasos de la ejecución de una canalización se muestran con los que aún no se han iniciado en gris. Los pasos finalizados muestran su duración.

Una vez completado el paso de una canalización, se presenta un resumen.

![Resumen del paso](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-step.png)

Seleccione el vínculo **Ver detalles** para mostrar la sección **Duración**. Esto incluye la duración promedio de la canalización en función de la tendencia histórica para ese programa.

![Duración](/help/implementing/cloud-manager/assets/configure-pipeline/duration.png)

Si la canalización contenía un paso **Escaneado de códigos** que ha planteado problemas, puede pulsar o hacer clic en el botón **Descargar detalles** para ver una lista de las [pruebas de calidad del código](/help/implementing/cloud-manager/code-quality-testing.md) que no se han superado.

![Problemas de calidad del código](assets/managing-pipelines-code-quality-issues.png)

La columna de **Ubicación de archivos del proyecto** está disponible en el archivo CSV para indicar la ubicación del código infractor. Esta columna es la ruta relativa al proyecto, mientras que la columna **Ubicación del archivo** es generada por Maven.

![Detalles del problema de análisis de código del proyecto](assets/managing-pipelines-code-quality-details.png)

>[!NOTE]
>
>Solo puede ver los detalles de una canalización que se esté ejecutando o que se haya ejecutado al menos una vez.

## Cancelar canalizaciones {#cancel}

Si una canalización se encuentra en la fase de validación o compilación de imagen, puede cancelar de forma segura la ejecución de la canalización.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. En la página de información general del programa, haga clic en el botón de puntos suspensivos de la canalización que desee cancelar en la tarjeta **Canalizaciones**.

   ![Cancelando una canalización](/help/implementing/cloud-manager/assets/cancel-pipeline.png)

1. Seleccione **Cancelar**.

También puede cancelar una canalización desde la página de detalles de la canalización.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a la pestaña **Canalizaciones** de la página **Resumen del programa** y seleccione la canalización que desee cancelar.

1. Se le redirigirá a la página de detalles de la canalización en ejecución.

   ![Cancelar detalles de canalización](/help/implementing/cloud-manager/assets/cancel-pipeline-details.png)

1. Seleccione **Cancelar**.
