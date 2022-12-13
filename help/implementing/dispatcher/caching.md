---
title: Almacenamiento en caché en AEM as a Cloud Service
description: Almacenamiento en caché en AEM as a Cloud Service
feature: Dispatcher
exl-id: 4206abd1-d669-4f7d-8ff4-8980d12be9d6
source-git-commit: df892e49307a5c125016f3b21e4b5551020eb2b6
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Introducción {#intro}

El tráfico pasa a través de la CDN a una capa de servidor web Apache, que admite módulos, incluido Dispatcher. Para aumentar el rendimiento, Dispatcher se utiliza principalmente como caché para limitar el procesamiento en los nodos de publicación.
Se pueden aplicar reglas a la configuración de Dispatcher para modificar cualquier configuración de caducidad de caché predeterminada, lo que resulta en el almacenamiento en caché en la CDN. Tenga en cuenta que Dispatcher también respeta los encabezados de caducidad de caché resultantes si `enableTTL` está habilitado en la configuración de Dispatcher, lo que implica que actualizará contenido específico incluso fuera del contenido que se está republicando.

Esta página también describe cómo se invalida la caché de Dispatcher y cómo funciona el almacenamiento en caché a nivel de explorador con respecto a las bibliotecas del lado del cliente.

## Almacenamiento en caché {#caching}

### HTML/Texto {#html-text}

* de forma predeterminada, el explorador lo almacena en caché durante cinco minutos, en función de la variable `cache-control` encabezado emitido por la capa de Apache. La CDN también respeta este valor.
* la configuración predeterminada de almacenamiento en caché de HTML/texto se puede deshabilitar definiendo la variable `DISABLE_DEFAULT_CACHING` en `global.vars`:

```
Define DISABLE_DEFAULT_CACHING
```

Esto puede resultar útil, por ejemplo, cuando la lógica empresarial requiere un ajuste preciso del encabezado de la página (con un valor basado en el día del calendario), ya que de forma predeterminada el encabezado de la página está establecido en 0. Dicho esto, **tenga cuidado al desactivar el almacenamiento en caché predeterminado.**

* se puede anular para todo el contenido de texto o HTML definiendo la variable `EXPIRATION_TIME` en `global.vars` uso de las AEM herramientas as a Cloud Service de SDK Dispatcher.
* puede anularse en un nivel más preciso, incluido el control de la CDN y la caché del navegador de forma independiente, con el siguiente Apache `mod_headers` directivas:

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header set Cache-Control "max-age=200"
        Header set Surrogate-Control "max-age=3600"
        Header set Age 0
   </LocationMatch>
   ```

   >[!NOTE]
   >El encabezado Surrogate-Control se aplica a la CDN administrada por Adobe. Si utiliza un [CDN gestionada por el cliente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html?lang=en#point-to-point-CDN), es posible que se requiera un encabezado diferente en función de su proveedor de CDN.

   Tenga cuidado al configurar encabezados de control de caché globales o aquellos que coinciden con un regex amplio para que no se apliquen a contenido que necesita mantener privado. Considere la posibilidad de utilizar varias directivas para garantizar que las reglas se apliquen de forma precisa. Dicho esto, AEM as a Cloud Service eliminará el encabezado de la caché si detecta que se ha aplicado a lo que detecta que Dispatcher no puede almacenar en caché, tal como se describe en la documentación de Dispatcher. Para obligar a los AEM a aplicar siempre los encabezados de almacenamiento en caché, se puede añadir la variable **always** como se indica a continuación:

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header unset Cache-Control
        Header unset Expires
        Header always set Cache-Control "max-age=200"
        Header set Age 0
   </LocationMatch>
   ```

   Debe asegurarse de que un archivo de `src/conf.dispatcher.d/cache` tiene la siguiente regla (que está en la configuración predeterminada):

   ```
   /0000
   { /glob "*" /type "allow" }
   ```

* Para evitar que se almacene en caché contenido específico **en la CDN**, establezca el encabezado Cache-Control en *private*. Por ejemplo, lo siguiente impediría el contenido html en un directorio denominado **secure** desde que se almacena en caché en la CDN:

   ```
      <LocationMatch "/content/secure/.*\.(html)$">.  // replace with the right regex
      Header unset Cache-Control
      Header unset Expires
      Header always set Cache-Control “private”
     </LocationMatch>
   ```

* Aunque el contenido del HTML establecido en privado no se almacenará en caché en la CDN, se puede almacenar en caché en el Dispatcher si [Almacenamiento en caché con permisos confidenciales](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=es) está configurado, lo que garantiza que solo se pueda servir el contenido a los usuarios autorizados.

   >[!NOTE]
   >Los demás métodos, incluido el [dispatcher-ttl AEM proyecto ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), no anulará correctamente los valores.

   >[!NOTE]
   >Tenga en cuenta que Dispatcher puede seguir almacenando en caché el contenido según su propio [reglas de almacenamiento en caché](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17497.html). Para que el contenido sea verdaderamente privado, debe asegurarse de que Dispatcher no lo almacene en caché.

### Bibliotecas de cliente (js, css) {#client-side-libraries}

* Al utilizar AEM marco de biblioteca del lado del cliente, el código JavaScript y CSS se generan de forma que los navegadores puedan almacenarlo en caché indefinidamente, ya que cualquier cambio se manifiesta como nuevos archivos con una ruta única.  En otras palabras, el HTML que hace referencia a las bibliotecas del cliente se producirá según sea necesario para que los clientes puedan experimentar contenido nuevo a medida que se publique. El control de caché se establece en &quot;inmutable&quot; o 30 días para los exploradores más antiguos que no respetan el valor &quot;inmutable&quot;.
* consulte la sección [Bibliotecas del lado del cliente y coherencia de la versión](#content-consistency) para obtener más información.

### Imágenes y cualquier contenido lo suficientemente grande como para almacenarse en blob. {#images}

El comportamiento predeterminado para los programas creados después de mediados de mayo de 2022 (específicamente, para los id de programa superiores a 65000) es almacenar en caché de forma predeterminada, respetando al mismo tiempo el contexto de autenticación de la solicitud. Los programas más antiguos (id de programa iguales o inferiores a 65000) no almacenan en caché el contenido del blob de forma predeterminada.

En ambos casos, los encabezados de almacenamiento en caché se pueden anular en un nivel más preciso en la capa Apache/Dispatcher mediante el uso de Apache `mod_headers` directivas, por ejemplo:

```
   <LocationMatch "^/content/.*\.(jpeg|jpg)$">
     Header set Cache-Control "max-age=222"
     Header set Age 0
   </LocationMatch>
```

Al modificar los encabezados de almacenamiento en caché en la capa de Dispatcher, tenga cuidado de no almacenar en caché demasiado ampliamente, vea la discusión en la sección HTML/texto [above](#html-text). Además, asegúrese de que los recursos que están destinados a ser guardados en privado (en lugar de en caché) no formen parte del `LocationMatch` filtros de directiva.

#### Nuevo comportamiento predeterminado de almacenamiento en caché {#new-caching-behavior}

La capa AEM establecerá los encabezados de caché en función de si el encabezado de caché ya se ha establecido y el valor del tipo de solicitud. Tenga en cuenta que si no se ha establecido ningún encabezado de control de caché, el contenido público se almacena en caché y el tráfico autenticado se establece en privado. Si se ha establecido un encabezado de control de caché, los encabezados de caché se dejarán intactos.

| ¿Existe el encabezado de control de caché? | Tipo de solicitud | AEM establece los encabezados de caché en |
|------------------------------|---------------|------------------------------------------------|
| No | público | Cache-Control: public, max-age=600, inmutable |
| No | autenticado | Cache-Control: privado, max-age=600, inmutable |
| Sí | cualquiera | sin cambios |

Aunque no se recomienda, es posible cambiar el nuevo comportamiento predeterminado para que siga el comportamiento anterior (id de programa iguales o inferiores a 65000) configurando la variable de entorno de Cloud Manager `AEM_BLOB_ENABLE_CACHING_HEADERS` en false.

#### Comportamiento de caché predeterminado anterior {#old-caching-behavior}

La capa AEM no almacenará en caché el contenido del blob de forma predeterminada.

>[!NOTE]
>Se recomienda cambiar el comportamiento predeterminado anterior para que sea coherente con el nuevo comportamiento (id de programa superiores a 65000) estableciendo la variable de entorno de Cloud Manager AEM_BLOB_ENABLE_CACHING_HEADERS en true. Si el programa ya está activo, asegúrese de que, después de los cambios, el contenido se comporta como espera.

Actualmente, las imágenes en almacenamiento de blob que están marcadas como privadas no se pueden almacenar en caché en el dispatcher mediante [Almacenamiento en caché con permisos confidenciales](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html). La imagen siempre se solicita desde el origen AEM y se proporciona si el usuario está autorizado.

>[!NOTE]
>Los demás métodos, incluido el [dispatcher-ttl AEM proyecto ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), no anulará correctamente los valores.

### Otros tipos de archivo de contenido en el almacén de nodos {#other-content}

* sin caché predeterminada
* el valor predeterminado no se puede establecer con la variable `EXPIRATION_TIME` variable utilizada para tipos de archivo html/text
* la caducidad de la caché se puede configurar con la misma estrategia LocationMatch descrita en la sección html/text especificando la regex adecuada

### Optimizaciones adicionales {#further-optimizations}

* Evite utilizar `User-Agent` como parte del `Vary` encabezado. Las versiones anteriores de la configuración predeterminada de Dispatcher (anteriores a la versión 28 del tipo de archivo) incluían esto y le recomendamos que lo elimine siguiendo los pasos a continuación.
   * Localice los archivos vhost en `<Project Root>/dispatcher/src/conf.d/available_vhosts/*.vhost`
   * Elimine o comente la línea: `Header append Vary User-Agent env=!dont-vary` de todos los archivos vhost, a excepción de default.vhost, que es de solo lectura
* Utilice la variable `Surrogate-Control` encabezado para controlar el almacenamiento en caché de CDN independientemente del almacenamiento en caché del explorador
* Considere la posibilidad de aplicar [`stale-while-revalidate`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-while-revalidate) y [`stale-if-error`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-if-error) directivas para permitir la actualización en segundo plano y evitar errores en la caché, lo que mantiene el contenido rápido y actualizado para los usuarios.
   * Existen muchas maneras de aplicar estas directivas, pero añadiendo un minuto `stale-while-revalidate` a todos los encabezados de control de caché es un buen punto de partida.
* A continuación se muestran algunos ejemplos de varios tipos de contenido, que pueden utilizarse como guía al configurar sus propias reglas de almacenamiento en caché. Tenga en cuenta y pruebe la configuración y los requisitos específicos:

   * Almacene en caché los recursos mutables de la biblioteca de cliente para las 12 horas y la actualización en segundo plano después de las 12 horas.

      ```
      <LocationMatch "^/etc\.clientlibs/.*\.(?i:json|png|gif|webp|jpe?g|svg)$">
         Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200,public" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * Almacene en caché los recursos inmutables de la biblioteca de cliente a largo plazo (30 días) con la actualización en segundo plano para evitar MISS.

      ```
      <LocationMatch "^/etc\.clientlibs/.*\.(?i:js|css|ttf|woff2)$">
         Header set Cache-Control "max-age=2592000,stale-while-revalidate=43200,stale-if-error=43200,public,immutable" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * Almacene en caché las páginas del HTML durante 5 minutos con la actualización en segundo plano de 1h en el explorador y 12h en CDN. Los encabezados Cache-Control siempre se añadirán, por lo que es importante asegurarse de que las páginas html coincidentes en /content/* sean públicas. Si no es así, considere la posibilidad de utilizar una regex más específica.

      ```
      <LocationMatch "^/content/.*\.html$">
         Header unset Cache-Control
         Header always set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
         Header always set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * Almacene en caché los servicios de contenido/las respuestas json del exportador del modelo Sling durante 5 minutos con la actualización en segundo plano de 1h en el navegador y 12h en la CDN.

      ```
      <LocationMatch "^/content/.*\.model\.json$">
         Header set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
         Header set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * Almacene en caché las direcciones URL inmutables del componente de imagen principal a largo plazo (30 días) con la actualización de fondo para evitar MISS.

      ```
      <LocationMatch "^/content/.*\.coreimg.*\.(?i:jpe?g|png|gif|svg)$">
         Header set Cache-Control "max-age=2592000,stale-while-revalidate=43200,stale-if-error=43200,public,immutable" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * Almacene en caché los recursos mutables de DAM como imágenes y vídeo durante 24h y la actualización de fondo después de 12h para evitar MISS

      ```
      <LocationMatch "^/content/dam/.*\.(?i:jpe?g|gif|js|mov|mp4|png|svg|txt|zip|ico|webp|pdf)$">
         Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

### Comportamiento de la solicitud del HEAD {#request-behavior}

Cuando se recibe una solicitud de HEAD en la CDN de Adobe para un recurso que **not** en la caché, la solicitud se transforma y se recibe mediante la instancia de Dispatcher o AEM como una solicitud de GET. Si la respuesta se puede almacenar en caché, las solicitudes de HEAD posteriores se servirán desde la CDN. Si la respuesta no se puede almacenar en caché, las solicitudes de HEAD posteriores se pasarán a la instancia de Dispatcher o AEM durante un período de tiempo que depende de la variable `Cache-Control` TTL.

### Parámetros de campaña de marketing {#marketing-parameters}

Las direcciones URL de sitios web suelen incluir parámetros de campaña de marketing que se utilizan para realizar el seguimiento del éxito de una campaña. Para utilizar la caché de Dispatcher de forma eficaz, se recomienda configurar la configuración de Dispatcher `ignoreUrlParams` property as [documentado aquí](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=es#ignoring-url-parameters).

La variable `ignoreUrlParams` no debe comentar y debe hacer referencia al archivo `conf.dispatcher.d/cache/marketing_query_parameters.any`. El archivo se puede modificar sin comentar las líneas correspondientes a los parámetros relevantes para los canales de marketing. También puede agregar otros parámetros.

```
/ignoreUrlParams {
{{ /0001 { /glob "*" /type "deny" }}}
{{ $include "../cache/marketing_query_parameters.any"}}
}
```

## Invalidación de caché de Dispatcher {#disp}

En general, no es necesario invalidar la caché de Dispatcher. En su lugar, debe confiar en que Dispatcher actualice su caché cuando se vuelva a publicar el contenido y en que la CDN respete los encabezados de caducidad de la caché.

### Invalidación de caché de Dispatcher durante la activación/desactivación {#cache-activation-deactivation}

Al igual que las versiones anteriores de AEM, al publicar o cancelar la publicación de páginas, se borra el contenido de la caché de Dispatcher. Si se sospecha que hay un problema con el almacenamiento en caché, los clientes deben volver a publicar las páginas en cuestión y asegurarse de que haya un host virtual disponible que coincida con la variable `ServerAlias` localhost, que es necesario para la invalidación de caché de Dispatcher.

Cuando la instancia de publicación recibe una nueva versión de una página o recurso del autor, utiliza el agente de vaciado para invalidar las rutas adecuadas en su Dispatcher. La ruta actualizada se elimina de la caché de Dispatcher, junto con sus principales, hasta un nivel (puede configurarla con el [statfileslevel](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level)).

## Invalidación explícita de la caché de Dispatcher {#explicit-invalidation}

Adobe recomienda confiar en los encabezados de caché estándar para controlar el ciclo de vida del envío de contenido. Sin embargo, si es necesario, es posible invalidar el contenido directamente en Dispatcher.

La siguiente lista contiene escenarios en los que puede que desee invalidar explícitamente la caché (mientras escucha opcionalmente la finalización de la invalidación):

* Después de publicar contenido, como fragmentos de experiencia o fragmentos de contenido, invalidando el contenido publicado y almacenado en caché que hace referencia a esos elementos.
* Notificar a un sistema externo cuando las páginas a las que se hace referencia se han invalidado correctamente.

Existen dos métodos para invalidar explícitamente la caché:

* El método preferido es usar Sling Content Distribution (SCD) de Author.
* Mediante el uso de la API de replicación para invocar el agente de replicación de vaciado de Dispatcher de publicación.

Los enfoques difieren en términos de disponibilidad del nivel, la capacidad de deduplicar eventos y la garantía de procesamiento de eventos. La tabla siguiente resume estas opciones:

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>N/D</th>
    <th>Disponibilidad de niveles</th>
    <th>Deduplicación </th>
    <th>Garantía </th>
    <th>Acción </th>
    <th>Impacto </th>
    <th>Descripción </th>
  </tr>  
  <tr>
    <td>API de distribución de contenido de Sling (SCD)</td>
    <td>Autor</td>
    <td>Posible uso de la API de Discovery o activación de la variable <a href="https://github.com/apache/sling-org-apache-sling-distribution-journal/blob/e18f2bd36e8b43814520e87bd4999d3ca77ce8ca/src/main/java/org/apache/sling/distribution/journal/impl/publisher/DistributedEventNotifierManager.java#L146-L149">modo de deduplicación</a>.</td>
    <td>Al menos una vez.</td>
    <td>
     <ol>
       <li>AÑADIR</li>
       <li>ELIMINAR</li>
       <li>INVALIDAR</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>Nivel jerárquico/estático</li>
       <li>Nivel jerárquico/estático</li>
       <li>Nivel de solo recurso</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>Publica contenido e invalida la caché.</li>
       <li>Elimina el contenido e invalida la caché.</li>
       <li>Invalida el contenido sin publicarlo.</li>
     </ol>
     </td>
  </tr>
  <tr>
    <td>API de replicación</td>
    <td>Publicación</td>
    <td>No es posible, el evento se ha generado en cada instancia de publicación.</td>
    <td>El mejor esfuerzo.</td>
    <td>
     <ol>
       <li>ACTIVAR</li>
       <li>DESACTIVAR</li>
       <li>ELIMINAR</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>Nivel jerárquico/estático</li>
       <li>Nivel jerárquico/estático</li>
       <li>Nivel jerárquico/estático</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>Publica contenido e invalida la caché.</li>
       <li>Desde el nivel de Author/Publish : elimina el contenido e invalida la caché.</li>
       <li><p><strong>Desde el nivel de Author</strong> - Elimina el contenido e invalida la caché (si se activa desde el nivel de AEM Author en el agente de publicación).</p>
           <p><strong>Desde el nivel de publicación</strong> : invalida solo la caché (si se activa desde el nivel de AEM Publish en el agente de vaciado o de vaciado de solo recursos).</p>
       </li>
     </ol>
     </td>
  </tr>
  </tbody>
</table>

Tenga en cuenta que las dos acciones directamente relacionadas con la invalidación de caché son la API de Sling Content Distribution (SCD) Invalidate y Replication API Deactivate.

Además, desde la mesa, observamos que:

* La API de SCD es necesaria cuando se debe garantizar cada evento, por ejemplo, sincronizándose con un sistema externo que requiera un conocimiento preciso. Si hay un evento de ampliación del nivel de publicación en el momento de la llamada de invalidación, se genera un evento adicional cuando cada nueva publicación procesa la invalidación.

* El uso de la API de replicación no es un caso de uso común, pero debe utilizarse en casos en los que el déclencheur para invalidar la caché proviene del nivel de publicación y no del de autor. Esto puede resultar útil si el TTL del distribuidor está configurado.

En conclusión, si desea invalidar la caché de Dispatcher, la opción recomendada es utilizar la acción de invalidación de la API SCD de Author. Además, también puede escuchar el evento para luego realizar más déclencheur en las acciones posteriores.

### Distribución de contenido de Sling (SCD) {#sling-distribution}

>[!NOTE]
>Cuando utilice las instrucciones que se muestran a continuación, tenga en cuenta que debe probar el código personalizado en un entorno de desarrollo de AEM Cloud Service y no localmente.

Al utilizar la acción SCD de Author, el patrón de implementación es el siguiente:

1. Desde Autor, escriba código personalizado para invocar la distribución de contenido de Sling [API](https://sling.apache.org/documentation/bundles/content-distribution.html), pasando la acción de invalidación con una lista de rutas:

```
@Reference
private Distributor distributor;

ResourceResolver resolver = ...; // the resource resolver used for authorizing the request
String agentName = "publish";    // the name of the agent used to distribute the request

String pathToInvalidate = "/content/to/invalidate";
DistributionRequest distributionRequest = new SimpleDistributionRequest(DistributionRequestType.INVALIDATE, false, pathToInvalidate);
distributor.distribute(agentName, resolver, distributionRequest);
```

* (Opcionalmente) Escuche un evento que refleje el recurso que se invalida para todas las instancias de Dispatcher:


```
package org.apache.sling.distribution.journal.shared;

import org.apache.sling.discovery.DiscoveryService;
import org.apache.sling.distribution.journal.impl.event.DistributionEvent;
import org.osgi.service.component.annotations.Component;
import org.osgi.service.component.annotations.Reference;
import org.osgi.service.event.Event;
import org.osgi.service.event.EventHandler;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import static org.apache.sling.distribution.DistributionRequestType.INVALIDATE;
import static org.apache.sling.distribution.event.DistributionEventProperties.DISTRIBUTION_PATHS;
import static org.apache.sling.distribution.event.DistributionEventProperties.DISTRIBUTION_TYPE;
import static org.apache.sling.distribution.event.DistributionEventTopics.AGENT_PACKAGE_DISTRIBUTED;
import static org.osgi.service.event.EventConstants.EVENT_TOPIC;

@Component(immediate = true, service = EventHandler.class, property = {
        EVENT_TOPIC + "=" + AGENT_PACKAGE_DISTRIBUTED
})
public class InvalidatedHandler implements EventHandler {
    private static final Logger LOG = LoggerFactory.getLogger(InvalidatedHandler.class);

    @Reference
    private DiscoveryService discoveryService;

    @Override
    public void handleEvent(Event event) {

        String distributionType = (String) event.getProperty(DISTRIBUTION_TYPE);

        if (INVALIDATE.name().equals(distributionType)) {
            boolean isLeader = discoveryService.getTopology().getLocalInstance().isLeader();
            // process the OSGi event on the leader author instance
            if (isLeader) {
                String[] paths = (String[]) event.getProperty(DISTRIBUTION_PATHS);
                String packageId = (String) event.getProperty(DistributionEvent.PACKAGE_ID);
                invalidated(paths, packageId);
            }
        }
    }

    private void invalidated(String[] paths, String packageId) {
        // custom logic
        LOG.info("Successfully applied package with id {}, paths {}", packageId, paths);
    }
}
```

<!-- Optionally, instead of using the isLeader approach, one could add an OSGi configuration for the PID org.apache.sling.distribution.journal.impl.publisher.DistributedEventNotifierManager and property deduplicateEvent=true. But we'll stick with just one strategy and not mention it (double-check this).**review this**-->

* (Opcional) Ejecute la lógica empresarial en la `invalidated(String[] paths, String packageId)` método anterior.

>[!NOTE]
>
>La CDN de Adobe no se vaciará cuando Dispatcher se invalide. La CDN gestionada por Adobe respeta los TTL y, por lo tanto, no es necesario vaciarla.

### API de replicación {#replication-api}

A continuación se muestra el patrón de implementación al utilizar la acción de desactivación de la API de replicación:

1. En el nivel de publicación, llame a la API de replicación para almacenar en déclencheur el agente de replicación de vaciado de Dispatcher de publicación.

El extremo del agente de vaciado no se puede configurar, sino que está preconfigurado para apuntar a Dispatcher, coincidiendo con el servicio de publicación que se ejecuta junto al agente de vaciado.

El agente de vaciado normalmente se puede activar mediante código personalizado basado en eventos o flujos de trabajo de OSGi.

```
String[] paths = …
ReplicationOptions options = new ReplicationOptions();
options.setSynchronous(true);
options.setFilter( new AgentFilter {
  public boolean isIncluded (Agent agent) {
   return agent.getId().equals(“flush”);
  }
});

Replicator.replicate (session,ReplicationActionType.DELETE,paths, options);
```

<!-- In general, it will not be necessary to manually invalidate content in the dispatcher, but it is possible if needed.

>[!NOTE]
>Prior to AEM as a Cloud Service, there were two ways of invalidating the dispatcher cache.
>
>1. Invoke the replication agent, specifying the publish dispatcher flush agent
>2. Directly calling the `invalidate.cache` API (for example, `POST /dispatcher/invalidate.cache`)
>
>The dispatcher's `invalidate.cache` API approach will no longer be supported since it addresses only a specific dispatcher node. AEM as a Cloud Service operates at the service level, not the individual node level and so the invalidation instructions in the [Invalidating Cached Pages From AEM](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html) page are not longer valid for AEM as a Cloud Service.

The replication flush agent should be used. This can be done using the [Replication API](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/replication/Replicator.html). The flush agent endpoint is not configurable but pre-configured to point to the dispatcher, matched with the publish service running the flush agent. The flush agent can typically be triggered by OSGi events or workflows.

<!-- Need to find a new link and/or example -->
<!-- 
and for an example of flushing the cache, see the [API example page](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) (specifically the `CustomStep` example issuing a replication action of type ACTIVATE to all available agents). 

The diagram presented below illustrates this.

![CDN](assets/cdnd.png "CDN")

If there is a concern that the dispatcher cache isn't clearing, contact [customer support](https://helpx.adobe.com/support.ec.html) who can flush the dispatcher cache if necessary.

The Adobe-managed CDN respects TTLs and thus there is no need fo it to be flushed. If an issue is suspected, [contact customer support](https://helpx.adobe.com/support.ec.html) support who can flush an Adobe-managed CDN cache as necessary. -->

## Bibliotecas de cliente y coherencia de la versión {#content-consistency}

Las páginas están compuestas de HTML, JavaScript, CSS e imágenes. Se recomienda a los clientes que aprovechen la variable [Marco de bibliotecas del lado del cliente (clientlibs)](/help/implementing/developing/introduction/clientlibs.md) para importar recursos de JavaScript y CSS en páginas de HTML, teniendo en cuenta las dependencias entre bibliotecas de JS.

El marco clientlibs proporciona administración automática de versiones, lo que significa que los desarrolladores pueden registrar cambios en las bibliotecas JS en control de código fuente y la última versión estará disponible cuando un cliente implemente su lanzamiento. Sin esto, los desarrolladores necesitarían cambiar manualmente el HTML con referencias a la nueva versión de la biblioteca, lo que resulta especialmente oneroso si muchas plantillas de HTML comparten la misma biblioteca.

Cuando se lanzan las nuevas versiones de las bibliotecas a la producción, las páginas del HTML de referencia se actualizan con nuevos vínculos a esas versiones actualizadas de la biblioteca. Una vez que la caché del explorador ha caducado para una página de HTML determinada, no existe ninguna preocupación en cuanto a que las bibliotecas antiguas se cargarán desde la caché del explorador, ya que la página actualizada (desde AEM) ahora hace referencia a las nuevas versiones de las bibliotecas. En otras palabras, una página HTML actualizada incluirá todas las versiones de la biblioteca más recientes.

El mecanismo para esto es un hash serializado, que se adjunta al vínculo de la biblioteca del cliente, lo que garantiza una url única y versionada para que el explorador almacene en caché CSS/JS. El hash serializado solo se actualiza cuando cambia el contenido de la biblioteca del cliente. Esto significa que si se producen actualizaciones no relacionadas (es decir, no se producen cambios en el css/js subyacente de la biblioteca del cliente) incluso con una nueva implementación, la referencia permanece igual, lo que garantiza menos interrupciones en la caché del explorador.

### Activación de versiones de Longcache de bibliotecas del cliente: inicio rápido AEM SDK as a Cloud Service {#enabling-longcache}

La clientlib predeterminada incluye en una página de HTML se parece al siguiente ejemplo:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.css" type="text/css">
```

Cuando está habilitado el control de versiones de clientlib estricto, se agrega una clave hash a largo plazo como selector a la biblioteca del cliente. Como resultado, la referencia clientlib tiene este aspecto:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.lc-7c8c5d228445ff48ab49a8e3c865c562-lc.css" type="text/css">
```

El control de versiones de clientlib estricto está habilitado de forma predeterminada en todos AEM entornos as a Cloud Service.

Para habilitar versiones clientlib estrictas en el SDK local Quickstart, realice las siguientes acciones:

1. Vaya al gestor de configuración OSGi `<host>/system/console/configMgr`
1. Busque la configuración OSGi para el Administrador de biblioteca del HTML de Adobe Granite:
   * Marque la casilla de verificación para activar el control estricto de versiones
   * En el campo denominado Long term client side cache key, introduzca el valor de /.*;hash
1. Guarde los cambios. No es necesario guardar esta configuración en el control de código fuente, ya que AEM as a Cloud Service habilita automáticamente esta configuración en entornos de desarrollo, fase y producción.
1. Cada vez que se cambia el contenido de la biblioteca del cliente, se genera una nueva clave hash y se actualiza la referencia del HTML.
