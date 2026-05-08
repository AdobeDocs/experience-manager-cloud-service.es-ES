---
title: Desarrollo local con herramientas de IA
description: Aprenda a configurar herramientas de codificación de IA con contexto de proyecto, habilidades de agente y servidores MCP para acelerar el desarrollo de AEM as a Cloud Service.
feature: Developing
role: Developer
exl-id: 09d6257d-36ad-49e5-831f-c44b356f1800
source-git-commit: 6fe463cb3f350f84e3853950e667eac851f672ef
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 0%

---

# Desarrollo local con herramientas de IA {#local-development-with-ai-tools}

>[!NOTE]
>
>Este artículo se centra en el desarrollo local con herramientas de IA para **desarrollo de pila Java de AEM**. Para Edge Delivery Services, consulte [Desarrollo con herramientas de IA](https://www.aem.live/developer/ai-coding-agents).

Los agentes de codificación de IA (Claude Code, Cursor, GitHub Copilot y herramientas similares) tienen un amplio conocimiento de las tecnologías subyacentes de AEM (Java, OSGi, Sling, JCR, HTL), pero no necesariamente conocen las prácticas recomendadas para generar código y configuración o cómo depurar problemas comunes de desarrollo de AEM.

Cuatro componentes complementarios se ocupan de esto:

| Componente | Función |
|---|---|
| **AGENTES.md** | Un archivo de contexto específico del proyecto que basa la IA en el proyecto de AEM Cloud Service para cada sesión |
| **Aptitudes de agente** | Conjuntos de instrucciones reutilizables para tareas de desarrollo recurrentes como la creación de componentes y la configuración de Dispatcher |
| **Servidor MCP local de inicio rápido de AEM** | Expone datos en tiempo de ejecución activos de una instancia local de AEM SDK para admitir la resolución de problemas |
| **Servidor MCP local de Dispatcher** | Habilita la validación y la inspección en tiempo de ejecución de una instancia de Dispatcher local |

Revise los [tutoriales de desarrollo asistido por IA](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/ai/ai-assisted-development/overview) para obtener instrucciones prácticas adicionales.

>[!NOTE]
>
> También son útiles para el desarrollo local, pero no se tratan en este artículo, los servidores MCP remotos de AEM Cloud Service. Obtenga más información sobre ellos en el artículo [Uso del MCP con Cloud Service](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md).

## AGENTS.md {#agentsmd}

`AGENTS.md` es un archivo Markdown en la raíz del proyecto de AEM que las herramientas de codificación de IA cargan automáticamente al principio de cada sesión para conectarse a tierra con la experiencia esencial del dominio de pila Java de AEM Cloud Service (y no otras soluciones de AEM como AEM 6.5 o Edge Delivery Services).

`AGENTS.md` no es un archivo estático que usted copia, sino que se genera por la aptitud de `ensure-agents-md` descrita en la siguiente sección. La aptitud lee su `pom.xml` para resolver el nombre del proyecto, descubrir módulos y detectar complementos instalados, lo que produce un archivo adaptado a su proyecto específico.

>[!NOTE]
>
>Una vez que `AGENTS.md` exista en la raíz del proyecto, la aptitud `ensure-agents-md` ya no se ejecutará. Edite el archivo directamente si cambia la estructura del proyecto.

## Aptitudes de agente {#agent-skills}

Las habilidades son conjuntos de instrucciones que codifican flujos de trabajo de desarrollo de varios pasos. Cuando se invoca, la IA sigue el procedimiento de la aptitud en lugar de basarse únicamente en el conocimiento general, lo que produce resultados coherentes y compatibles con la convención.

Adobe publica las aptitudes de AEM as a Cloud Service en el repositorio **[adobe/skills](https://github.com/adobe/skills/tree/main/plugins/aem/cloud-service)**:

| Aptitud | Función |
|---|---|
| `ensure-agents-md` | Las correas de inicio `AGENTS.md` y `CLAUDE.md` se adaptaron a la estructura de módulos real del proyecto |
| `create-component` | Andamiajes para un componente completo de AEM: definición de componente, XML de diálogo, plantilla HTL, modelo Sling, pruebas unitarias y clientlibs |
| `dispatcher` | Asistente de configuración HTTPD de Apache y Dispatcher con tecnología de IA que cubre la creación de configuraciones, el asesoramiento técnico, la respuesta a incidentes, la optimización del rendimiento y la protección de la seguridad |
| `workflow` | Punto de entrada único para todas las aptitudes del flujo de trabajo de AEM as a Cloud Service. Abarca el diseño del modelo de flujo de trabajo, el paso de proceso personalizado y el desarrollo del selector de participantes, la configuración del lanzador, el activador del flujo de trabajo y la compatibilidad con la producción, incluida la depuración de flujos de trabajo atascados/fallidos, la activación de incidentes con registros de Cloud Manager, el análisis del pool de hilos y los diagnósticos de trabajo de Sling para el motor de flujo de trabajo de Granite. |

### Instalar aptitudes {#install-skills}

Elija el método que coincida con la herramienta de codificación de IA. La instalación de habilidades una vez las pone a disposición de todos los proyectos de ese equipo. Consulte el tutorial [Configurar aptitudes de agente de AEM](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/ai/ai-assisted-development/setup/agent-skills) para ver un tutorial concreto.

#### Código Claude {#claude-code}

```bash
# Add the Adobe Skills marketplace (one-time setup)
/plugin marketplace add adobe/skills

# Install all available skills
/plugin install aem-cloud-service@adobe-skills
```

#### Aptitudes Npx {#npx-skills}

```bash
# Install all available skills
npx skills add https://github.com/adobe/skills/tree/main/skills/aem/cloud-service --all
```

#### Actualización (extensión CLI de GitHub) {#upskill-github-cli-extension}

```bash
# Install the gh-upskill extension (one-time setup)
gh extension install ai-ecoverse/gh-upskill

# Install all available skills
gh upskill adobe/skills --path skills/aem/cloud-service --all
```

### Use la habilidad de secure-agents-md {#use-the-ensure-agents-md-skill}

Después de instalar la aptitud, abra el asistente de IA en cualquier proyecto de AEM Cloud Service que aún no tenga `AGENTS.md`. La aptitud se ejecuta automáticamente antes de procesar la primera solicitud, lo que crea ambos archivos en la raíz del proyecto sin requerir una invocación explícita.

### Uso de la aptitud create-component {#use-the-create-component-skill}

En el primer uso, la aptitud detecta automáticamente `project`, `package` y `group` de `pom.xml` y de los componentes existentes, le pide que confirme los valores detectados y, a continuación, crea `.aem-skills-config.yaml` en la raíz del proyecto. No se requiere ninguna configuración manual antes del primer uso.

Si prefiere crear previamente el archivo, coloque `.aem-skills-config.yaml` en la raíz del proyecto con la siguiente estructura:

```yaml
configured: true

project: "wknd"                                    # Check /apps/{project}/ or pom.xml
package: "com.adobe.aem.guides.wknd.core"          # Check core/pom.xml
group: "WKND Components"                           # Check existing component .content.xml files
```

El archivo se encuentra fuera del directorio de aptitudes y nunca se sobrescribe cuando se actualiza la aptitud.

Describa el componente en su chat de IA:

```
Create an AEM component called "Hero Banner"

Dialog specification:
Title (title) - Textfield, mandatory
Subtitle (subtitle) - Textfield
Background Image (backgroundImage) - Fileupload
CTA Text (ctaText) - Textfield
CTA Link (ctaLink) - Pathfield
```

El agente hace eco de la especificación del campo para la confirmación y, a continuación, genera todos los archivos de componente. Los patrones admitidos son varios campos con elementos anidados compuestos, lógica condicional de mostrar/ocultar, extensión de componente principal mediante fusión de recursos de Sling y pruebas JUnit 5 con AEM Mocks. El diseño puede provenir de varias fuentes, incluyendo una descripción textual, una imagen o una URL de diseño Figma usando el servidor MCP de Figma.

Obtenga más información siguiendo el [desarrollo de componentes mediante el tutorial de habilidades del agente de AEM](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/ai/ai-assisted-development/use-cases/component-development).

### Uso de la aptitud de Dispatcher {#use-the-dispatcher-skill}

Invoque la aptitud de Dispatcher para cualquier trabajo de configuración HTTPD de Dispatcher o Apache. La aptitud dirige las solicitudes a una de las seis subaptitudes especializadas según la naturaleza de la solicitud:

| Subaptitud | Función |
|---|---|
| `workflow-orchestrator` | Trabajo completo que abarca el diseño, los cambios de configuración, la validación y el seguimiento |
| `config-authoring` | Cambios concretos en la configuración: filtros, reglas de caché, reescrituras, vhosts, encabezados y granjas |
| `technical-advisory` | Orientación conceptual, explicación de políticas y recomendaciones respaldadas por citas |
| `incident-response` | Errores, anomalías de caché y regresiones en tiempo de ejecución |
| `performance-tuning` | Optimización de la eficiencia, latencia y rendimiento de la caché |
| `security-hardening` | Revisión de la exposición y endurecimiento de la producción |

Para solicitudes amplias o iniciales, empiece con la subaptitud `workflow-orchestrator`. Para un trabajo específico, describa la preocupación específica y las rutas de aptitudes al especialista adecuado.

La habilidad del despachante gestiona la orquestación y la orientación consultiva. El servidor MCP de Dispatcher, que se describe a continuación, proporciona las siete herramientas de validación y tiempo de ejecución que la aptitud utiliza cuando necesita pruebas locales.

## Servidor MCP de Quickstart de AEM {#aem-quickstart-mcp-server}

El Protocolo de contexto de modelo (MCP) es un estándar abierto que permite a las herramientas de codificación de IA conectarse a fuentes de datos y servicios externos. El servidor AEM Quickstart MCP es un paquete de contenido que, una vez instalado en una instancia local de AEM SDK, expone los datos de tiempo de ejecución directamente a las herramientas de IA conectadas, lo que permite a los agentes recuperar registros, diagnosticar errores de OSGi e inspeccionar el procesamiento de solicitudes sin salir del IDE.

### Instalación del paquete de contenido {#install-the-content-package}

Descargue el paquete de contenido del [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?fulltext=mcp*&1_group.propertyvalues.property=.%2Fjcr%3Acontent%2Fmetadata%2Fdc%3AsoftwareType&1_group.propertyvalues.operation=equals&1_group.propertyvalues.0_values=software-type%3Atooling&orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&orderby.sort=desc&layout=list&p.offset=0&p.limit=3) e instale `com.adobe.aem:com.adobe.aem.mcp-server-contribs-content` en su Quickstart local mediante el Administrador de paquetes en `/crx/packmgr`.

**Compatibilidad:** Validada con AEM SDK `2026.2.24678.20260226T154829Z-260200` y posterior.

### Herramientas disponibles {#available-tools}

| Herramienta | Descripción |
|---|---|
| `aem-logs` | Recupera las entradas de registro de AEM y OSGi, que se pueden filtrar por patrón regex, nivel de registro y recuento de entradas |
| `diagnose-osgi-bundle` | Diagnostica por qué no se inicia un paquete o componente DS; informa de paquetes que faltan, referencias no satisfechas y problemas de configuración |
| `recent-requests` | Devuelve solicitudes HTTP recientes con el seguimiento de procesamiento interno completo de Sling (resolución de recursos, resolución de scripts, cadena de filtros), filtrable por regex de ruta |

### Configurar el IDE {#configure-your-ide}

#### Cursor {#cursor}

En Configuración de cursor, agregue un nuevo servidor MCP personalizado:

```json
"aem-cs-sdk": {
  "type": "streamable-http",
  "url": "http://localhost:4502/bin/mcp",
  "headers": {
    "Authorization": "Basic YWRtaW46YWRtaW4="
  }
}
```

#### Copiloto de GitHub con IntelliJ IDEA {#github-copilot-with-ihtellij-idea}

Vaya a **Herramientas > GitHub Copilot > Protocolo de contexto de modelo (MCP)** y haga clic en **Configurar**. Agregar:

```json
"aem-cs-sdk": {
  "url": "http://localhost:4502/bin/mcp",
  "requestInit": {
    "headers": {
      "Authorization": "Basic YWRtaW46YWRtaW4="
    }
  }
}
```

#### Otros IDE {#other-ides}

Cualquier cliente MCP puede conectarse señalando `http://localhost:4502/bin/mcp` con un encabezado `Authorization: Basic YWRtaW46YWRtaW4=`. Configure encabezados personalizados mediante la configuración de MCP del IDE.

>[!NOTE]
>
>El valor `Basic YWRtaW46YWRtaW4=` es la codificación Base64 de `admin:admin`, la credencial predeterminada para un inicio rápido local. No utilice esta opción con entornos no locales.

## Servidor MCP de Dispatcher {#dispatcher-mcp-server}

>[!IMPORTANT]
>
>Esta característica es **beta**. El acceso anticipado a las funciones que Adobe está desarrollando permite a los clientes y socios proporcionar comentarios (enviando un correo electrónico a [aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com)) y dar forma al desarrollo de productos. También les ayuda a prepararse para adoptar nuevas capacidades antes de la disponibilidad general.
>
>Las versiones de Beta pueden contener defectos y se proporcionan &quot;TAL CUAL&quot; sin garantía de ningún tipo. Adobe no tiene obligación de mantener, corregir, actualizar, cambiar, modificar o admitir de otro modo (mediante los Servicios de soporte de Adobe o de otro modo) las versiones beta. Adobe recomienda a los clientes tener cuidado y no depender del funcionamiento o el rendimiento correctos de las versiones beta, ni de la documentación o los materiales adjuntos. Las funciones y las API de la versión beta están sujetas a cambios sin previo aviso. Por lo tanto, cualquier uso de las versiones beta es totalmente bajo el propio riesgo del cliente.

El servidor MCP de Dispatcher está empaquetado con AEM Dispatcher SDK. Permite a las herramientas de IA validar la configuración de HTTPD de Dispatcher y Apache, rastrear la administración de solicitudes e inspeccionar el comportamiento de la caché con una instancia de Dispatcher que se ejecuta localmente en Docker.

A diferencia de la aptitud de Dispatcher, el servidor MCP de Dispatcher expone solo herramientas: siete herramientas MCP y sin peticiones de datos ni recursos.

### Requisitos previos {#prerequisites}

- Docker Desktop 4.x o posterior, instalado y en ejecución
- AEM Dispatcher SDK descargado del [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?fulltext=mcp*&1_group.propertyvalues.property=.%2Fjcr%3Acontent%2Fmetadata%2Fdc%3AsoftwareType&1_group.propertyvalues.operation=equals&1_group.propertyvalues.0_values=software-type%3Atooling&orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&orderby.sort=desc&layout=list&p.offset=0&p.limit=3)

>[!NOTE]
>
>Si ve `client version 1.43 is too new`, establezca `DOCKER_API_VERSION=1.41` en su shell o en `mcp.json`.

### Instalación de Dispatcher SDK {#install-the-dispatcher-sdk}

**macOS y Linux:**

```bash
chmod +x aem-sdk-dispatcher-tools-<version>-unix.sh
./aem-sdk-dispatcher-tools-<version>-unix.sh
cd dispatcher-sdk-<version>
chmod +x ./bin/docker_run_mcp.sh
./bin/docker_run_mcp.sh test
```

**Windows:**

```powershell
Expand-Archive aem-sdk-dispatcher-tools-<version>-windows.zip
```

Ejecute `./bin/docker_run_mcp.sh help` para recuperar la configuración del IDE de copiar y pegar y `./bin/docker_run_mcp.sh version` para confirmar la versión del MCP y SDK agrupados. Use `./bin/docker_run_mcp.sh diagnose` para investigar los problemas de conectividad.

### Configurar cursor {#configure-cursor}

Agregar una entrada `aem-dispatcher-mcp` a `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "aem-dispatcher-mcp": {
      "command": "<path_to_dispatcher_sdk>/bin/docker_run_mcp.sh",
      "env": {
        "DOCKER_API_VERSION": "1.43",
        "AEM_DEPLOYMENT_MODE": "cloud",
        "MCP_LOG_LEVEL": "trace",
        "MCP_LOG_FILE": "/tmp/dispatcher-mcp.log",
        "DISPATCHER_CONFIG_PATH": "<path_to_dispatcher_src>"
      }
    }
  }
}
```

Reemplace `<path_to_dispatcher_sdk>` por la ubicación de Dispatcher SDK extraída y `<path_to_dispatcher_src>` por el directorio de Dispatcher `src` del proyecto. Establezca `DISPATCHER_CONFIG_PATH` en la raíz de configuración que incluye los archivos donde se define `/docroot`. `MCP_LOG_LEVEL` y `MCP_LOG_FILE` son opciones de depuración opcionales. Si ve `client version 1.43 is too new`, establezca `DOCKER_API_VERSION` en `1.41`. Si ya se han configurado otros servidores MCP, agregue la entrada `aem-dispatcher-mcp` sin reemplazarlos. Reinicie Cursor después de guardar.

Otros IDE se pueden configurar de manera similar. `docs/DispatcherMCP.md` de SDK incluye ejemplos completos de Claude Desktop y código VS.

### Herramientas disponibles {#available-tools-dispatcher}

| Herramienta | Descripción |
|---|---|
| `validate` | Valida las configuraciones de HTTPD de Dispatcher y Apache |
| `lint` | Ejecuta comprobaciones estáticas según el modo y análisis de prácticas recomendadas |
| `sdk` | Ejecuta flujos de trabajo de Dispatcher SDK: `validate`, `validate-full`, `three-phase-validate`, `docker-test`, `check-files`, `diff-baseline` |
| `trace_request` | Rastrea el comportamiento de la solicitud con pruebas de tiempo de ejecución |
| `inspect_cache` | Inspecciona el comportamiento de caché y docroot para una URL de destino |
| `monitor_metrics` | Lee las métricas de tiempo de ejecución de los registros de Dispatcher y HTTPD |
| `tail_logs` | Sigue los registros de tiempo de ejecución relevantes de Dispatcher y HTTPD |

La superficie de MCP expone intencionadamente solo estas siete herramientas; los indicadores y los recursos permanecen en la capa de habilidad. La documentación de referencia completa está disponible en `docs/DispatcherMCP.md` dentro del SDK de Dispatcher extraído.
