---
title: Tareas de mantenimiento en AEM as a Cloud Service
description: Tareas de mantenimiento en AEM as a Cloud Service
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
source-git-commit: f1d1009db31585ff82c02080a6ab7ea7ca5bf66b
workflow-type: tm+mt
source-wordcount: '1068'
ht-degree: 75%

---

# Tareas de mantenimiento en AEM as a Cloud Service {#maintenance-tasks-in-aem-as-a-cloud-service}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_maintenance"
>title="Tareas de mantenimiento"
>abstract="Las tareas de mantenimiento son procesos que se ejecutan según una programación para optimizar el repositorio. Con AEM as a Cloud Service, la necesidad de que los clientes configuren las propiedades operativas de las tareas de mantenimiento es mínima. Los clientes pueden enfocar sus recursos en preocupaciones del nivel de la aplicación y dejar que Adobe se encargue de las operaciones de infraestructura."

Las tareas de mantenimiento son procesos que se ejecutan según una programación para optimizar el repositorio. Con AEM as a Cloud Service, la necesidad de que los clientes configuren las propiedades operativas de las tareas de mantenimiento es mínima. Los clientes pueden enfocar sus recursos en preocupaciones del nivel de la aplicación y dejar que Adobe se encargue de las operaciones de infraestructura.

## Configuración de tareas de mantenimiento {#maintenance-tasks-configuring}

En versiones anteriores de AEM, se podían configurar tareas de mantenimiento mediante la tarjeta de mantenimiento (Herramientas > Operaciones > Mantenimiento). La tarjeta de mantenimiento ya no está disponible para AEM as a Cloud Service, por lo que las configuraciones deben enviarse al control de origen e implementarse mediante Cloud Manager. Adobe administra las tareas de mantenimiento que tienen configuraciones que los clientes no pueden modificar (por ejemplo, Recopilación de residuos del almacén de datos, Purga del registro de auditoría, Purga de la versión). Los clientes pueden configurar otras tareas de mantenimiento, como se describe en la tabla siguiente.

>[!CAUTION]
>
>Adobe se reserva el derecho de anular los ajustes de configuración de tareas de mantenimiento de un cliente para mitigar problemas como la degradación del rendimiento.

La siguiente tabla ilustra las tareas de mantenimiento disponibles en el momento de la publicación de AEM as a Cloud Service.

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>Tarea de mantenimiento</th>
    <th>Quién posee la configuración</th>
    <th>Cómo se configura (opcional)</th>
  </tr>  
  <tr>
    <td>Recopilación de residuos del almacén de datos</td>
    <td>Adobe</td>
    <td>N/D: propiedad total de Adobe</td>
  </td> 
  </tr>
  <tr>
    <td>Depuración de la versión</td>
    <td>Adobe</td>
    <td>Para los entornos existentes (los creados antes del 1 de marzo de 2023), la depuración está deshabilitada y no se habilitará en el futuro a menos que el cliente lo habilite explícitamente, momento en el cual también puede configurarla con valores personalizados.<br><br> <!--Alexandru: please leave the two line breaks in place, otherwise spacing won't render properly-->Los nuevos entornos (los creados a partir del 1 de marzo de 2023) tendrán la depuración habilitada de forma predeterminada con los valores siguientes, y los clientes podrán configurarla con valores personalizados.
     <ol>
       <li>Se eliminan las versiones con más de 30 días</li>
       <li>Se conservan las cinco versiones más recientes de los últimos 30 días</li>
       <li>Independientemente de las reglas anteriores, se conserva la versión más reciente.</li>
       <br>Se recomienda que los clientes que tengan requisitos regulatorios para procesar páginas de sitio exactamente como aparecieron en una fecha específica, se integren con servicios externos especializados.
     </ol></td>
  </td>
  </tr>
  <tr>
    <td>Purga del registro de auditoría</td>
    <td>Adobe</td>
    <td>Para los entornos existentes (los creados antes del 1 de marzo de 2023), la depuración está deshabilitada y no se habilitará en el futuro a menos que el cliente lo habilite explícitamente, momento en el cual también puede configurarla con valores personalizados.<br><br> <!-- See above for the two line breaks -->Los nuevos entornos (los creados a partir del 1 de marzo de 2023) tendrán la depuración habilitada de forma predeterminada en <code>/content</code> del repositorio según el siguiente comportamiento:
     <ol>
       <li>Para la auditoría de replicación, se eliminan los registros de auditoría con más de tres días</li>
       <li>Para la auditoría de DAM (Assets), se eliminan los registros de auditoría con más de 30 días</li>
       <li>Para la auditoría de páginas, se eliminan los registros con más de tres días.</li>
       <br>Se recomienda que los clientes que tengan requisitos regulatorios para producir registros de auditoría no editables se integren con servicios externos especializados.
     </ol></td>
   </td>
  </tr>
  <tr>
    <td>Limpieza de archivos binarios de Lucene</td>
    <td>Adobe</td>
    <td>No se utiliza y, por lo tanto, Adobe lo ha desactivado.</td>
  </td>
  </tr>
  <tr>
    <td>Purga de la tarea ad hoc</td>
    <td>Cliente</td>
    <td>
    <p>Debe hacerse en Git. Anule el nodo de configuración de la ventana de mantenimiento predeterminado en <code>/libs</code> creando propiedades en la carpeta <code>/apps/settings/granite/operations/maintenance/granite_weekly</code> o <code>granite_daily</code>.</p>
    <p>Consulte la tabla Ventana de mantenimiento a continuación para obtener más información sobre la configuración. Habilite la tarea de mantenimiento añadiendo otro nodo bajo el nodo de arriba. Asígnele un nombre <code>granite_TaskPurgeTask</code>, con atributo <code>sling:resourceType</code> establezca en <code>granite/operations/components/maintenance/task</code> Atributo y <code>granite.maintenance.name</code> establezca en <code>TaskPurge</code>. Configure las propiedades de OSGI, consulte <code>com.adobe.granite.taskmanagement.impl.purge.TaskPurgeMaintenanceTask</code> para obtener la lista de propiedades.</p>
  </td>
  </tr>
    <tr>
    <td>Depuración de flujo de trabajo</td>
    <td>Cliente</td>
    <td>
    <p>Debe hacerse en Git. Anule el nodo de configuración de la ventana de mantenimiento predeterminado en <code>/libs</code> creando propiedades en la carpeta <code>/apps/settings/granite/operations/maintenance/granite_weekly</code> o <code>granite_daily</code>. Consulte la tabla Ventana de mantenimiento a continuación para obtener más información sobre la configuración.</p>
    <p>Habilite la tarea de mantenimiento añadiendo otro nodo bajo el anterior (asígnele el nombre <code>granite_WorkflowPurgeTask</code>) con las propiedades adecuadas. Configure las propiedades de OSGI. Consulte <a href="https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/workflows-administering.html?lang=es#regular-purging-of-workflow-instances">Documentación de la tarea de mantenimiento de la versión 6.5 de AEM</a>.</p>
  </td>
  </tr>
  <tr>
    <td>Depuración del proyecto</td>
    <td>Cliente</td>
    <td>
    <p>Debe hacerse en Git. Anule el nodo de configuración de la ventana de mantenimiento predeterminado en <code>/libs</code> creando propiedades en la carpeta <code>/apps/settings/granite/operations/maintenance/granite_weekly</code> o <code>granite_daily</code>. Consulte la tabla Ventana de mantenimiento a continuación para obtener más información sobre la configuración.</p>
    <p>Habilite la tarea de mantenimiento añadiendo otro nodo bajo el anterior (asígnele el nombre <code>granite_ProjectPurgeTask</code>) con las propiedades adecuadas. Configure las propiedades de OSGI.</p>
  </td>
  </tr>
  </tbody>
</table>

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>Configuración de la ventana de mantenimiento</th>
    <th>Quién posee la configuración</th>
    <th>Tipo de configuración</th>
    <th>Parámetros</th>
  </tr>
  <tr>
    <td>Cada día</td>
    <td>Cliente</td>
    <td>Definición del nodo JCR</td>
  <td>
  <p><strong>windowSchedule=daily</strong> (este valor no debe cambiarse)</p>
  <p><strong>windowStartTime=HH:MM</strong> como reloj de 24 horas. Define cuándo deben comenzar a ejecutarse las tareas de mantenimiento asociadas con la ventana de mantenimiento diario.</p>
  <p><strong>windowEndTime=HH:MM</strong> como reloj de 24 horas. Define cuándo deben dejar de ejecutarse las tareas de mantenimiento asociadas con la ventana de mantenimiento diario si aún no se han completado.</p>
  </td> 
  </tr>
  <tr>
    <td>Cada semana</td>
    <td>Cliente</td>
    <td>Definición del nodo JCR</td>
    <td>
    <p><strong>windowSchedule=weekly</strong> (este valor no debe cambiarse)</p>
    <p><strong>windowStartTime=HH:MM</strong> como reloj de 24 horas. Define cuándo deben comenzar a ejecutarse las tareas de mantenimiento asociadas con la ventana de mantenimiento semanal.</p>
    <p><strong>windowEndTime=HH:MM</strong> como reloj de 24 horas. Define cuándo deben dejar de ejecutarse las tareas de mantenimiento asociadas con la ventana de mantenimiento semanal si aún no se han completado.</p>
    <p><strong>windowScheduleWeekdays= Matriz de dos valores entre 1 y 7 (por ejemplo, [5,5])</strong> El primer valor de la matriz es el día de inicio cuando se programa el trabajo y el segundo valor es el día de finalización cuando se detiene el trabajo. La hora exacta del inicio y la finalización se rige por windowStartTime y windowEndTime respectivamente.</p>
    </td>
  </tr>
  <tr>
    <td>Mensual</td>
    <td>Cliente</td>
    <td>Definición del nodo JCR</td>
    <td>
    <p><strong>windowSchedule=daily</strong> (este valor no debe cambiarse)</p>
    <p><strong>windowStartTime=HH:MM</strong> como reloj de 24 horas. Define cuándo deben comenzar a ejecutarse las tareas de mantenimiento asociadas con la ventana de mantenimiento mensual.</p>
    <p><strong>windowEndTime=HH:MM</strong> como reloj de 24 horas. Define cuándo deben dejar de ejecutarse las tareas de mantenimiento asociadas con la ventana de mantenimiento mensual si aún no se han completado.</p>
    <p><strong>windowScheduleWeekdays=Matriz de dos valores entre 1 y 7 (por ejemplo, [5,5])</strong> El primer valor de la matriz es el día de inicio cuando se programa el trabajo y el segundo valor es el día de finalización cuando se detiene el trabajo. La hora exacta del inicio y la finalización se rige por windowStartTime y windowEndTime respectivamente.</p>
    <p><strong>windowFirstLastStartDay= 0/1</strong> 0 para programar en la primera semana del mes o 1 para programar en la última semana del mes. La ausencia de un valor programaría los trabajos todos los días, según se rige por windowScheduleWeekdays cada mes.</p>
    </td> 
    </tr>
    </tbody>
</table>

**Ubicaciones**:

* Diario: /apps/settings/granite/operations/maintenance/granite_daily
* Semanal: /apps/settings/granite/operations/maintenance/granite_weekly
* Mensual: /apps/settings/granite/operations/maintenance/granite_monthly

**Muestras de código**:

Muestra de código 1 (diario)

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

Muestra de código 2 (semanal)

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

Muestra de código 3 (mensual)

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
