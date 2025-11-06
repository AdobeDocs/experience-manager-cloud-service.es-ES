---
title: Asignación de modelos dinámicos a componentes para SPA
description: Este artículo describe cómo se produce la asignación de modelos dinámicos a componentes en JavaScript SPA SDK para AEM.
exl-id: 3a7b3f26-4a09-40c1-af03-bb8408a68e57
feature: Developing
role: Admin, Developer
index: false
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 4%

---


# Asignación de modelos dinámicos a componentes para SPA {#dynamic-model-to-component-mapping-for-spas}

Este documento describe cómo se produce la asignación de modelos dinámicos a componentes en JavaScript SPA SDK para AEM.

{{ue-over-spa}}

## Módulo de asignación de componentes {#componentmapping-module}

El módulo `ComponentMapping` se proporciona como paquete NPM al proyecto front-end. Almacena componentes front-end y proporciona una forma para que la aplicación de una sola página asigne componentes front-end a tipos de recursos de AEM. El módulo habilita una resolución dinámica de componentes al analizar el modelo JSON de la aplicación.

Cada elemento presente en el modelo contiene un campo `:type` que expone un tipo de recurso de AEM. Cuando se monta, el componente front-end puede representarse a sí mismo utilizando el fragmento de modelo que ha recibido de las bibliotecas subyacentes.

Consulte el documento [Modelo SPA](blueprint.md) para obtener más información sobre el análisis del modelo y el acceso del componente front-end al modelo.

Consulte también el paquete npm: [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## Aplicación de una sola página impulsada por modelo {#model-driven-single-page-application}

Las aplicaciones de una sola página que utilizan JavaScript SPA SDK para AEM están basadas en modelos:

1. Los componentes front-end se registran a sí mismos en el [Almacén de asignaciones de componentes](#componentmapping-module).
1. A continuación, el [contenedor](blueprint.md#container), una vez proporcionado con un modelo por el [proveedor de modelos](blueprint.md#the-model-provider), se repite sobre el contenido de su modelo (`:items`).

1. Si hay una página, sus elementos secundarios (`:children`) obtienen primero una clase de componente de la [asignación de componentes](blueprint.md#componentmapping) y, a continuación, crean una instancia de ella.

## Inicialización de aplicaciones {#app-initialization}

Cada componente se amplía con las capacidades de [`ModelProvider`](blueprint.md#the-model-provider). Por lo tanto, la inicialización adopta la siguiente forma general:

1. Cada proveedor de modelos se inicializa a sí mismo y escucha los cambios realizados en el fragmento de modelo que corresponde a su componente interno.
1. [`PageModelManager`](blueprint.md#pagemodelmanager) debe inicializarse tal como lo representa el [flujo de inicialización](blueprint.md).

1. Una vez almacenado, el administrador de modelos de página devuelve el modelo completo de la aplicación.
1. A continuación, se pasa este modelo al componente [Contenedor](blueprint.md#container) raíz del front-end de la aplicación.
1. Las partes del modelo finalmente se propagan a cada componente secundario individual.

![Inicialización del modelo de aplicación](assets/app-model-initialization.png)
