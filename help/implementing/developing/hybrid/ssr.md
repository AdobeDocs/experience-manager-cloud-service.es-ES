---
title: SPA y procesamiento en el servidor
description: El uso del procesamiento del lado del servidor (SSR) en la SPA puede acelerar la carga inicial de la página y, a continuación, pasar el procesamiento adicional al cliente.
translation-type: tm+mt
source-git-commit: fc61f13fbf976c43fcdd6921178a9bd4e82fc68d
workflow-type: tm+mt
source-wordcount: '1435'
ht-degree: 0%

---


# SPA y renderización del lado del servidor{#spa-and-server-side-rendering}

Las aplicaciones de una sola página (SPA) pueden ofrecer al usuario una experiencia dinámica y rica que reacciona y se comporta de formas familiares, a menudo como una aplicación nativa. [Esto se consigue confiando en que el cliente cargue el contenido por adelantado y luego realice el trabajo pesado de gestionar la ](introduction.md#how-does-a-spa-work) interacción del usuario, minimizando así la cantidad de comunicación necesaria entre el cliente y el servidor, lo que hace que la aplicación sea más reactiva.

Sin embargo, esto puede provocar tiempos de carga iniciales más largos, especialmente si la SPA es grande y tiene contenido enriquecido. Para optimizar los tiempos de carga, parte del contenido se puede representar en el lado del servidor. El uso de la renderización del lado del servidor (SSR) puede acelerar la carga inicial de la página y luego pasar una renderización adicional al cliente.

## Cuándo se utiliza SSR {#when-to-use-ssr}

La SSR no es necesaria en todos los proyectos. Aunque AEM admite totalmente JS SSR para SPA, Adobe no recomienda implementarlo sistemáticamente para cada proyecto.

Al decidir implementar SSR, primero debe estimar qué complejidad adicional, esfuerzo y costo de agregar SSR representa de manera realista para el proyecto, incluido el mantenimiento a largo plazo. Una arquitectura SSR solo debe elegirse cuando el valor añadido exceda claramente los costes estimados.

SSR normalmente proporciona algún valor cuando hay un claro &quot;sí&quot; a cualquiera de las siguientes preguntas:

* **SEO:**  ¿Es necesario realizar una SSR para que el sitio esté correctamente indexado por los motores de búsqueda que traen tráfico? Tenga en cuenta que los principales rastreadores de motores de búsqueda ahora evalúan JS.
* **Velocidad de página:** ¿La SSR proporciona una mejora de velocidad medible en entornos reales y contribuye a la experiencia del usuario en general?

Solo cuando al menos una de estas dos preguntas se responda con un claro &quot;sí&quot; para el proyecto, Adobe recomienda implementar SSR. Las siguientes secciones describen cómo hacerlo con Adobe I/O Runtime.

## Tiempo de ejecución de Adobe I/O {#adobe-i-o-runtime}

Si [está seguro de que su proyecto requiere la implementación de SSR](#when-to-use-ssr), la solución recomendada de Adobe es utilizar Adobe I/O Runtime.

Para obtener más información sobre Adobe I/O Runtime, consulte

* [https://www.adobe.io/apis/experienceplatform/runtime.html](https://www.adobe.io/apis/experienceplatform/runtime.html) : para obtener una descripción general del servicio
* [https://www.adobe.io/apis/experienceplatform/runtime/docs.html](https://www.adobe.io/apis/experienceplatform/runtime/docs.html) : para obtener documentación detallada sobre la plataforma

Las siguientes secciones detallan cómo se puede utilizar Adobe I/O Runtime para implementar SSR para su SPA en dos modelos diferentes:

* [Flujo de comunicación impulsado por AEM](#aem-driven-communication-flow)
* [Flujo de comunicación impulsado por el tiempo de ejecución de Adobe I/O](#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>Adobe recomienda una instancia de Adobe I/O Runtime independiente para cada entorno de AEM (autor, publicación, fase, etc.).

## Configuración del procesador remoto {#remote-content-renderer-configuration}

AEM debe saber dónde se puede recuperar el contenido procesado de forma remota. Independientemente del [modelo que elija implementar para SSR,](#adobe-i-o-runtime) deberá especificar a AEM cómo acceder a este servicio de procesamiento remoto.

Esto se realiza a través del **RemoteContentRenderer - Configuration Factory OSGi service**. Busque la cadena &quot;RemoteContentRenderer&quot; en la consola de configuración de la consola web en `http://<host>:<port>/system/console/configMgr`.

![Configuración del procesador](assets/renderer-configuration.png)

Los campos siguientes están disponibles para la configuración:

* **Patrón de ruta de contenido** : expresión regular para que coincida con una parte del contenido, si es necesario
* **Dirección URL de extremo remoto** : dirección URL del extremo responsable de generar el contenido
   * Utilice el protocolo HTTPS protegido si no está en la red local.
* **Encabezados de solicitud adicionales** : encabezados adicionales que se agregarán a la solicitud enviada al extremo remoto.
   * Patrón: `key=value`
* **Tiempo de espera de solicitud** : tiempo de espera de solicitud de host remoto en milisegundos

>[!NOTE]
>
>Independientemente de si decide implementar el [flujo de comunicación dirigido por AEM](#aem-driven-communication-flow) o el [flujo impulsado por Adobe I/O Runtime,](#adobe-i-o-runtime-driven-communication-flow) debe definir una configuración del procesador de contenido remoto.

>[!NOTE]
>
>Esta configuración aprovecha el [Procesador de contenido remoto,](#remote-content-renderer) que tiene opciones de personalización y extensión adicionales disponibles.

## Flujo de comunicación impulsado por AEM {#aem-driven-communication-flow}

Al utilizar SSR, el [flujo de trabajo de interacción de componentes](introduction.md#interaction-with-the-spa-editor) de las SPA en AEM incluye una fase en la que el contenido inicial de la aplicación se genera en Adobe I/O Runtime.

1. El navegador solicita el contenido SSR de AEM.
1. AEM publica el modelo en Adobe I/O Runtime.
1. Adobe I/O Runtime devuelve el contenido generado.
1. AEM proporciona el HTML devuelto por Adobe I/O Runtime a través de la plantilla HTL del componente de página back-end.

![AEM Adobe I/O impulsado por SSE CMS](assets/ssr-cms-drivenaemnode-adobeio.png)

## Flujo de comunicación impulsado por el tiempo de ejecución de Adobe I/O {#adobe-i-o-runtime-driven-communication-flow}

En la sección anterior se describe la implementación estándar y recomendada del procesamiento en el servidor con respecto a las SPA en AEM, donde AEM realiza el bootstrapping y la entrega de contenido.

Alternativamente, SSR se puede implementar para que Adobe I/O Runtime sea responsable del arranque, revirtiendo efectivamente el flujo de comunicación.

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
     <li>Los recursos solo deben mantenerse en AEM<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Posiblemente no sea familiar para el desarrollador de SPA<br /> </li>
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
     <li>Los recursos de Clientlib requeridos por la aplicación, como CSS y JavaScript, deberán estar disponibles para el desarrollador de AEM a través de la propiedad <code><a href="/help/implementing/developing/introduction/clientlibs.md">allowProxy</a></code><br /> </li>
     <li>Los recursos deben sincronizarse entre AEM y Adobe I/O Runtime<br /> </li>
     <li>Para habilitar la creación de SPA, puede ser necesario un servidor proxy para Adobe I/O Runtime</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Planificación de SSR {#planning-for-ssr}

Por lo general, solo una parte de una aplicación debe representarse en el servidor. El ejemplo común es el contenido que se muestra encima del pliegue en la carga inicial de la página que se representa en el servidor. Esto ahorra tiempo al enviar al cliente contenido ya procesado. A medida que el usuario interactúa con la SPA, el cliente procesa el contenido adicional.

Como tiene en cuenta la implementación del procesamiento del lado del servidor para su SPA, debe comprobar qué partes de la aplicación serán necesarias.

## Desarrollo de una SPA mediante SSR {#developing-an-spa-using-ssr}

Los componentes de SPA podrían ser procesados por el cliente (en el navegador) o por el servidor. Cuando se procesa en el servidor, las propiedades del explorador, como el tamaño de la ventana y la ubicación, no están presentes. Por lo tanto, los componentes de la SPA deben ser isomórficos, lo que no supone dónde se procesarán.

Para aprovechar SSR, deberá implementar su código en AEM, así como en Adobe I/O Runtime, que es responsable del procesamiento en el servidor. La mayoría del código será el mismo, pero las tareas específicas del servidor diferirán.

## SSR para SPA en AEM {#ssr-for-spas-in-aem}

SSR para SPA en AEM requiere Adobe I/O Runtime, que se llama para la representación del servidor de contenido de la aplicación. Dentro de HTL de la aplicación, se llama a un recurso en Adobe I/O Runtime para procesar el contenido.

Al igual que AEM admite los marcos de SPA Angular y React de forma predeterminada, el procesamiento en el servidor también es compatible con las aplicaciones Angular y React. Para más detalles, consulte la documentación de NPM para ambos marcos.

## Procesador de contenido remoto {#remote-content-renderer}

La [Configuración del procesador de contenido remoto](#remote-content-renderer-configuration) necesaria para utilizar SSR con el SPA en AEM se conecta a un servicio de renderización más generalizado que se puede ampliar y personalizar para satisfacer sus necesidades.

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService` es un servicio OSGi para recuperar contenido procesado en un servidor remoto, como desde Adobe I/O. El contenido enviado al servidor remoto se basa en el parámetro de solicitud pasado.

`RemoteContentRenderingService` se puede insertar mediante la inversión de dependencias en un modelo Sling personalizado o servlet cuando se requiere una manipulación de contenido adicional.

Este servicio lo utiliza internamente [RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet).

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

El `RemoteContentRendererRequestHandlerServlet` se puede usar para establecer programáticamente la configuración de la solicitud. `DefaultRemoteContentRendererRequestHandlerImpl`, la implementación predeterminada del controlador de solicitud proporcionada, le permite crear varias configuraciones OSGi para asignar una ubicación en la estructura de contenido a un punto final remoto.

Para agregar un controlador de solicitud personalizado, implemente la interfaz `RemoteContentRendererRequestHandler` . Asegúrese de establecer la propiedad del componente `Constants.SERVICE_RANKING` en un entero mayor que 100, que es la clasificación de `DefaultRemoteContentRendererRequestHandlerImpl`.

```javascript
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### Configurar la configuración OSGi del controlador predeterminado {#configure-default-handler}

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

Los servlets aprovechan el Exportador del modelo de Sling para serializar los datos del componente. De forma predeterminada, tanto `com.adobe.cq.export.json.ContainerExporter` como `com.adobe.cq.export.json.ComponentExporter` son compatibles como adaptadores del modelo Sling. Si es necesario, puede añadir clases en las que la solicitud debe adaptarse para utilizar `RemoteContentRendererServlet` e implementar el `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`. Las clases adicionales deben ampliar el `ComponentExporter`.
