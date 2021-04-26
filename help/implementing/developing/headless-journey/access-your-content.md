---
title: Cómo acceder al contenido a través de las API de envío de AEM
description: En esta parte del Recorrido para desarrolladores sin encabezado de AEM, aprenda a utilizar las consultas de GraphQL para acceder al contenido de los fragmentos de contenido.
hide: true
hidefromtoc: true
index: false
translation-type: tm+mt
source-git-commit: d17583399b6792583e3e210005b62d360b91d05a
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 2%

---


# Cómo acceder al contenido a través de las API de envío de AEM {#access-your-content}

>[!CAUTION]
>
>TRABAJO EN CURSO - La creación de este documento está en curso y no debe entenderse como completo o definitivo ni debe utilizarse con fines de producción.

En esta parte del [AEM Recorrido para desarrolladores sin encabezado,](#overview.md) aprenda a utilizar las consultas de GraphQL para acceder al contenido de sus fragmentos de contenido.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido AEM sin encabezado, [Cómo modelar el contenido](model-your-content.md) ha aprendido los conceptos básicos del modelado de datos en AEM y ahora debería:

* Comprenda las consideraciones de planificación importantes para diseñar su contenido.
* Comprender los pasos para implementar sin encabezado según los requisitos de nivel de integración.
* Configure las herramientas y configuraciones de AEM necesarias.
* Conozca las prácticas recomendadas para que su recorrido sin objetivos sea fluido, mantenga la eficiencia de la generación de contenido y asegúrese de que el contenido se entregue rápidamente.

Este artículo se basa en estos aspectos básicos para que pueda comprender cómo acceder al contenido sin encabezado existente en AEM mediante API.

* **Audiencia**: Principiante
* **Objetivo**: Obtenga información sobre cómo acceder al contenido de los fragmentos de contenido mediante AEM consultas de GraphQL:
   * Presente GraphQL.
   * Presentación AEM API de GraphQL.
   * Descubra los detalles de la API de AEM GraphQL.
   * Observe algunas consultas de ejemplo para ver cómo funcionan las cosas en la práctica.

Con Adobe Experience Manager (AEM) como Cloud Service, puede utilizar los fragmentos de contenido, junto con la API de GraphQL de AEM, para entregar sin problemas contenido estructurado para utilizarlo en sus aplicaciones. La capacidad de personalizar una sola consulta de API le permite recuperar y entregar el contenido específico que desea o necesita procesar (como respuesta a la consulta de API única).

>[!NOTE]
>AEM API de GraphQL es una implementación personalizada, basada en GraphQL estándar.

## GraphQL: Introducción {#graphql-introduction}

GraphQL es:

* &quot;*...un idioma de consulta para API y un tiempo de ejecución para cumplir esas consultas con los datos existentes.*&quot;.

   Consulte *GraphQL*.

### GraphQL: Tipos {#graphql-types}

### GraphQL: Esquemas {#graphql-schemas}

### GraphQL: Consultas {#graphql-queries}

## AEM y GraphQL {#aem-graphql}

GraphQL se utiliza en varias ubicaciones de AEM:

* Comercio
   * Marcador de posición
* Fragmentos de contenido
   * Se ha desarrollado una API personalizada para este caso de uso.
   * Esta es la API de AEM GraphQL.

## API de AEM GraphQL {#aem-graphql-api}

Para Adobe Experience as a Cloud Experience, se ha desarrollado una implementación personalizada de la API estándar de GraphQL.

La API de AEM GraphQL permite realizar consultas (complejas) en los fragmentos de contenido; con cada consulta siendo según un tipo de modelo específico. Las aplicaciones pueden utilizar el contenido devuelto.

>[!NOTE]
>
>La implementación de la API de AEM GraphQL se basa en las bibliotecas Java de GraphQL.

### AEM API de GraphQL y fragmentos de contenido {#aem-graphql-content-fragments}

## Fragmentos de contenido para usar con la API de AEM GraphQL {#content-fragments-use-with-aem-graphql-api}

Los fragmentos de contenido se pueden usar como base para GraphQL para AEM consultas como:

* Permiten diseñar, crear, depurar y publicar contenido independiente de las páginas.
* Los modelos de fragmento de contenido proporcionan la estructura necesaria mediante tipos de datos definidos.
* La Referencia de fragmento, disponible al definir un modelo, se puede utilizar para definir capas de estructura adicionales.

### Fragmentos de contenido {#content-fragments}

Fragmentos de contenido:

* Contienen contenido estructurado.

* Se basan en un modelo de fragmento de contenido, que predefine la estructura del fragmento resultante.

### Modelos de fragmento de contenido {#content-fragments-models}

Estos modelos de fragmento de contenido:

* Se utilizan para generar los esquemas, una vez **Enabled**.

* Proporcione los tipos de datos y campos requeridos para GraphQL. Se aseguran de que la aplicación solo solicita lo que es posible y recibe lo que se espera.

* El tipo de datos **Referencias de fragmento** se puede usar en el modelo para hacer referencia a otro fragmento de contenido y, por lo tanto, introducir niveles adicionales de estructura.

### Referencias de fragmento {#fragment-references}

La **Referencia de fragmento**:

* Es de particular interés en conjunto con GraphQL.

* Es un tipo de datos específico que se puede utilizar al definir un modelo de fragmento de contenido.

* Hace referencia a otro fragmento, según un modelo de fragmento de contenido específico.

* Permite recuperar datos estructurados.

   * Cuando se define como una **fuente múltiple**, el fragmento principal puede hacer referencia (recuperar) a varios subfragmentos.

### Vista previa de JSON {#json-preview}

Para ayudar a diseñar y desarrollar los modelos de fragmento de contenido, puede obtener una vista previa de [JSON output](/help/assets/content-fragments/content-fragments-json-preview.md).

## Siguientes {#whats-next}

[Aprenda a utilizar la API de REST para acceder y actualizar el contenido de los fragmentos](/help/implementing/developing/headless-journey/update-your-content.md) de contenido.

## Recursos adicionales {#additional-resources}

* [Introducción a AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) : una breve serie de tutoriales de vídeo que ofrecen información general sobre el uso de AEM funciones sin encabezado, incluidos el modelado de datos y GraphQL.
* [GraphQL.org](https://graphql.org)
   * [Esquemas](https://graphql.org/learn/schema/)
   * [Bibliotecas Java de GraphQL](https://graphql.org/code/#java)
* [AEM API de GraphQL para su uso con fragmentos de contenido](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * [Aprender a utilizar GraphQL con AEM: contenido de muestra y consultas](/help/assets/content-fragments/content-fragments-graphql-samples.md)
   * [Autenticación para consultas de GraphQL remotas en fragmentos de contenido](/help/assets/content-fragments/graphql-authentication-content-fragments.md)
* [Trabajar con fragmentos de contenido](/help/assets/content-fragments/content-fragments.md)
   * [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md)
   * [Salida JSON](/help/assets/content-fragments/content-fragments-json-preview.md)
