---
title: Procesamiento del contenido en una aplicación sencilla
description: Explore la recuperación de contenido JSON desde su entorno de prueba con una aplicación de ejemplo CodePen y el cliente sin encabezado de AEM para JavaScript.
hidefromtoc: true
index: false
exl-id: b7dc70f2-74a2-49f7-ae7e-776eab9845ae
source-git-commit: 635f4c990c27a7646d97ebd08b453c71133f01b3
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 98%

---


# Procesamiento del contenido en una aplicación sencilla {#render-content-simple-app}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript"
>title="Procesamiento del contenido en una aplicación sencilla"
>abstract="Explore la recuperación de contenido JSON desde su entorno de prueba con una aplicación de ejemplo CodePen y el cliente sin encabezado de AEM para JavaScript."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide"
>title="Iniciar la aplicación CodePen de muestra"
>abstract="Esta guía explica cómo consultar los datos JSON de su entorno de prueba en una aplicación web básica de JavaScript. Utilizaremos los fragmentos de contenido que ha modelado y creado en los módulos de aprendizaje anteriores, así que consulte estas guías primero antes de empezar esta."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide_footer"
>title="En este módulo, ha aprendido a utilizar el cliente de AEM sin encabezado para JavaScript para recuperar datos JSON de su entorno de prueba mediante consultas persistentes de GraphQL.<br><br>Ahora comprende cómo puede utilizar este cliente para consumir datos desde su propia aplicación web."
>abstract=""

## CodePen {#codepen}

CodePen es un editor de código en línea y un área de reproducción para el desarrollo web front-end. Le permite escribir código HTML, CSS y JavaScript en su explorador y ver los resultados de su trabajo casi al instante. También puede guardar su trabajo y compartirlo con otros. Hemos creado una aplicación en CodePen que puede usar para recuperar datos JSON de su entorno de prueba con el [Cliente sin encabezado de AEM para JavaScript](https://github.com/adobe/aem-headless-client-js). Puede usar esta aplicación tal cual, o ramificarla en su cuenta de CodePen para personalizarla aún más.

Al hacer clic en el botón **Iniciar la aplicación CodePen de ejemplo** de la versión de prueba le llevará a la aplicación en CodePen. La aplicación es un ejemplo mínimo de recuperación de datos JSON con JavaScript. La aplicación de muestra está diseñada para procesar cualquier contenido JSON que se devuelva, independientemente de la estructura del modelo de fragmento de contenido subyacente. De serie, la aplicación recuperará datos de una consulta `aem-demo-assets` persistente que se incluye en el entorno de prueba. Debería ver una respuesta JSON similar a la siguiente:

```json
{
  "data": {
    "adventureList": {
      "items": [
        {
          "_path": "/content/dam/aem-demo-assets/en/adventures/bali-surf-camp/bali-surf-camp",
          "title": "Bali Surf Camp",
          "price": "$5000 USD",
          ...
```

Si ve un error en su lugar, consulte la consola del explorador para obtener más información o póngase en contacto con [en Slack](https://adobe-dx-support.slack.com).

Ahora que conoce un poco sobre CodePen, a continuación configurará la aplicación para recuperar datos de la consulta persistente que creó en un módulo anterior.

## Tutorial de código JavaScript {#code-walkthrough}

La variable **JS** a la derecha de CodePen contiene el JavaScript de la aplicación de ejemplo. A partir de la línea 2, importamos el cliente de AEM sin encabezado para JavaScript desde la CDN de Skypack. Skypack se utiliza para facilitar el desarrollo sin un paso de compilación, pero también puede utilizar el cliente de AEM sin encabezado con NPM o Yarn en sus propios proyectos. Consulte las instrucciones de uso en el archivo [Léame](https://github.com/adobe/aem-headless-client-js#aem-headless-client-for-javascript) para obtener más información.

```javascript
import AdobeAemHeadlessClientJs from 'https://cdn.skypack.dev/@adobe/aem-headless-client-js@v3.2.0';
```

En la línea 6, leemos los detalles de su host de publicación desde el parámetro de consulta `publishHost`. Este es el host desde el que el cliente de AEM sin encabezado recuperará los datos. Normalmente, esto se codificaría en la aplicación, pero se utiliza un parámetro de consulta para facilitar el trabajo de la aplicación CodePen con distintos entornos.

Configuramos el cliente sin encabezado de AEM en la línea 12:

```javascript
const aemHeadlessClient = new AdobeAemHeadlessClientJs({
  // Use a proxy to avoid CORS issues
  serviceURL: 'https://102588-505tanocelot.adobeioruntime.net/api/v1/web/aem/proxy',
  headers: {
    'aem-url': publishHost
  }
});
```

>[!NOTE]
>
>La variable **serviceURL** está configurada para utilizar una función de tiempo de ejecución de IO de Adobe proxy para evitar problemas con CORS. Esto no es necesario para sus propios proyectos, pero sí para que la aplicación CodePen funcione con el entorno de prueba. La función proxy está configurada para utilizar el valor **publishHost** que se proporcionó en el parámetro de consulta.

Por último, la función `fetchJsonFromGraphQL()` se utiliza para realizar la solicitud de recuperación mediante el cliente de AEM sin encabezado. Se llama cada vez que se modifica el código, o se puede activar pulsando el enlace **Volver a obtener**. La llamada `aemHeadlessClient.runPersistedQuery(..)` en sí se realiza en la línea 34. Un poco más adelante haremos un cambio en la forma en que estos datos JSON se procesan, pero por ahora vamos a imprimirlos en el div `#output` utilizando la función `resultToPreTag(queryResult)`.

## Recuperar datos de la consulta persistente {#use-persisted-query}

En la línea 25 indicamos de qué consulta persistente de GraphQL debe recuperar datos la aplicación. El nombre de la consulta persistente es una combinación del nombre del punto final (es decir, `your-project` o `aem-demo-assets`), seguido de una barra diagonal y, a continuación, el nombre de la consulta. Si ha seguido exactamente las instrucciones de módulo anteriores, la consulta persistente que ha creado se encuentra en el `your-project` punto final.

1. Actualice la variable `persistedQueryName` para utilizar la consulta persistente que ha creado en el módulo anterior. Si hubiera seguido exactamente la sugerencia de asignación de nombres, habría creado una consulta persistente denominada `adventure-list` en el punto final `your-project`, y habría establecido la variable `persistedQueryName` en `your-project/adventure-list`:

   ```javascript
   //
   // TODO: Use your persisted query here
   //
   persistedQueryName = 'your-project/adventure-list';
   ```

1. Una vez realizado este cambio, la aplicación debería actualizarse automáticamente e imprimir la respuesta JSON sin procesar de la consulta persistente en el div `#output`. Si aparece un mensaje de error, compruebe la consola para obtener más información. Alcance [en Slack](https://adobe-dx-support.slack.com) si sigue teniendo problemas con este paso.

1. ¿Este JSON contiene las propiedades exactas que necesita la aplicación? Si no es así, vuelva a la guía de aprendizaje [Extraer contenido mediante la API de GraphQL](https://experience.adobe.com/experiencemanager/learn/extract_content_using_graphql) para realizar cambios. No olvide guardar y publicar la consulta una vez que haya terminado.

## Cambiar el procesamiento de JSON {#change-rendering}

Actualmente, el JSON se está procesando tal cual en una etiqueta `pre`, lo que no es muy creativo. Podemos cambiar nuestro CodePen para utilizar la función `resultToDom()` en su lugar para ilustrar cómo se puede iterar sobre la respuesta JSON para crear un resultado más interesante.

1. Para realizar este cambio, comente la línea 37 y quite el comentario de la línea 40:

   ```javascript
   // Output the results to a pre tag
   //resultToPreTag(queryResult);
   
   // Alternatively, build a colorful div structure with the JSON results and render images inline
   resultToDom(queryResult);
   ```

1. Esta función también procesará cualquier imagen incluida en la respuesta JSON como una etiqueta `img`. Si los fragmentos de contenido **Aventura** que ha creado no incluyen ninguna imagen, puede intentar cambiar para utilizar la `aem-demo-assets/adventures-all` consulta persistente modificando la línea 25:

   ```javascript
   persistedQueryName = 'aem-demo-assets/adventures-all';
   ```

Esta consulta generará una respuesta JSON que incluye imágenes, y la función `resultToDom()` las procesará en línea.

![Resultado de la consulta adventures-all y de la función de procesamiento resultToDom](assets/do-not-localize/adventures-all-query-result.png)

Ahora que ha hecho el trabajo para generar los modelos y las consultas, su equipo de contenido puede asumir el control con facilidad. Se mostrará el flujo de creación de contenido en el siguiente módulo.
