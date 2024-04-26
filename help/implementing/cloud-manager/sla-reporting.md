---
title: Crear informes de SLA
description: Aprenda cómo ver el rendimiento de su entorno de AEM de producción en relación con el contrato de nivel de servicio (SLA).
exl-id: 03932415-a029-4703-b44a-f86a87edb328
source-git-commit: a0f80a363cb47be9e3d8f7fa96ea3068eb077d42
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 52%

---


# Crear informes de SLA {#sla-reporting}

Aprenda cómo ver el rendimiento de su entorno de AEM de producción en relación con el contrato de nivel de servicio (SLA).

## Introducción {#introduction}

Los datos de informes de SLA están disponibles para cada programa de producción a través de la pestaña **Informes**. Siga estos pasos para acceder.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En el **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)** , seleccione el programa.

1. Con el panel de navegación lateral, vaya al **Informes** de la pestaña **Información general** página.

1. Haga clic en el año deseado para ver los datos de SLA en gráficos.

![Ejemplo de gráfico de SLA](assets/sla-reporting-1.png)

Desplace el cursor sobre un punto de datos para mostrar los valores específicos de ese punto.

![Visualizar datos detallados](assets/sla-reporting-b.png)

## Métricas de SLA {#sla-metrics}

El gráfico del año seleccionado incluye varios conjuntos de datos.

* **Publicar contrato de nivel**: Este es el SLA definido en su contrato con Adobe para el nivel de publicación.

* **Publicar nivel real**: Este es el tiempo de actividad medido de los incidentes de factorización del nivel de publicación de producción causados por los proveedores de Adobe o por Adobe.

* **Contrato de nivel de autor**: Este es el SLA definido en su contrato con Adobe para el nivel de autor.

* **Nivel de autor actual**: Este es el tiempo de actividad medido de los incidentes de factorización del nivel de autor de producción causados por los proveedores de Adobe o por Adobe.

## Análisis de eventos {#event-analysis}

La sección **Análisis de eventos** en el gráfico muestra el conjunto de incidentes ocurridos para el programa durante el año seleccionado.

Cada incidente tiene un intervalo de tiempo, una causa y un conjunto de comentarios.

![Ejemplo de análisis de eventos](assets/sla-reporting-c.png)

## Actualizar intervalo {#refresh}

AEM La creación de informes de SLA le ofrecen una perspectiva del rendimiento de su entorno de producción de y está actualizado, pero no es instantánea. La generación de informes de SLA se produce mensualmente y se genera para nuevos programas marcados como Producción el mes anterior. No es instantáneo. Debido a este retraso, tenga en cuenta lo siguiente al revisar su informe de SLA:

* El SLA notificado será el que existió a principios de mes, incluso si el SLA cambió durante ese mes.
* Si no había SLA a principios de mes porque el programa no existía en ese momento, se aplica el SLA que existía en la fecha de creación del programa.

## Previsualizar entornos {#preview}

El entorno de vista previa está diseñado como una herramienta para que los autores de contenido comprueben la experiencia final del contenido antes de publicarlo. Debido a esto, los entornos de vista previa no están diseñados con alta disponibilidad y no tienen un SLA asociado.
