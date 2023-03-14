---
title: Almacenamiento en caché en AEM as a Cloud Service
description: Almacenamiento en caché en AEM as a Cloud Service
feature: Dispatcher
exl-id: 4206abd1-d669-4f7d-8ff4-8980d12be9d6
source-git-commit: 6bca307dcf41b138b5b724a8eb198ac35e2d906e
workflow-type: tm+mt
source-wordcount: '2832'
ht-degree: 2%

---

# Introducción {#intro}

El tráfico pasa a través de la CDN a una capa de servidor web Apache, que admite módulos como Dispatcher. Para aumentar el rendimiento, Dispatcher se utiliza principalmente como caché para limitar el procesamiento en los nodos de publicación.
Se pueden aplicar reglas a la configuración de Dispatcher para modificar cualquier configuración de caducidad de caché predeterminada, lo que resulta en el almacenamiento en caché en la CDN. Tenga en cuenta que Dispatcher también respeta los encabezados de caducidad de caché resultantes si `enableTTL` está habilitado en la configuración de Dispatcher, lo que implica que actualizará contenido específico incluso fuera del contenido que se vuelve a publicar.

Esta página también describe cómo se invalida la caché de Dispatcher y cómo funciona el almacenamiento en caché en el nivel del explorador con respecto a las bibliotecas del lado del cliente.

## Almacenamiento en caché {#caching}

### HTML/Texto {#html-text}

* de forma predeterminada, el explorador almacena en caché durante cinco minutos, según el `cache-control` encabezado emitido por la capa de Apache. La CDN también respeta este valor.
* la configuración predeterminada de almacenamiento en caché de HTML/texto se puede deshabilitar definiendo la variable `DISABLE_DEFAULT_CACHING` variable en `global.vars`:

```
Define DISABLE_DEFAULT_CACHING
```

Esto puede resultar útil, por ejemplo, cuando la lógica empresarial requiere un ajuste preciso del encabezado de edad (con un valor basado en el día del calendario), ya que de forma predeterminada el encabezado de edad se establece en 0. Dicho esto, **tenga cuidado al desactivar el almacenamiento en caché predeterminado.**

* se puede sobrescribir para todo el contenido de HTML/texto definiendo la variable `EXPIRATION_TIME` variable en `global.vars` AEM uso de las herramientas de Dispatcher del SDK as a Cloud Service de.
* puede anularse en un nivel más preciso, incluido el control independiente de la CDN y la caché del explorador, con el siguiente Apache `mod_headers` directivas:

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header set Cache-Control "max-age=200"
        Header set Surrogate-Control "max-age=3600"
        Header set Age 0
   </LocationMatch>
   ```

   >[!NOTE]
   >El encabezado Surrogate-Control se aplica a la CDN administrada por Adobe. Si se usa un [CDN administrado por el cliente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html?lang=en#point-to-point-CDN), es posible que se requiera un encabezado diferente según el proveedor de CDN.

   Tenga cuidado al configurar los encabezados de control de caché global o los que coinciden con una regex amplia, de modo que no se apliquen al contenido que necesita mantener privado. Considere la posibilidad de utilizar varias directivas para garantizar que las reglas se aplican de manera precisa. AEM Dicho esto, el encabezado de caché se eliminará de manera as a Cloud Service si detecta que Dispatcher lo ha aplicado a lo que detecta que Dispatcher no puede almacenar en caché, tal como se describe en la documentación de Dispatcher. AEM Para obligar a los usuarios a aplicar siempre los encabezados de almacenamiento en caché, se puede añadir la variable **siempre** como se indica a continuación:

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header unset Cache-Control
        Header unset Expires
        Header always set Cache-Control "max-age=200"
        Header set Age 0
   </LocationMatch>
   ```

   Debe asegurarse de que un archivo en `src/conf.dispatcher.d/cache` tiene la siguiente regla (que está en la configuración predeterminada):

   ```
   /0000
   { /glob "*" /type "allow" }
   ```

* Para evitar que el contenido específico se almacene en caché **en la CDN**, establezca el encabezado Cache-Control en *privado*. Por ejemplo, lo siguiente impediría el contenido html en un directorio llamado **secure** de la caché en la CDN:

   ```
      <LocationMatch "/content/secure/.*\.(html)$">.  // replace with the right regex
      Header unset Cache-Control
      Header unset Expires
      Header always set Cache-Control "private"
     </LocationMatch>
   ```

* Aunque el contenido del HTML establecido en privado no se almacenará en caché en la CDN, se puede almacenar en caché en el despachante si [Almacenamiento en caché con permisos confidenciales](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=es) , asegurándose de que solo los usuarios autorizados puedan recibir el contenido.

   >[!NOTE]
   >Los demás métodos, incluido el [AEM dispatcher-ttl proyecto de ACS Commons en el que se](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), no anulará correctamente los valores.

   >[!NOTE]
   >Tenga en cuenta que Dispatcher podría seguir almacenando en caché el contenido según su propio código [reglas de almacenamiento en caché](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17497.html). Para que el contenido sea verdaderamente privado, debe asegurarse de que Dispatcher no lo almacene en caché.

### Bibliotecas del lado cliente (js,css) {#client-side-libraries}

* AEM Al utilizar el marco de trabajo de biblioteca del lado del cliente de, el código JavaScript y CSS se genera de tal manera que los exploradores pueden almacenarlo en caché indefinidamente, ya que cualquier cambio se manifiesta como nuevos archivos con una ruta única.  Es decir, el HTML que haga referencia a las bibliotecas del cliente se creará según sea necesario para que los clientes puedan experimentar el nuevo contenido a medida que se publique. El control de caché se establece en &quot;inmutable&quot; o 30 días para exploradores más antiguos que no respetan el valor &quot;inmutable&quot;.
* consulte la sección [Bibliotecas del lado del cliente y coherencia de versiones](#content-consistency) para obtener más información.

### Las imágenes y cualquier contenido lo suficientemente grande como para almacenarse en el almacenamiento de blobs {#images}

El comportamiento predeterminado de los programas creados después de mediados de mayo de 2022 (específicamente, para los ID de programa superiores a 65000) es almacenar en caché de forma predeterminada, respetando también el contexto de autenticación de la solicitud. Los programas más antiguos (ID de programa iguales o inferiores a 65000) no almacenan en caché el contenido del blob de forma predeterminada.

En ambos casos, los encabezados de almacenamiento en caché se pueden sobrescribir en un nivel de granulado más preciso en la capa de Apache/Dispatcher mediante Apache `mod_headers` directivas, por ejemplo:

```
   <LocationMatch "^/content/.*\.(jpeg|jpg)$">
     Header set Cache-Control "max-age=222"
     Header set Age 0
   </LocationMatch>
```

Al modificar los encabezados de almacenamiento en caché en la capa de Dispatcher, tenga cuidado de no almacenar en caché demasiado ampliamente. Consulte la descripción en la sección HTML/texto [superior](#html-text). Además, asegúrese de que los recursos que se supone que deben mantenerse privados (en lugar de almacenarse en caché) no formen parte del `LocationMatch` filtros de directiva.

#### Nuevo comportamiento de almacenamiento en caché predeterminado {#new-caching-behavior}

AEM La capa de datos establecerá encabezados de caché en función de si el encabezado de caché ya se ha establecido y el valor del tipo de solicitud. Tenga en cuenta que si no se ha establecido ningún encabezado de control de caché, el contenido público se almacena en caché y el tráfico autenticado se establece en privado. Si se ha establecido un encabezado de control de caché, los encabezados de caché no se tocarán.

| ¿Existe el encabezado de control de caché? | Tipo de solicitud | AEM establece encabezados de caché en |
|------------------------------|---------------|------------------------------------------------|
| No | público | Cache-Control: public, max-age=600, inmutable |
| No | autenticado | Cache-Control: private, max-age=600, inmutable |
| Sí | cualquiera | inalterable |

Aunque no se recomienda, es posible cambiar el nuevo comportamiento predeterminado para seguir el comportamiento anterior (ID de programa iguales o inferiores a 65000) configurando la variable de entorno de Cloud Manager `AEM_BLOB_ENABLE_CACHING_HEADERS` a false.

#### Comportamiento de almacenamiento en caché predeterminado anterior {#old-caching-behavior}

AEM La capa no almacenará en caché el contenido del blob de forma predeterminada.

>[!NOTE]
>AEM Se recomienda cambiar el comportamiento predeterminado anterior para que sea coherente con el nuevo comportamiento (ID de programa superiores a 65000) estableciendo la variable de entorno de Cloud Manager,_BLOB_ENABLE_CACHING_HEADERS, en true. Si el programa ya está activo, asegúrese de verificar que después de los cambios, el contenido se comporta como espera.

En este momento, las imágenes en el almacenamiento del blob marcadas como privadas no se pueden almacenar en caché en Dispatcher mediante [Almacenamiento en caché con permisos confidenciales](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=es). AEM La imagen siempre se solicita desde el origen de la y se sirve si el usuario está autorizado.

>[!NOTE]
>Los demás métodos, incluido el [AEM dispatcher-ttl proyecto de ACS Commons en el que se](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), no anulará correctamente los valores.

### Otros tipos de archivo de contenido en el almacén de nodos {#other-content}

* sin almacenamiento en caché predeterminado
* el valor predeterminado no se puede establecer con `EXPIRATION_TIME` variable utilizada para tipos de archivo html/text
* la caducidad de la caché se puede establecer con la misma estrategia de LocationMatch descrita en la sección html/text especificando la regex adecuada

### Optimizaciones adicionales {#further-optimizations}

* Evite utilizar `User-Agent` como parte de `Vary` encabezado. Las versiones anteriores de la configuración predeterminada de Dispatcher (anteriores a la versión 28 del tipo de archivo) incluían esto y le recomendamos que lo elimine siguiendo los pasos a continuación.
   * Busque los archivos vhost en `<Project Root>/dispatcher/src/conf.d/available_vhosts/*.vhost`
   * Elimine o comente la línea: `Header append Vary User-Agent env=!dont-vary` de todos los archivos vhost, excepto default.vhost, que es de sólo lectura
* Utilice el `Surrogate-Control` encabezado para controlar el almacenamiento en caché de CDN independiente del almacenamiento en caché del explorador
* Considere aplicar [`stale-while-revalidate`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-while-revalidate) y [`stale-if-error`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-if-error) directivas para permitir la actualización en segundo plano y evitar errores de caché, manteniendo el contenido rápido y fresco para los usuarios.
   * Existen muchas maneras de aplicar estas directivas, pero se añade un intervalo de 30 minutos `stale-while-revalidate` la conexión a todos los encabezados de control de caché es un buen punto de partida.
* A continuación se muestran algunos ejemplos de varios tipos de contenido, que pueden utilizarse como guía al configurar sus propias reglas de almacenamiento en caché. Tenga en cuenta y pruebe su configuración y requisitos específicos:

   * Almacenar en caché recursos de biblioteca de cliente mutables durante 12 horas y actualizar en segundo plano después de 12 horas.

      ```
      <LocationMatch "^/etc\.clientlibs/.*\.(?i:json|png|gif|webp|jpe?g|svg)$">
         Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200,public" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * Almacene en caché los recursos de la biblioteca de cliente inmutables a largo plazo (30 días) con actualización en segundo plano para evitar errores.

      ```
      <LocationMatch "^/etc\.clientlibs/.*\.(?i:js|css|ttf|woff2)$">
         Header set Cache-Control "max-age=2592000,stale-while-revalidate=43200,stale-if-error=43200,public,immutable" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * Almacene en caché las páginas del HTML durante 5 minutos con una actualización en segundo plano en el navegador durante 1 hora y en CDN durante 12 horas. Los encabezados Cache-Control siempre se añadirán, por lo que es importante asegurarse de que las páginas HTML coincidentes en /content/* están pensadas para ser públicas. Si no es así, considere la posibilidad de utilizar una regex más específica.

      ```
      <LocationMatch "^/content/.*\.html$">
         Header unset Cache-Control
         Header always set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
         Header always set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * Almacene en caché las respuestas json del exportador de servicios de contenido/modelos Sling durante 5 minutos con una actualización en segundo plano 1 h en el explorador y 12 h en CDN.

      ```
      <LocationMatch "^/content/.*\.model\.json$">
         Header set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
         Header set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * Almacene en caché las URL inmutables del componente de imagen principal a largo plazo (30 días) con una actualización en segundo plano para evitar errores.

      ```
      <LocationMatch "^/content/.*\.coreimg.*\.(?i:jpe?g|png|gif|svg)$">
         Header set Cache-Control "max-age=2592000,stale-while-revalidate=43200,stale-if-error=43200,public,immutable" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * Almacene en caché recursos mutables de DAM, como imágenes y vídeo, durante 24 horas y actualizaciones en segundo plano después de 12 horas para evitar errores

      ```
      <LocationMatch "^/content/dam/.*\.(?i:jpe?g|gif|js|mov|mp4|png|svg|txt|zip|ico|webp|pdf)$">
         Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

### comportamiento de solicitud del HEAD {#request-behavior}

Cuando se recibe una solicitud de HEAD en la CDN de Adobe para un recurso que **no** AEM en caché, la solicitud se transforma y recibe en Dispatcher o en la instancia de como una solicitud de GET. Si la respuesta se puede almacenar en caché, las solicitudes de HEAD posteriores se atenderán desde la CDN. Si la respuesta no se puede almacenar en caché, las solicitudes de HEAD AEM posteriores se pasarán a la instancia de Dispatcher o a la instancia de durante un período de tiempo que depende de la variable `Cache-Control` TTL.

### Parámetros de campaña de marketing {#marketing-parameters}

Las direcciones URL del sitio web suelen incluir parámetros de campañas de marketing que se utilizan para realizar el seguimiento del éxito de una campaña. Para utilizar la caché de Dispatcher de forma eficaz, se recomienda configurar el `ignoreUrlParams` propiedad como [documentado aquí](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=es#ignoring-url-parameters).

El `ignoreUrlParams` La sección debe estar descomentada y debe hacer referencia al archivo `conf.dispatcher.d/cache/marketing_query_parameters.any`. El archivo se puede modificar sin comentar las líneas correspondientes a los parámetros relevantes para sus canales de marketing. También puede agregar otros parámetros.

```
/ignoreUrlParams {
{{ /0001 { /glob "*" /type "deny" }}}
{{ $include "../cache/marketing_query_parameters.any"}}
}
```

## Invalidación de caché de Dispatcher {#disp}

En general, no será necesario invalidar la caché de Dispatcher. En su lugar, debe depender de que Dispatcher actualice su caché cuando el contenido se vuelve a publicar y que la CDN respete los encabezados de caducidad de la caché.

### Invalidación de la caché de Dispatcher durante la activación/desactivación {#cache-activation-deactivation}

AEM Al igual que las versiones anteriores de la aplicación, la publicación o cancelación de la publicación de páginas borra el contenido de la caché de Dispatcher. Si se sospecha un problema de almacenamiento en caché, debe volver a publicar las páginas en cuestión y asegurarse de que haya un host virtual disponible que coincida con el de `ServerAlias` localhost, que es necesario para invalidar la caché de Dispatcher.

>[!NOTE]
>Para la correcta invalidación de Dispatcher, asegúrese de que las solicitudes de &quot;127.0.0.1&quot;, &quot;localhost&quot;, &quot;.local&quot;, &quot;.adobeaemcloud.com&quot; y &quot;.adobeaemcloud.net&quot; coincidan y se gestionen mediante una configuración de vhost para que se puedan servir esas solicitudes. Puede hacerlo haciendo coincidir globalmente &quot;*&quot; en una configuración de vhost global siguiendo el patrón de la referencia [AEM tipo de archivo de](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/dispatcher.cloud/src/conf.d/available_vhosts/default.vhost) o asegurándose de que la lista mencionada anteriormente sea capturada por uno de los vhosts.

Cuando la instancia de publicación recibe una nueva versión de una página o recurso del autor, utiliza el agente de vaciado para invalidar las rutas adecuadas en su Dispatcher. La ruta actualizada se elimina de la caché de Dispatcher, junto con sus elementos primarios, hasta un nivel (puede configurarlo con la variable [statfileslevel](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level)).

## Invalidación explícita de la caché de Dispatcher {#explicit-invalidation}

La Adobe recomienda confiar en los encabezados de caché estándar para controlar el ciclo de vida de la entrega de contenido. Sin embargo, si es necesario, es posible invalidar el contenido directamente en Dispatcher.

La siguiente lista contiene escenarios en los que puede que desee invalidar explícitamente la caché (mientras escucha opcionalmente la finalización de la invalidación):

* Después de publicar contenido, como fragmentos de experiencias o fragmentos de contenido, invalide el contenido publicado y almacenado en caché que hace referencia a esos elementos.
* Notificar a un sistema externo cuando se han invalidado correctamente las páginas a las que se hace referencia.

Existen dos métodos para invalidar explícitamente la caché:

* El método preferido es usar Sling Content Distribution (SCD) de Author.
* Mediante la API de replicación para invocar el agente de replicación de vaciado de Dispatcher de publicación.

Los enfoques difieren en términos de disponibilidad de niveles, la capacidad de deduplicar eventos y la garantía de procesamiento de eventos. La tabla siguiente resume estas opciones:

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>N/D</th>
    <th>Disponibilidad de nivel</th>
    <th>Deduplicación </th>
    <th>Garantía </th>
    <th>Acción </th>
    <th>Impacto </th>
    <th>Descripción </th>
  </tr>  
  <tr>
    <td>API de distribución de contenido de Sling (SCD)</td>
    <td>Autor</td>
    <td>Es posible mediante la API de detección o habilitando <a href="https://github.com/apache/sling-org-apache-sling-distribution-journal/blob/e18f2bd36e8b43814520e87bd4999d3ca77ce8ca/src/main/java/org/apache/sling/distribution/journal/impl/publisher/DistributedEventNotifierManager.java#L146-L149">modo de deduplicación</a>.</td>
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
       <li>Redistribuir solo recursos</li>
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
    <td>No es posible, se produjo un evento en cada instancia de publicación.</td>
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
       <li>Desde el nivel de creación/publicación: elimina el contenido e invalida la caché.</li>
       <li><p><strong>Desde el nivel de Author</strong> : elimina el contenido e invalida la caché (si se activa desde el nivel de AEM Author en el agente de publicación).</p>
           <p><strong>Desde nivel de publicación</strong> : invalida únicamente la caché (si se activa desde el nivel de publicación de AEM en el agente de vaciado o de vaciado solo de recursos).</p>
       </li>
     </ol>
     </td>
  </tr>
  </tbody>
</table>

Tenga en cuenta que las dos acciones directamente relacionadas con la invalidación de la caché son Invalidación de la API de Sling Content Distribution (SCD) y Desactivación de la API de replicación.

Además, desde la mesa, observamos que:

* La API de SCD es necesaria cuando se debe garantizar cada evento, por ejemplo, la sincronización con un sistema externo que requiera un conocimiento preciso. Si hay un evento de actualización del nivel de publicación en el momento de la llamada de invalidación, se genera un evento adicional cuando cada nueva publicación procesa la invalidación.

* El uso de la API de replicación no es un caso de uso común, pero debe utilizarse en casos en que la déclencheur para invalidar la caché provenga del nivel de publicación y no del de creación. Esto puede resultar útil si se ha configurado el TTL de Dispatcher.

En conclusión, si desea invalidar la caché de Dispatcher, la opción recomendada es utilizar la acción Invalidar la API de SCD del autor. Además, también puede escuchar el evento para poder almacenar en déclencheur más acciones descendentes.

### Sling Content Distribution (SCD) {#sling-distribution}

>[!NOTE]
>Cuando utilice las instrucciones presentadas a continuación, tenga en cuenta que debe probar el código personalizado en un entorno de desarrollo de AEM Cloud Service y no localmente.

Al utilizar la acción SCD de Autor, el patrón de implementación es el siguiente:

1. Desde Autor, escriba un código personalizado para invocar la distribución de contenido de Sling [API](https://sling.apache.org/documentation/bundles/content-distribution.html), pasando la acción de invalidación con una lista de rutas:

```
@Reference
private Distributor distributor;

ResourceResolver resolver = ...; // the resource resolver used for authorizing the request
String agentName = "publish";    // the name of the agent used to distribute the request

String pathToInvalidate = "/content/to/invalidate";
DistributionRequest distributionRequest = new SimpleDistributionRequest(DistributionRequestType.INVALIDATE, false, pathToInvalidate);
distributor.distribute(agentName, resolver, distributionRequest);
```

* (Opcional) Escuche un evento que refleje el recurso que se está invalidando para todas las instancias de Dispatcher:


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

* (Opcional) Ejecute la lógica empresarial en la variable `invalidated(String[] paths, String packageId)` método anterior.

>[!NOTE]
>
>La CDN de Adobe no se vacía cuando Dispatcher se invalida. La CDN administrada por la Adobe respeta los TTL y, por lo tanto, no es necesario vaciarla.

### API de replicación {#replication-api}

A continuación se muestra el patrón de implementación al utilizar la acción de desactivación de la API de replicación:

1. En el nivel de publicación, llame a la API de replicación para almacenar en déclencheur el agente de replicación de vaciado de Dispatcher de publicación.

El extremo del agente de vaciado no se puede configurar, sino que está preconfigurado para señalar a Dispatcher, lo que coincide con el servicio de publicación que se ejecuta junto con el agente de vaciado.

El agente de vaciado suele activarse mediante código personalizado basado en eventos OSGi o flujos de trabajo.

```
String[] paths = …
ReplicationOptions options = new ReplicationOptions();
options.setSynchronous(true);
options.setFilter( new AgentFilter {
  public boolean isIncluded (Agent agent) {
   return agent.getId().equals("flush");
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

## Bibliotecas del lado del cliente y coherencia de versiones {#content-consistency}

Las páginas están compuestas por HTML, JavaScript, CSS e imágenes. Se recomienda a los clientes que aprovechen las [Marco de bibliotecas del lado del cliente (clientlibs)](/help/implementing/developing/introduction/clientlibs.md) para importar recursos Javascript y CSS en páginas de HTML, teniendo en cuenta las dependencias entre bibliotecas JS.

El marco clientlibs proporciona administración automática de versiones, lo que significa que los desarrolladores pueden proteger los cambios en las bibliotecas JS en el control de código fuente y la última versión estará disponible cuando un cliente inserte su versión. Sin esto, los desarrolladores tendrían que cambiar manualmente HTML con referencias a la nueva versión de la biblioteca, lo que resulta especialmente oneroso si muchas plantillas de HTML comparten la misma biblioteca.

Cuando se publican las nuevas versiones de las bibliotecas de en producción, las páginas del HTML de referencia se actualizan con nuevos vínculos a esas versiones de la biblioteca actualizadas. Una vez que la caché del explorador ha caducado para una página de HTML AEM determinada, no hay problema con que las bibliotecas antiguas se carguen desde la caché del explorador, ya que ahora se garantiza que la página actualizada (desde la que se actualizó la biblioteca) hace referencia a las nuevas versiones de las bibliotecas. En otras palabras, una página de HTML actualizada incluirá todas las versiones de la biblioteca más recientes.

El mecanismo para esto es un hash serializado, que se anexa al vínculo de biblioteca del cliente, lo que garantiza una URL única con versiones para que el explorador almacene en caché el CSS/JS. El hash serializado solo se actualiza cuando cambia el contenido de la biblioteca de cliente. Esto significa que si se producen actualizaciones no relacionadas (es decir, no se producen cambios en el css/js subyacente de la biblioteca del cliente) incluso con una nueva implementación, la referencia sigue siendo la misma, lo que garantiza menos interrupciones en la caché del explorador.

### AEM Activación de las versiones de caché larga de las bibliotecas del lado del cliente: inicio rápido del SDK as a Cloud Service de {#enabling-longcache}

Las inclusiones clientlib predeterminadas en una página de HTML tienen el siguiente aspecto:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.css" type="text/css">
```

Cuando se habilita el control de versiones de clientlib estricto, se agrega una clave hash a largo plazo como selector a la biblioteca de cliente. Como resultado, la referencia clientlib tiene este aspecto:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.lc-7c8c5d228445ff48ab49a8e3c865c562-lc.css" type="text/css">
```

AEM Las versiones de clientlib estrictas están habilitadas de forma predeterminada en todos los entornos as a Cloud Service de.

Para habilitar las versiones clientlib estrictas en el Quickstart de SDK local, realice las siguientes acciones:

1. Vaya al Administrador de configuración de OSGi `<host>/system/console/configMgr`
1. Busque la configuración OSGi para el administrador de bibliotecas del HTML de Adobe Granite:
   * Marque la casilla de verificación para habilitar las versiones estrictas.
   * En el campo denominado Long term client side cache key, introduzca el valor de /.*;hash
1. Guarde los cambios. AEM No es necesario guardar esta configuración en el control de código fuente, ya que la configuración as a Cloud Service de la habilita automáticamente en los entornos de desarrollo, fase y producción.
1. Cada vez que se cambia el contenido de la biblioteca del cliente, se genera una nueva clave hash y se actualiza la referencia del HTML.
