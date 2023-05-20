---
title: Procesar el contenido en una aplicación sencilla
description: Explore la recuperación de contenido JSON desde su entorno de prueba con una aplicación de ejemplo CodePen y el cliente sin encabezado de AEM para JavaScript.
hidefromtoc: true
index: false
exl-id: b7dc70f2-74a2-49f7-ae7e-776eab9845ae
source-git-commit: 1949ee211b4f816e05aa779deb9e287347f006ad
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 48%

---


# Procesar el contenido en una aplicación sencilla {#render-content-simple-app}

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

CodePen es un editor de código en línea y un área de reproducción para el desarrollo web front-end. Permite escribir código HTML, CSS y JavaScript en el explorador y ver los resultados de su trabajo casi al instante. También puede guardar su trabajo y compartirlo con otros. Hemos creado una aplicación en CodePen que puede utilizar para recuperar datos JSON de su entorno de prueba con el [AEM Cliente sin encabezado para JavaScript](https://github.com/adobe/aem-headless-client-js). Puede utilizar esta aplicación tal cual, o ramificarla en su cuenta de CodePen para personalizarla más.

Haciendo clic en **Inicie la aplicación CodePen de ejemplo.** del periodo de prueba lo llevará a la aplicación en CodePen. La aplicación sirve como un ejemplo mínimo de captura de datos JSON con JavaScript. La aplicación de ejemplo está diseñada para procesar cualquier contenido JSON que se devuelva, independientemente de la estructura del modelo de fragmento de contenido subyacente. De forma predeterminada, la aplicación recuperará datos de un `aem-demo-assets` consulta persistente incluida en el entorno de prueba. Debería ver una respuesta JSON similar a la siguiente:

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

Si aparece un error, compruebe la consola del explorador para obtener más detalles o póngase en contacto con [en el Slack](https://adobe-dx-support.slack.com).

Ahora que conoce un poco sobre CodePen, a continuación configurará la aplicación para recuperar datos de la consulta persistente que creó en un módulo anterior.

## Tutorial con código JavaScript {#code-walkthrough}

El **JS** a la derecha en CodePen contiene el código JavaScript de la aplicación de ejemplo. A partir de la línea 2, importamos el cliente de AEM sin encabezado para JavaScript desde la CDN de Skypack. Skypack se utiliza para facilitar el desarrollo sin un paso de compilación, pero también puede utilizar el cliente de AEM sin encabezado con NPM o Yarn en sus propios proyectos. Consulte las instrucciones de uso en el archivo [Léame](https://github.com/adobe/aem-headless-client-js#aem-headless-client-for-javascript) para obtener más información.

```javascript
import AdobeAemHeadlessClientJs from 'https://cdn.skypack.dev/@adobe/aem-headless-client-js@v3.2.0';
```

En la línea 6, leemos los detalles de su host de publicación desde el parámetro de consulta `publishHost`. Este es el host desde el que el cliente de AEM sin encabezado recuperará los datos. Normalmente, esto se codificaría en la aplicación, pero se utiliza un parámetro de consulta para facilitar el trabajo de la aplicación CodePen con distintos entornos.

AEM Configuramos el cliente sin encabezado de la línea 12:

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
>El **serviceURL** está configurado para utilizar una función de tiempo de ejecución de E/S de Adobe proxy para evitar problemas de CORS. Esto no es necesario para sus propios proyectos, pero sí para que la aplicación CodePen funcione con el entorno de prueba. La función proxy está configurada para utilizar el **publishHost** valor proporcionado en el parámetro de consulta.

Por último, la función `fetchJsonFromGraphQL()` se utiliza para realizar la solicitud de recuperación mediante el cliente de AEM sin encabezado. Se llama cada vez que se cambia el código o se puede activar haciendo clic en el **Recuperar** vínculo. La llamada `aemHeadlessClient.runPersistedQuery(..)` en sí se realiza en la línea 34. Un poco más adelante haremos un cambio en la forma en que estos datos JSON se procesan, pero por ahora vamos a imprimirlos en el div `#output` utilizando la función `resultToPreTag(queryResult)`.

## Recuperación de datos de la consulta persistente {#use-persisted-query}

En la línea 25 indicamos de qué consulta persistente de GraphQL debe recuperar datos la aplicación. El nombre de la consulta persistente es una combinación del nombre del extremo (es decir, `your-project` o `aem-demo-assets`), seguido de una barra diagonal y el nombre de la consulta. Si ha seguido exactamente las instrucciones de módulo anteriores, la consulta persistente que ha creado estará en el `your-project` punto final.

1. Actualice la variable `persistedQueryName` para utilizar la consulta persistente que ha creado en el módulo anterior. Si hubiera seguido la sugerencia de nomenclatura, habría creado una consulta persistente denominada `adventure-list` en el `your-project` extremo, y establecería la variable `persistedQueryName` variable a `your-project/adventure-list`:

   ```javascript
   //
   // TODO: Use your persisted query here
   //
   persistedQueryName = 'your-project/adventure-list';
   ```

1. Una vez realizado este cambio, la aplicación debería actualizarse automáticamente e imprimir la respuesta JSON sin procesar de la consulta persistente en el div `#output`. Si aparece un mensaje de error, compruebe la consola para obtener más información. Extender la mano [en el Slack](https://adobe-dx-support.slack.com) si sigue teniendo problemas con este paso.

1. ¿Este JSON contiene las propiedades exactas que necesita la aplicación? Si no es así, vuelva al [Extraer contenido mediante la API de GraphQL](https://experience.adobe.com/experiencemanager/learn/extract_content_using_graphql) guía de aprendizaje para realizar cambios. No olvide guardar y publicar la consulta una vez que haya terminado.

## Cambiar el procesamiento de JSON {#change-rendering}

El JSON se procesa tal cual en un `pre` , que no es muy creativo. Podemos cambiar nuestro CodePen para utilizar la función `resultToDom()` en su lugar para ilustrar cómo se puede iterar sobre la respuesta JSON para crear un resultado más interesante.

1. Para realizar este cambio, comente la línea 37 y quite el comentario de la línea 40:

   ```javascript
   // Output the results to a pre tag
   //resultToPreTag(queryResult);
   
   // Alternatively, build a colorful div structure with the JSON results and render images inline
   resultToDom(queryResult);
   ```

1. Esta función también procesará cualquier imagen incluida en la respuesta JSON como una etiqueta `img`. Si la variable **Aventura** los fragmentos de contenido que ha creado no incluyen imágenes. puede intentar cambiar a usar la variable `aem-demo-assets/adventures-all` consulta persistente al modificar línea 25:

   ```javascript
   persistedQueryName = 'aem-demo-assets/adventures-all';
   ```

Esta consulta generará una respuesta JSON que incluye imágenes, y la función `resultToDom()` las procesará en línea.

![Resultado de la consulta adventures-all y de la función de procesamiento resultToDom](assets/do-not-localize/adventures-all-query-result.png)

Ahora que ha hecho el trabajo para crear los modelos y las consultas, su equipo de contenido puede encargarse con facilidad. Mostraremos el flujo de creación de contenido en el siguiente módulo.
