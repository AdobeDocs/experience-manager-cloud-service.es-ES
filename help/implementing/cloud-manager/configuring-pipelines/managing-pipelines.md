---
title: Administrar canalizaciones
description: Obtenga información sobre cómo administrar las canalizaciones existentes, como editarlas, ejecutarlas y eliminarlas.
index: true
exl-id: 4aff5a84-134a-43fa-8de8-8d564f4edd16
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f7a8e823f058115f11241f0864517432a7dea5ab
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 32%

---


# Administrar canalizaciones {#managing-pipelines}

Obtenga información sobre cómo administrar las canalizaciones existentes, como editarlas, ejecutarlas y eliminarlas.

## Tarjeta de canalizaciones {#pipeline-card}

La tarjeta **Canalizaciones** de la página **Información general del programa** en Cloud Manager le ofrece una descripción general de todas sus canalizaciones y de su estado actual.

![Tarjeta de canalización en Cloud Manager](/help/implementing/cloud-manager/assets/configure-pipeline/pipelines-card.png)

Al hacer clic en ![Puntos suspensivos - Icono de más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) junto a cada canalización, podrá realizar las siguientes acciones:

* [Ejecutar una canalización](#running-pipelines)
* [Cancelar una canalización](#cancel)
* [Edición de una canalización](#editing-pipelines)
* [Eliminación de una canalización](#deleting-pipelines)
* [Ver los detalles de la última ejecución de una canalización](#view-details)

En la parte inferior de la lista de canalizaciones, tiene las siguientes opciones generales:

* **Agregar** - Para [agregar una nueva canalización de producción](configuring-production-pipelines.md) o [agregar una nueva canalización que no sea de producción](configuring-non-production-pipelines.md)
* **Mostrar todo**: Lleva al usuario a la pantalla Canalizaciones para ver todas las canalizaciones en una tabla más detallada.
* **Acceder a la info del repositorio**: Muestra la información necesaria para acceder al repositorio de Git de Cloud Manager
* **Más información**: Navega hasta los recursos de documentación de canalización de CI/CD.

## Página Canalizaciones {#pipelines}

La página **Canalizaciones** muestra una lista completa de todas las canalizaciones del programa seleccionado. Esta información es útil porque presenta información más completa que la disponible en la [tarjeta de canalización](#pipeline-card).

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.

1. En la página **Resumen del programa**, haga clic en ![Pestaña Canalización: icono de flujo de trabajo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) **Pestaña Canalizaciones**.

1. En la página **Canalizaciones**, puede ver una lista de todas las canalizaciones para el programa y comenzar y detener la ejecución de la canalización como lo haría en la **Tarjeta de canalizaciones**.

Si se está ejecutando una canalización, haga clic en ![Información - icono mediano](https://spectrum.adobe.com/static/icons/ui_18/InfoMedium.svg) en la columna **Estado** para mostrar una ventana emergente con detalles sobre la ejecución. En el elemento emergente, haga clic en **Ver detalles** para ver los [detalles de la ejecución de la canalización](#view-details).

![Detalles de ejecución de canalización](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-status.png)


También puede hacer clic en ![Puntos suspensivos - Más icono](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) junto a la canalización para realizar acciones adicionales apropiadas para el estado de la canalización, como [editarla](#editing-pipelines) o [cancelar la ejecución](#cancel).

![Acciones de canalización](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-actions.png)

## Página de actividad {#activity}

La página **Actividad** muestra una lista completa de todas las ejecuciones de canalizaciones para el programa seleccionado, así como otros eventos de programa importantes.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. En la página **Resumen del programa**, en el menú lateral, haz clic en ![Icono de campana](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Bell_18_N.svg) **Actividad**.

1. En la página **Actividad**, puede ver una lista de todas las ejecuciones de canalización del programa, incluidas las ejecuciones actuales y las históricas.

Si se está ejecutando una canalización, puede hacer clic en ![Información - icono mediano](https://spectrum.adobe.com/static/icons/ui_18/InfoMedium.svg) en la columna **Estado** para mostrar una ventana emergente que muestra información sobre la ejecución.

![Detalles de ejecución de canalización](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-activity.png)

Haga clic en la fila que representa la ejecución de la canalización para ver los [detalles de la ejecución de la canalización](#view-details).

También puede hacer clic en ![Puntos suspensivos - Icono de más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) para realizar acciones adicionales en la ejecución de la canalización, como ver sus detalles o descargar el registro, que lo lleva a la [página de detalles de la canalización](#view-details).

![Acciones de ejecución de canalización](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-execution-actions.png)

## Ejecutar una canalización {#running-pipelines}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a la tarjeta **Canalizaciones** de la página **Información general del programa**.

1. Haga clic en ![puntos suspensivos - Icono de más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) junto a la canalización que ejecute.

1. En el menú desplegable, haga clic en ![Ejecutar - Icono de reproducción](https://spectrum.adobe.com/static/icons/workflow_18/Smock_PlayCircle_18_N.svg) **Ejecutar**.

   Se inicia la ejecución de la canalización y la columna **Estado** muestra su progreso.

Para ver los detalles de la ejecución, vuelva a hacer clic en ![Puntos suspensivos - Más icono](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) y haga clic en **[Ver detalles](#view-details)**.

Según el tipo de canalización, puede cancelar la ejecución si hace clic de nuevo en ![Puntos suspensivos - Icono de más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) y hace clic en **Cancelar**.

## Edición de una canalización {#editing-pipelines}

Puede editar una canalización si no se está ejecutando.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a la tarjeta **Canalizaciones** de la página **Información general del programa**.

1. Haga clic en ![puntos suspensivos - Icono de más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) junto a la canalización que desee editar.

1. En el menú desplegable, haga clic en **Editar**.

1. En el cuadro de diálogo **Editar canalización de producción** o **Editar canalización que no sea de producción**, edite los mismos detalles que introdujo al crear la canalización.

   Consulte las siguientes páginas para obtener más información sobre los campos y las opciones de configuración disponibles para las canalizaciones.
   * [Configuración de una canalización de producción](configuring-production-pipelines.md)
   * [Añadir una canalización que no es de producción](configuring-non-production-pipelines.md)

1. Cuando haya terminado, haga clic en **Actualizar**.

>[!NOTE]
>
>Las canalizaciones de configuración de nivel web no son compatibles con los repositorios privados. Consulte [Agregar un repositorio privado de GitHub en Cloud Manager](/help/implementing/cloud-manager/managing-code/private-repositories.md) para obtener detalles y la lista completa de limitaciones.

## Eliminación de una canalización {#deleting-pipelines}

Puede eliminar una canalización si no se está ejecutando.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a la tarjeta **Canalizaciones** de la página **Información general del programa**.

1. Haga clic en ![puntos suspensivos - Icono de más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) junto a la canalización que ejecute.

1. En el menú desplegable, haga clic en **Eliminar**.


## Ver los detalles de la última ejecución de una canalización {#view-details}

Puede comprobar los detalles de una canalización para ver el estado y los registros de su ejecución más reciente. Sin embargo, solo puede acceder a los detalles si la canalización se está ejecutando actualmente o se ha ejecutado al menos una vez.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a la tarjeta **Canalizaciones** de la página **Información general del programa**.

1. En el menú desplegable, haga clic en ![Puntos suspensivos - Icono de más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) junto a la canalización que ejecute.

1. En el menú desplegable, haga clic en **Ver última ejecución**.

   Se le redirigirá a la página de detalles de la canalización en ejecución.

   ![Detalles de canalización](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-running-details.png)

   Desde aquí, puede ver el estado de los distintos pasos de la canalización y recuperar los registros de compilación para fines diagnósticos. Consulte [Implementar su código](/help/implementing/cloud-manager/deploy-code.md) para obtener más información sobre la implementación de código y la ejecución de pruebas.

   Todos los pasos de la ejecución de una canalización se muestran con los que aún no se han iniciado en gris. Los pasos finalizados muestran su duración.

   Una vez completado el paso de una canalización, se presenta un resumen.

   ![Resumen de pasos](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-step.png)

1. Haga clic en **Ver detalles** para expandir la sección **Duración**, donde podrá ver la duración promedio de la canalización en función de las tendencias históricas del programa.

   ![Duración](/help/implementing/cloud-manager/assets/configure-pipeline/duration.png)

1. Si su canalización incluyó un paso de **escaneo de código** que marcó problemas, haga clic en **Descargar detalles** para acceder a una lista de [pruebas de calidad de código](/help/implementing/cloud-manager/code-quality-testing.md) que no se superaron.

   ![Problemas de calidad del código](assets/managing-pipelines-code-quality-issues.png)

   El archivo CSV incluye una columna **Ubicación del archivo de proyecto**, que muestra la ruta de acceso al código problemático relativo al proyecto. Por el contrario, la columna **Ubicación del archivo** refleja la ruta generada por Maven.

   ![Detalles del problema de análisis de código del proyecto](assets/managing-pipelines-code-quality-details.png)

## Cancelar una canalización {#cancel}

Puede cancelar de forma segura la ejecución de la canalización si está en la fase de validación o compilación de la imagen.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. En la página de información general del programa, haga clic en ![Puntos suspensivos - Icono de más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) de la canalización que desee cancelar en la tarjeta **Canalizaciones**.

   ![Cancelando una canalización](/help/implementing/cloud-manager/assets/cancel-pipeline.png)

1. Haga clic en **Cancelar**.

También puede cancelar una canalización desde la página de detalles de la canalización.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a la pestaña ![Canalizaciones: icono de flujo de trabajo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) **Canalizaciones** de la página **Información general del programa** y seleccione la canalización que desee cancelar.

   Se le redirigirá a la página de detalles de la canalización en ejecución.

   ![Cancelar detalles de canalización](/help/implementing/cloud-manager/assets/cancel-pipeline-details.png)

1. Haga clic en **Cancelar**.
