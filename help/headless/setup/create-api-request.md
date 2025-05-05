---
title: 'Creación de una solicitud de API: configuración sin encabezado'
description: Aprenda a utilizar la API de GraphQL para la entrega sin encabezado de contenido de fragmentos de contenido y la API de REST de Assets de AEM para administrar fragmentos de contenido.
exl-id: 2b72f222-2ba5-4a21-86e4-40c763679c32
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 89%

---

# Creación de una solicitud de API: configuración sin encabezado {#accessing-delivering-content-fragments}

Aprenda a utilizar la API de GraphQL para la entrega sin encabezado de contenido de fragmentos de contenido y la API de REST de Assets de AEM para administrar fragmentos de contenido.

## ¿Qué son las API de REST de GraphQL y Assets? {#what-are-the-apis}

AEM [Ahora que ha creado algunos fragmentos de contenido](create-content-fragment.md), puede usar las API de envío de la aplicación para enviarlos sin encabezado.

* [La API de GraphQL](/help/headless/graphql-api/content-fragments.md) permite crear solicitudes para acceder a fragmentos de contenido y enviarlos. Esta API ofrece el conjunto más sólido de funciones para consultar y consumir contenido de fragmentos de contenido.
   * Para utilizar la API, [defina y habilite puntos finales en AEM](/help/headless/graphql-api/graphql-endpoint.md) y, si es necesario, la [interfaz de GraphiQL instalada](/help/headless/graphql-api/graphiql-ide.md).
* [La API de REST de Assets](/help/assets/content-fragments/assets-api-content-fragments.md) le permite crear y modificar fragmentos de contenido (y otros recursos).

>[!NOTE]
>
>Las [OpenAPI de fragmento de contenido y modelo de fragmento de contenidos](/help/headless/content-fragment-openapis.md) también están disponibles.

El resto de esta guía se centra en el acceso a GraphQL y la entrega de fragmentos de contenido.

## Habilitación del punto de conexión de GraphQL {#enable-graphql-endpoint}

Antes de poder utilizar las API de GraphQL, se debe crear un punto de conexión de GraphQL.

1. Vaya a **Herramientas**, **General** y, a continuación, seleccione **GraphQL**.
1. Seleccione **Crear**.
1. Se abre el cuadro de diálogo **Crear nuevo punto final de GraphQL**. Aquí puede especificar lo siguiente:
   * **Nombre**: nombre del punto de conexión; puede escribir cualquier texto.
   * **Usar esquema de GraphQL proporcionado por**: use la lista desplegable para seleccionar la configuración requerida.
1. Confirme con **Crear**.
1. En la consola, ahora se muestra una **Ruta** en función de la configuración creada anteriormente. Esta ruta se utiliza para ejecutar consultas de GraphQL.

   ```
   /content/cq:graphql/<configuration-name>/endpoint
   ```

Para obtener más información acerca de cómo habilitar los extremos de GraphQL, consulte [Administrar extremos de GraphQL en la lista de puntos de conexión de AEM en la lista de puntos de conexión de 1&rbrace;.](/help/headless/graphql-api/graphql-endpoint.md)

## Consulta de contenido mediante GraphQL con GraphiQL

Los arquitectos de la información diseñan consultas para sus puntos finales de canal para entregar contenido. Considere estas consultas solo una vez por punto final, por modelo. Para los fines de esta guía de introducción, solo debe crear uno.

GraphiQL es un IDE, incluido en su entorno AEM; es accesible/visible después de [configurar los extremos](#enable-graphql-endpoint).

1. Inicie sesión en AEM as a Cloud Service y acceda a la interfaz de GraphiQL:

   Puede acceder al editor de consultas desde:

   * **Herramientas** > **General** > **Editor de consultas de GraphQL**
   * directamente; por ejemplo, `http://localhost:4502/aem/graphiql.html`

1. El IDE de GraphiQL es un editor de consultas en el explorador para GraphQL. Puede utilizarlo para generar consultas, recuperar fragmentos de contenido y entregarlos sin encabezado como JSON.
   * La parte superior derecha desplegable le permite seleccionar el punto de conexión.
   * Un panel del extremo izquierdo enumera las consultas persistentes (cuando están disponibles)
   * El panel intermedio de la izquierda le permite generar la consulta.
   * El panel intermedio de la derecha muestra los resultados.
   * El editor de consultas incluye la finalización del código y teclas de función para ejecutar fácilmente la consulta.

   ![Editor de GraphiQL](../assets/graphiql.png)

1. Suponiendo que el modelo que hemos creado se llamara `person` con campos `firstName`, `lastName` y `position`, podemos generar una consulta sencilla para recuperar el contenido de nuestro fragmento de contenido.

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

1. Haga clic en el botón **Ejecutar consulta** o use la tecla de función `Ctrl-Enter`, los resultados se mostrarán como JSON en el panel derecho.
   ![Resultados de GraphiQL](../assets/graphiql-results.png)

1. En la esquina superior derecha de la página, haga clic en **Documentos** para mostrar la documentación en contexto y poder crear consultas que se adapten a sus propios modelos.
   ![Documentación de GraphiQL](../assets/graphiql-documentation.png)

GraphQL permite consultas estructuradas que pueden dirigirse no solo a conjuntos de datos específicos u objetos de datos individuales, sino que también pueden proporcionar elementos específicos de los objetos, resultados anidados, compatibilidad con variables de consulta y mucho más.

GraphQL puede evitar las solicitudes de API iterativas y el exceso de entrega, y en su lugar permite realizar entregas masivas de exactamente lo que se necesita para procesar como respuesta a una única consulta de API. El JSON resultante se puede utilizar para entregar datos en otros sitios o aplicaciones.

## Siguientes pasos {#next-steps}

¡Eso es todo! Ahora tiene una comprensión básica de la administración de contenido sin encabezado en AEM. Hay muchos más recursos en los que puede profundizar para comprender las funciones disponibles.

* **[Fragmentos de contenido](/help/sites-cloud/administering/content-fragments/managing.md)**: para obtener más información acerca de la creación y administración de fragmentos de contenido
* **[Compatibilidad con fragmentos de contenido en la API HTTP de AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)**: para obtener más información sobre el acceso al contenido de AEM directamente a través de la API HTTP, mediante las operaciones CRUD (Crear, Leer, Actualizar, Eliminar)
* **[API de GraphQL](/help/headless/graphql-api/content-fragments.md)**: para obtener más información sobre cómo enviar fragmentos de contenido sin encabezado

>[!NOTE]
>
>Las [OpenAPI de fragmento de contenido y modelo de fragmento de contenidos](/help/headless/content-fragment-openapis.md) también están disponibles.
