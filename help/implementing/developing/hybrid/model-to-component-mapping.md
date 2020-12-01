---
title: Asignación dinámica de modelo a componente para SPA
description: En este artículo se describe cómo se produce la asignación de modelos dinámicos a componentes en el SDK de SPA de JavaScript para AEM.
translation-type: tm+mt
source-git-commit: cdd92032c627740c66de7b2f3836fa1dcd2ee2ca
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# Asignación dinámica de modelo a componente para SPA {#dynamic-model-to-component-mapping-for-spas}

En este documento se describe cómo se produce la asignación de modelos dinámicos a componentes en el SDK de SPA de Javascript para AEM.

## Módulo ComponentMapping {#componentmapping-module}

El módulo `ComponentMapping` se proporciona como paquete NPM al proyecto front-end. Almacena componentes front-end y proporciona una forma para que la aplicación de una sola página asigne componentes front-end a AEM tipos de recursos. Esto permite una resolución dinámica de los componentes al analizar el modelo JSON de la aplicación.

Cada elemento presente en el modelo contiene un campo `:type` que expone un tipo de recurso AEM. Cuando se monta, el componente front-end puede procesarse utilizando el fragmento de modelo que ha recibido de las bibliotecas subyacentes.

Consulte el documento [SPA modelo](blueprint.md) para obtener más información sobre el análisis de modelos y el acceso de componentes front-end al modelo.

Consulte también el paquete npm: [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## Aplicación de página única basada en modelo {#model-driven-single-page-application}

Las aplicaciones de una sola página que utilizan el SDK de SPA de Javascript para AEM están basadas en modelos:

1. Los componentes front-end se registran en el [Almacenamiento de asignación de componentes](#componentmapping-module).
1. A continuación, el [Contenedor](blueprint.md#container), una vez proporcionado con un modelo por el [Proveedor del modelo](blueprint.md#the-model-provider), se repite sobre su contenido del modelo (`:items`).

1. En el caso de una página, sus elementos secundarios (`:children`) primero obtienen una clase de componente de la [Asignación de componentes](blueprint.md#componentmapping) y, a continuación, la instancian.

## Inicialización de la aplicación {#app-initialization}

Cada componente se amplía con las capacidades de [`ModelProvider`](blueprint.md#the-model-provider). Por consiguiente, la inicialización tiene la siguiente forma general:

1. Cada proveedor de modelos se inicializa y escucha los cambios realizados en la pieza del modelo que corresponde a su componente interior.
1. El [`PageModelManager`](blueprint.md#pagemodelmanager) debe inicializarse como representado por el [flujo de inicialización](blueprint.md).

1. Una vez almacenado, el administrador de modelos de página devuelve el modelo completo de la aplicación.
1. A continuación, este modelo se pasa al componente raíz [Contenedor](blueprint.md#container) del front-end de la aplicación.
1. Las partes del modelo se propagan finalmente a cada componente secundario individual.

![Inicialización del modelo de aplicación](assets/app-model-initialization.png)
