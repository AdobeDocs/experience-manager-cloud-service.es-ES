---
title: SPA Procesamiento del lado del servidor y de
description: SPA El uso del procesamiento del lado del servidor (SSR) en la puede acelerar la carga inicial de la página y, a continuación, pasar más procesamiento al cliente.
exl-id: be409559-c7ce-4bc2-87cf-77132d7c2da1
source-git-commit: a9eb03d4db478a4db8e6d2436bd06dcde70a3eeb
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 0%

---

# SPA Procesamiento del lado del servidor y de{#spa-and-server-side-rendering}

SPA Las aplicaciones de una sola página () pueden ofrecer al usuario una experiencia enriquecida y dinámica que reacciona y se comporta de formas familiares, a menudo igual que una aplicación nativa. [Esto se logra confiando en que el cliente cargue el contenido por adelantado y luego haga el trabajo pesado de manejar la interacción del usuario](introduction.md#how-does-a-spa-work) y, por lo tanto, minimiza la cantidad de comunicación necesaria entre el cliente y el servidor, lo que hace que la aplicación sea más reactiva.

SPA Sin embargo, esto puede conllevar tiempos de carga inicial más largos, especialmente si el contenido del es grande y rico. Para optimizar los tiempos de carga, parte del contenido se puede procesar en el servidor. El uso del procesamiento del lado del servidor (SSR) puede acelerar la carga inicial de la página y, a continuación, pasar más procesamiento al cliente.

## Cuándo usar SSR {#when-to-use-ssr}

No se requiere SSR en todos los proyectos. AEM SPA Aunque admite totalmente la SR de JS para la, Adobe no recomienda implementarla sistemáticamente en todos los proyectos.

Al decidir implementar SSR primero debe estimar qué complejidad adicional, esfuerzo y costo adicional representa SSR de manera realista para el proyecto, incluido el mantenimiento a largo plazo. Sólo debe elegirse una arquitectura SSR cuando el valor añadido supere claramente los costes estimados.

SSR generalmente proporciona algún valor cuando hay un claro &quot;sí&quot; a cualquiera de las siguientes preguntas:

* **SEO:** ¿Se sigue necesitando SSR para que los motores de búsqueda que generan tráfico indexen correctamente su sitio? Tenga en cuenta que los rastreadores del motor de búsqueda principal ahora evalúan JS.
* **Velocidad de página:** ¿Proporciona la SSR una mejora de velocidad mensurable en entornos de la vida real y aumenta la experiencia general del usuario?

Solo cuando al menos una de estas dos preguntas se responda con un claro &quot;sí&quot; para su proyecto, el Adobe recomienda implementar SSR. En las secciones siguientes se describe cómo hacerlo utilizando Adobe I/O Runtime, parte de [Generador de aplicaciones](https://developer.adobe.com/app-builder).

## Adobe I/O Runtime {#adobe-i-o-runtime}

Si usted [está seguro de que su proyecto requiere la implementación de la SSR](#when-to-use-ssr), la solución recomendada por Adobe es utilizar Adobe I/O Runtime.

Para obtener más información sobre Adobe I/O Runtime, consulte

* [https://developer.adobe.com/runtime](https://developer.adobe.com/runtime) : para obtener una descripción general de la función Tiempo de ejecución de App Builder
* [https://developer.adobe.com/app-builder](https://developer.adobe.com/app-builder) : para obtener más información sobre el producto App Builder completo
* [https://developer.adobe.com/runtime/docs/](https://developer.adobe.com/runtime/docs) - para obtener documentación detallada

Las siguientes secciones detallan cómo se puede utilizar Adobe I/O Runtime SPA para implementar SSR para su en dos modelos diferentes:

* [AEM Flujo de comunicación impulsado por el](#aem-driven-communication-flow)
* [Flujo de comunicación impulsado por Adobe I/O Runtime](#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>Adobe recomienda un espacio de trabajo de Adobe I/O Runtime independiente por entorno (ensayo, producción, prueba, etc.). Esto permite patrones típicos del ciclo de vida de desarrollo de sistemas (SDLC) con diferentes versiones de una sola aplicación implementada en diferentes entornos.  Ver el documento [CI/CD para aplicaciones de App Builder](https://developer.adobe.com/app-builder/docs/guides/deployment/ci_cd_for_firefly_apps/) para obtener más información.
>
>No se necesita un espacio de trabajo independiente por instancia (autor, publicación) a menos que haya diferencias en la implementación de tiempo de ejecución por tipo de instancia.

## Configuración del procesador remoto {#remote-content-renderer-configuration}

AEM Debe saber dónde se puede recuperar el contenido procesado de forma remota. Independientemente de [qué modelo decide implementar para SSR,](#adobe-i-o-runtime) AEM deberá especificar cómo acceder a este servicio de procesamiento remoto para obtener acceso a los datos de la aplicación.

Esto se realiza mediante la variable **RemoteContentRenderer: servicio OSGi de fábrica de configuración**. Busque la cadena &quot;RemoteContentRenderer&quot; en la consola de configuración de la consola web en `http://<host>:<port>/system/console/configMgr`.

![Configuración del procesador](assets/renderer-configuration.png)

Los campos siguientes están disponibles para la configuración:

* **Patrón de ruta de contenido** - Expresión regular para que coincida con una parte del contenido, si es necesario
* **URL de extremo remoto** : URL del punto de conexión responsable de la generación del contenido
   * Utilice el protocolo HTTPS protegido si no está en la red local.
* **Encabezados de solicitud adicionales** - Encabezados adicionales que se añadirán a la solicitud enviada al extremo remoto
   * Patrón: `key=value`
* **Tiempo de espera de solicitud** - Tiempo de espera de solicitud de host remoto en milisegundos

>[!NOTE]
>
>Independientemente de si decide implementar el [AEM Flujo de comunicación impulsado por el](#aem-driven-communication-flow) o el [Flujo impulsado por Adobe I/O Runtime,](#adobe-i-o-runtime-driven-communication-flow) debe definir una configuración de procesador de contenido remoto.

>[!NOTE]
>
>Esta configuración aprovecha las [Procesador de contenido remoto,](#remote-content-renderer) que tiene opciones de extensión y personalización adicionales disponibles.

## AEM Flujo de comunicación impulsado por el {#aem-driven-communication-flow}

Cuando se utiliza SSR, la variable [flujo de trabajo de interacción](introduction.md#interaction-with-the-spa-editor) SPA AEM de la en la que se incluye una fase en la que el contenido inicial de la aplicación se genera en Adobe I/O Runtime.

1. AEM El explorador solicita el contenido SSR a los usuarios de la interfaz de usuario de.
1. AEM Publica el modelo en Adobe I/O Runtime.
1. Adobe I/O Runtime devuelve el contenido generado.
1. AEM sirve al HTML devuelto por Adobe I/O Runtime a través de la plantilla HTL del componente de página back-end.

![AEM SSE Adobe I/O de trabajo impulsado por CMS](assets/ssr-cms-drivenaemnode-adobeio.png)

## Flujo de comunicación impulsado por Adobe I/O Runtime {#adobe-i-o-runtime-driven-communication-flow}

SPA AEM AEM En la sección anterior se describe la implementación estándar y recomendada del procesamiento en el servidor con respecto a la en la que el usuario realiza el arranque y la entrega de contenido en el lado del servidor, en el que el usuario realiza el procesamiento de manera predeterminada y de manera predeterminada, en el lado del servidor, en lo que respecta a la en la que se realiza el procesamiento y la entrega de contenido.

Como alternativa, SSR se puede implementar de modo que Adobe I/O Runtime sea responsable del arranque, lo que invierte de forma eficaz el flujo de comunicación.

AEM Ambos modelos son válidos y compatibles con el servicio de asistencia de la aplicación de la. Sin embargo, se deben considerar las ventajas y desventajas de cada uno antes de implementar un modelo en particular.

<table>
 <tbody>
  <tr>
   <th><strong>Bootstrapping</strong></th>
   <th><strong>Ventajas</strong></th>
   <th><strong>Desventajas</strong></th>
  </tr>
  <tr>
   <th><strong>AEM vía de la</strong><br /> </th>
   <td>
    <ul>
     <li>AEM administra la inyección de bibliotecas donde sea necesario</li>
     <li>AEM Solo es necesario mantener los recursos en el área de la<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>SPA Posiblemente desconocido para el desarrollador de<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <th><strong>mediante Adobe I/O Runtime<br /> </strong></th>
   <td>
    <ul>
     <li>SPA Más familiar para los desarrolladores de<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>AEM Los recursos de Clientlib requeridos por la aplicación, como CSS y JavaScript, los deberá poner a disposición el desarrollador de la aplicación a través de la interfaz de usuario de la biblioteca de cliente de la aplicación de desarrollador de. <code><a href="/help/implementing/developing/introduction/clientlibs.md">allowProxy</a></code> propiedad<br /> </li>
     <li>AEM Los recursos deben sincronizarse entre la aplicación y la aplicación de Adobe I/O Runtime<br /> </li>
     <li>SPA Para habilitar la creación de la, puede ser necesario un servidor proxy para Adobe I/O Runtime</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Planificación de la SSR {#planning-for-ssr}

Por lo general, solo parte de una aplicación debe procesarse en el servidor. El ejemplo común es el contenido que se muestra encima del pliegue en la carga inicial de la página y que se procesa en el servidor. Esto ahorra tiempo al enviar al cliente contenido ya procesado. SPA A medida que el usuario interactúa con el usuario, el cliente procesa el contenido adicional.

SPA A medida que considere la posibilidad de implementar el procesamiento en el servidor para su, deberá revisar qué partes de la aplicación serán necesarias.

## SPA Desarrollo de una mediante SSR {#developing-an-spa-using-ssr}

SPA El cliente (en el explorador) o el servidor pueden procesar los componentes de la. Cuando se representan en el servidor, las propiedades del explorador como el tamaño y la ubicación de la ventana no están presentes. SPA Por lo tanto, los componentes de la deben ser isomórficos, sin dar por hecho dónde se procesarán.

AEM Para aprovechar la SSR, deberá implementar su código tanto en el servidor como en el Adobe I/O Runtime, que es responsable del procesamiento del lado del servidor. La mayoría del código será el mismo, aunque las tareas específicas del servidor diferirán.

## SPA AEM SSR para la en el {#ssr-for-spas-in-aem}

SPA AEM SSR para la en la práctica requiere Adobe I/O Runtime, que es necesario para el procesamiento del lado del servidor de contenido de la aplicación. Dentro del HTL de la aplicación, se llama a un recurso en Adobe I/O Runtime para procesar el contenido.

AEM Del mismo modo que admite los módulos Angular SPA y React de forma predeterminada, el procesamiento en el servidor también es compatible con las aplicaciones de Angular y React. Consulte la documentación de NPM para ambos marcos para obtener más información.

## Procesador de contenido remoto {#remote-content-renderer}

El [Configuración del procesador de contenido remoto](#remote-content-renderer-configuration) SPA AEM que es necesario para utilizar SSR con sus en la práctica, utiliza un servicio de renderización más generalizado que se puede ampliar y personalizar para satisfacer sus necesidades.

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService` es un servicio OSGi para recuperar contenido procesado en un servidor remoto, como desde el Adobe I/O. El contenido enviado al servidor remoto se basa en el parámetro de solicitud pasado.

`RemoteContentRenderingService` se puede insertar mediante la inversión de dependencia en un modelo Sling personalizado o servlet cuando se requiere una manipulación de contenido adicional.

Este servicio lo utiliza internamente el [RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet).

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

El `RemoteContentRendererRequestHandlerServlet` se puede utilizar para establecer mediante programación la configuración de la solicitud. `DefaultRemoteContentRendererRequestHandlerImpl`, la implementación del controlador de solicitudes predeterminada proporcionada, le permite crear varias configuraciones de OSGi para asignar una ubicación en la estructura de contenido a un extremo remoto.

Para agregar un controlador de solicitud personalizado, implemente la variable `RemoteContentRendererRequestHandler` interfaz. Asegúrese de configurar el `Constants.SERVICE_RANKING` propiedad de componente a un entero superior a 100, que es la clasificación del `DefaultRemoteContentRendererRequestHandlerImpl`.

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

Para que un servlet recupere y devuelva contenido que se pueda insertar en la página:

1. Asegúrese de que el servidor remoto sea accesible.
1. AEM Agregue uno de los siguientes fragmentos de código a la plantilla HTL de un componente de la.
1. Opcionalmente, puede crear o modificar las configuraciones de OSGi.
1. Explorar el contenido del sitio

Normalmente, la plantilla HTL de un componente de página es el destinatario principal de una función de este tipo.

```html
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### Requisitos  {#requirements}

Los servlets aprovechan el exportador de modelos Sling para serializar los datos del componente. De forma predeterminada, tanto la variable `com.adobe.cq.export.json.ContainerExporter` y `com.adobe.cq.export.json.ComponentExporter` se admiten como adaptadores del modelo Sling. Si es necesario, puede agregar clases a las que se debe adaptar la solicitud utilizando `RemoteContentRendererServlet` y la implementación de `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`. Las clases adicionales deben ampliar el `ComponentExporter`.
