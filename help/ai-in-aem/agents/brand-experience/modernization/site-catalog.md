---
title: Aptitud de catálogo del sitio
description: Descubra cómo la aptitud para catálogos de sitios del agente de modernización de experiencias realiza análisis automatizados de un sitio web existente para admitir la planificación de la migración a Edge Delivery Services.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
source-git-commit: 30037f08d5caeab878b6cf89b936308d16ae3e8d
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 0%

---


# Aptitud de catálogo del sitio {#site-catalog-skill}

Descubra cómo la aptitud para catálogos de sitios del agente de modernización de experiencias realiza análisis automatizados de un sitio web existente para admitir la planificación de la migración a Edge Delivery Services.

## Información general {#overview}

La aptitud para catálogos del sitio detecta todas las páginas del sitio, identifica las plantillas de página y las variantes de bloque en uso, captura capturas de pantalla de cada una y genera un paquete de informes interactivo de HTML que puede examinar en la pestaña Vista previa de la consola o descargar y abrir localmente.

La aptitud es compatible con usted y con la migración de un proyecto existente a Edge Delivery Services de las siguientes maneras:

* **Inicio de un proyecto de migración**: ejecute la aptitud antes de que comience cualquier trabajo para comprender la escala del sitio, incluido el recuento de páginas, las plantillas, las variantes de bloque y las configuraciones regionales. Establece el inventario de referencia del que dependen todas las decisiones posteriores.
* **Estimación y planificación del esfuerzo**: obtenga métricas cuantificadas para apoyar propuestas, planificación de sprint y obtención de recursos.
* **Preparación de importaciones en lotes**: use `template-catalog.json` para identificar qué páginas comparten el mismo diseño y planifique las importaciones en lotes de plantilla a plantilla.
* **Informes de partes interesadas**: comparta el paquete de informes interactivo de HTML con los jefes de proyecto, arquitectos e interesados empresariales.

## Invocando {#invoking}

[En la consola de modernización de experiencias,](/help/ai-in-aem/agents/brand-experience/modernization/console.md) usa lenguaje natural para pedirle al agente que genere un catálogo para un sitio. A continuación se muestran ejemplos de peticiones de datos.

* `scope site https://www.example.com`
* `site scope https://www.example.com`
* `analyze https://www.example.com`
* `find templates on https://www.example.com`
* `discover templates on https://www.example.com`
* `catalog site https://www.example.com`
* `how many page types are there on https://www.example.com`
* `what are the layouts on https://www.example.com`
* `analyze site structure of https://www.example.com`

Observará que el flujo de trabajo de la aptitud tiene cuatro fases que se ejecutan en secuencia:

1. Análisis
1. Plantillas
1. Ajuste
1. Bloquear catalogación

Puede reproducir cualquier fase y el agente borra las salidas de esa fase y todas las salidas de flujo descendente y luego se reanuda a partir de ese momento. A continuación se muestran algunos ejemplos de indicadores de reproducción de fases.

* `Repeat analyzing` / `Redo page analysis` / `Rerun analyze pages`
* `Repeat templating` / `Redo the template discovery step` / `Restart the templating step`
* `Repeat tuning` / `Rerun tune templates` / `Redo template tuning`
* `Repeat block cataloging` / `Restart catalog block variants`

Al reproducir una fase, se conservan las fases anteriores.

## Salida {#output}

Cuando la aptitud complete la catalogación del sitio, recibirá tres tipos diferentes de resultados.

1. **Un resumen de finalización en el chat** que incluye totales (páginas, plantillas, variantes de bloque con desglose asignado por EDS frente a personalizado), desglose de configuración regional, porcentaje de cobertura y estado general del informe (completo/incompleto/con error)
1. **Un paquete interactivo de informe de HTML** como su entrega principal, guardado en `catalog/template-catalog-report-bundle.zip`
   * El paquete contiene `template-catalog-report.html` además de todas las capturas de pantalla y recursos a los que se hace referencia.
   * Puede descargar el paquete y verlo localmente o compartirlo.
   * O puede pedirle al agente que `Move template-catalog-report-bundle.zip to the /content folder to render it in the preview tab. Update all references as needed.` vea el informe en la consola.
1. **Artefactos JSON estructurados** en `catalog/` para habilidades de flujo descendente y uso programático, incluidos `summary.json`, `template-catalog.json`, `block-catalog.json`, `urls-all.json`, `urls-grouped.json`, `urls-checklist.json`, `.pages/`, `.blocks/`

### Contenido de carpeta de catálogo {#contents}

La aptitud almacena los artefactos JSON estructurados en `catalog/`.

| Archivo | Descripción |
|---|---|
| `template-catalog-report-bundle.zip` | Paquete de informes interactivo de HTML (entrega principal) |
| `summary.json` | Métricas de resumen y [estado del informe](#status) |
| `template-catalog.json` | Todas las plantillas únicas con las direcciones URL que utilizan cada una (utilizadas para las importaciones masivas) |
| `block-catalog.json` | Todas las variantes de bloque con metadatos y referencias de captura de pantalla |
| `urls-all.json` | Cada URL descubierta |
| `urls-grouped.json` | URL agrupadas por patrón y configuración regional |
| `urls-sample.json` | URL representativas muestreadas para su análisis |
| `urls-checklist.json` | Estado del análisis por URL |
| `catalog.log` | Registro de ejecución |
| `.pages/<page-slug>/page-catalog.json` | Salida de análisis de nivel de página |
| `.pages/<page-slug>/full-page.jpg` | Captura de pantalla de página completa |
| `.pages/<page-slug>/blocks/<block-name>.jpg` | Capturas de pantalla por bloque |
| `.pages/_global/header.json + header.jpg` | Análisis de encabezado global y captura de pantalla |
| `.pages/_global/footer.json + footer.jpg` | Análisis y captura de pantalla del pie de página global |
| `.blocks/<variantId>/metadata.json` | Bloquear metadatos de variante |
| `.blocks/<variantId>/screenshots/<name>.jpg` | Bloquear capturas de pantalla de variante |

### Estados de informes {#status}

El campo `status` de [`summary.json`](#contents) puede ser:

| Estado | Significado |
|---|---|
| `complete` | Todas las páginas se analizaron correctamente (o hubo una tasa de error del 10 % o inferior). |
| `incomplete` | Error en más del 10 % de las páginas o la detección de bloques se bloqueó en más del 50 % de las páginas. Los resultados aún se pueden utilizar pero son parciales. |
| `failed` | No se analizó correctamente ninguna página. |

## Muestreo para sitios grandes {#sampling}

De forma predeterminada, la aptitud limita el análisis profundo de página a 1000 direcciones URL. Se analizan todas las páginas de los sitios con hasta 1000 URL inclusive.

En el caso de los sitios con más de 1000 direcciones URL, el agente realiza una pausa y pregunta cómo proceder:

* Aumento del límite de muestreo (hasta un máximo de 4000 URL)
* Analizar solo un grupo específico (por ejemplo, solo `/products/*` o `/blog/*`)
* Analice todas las direcciones URL y ejecute el sitio completo sin muestreo

La detección de URL siempre cubre el sitio completo, independientemente del límite de muestra. Solo es limitada la fase de análisis profundo por página.

Para anular y analizar cada página, informe al agente de:

* `analyze all URLs`
* `analyze everything`
* `analyze every page`
* `run the full site`

## Flujo de trabajo de importación masiva {#bulk-import}

El conocimiento del catálogo de sitios forma parte del método recomendado para migrar un sitio completo.

1. Ejecute la aptitud de catálogo del sitio para obtener el catálogo de plantillas completo y el catálogo de bloques.
1. Abra [el paquete de informes de HTML](#output) para revisar visualmente las plantillas que identificó el agente.
1. Para cada plantilla, importe manualmente las páginas representativas (enumeradas en [`template-catalog.json`](#output)) y perfeccione la importación hasta que el resultado sea correcto.
1. Importe de forma masiva las páginas restantes de esa plantilla mediante la lista de direcciones URL de `template-catalog.json`.
1. Repita el proceso para cada plantilla hasta que migre el sitio completo.

## Restricciones {#limitations}

El conocimiento del catálogo del sitio tiene las siguientes limitaciones.

* **Solo sitios públicos**: el destino debe ser de acceso público (sin autenticación, VPN ni firewall).
* **No se admite contenido dinámico**: Es posible que no se capture el contenido que requiere la interacción del usuario para aparecer en el DOM.
* **Límite predeterminado de 1000 URL**: la fase de análisis profundo está limitada de forma predeterminada a 1000 URL, [que se pueden sobrescribir](#sampling) hasta un máximo de 4000 URL.

