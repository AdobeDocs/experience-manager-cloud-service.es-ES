---
title: Acceso y entrega de fragmentos de contenido Guía de Inicio rápido sin encabezado
description: La API de REST de Recursos permite administrar fragmentos de contenido y la API de GraphQL permite un envío sencillo y directo del contenido del fragmento de contenido.
translation-type: tm+mt
source-git-commit: 7ed96dc0da879800d731983a0399b4f4fb3d7d41
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---


# Acceso y entrega de fragmentos de contenido Guía de Inicio rápido sin encabezado {#accessing-delivering-content-fragments}

La API de REST de Recursos permite administrar fragmentos de contenido y la API de GraphQL permite un envío sencillo y directo del contenido del fragmento de contenido.

## ¿Qué son las API de REST de GraphQL y Assets? {#what-are-the-apis}

[Ahora que ha creado algunos fragmentos de contenido, ](create-content-fragment.md) puede utilizar API de AEM para distribuirlos sin problemas.

* [La ](/help/assets/content-fragments/graphql-api-content-fragments.md) API de GraphQL le permite crear solicitudes para acceder y enviar fragmentos de contenido.
* [La ](/help/assets/content-fragments/assets-api-content-fragments.md) API de REST de recursos le permite crear y modificar fragmentos de contenido (y otros recursos).

El resto de esta guía se centrará en el acceso a GraphQL y en el envío de fragmentos de contenido.

## Cómo entregar un fragmento de contenido usando GraphQL {#how-to-deliver-a-content-fragment}

Los arquitectos de la información necesitarán diseñar consultas para los extremos de canal a fin de ofrecer contenido. Estas consultas sólo tendrán que considerarse una vez por punto final por modelo. Para los fines de esta guía de introducción solo necesitamos crear una.

1. Inicie sesión en AEM como Cloud Service y, en el menú principal, seleccione **Herramientas -> Recursos -> GraphQL**
   * También puede abrir la página directamente en `https://<host>:<port>/content/graphiql.html`.

1. GraphiQL es un editor de consultas en el navegador para GraphQL. Puede utilizarla para crear consultas para recuperar fragmentos de contenido y distribuirlos de forma directa como JSON.
   * El panel izquierdo le permite crear su consulta.
   * El panel derecho muestra los resultados.
   * El editor de consultas incluye la finalización de código y teclas de acceso directo para ejecutar la consulta con facilidad.
      ![Editor de GraphiQL](../assets/graphiql.png)

1. Suponiendo que el modelo que hemos creado se denominó `person` con los campos `firstName`, `lastName` y `position`, podemos crear una consulta simple para recuperar el contenido de nuestro fragmento de contenido.

   ```
   query {
     persons {
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

1. Haga clic en el botón **Ejecutar Consulta** o utilice la tecla de acceso directo `Ctrl-Enter` y los resultados se mostrarán como JSON en el panel derecho.
   ![Resultados de GraphiQL](../assets/graphiql-results.png)

1. Haga clic en el vínculo **Docs** en la parte superior derecha de la página para mostrar la documentación en contexto y ayudarle a crear sus consultas que se adapten a sus propios modelos.
   ![Documentación de GraphiQL](../assets/graphiql-documentation.png)

GraphQL permite consultas estructuradas que pueden dar destinatario no sólo a conjuntos de datos específicos u objetos de datos individuales, sino también a elementos específicos de los objetos, resultados anidados, ofertas compatibles con variables de consulta y mucho más.

GraphQL puede evitar tanto las solicitudes de API iterativas como el envío excesivo y, en su lugar, permite el envío masivo de exactamente lo que se necesita para el procesamiento como respuesta a una única consulta de API. El JSON resultante se puede usar para enviar datos a otros sitios o aplicaciones.

## Próximos pasos {#next-steps}

¡Eso es todo! Ahora tienes una comprensión básica de gestor de contenido sin cabeza en AEM. Por supuesto, hay muchos más recursos en los que puede profundizar para una comprensión completa de las funciones disponibles.

* **Navegador**  de configuración: para obtener más información sobre el Explorador de configuración de AEM
* **[Fragmentos](/help/assets/content-fragments/content-fragments.md)**  de contenido: para obtener más información sobre la creación y administración de fragmentos de contenido
* **[Compatibilidad con fragmentos de contenido en la API](/help/assets/content-fragments/assets-api-content-fragments.md)**  HTTP de AEM Assets: para obtener más información sobre el acceso al contenido de AEM directamente a través de la API HTTP, mediante operaciones CRUD (Crear, Leer, Actualizar, Eliminar)
* **[API](/help/assets/content-fragments/graphql-api-content-fragments.md)**  de GraphQL: para obtener más información sobre cómo distribuir fragmentos de contenido sin problemas
