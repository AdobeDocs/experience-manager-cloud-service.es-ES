---
title: SPA Asignación de modelos dinámicos a componentes para la creación de
description: SPA AEM En este artículo se describe cómo se produce la asignación de modelos dinámicos a componentes en el SDK de JavaScript para la.
exl-id: 3a7b3f26-4a09-40c1-af03-bb8408a68e57
source-git-commit: d361ddc9a50a543cd1d5f260c09920c5a9d6d675
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# SPA Asignación de modelos dinámicos a componentes para la creación de {#dynamic-model-to-component-mapping-for-spas}

SPA AEM Este documento describe cómo se produce la asignación de modelos dinámicos a componentes en el SDK de JavaScript para la.

## Módulo de asignación de componentes {#componentmapping-module}

El `ComponentMapping` El módulo se proporciona como paquete NPM al proyecto front-end. AEM Almacena componentes front-end y proporciona una forma para que la aplicación de una sola página asigne componentes front-end a tipos de recursos de. El módulo habilita una resolución dinámica de componentes al analizar el modelo JSON de la aplicación.

Cada elemento presente en el modelo contiene un `:type` AEM campo que expone un tipo de recurso de. Cuando se monta, el componente front-end puede representarse a sí mismo utilizando el fragmento de modelo que ha recibido de las bibliotecas subyacentes.

Consulte [SPA Modelo de](blueprint.md) para obtener más información sobre el análisis del modelo y el acceso del componente front-end al modelo.

Consulte también el paquete npm: [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## Aplicación de una sola página impulsada por modelo {#model-driven-single-page-application}

SPA AEM Las aplicaciones de una sola página que utilizan el SDK de JavaScript para la creación de páginas para la creación de informes están basadas en modelos:

1. Los componentes front-end se registran en el [Almacén de asignación de componentes](#componentmapping-module).
1. A continuación, el [Contenedor](blueprint.md#container), una vez proporcionada con un modelo por el [Proveedor de modelo](blueprint.md#the-model-provider), se repite sobre el contenido de su modelo (`:items`).

1. Si hay una página, sus elementos secundarios (`:children`) obtenga primero una clase de componente del [Asignación de componentes](blueprint.md#componentmapping) y luego instanciarlo.

## Inicialización de aplicaciones {#app-initialization}

Cada componente se amplía con las capacidades del [`ModelProvider`](blueprint.md#the-model-provider). Por lo tanto, la inicialización adopta la siguiente forma general:

1. Cada proveedor de modelos se inicializa a sí mismo y escucha los cambios realizados en el fragmento de modelo que corresponde a su componente interno.
1. El [`PageModelManager`](blueprint.md#pagemodelmanager) se debe inicializar tal como lo representa el [flujo de inicialización](blueprint.md).

1. Una vez almacenado, el administrador de modelos de página devuelve el modelo completo de la aplicación.
1. Este modelo se pasa a la raíz del front-end [Contenedor](blueprint.md#container) componente de la aplicación.
1. Las partes del modelo finalmente se propagan a cada componente secundario individual.

![Inicialización del modelo de aplicación](assets/app-model-initialization.png)
