---
title: Creación de informes de SLA
description: Aprenda a ver el rendimiento de su entorno de AEM de producción en relación con el contrato de contrato de nivel de servicio (SLA).
exl-id: 03932415-a029-4703-b44a-f86a87edb328
source-git-commit: 6cf164093cc543fe4847859b248e70efd86efbb1
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 2%

---


# Creación de informes de SLA {#sla-reporting}

Aprenda a ver el rendimiento de su entorno de AEM de producción en relación con el contrato de contrato de nivel de servicio (SLA).

## Introducción {#introduction}

Los datos de informes de SLA están disponibles para cada programa de producción a través de la variable **Informes** pestaña . Siga estos pasos para acceder.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y el programa adecuados.

1. Vaya a la **Informes** en la ficha **Información general** página.

1. Haga clic en el año deseado para ver los datos de SLA graficados.

![Ejemplo de gráfico de SLA](assets/sla-reporting-1.png)

Desplace el cursor sobre un punto de datos para mostrar los valores específicos de ese punto.

![Visualización de datos detallados](assets/sla-reporting-b.png)

## Métricas de SLA {#sla-metrics}

El gráfico del año seleccionado incluye varios conjuntos de datos.

* **Publicar contrato de nivel** - Este es el SLA definido en su contrato con Adobe para el nivel de publicación.

* **Publicar nivel real** - Este es el tiempo de actividad medido de los incidentes de factorización del nivel de publicación de producción causados por los proveedores de Adobes o Adobes.

* **Contrato de nivel de Author** - Este es el SLA definido en su contrato con Adobe para el nivel de Author.

* **Nivel de Author Real** - Este es el tiempo de actividad medido de los incidentes de factorización de nivel de autor de producción causados por los proveedores de Adobes o Adobes.

## Análisis de eventos {#event-analysis}

La variable **Análisis de eventos** en el gráfico se muestra el conjunto de incidentes ocurridos para el programa durante el año seleccionado.

Cada incidente tiene un intervalo de tiempo, una causa y un conjunto de comentarios.

![Ejemplo de análisis de eventos](assets/sla-reporting-c.png)
