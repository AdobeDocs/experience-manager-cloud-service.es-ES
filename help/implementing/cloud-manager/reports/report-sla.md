---
title: Informes SLA
description: Aprenda a ver el rendimiento de su entorno de producción de AEM en relación con la Service level agreement contratada.
exl-id: 03932415-a029-4703-b44a-f86a87edb328
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 13%

---


# Informes de SLA {#sla-reporting}

Aprenda a ver el rendimiento de su entorno de producción de AEM en relación con la SLA contratada (Service level agreement).

## Ver un informe de SLA {#introduction}

Los datos del informe de SLA hacen un seguimiento de las métricas de rendimiento para dos niveles de producción: nivel de creación y nivel de publicación.

El gráfico de líneas de un año seleccionado incluye puntos de datos para cada mes de enero a diciembre. Se realiza un seguimiento de las siguientes métricas.

| Métrica rastreada | Color de línea | Descripción |
| --- | --- | --- |
| Nivel de autor real | Verde claro | El tiempo de actividad medido de los incidentes de factorización de nivel de creación de producción causados por los proveedores de Adobe o Adobe. |
| Contrato de nivel de autor | Azul oscuro | El SLA definido en su contrato con Adobe para el nivel de Author. |
| Publicar nivel real | Naranja | El tiempo de actividad medido del nivel de publicación de producción, los incidentes de factorización causados por Adobe o los proveedores de Adobe. |
| Publicar contrato de nivel | Rojo | El SLA definido en su contrato con Adobe para el nivel de publicación. |

**Para ver un informe de SLA:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.

1. En la página **Resumen del programa**, en el menú de la izquierda, haga clic en **Informes**.

1. Haga clic en **Informes de SLA**.

   ![Gráfico de líneas de informe de SLA](/help/implementing/cloud-manager/reports/assets/cm-sla-report2.png)

1. Haga clic en el año deseado para ver un gráfico de líneas de datos de SLA.

1. (Opcional) Realice una de las siguientes acciones:

   * Desplace el cursor sobre un punto de datos del gráfico de líneas para mostrar los valores específicos de ese punto.
   * Debajo del año del gráfico de líneas, haga clic en el icono **Descargar** para guardar un archivo de imagen PNG del gráfico de líneas.
   * Haga clic en el nombre de una métrica para ver únicamente los datos de esa métrica. O bien, presione `Shift` en el teclado mientras selecciona o anula la selección de uno o más nombres de métricas.

## Análisis de eventos {#event-analysis}

La sección **Análisis de eventos** en el gráfico muestra el conjunto de incidentes que ocurrieron para el programa durante el año seleccionado.

Cada incidente tiene un intervalo de tiempo, una causa y un conjunto de comentarios.

![Ejemplo de análisis de eventos](/help/implementing/cloud-manager/reports/assets/sla-reporting-c.png)

## Actualizar el intervalo de los informes de SLA {#refresh}

Los informes de SLA insight le permiten conocer el rendimiento de su entorno de producción de AEM y están actualizados, pero no son instantáneos. La generación de informes de SLA se produce mensualmente y se genera para los nuevos programas que se han marcado como `Production previous month`. No es instantáneo. Debido a este retraso, tenga en cuenta lo siguiente al revisar el informe de SLA:

* El SLA del que se informa es el que existía a principios de mes, incluso si SLA había cambiado durante ese mes.
* Si no había ningún SLA a principios de mes porque el programa no existía, se aplica el SLA que existía en la fecha de creación del programa.

## Previsualizar entornos {#preview}

El entorno de vista previa está diseñado como una herramienta para que los autores de contenido comprueben la experiencia final del contenido antes de publicarlo. Debido a esta funcionalidad, los entornos de vista previa no están diseñados con alta disponibilidad y no tienen una SLA asociada.

