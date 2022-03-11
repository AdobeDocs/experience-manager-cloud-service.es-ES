---
title: Asignación de modelos dinámicos a componentes para SPA
description: En este artículo se describe cómo se produce la asignación del modelo dinámico a los componentes en el SDK de SPA de JavaScript para AEM.
exl-id: 3a7b3f26-4a09-40c1-af03-bb8408a68e57
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# Asignación de modelos dinámicos a componentes para SPA {#dynamic-model-to-component-mapping-for-spas}

En este documento se describe cómo se produce la asignación de modelos dinámicos a componentes en el SDK de SPA de JavaScript para AEM.

## Módulo ComponentMapping {#componentmapping-module}

La variable `ComponentMapping` se proporciona como paquete NPM al proyecto front-end. Almacena componentes front-end y proporciona una forma para que la aplicación de una sola página asigne componentes front-end a AEM tipos de recursos. Esto permite una resolución dinámica de los componentes al analizar el modelo JSON de la aplicación.

Cada elemento presente en el modelo contiene un `:type` campo que muestra un tipo de recurso AEM. Cuando se monta, el componente frontal puede procesarse utilizando el fragmento de modelo que ha recibido de las bibliotecas subyacentes.

Consulte la [Modelo SPA](blueprint.md) documento para obtener más información sobre el análisis de modelos y el acceso de componentes front-end al modelo.

Consulte también el paquete npm: [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## Aplicación de página única impulsada por modelo {#model-driven-single-page-application}

Las aplicaciones de una sola página que aprovechan el SDK de SPA de Javascript para AEM están basadas en modelos:

1. Los componentes del front-end se registran a sí mismos en el [Almacén de asignación de componentes](#componentmapping-module).
1. A continuación, el [Contenedor](blueprint.md#container), una vez que el [Proveedor de modelo](blueprint.md#the-model-provider), se repite sobre el contenido del modelo (`:items`).

1. En el caso de una página, sus elementos secundarios (`:children`) obtenga primero una clase de componente de la [Asignación de componentes](blueprint.md#componentmapping) y luego instancie.

## Inicialización de la aplicación {#app-initialization}

Cada componente se amplía con las capacidades del [`ModelProvider`](blueprint.md#the-model-provider). Por lo tanto, la inicialización adopta la siguiente forma general:

1. Cada proveedor de modelos se inicializa y escucha los cambios realizados en la pieza del modelo que corresponde a su componente interno.
1. La variable [`PageModelManager`](blueprint.md#pagemodelmanager) debe inicializarse tal y como lo representa el [flujo de inicialización](blueprint.md).

1. Una vez almacenado, el administrador del modelo de página devuelve el modelo completo de la aplicación.
1. Este modelo se pasa entonces a la raíz del front-end [Contenedor](blueprint.md#container) de la aplicación.
1. Los fragmentos del modelo se propagan finalmente a cada componente secundario individual.

![Inicialización del modelo de aplicación](assets/app-model-initialization.png)
