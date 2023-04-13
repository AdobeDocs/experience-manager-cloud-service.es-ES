---
title: Recuperación de contenido JSON con JavaScript
description: Explore la recuperación de contenido JSON desde su entorno de prueba con una aplicación CodePen y el cliente sin encabezado AEM para JavaScript.
hidefromtoc: true
index: false
source-git-commit: 3aff5ef2fb9ecdd815f0bc1a813d3a3982b4e0ed
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 0%

---


# Recuperación de contenido JSON con JavaScript {#fetch-json}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript"
>title="Recuperación de contenido JSON con JavaScript"
>abstract="Explore la recuperación de contenido JSON desde su entorno de prueba con una aplicación CodePen y el cliente sin encabezado AEM para JavaScript."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide"
>title="Inicie la aplicación CodePen de ejemplo"
>abstract="Hemos creado una aplicación CodePen mínima para presentar la recuperación de datos JSON de su entorno de prueba mediante consultas persistentes de GraphQL.<br><br>Inicie el ejemplo de CodePen haciendo clic a continuación y siga esta guía para obtener más información."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide_footer"
>title="En este módulo, ha aprendido a utilizar el cliente sin encabezado de AEM para JavaScript para recuperar datos JSON de su entorno de prueba mediante consultas persistentes de GraphQL.<br><br>Ahora comprende cómo puede utilizar este cliente para consumir datos desde su propia aplicación web."
>abstract=""

## Introducción {#intro}

Comienza en la aplicación CodePen, que sirve como ejemplo mínimo de recuperación de datos JSON mediante el uso de [AEM cliente sin encabezado para JavaScript](https://github.com/adobe/aem-headless-client-js). La aplicación de ejemplo está diseñada para procesar cualquier contenido JSON que se devuelva, independientemente de la estructura del modelo de fragmento de contenido subyacente. La aplicación CodePen intenta ser exhaustiva con cualquier error que se encuentre, por lo que puede ver el siguiente mensaje de error impreso en el panel inferior de la aplicación:

```
{
  "status": "Failed to fetch persisted query: your-project/USE-YOUR-QUERY-HERE from publishHost: https://publish-p00000-e12345.adobeaemcloud.com",
  "message": "[AEMHeadless:REQUEST_ERROR] General Request error: Failed to fetch."
}
```

Se espera este error, ya que la aplicación aún no está configurada para utilizar la consulta persistente que guardó y publicó en un módulo anterior. La aplicación se configurará para recuperar datos de la consulta específica en los pasos siguientes.

## Recorrido por CodePen {#code-walkthrough}

El panel JS (Javascript) de CodePen contiene los cerebros de la aplicación de ejemplo. A partir de la línea 2, importamos el cliente sin encabezado AEM para JavaScript desde la CDN Skypack. Skypack se utiliza para facilitar el desarrollo sin un paso de compilación, pero también puede utilizar el cliente sin encabezado AEM con NPM o Yarn en sus propios proyectos. Consulte las instrucciones de uso en la [README](https://github.com/adobe/aem-headless-client-js#aem-headless-client-for-javascript) para obtener más información.

```
import AdobeAemHeadlessClientJs from 'https://cdn.skypack.dev/@adobe/aem-headless-client-js@v3.2.0';
```

En la línea 6 leemos los detalles de su host de publicación desde la `publishHost` parámetro de consulta. Este es el host desde el que el cliente sin encabezado de AEM recuperará datos. Normalmente, esto se codificaría en la aplicación, pero se utiliza un parámetro de consulta para facilitar el trabajo de la aplicación CodePen con distintos entornos.

Configuramos el cliente sin AEM en la línea 12 para utilizar una función de tiempo de ejecución de IO de Adobe proxy para evitar problemas con CORS. Esto no es necesario para sus propios proyectos, pero es necesario para que la aplicación CodePen funcione con su entorno de prueba. La función proxy está configurada para usar la variable `publishHost` que se proporcionó en el parámetro de consulta.

```
const aemHeadlessClient = new AdobeAemHeadlessClientJs({
  // Use a proxy to avoid CORS issues
  serviceURL: 'https://102588-505tanocelot.adobeioruntime.net/api/v1/web/aem/proxy',
  headers: {
    'aem-url': publishHost
  }
});
```

Finalmente, la función `fetchJsonFromGraphQL()` se utiliza para realizar la solicitud de recuperación mediante el cliente sin encabezado AEM. Se llama cada vez que se cambia el código o se puede activar pulsando el vínculo &quot;Recuperación&quot;. El `aemHeadlessClient.runPersistedQuery(..)` se produce en la línea 34. Un poco más tarde haremos un cambio en la forma en que se procesan los datos JSON, pero por ahora solo lo imprimiremos en la variable `#output` div usando la variable `resultToPreTag(queryResult)` función.

## Recuperación de datos de la consulta persistente {#use-persisted-query}

En la línea 25 indicamos de qué consulta de GraphQL persistió la aplicación y desde qué la aplicación debería recuperar datos. El nombre de la consulta persistente es una combinación del nombre del proyecto (por ejemplo, `your-project`), seguido de una barra diagonal y, a continuación, el nombre de la consulta.

Actualice el `persistedQueryName` para utilizar la consulta persistente que creó en el módulo anterior. Si hubiera seguido la sugerencia de asignación de nombres exactamente habría creado una consulta persistente denominada `adventures` en el `your-project` y establecería la variable `persistedQueryName` a `your-project/adventures`:

```
//
// TODO: Use your persisted query here
//
persistedQueryName = 'your-project/adventures';
```

Una vez realizado este cambio, la aplicación debe actualizarse automáticamente e imprimir la respuesta JSON sin procesar de la consulta persistente en la variable `#output` div. Si ve un mensaje de error, consulte la consola para obtener más información.

¿Contiene este JSON las propiedades exactas que necesita su aplicación? Si no es así, vuelva al entorno de AEM Author, a las herramientas o al Editor de consultas de GraphQL (o vaya a la `/aem/graphiql.html` ) y realice cambios en la consulta persistente. No olvide guardar y publicar la consulta una vez que haya terminado.

## Cambiar la renderización JSON {#change-rendering}

Actualmente, el JSON se está procesando tal cual en un `pre` , que no es muy creativa. Podemos cambiar nuestro CodePen para usar el `resultToDom()` para ilustrar cómo se puede iterar la respuesta JSON para crear un resultado más interesante.

Para realizar este cambio, comente la línea 37 y elimine el comentario de la línea 40:

```
// Output the results to a pre tag
//resultToPreTag(queryResult);

// Alternatively, build a colorful div structure with the JSON results and render images inline
resultToDom(queryResult);
```

Esta función también procesará todas las imágenes incluidas en la respuesta JSON como una `img` etiqueta. Si los fragmentos de contenido &quot;Aventura&quot; que ha creado no incluyen imágenes, puede intentar cambiar para usar la variable `aem-demo-assets/adventures-all` consulta persistente mediante la modificación de la línea 25:

```
persistedQueryName = 'aem-demo-assets/adventures-all';
```

Esta consulta generará una respuesta JSON que incluye imágenes y la variable `resultToDom()` los procesará en línea.

![Resultado de la consulta adventures-all y de la función de renderización resultToDom](assets/do-not-localize/adventures-all-query-result.png)
