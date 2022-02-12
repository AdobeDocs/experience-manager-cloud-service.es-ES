---
title: 'Crear una solicitud de API: configuración sin encabezado'
description: Aprenda a utilizar la API de GraphQL para la entrega sin objetivos de contenido de fragmentos de contenido y AEM API de REST de recursos para administrar fragmentos de contenido.
exl-id: 2b72f222-2ba5-4a21-86e4-40c763679c32
source-git-commit: e81b852dc90e3cc5abc8b9f218f48d0fc1cc66eb
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 1%

---

# Crear una solicitud de API: configuración sin encabezado {#accessing-delivering-content-fragments}

Aprenda a utilizar la API de GraphQL para la entrega sin objetivos de contenido de fragmentos de contenido y AEM API de REST de recursos para administrar fragmentos de contenido.

## ¿Qué son las API de REST de GraphQL y Assets? {#what-are-the-apis}

[Ahora que ha creado algunos fragmentos de contenido,](create-content-fragment.md) puede utilizar API AEM para entregarlas sin problemas.

* [La API de GraphQL](/help/headless/graphql-api/content-fragments.md) permite crear solicitudes para acceder a fragmentos de contenido y enviarlos. Esta API ofrece el conjunto más sólido de funciones para consultar y consumir contenido de fragmentos de contenido.
   * Para usar esto, [los extremos deben definirse y habilitarse en AEM](/help/headless/graphql-api/graphql-endpoint.md)y, si es necesario, la variable [Interfaz GraphiQL instalada](/help/headless/graphql-api/graphiql-ide.md).
* [API de REST de Assets](/help/assets/content-fragments/assets-api-content-fragments.md) permite crear y modificar fragmentos de contenido (y otros recursos).

El resto de esta guía se centrará en el acceso a GraphQL y la entrega de fragmentos de contenido.

## Habilitar extremo de GraphQL

Antes de poder utilizar las API de GraphQL, se debe crear un extremo de GraphQL.

1. Vaya a **Herramientas**, **Recursos** y, a continuación, seleccione **GraphQL**.
1. Seleccione **Crear**.
1. La variable **Crear nuevo extremo de GraphQL** se abrirá. Aquí puede especificar:
   * **Nombre**: nombre del extremo; puede escribir cualquier texto.
   * **Utilice el esquema GraphQL proporcionado por**: utilice la lista desplegable para seleccionar la configuración requerida.
1. Confirme con **Crear**.
1. En la consola, una **Ruta** ahora se muestra en función de la configuración creada anteriormente. Esta es la ruta utilizada para ejecutar consultas de GraphQL.

   ```
   /content/cq:graphql/<configuration-name>/endpoint
   ```

Más detalles sobre la activación de [Los extremos de GraphQL se pueden encontrar aquí](/help/headless/graphql-api/graphql-endpoint.md).

## Consulta de contenido mediante GraphQL con GraphiQL

Los arquitectos de la información deberán diseñar consultas para sus extremos de canal para poder entregar contenido. Por lo general, estas consultas solo tendrán que considerarse una vez por punto final por modelo. Para los fines de esta guía de introducción solo tendremos que crear una.

GraphiQL es un IDE que se puede instalar en un entorno AEM. Siga los pasos de [Uso del IDE de GraphiQL](/help/headless/graphql-api/graphiql-ide.md) para instalar en su entorno de AEM.

1. Inicie sesión en AEM as a Cloud Service y acceda a la interfaz de GraphiQL:
   * Por ejemplo: `https://<host>:<port>/content/graphiql.html`.

1. El IDE de GraphiQL es un editor de consultas en el navegador para GraphQL. Puede utilizarla para crear consultas para recuperar fragmentos de contenido y entregarlos en encabezado como JSON.
   * El panel izquierdo le permite crear la consulta.
   * El panel derecho muestra los resultados.
   * El editor de consultas incluye la finalización del código y teclas de acceso directo para ejecutar fácilmente la consulta.
      ![Editor de GraphiQL](../assets/graphiql.png)

1. Suponiendo que el modelo que creamos se llamara `person` con campos `firstName`, `lastName`y `position`, podemos crear una consulta sencilla para recuperar el contenido de nuestro fragmento de contenido.

   ```text
   query 
   {
     personList {
       items {
         _path
         firstName
         lastName
         position
       }
     }
   }
   ```

1. Introduzca la consulta en el panel izquierdo.
   ![Consulta de GraphiQL](../assets/graphiql-query.png)

1. Haga clic en el **Ejecutar consulta** o use el botón `Ctrl-Enter` teclas de acceso directo y los resultados se muestran como JSON en el panel derecho.
   ![Resultados de GraphiQL](../assets/graphiql-results.png)

1. Haga clic en el **Documentos** en la parte superior derecha de la página para mostrar la documentación en contexto que le ayudará a crear sus consultas que se adaptan a sus propios modelos.
   ![Documentación de GraphiQL](../assets/graphiql-documentation.png)

GraphQL permite consultas estructuradas que pueden dirigirse no solo a conjuntos de datos específicos u objetos de datos individuales, sino que también pueden proporcionar elementos específicos de los objetos, resultados anidados, ofrece compatibilidad con variables de consulta y mucho más.

GraphQL puede evitar solicitudes de API iterativas, así como envíos excesivos, y en su lugar permite realizar envíos masivos de exactamente lo que se necesita para procesar como respuesta a una única consulta de API. El JSON resultante se puede utilizar para enviar datos a otros sitios o aplicaciones.

## Siguientes pasos {#next-steps}

¡Eso es todo! Ahora tiene una comprensión básica de la administración de contenido sin encabezado en AEM. Por supuesto, hay muchos más recursos en los que puede profundizar para comprender las funciones disponibles.

* **[Fragmentos de contenido](/help/assets/content-fragments/content-fragments.md)** : para obtener más información sobre la creación y administración de fragmentos de contenido
* **[Compatibilidad con fragmentos de contenido en la API HTTP de AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)** - Para obtener más información sobre el acceso AEM contenido directamente a través de la API HTTP, a través de las operaciones CRUD (Crear, Leer, Actualizar, Eliminar)
* **[API de GraphQL](/help/headless/graphql-api/content-fragments.md)** : para obtener más información sobre cómo enviar fragmentos de contenido sin encabezado
