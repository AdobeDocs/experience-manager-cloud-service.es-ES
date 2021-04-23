---
title: Tareas de mantenimiento en AEM como Cloud Service
description: Tareas de mantenimiento en AEM como Cloud Service
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
translation-type: tm+mt
source-git-commit: 5892ef2998b8bb0e955998662a3cbe8aaa624e97
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 2%

---

# Tareas de mantenimiento en AEM como Cloud Service

Las tareas de mantenimiento son procesos que se ejecutan según una programación para optimizar el repositorio. Con AEM como Cloud Service, la necesidad de que los clientes configuren las propiedades operativas de las tareas de mantenimiento es mínima. Los clientes pueden concentrar sus recursos en preocupaciones a nivel de aplicación, dejando las operaciones de infraestructura en Adobe.

Para obtener información adicional sobre las tareas de mantenimiento, consulte las páginas siguientes:

* [Guía de mantenimiento de AEM](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html)
* [Tareas de mantenimiento del panel de operaciones](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/operations-dashboard.html#AutomatedMaintenanceTasks)

## Configuración de tareas de mantenimiento

En versiones anteriores de AEM, se podían configurar tareas de mantenimiento mediante la tarjeta de mantenimiento (Herramientas > Operaciones > Mantenimiento). Para AEM como Cloud Service, la tarjeta de mantenimiento ya no está disponible, por lo que las configuraciones deben comprometerse con el control de código fuente e implementarse mediante Cloud Manager. Adobe gestionará las tareas de mantenimiento que no requieran decisiones de cliente (por ejemplo, la colección de residuos del almacén de datos), mientras que el cliente puede configurar otras tareas de mantenimiento (consulte la tabla siguiente).

>[!CAUTION]
>
>Adobe se reserva el derecho de anular los ajustes de configuración de tareas de mantenimiento de un cliente para mitigar problemas como la degradación del rendimiento.

La siguiente tabla ilustra las tareas de mantenimiento disponibles en el momento del lanzamiento de AEM como Cloud Service.

| Tarea de mantenimiento | Quién es el propietario de la configuración | Configuración (opcional) |
|---|---|---|
| Colección de residuos del almacén de datos | Adobe | N/D: propiedad total del Adobe |
| Depuración de la versión | Adobe | Totalmente propiedad de Adobe, pero en el futuro, los clientes podrán configurar ciertos parámetros. |
| Purga de registro de auditoría | Adobe | Totalmente propiedad de Adobe, pero en el futuro, los clientes podrán configurar ciertos parámetros. |
| Limpieza de archivos binarios de Lucene | Adobe | No se utiliza y, por lo tanto, se desactiva mediante el Adobe. |
| Depuración de tarea ad hoc | Cliente | Debe hacerse en github. <br> Anule el nodo de configuración de la ventana de mantenimiento predeterminado en  `/libs` creando propiedades en la carpeta  `/apps/settings/granite/operations/maintenance/granite_weekly` o  `granite_daily`. Consulte la tabla Ventana de mantenimiento a continuación para obtener más información sobre la configuración. <br> Habilite la tarea de mantenimiento añadiendo otro nodo bajo el nodo anterior (asígnele el nombre  `granite_TaskPurgeTask`) con las propiedades adecuadas. <br> Configure las propiedades de OSGI consulte la documentación de la tarea de mantenimiento de  [AEM 6.5](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| Depuración de flujo de trabajo | Cliente | Debe hacerse en github. <br> Anule el nodo de configuración de la ventana de mantenimiento integrado en  `/libs` creando propiedades en la `/apps/settings/granite/operations/maintenance/granite_weekly` carpeta  `granite_daily`. Consulte la tabla Ventana de mantenimiento a continuación para obtener más información sobre la configuración. <br> Habilite la tarea de mantenimiento añadiendo otro nodo bajo el nodo anterior (asígnele el nombre  `granite_WorkflowPurgeTask`) con las propiedades adecuadas. <br> Configure las propiedades de OSGI consulte la documentación de la tarea de mantenimiento de  [AEM 6.5](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| Depuración del proyecto | Cliente | Debe hacerse en github. <br> Anule el nodo de configuración de la ventana de mantenimiento predeterminado en  `/libs` creando propiedades en la carpeta  `/apps/settings/granite/operations/maintenance/granite_weekly` o  `granite_daily`. Consulte la tabla Ventana de mantenimiento a continuación para obtener más información sobre la configuración. <br> Habilite la tarea de mantenimiento añadiendo un nodo bajo el nodo anterior (asígnele el nombre  `granite_ProjectPurgeTask`) con las propiedades adecuadas. <br> Configurar las propiedades de OSGI consulte la documentación de la tarea de mantenimiento de  [AEM 6.5](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |

Los clientes pueden programar cada una de las tareas de Purga de flujo de trabajo, Depuración de tareas ad hoc y Mantenimiento de purga de proyectos para que se ejecuten durante las ventanas de mantenimiento diario, semanal o mensual. Estas configuraciones deben editarse directamente en el control de código fuente. La tabla siguiente describe los parámetros de configuración disponibles para cada una de las ventanas.

<table>
 <tbody>
  <tr>
    <th>Configuración de la ventana de mantenimiento</th>
    <th>Quién es el propietario de la configuración</th>
    <th>Tipo de configuración</th>
    <th>Lugar de residencia</th>
    <th>Ejemplo</th>
    <th>Parámetros</th>
  </tr>
  <tr>
    <td>Cada día</td>
    <td>Cliente</td>
    <td>Definición de nodo JCR</td>
    <td>1</td>
    <td>1</td>
  <td>
  <p><strong>windowSchedule= daily</strong>  (este valor no debe cambiarse)</p>
  <p><strong>windowStartTime= HH:</strong>  usando como reloj de 24 horas. Define cuándo deben comenzar a ejecutarse las tareas de mantenimiento asociadas con la ventana de mantenimiento diario.</p>
  <p><strong>windowEndTime= HH:</strong> Usando como reloj de 24 horas. Define cuándo las tareas de mantenimiento asociadas con la ventana de mantenimiento diario deben dejar de ejecutarse si aún no se han completado.</p>
  </td> 
  </tr>
  <tr>
    <td>Cada semana</td>
    <td>Cliente</td>
    <td>Definición de nodo JCR</td>
    <td>Ver la ubicación 2 más abajo</td>
    <td>Consulte el ejemplo de código 2 a continuación</td>
    <td>
    <p><strong>windowSchedule= weekly</strong>  (este valor no debe cambiarse)</p>
    <p><strong>windowStartTime= HH:</strong>  usando como reloj de 24 horas. Define cuándo deben comenzar a ejecutarse las tareas de mantenimiento asociadas con la ventana de mantenimiento semanal.</p>
    <p><strong>windowEndTime= HH:</strong> Usando como reloj de 24 horas. Define cuándo las tareas de mantenimiento asociadas con la ventana de mantenimiento semanal deben dejar de ejecutarse si aún no se han completado.</p>
    <p><strong>windowScheduleWeekdays= Matriz de 2 valores entre 1 y 7 (p. ej. [5,5])</strong> El primer valor de la matriz es el día de inicio cuando se programa el trabajo y el segundo valor es el día de finalización cuando se detiene el trabajo. La hora exacta del inicio y del final se rige por windowStartTime y windowEndTime respectivamente.</p>
    </td>
  </tr>
  <tr>
    <td>Mensual</td>
    <td>Cliente</td>
    <td>Definición de nodo JCR</td>
    <td>Ver la ubicación 3 a continuación</td>
    <td>Consulte la muestra de código 3 a continuación</td>
    <td>
    <p><strong>windowSchedule= daily</strong>  (este valor no debe cambiarse)</p>
    <p><strong>windowStartTime= HH:</strong>  usando como reloj de 24 horas. Define cuándo deben comenzar a ejecutarse las tareas de mantenimiento asociadas con la ventana de mantenimiento mensual.</p>
    <p><strong>windowEndTime= HH:</strong> Usando como reloj de 24 horas. Define cuándo las tareas de mantenimiento asociadas con la ventana de mantenimiento mensual deben dejar de ejecutarse si aún no se han completado.</p>
    <p><strong>windowScheduleWeekdays = Matriz de 2 valores entre 1 y 7 (p. ej. [5,5])</strong> El primer valor de la matriz es el día de inicio cuando se programa el trabajo y el segundo valor es el día de finalización cuando se detiene el trabajo. La hora exacta del inicio y del final se rige por windowStartTime y windowEndTime respectivamente.</p>
    <p><strong>windowFirstLastStartDay= 0/1</strong> 0 para programar la primera semana del mes o 1 para programar la última semana del mes. La ausencia de un valor programaría los trabajos todos los días según windowScheduleWeekdays cada mes.</p>
    </td> 
    </tr>
    </tbody>
</table>

Ubicaciones:

1. /apps/settings/granite/operations/maintenance/granite_daily
2. /apps/settings/granite/operations/maintenance/granite_weekly
3. /apps/settings/granite/operations/maintenance/granite_month

Ejemplos de código:

Ejemplo de código 1

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" 
  xmlns:jcr="http://www.jcp.org/jcr/1.0" 
  jcr:primaryType="sling:Folder"
  sling:configCollectionInherit="true"
  sling:configPropertyInherit="true"
  windowSchedule="daily"
  windowStartTime="03:00"
  windowEndTime="05:00"
 />
```

Ejemplo de código 2

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" 
   xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="sling:Folder"
   sling:configCollectionInherit="true"
   sling:configPropertyInherit="true"
   windowEndTime="15:30"
   windowSchedule="weekly"
   windowScheduleWeekdays="[5,5]"
   windowStartTime="14:30"/>
```

Ejemplo de código 3

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" 
   xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="sling:Folder"
   sling:configCollectionInherit="true"
   sling:configPropertyInherit="true"
   windowEndTime="15:30"
   windowSchedule="monthly"
   windowFirstLastStartDay=0
   windowScheduleWeekdays="[5,5]"
   windowStartTime="14:30"/>
```
