---
title: SPA Asignación de modelos dinámicos a componentes para la creación de
description: En este artículo se describe cómo se produce la asignación de modelos dinámicos a componentes en JavaScript SPA SDK AEM para su.
exl-id: 3a7b3f26-4a09-40c1-af03-bb8408a68e57
feature: Developing
role: Admin, Architect, Developer
source-git-commit: e06766160009eaa1bbc41bbf7cfad967a5195e71
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# SPA Asignación de modelos dinámicos a componentes para la creación de {#dynamic-model-to-component-mapping-for-spas}

En este documento se describe cómo se produce la asignación de modelos dinámicos a componentes en JavaScript SPA SDK AEM para su uso en el sector de la.

{{ue-over-spa}}

## Módulo de asignación de componentes {#componentmapping-module}

El módulo `ComponentMapping` se proporciona como paquete NPM al proyecto front-end. AEM Almacena componentes front-end y proporciona una forma para que la aplicación de una sola página asigne componentes front-end a tipos de recursos de. El módulo habilita una resolución dinámica de componentes al analizar el modelo JSON de la aplicación.

AEM Cada elemento presente en el modelo contiene un campo `:type` que expone un tipo de recurso de. Cuando se monta, el componente front-end puede representarse a sí mismo utilizando el fragmento de modelo que ha recibido de las bibliotecas subyacentes.

SPA Consulte el documento [Modelo de](blueprint.md) para obtener más información sobre el análisis del modelo y el acceso del componente front-end al modelo.

Consulte también el paquete npm: [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## Aplicación de una sola página impulsada por modelo {#model-driven-single-page-application}

Las aplicaciones de una sola página que utilizan JavaScript SPA SDK AEM para la creación de informes están basadas en modelos:

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
