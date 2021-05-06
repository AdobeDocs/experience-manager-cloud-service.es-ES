---
title: Cómo acceder al contenido a través de las API de envío de AEM
description: En esta parte del Recorrido para desarrolladores sin encabezado de AEM, aprenda a utilizar las consultas de GraphQL para acceder al contenido de los fragmentos de contenido.
hide: true
hidefromtoc: true
index: false
exl-id: 5ef557ff-e299-4910-bf8c-81c5154ea03f
translation-type: tm+mt
source-git-commit: 0c47dec1e96fc3137d17fc3033f05bf1ae278141
workflow-type: tm+mt
source-wordcount: '2181'
ht-degree: 1%

---

# Cómo acceder al contenido a través de las API de envío de AEM {#access-your-content}

>[!CAUTION]
>
>TRABAJO EN CURSO - La creación de este documento está en curso y no debe entenderse como completo o definitivo ni debe utilizarse con fines de producción.

En esta parte del [AEM Recorrido para desarrolladores sin encabezado,](overview.md) puede aprender a utilizar las consultas de GraphQL para acceder al contenido de sus fragmentos de contenido y alimentarlo en su aplicación (entrega sin encabezado).

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido AEM sin encabezado, [Cómo modelar el contenido](model-your-content.md) ha aprendido los conceptos básicos del modelado de contenido en AEM, por lo que ahora debe comprender cómo modelar la estructura de contenido y, a continuación, darse cuenta de esa estructura utilizando AEM modelos de fragmentos de contenido y fragmentos de contenido:

* Reconocer los conceptos y la terminología relacionados con el modelado de contenido.
* Comprenda por qué el modelado de contenido es necesario para la entrega de contenido sin encabezado.
* Obtenga información sobre cómo llevar a cabo esta estructura mediante AEM modelos de fragmento de contenido (y cree contenido con fragmentos de contenido).
* Comprender cómo modelar el contenido; principios con muestras básicas.

Este artículo se basa en estos aspectos básicos para que pueda comprender cómo acceder al contenido sin encabezado existente en AEM mediante la API de GraphQL de AEM.

* **Audiencia**: Principiante
* **Objetivo**: Obtenga información sobre cómo acceder al contenido de los fragmentos de contenido mediante AEM consultas de GraphQL:
   * Presente GraphQL y la API de AEM GraphQL.
   * Descubra los detalles de la API de AEM GraphQL.
   * Observe algunas consultas de ejemplo para ver cómo funcionan las cosas en la práctica.

## ¿Le gustaría acceder a su contenido? {#so-youd-like-to-access-your-content}

Así que...tiene todo este contenido, bien estructurado (en fragmentos de contenido) y esperando para alimentar su nueva aplicación. La pregunta es: ¿cómo llegar allí?

Lo que necesita es una forma de segmentar contenido específico, seleccionar lo que necesita y devolverlo a su aplicación para un procesamiento posterior.

Con Adobe Experience Manager (AEM) como Cloud Service, puede acceder selectivamente a sus fragmentos de contenido mediante la API de GraphQL de AEM para devolver solo el contenido que necesita. Esto significa que puede realizar envíos sin objetivos de contenido estructurado para utilizarlo en sus aplicaciones.

>[!NOTE]
>
>AEM API de GraphQL es una implementación personalizada, basada en la especificación estándar de la API de GraphQL.

## GraphQL: Introducción {#graphql-introduction}

GraphQL es una especificación de código abierto que proporciona:

* lenguaje de consulta que permite seleccionar contenido específico de objetos estructurados.
* un tiempo de ejecución para realizar estas consultas con el contenido estructurado.

GraphQL es una API con *tipos de inflexible*. Esto significa que el contenido de *todo* debe estar claramente estructurado y organizado por tipo, de modo que GraphQL *entienda* a qué acceder y cómo hacerlo. Los campos de datos se definen en los esquemas de GraphQL, que definen la estructura de los objetos de contenido.

Los extremos de GraphQL proporcionan las rutas que responden a las consultas de GraphQL.

Todo esto significa que la aplicación puede seleccionar de forma precisa, fiable y eficaz el contenido que necesita, justo lo que necesita cuando se utiliza con AEM.

>[!NOTE]
>
>Consulte *GraphQL*.org y *GraphQL*.com.

## AEM y GraphQL {#aem-graphql}

GraphQL se utiliza en varias ubicaciones de AEM; por ejemplo:

* Fragmentos de contenido
   * Se ha desarrollado una API personalizada para este caso de uso (entrega sin encabezado a su aplicación).
      * Esta es la API de AEM GraphQL.
* Comercio
   * AEM Commerce consume datos de una plataforma de comercio a través de GraphQL.
   * Existen integraciones de GraphQL entre AEM y varias soluciones de comercio de terceros, que se utilizan con los enlaces de extensión proporcionados por los componentes principales del CIF.
      * Esto no utiliza la API de AEM GraphQL.

>[!NOTE]
>
>Este paso del Recorrido sin encabezado solo se refiere a la API de AEM GraphQL y a los fragmentos de contenido.

## API de AEM GraphQL {#aem-graphql-api}

La API de AEM GraphQL es una versión personalizada basada en la especificación estándar de la API de GraphQL, especialmente configurada para permitirle realizar consultas (complejas) en los fragmentos de contenido.

Se utilizan fragmentos de contenido, ya que el contenido está estructurado según los modelos de fragmento de contenido. Esto cumple un requisito básico de GraphQL.

* Un modelo de fragmento de contenido está formado por uno o más campos.
   * Cada campo se define según un Tipo de datos.
* Los modelos de fragmento de contenido se utilizan para generar los esquemas AEM de GraphQL correspondientes.

Para acceder realmente a GraphQL para AEM (y el contenido) se utiliza un punto final para proporcionar la ruta de acceso.

El contenido devuelto, a través de la API de AEM GraphQL, puede ser utilizado por sus aplicaciones.

>[!NOTE]
>
>La implementación de la API de AEM GraphQL se basa en las bibliotecas Java de GraphQL.

### Casos de uso para entornos de autor y publicación {#use-cases-author-publish-environments}

Los casos de uso de la API de AEM GraphQL pueden depender del tipo de AEM como entorno de Cloud Service:

* Entorno de publicación; se usa para:
   * Contenido de consulta para la aplicación JS (caso de uso estándar)

* Entorno de creación; se usa para:
   * Contenido de la consulta para &quot;fines de administración de contenido&quot;:
      * GraphQL en AEM as a Cloud Service es actualmente una API de solo lectura.
      * La API de REST se puede utilizar para operaciones CR(u)D.

## Fragmentos de contenido para usar con la API de AEM GraphQL {#content-fragments-use-with-aem-graphql-api}

Los fragmentos de contenido se pueden usar como base para GraphQL para AEM esquemas y consultas como:

* Permiten diseñar, crear, depurar y publicar contenido independiente de las páginas.
* Se basan en un modelo de fragmento de contenido, que predefine la estructura del fragmento resultante mediante tipos de datos definidos.
* Se pueden lograr capas de estructura adicionales con el tipo de datos Referencia de fragmento , disponible al definir un modelo.

### Modelos de fragmento de contenido {#content-fragments-models}

Estos modelos de fragmento de contenido:

* Se utilizan para generar los esquemas, una vez **Enabled**.

* Proporcione los tipos de datos y campos requeridos para GraphQL. Se aseguran de que la aplicación solo solicita lo que es posible y recibe lo que se espera.

* El tipo de datos **Referencias de fragmento** se puede usar en el modelo para hacer referencia a otro fragmento de contenido y, por lo tanto, introducir niveles adicionales de estructura.

### Referencias de fragmento {#fragment-references}

La **Referencia de fragmento**:

* Es un tipo de datos específico disponible al definir un modelo de fragmento de contenido.

* Hace referencia a otro fragmento, según un modelo de fragmento de contenido específico.

* Permite crear y recuperar datos estructurados.

   * Cuando se define como una **fuente múltiple**, el fragmento principal puede hacer referencia (recuperar) a varios subfragmentos.

### Vista previa de JSON {#json-preview}

Para ayudar a diseñar y desarrollar los modelos de fragmento de contenido, puede obtener una vista previa del resultado de JSON en el Editor de fragmentos de contenido.

### Creación de modelos de fragmentos de contenido y fragmentos de contenido {#creating-content-fragment-models-and-content-fragments}

En primer lugar, los modelos de fragmento de contenido están habilitados para su sitio, esto se hace en el Explorador de configuración:

![Definir configuración](assets/cfm-configuration.png)

A continuación, se pueden modelar los modelos de fragmentos de contenido:

![Modelo de fragmento de contenido](assets/cfm-model.png)

Después de seleccionar el modelo adecuado, se abre un fragmento de contenido para editarlo en el Editor de fragmentos de contenido:

![Editor de fragmento de contenido](assets/cfm-editor.png)

>[!NOTE]
>
>Consulte Uso de fragmentos de contenido.

## Generación de esquemas de GraphQL a partir de fragmentos de contenido {#graphql-schema-generation-content-fragments}

GraphQL es una API con establecimiento inflexible de tipos, lo que significa que el contenido debe estar claramente estructurado y organizado por tipo. La especificación de GraphQL proporciona una serie de directrices sobre cómo crear una API sólida para interrogar contenido en un determinado caso. Para ello, un cliente debe recuperar el Esquema , que contiene todos los tipos necesarios para una consulta.

Para los fragmentos de contenido, los esquemas (estructura y tipos) de GraphQL se basan en modelos de **Fragmento de contenido habilitado** y sus tipos de datos.

>[!CAUTION]
>
>Todos los esquemas de GraphQL (derivados de los modelos de fragmento de contenido que han sido **Enabled**) se pueden leer a través del extremo de GraphQL.
>
>Esto significa que debe asegurarse de que no hay contenido confidencial disponible, para garantizar que no se expongan datos confidenciales a través de los extremos de GraphQL; por ejemplo, esto incluye información que podría estar presente como nombres de campo en la definición del modelo.

Por ejemplo, si un usuario creó un Modelo de fragmento de contenido denominado `Article`, AEM genera el objeto `article` que es de un tipo `ArticleModel`. Los campos dentro de este tipo corresponden a los campos y tipos de datos definidos en el modelo.

1. Un modelo de fragmento de contenido:

   ![Modelo de fragmento de contenido para usar con el Modelo de fragmento de ](assets/graphqlapi-cfmodel.png "GraphQLContent para usar con GraphQL")

1. El esquema correspondiente de GraphQL (salida de la documentación automática de GraphiQL):
   ![Esquema GraphQL basado en el ](assets/graphqlapi-cfm-schema.png "modelo de fragmento de contenidoEsquema de GraphQL basado en el modelo de fragmento de contenido")

   Esto muestra que el tipo generado `ArticleModel` contiene varios [campos](#fields).

   * Tres de ellos han sido controlados por el usuario: `author`, `main` y `referencearticle`.

   * Los demás campos los agregó automáticamente AEM y representan métodos útiles para proporcionar información sobre un determinado fragmento de contenido; en este ejemplo, `_path`, `_metadata`, `_variations`. Estos [campos de ayuda](#helper-fields) están marcados con un `_` anterior para distinguir entre lo que ha definido el usuario y lo que se ha generado automáticamente.

1. Después de que un usuario crea un fragmento de contenido basado en el modelo de artículo, se puede interrogar a través de GraphQL. Para ver ejemplos, consulte Sample Queries.md#graphql-sample-queries) (basado en una estructura de fragmento de contenido de ejemplo para usar con GraphQL.

En GraphQL para AEM, el esquema es flexible. Esto significa que se genera automáticamente cada vez que se crea, actualiza o elimina un modelo de fragmento de contenido. Las cachés del esquema de datos también se actualizan al actualizar el modelo de fragmento de contenido.

El servicio Sites GraphQL escucha (en segundo plano) cualquier modificación realizada en un modelo de fragmento de contenido. Cuando se detectan actualizaciones, solo se regenera esa parte del esquema. Esta optimización ahorra tiempo y proporciona estabilidad.

Por ejemplo, si:

1. Instale un paquete que contenga `Content-Fragment-Model-1` y `Content-Fragment-Model-2`:

   1. Se generarán los tipos de GraphQL para `Model-1` y `Model-2`.

1. A continuación, modifique `Content-Fragment-Model-2`:

   1. Solo se actualizará el tipo `Model-2` GraphQL.

   1. Mientras que `Model-1` permanecerá igual.

>[!NOTE]
>
>Esto es importante tener en cuenta en caso de que desee realizar actualizaciones masivas en los modelos de fragmento de contenido a través de la api de REST o de otro modo.

El esquema se sirve a través del mismo extremo que las consultas de GraphQL, con el cliente manejando el hecho de que se llama al esquema con la extensión `GQLschema`. Por ejemplo, si se realiza una solicitud `GET` simple en `/content/cq:graphql/global/endpoint.GQLschema`, el resultado del esquema será el tipo Content: `text/x-graphql-schema;charset=iso-8859-1`.

### Generación de esquemas: modelos no publicados {#schema-generation-unpublished-models}

Cuando los fragmentos de contenido están anidados, puede ocurrir que se publique un modelo de fragmento de contenido principal, pero no un modelo al que se hace referencia.

>[!NOTE]
>
>La interfaz de usuario de AEM evita que esto ocurra, pero si la publicación se realiza mediante programación o con paquetes de contenido, puede ocurrir.

Cuando esto sucede, AEM genera un esquema *incompleto* para el modelo de fragmento de contenido principal. Esto significa que la referencia de fragmento, que depende del modelo no publicado, se elimina del esquema.

## Puntos finales de AEM GraphQL {#aem-graphql-endpoints}

<!--
need details/examples
-->

Un punto final es la ruta utilizada para acceder a GraphQL para AEM. Al utilizar esta ruta, usted (o su aplicación) pueden:

* acceda a los esquemas de GraphQL,
* envíe sus consultas de GraphQL,
* reciba las respuestas (a sus consultas de GraphQL).

AEM permite:

* Un punto final global - disponible para su uso en todos los sitios.
* Puntos finales del inquilino : que puede configurar, específicos de un sitio o proyecto especificado.

## Permisos    {#permissions}

Los permisos son los necesarios para acceder a Assets.

## Interfaz de GraphiQL de AEM {#aem-graphiql-interface}

Para ayudarle a introducir y probar consultas directamente, una implementación de la interfaz estándar de GraphiQL está disponible para su uso con AEM GraphQL. Esto se puede instalar con AEM.

Proporciona funciones como resaltado de sintaxis, autocompletado, autosugerencia, junto con un historial y documentación en línea.

![Interfaz ](assets/graphiql-interface.png "GraphiQL de GraphiQL")

## Uso real de la API de AEM GraphQL {#actually-using-aem-graphiql}

Para utilizar la API de AEM GraphQL en una consulta, podemos utilizar las dos estructuras básicas del Modelo de fragmento de contenido:

* Empresa
   * Nombre
   * Director general (persona)
   * Empleados (personas)
* Person
   * Nombre
   * Nombre

Como puede ver, los campos CEO y Empleados hacen referencia a los fragmentos Persona .

Se utilizarán los modelos de fragmento:

* al crear el contenido en el editor de fragmentos de contenido
* para generar los esquemas de GraphQL que vaya a consultar

Las consultas se pueden introducir en la interfaz de GraphiQL, por ejemplo en:

* `http://localhost:4502/content/graphiql.html `

Una consulta directa es devolver el nombre de todas las entradas del esquema Company. Aquí puede solicitar una lista de todos los nombres de compañía:

```xml
query {
  companyList {
    items {
      name
    }
  }
}
```

Una consulta ligeramente más compleja es seleccionar todas las personas que no tienen un nombre de &quot;Trabajos&quot;. Esto filtrará todas las personas para aquellas que no tengan el nombre Trabajos. Esto se logra con el operador EQUALS_NOT (hay muchos más):

```xml
query {
  personList(filter: {
    name: {
      _expressions: [
        {
          value: "Jobs"
          _operator: EQUALS_NOT
        }
      ]
    }
  }) {
    items {
      name
      firstName
    }
  }
}
```

También puede crear consultas más complejas. Por ejemplo, realice una consulta a todas las empresas que tengan al menos un empleado con el nombre &quot;Smith&quot;. Esta consulta ilustra el filtrado para cualquier persona de nombre &quot;Smith&quot;, que devuelve información de los fragmentos anidados:

```xml
query {
  companyList(filter: {
    employees: {
      _match: {
        name: {
          _expressions: [
            {
              value: "Smith"
            }
          ]
        }
      }
    }
  }) {
    items {
      name
      ceo {
        name
        firstName
      }
      employees {
        name
        firstName
      }
    }
  }
}
```

<!-- need code / curl / cli examples-->

Para obtener toda la información sobre el uso de la API de AEM GraphQL, junto con la configuración de los elementos necesarios, puede hacer referencia a:

* Aprender a usar GraphQL con AEM
* La estructura de fragmento de contenido de ejemplo
* Aprender a utilizar GraphQL con AEM: contenido de muestra y consultas

## Siguientes {#whats-next}

Ahora que ha aprendido a acceder y consultar el contenido sin encabezado mediante la API de AEM GraphQL, ahora puede [aprender a utilizar la API de REST para acceder y actualizar el contenido de sus fragmentos de contenido](/help/implementing/developing/headless-journey/update-your-content.md).

## Recursos adicionales {#additional-resources}

* [GraphQL.org](https://graphql.org)
   * [Esquemas](https://graphql.org/learn/schema/)
   * [Variables](https://graphql.org/learn/queries/#variables)
   * [Bibliotecas Java de GraphQL](https://graphql.org/code/#java)
* [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql)
* [Aprender a usar GraphQL con AEM](/help/assets/content-fragments/graphql-api-content-fragments.md)
* [La estructura de fragmento de contenido de ejemplo](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)
* [Aprender a utilizar GraphQL con AEM: contenido de muestra y consultas](/help/assets/content-fragments/content-fragments-graphql-samples.md)
   * [Consulta De Muestra: Un Solo Fragmento De Ciudad Específico](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)
   * [Consulta de ejemplo para metadatos: enumera los metadatos de los premios titulados GB](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb)
   * [Consulta de ejemplo: todas las ciudades con una variación con nombre](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation)
* [Habilitar la funcionalidad de fragmento de contenido en el navegador de configuración](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)
* [Trabajar con fragmentos de contenido](/help/assets/content-fragments/content-fragments.md)
   * [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md)
   * [Salida JSON](/help/assets/content-fragments/content-fragments-json-preview.md)
* [Comprender el uso compartido de recursos de origen cruzado (CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=en#understand-cross-origin-resource-sharing-(cors))
* [Generación de tokens de acceso para las API del servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)
* [Introducción a AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) : una breve serie de tutoriales de vídeo que ofrecen información general sobre el uso de AEM funciones sin encabezado, incluidos el modelado de contenido y GraphQL.
