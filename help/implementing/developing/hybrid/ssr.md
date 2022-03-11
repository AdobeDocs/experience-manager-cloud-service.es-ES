---
title: SPA y procesamiento en el servidor
description: El uso del procesamiento del lado del servidor (SSR) en el SPA puede acelerar la carga inicial de la página y, a continuación, pasar el procesamiento adicional al cliente.
exl-id: be409559-c7ce-4bc2-87cf-77132d7c2da1
source-git-commit: 4965bd30c02536efb81a26fff8da6e5f75dbfae4
workflow-type: tm+mt
source-wordcount: '1502'
ht-degree: 0%

---

# SPA y procesamiento en el servidor{#spa-and-server-side-rendering}

Las aplicaciones de una sola página (SPA) pueden ofrecer al usuario una experiencia rica y dinámica que reacciona y se comporta de formas familiares, a menudo como una aplicación nativa. [Esto se logra confiando en que el cliente cargue el contenido por adelantado y luego haga el trabajo pesado de manejar la interacción del usuario](introduction.md#how-does-a-spa-work) y, de este modo, se minimiza la cantidad de comunicación necesaria entre el cliente y el servidor, lo que hace que la aplicación sea más reactiva.

Sin embargo, esto puede provocar tiempos de carga iniciales más largos, especialmente si el SPA es grande y tiene un contenido enriquecido. Para optimizar los tiempos de carga, parte del contenido se puede representar en el lado del servidor. El uso de la renderización del lado del servidor (SSR) puede acelerar la carga inicial de la página y luego pasar una renderización adicional al cliente.

## Cuándo utilizar SSR {#when-to-use-ssr}

La SSR no es necesaria en todos los proyectos. Aunque AEM admite totalmente la SSR de JS para SPA, Adobe no recomienda implementarla sistemáticamente para cada proyecto.

Al decidir implementar SSR, primero debe estimar qué complejidad adicional, esfuerzo y costo de agregar SSR representa de manera realista para el proyecto, incluido el mantenimiento a largo plazo. Una arquitectura SSR solo debe elegirse cuando el valor añadido exceda claramente los costes estimados.

SSR normalmente proporciona algún valor cuando hay un claro &quot;sí&quot; a cualquiera de las siguientes preguntas:

* **SEO:** ¿Sigue siendo necesario realizar una SSR para que el sitio esté correctamente indexado por los motores de búsqueda que traen tráfico? Tenga en cuenta que los principales rastreadores de motores de búsqueda ahora evalúan JS.
* **Velocidad de página:** ¿La SSR proporciona una mejora de velocidad mensurable en entornos reales y contribuye a la experiencia del usuario general?

Solo cuando al menos una de estas dos preguntas se responda con un claro &quot;sí&quot; para el proyecto, Adobe recomienda implementar SSR. Las secciones siguientes describen cómo hacerlo mediante Adobe I/O Runtime.

## Adobe I/O Runtime {#adobe-i-o-runtime}

Si [están seguros de que su proyecto requiere la implementación de SSR](#when-to-use-ssr), la solución recomendada de Adobe es utilizar Adobe I/O Runtime.

Para obtener más información sobre Adobe I/O Runtime, consulte

* [https://www.adobe.io/apis/experienceplatform/runtime.html](https://www.adobe.io/apis/experienceplatform/runtime.html) - para una descripción general del servicio
* [https://www.adobe.io/apis/experienceplatform/runtime/docs.html](https://www.adobe.io/apis/experienceplatform/runtime/docs.html) : para obtener documentación detallada sobre la plataforma

Las secciones siguientes detallan cómo se puede utilizar Adobe I/O Runtime para implementar SSR para su SPA en dos modelos diferentes:

* [Flujo de comunicación AEM](#aem-driven-communication-flow)
* [Flujo de comunicación impulsado por Adobe I/O Runtime](#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>Adobe recomienda un espacio de trabajo de Adobe I/O Runtime independiente por entorno (etapa, producto, prueba, etc.). Esto permite patrones típicos del ciclo de vida del desarrollo de sistemas (SDLC) con distintas versiones de una sola aplicación implementada en diferentes entornos. Consulte el documento [CI/CD para aplicaciones de luciérnagas del proyecto](https://www.adobe.io/apis/experienceplatform/project-firefly/docs.html#!AdobeDocs/project-firefly/master/guides/ci_cd_for_firefly_apps.md) para obtener más información.
>
>No se necesita un espacio de trabajo independiente por instancia (autor, publicación) a menos que haya diferencias en la implementación de tiempo de ejecución por tipo de instancia.

## Configuración del procesador remoto {#remote-content-renderer-configuration}

AEM saber dónde se puede recuperar el contenido procesado de forma remota. Independientemente de [qué modelo elige implementar para SSR,](#adobe-i-o-runtime) tendrá que especificar cómo AEM acceder a este servicio de procesamiento remoto.

Esto se realiza mediante la variable **RemoteContentRenderer - Servicio OSGi de fábrica de configuración**. Busque la cadena &quot;RemoteContentRenderer&quot; en la consola de configuración de la consola web en `http://<host>:<port>/system/console/configMgr`.

![Configuración del procesador](assets/renderer-configuration.png)

Los campos siguientes están disponibles para la configuración:

* **Patrón de ruta de contenido** - Expresión regular para que coincida con una parte del contenido, si es necesario
* **URL de extremo remoto** - URL del punto final responsable de generar el contenido
   * Utilice el protocolo HTTPS protegido si no está en la red local.
* **Encabezados de solicitud adicionales** - Encabezados adicionales que se añadirán a la solicitud enviada al extremo remoto
   * Patrón: `key=value`
* **Tiempo de espera de la solicitud** - Tiempo de espera de solicitud de host remoto en milisegundos

>[!NOTE]
>
>Independientemente de si decide implementar la variable [Flujo de comunicación AEM](#aem-driven-communication-flow) o [Flujo impulsado por Adobe I/O Runtime,](#adobe-i-o-runtime-driven-communication-flow) debe definir una configuración del procesador de contenido remoto.

>[!NOTE]
>
>Esta configuración aprovecha el [Procesador de contenido remoto,](#remote-content-renderer) que tiene opciones adicionales de extensión y personalización disponibles.

## Flujo de comunicación AEM {#aem-driven-communication-flow}

Cuando se utiliza SSR, la variable [flujo de trabajo de interacción de componentes](introduction.md#interaction-with-the-spa-editor) de SPA en AEM incluye una fase en la que el contenido inicial de la aplicación se genera en Adobe I/O Runtime.

1. El navegador solicita el contenido SSR a AEM.
1. AEM publica el modelo en Adobe I/O Runtime.
1. Adobe I/O Runtime devuelve el contenido generado.
1. AEM sirve al HTML devuelto por Adobe I/O Runtime a través de la plantilla HTL del componente de página back-end.

![Adobe I/O de AEM impulsado por SSE CMS](assets/ssr-cms-drivenaemnode-adobeio.png)

## Flujo de comunicación impulsado por Adobe I/O Runtime {#adobe-i-o-runtime-driven-communication-flow}

La sección anterior describe la implementación estándar y recomendada del procesamiento del lado del servidor con respecto a la SPA en AEM, donde AEM realiza el arranque y la entrega del contenido.

Alternativamente, SSR puede implementarse para que Adobe I/O Runtime sea responsable del arranque, revirtiendo efectivamente el flujo de comunicación.

Ambos modelos son válidos y son compatibles con AEM. Sin embargo, hay que tener en cuenta las ventajas y desventajas de cada uno antes de aplicar un modelo determinado.

<table>
 <tbody>
  <tr>
   <th><strong>Agrupamiento</strong></th>
   <th><strong>Ventajas</strong></th>
   <th><strong>Desventajas</strong></th>
  </tr>
  <tr>
   <th><strong>a través de AEM</strong><br /> </th>
   <td>
    <ul>
     <li>AEM administra las bibliotecas de inyección donde sea necesario</li>
     <li>Los recursos sólo deben mantenerse en AEM<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Posiblemente no esté familiarizado con SPA desarrollador<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <th><strong>a través de Adobe I/O Runtime<br /> </strong></th>
   <td>
    <ul>
     <li>Más familiarizado con los desarrolladores de SPA<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Los recursos de Clientlib requeridos por la aplicación, como CSS y JavaScript, deberán estar disponibles para el desarrollador de AEM a través del <code><a href="/help/implementing/developing/introduction/clientlibs.md">allowProxy</a></code> property<br /> </li>
     <li>Los recursos deben sincronizarse entre AEM y Adobe I/O Runtime<br /> </li>
     <li>Para habilitar la creación de la SPA, puede ser necesario un servidor proxy para Adobe I/O Runtime</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Planificación de SSR {#planning-for-ssr}

Por lo general, solo una parte de una aplicación debe representarse en el servidor. El ejemplo común es el contenido que se muestra encima del pliegue en la carga inicial de la página que se representa en el servidor. Esto ahorra tiempo al enviar al cliente contenido ya procesado. A medida que el usuario interactúa con el SPA, el cliente procesa el contenido adicional.

Al considerar la implementación del procesamiento del lado del servidor para su SPA, debe comprobar qué partes de la aplicación serán necesarias.

## Desarrollo de una SPA mediante SSR {#developing-an-spa-using-ssr}

SPA componentes podrían ser procesados por el cliente (en el navegador) o por el servidor. Cuando se procesa en el servidor, las propiedades del explorador, como el tamaño de la ventana y la ubicación, no están presentes. Por lo tanto, SPA componentes deben ser isomórficos, sin suponer dónde se procesarán.

Para aprovechar SSR, deberá implementar su código en AEM así como en Adobe I/O Runtime, que es responsable de la renderización del lado del servidor. La mayoría del código será el mismo, pero las tareas específicas del servidor diferirán.

## SSR para SPA en AEM {#ssr-for-spas-in-aem}

El SSR para SPA en AEM requiere Adobe I/O Runtime, que se llama para la renderización del servidor de contenido de la aplicación. Dentro de HTL de la aplicación, se llama a un recurso en Adobe I/O Runtime para procesar el contenido.

Del mismo modo que AEM admite los marcos de SPA Angular y React de forma predeterminada, el procesamiento en el servidor también se admite para aplicaciones de Angular y React. Para más detalles, consulte la documentación de NPM para ambos marcos.

## Procesador de contenido remoto {#remote-content-renderer}

La variable [Configuración del procesador de contenido remoto](#remote-content-renderer-configuration) que es necesario para utilizar SSR con su SPA en AEM toque en un servicio de renderización más generalizado que se puede ampliar y personalizar para satisfacer sus necesidades.

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService` es un servicio OSGi para recuperar contenido procesado en un servidor remoto, como desde el Adobe I/O. El contenido enviado al servidor remoto se basa en el parámetro de solicitud pasado.

`RemoteContentRenderingService` se puede insertar mediante la inversión de dependencias en un modelo Sling personalizado o servlet cuando se requiere una manipulación de contenido adicional.

Este servicio lo utiliza internamente el [RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet).

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

La variable `RemoteContentRendererRequestHandlerServlet` se puede utilizar para configurar la solicitud mediante programación. `DefaultRemoteContentRendererRequestHandlerImpl`, la implementación predeterminada del controlador de solicitud proporcionada, le permite crear varias configuraciones OSGi para asignar una ubicación en la estructura de contenido a un punto final remoto.

Para agregar un controlador de solicitud personalizado, implemente el `RemoteContentRendererRequestHandler` interfaz. Asegúrese de establecer la variable `Constants.SERVICE_RANKING` propiedad component a un entero mayor que 100, que es la clasificación del `DefaultRemoteContentRendererRequestHandlerImpl`.

```javascript
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### Configuración de la configuración OSGi del controlador predeterminado {#configure-default-handler}

La configuración del controlador predeterminado debe configurarse como se describe en la sección [Configuración del procesador de contenido remoto](#remote-content-renderer-configuration).

### Uso del procesador de contenido remoto {#usage}

Para que un servlet recupere y devuelva contenido que se puede insertar en la página:

1. Asegúrese de que el servidor remoto es accesible.
1. Agregue uno de los siguientes fragmentos a la plantilla HTL de un componente AEM.
1. De forma opcional, cree o modifique las configuraciones de OSGi.
1. Explorar el contenido del sitio

Normalmente, la plantilla HTL de un componente de página es el destinatario principal de dicha función.

```html
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### Requisitos {#requirements}

Los servlets aprovechan el Exportador del modelo de Sling para serializar los datos del componente. De forma predeterminada, ambas variables `com.adobe.cq.export.json.ContainerExporter` y `com.adobe.cq.export.json.ComponentExporter` son compatibles con los adaptadores del modelo Sling. Si es necesario, puede añadir clases en las que se debe adaptar la solicitud para utilizar la variable `RemoteContentRendererServlet` y la implementación de `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`. Las clases adicionales deben ampliar el `ComponentExporter`.
