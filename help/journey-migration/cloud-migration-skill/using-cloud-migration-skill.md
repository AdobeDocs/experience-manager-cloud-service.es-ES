---
title: Uso de la habilidad de migración de AEM Cloud
description: Referencia para cada patrón de migración admitido por la aptitud de migración de AEM Cloud, incluida la conversión de la configuración de OSGi, las opciones de fuentes de BPA y las directrices de administración de sesiones.
feature: Migration
role: Developer
source-git-commit: 7ea634871fc1655e5f0ec5b3fb88edbb0f317249
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 0%

---


# Uso de la habilidad de migración de AEM Cloud {#using-cloud-migration-skill}

Esta referencia abarca cada patrón de migración admitido, cómo proporcionar conclusiones de BPA y cómo administrar las sesiones en un proyecto grande. Para obtener instrucciones de introducción y configuración, consulte la [descripción general](/help/journey-migration/cloud-migration-skill/overview-cloud-migration-skill.md).

## Cómo funciona una sesión {#workflow-overview}

Cada sesión de migración sigue esta secuencia:

1. **Asigne un nombre al patrón**: especifique un patrón (por ejemplo, `scheduler`)
2. **Proporcione resultados**: desde un archivo CSV de BPA, CAM a través de MCP o rutas de acceso a archivos específicas
3. **El agente lee las reglas de transformación**: la aptitud lee las reglas de transformación relevantes de la aptitud de `code-assessment` acompañante antes de realizar cualquier cambio de código
4. **Primer lote de cinco**: el agente transforma hasta cinco resultados e informa de los cambios
5. **Usted revisa y continúa**: después de revisar cada lote, responda `continue` para continuar con el siguiente

El agente procesa un patrón y un lote a la vez. No se realiza automáticamente; cada lote requiere su confirmación.

## Patrones de migración {#patterns}

### Planificador {#scheduler}

Se dirige a clases Java que utilizan la inyección `sling.commons.scheduler` o `Scheduler` que son incompatibles con el tiempo de ejecución en contenedores sin estado de AEMaaCS.

**Id. de patrón BPA:** `scheduler`

El agente convierte los trabajos insertados por `Scheduler` en `@Component` implementaciones de `Runnable` mediante `@Designate`, reemplazando el registro de programador basado en constructor con los métodos de ciclo de vida `@Activate` / `@Deactivate`.

### ResourceChangeListener {#resource-change-listener}

Se dirige a `ResourceChangeListener` o `ResourceChange` implementaciones de escucha que requieren actualizaciones para AEMaaCS.

**Id. de patrón BPA:** `resourceChangeListener`

### Replicación {#replication}

Clases de destino que importan `com.day.cq.replication.Replicator` o API de replicación relacionadas, que no se admiten en AEMaaCS. El agente los reemplaza con equivalentes basados en `ContentDistribution` y actualiza las referencias del servicio OSGi correspondientes.

**Id. de patrón BPA:** `replication`

### Escuchador de eventos {#event-listener}

Se dirige a implementaciones OSGi `EventListener` o `EventHandler` que deben actualizarse para la semántica del procesamiento de eventos AEMaaCS.

**Id. de patrón BPA:** `eventListener`

### Controlador de eventos {#event-handler}

Se dirige a servicios sincrónicos de OSGi `EventHandler` que deben adaptarse para AEMaaCS.

**Id. de patrón BPA:** `eventHandler`

### API de recursos {#asset-api}

Clases de Target que utilizan `AssetManager`, `DAMEvent` o API de DAM no admitidas en desuso. El agente los reemplaza por los equivalentes de API de AEM Assets admitidos.

**Id. de patrón BPA:** `assetApi`

### HTL Lint (data-sly-test) {#htl-lint}

Se dirige a plantillas HTL en `ui.apps` que producen `data-sly-test: redundant constant value comparison` advertencias de pelusa. El agente detecta las plantillas afectadas analizando el paquete de contenido directamente; este patrón no requiere una conexión CSV o CAM de BPA.

**Id. de patrón BPA:** `htlLint`

>[!NOTE]
>Los resultados de `htlLint` no aparecen en las exportaciones de CSV de BPA. El agente los descubre a través del análisis directo de archivos cuando inicia una sesión para este patrón.

### Configuraciones de OSGi para Cloud Manager {#osgi-cloud-manager}

Convierte las configuraciones de OSGi en `ui.config` al formato `.cfg.json` compatible con Cloud Manager con un control completo específico del entorno. Esto cubre dos tareas relacionadas:

**Conversión de formato de configuración**

AEMaaCS requiere que las configuraciones de OSGi se almacenen como archivos de `.cfg.json`, con configuraciones específicas del entorno en carpetas con ámbitos en modo de ejecución (`config.author/`, `config.publish/`, `config.dev/`, etc.). El agente:

* Convierte las configuraciones existentes de OSGi de `.config`, `.cfg` y formato XML a `.cfg.json`
* Divide las configuraciones que contienen valores específicos de autor y publicación en archivos con ámbitos de modo de ejecución independientes
* Valida los tipos de propiedad con la especificación del tipo de metal OSGi (cadenas, enteros, booleanos, matrices)
* Indica los PID propiedad de Adobe para su revisión manual en lugar de convertirlos automáticamente

**Secretos y variables de entorno**

Quita los secretos de texto sin formato y los valores específicos del entorno de los archivos de configuración confirmados y los reemplaza por marcadores de posición de Cloud Manager:

* `$[secret:NAME]`: para contraseñas, tokens y otros valores confidenciales
* `$[env:NAME]`: para valores no confidenciales que difieren por entorno (por ejemplo, direcciones URL de servicio)

Las variables y los secretos correspondientes se aplican en Cloud Manager y se insertan durante la ejecución; no se almacena ningún valor en el control de código fuente.

>[!IMPORTANT]
>El agente nunca emite valores secretos en la conversación. Todos los datos confidenciales se escriben en un archivo de transferencia ignorado para que los aplique a través de la API o la IU de Cloud Manager.

**Este patrón no utiliza CSV o CAM de BPA.** Inicie una sesión con:

```
Scan my config files and create Cloud Manager environment secrets or variables.
```

## Opciones de Source de BPA {#bpa-source}

| Origen | Cuándo se usa |
|--------|------------|
| **archivo CSV de BPA** | Ha exportado un CSV desde su instancia de AEM o Cloud Acceleration Manager. Proporcione la ruta de acceso al iniciar la sesión. |
| **CAM a través de MCP** | Tiene configurado el MCP de migración de AEM Cloud. El agente enumera sus proyectos CAM, usted confirma cuál utilizar y los resultados se recuperan directamente. Consulte [Uso del MCP de migración de nube](/help/journey-migration/cloud-migration-skill/using-cloud-migration-mcp.md). |
| **Rutas de archivo manuales** | Desea migrar archivos específicos sin un informe de BPA. Proporcione las rutas directamente en el mensaje. |

### Gestión de errores de MCP {#mcp-errors}

Si la conexión MCP devuelve un error (incluidos los errores de autenticación o los que no se encuentran en el proyecto), el agente se detiene y le muestra el error. No cambia automáticamente a otra fuente. Desde el estado detenido, puede:

* Confirme el proyecto correcto de la lista que muestra el agente
* Proporcione una ruta CSV de BPA como alternativa
* Proporcionar rutas de archivo Java específicas para una migración manual

## Administración de sesiones en informes grandes {#large-reports}

Para los informes de BPA con muchas conclusiones, el método por lotes le permite validar de forma incremental:

1. Revisar la diferencia de cada lote
2. Confirmar el lote con un mensaje de confirmación de ámbito de patrón
3. Responder `continue` para iniciar el siguiente lote
4. Repita el proceso hasta que el agente informe de que se han realizado todos los resultados del patrón

**Un patrón por confirmación** mantiene el historial de Git legible y hace que las transformaciones de patrones individuales sean fáciles de revertir si es necesario.

>[!NOTE]
>Si finaliza una sesión antes de que se procesen todos los resultados, reinicie con el mismo patrón y origen de BPA en una nueva sesión. El agente se reanuda desde donde lo dejó.

## Ámbito de Workspace {#workspace-scope}

El agente busca y edita archivos sólo en las carpetas abiertas del espacio de trabajo del IDE. No analiza los directorios principales, las carpetas del mismo nivel ni otras ubicaciones del disco.

Si un hallazgo de BPA hace referencia a una ruta de archivo que no existe en el espacio de trabajo, el agente se detiene y le informa de qué rutas faltan. Abra la carpeta de proyecto correcta o proporcione las rutas explícitamente para continuar.

