---
title: Crear informes de SLA
description: Aprenda cómo ver el rendimiento de su entorno de AEM de producción en relación con el contrato de nivel de servicio (SLA).
exl-id: 03932415-a029-4703-b44a-f86a87edb328
source-git-commit: 90250c13c5074422e24186baf78f84c56c9e3c4f
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 88%

---


# Crear informes de SLA {#sla-reporting}

Aprenda cómo ver el rendimiento de su entorno de AEM de producción en relación con el contrato de nivel de servicio (SLA).

## Introducción {#introduction}

Los datos de informes de SLA están disponibles para cada programa de producción a través de la pestaña **Informes**. Siga estos pasos para acceder.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En el **[Mis programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** seleccione el programa.

1. Navegue hasta la pestaña **Informes** desde la página **Información general**.

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
