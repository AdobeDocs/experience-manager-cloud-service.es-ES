---
title: Actualizar los fragmentos de contenido para referencias de UUID
description: Obtenga información sobre cómo actualizar los fragmentos de contenido para referencias de UUID optimizadas en Adobe Experience Manager as a Cloud Service para la entrega de contenido sin encabezado.
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
exl-id: 004d1340-8e3a-4e9a-82dc-fa013cea45a7
source-git-commit: fdfe0291ca190cfddf3bed363a8c2271a65593a1
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 2%

---

# Actualizar los fragmentos de contenido para referencias de UUID {#upgrade-content-fragments-for-UUID-references}

Para optimizar la estabilidad de los filtros de GraphQL, puede actualizar el contenido y las referencias de fragmento en los fragmentos de contenido para que utilicen identificadores únicos universales (UUID).

Originalmente, los modelos de fragmentos de contenido proporcionaban los tipos de datos de **Referencia de contenido** y **Referencia de fragmento**. Ambas referencias utilizan una ruta que apunta al recurso al que se hace referencia y esta ruta puede quedar obsoleta si se mueve el recurso. Aunque estas referencias son más que suficientes en la mayoría de los casos, los modelos de fragmentos de contenido se han ampliado para proporcionar también referencias basadas en un UUID:

* **Referencia de contenido (UUID)**
* **Referencia de fragmento (UUID)**.

Estos nuevos tipos de referencia se pueden utilizar tanto en nuevos modelos de fragmentos de contenido como en fragmentos, y para ampliar las instancias existentes.

Para actualizar los fragmentos y modelos de contenido existentes, puede ejecutar el procedimiento documentado aquí.

>[!CAUTION]
>
>Antes de ejecutar el procedimiento de actualización, siempre debe [ejecutar una ejecución en seco](#execute-a-dry-run) para resaltar cualquier posible problema con el contenido.

## Qué se actualiza {#what-is-upgraded}

Se realizan las siguientes actualizaciones:

* Campos de los tipos de datos:
   * **Las referencias de contenido** se han convertido en **referencias de contenido (UUID)**
   * **La referencia de fragmento** se ha convertido en **referencia de fragmento (UUID)**
* Los valores de las referencias basadas en rutas que se mantienen en estos campos se sustituyen por los UUID correspondientes

>[!NOTE]
>
>Después de la actualización, ambos tipos de datos seguirán estando disponibles en el editor del modelo de fragmentos de contenido. Puede crear nuevos campos basados en ambos tipos (aunque se prevé que utilizará los tipos basados en UUID) y volver a ejecutar la actualización si es necesario.

## Qué NO se actualiza {#what-is-not-upgraded}

Las siguientes referencias no se actualizan:

* Referencias de página: los UUID aún no son compatibles
* Cualquier referencia no válida; por ejemplo, donde el destino de la ruta del fragmento de contenido o la ruta del recurso no existe

   * Las referencias no válidas no se actualizan, ya que si la ruta del fragmento de contenido o la ruta del recurso no es válida, no hay un UUID correspondiente para asignar. La referencia original permanece intacta.

   * Use una [ejecución en seco](#execute-a-dry-run) para detectar referencias no válidas.

  >[!NOTE]
  >
  >Al no ser válidos, no se pueden utilizar, independientemente de la actualización.

## Cuándo no se debe actualizar {#when-you-should-not-upgrade}

No actualizar:

* Cuando cualquiera de los fragmentos de contenido utiliza referencias de página; como, los UUID aún no son compatibles con las referencias de página

## Limitaciones de referencias de UUID {#limitations-of-uuid-references}

Actualmente, se aplican las siguientes limitaciones al utilizar referencias basadas en un UUID:

* Modelos

   * Los nuevos modelos de fragmentos de contenido con campos UUID de fragmento de contenido o UUID de referencia de contenido no se pueden crear mediante OpenAPI.
   * El campo `id` de los modelos no se ha cambiado para que se base en UUID. Utiliza la ruta descodificada base64 del modelo. Los modelos no se pueden mover, por lo tanto, este valor sigue siendo estable.

* Recursos

   * Al crear un fragmento de contenido mediante OpenAPI, se deben usar los tipos de campo `fragment-reference` o `content-reference` para especificar referencias a un fragmento o recurso respectivamente, incluso al establecer el valor de un campo de referencia basado en UUID.

## Planificación de actualización {#upgrade-planning}

Antes de ejecutar la actualización hay que realizar algunos pasos de preparación.

### Ejecutar una ejecución en seco {#execute-a-dry-run}

Se recomienda que *cada* vez que actualice el contenido, realice primero una ejecución sin interrupciones. Esto creará archivos de registro con entradas que resaltan cualquier problema potencial:

* Referencias no válidas
* Referencias de página

Ejecute la actualización de contenido en el modo `dryRun` para:

* identificar referencias no válidas; enumerándolas en los archivos de registro
A continuación, puede corregir estas referencias antes de ejecutar la actualización de contenido real.
* identificar cualquier referencia de página; enumerándolas en los archivos de registro
Cuando se detecten referencias de página, [no debería ejecutar la actualización de contenido](#when-you-should-not-upgrade).


### Aplicar la congelación de contenido {#enforce-a-content-freeze}

La ejecución de la actualización de contenido debe planificarse durante un periodo de congelación de contenido.

La duración de la congelación de contenido depende del volumen de fragmentos de contenido que se actualicen. Por lo tanto, la actualización puede variar desde unos minutos hasta unas pocas horas, y también depende de los parámetros utilizados al iniciar la actualización de contenido.

## Ejecución de la actualización de contenido {#running-the-content-upgrade}

La actualización de contenido se puede administrar mediante el extremo: `/libs/dam/cfm/maintenance.json`

>[!NOTE]
>
>Su cuenta necesita el rol `Administrator` para tener acceso al extremo.

### Iniciar una actualización de contenido {#start-a-content-upgrade}

| Punto final | Tipo de solicitud HTTP | Comentar |
|--- |--- |--- |
| `/libs/dam/cfm/maintenance.json` | `POST` | |
| **Parámetros de solicitud** | **Valor** | |
| acción | `start` | |
| serviceTypeId | `uuidUpgradeService` | El ID de tipo de servicio (predefinido, valor fijo). |
|  segmentSize | `1000` | El número de fragmentos de contenido o modelos que se actualizarán en un segmento (lote). |
| basePath | `/conf` | Especifique una de estas opciones:<ul><li>la raíz `/conf` para actualizar todas las configuraciones de AEM</li><li>una ruta de configuración de AEM seleccionada. para el cual se ejecuta la actualización de contenido<br>Por ejemplo: `/conf/wknd-shared` solo actualiza el inquilino único `wknd-shared`</li></ul> |
| intervalo | `10` | Intervalo en segundos, después del cual se actualiza el siguiente segmento de fragmentos de contenido o modelos. |
| modo | `replicate`, `noReplicate` | <ul><li>`replicate`: replica el mismo trabajo en todas las instancias de publicación de AEM</li><li>`noReplicate`: solo ejecuta el trabajo en instancias de autor de AEM</li></ul> |
| dryRun |  `true`, `false` | <ul><li>`false`: simular la actualización de contenido, sin guardar ningún cambio de contenido</li><li>`true`: realice la actualización de contenido y guarde los cambios del contenido</li></ul> |
| **Detalles de la respuesta** | **Valor** | |
| jobId | `UUID` |  El ID del trabajo que ejecuta la actualización de contenido.<ul><li>Este ID es necesario en cualquier llamada posterior relacionada con esta ejecución.</li><li>Si el valor `mode` está establecido en `replicate`, la ejecución en instancias de publicación de AEM también debe estar en el mismo `jobId`.</li></ul> |
| parámetros | Los parámetros de actualización de contenido | Estos incluyen los parámetros iniciales proporcionados para iniciar la actualización del contenido y algunos valores predeterminados internos. |


### Ejemplo de solicitud de actualización de contenido {#example-content-upgrade-request}

+++Solicitud

```http
POST http://localhost:4502/libs/dam/cfm/maintenance.json
Content-Type: application/json
Authorization: _REPLACE_WITH_VALID_AUTH_
Accept: application/json
 
{
    "action": "start",
    "serviceTypeId": "uuidUpgradeService",
    "segmentSize": 1000,
    "basePath": "/conf/wknd-shared",
    "interval": 10,
    "mode": "replicate",
    "dryRun": true
}
```

+++

+++Respuesta

```http
HTTP/1.1 200 OK
Date: Wed, 16 Oct 2024 14:34:37 GMT
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
Content-Type: application/json
Content-Length: 386
 
{
  "jobId": "91af43a6-63ff-45e5-ac7b-06ccf565bdfa",
  "jcr:created": 1729089277309,
  "parameters": {
    "mode": "replicate",
    "dryRun": true,
    "segmentSize": 1000,
    "serviceTypeId": "uuidUpgradeService",
    "action": "start",
    "basePath": "/conf/wknd-shared",
    "topic": "cfm/maintenance",
    "interval": 10,
    "cronSchedule": "*/10 * * * * ?"
  }
}
```

+++

### Obtener el estado de una actualización de contenido {#get-the-status-of-a-content-upgrade}

| Punto final | Tipo de solicitud HTTP | Comentar |
|--- |--- |--- |
| `/libs/dam/cfm/maintenance.json` | `GET` | |
| **Parámetros de solicitud** | **Valor** | |
| acción | status | |
| jobId | `<UUID>` | `jobId` que se devolvió desde la llamada para iniciar la actualización de contenido. |
| **Detalles de la respuesta** | **Valor** | |
| status | Valores JSON | Contiene el estado detallado de la actualización de contenido:<ul><li>Se actualiza después de cada intervalo (segundos).</li><li>La ejecución de `uuidUpgradeService` tiene dos fases:<ol><li>fase 0 para actualizar los modelos de fragmento de contenido</li><li>fase-1 para actualizar fragmentos de contenido</li></ol></li><li>En cada fase, las estadísticas se actualizan después de cada intervalo.</li><li>&quot;jobStatus&quot;: &quot;COMPLETADO&quot; marca la actualización como completada correctamente.</li><li>Otros valores de estado se explican por sí mismos.</li></ul> |

### Ejemplo de solicitud de estado de actualización de contenido {#example-content-upgrade-status-request}

+++Solicitud

```http
GET http://localhost:4502/libs/dam/cfm/maintenance.json?action=status&jobId=91af43a6-63ff-45e5-ac7b-06ccf565bdfa
Authorization: _REPLACE_WITH_VALID_AUTH_
Accept: application/json
```

+++

+++Respuesta

```http
HTTP/1.1 200 OK
Date: Wed, 16 Oct 2024 14:35:51 GMT
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
Content-Type: application/json
Content-Length: 1116
 
{
  "jobId": "91af43a6-63ff-45e5-ac7b-06ccf565bdfa",
  "jcr:created": 1729089277309,
  "eventProcessed": 1,
  "parameters": {
    "mode": "replicate",
    "dryRun": true,
    "segmentSize": 1000,
    "serviceTypeId": "uuidUpgradeService",
    "action": "start",
    "confPath": "/conf/wknd-shared",
    "topic": "cfm/uuid-migration",
    "interval": 10,
    "cronSchedule": "*/10 * * * * ?"
  },
  "status": {
    "jobStatus": "COMPLETED",
    "lastModified": 1729089310301,
    "currentPhaseIndex": 1,
    "phases": {
      "phase-0": {
        "bookmark": 1727183332520,
        "stats": {
          "successCount": 2,
          "skippedCount": 1,
          "errorCount": 0
        },
        "name": "modelUpgrade",
        "lastModified": 1729089290040,
        "isCompleted": true
      },
      "phase-1": {
        "bookmark": 1727183347990,
        "stats": {
          "successCount": 29,
          "skippedCount": 0,
          "errorCount": 1
        },
        "name": "cfUpgrade",
        "lastModified": 1729089310298,
        "isCompleted": true
      }
    }
  }
}
```

+++

+++Archivos de registro de muestra

Además del estado de una actualización de contenido en ejecución obtenida del extremo HTTP, los registros de AEM proporcionan información detallada del progreso en el nivel de contenido. Por ejemplo:

```xml
#Successful model upgrade
com.adobe.cq.dam.cfm.impl.servicing.uuid.* Phase phase-0: resource: /conf/wknd-shared/settings/dam/cfm/models/article , status: SUCCESS, skips: [], errors: []
 
#Successful content fragment upgrade
com.adobe.cq.dam.cfm.impl.servicing.uuid.* Phase phase-1: resource: /content/dam/wknd-shared/en/magazine/san-diego-surf-spots/san-diego-surfspots , status: SUCCESS, skips: [], errors: []
 
#Unsuccessful/Skipped model upgrade
com.adobe.cq.dam.cfm.impl.servicing.uuid.* Phase phase-0: resource: /conf/wknd-shared/settings/dam/cfm/models/adventure , status: SKIPPED, skips: [Model: '/conf/wknd-shared/settings/dam/cfm/models/adventure', no upgradeable fields found], errors: []
 
#Unsuccessful content fragment upgrade
com.adobe.cq.dam.cfm.impl.servicing.uuid.* Phase phase-1: resource: /content/dam/wknd-shared/en/magazine/western-australia/western-australia-by-camper-van , status: FAILED, skips: [], errors: [Path '/content/dam/wknd-shared/en/magazine/western-australia/western-australia-by-camper-van', Variation: 'master' Field 'featuredImage', Value '/content/dam/wknd-shared/en/magazine/western-australia/adobestock_156407519.jpeg' is invalid; will not upgrade this field.] 
```

Además, después del procesamiento de cada segmento (lote) de fragmentos de contenido y modelos, se registra un estado acumulado, que resume el progreso hasta el momento. Por ejemplo:

```xml
com.adobe.cq.dam.cfm.impl.servicing.PhaseChainProcessor Phase phase-x, processed a segment, stats: {successCount=29, skippedCount=0, errorCount=1}
```

+++

### Anulación de una actualización de contenido {#abort-a-content-upgrade}

>[!CAUTION]
>
>Cancelación de una actualización de contenido (que no es una ejecución seca):
>
>* no revierte ningún cambio ya realizado
>* podría dejar el contenido en un estado mixto
>
>Utilice esta acción con precaución.

| Punto final | Tipo de solicitud HTTP | Comentar |
|--- |--- |--- |
| `/libs/dam/cfm/maintenance.json` | `POST` | |
| **Parámetros de solicitud** | **Valor** | |
| acción | abort | |
| jobId | `<UUID>` | `jobId` que se devolvió desde la llamada para iniciar la actualización de contenido. |
| **Detalles de la respuesta** | **Valor** | |
| status | Valores JSON | Contiene el estado detallado de la actualización de contenido:<ul><li>El estado que se debe tener en cuenta es &quot;jobStatus&quot;: &quot;ABORTADO&quot;.<br>Después de una acción de anulación, los segmentos de datos pendientes no se procesarán.</li><li>Si el jobStatus está &quot;COMPLETADO&quot; antes de una anulación, la llamada no tiene ningún efecto.</li></ul> |

### Ejemplo de anulación de una solicitud de actualización de contenido {#example-abort-content-upgrade-request}

+++Solicitud

```http
POST http://localhost:4502/libs/dam/cfm/maintenance.json
Content-Type: application/json
Authorization: Basic YWRtaW46YWRtaW4=
Accept: application/json
 
{
    "action": "abort",
    "jobId": "b1dbf6f9-5f59-4007-b631-01b63cd17807"
    "mode": "replicate",
}
```

+++

+++Respuesta

```http
HTTP/1.1 200 OK
Date: Wed, 16 Oct 2024 14:39:03 GMT
 
{
  "jobId": "b1dbf6f9-5f59-4007-b631-01b63cd17807",
   ...
  "eventProcessed": 2,
  "parameters": {
    ...
    "abort": true,
    ...
  },
  "status": {
     "jobStatus": "ABORTED",
    ...
  }
}
```

+++
