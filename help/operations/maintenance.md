---
title: Tareas de mantenimiento en AEM as a Cloud Service
description: Obtenga información sobre las tareas de mantenimiento en AEM as a Cloud Service y cómo configurarlas.
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
feature: Operations
role: Admin
source-git-commit: f6e8066ecdfdbd0c7e79c2557dc19eec81657047
workflow-type: tm+mt
source-wordcount: '2042'
ht-degree: 30%

---


# Tareas de mantenimiento en AEM as a Cloud Service {#maintenance-tasks-in-aem-as-a-cloud-service}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_maintenance"
>title="Tareas de mantenimiento"
>abstract="Las tareas de mantenimiento son procesos que se ejecutan según una programación para optimizar el repositorio. Con AEM as a Cloud Service, la necesidad de que los clientes configuren las propiedades operativas de las tareas de mantenimiento es mínima. Los clientes pueden enfocar sus recursos en preocupaciones del nivel de la aplicación y dejar que Adobe se encargue de las operaciones de infraestructura."

Las tareas de mantenimiento son procesos que se ejecutan según una programación para optimizar el repositorio. Con AEM as a Cloud Service, la necesidad de que los clientes configuren las propiedades operativas de las tareas de mantenimiento es mínima. Los clientes pueden enfocar sus recursos en preocupaciones del nivel de la aplicación y dejar que Adobe se encargue de las operaciones de infraestructura.

## Configuración de tareas de mantenimiento {#maintenance-tasks-configuring}

En versiones anteriores de AEM, se podían configurar tareas de mantenimiento mediante la tarjeta de mantenimiento (Herramientas > Operaciones > Mantenimiento). La tarjeta de mantenimiento ya no está disponible para AEM as a Cloud Service, por lo que las configuraciones deben enviarse al control de origen e implementarse mediante Cloud Manager. Adobe administra las tareas de mantenimiento que tienen configuraciones que los clientes no pueden configurar (por ejemplo, Recopilación de elementos no utilizados del almacén de datos). Los clientes pueden configurar otras tareas de mantenimiento, como se describe en la tabla siguiente.

>[!CAUTION]
>
>Adobe se reserva el derecho de anular los ajustes de configuración de tareas de mantenimiento de un cliente para mitigar problemas como la degradación del rendimiento.

En la tabla siguiente se ilustran las tareas de mantenimiento disponibles.

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>Tarea de mantenimiento</th>
    <th>Quién posee la configuración</th>
    <th>Cómo se configura (opcional)</th>
  </tr>  
  <tr>
    <td>Recopilación de datos desechables del almacén de datos</td>
    <td>Adobe</td>
    <td>N/D: propiedad total de Adobe</td>
  </td> 
  </tr>
  <tr>
    <td>Depuración de la versión</td>
    <td>Cliente</td>
    <td>La depuración de versiones está deshabilitada de manera predeterminada, pero la directiva se puede configurar, tal como se describe en la sección <a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/maintenance#purge_tasks">Tareas de mantenimiento de purga de versiones y depuración de registros de auditoría</a>.<br/><br/>La depuración se habilitará pronto de manera predeterminada, con estos valores reemplazables.<br>
   </td>
  </td>
  </tr>
  <tr>
    <td>Purga del registro de auditoría</td>
    <td>Cliente</td>
    <td>La depuración del registro de auditoría está deshabilitada de manera predeterminada, pero la directiva se puede configurar, tal como se describe en la sección <a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/maintenance#purge_tasks">Tareas de mantenimiento de purga de versiones y depuración del registro de auditoría</a>.<br/><br/>La depuración se habilitará pronto de manera predeterminada, con estos valores reemplazables.<br>
   </td>
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
    <p>Debe hacerse en Git. Anule el nodo de configuración de la ventana de mantenimiento predeterminado en <code>/libs</code> creando propiedades en la carpeta <code>/apps/settings/granite/operations/maintenance/granite_weekly</code>, <code>granite_daily</code> o <code>granite_monthly</code>.</p>
    <p>Consulte la tabla Ventana de mantenimiento a continuación para obtener más información sobre la configuración. Habilite la tarea de mantenimiento añadiendo otro nodo bajo el nodo de arriba. Asígnele el nombre <code>granite_TaskPurgeTask</code>, con el atributo <code>sling:resourceType</code> establecido en <code>granite/operations/components/maintenance/task</code> y el atributo <code>granite.maintenance.name</code> establecido en <code>TaskPurge</code>. Configure las propiedades de OSGI; consulte <code>com.adobe.granite.taskmanagement.impl.purge.TaskPurgeMaintenanceTask</code> para ver la lista de propiedades.</p>
  </td>
  </tr>
    <tr>
    <td>Depuración de flujo de trabajo</td>
    <td>Cliente</td>
    <td>
    <p>Debe hacerse en Git. Anule el nodo de configuración de la ventana de mantenimiento predeterminado en <code>/libs</code> creando propiedades en la carpeta <code>/apps/settings/granite/operations/maintenance/granite_weekly</code>, <code>granite_daily</code> o <code>granite_monthly</code>. Consulte la tabla Ventana de mantenimiento a continuación para obtener más información sobre la configuración.</p>
    <p>Habilite la tarea de mantenimiento añadiendo otro nodo bajo el anterior (asígnele el nombre <code>granite_WorkflowPurgeTask</code>) con las propiedades adecuadas. Configure las propiedades de OSGI; consulte <a href="/help/sites-cloud/administering/workflows-administering.md#regular-purging-of-workflow-instances">Depuración regular de instancias de flujo de trabajo</a>.</p>
  </td>
  </tr>
  <tr>
    <td>Depuración del proyecto</td>
    <td>Cliente</td>
    <td>
    <p>Debe hacerse en Git. Anule el nodo de configuración de la ventana de mantenimiento predeterminado en <code>/libs</code> creando propiedades en la carpeta <code>/apps/settings/granite/operations/maintenance/granite_weekly</code>, <code>granite_daily</code> o <code>granite_monthly</code>. Consulte la tabla Ventana de mantenimiento a continuación para obtener más información sobre la configuración.</p>
    <p>Habilite la tarea de mantenimiento añadiendo otro nodo bajo el anterior (asígnele el nombre <code>granite_ProjectPurgeTask</code>) con las propiedades adecuadas. Consulte la lista de <a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi">Propiedades OSGi</a> para <b>Configuración de purga de proyectos Adobe</b> .</p>
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
  <p>Una tarea de mantenimiento no se puede ejecutar más de una vez durante este periodo de tiempo.</p>
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
    <p>Una tarea de mantenimiento no se puede ejecutar más de una vez durante este periodo de tiempo.</p>
    <p><strong>windowScheduleWeekdays= Matriz de dos valores entre 1 y 7 (por ejemplo, [5,5])</strong> El primer valor de la matriz es el día de inicio, cuando se programa el trabajo, y el segundo es el día de finalización, cuando se detiene el trabajo. La hora exacta del inicio y la finalización se rige por windowStartTime y windowEndTime respectivamente.</p>
    </td>
  </tr>
  <tr>
    <td>Mensual</td>
    <td>Cliente</td>
    <td>Definición del nodo JCR</td>
    <td>
    <p><strong>windowSchedule=month</strong> (este valor no debe cambiarse)</p>
    <p><strong>windowStartTime=HH:MM</strong> como reloj de 24 horas. Define cuándo deben comenzar a ejecutarse las tareas de mantenimiento asociadas con la ventana de mantenimiento mensual.</p>
    <p><strong>windowEndTime=HH:MM</strong> como reloj de 24 horas. Define cuándo deben dejar de ejecutarse las tareas de mantenimiento asociadas con la ventana de mantenimiento mensual si aún no se han completado.</p>
    <p>Una tarea de mantenimiento no se puede ejecutar más de una vez durante este periodo de tiempo.</p>
    <p><strong>windowScheduleWeekdays=Matriz de dos valores entre 1 y 7 (por ejemplo, [5,5])</strong> El primer valor de la matriz es el día de inicio, cuando se programa el trabajo, y el segundo es el día de finalización, cuando se detiene el trabajo. La hora exacta del inicio y la finalización se rige por windowStartTime y windowEndTime respectivamente.</p>
    <p><strong>windowFirstLastStartDay= 0/1</strong> 0 para programar en la primera semana del mes o 1 para programar en la última semana del mes. La ausencia de un valor programaría los trabajos en el día regido por windowScheduleWeekdays (cada mes).</p>
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

## Tareas de mantenimiento de purga de versiones y depuración de registros de auditoría {#purge-tasks}

La depuración de versiones y del registro de auditoría reduce el tamaño del repositorio y, en algunos casos, puede mejorar el rendimiento.

>[!NOTE]
>
>Los clientes de AEM Guides no deben configurar la depuración de versiones.

### Valores predeterminados {#defaults}

Actualmente, la depuración no está habilitada de forma predeterminada, pero esto cambiará en el futuro. Los entornos que se crearon antes de habilitar la depuración predeterminada tendrán un umbral más conservador para que la depuración no se produzca de forma inesperada. Consulte las secciones Depuración de versiones y Depuración del registro de auditoría a continuación para obtener más detalles sobre la política de depuración predeterminada.
<!-- Version purging and audit log purging are on by default, with different default values for environments with ids higher than **TBD** versus those with ids lower than that value. -->

<!-- ### Overriding the default values with a new configuration {#override} -->

Los valores de depuración predeterminados se pueden sobrescribir declarando un archivo de configuración e implementándolo como se describe a continuación.

<!-- The reason for this behavior is to clarify the ambiguity over whether the default purge values would take effect once you remove the declaration. -->

### Aplicación de una configuración {#configure-purge}

Declare un archivo de configuración e impleméntelo como se describe en los pasos siguientes.

>[!NOTE]
>Una vez implementado el nodo de depuración de versiones en el archivo de configuración, debe mantenerlo declarado y no eliminarlo. La canalización de configuración fallará si intenta hacerlo.
> 
>Del mismo modo, una vez que implemente el nodo de depuración del registro de auditoría en el archivo de configuración, debe mantenerlo declarado y no eliminarlo.

**1** Cree un archivo con el nombre `mt.yaml` o similar.

**2** Coloque el archivo en algún lugar bajo una carpeta de nivel superior llamada `config` o similar, como se describe en [Uso de canalizaciones de configuración](/help/operations/config-pipeline.md#folder-structure).

**3** - Declarar propiedades en el archivo de configuración, que incluyen:

* Algunas propiedades encima del nodo de datos. Consulte [Uso de canalizaciones de configuración](/help/operations/config-pipeline.md#common-syntax) para obtener una descripción. El valor de la propiedad `kind` debe ser *MaintenanceTasks* y la versión debe establecerse en *1*.

* un objeto de datos con `versionPurge` y `auditLogPurge` objetos.

Vea las definiciones y sintaxis de los objetos `versionPurge` y `auditLogPurge` a continuación.

La configuración es similar al siguiente ejemplo:

```
kind: "MaintenanceTasks"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  versionPurge:
    maximumVersions: 15
    maximumAgeDays: 20
    paths: ["/content"]
    minimumVersions: 1
    retainLabelledVersions: false
  auditLogPurge:
    rules:
      - replication:
          maximumAgeDays: 15
          contentPath: "/content"
          types: ["Activate", "Deactivate", "Delete", "Test", "Reverse", "Internal Poll"]
      - pages:
          maximumAgeDays: 15
          contentPath: "/content"
          types: ["PageCreated", "PageModified", "PageMoved", "PageDeleted", "VersionCreated", "PageRestored", "PageValid", "PageInvalid"]
      - dam:
          maximumAgeDays: 15
          contentPath: "/content"
          types: ["ASSET_EXPIRING", "METADATA_UPDATED", "ASSET_EXPIRED", "ASSET_REMOVED", "RESTORED", "ASSET_MOVED", "ASSET_VIEWED", "PROJECT_VIEWED", "PUBLISHED_EXTERNAL", "COLLECTION_VIEWED", "VERSIONED", "ADDED_COMMENT", "RENDITION_UPDATED", "ACCEPTED", "DOWNLOADED", "SUBASSET_UPDATED", "SUBASSET_REMOVED", "ASSET_CREATED", "ASSET_SHARED", "RENDITION_REMOVED", "ASSET_PUBLISHED", "ORIGINAL_UPDATED", "RENDITION_DOWNLOADED", "REJECTED"]
```

Tenga en cuenta que para que la configuración sea válida:

* todas las propiedades deben estar definidas. No hay valores predeterminados heredados.
* se deben respetar los tipos (enteros, cadenas, booleanos, etc.) de las tablas de propiedades siguientes.

**4**: cree una canalización de configuración en Cloud Manager, tal como se describe en el artículo [canalización de configuración](/help/operations/config-pipeline.md#managing-in-cloud-manager).

### Depuración de la versión {#version-purge}

>[!NOTE]
>
>Los clientes de AEM Guides no deben configurar la depuración de versiones.

#### Valores predeterminados de depuración de versión {#version-purge-defaults}

<!-- For version purging, environments with an id higher than **TBD** have the following default values: -->

Actualmente, la depuración no está habilitada de forma predeterminada, pero esto cambiará en el futuro.

Los entornos que se crearon después de habilitar la depuración predeterminada tendrán los siguientes valores predeterminados:

* Se eliminan las versiones con más de 30 días.
* Se conservan las cinco versiones más recientes de los últimos 30 días.
* Independientemente de las reglas anteriores, se conserva la versión más reciente (además del archivo actual).

<!-- Environments with an id equal or lower than **TBD** will have the following default values: -->

Los entornos que se crearon antes de habilitar la depuración predeterminada tendrán los valores predeterminados que se enumeran a continuación, pero se recomienda reducir esos valores para optimizar el rendimiento.

* Se eliminan las versiones anteriores a 7 años.
* Se conservan todas las versiones de los últimos 7 años.
* Después de 7 años, se eliminan otras versiones que no sean la más reciente (además del archivo actual).

#### Propiedades de purga de versiones {#version-purge-properties}

Las propiedades permitidas se enumeran a continuación.

Las columnas que indican *default* indican los valores predeterminados en el futuro, cuando se apliquen los valores predeterminados; *TBD* refleja un identificador de entorno que aún no se ha determinado.

| Propiedades | valor predeterminado futuro para envs>TBD | valor predeterminado futuro para envs&lt;=TBD | Requerido | tipo | Valores |
|-----------|--------------------------|-------------|-----------|---------------------|-------------|
| rutas | [&quot;/content&quot;] | [&quot;/content&quot;] | Sí | matriz de cadenas | Especifica en qué rutas purgar versiones cuando se crean nuevas versiones.  Los clientes deben declarar esta propiedad, pero el único valor permitido es &quot;/content&quot;. |
| maximumAgeDays | 30 | 2557 (7 años + 2 días bisiestos) | Sí | Entero | Se elimina cualquier versión anterior al valor configurado. Si el valor es 0, la depuración no se realiza según la antigüedad de la versión. |
| maximumVersions | 5 | 0 (sin límite) | Sí | Entero | Se elimina cualquier versión anterior a la n-ª versión más reciente. Si el valor es 0, la depuración no se realiza según el número de versiones. |
| minimumVersions | 1 | 1 | Sí | Entero | El número mínimo de versiones que se conservan independientemente de la edad. Tenga en cuenta que siempre se conserva al menos 1 versión; su valor debe ser 1 o superior. |
| keepLabelsVersioned | false | false | Sí | booleano | Determina si se excluirán de la depuración las versiones etiquetadas explícitamente. Para mejorar la optimización del repositorio, se recomienda establecer este valor en false. |


**Interacciones de propiedades**

Los siguientes ejemplos ilustran cómo interactúan las propiedades al combinarse.

Ejemplo:

```
maximumAgeDays = 30
maximumVersions = 10
minimumVersions = 2
```

Si hay 11 versiones el día 23, la versión más antigua se purgará la próxima vez que se ejecute la tarea de mantenimiento de purga, ya que la propiedad `maximumVersions` está establecida en 10.

Si hay 5 versiones en el día 31, solo se purgarán 3, ya que la propiedad `minimumVersions` está establecida en 2.

Ejemplo:

```
maximumAgeDays = 30
maximumVersions = 0
minimumVersions = 1
```

No se purgarán versiones posteriores a los 30 días debido a que la propiedad `maximumVersions` está establecida en 0.

Se conservará una versión con más de 30 días.

### Purga del registro de auditoría {#audit-purge}

#### Valores predeterminados de purga del registro de auditoría {#audit-purge-defaults}

<!-- For audit log purging, environments with an id higher than **TBD** have the following default values: -->

Actualmente, la depuración no está habilitada de forma predeterminada, pero esto cambiará en el futuro.

Los entornos que se crearon después de habilitar la depuración predeterminada tendrán los siguientes valores predeterminados:

* Se eliminan los registros de replicación, DAM y auditoría de página anteriores a 7 días.
* Se registran todos los eventos posibles.

<!-- Environments with an id equal or lower than **TBD** will have the following default values: -->

Los entornos que se crearon antes de habilitar la depuración predeterminada tendrán los valores predeterminados que se enumeran a continuación, pero se recomienda reducir esos valores para optimizar el rendimiento.

* Se eliminan los registros de replicación, DAM y auditoría de página anteriores a 7 años.
* Se registran todos los eventos posibles.

>[!NOTE]
>Se recomienda que los clientes, que tienen requisitos regulatorios para producir registros de auditoría no editables, se integren con servicios externos especializados.

#### Propiedades de purga del registro de auditoría {#audit-purge-properties}

Las propiedades permitidas se enumeran a continuación.

Las columnas que indican *default* indican los valores predeterminados en el futuro, cuando se apliquen los valores predeterminados; *TBD* refleja un identificador de entorno que aún no se ha determinado.


| Propiedades | valor predeterminado futuro para envs>TBD | valor predeterminado futuro para envs&lt;=TBD | Requerido | tipo | Valores |
|-----------|--------------------------|-------------|-----------|---------------------|-------------|
| reglas | - | - | Sí | Objeto | Uno o más de los siguientes nodos: replicación, páginas, DAM. Cada uno de estos nodos define reglas, con las propiedades a continuación. Todas las propiedades deben declararse. |
| maximumAgeDays | 7 días | para todos, 2557 (7 años + 2 días bisiestos) | Sí | integer | Para replicación, páginas o dam: número de días que se guardan los registros de auditoría. Los registros de auditoría anteriores al valor configurado se depuran. |
| contentPath | &quot;/content&quot; | &quot;/content&quot; | Sí | Cadena | Ruta de acceso en la que se purgarán los registros de auditoría, para el tipo relacionado. Debe establecerse en &quot;/content&quot;. |
| tipos | todos los valores | todos los valores | Sí | Matriz de enumeración | Para **replication**, los valores enumerados son: Activate, Deactivate, Delete, Test, Reverse, Internal Poll. Para **páginas**, los valores enumerados son: PageCreated, PageModified, PageMoved, PageDeleted, VersionCreated, PageRestored, PageRolled Out, PageValid, PageInvalid. Para **dam**, los valores enumerados son: ASSET_EXPIRING, METADATA_UPDATED, ASSET_EXPIRED, ASSET_REMOVED, RESTORED, ASSET_MOVED, ASSET_VIEWED, PROJECT_VIEWED, PUBLISHED_EXTERNAL, COLLECTION_VIEWED, VERSIONED, ADDED_COMMENT, RENDITION_UPDATED, ACCEPTED, DOWNLOADED, SUBASSET_UPDATED, SUBASSET_REMOVED, ASSET_CREATED, ASSET_SHARED, RENDITION_REMOVED, ASSET_PUBLISHED, ORIGINAL_UPDATED, RENDITION_DOWNLOADED, REJECTED. |
