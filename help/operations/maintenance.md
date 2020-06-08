---
title: Tareas de mantenimiento en AEM como servicio de nube
description: 'Tareas de mantenimiento en AEM como servicio de nube '
translation-type: tm+mt
source-git-commit: 8fba31951276d7e0de1f3bd079e42e431edaff4e
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 2%

---


# Tareas de mantenimiento en AEM como servicio de nube

Las Tareas de mantenimiento son procesos que se ejecutan según una programación para optimizar el repositorio. Con AEM como servicio de nube, la necesidad de que los clientes configuren las propiedades operativas de las tareas de mantenimiento es mínima. Los clientes pueden concentrar sus recursos en las preocupaciones de nivel de aplicación, dejando las operaciones de infraestructura a Adobe.

Para obtener información adicional sobre tareas de mantenimiento, consulte las páginas siguientes:

* [Guía de mantenimiento de AEM](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html)
* [Tareas de mantenimiento de Panel de operaciones](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/operations-dashboard.html#AutomatedMaintenanceTasks)

## Configuración de tareas de mantenimiento

En versiones anteriores de AEM, se podían configurar tareas de mantenimiento mediante la tarjeta de mantenimiento (Herramientas > Operaciones > Mantenimiento). Para AEM como servicio de nube, la tarjeta de mantenimiento ya no está disponible, por lo que las configuraciones deben comprometerse con el control de código fuente e implementarse mediante el Administrador de nube. Adobe administrará tareas de mantenimiento que no requieren decisiones de cliente (por ejemplo, Recopilación de elementos no utilizados del almacén de datos) mientras que el cliente puede configurar otras tareas de mantenimiento (consulte la tabla siguiente).

>[!CAUTION]
>
>Adobe se reserva el derecho de anular la configuración de tarea de mantenimiento de un cliente para mitigar problemas como la degradación del rendimiento.

La siguiente tabla ilustra las tareas de mantenimiento disponibles en el momento de la versión de AEM como servicio de nube.

| Tarea de mantenimiento | Quién es el propietario de la configuración | Cómo configurar (opcional) |
|---|---|---|
| Recopilación de elementos no utilizados del almacén de datos | Adobe | N/D: propiedad total de Adobe |
| Depuración de la versión | Adobe | Totalmente propiedad de Adobe, pero en el futuro, los clientes podrán configurar determinados parámetros. |
| Depuración del registro de auditoría | Adobe | Totalmente propiedad de Adobe, pero en el futuro, los clientes podrán configurar determinados parámetros. |
| Limpieza de archivos binarios de Lucene | Adobe | No utilizado y, por lo tanto, desactivado por Adobe. |
| Depuración de Tareas ad-hoc | Cliente | Debe hacerse en github. <br> Omitir el nodo de configuración de la ventana Mantenimiento debajo `/libs` y `/apps` con `/conf/global/settings/granite/operations/maintenance/granite_weekly` o `granite_daily`. Consulte la tabla Ventana de mantenimiento siguiente para obtener más detalles de configuración. <br> Habilite la tarea de mantenimiento agregando otro nodo debajo del nodo anterior (asígnele el nombre `granite_TaskPurgeTask`) con las propiedades correspondientes. <br> Configure las propiedades de OSGI en la documentación de Tarea de mantenimiento de [AEM 6.5](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| Depuración de flujo de trabajo | Cliente | Debe hacerse en github. <br> Omitir el nodo de configuración de la ventana Mantenimiento debajo `/libs` y `/apps` con `/conf/global/settings/granite/operations/maintenance/granite_weekly` o `granite_daily`. Consulte la tabla Ventana de mantenimiento siguiente para obtener más detalles de configuración. <br> Habilite la tarea de mantenimiento agregando otro nodo debajo del nodo anterior (asígnele el nombre `granite_WorkflowPurgeTask`) con las propiedades correspondientes. <br> Configuración de las propiedades de OSGI consulte la documentación de Tarea de mantenimiento de [AEM 6.5](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| Depuración del proyecto | Cliente | Debe hacerse en github. <br> Omitir el nodo de configuración de la ventana Mantenimiento debajo `/libs` y `/apps` con `/conf/global/settings/granite/operations/maintenance/granite_weekly` o `granite_daily`. Consulte la tabla Ventana de mantenimiento siguiente para obtener más detalles de configuración. <br> Habilite la tarea de mantenimiento agregando un nodo debajo del nodo anterior (asígnele el nombre `granite_ProjectPurgeTask`) con las propiedades correspondientes. <br> Configuración de las propiedades de OSGI consulte la documentación de Tarea de mantenimiento de [AEM 6.5](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |

Los clientes pueden programar cada una de las tareas de mantenimiento Depuración de flujo de trabajo, Depuración de Tareas ad hoc y Depuración de proyectos para que se ejecuten durante las ventanas de mantenimiento diario, semanal o mensual. Estas configuraciones deben editarse directamente en el control de código fuente. En la tabla siguiente se describen los parámetros de configuración disponibles para cada ventana.

<table>
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
    <td><code>/conf/global/settings/granite/operations/maintenance/granite_daily </code> (que anula el nodo en <code>/apps</code> y <code>/libs</code>)</td>
    <td>Consulte el ejemplo de código 1 a continuación</td>
   <td>
    <ul>
    <li><strong>windowSchedule</strong> = day (este valor no debe cambiarse)</li>
    <li><strong>windowStartTime</strong> = HH:MM usando como reloj de 24 horas. Define cuándo deben comenzar a ejecutarse las Tareas de mantenimiento asociadas con la ventana de mantenimiento diario.</li>
    <li><strong>windowEndTime</strong> = HH:MM usando como reloj de 24 horas. Define cuándo las Tareas de mantenimiento asociadas con la ventana de mantenimiento diario deben dejar de ejecutarse si aún no se han completado.</li>
    </ul> </td> 
  </tr>
  <tr>
    <td>Cada semana</td>
    <td>Cliente</td>
    <td>Definición de nodo JCR</td>
    <td><code>/conf/global/settings/granite/operations/maintenance/granite_weekly</code> (que anula el nodo en <code>/apps</code> y <code>/libs</code>)</td>
    <td>Véase el ejemplo de código 2 a continuación</td>
     <td>
    <ul>
    <li><strong>windowSchedule</strong> = semanal (este valor no debe cambiarse)</li>
    <li><strong>windowStartTime</strong> = HH:MM usando como reloj de 24 horas. Define cuándo deben comenzar a ejecutarse las Tareas de mantenimiento asociadas con la ventana de mantenimiento semanal.</li>
    <li><strong>windowEndTime</strong> = HH:MM usando como reloj de 24 horas. Define cuándo las Tareas de mantenimiento asociadas con la ventana de mantenimiento semanal deben dejar de ejecutarse si aún no se han completado.</li>
    <li><strong>windowScheduleWeekdays = Matriz de 2 valores de 1 a 7. p. ej. [5,5].</strong> El primer valor de la matriz es el día de inicio en el que se programa el trabajo y el segundo valor es el día final en el que se detendrá el trabajo. La hora exacta del inicio y del final se rige por windowStartTime y windowEndTime respectivamente.</li>
    </ul> </td> 
  </tr>
  <tr>
    <td>Mensual</td>
    <td>Cliente</td>
    <td>Definición de nodo JCR</td>
    <td><code>/conf/global/settings/granite/operations/maintenance/granite_monthly</code> (que anula el nodo en <code>/apps</code> y <code>/libs</code>)</td>
    <td>Véase el ejemplo de código 3 a continuación</td>
     <td>
    <ul>
    <li><strong>windowSchedule</strong> = day (este valor no debe cambiarse)</li>
    <li><strong>windowStartTime</strong> = HH:MM usando como reloj de 24 horas. Define cuándo deben comenzar a ejecutarse las Tareas de mantenimiento asociadas con la ventana de mantenimiento mensual.</li>
    <li><strong>windowEndTime</strong> = HH:MM usando como reloj de 24 horas. Define cuándo las Tareas de mantenimiento asociadas con la ventana de mantenimiento mensual deben dejar de ejecutarse si aún no se han completado.</li>
    <li><strong>windowScheduleWeekdays = Matriz de 2 valores de 1 a 7. p. ej. [5,5].</strong> El primer valor de la matriz es el día de inicio en el que se programa el trabajo y el segundo valor es el día final en el que se detendrá el trabajo. La hora exacta del inicio y del final se rige por windowStartTime y windowEndTime respectivamente.</li>
    <li><strong>windowFirstLastStartDay - 0/1</strong> 0 para programar la primera semana del mes o 1 para programar la última semana del mes. La ausencia de un valor programaría los trabajos de forma efectiva todos los días, según lo regido por windowScheduleWeekdays cada mes.</li>
    </ul> </td> 
  </tr>
</table>

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

Muestra de código 3

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

Muestra de código 3

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
