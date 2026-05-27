---
title: Uso del MCP de migración de AEM Cloud
description: Obtenga información sobre cómo añadir el servidor MCP de migración de AEM Cloud a su IDE con IA habilitada y utilizarlo para recuperar los resultados del Analizador de prácticas recomendadas de Cloud Acceleration Manager durante una sesión de migración.
feature: Migration
role: Developer
source-git-commit: f3f81e043b95576bbd1d236645a562668c355e76
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 1%

---


# Uso del MCP de migración de AEM Cloud {#using-cloud-migration-mcp}

El **MCP de migración de AEM Cloud** es un servidor [Model Context Protocol (MCP)](https://modelcontextprotocol.io) alojado que conecta su agente IDE con **Cloud Acceleration Manager (CAM)**. Una vez configurada, la [aptitud de migración de AEM Cloud](/help/journey-migration/cloud-migration-skill/overview-cloud-migration-skill.md) puede recuperar los resultados del Analizador de prácticas recomendadas directamente desde el proyecto CAM sin necesidad de exportar a CSV.

## URL del servidor MCP {#server-url}

```
https://mcp.adobeaemcloud.com/adobe/mcp/cloud-migration
```

Agregue esta URL a la configuración MCP de su IDE para conectarse.

## Qué proporciona {#what-it-provides}

El servidor MCP expone dos herramientas que la aptitud de migración invoca automáticamente durante una sesión:

| Herramienta | Descripción |
|------|-------------|
| `fetch-cam-bpa-findings-by-pattern` | Devuelve los resultados de BPA de un patrón de migración específico (`scheduler`, `assetApi`, `eventListener`, `resourceChangeListener`, `eventHandler` o `all`) del último informe de BPA de un proyecto CAM. |
| `fetch-cam-bpa-findings-by-importance` | Devuelve todos los resultados de BPA con una gravedad determinada (`CRITICAL`, `MAJOR`, `ADVISORY`, `INFO`) del último informe de BPA, ordenados en orden descendente. Útil para priorizar qué patrones abordar primero. |

## Requisitos previos {#prerequisites}

* Un proyecto de **Cloud Acceleration Manager** con un informe de BPA cargado. Consulte [Fase de preparación para CAM](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md).
* Un **Adobe ID** con acceso a ese proyecto CAM.
* Un IDE habilitado para IA que admite servidores MCP remotos.

## Configuración {#setup}

1. En la configuración MCP del IDE, agregue una nueva entrada de servidor MCP con la dirección URL `https://mcp.adobeaemcloud.com/adobe/mcp/cloud-migration`.
2. Guarde o active la configuración de modo que el IDE se conecte al servidor.
3. Cuando se le pida, inicie sesión con su **Adobe ID** para completar la autenticación.
4. Una vez autenticado, el IDE detecta las herramientas de migración disponibles y la habilidad de migración puede utilizarlas en las sesiones.

Para ver los pasos de configuración específicos de IDE, consulte las guías en [Configuración de MCP con AEM](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md).

>[!NOTE]
>Debe iniciar sesión con el Adobe ID que tiene acceso a sus proyectos CAM. Si ve un error de autorización, compruebe que su cuenta tenga los permisos adecuados en Cloud Acceleration Manager.

## Uso del MCP en una sesión de migración {#using-in-session}

Con el servidor MCP conectado, inicie una sesión de migración en el IDE con un mensaje como:

```
Fetch scheduler findings for project <name>/<id>.
```

El agente:

1. Obtiene los resultados de BPA para ese proyecto
2. Continúa con el flujo de trabajo de migración lote a lote

>[!IMPORTANT]
>Confirme siempre el proyecto de la lista antes de que el agente continúe. Los resultados no se recuperarán hasta que haya seleccionado explícitamente un proyecto.

### Priorización por gravedad {#by-severity}

Para ver un resumen ordenado por recuento de los resultados de los informes de BPA antes de iniciar la migración de patrones:

```
Show me CRITICAL findings from CAM for project <name>/<id>.
```

Utilice esto para decidir qué patrones priorizar en las sesiones.

## Resolución de problemas {#troubleshooting}

**IDE no se puede conectar al servidor MCP**

* Compruebe que la dirección URL se ha introducido exactamente como se muestra arriba, sin barra diagonal
* Reinicie el IDE después de guardar la configuración de MCP

**Error de autenticación**

* Asegúrese de iniciar sesión con el Adobe ID que tiene acceso a sus proyectos CAM

**No se encontró ningún informe de BPA**

* Compruebe que se ha cargado un informe de BPA en el proyecto CAM seleccionado. Ver [Uso del Analizador de prácticas recomendadas](/help/journey-migration/best-practices-analyzer/using-best-practices-analyzer.md).

## Siguientes pasos {#whats-next}

Con el MCP configurado, consulte [Uso de la habilidad de migración de la nube](/help/journey-migration/cloud-migration-skill/using-cloud-migration-skill.md) para obtener una referencia completa sobre los patrones de migración y la administración de sesiones.
