---
title: Migración de código con asistencia de IA a AEM as a Cloud Service
description: Descripción general de la aptitud de migración de AEM Cloud y MCP, una solución de agente de IA que lee los hallazgos de BPA y migra el código de AEM 6.x a AEM as a Cloud Service, patrón a patrón.
feature: Migration
role: Developer
source-git-commit: 087017a7c0528f0806dfa8e8bd18a057a1763b14
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 1%

---


# Migración de código con asistencia de IA a AEM as a Cloud Service {#cloud-migration-skill-overview}

La solución **AEM Cloud Migration** es un conjunto de herramientas basadas en agentes que guía a los desarrolladores a través de la migración de AEM 6.x, AMS o código Java local y configuraciones OSGi a **AEM as a Cloud Service (AEMaaCS)**. Funciona dentro de cualquier IDE habilitado para IA que admite habilidades de agente y el Protocolo de contexto de modelo (MCP).

El siguiente vídeo de demostración proporciona una guía completa rápida de la solución de migración a AEM Cloud y se incluye como referencia.

>[!VIDEO](https://video.tv.adobe.com/v/3491438?learn=on)

La solución consta de dos componentes:

| Componente | Función |
|-----------|------|
| **Habilidad de migración** | Orquesta el flujo de trabajo de migración, obtiene resultados del Analizador de prácticas recomendadas (BPA), identifica los archivos afectados en el proyecto y aplica transformaciones de código patrón a patrón. Funciona con una exportación de CSV de BPA local o con el MCP de migración de la nube (recomendado). |
| **Migración de nube MCP** | Conecta su agente IDE a Cloud Acceleration Manager (CAM), lo que le permite recuperar conclusiones de BPA directamente sin una exportación de CSV. Recomendado con respecto a un CSV local para los resultados más actualizados. |

## Requisitos previos {#prerequisites}

- Un proyecto de AEM (Maven o Gradle) abierto en su IDE
- Una de las siguientes fuentes de búsqueda de BPA (se recomienda encarecidamente, no es necesaria para flujos manuales):
   - Una **exportación de CSV de BPA** desde su instancia de AEM
   - Un **proyecto de Cloud Acceleration Manager** con un informe de BPA cargado y el MCP de migración de nube configurado

## La aptitud para la migración {#migration-skill}

La habilidad de migración es una habilidad del agente para IDE habilitados para IA. Organiza un flujo de trabajo de **un patrón por sesión**: asigne un nombre al patrón que se va a corregir, señale los resultados de BPA al agente y este leerá las reglas de transformación relevantes, localice los archivos afectados en el proyecto y aplique los cambios en lotes de cinco, pausando para la revisión después de cada lote.

### Patrones admitidos {#supported-patterns}

| Patrón | Qué soluciona |
|---------|--------------|
| `scheduler` | Trabajos basados en `sling.commons.scheduler` incompatibles con el tiempo de ejecución sin estado de AEMaaCS |
| `resourceChangeListener` | Implementaciones de `ResourceChangeListener` que requieren actualizaciones de Cloud Service |
| `replication` | Se reemplazaron las llamadas heredadas a la API `Replicator` por equivalentes de `ContentDistribution` |
| `eventListener` | Implementaciones OSGi `EventListener` actualizadas para la semántica de eventos AEMaaCS |
| `eventHandler` | Servicios sincrónicos de OSGi `EventHandler` adaptados para Cloud Service |
| `assetApi` | Se reemplazaron las llamadas obsoletas a la API `AssetManager` y DAM por equivalentes compatibles |
| `htlLint` | `data-sly-test` advertencias de comparación de constantes redundantes en plantillas HTL |
| Configuraciones de OSGi | `.cfg.json` conversión, ámbito de modo de ejecución y extracción de secretos/env-var de Cloud Manager |

La aptitud delega todos los pasos de transformación de código en la aptitud `code-assessment` complementaria. Ambos se distribuyen juntos como el paquete de aptitudes `aem-cloud-service`; instale el paquete una vez para obtener ambos.

### Introducción {#getting-started-skill}

1. Instale el paquete de aptitudes `aem-cloud-service` desde el [repositorio de aptitudes de Adobe](https://github.com/adobe/skills).
2. Abra el proyecto de AEM como la raíz del espacio de trabajo en el IDE.
3. Obtener conclusiones de BPA: exporte un CSV de BPA o configure el MCP de migración de la nube (consulte a continuación).
4. Inicie una sesión con su agente mediante una de estas indicaciones:

   **CSV DE BPA:**

   ```
   Use the migration skill: scheduler only, BPA CSV at ./reports/bpa.csv
   ```

   **CAM a través de MCP:**

   ```
   Fix replictaion findings from project <projectname>/<projectId>.
   ```

   **Manual (sin BPA):**

   ```
   Migrate event listener in core/src/main/java/com/example/Listener.java
   ```

   **configuraciones de OSGi:**

   ```
   Scan my config files and create Cloud Manager environment secrets or variables.
   ```

   **HTL lint:**

   ```
   Fix htlLint in ui.apps - scan for data-sly-test redundant constant warnings.
   ```

>[!NOTE]
>La aptitud procesa un patrón por sesión. Si el informe de BPA contiene varios patrones, el agente le pedirá que elija uno antes de comenzar.

Para obtener una referencia de patrón completa y una guía de administración de sesiones, consulte [Uso de la habilidad de migración de nube](/help/journey-migration/cloud-migration-skill/using-cloud-migration-skill.md).

## El MCP de migración de nube {#cloud-migration-mcp}

El **MCP de migración de AEM Cloud** es un servidor [Model Context Protocol](https://modelcontextprotocol.io) que conecta su agente IDE con Cloud Acceleration Manager. Cuando se configura, la aptitud de migración puede recuperar los resultados de BPA directamente desde el proyecto CAM sin necesidad de descargar un CSV.

### Qué proporciona el MCP {#mcp-tools}

| Herramienta | Descripción |
|------|-------------|
| `fetch-cam-bpa-findings-by-pattern` | Devuelve los resultados de BPA para un patrón de migración de código específico a partir del último informe de BPA en un proyecto CAM. |
| `fetch-cam-bpa-findings-by-importance` | Devuelve todos los resultados de BPA con una gravedad determinada (`CRITICAL`, `MAJOR`, `ADVISORY`, `INFO`), ordenados por recuento. Útil para priorizar en qué patrones trabajar primero. |

La aptitud para migrar invoca automáticamente estas herramientas; no las llama directamente.

### Introducción {#getting-started-mcp}

1. En la configuración MCP del IDE, agregue la URL del servidor MCP de migración en la nube: `https://mcp.adobeaemcloud.com/adobe/mcp/cloud-migration`
2. Cuando se le pida, inicie sesión con su Adobe ID para autenticarse en Cloud Acceleration Manager.
3. La habilidad de migración ahora puede obtener resultados de BPA directamente de sus proyectos de CAM.

Para obtener información detallada sobre la configuración y la solución de problemas, consulte [Uso del MCP de migración a la nube](/help/journey-migration/cloud-migration-skill/using-cloud-migration-mcp.md).

## Cómo encajan en el Recorrido de migración {#migration-journey}

La aptitud y el MCP complementan las demás herramientas de la **fase de implementación**:

- **Analizador de prácticas recomendadas**: produce los resultados que impulsan la aptitud. Ver [Uso del Analizador de prácticas recomendadas](/help/journey-migration/best-practices-analyzer/using-best-practices-analyzer.md).
- **Cloud Acceleration Manager**: aloja informes de BPA y rastrea el progreso general de la migración. Consulte [Introducción a CAM](/help/journey-migration/cloud-acceleration-manager/using-cam/getting-started-cam.md).
- **Herramientas de refactorización**: administra la estructura del repositorio y la modernización de la configuración de Dispatcher. Consulte [Información general sobre herramientas de refactorización](/help/journey-migration/refactoring-tools/overview-refactoring-tools.md).
- **Herramienta de transferencia de contenido**: migra el contenido del repositorio de AEM 6.x a AEMaaCS.

Consulte la [Descripción general de la fase de implementación](/help/journey-migration/implementation.md) para obtener una imagen completa.

