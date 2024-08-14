---
title: Extracción de contenido mediante la API de GraphQL
description: Aprenda a utilizar los fragmentos de contenido y la API de GraphQL como un sistema de administración de contenido sin encabezado.
hidefromtoc: true
index: false
exl-id: f5e379c8-e63e-41b3-a9fe-1e89d373dc6b
feature: Headless
role: Admin, User, Developer
source-git-commit: f66ea281e6abc373e9704e14c97b77d82c55323b
workflow-type: ht
source-wordcount: '1069'
ht-degree: 100%

---


# Extracción de contenido mediante la API de GraphQL {#extract-content}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_graphql"
>title="Extraer contenido mediante la API de GraphQL"
>abstract="En este módulo aprenderá a utilizar los fragmentos de contenido y la API de GraphQL como un sistema de administración de contenido sin encabezado."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_graphql_guide"
>title="Lanzamiento de GraphQL Explorer"
>abstract="GraphQL proporciona una API basada en consultas que permite a las aplicaciones de cliente externas realizar consultas en AEM solo para el contenido que necesita, mediante una sola llamada de API. Siga este módulo para aprender a ejecutar dos tipos diferentes de consultas. A continuación, aprenda a recuperar el contenido del fragmento de contenido creado en el módulo anterior.<br><br>Inicie este módulo en una nueva pestaña haciendo clic abajo."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_graphql_guide_footer"
>title="Buen trabajo. Ha obtenido información sobre los dos tipos básicos de consultas y cómo consultar su propio contenido. Ya sabe cómo usar la API de GraphQL de AEM para crear consultas eficientes que entreguen contenido en el formato que la aplicación espera."
>abstract=""

## Consulta de una lista de contenido de muestra {#list-query}

Inicie GraphQL Explorer en una pestaña nueva. Aquí puede generar y validar consultas sobre su contenido sin encabezado antes de utilizarlas para impulsar el contenido en su aplicación o sitio web.

1. La versión de prueba de AEM sin encabezado incluye un punto final precargado con fragmentos de contenido desde el que se puede extraer contenido para pruebas. Asegúrese de que el punto final **Recursos de demostración de AEM** esté seleccionado en el menú desplegable **Punto final** en la esquina superior derecha del editor.

1. Copie el siguiente fragmento de código para una consulta de lista del punto final **Recursos de demostración de AEM**. La consulta de lista devuelve una lista de todo el contenido que utiliza el modelo de fragmento de contenido específico. Las páginas de inventario y categoría suelen utilizar este formato de consulta.

   ```text
   {
    adventureList {
     items {
       _path
       title
       price
       tripLength
       primaryImage {
         ... on ImageRef {
           _path
           mimeType
           width
           height
         }
       }
     }
    }
   }
   ```

1. Reemplace el contenido existente en el editor de consultas pegando el código copiado.

1. Una vez pegado, haga clic en el botón **Reproducir** en la parte superior izquierda del editor de consultas para ejecutar la consulta.

1. Los resultados se muestran en el panel derecho, junto al editor de consultas. Si la consulta es incorrecta, aparece “error” en el panel derecho.

   ![Consulta de lista](assets/do-not-localize/list-query-1-3-4-5.png)

Acaba de validar una consulta de lista para obtener una lista completa de todos los fragmentos de contenido. Este proceso garantiza que la respuesta sea lo que espera la aplicación, con resultados que ilustran cómo las aplicaciones y sitios web recuperarán el contenido creado en AEM.

## Consulta de un fragmento específico de contenido de muestra {#bypath-query}

La ejecución de una consulta byPath permite recuperar contenido para un fragmento de contenido específico. Las páginas de detalles del producto y las que se centran en un conjunto específico de contenido, generalmente, requieren este tipo de consulta.

1. Copie el siguiente fragmento de código para una consulta byPath del punto final **Recursos de demostración de AEM** precargado.

   ```text
    {
     adventureByPath(
       _path: "/content/dam/aem-demo-assets/en/adventures/bali-surf-camp/bali-surf-camp"
     ) {
       item {
         _path
         title
         description {
           json
         }
         primaryImage {
           ... on ImageRef {
             _path
             width
             height
           }
         }
       }
     }
   }
   ```

1. Reemplace el contenido existente en el editor de consultas pegando el código copiado.

1. Una vez pegado, haga clic en el botón **Reproducir** en la parte superior izquierda del editor de consultas para ejecutar la consulta.

1. Los resultados se muestran en el panel derecho, junto al editor de consultas. Si la consulta es incorrecta, aparece “error” en el panel derecho.

   ![Resultados de consulta de byPath](assets/do-not-localize/bypath-query-2-3-4.png)

Acaba de validar una consulta byPath para recuperar un fragmento de contenido específico identificado por la ruta de ese fragmento.

## Consulta de su propio contenido {#own-queries}

Ahora que ha ejecutado los dos tipos principales de consultas, está listo para consultar su propio contenido.

1. Para ejecutar consultas con sus propios fragmentos de contenido, cambie el punto final de la carpeta **Recursos de demostración de AEM** a la carpeta **Su proyecto**.

1. Elimine todo el contenido existente en el editor de consultas. A continuación, escriba la llave de apertura `{` y pulse Ctrl+Espacio u Opción+Espacio para ver una lista de autocompletar de los modelos definidos en el punto final. Seleccione el modelo que ha creado y que termina en `List` en las opciones. Si ha seguido los ejemplos de los módulos anteriores, deberá encontrar `adventureList` en la lista de autocompletar.

   ![Inicio de consulta personalizada](assets/do-not-localize/custom-query-1.png)

1. Defina los elementos que debe contener la consulta para el modelo de fragmento de contenido que ha seleccionado. De nuevo, escriba la llave de apertura `{` y, a continuación, pulse Ctrl+Espacio u Opción+Espacio para ver una lista de autocompletado. Seleccione `items` de las opciones.

1. Haga clic en el botón **Embellecer** para dar formato automáticamente al código y facilitar su lectura.

1. Una vez finalizada, haga clic en el botón **Reproducir** en la parte superior izquierda del editor para ejecutar la consulta. El editor completa automáticamente los `items`, que se resaltan brevemente en amarillo, y se ejecuta la consulta.

1. Los resultados se muestran en el panel derecho, junto al editor de consultas.

   ![Ejecución de una consulta personalizada](assets/do-not-localize/custom-query-2.png)

Así es como el contenido se puede entregar en experiencias digitales omnicanal.

## Consultas persistentes {#persisted-queries}

Las consultas persistentes son el mecanismo preferido para exponer la API de GraphQL a las aplicaciones cliente. Una vez que una consulta persiste, esta se puede solicitar mediante una petición de GET y almacenar en caché para una recuperación rápida.

Puede crear una consulta persistente que incluya los datos que desee consumir de la aplicación cliente.

1. Utilizará los datos que ha creado como fragmento de contenido anteriormente, por lo que asegúrese de que el punto de conexión de **Su proyecto** está seleccionado en el menú desplegable **Punto de conexión** en la esquina superior derecha del editor.

1. Copie el siguiente fragmento de código.

   ```text
      {
      adventureList {
       items {
         title
         description {
           plaintext
         }
         price
         image {
           ... on ImageRef {
             _publishUrl
             mimeType
           }
         }
       }
     }
   }
   ```

1. Reemplace el contenido existente en el editor de consultas pegando el código copiado.

   >[!NOTE]
   >
   >Si no ha utilizado las mismas descripciones de campo que se describen en los módulos anteriores, actualice los nombres de campo en esta consulta.
   >
   >Utilice la función de autocompletado de GraphQL (Ctrl+Espacio u Opción+Espacio) como se describió anteriormente para ayudar a identificar las propiedades disponibles.

1. Una vez pegado, haga clic en el botón **Reproducir** en la parte superior izquierda del editor de consultas para ejecutar la consulta.

1. Los resultados se muestran en el panel derecho, junto al editor de consultas. Si la consulta es incorrecta, aparece “error” en el panel derecho.

   ![Crear una consulta propia](assets/do-not-localize/own-query.png)

1. Cuando esté satisfecho con la consulta, haga clic en el botón **Guardar como** en la parte superior del editor de consultas para mantener la consulta.

1. En el elemento emergente de **Nombre de la consulta**, asígnele el nombre a la consulta `adventure-list`.

1. Seleccione **Guardar como**.

   ![Consulta persistente](assets/do-not-localize/persist-query.png)

1. La consulta se mantiene tal y como se confirma con un mensaje de banner en la parte inferior de la pantalla. La consulta ahora aparece en el panel izquierdo de consultas persistentes de la ventana.

1. Para que la consulta persistente esté disponible públicamente, deberá publicarse, de forma muy parecida a cómo deben publicarse los Fragmentos de contenido. Haga clic en el botón **Publicar** en la parte superior derecha del editor de consultas para publicar la consulta.

1. La publicación se confirma mediante una notificación de banner.

Ahora tiene una nueva consulta persistente que contendrá únicamente las propiedades y los formatos específicos definidos.
