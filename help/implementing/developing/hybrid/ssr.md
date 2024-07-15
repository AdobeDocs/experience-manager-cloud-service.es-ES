---
title: SPA Procesamiento del lado del servidor y de
description: SPA El uso del procesamiento del lado del servidor (SSR) en el servidor puede acelerar la carga inicial de la página y, a continuación, pasar más procesamiento al cliente.
exl-id: be409559-c7ce-4bc2-87cf-77132d7c2da1
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1492'
ht-degree: 0%

---

# SPA Procesamiento del lado del servidor y de{#spa-and-server-side-rendering}

SPA Las aplicaciones de una sola página () pueden ofrecer al usuario una experiencia enriquecida y dinámica que reacciona y se comporta de formas familiares, a menudo igual que una aplicación nativa. [Esta funcionalidad se logra al depender del cliente para cargar el contenido por adelantado y luego hacer el trabajo pesado de administrar la interacción del usuario](introduction.md#how-does-a-spa-work). Este proceso minimiza la cantidad de comunicación necesaria entre el cliente y el servidor, lo que hace que la aplicación sea más reactiva.

SPA Sin embargo, este proceso puede conllevar tiempos de carga inicial más largos, especialmente si el contenido de la es grande y rico. Para optimizar los tiempos de carga, parte del contenido se puede procesar en el servidor. El uso del procesamiento del lado del servidor (SSR) puede acelerar la carga inicial de la página y, a continuación, pasar más procesamiento al cliente.

## Cuándo usar SSR {#when-to-use-ssr}

No se requiere SSR en todos los proyectos. AEM SPA Aunque admite totalmente la SR de JS para la, Adobe no recomienda implementarla sistemáticamente en todos los proyectos.

Al decidir implementar SSR, primero debe estimar qué complejidad, esfuerzo y costo adicionales representan SSR de manera realista para el proyecto, incluido el mantenimiento a largo plazo. Sólo debe elegirse una arquitectura SSR cuando el valor añadido supere claramente los costes estimados.

SSR generalmente proporciona algún valor cuando hay un claro &quot;sí&quot; a cualquiera de las siguientes preguntas:

* **SEO:** ¿Se requiere SSR para que el sitio sea indexado correctamente por los motores de búsqueda que generan tráfico? Tenga en cuenta que los rastreadores del motor de búsqueda principal ahora evalúan JS.
* **Velocidad de la página:** ¿El SSR proporciona una mejora de velocidad medible en entornos reales y agrega a la experiencia general del usuario?

Solo cuando al menos una de estas dos preguntas se responda con un claro &quot;sí&quot; para su proyecto, el Adobe recomienda implementar SSR. En las secciones siguientes se describe cómo hacerlo usando Adobe I/O Runtime, parte de [App Builder](https://developer.adobe.com/app-builder).

## Adobe I/O Runtime {#adobe-i-o-runtime}

Si está seguro de que su proyecto requiere la implementación de SSR](#when-to-use-ssr), la solución recomendada por Adobe es usar Adobe I/O Runtime.[

Para obtener más información sobre Adobe I/O Runtime, consulte lo siguiente:

* [https://developer.adobe.com/runtime](https://developer.adobe.com/runtime): para obtener una descripción general de la característica Runtime de App Builder
* [https://developer.adobe.com/app-builder](https://developer.adobe.com/app-builder) - para obtener detalles sobre el producto App Builder completo
* [https://developer.adobe.com/runtime/docs/](https://developer.adobe.com/runtime/docs): para obtener documentación detallada

Las siguientes secciones detallan cómo se puede utilizar Adobe I/O Runtime SPA para implementar SSR para su en dos modelos diferentes:

* [AEM Flujo de comunicación impulsado por el](#aem-driven-communication-flow)
* [Flujo de comunicación impulsado por Adobe I/O Runtime](#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>Adobe recomienda un espacio de trabajo de Adobe I/O Runtime independiente por entorno (ensayo, producción, prueba, etc.). Esto permite crear patrones típicos del ciclo de vida de desarrollo de sistemas (SDLC) con diferentes versiones de una sola aplicación implementada en diferentes entornos. Consulte [CI/CD para aplicaciones de App Builder](https://developer.adobe.com/app-builder/docs/guides/deployment/ci_cd_for_firefly_apps/) para obtener más información.
>
>No se necesita un espacio de trabajo independiente por instancia (autor, publicación) a menos que haya diferencias en la implementación de tiempo de ejecución por tipo de instancia.

>[!NOTE]
>
>Cloud Manager no admite la implementación en Adobe I/O Runtime. Como resultado, debe configurar su propia infraestructura para implementar el código SSR en Adobe I/O Runtime.

## Configuración del procesador remoto {#remote-content-renderer-configuration}

AEM Debe saber dónde se puede recuperar el contenido procesado de forma remota. AEM Independientemente de [qué modelo elija implementar para SSR,](#adobe-i-o-runtime) debe especificar a los usuarios cómo acceder a este servicio de representación remota de datos (RDS) para obtener acceso a este servicio de representación remota.

Este servicio se realiza mediante el **RemoteContentRenderer - Servicio OSGi de fábrica de configuración**. Busque la cadena &quot;RemoteContentRenderer&quot; en la consola de configuración de la consola web en `http://<host>:<port>/system/console/configMgr`.

![Configuración del procesador](assets/renderer-configuration.png)

Los campos siguientes están disponibles para la configuración:

* **Patrón de ruta de contenido**: expresión regular para que coincida con una parte del contenido, si es necesario
* **URL de extremo remoto**: URL del extremo responsable de generar el contenido
   * Utilice el protocolo HTTPS protegido si no está en la red local.
* **Encabezados de solicitud adicionales**: se agregarán encabezados adicionales a la solicitud enviada al extremo remoto
   * Patrón: `key=value`
* **Tiempo de espera de solicitud** - Tiempo de espera de solicitud de host remoto en milisegundos

>[!NOTE]
>
>AEM Independientemente de si elige implementar el flujo de comunicación [impulsado por el](#aem-driven-communication-flow) o el [flujo impulsado por Adobe I/O Runtime](#adobe-i-o-runtime-driven-communication-flow), debe definir una configuración de procesador de contenido remoto.

>[!NOTE]
>
>Esta configuración usa el [Procesador de contenido remoto,](#remote-content-renderer), que tiene opciones adicionales de extensión y personalización disponibles.

## AEM Flujo de comunicación impulsado por el {#aem-driven-communication-flow}

SPA AEM Al utilizar SSR, el [flujo de trabajo de interacción de componentes](introduction.md#interaction-with-the-spa-editor) de la en incluye una fase en la que el contenido inicial de la aplicación se genera en Adobe I/O Runtime.

1. AEM El explorador solicita el contenido SSR a los usuarios de la interfaz de usuario de.
1. AEM Publica el modelo en Adobe I/O Runtime.
1. Adobe I/O Runtime devuelve el contenido generado.
1. AEM sirve al HTML devuelto por Adobe I/O Runtime a través de la plantilla HTL del componente de página back-end.

AEM ![Adobe I/O de trabajo impulsado por CMS de SSE](assets/ssr-cms-drivenaemnode-adobeio.png)

## Flujo de comunicación impulsado por Adobe I/O Runtime {#adobe-i-o-runtime-driven-communication-flow}

SPA AEM AEM En la sección anterior se describe la implementación estándar y recomendada del procesamiento del lado del servidor con respecto a la en la que el usuario realiza el arranque y la entrega de contenido de manera independiente, y se realiza una prueba de ello con el fin de obtener un resultado más eficaz en el.

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
   <th>AEM <strong>vía</strong><br /> </th>
   <td>
    <ul>
     <li>AEM administra la inyección de bibliotecas donde sea necesario</li>
     <li>AEM Mantener recursos solo en el <br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>SPA Posiblemente desconocido para el desarrollador de la<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <th><strong>mediante Adobe I/O Runtime<br /> </strong></th>
   <td>
    <ul>
     <li>SPA Más familiar para los desarrolladores de la<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>El desarrollador debe poner a disposición los recursos de Clientlib requeridos por la aplicación, como CSS y JavaScript AEM, mediante la propiedad <code><a href="/help/implementing/developing/introduction/clientlibs.md">allowProxy</a></code> <br /> </li>
     <li>AEM Los recursos deben sincronizarse entre los recursos de y el de Adobe I/O Runtime <br /> </li>
     <li>SPA Para habilitar la creación de la, puede ser necesario un servidor proxy para Adobe I/O Runtime</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Planificación de la SSR {#planning-for-ssr}

Por lo general, solo parte de una aplicación se debe procesar en el servidor. El ejemplo más común es el contenido que se muestra encima del pliegue en la carga inicial de la página y que se procesa en el servidor. Este proceso ahorra tiempo al enviar al cliente contenido ya procesado. SPA A medida que el usuario interactúa con el usuario, el cliente procesa el contenido adicional.

SPA A medida que considere la posibilidad de implementar el procesamiento en el lado del servidor para su, revise qué partes de la aplicación son necesarias.

## SPA Desarrollo de una mediante SSR {#developing-an-spa-using-ssr}

SPA El cliente (en el explorador) o el servidor pueden procesar los componentes de la. Cuando se representan en el servidor, las propiedades del explorador como el tamaño y la ubicación de la ventana no están presentes. SPA Por lo tanto, los componentes de la deben ser isomórficos, sin dar por hecho dónde se representan.

AEM Para utilizar SSR, debe implementar el código en y en Adobe I/O Runtime, que es responsable de la representación en el servidor de, y en la interfaz de usuario de y en la interfaz de usuario de. La mayoría del código es el mismo, aunque las tareas específicas del servidor difieren.

## SPA AEM SSR para la en el {#ssr-for-spas-in-aem}

SPA AEM SSR para la en la requiere Adobe I/O Runtime, que es necesario para el procesamiento del lado del servidor de contenido de la aplicación. Dentro del HTL de la aplicación, se llama a un recurso en Adobe I/O Runtime para procesar el contenido.

AEM Del mismo modo que admite los módulos Angular SPA y React de forma predeterminada, el procesamiento del lado del servidor también es compatible con las aplicaciones de Angular y React. Consulte la documentación de NPM para ambos marcos para obtener más información.

## Procesador de contenido remoto {#remote-content-renderer}

SPA AEM La [configuración del procesador de contenido remoto](#remote-content-renderer-configuration) necesaria para usar SSR con sus en el modo de trabajo, se utiliza en un servicio de procesamiento más generalizado que se puede ampliar y personalizar para satisfacer sus necesidades.

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService` Un servicio OSGi para recuperar contenido procesado en un servidor remoto, como del Adobe I/O. El contenido enviado al servidor remoto se basa en el parámetro de solicitud pasado.

`RemoteContentRenderingService` se puede insertar mediante la inversión de dependencia en un modelo Sling personalizado o servlet cuando se requiere manipulación de contenido adicional.

Este servicio lo usa internamente [RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet).

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

`RemoteContentRendererRequestHandlerServlet` se usa para establecer la configuración de la solicitud mediante programación. `DefaultRemoteContentRendererRequestHandlerImpl`, la implementación del controlador de solicitudes predeterminada proporcionada, le permite crear varias configuraciones de OSGi para poder asignar una ubicación en la estructura de contenido a un extremo remoto.

Para agregar un controlador de solicitud personalizado, implemente la interfaz `RemoteContentRendererRequestHandler`. Asegúrese de establecer la propiedad del componente `Constants.SERVICE_RANKING` en un número entero superior a 100, que es la clasificación de `DefaultRemoteContentRendererRequestHandlerImpl`.

```javascript
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### Configurar la configuración OSGi del controlador predeterminado {#configure-default-handler}

La configuración del controlador predeterminado debe configurarse tal como se describe en la sección [Configuración del procesador de contenido remoto](#remote-content-renderer-configuration).

### Uso del procesador de contenido remoto {#usage}

Haga que un servlet recupere y devuelva contenido que se haya insertado en la página:

1. Asegúrese de que el servidor remoto sea accesible.
1. AEM Agregue uno de los siguientes fragmentos de código a la plantilla HTL de un componente de la.
1. Opcionalmente, puede crear o modificar las configuraciones de OSGi.
1. Explorar el contenido del sitio

Normalmente, la plantilla HTL de un componente de página es el destinatario principal de una función de este tipo.

```html
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### Requisitos  {#requirements}

Los servlets utilizan el Exportador del modelo Sling para serializar los datos del componente. De manera predeterminada, `com.adobe.cq.export.json.ContainerExporter` y `com.adobe.cq.export.json.ComponentExporter` se admiten como adaptadores del modelo Sling. Si es necesario, puede agregar clases a las que se debe adaptar la solicitud mediante el `RemoteContentRendererServlet` y la implementación de `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`. Las clases adicionales deben extender `ComponentExporter`.
