---
title: Almacenamiento en caché en AEM as a Cloud Service
description: Obtenga información acerca de los conceptos básicos del almacenamiento en caché en AEM as a Cloud Service
feature: Dispatcher
exl-id: 4206abd1-d669-4f7d-8ff4-8980d12be9d6
role: Admin
source-git-commit: 3a46db9c98fe634bf2d4cffd74b54771de748515
workflow-type: tm+mt
source-wordcount: '3071'
ht-degree: 1%

---

# Introducción {#intro}

El tráfico pasa a través de la CDN a una capa de servidor web Apache, que admite módulos como Dispatcher. Para aumentar el rendimiento, Dispatcher se utiliza principalmente como caché para limitar el procesamiento en los nodos de publicación.
Se pueden aplicar reglas a la configuración de Dispatcher para modificar cualquier configuración de caducidad de caché predeterminada, lo que resulta en el almacenamiento en caché en la CDN. Dispatcher también respeta los encabezados de caducidad de caché resultantes si `enableTTL` está habilitado en la configuración de Dispatcher, lo que implica que actualiza contenido específico incluso fuera del contenido que se vuelve a publicar.

Esta página también describe cómo se invalida la caché de Dispatcher y cómo funciona el almacenamiento en caché a nivel del explorador con respecto a las bibliotecas del lado del cliente.

## Almacenamiento en caché {#caching}

El almacenamiento en caché de las respuestas HTTP en la CDN de AEM as a Cloud Service está controlado por los siguientes encabezados de respuesta HTTP del origen: `Cache-Control`, `Surrogate-Control` o `Expires`.

Estos encabezados de caché generalmente se establecen en configuraciones vhost de AEM Dispatcher mediante mod_headers, pero también se pueden establecer en código Java™ personalizado que se ejecuta en la propia publicación de AEM (consulte [Cómo habilitar el almacenamiento en caché de CDN](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/caching/how-to/enable-caching)).

La clave de caché para los recursos de CDN contiene la dirección URL de solicitud completa, incluidos los parámetros de consulta, por lo que cada parámetro de consulta diferente producirá una entrada de caché diferente. Considere la posibilidad de eliminar los parámetros de consulta no deseados; [consulte lo siguiente](#marketing-parameters) para mejorar la proporción de visitas de caché.

La CDN de AEM as a Cloud Service no almacena en caché las respuestas de origen que contienen `private`, `no-cache` o `no-store` en `Cache-Control` (consulte [Cómo deshabilitar el almacenamiento en caché de CDN](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/caching/how-to/disable-caching) para obtener más información).  Además, la CDN no almacena en caché las respuestas que configuran cookies, es decir, que tienen un encabezado de respuesta `Set-Cookie`.

### HTML/Texto {#html-text}

La configuración de Dispatcher establece algunos encabezados de almacenamiento en caché predeterminados para el tipo de contenido `text/html`.

* de forma predeterminada, el explorador almacena en caché durante cinco minutos, según el encabezado `cache-control` emitido por la capa de Apache. La CDN también respeta este valor.
* la configuración predeterminada de almacenamiento en caché de HTML/texto se puede deshabilitar definiendo la variable `DISABLE_DEFAULT_CACHING` en `global.vars`:

```
Define DISABLE_DEFAULT_CACHING
```

Este método es útil, por ejemplo, cuando la lógica empresarial requiere ajustar el encabezado age (con un valor basado en el día del calendario) ya que, de forma predeterminada, el encabezado age se establece en 0. Dicho esto, **tenga cuidado al desactivar el almacenamiento en caché predeterminado.**

* se puede sobrescribir para todo el contenido de HTML/Text definiendo la variable `EXPIRATION_TIME` en `global.vars` con las herramientas de AEM as a Cloud Service SDK Dispatcher.
* puede anularse en un nivel más preciso, incluido el control independiente de la CDN y la caché del explorador, con las siguientes directivas de Apache `mod_headers`:

  ```
  <LocationMatch "^/content/.*\.(html)$">
       Header set Cache-Control "max-age=200"
       Header set Surrogate-Control "max-age=3600"
       Header set Age 0
  </LocationMatch>
  ```

  >[!NOTE]
  >El encabezado Surrogate-Control se aplica a la CDN administrada por Adobe. Si utiliza una [CDN administrada por el cliente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html?lang=es#point-to-point-CDN), puede ser necesario un encabezado diferente en función de su proveedor de CDN.

  Tenga cuidado al configurar encabezados de control de caché globales o encabezados de caché similares que coincidan con una regex amplia, de modo que no se apliquen al contenido que debe mantener privado. Considere la posibilidad de utilizar varias directivas para garantizar que las reglas se aplican de manera precisa. Dicho esto, AEM as a Cloud Service elimina el encabezado de la caché si detecta que Dispatcher lo ha aplicado a lo que detecta que no se puede almacenar en caché, tal como se describe en la documentación de Dispatcher. Para obligar a AEM a aplicar siempre los encabezados de almacenamiento en caché, se puede agregar la opción **`always`** de la siguiente manera:

  ```
  <LocationMatch "^/content/.*\.(html)$">
       Header unset Cache-Control
       Header unset Expires
       Header always set Cache-Control "max-age=200"
       Header set Age 0
  </LocationMatch>
  ```

  Asegúrese de que un archivo de `src/conf.dispatcher.d/cache` tenga la siguiente regla (que se encuentra en la configuración predeterminada):

  ```
  /0000
  { /glob "*" /type "allow" }
  ```

* Para evitar que contenido específico se almacene en caché **en la red de distribución de contenido (CDN)**, establezca el encabezado Cache-Control en *private*. Por ejemplo, lo siguiente impediría que el contenido html de un directorio llamado **secure** se almacenara en la caché en la CDN:

  ```
     <LocationMatch "/content/secure/.*\.(html)$">.  // replace with the right regex
     Header unset Cache-Control
     Header unset Expires
     Header always set Cache-Control "private"
    </LocationMatch>
  ```

* Aunque el contenido de HTML establecido en privado no se almacena en caché en la red de distribución de contenido (CDN), se puede almacenar en caché en Dispatcher si se ha configurado [Almacenamiento en caché con permisos confidenciales](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=es), lo que garantiza que solo se pueda proporcionar el contenido a los usuarios autorizados.

  >[!NOTE]
  >Los otros métodos, incluido el [proyecto Dispatcher-ttl AEM ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), no invalidan correctamente los valores.

  >[!NOTE]
  >Es posible que Dispatcher siga almacenando en caché el contenido según sus propias [reglas de almacenamiento en caché](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17497.html?lang=es). Para que el contenido sea verdaderamente privado, asegúrese de que Dispatcher no lo almacene en caché.

### Bibliotecas del lado cliente (js,css) {#client-side-libraries}

* Al utilizar el marco de trabajo de biblioteca del lado del cliente de AEM, el código JavaScript y CSS se genera de tal manera que los exploradores pueden almacenarlo en caché indefinidamente, ya que cualquier cambio se manifiesta como nuevos archivos con una ruta única. En otras palabras, las HTML que hacen referencia a las bibliotecas de cliente se generan según sea necesario para que los clientes puedan experimentar el nuevo contenido a medida que se publica. El control de caché se establece en &quot;inmutable&quot; o 30 días para exploradores más antiguos que no respetan el valor &quot;inmutable&quot;.
* consulte la sección [Bibliotecas del lado del cliente y coherencia de la versión](#content-consistency) para obtener más información.

### Las imágenes y cualquier contenido lo suficientemente grande como para almacenarse en el almacenamiento de blobs {#images}

El comportamiento predeterminado de los programas creados después de mediados de mayo de 2022 (específicamente, para los ID de programa superiores a 65000) es almacenar en caché de forma predeterminada, respetando también el contexto de autenticación de la solicitud. Los programas más antiguos (ID de programa iguales o inferiores a 65000) no almacenan en caché el contenido del blob de forma predeterminada.

En ambos casos, los encabezados de almacenamiento en caché se pueden anular en un nivel de granulado más preciso en la capa de Apache/Dispatcher mediante las directivas de Apache `mod_headers`, por ejemplo:

```
   <LocationMatch "^/content/.*\.(jpeg|jpg)$">
     Header set Cache-Control "max-age=222"
     Header set Age 0
   </LocationMatch>
```

Al modificar los encabezados de almacenamiento en caché en la capa de Dispatcher, tenga cuidado de no almacenar en caché demasiado ampliamente. Consulte la discusión en la sección HTML/text [más arriba](#html-text). Además, asegúrese de que los recursos que se pretende mantener privados (en lugar de almacenados en caché) no formen parte de los filtros de directiva `LocationMatch`.

Los recursos JCR (superiores a 16 KB) almacenados en el almacén de blobs generalmente se sirven como redirecciones 302 mediante AEM. Estas redirecciones son interceptadas y seguidas por CDN y el contenido se entrega directamente desde el almacén de blobs. En estas respuestas solo se puede personalizar un conjunto limitado de encabezados. Por ejemplo, para personalizar `Content-Disposition` debe usar las directivas de Dispatcher de la siguiente manera:

```
<LocationMatch "\.(?i:pdf)$">
  ForceType application/pdf
  Header set Content-Disposition inline
  </LocationMatch>
```

La lista de encabezados que se pueden personalizar en las respuestas de blob es la siguiente:

```
content-security-policy
x-frame-options
x-xss-protection
x-content-type-options
x-robots-tag
access-control-allow-origin
content-disposition
permissions-policy
referrer-policy
x-vhost
content-disposition
cache-control
vary
```

#### Nuevo comportamiento de almacenamiento en caché predeterminado {#new-caching-behavior}

La capa de AEM establece los encabezados de caché en función de si ya se ha establecido el encabezado de caché y el valor del tipo de solicitud. Si no se establece ningún encabezado de control de caché, el contenido público se almacena en caché y el tráfico autenticado se establece en privado. Si se establece un encabezado de control de caché, los encabezados de caché no se tocan.

| ¿Existe el encabezado de control de caché? | Tipo de solicitud | AEM establece los encabezados de caché en |
|------------------------------|---------------|------------------------------------------------|
| No | público | Cache-Control: public, max-age=600, inmutable |
| No | autenticado | Cache-Control: private, max-age=600, inmutable |
| Sí | cualquiera | sin modificar |

Aunque no se recomienda, es posible cambiar el nuevo comportamiento predeterminado para seguir el comportamiento anterior (ID de programa iguales o inferiores a 65000) estableciendo la variable de entorno de Cloud Manager `AEM_BLOB_ENABLE_CACHING_HEADERS` en false.

#### Comportamiento de almacenamiento en caché predeterminado anterior {#old-caching-behavior}

La capa de AEM no almacena en caché el contenido del blob de forma predeterminada.

>[!NOTE]
>Cambie el comportamiento predeterminado anterior para que sea coherente con el nuevo comportamiento (ID de programa superiores a 65000) estableciendo la variable de entorno de Cloud Manager AEM_BLOB_ENABLE_CACHING_HEADERS en true. Si el programa ya está activo, asegúrese de verificar que después de los cambios, el contenido se comporta como espera.

Ahora, las imágenes en el almacenamiento del blob marcadas como privadas no se pueden almacenar en caché en Dispatcher usando [Almacenamiento en caché con permisos confidenciales](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=es). La imagen siempre se solicita desde el origen de AEM y se sirve si el usuario está autorizado.

>[!NOTE]
>Los otros métodos, incluido el [proyecto Dispatcher-ttl AEM ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), no anulan correctamente los valores.

### Otros tipos de archivo de contenido en el almacén de nodos {#other-content}

* sin almacenamiento en caché predeterminado
* no se puede establecer el valor predeterminado con la variable `EXPIRATION_TIME` utilizada para los tipos de archivo html/text
* la caducidad de la caché se puede establecer con la misma estrategia de LocationMatch descrita en la sección html/text especificando la regex adecuada

### Optimizaciones adicionales {#further-optimizations}

* Evite usar `User-Agent` como parte del encabezado `Vary`. Las versiones anteriores de la configuración predeterminada de Dispatcher (antes de la versión 28 del tipo de archivo) la incluían y Adobe recomienda eliminarla siguiendo los pasos a continuación.
   * Busque los archivos vhost en `<Project Root>/dispatcher/src/conf.d/available_vhosts/*.vhost`
   * Elimine o comente la línea: `Header append Vary User-Agent env=!dont-vary` de todos los archivos vhost, excepto default.vhost, que es de solo lectura
* Utilice el encabezado `Surrogate-Control` para controlar el almacenamiento en caché de CDN de forma independiente del almacenamiento en caché del explorador
* Considere la posibilidad de aplicar las directivas [`stale-while-revalidate`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-while-revalidate) y [`stale-if-error`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-if-error) para permitir la actualización en segundo plano y evitar errores de caché, con lo que el contenido se mantendrá actualizado y rápido para los usuarios.
   * Hay muchas maneras de aplicar estas directivas, pero agregar un objeto `stale-while-revalidate` de 30 minutos a todos los encabezados de control de caché es un buen punto de partida.
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

   * Almacene en caché las páginas de HTML durante cinco minutos con la actualización en segundo plano una hora en el explorador y 12 horas en CDN. Los encabezados Cache-Control siempre se agregan, por lo que es importante asegurarse de que las páginas HTML coincidentes en /content/* están pensadas para ser públicas. Si no es así, considere la posibilidad de utilizar una regex más específica.

     ```
     <LocationMatch "^/content/.*\.html$">
        Header unset Cache-Control
        Header always set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
        Header always set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

   * Almacene en caché las respuestas json del exportador de servicios de contenido/modelo Sling durante cinco minutos con una actualización en segundo plano una hora en el explorador y 12 horas en CDN.

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

   * Almacene en caché los recursos mutables de DAM, como imágenes y vídeo, durante 24 horas y actualice en segundo plano después de 12 horas para evitar errores.

     ```
     <LocationMatch "^/content/dam/.*\.(?i:jpe?g|gif|js|mov|mp4|png|svg|txt|zip|ico|webp|pdf)$">
        Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

### Análisis de la proporción de visitas de caché de CDN {#analyze-chr}

Consulte el [tutorial de análisis de proporción de aciertos de caché](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/caching/cdn-cache-hit-ratio-analysis.html?lang=es) para obtener información sobre cómo descargar registros de CDN y analizar la proporción de blancos de caché del sitio mediante un tablero.

### Comportamiento de petición HEAD {#request-behavior}

Cuando se recibe una solicitud de HEAD en la CDN de Adobe para un recurso que está en caché **no**, la solicitud se transforma y la recibe la instancia de Dispatcher o AEM como una solicitud de GET. Si la respuesta se puede almacenar en caché, las solicitudes de HEAD posteriores se proporcionan desde la CDN. Si la respuesta no se puede almacenar en caché, las solicitudes de HEAD posteriores se pasan a la instancia de Dispatcher, AEM o ambas, durante un tiempo que depende del TTL `Cache-Control`.

### Parámetros de campaña de marketing {#marketing-parameters}

Las direcciones URL del sitio web suelen incluir parámetros de campañas de marketing que se utilizan para realizar el seguimiento del éxito de una campaña.

En el caso de los entornos creados en octubre de 2023 o posterior, para almacenar en caché mejor las solicitudes, la CDN eliminará los parámetros de consulta comunes relacionados con el marketing, específicamente los que coinciden con el siguiente patrón regex:

```
^(utm_.*|gclid|gdftrk|_ga|mc_.*|trk_.*|dm_i|_ke|sc_.*|fbclid|msclkid|ttclid)$
```

Esta funcionalidad se puede activar y desactivar mediante el indicador `requestTransformations` en la [configuración de CDN](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#request-transformations).

Por ejemplo, para detener la eliminación de parámetros de marketing en el nivel CDN, uno debe implementar `removeMarketingParams: false` mediante una configuración que contenga la siguiente sección.

```
kind: "CDN"
version: "1"
data:
  requestTransformations:
    removeMarketingParams: false
```

En caso de que la funcionalidad `removeMarketingParams` esté deshabilitada en el nivel CDN, se recomienda configurar la propiedad `ignoreUrlParams` de la configuración de Dispatcher; consulte [Configuración de Dispatcher: omitiendo parámetros de URL](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=es#ignoring-url-parameters).

Existen dos formas de ignorar los parámetros de marketing. (Donde se prefiere el primero para ignorar la eliminación de caché mediante parámetros de consulta):

1. Ignore todos los parámetros y permita selectivamente los parámetros utilizados.
En el ejemplo siguiente, solo no se omiten los parámetros `page` y `product`, y las solicitudes se reenviarán al editor.

```
/ignoreUrlParams {
   /0001 { /glob "*" /type "allow" }
   /0002 { /glob "page" /type "deny" }
   /0003 { /glob "product" /type "deny" }
}
```

1. Permitir todos los parámetros excepto los de marketing. El archivo [marketing_query_parameters.any](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/dispatcher.cloud/src/conf.dispatcher.d/cache/marketing_query_parameters.any) define una lista de parámetros de marketing que se omitirán y que se utilizarán con frecuencia. Adobe no actualizará este archivo. Los usuarios pueden ampliarla en función de sus proveedores de marketing.

```
/ignoreUrlParams {
   /0001 { /glob "*" /type "deny" }
   $include "../cache/marketing_query_parameters.any"
}
```


## Invalidación de caché de Dispatcher {#disp}

En general, no es necesario invalidar la caché de Dispatcher. En su lugar, debe confiar en que Dispatcher actualizará su caché cuando se vuelva a publicar el contenido y en que la CDN respete los encabezados de caducidad de la caché.

### Invalidación de la caché de Dispatcher durante la activación/desactivación {#cache-activation-deactivation}

Al igual que las versiones anteriores de AEM, la publicación o cancelación de la publicación de páginas borra el contenido de la caché de Dispatcher. Si se sospecha un problema de almacenamiento en caché, debe volver a publicar las páginas en cuestión y asegurarse de que haya un host virtual disponible que coincida con el host local `ServerAlias`, que es necesario para invalidar la caché de Dispatcher.

>[!NOTE]
>Para la correcta invalidación de Dispatcher, asegúrese de que las solicitudes de &quot;127.0.0.1&quot;, &quot;localhost&quot;, &quot;\*.local&quot;, &quot;\*.adobeaemcloud.com&quot; y &quot;\*.adobeaemcloud.net&quot; coincidan y se gestionen mediante una configuración de vhost para que se pueda atender la solicitud. Puede realizar esta tarea haciendo coincidir globalmente &quot;*&quot; en una configuración de vhost global siguiendo el patrón de la referencia [arquetipo de AEM](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/dispatcher.cloud/src/conf.d/available_vhosts/default.vhost). O bien, puede asegurarse de que la lista mencionada anteriormente sea capturada por uno de los vhosts.

Cuando la instancia de publicación recibe una nueva versión de una página o recurso del autor, utiliza el agente de vaciado para invalidar las rutas adecuadas en su Dispatcher. La ruta actualizada se quita de la caché de Dispatcher, junto con sus elementos primarios, hasta un nivel (puede configurar este nivel con [statfileslevel](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=es#invalidating-files-by-folder-level)).

## Invalidación explícita de la caché de Dispatcher {#explicit-invalidation}

Adobe recomienda confiar en los encabezados de caché estándar para controlar el ciclo de vida de la entrega de contenido. Sin embargo, si es necesario, es posible invalidar el contenido directamente en Dispatcher.

La siguiente lista contiene escenarios en los que puede que desee invalidar explícitamente la caché (mientras escucha opcionalmente la finalización de la invalidación):

* Después de publicar contenido, como fragmentos de experiencias o fragmentos de contenido, invalide el contenido publicado y almacenado en caché que hace referencia a esos elementos.
* Notificar a un sistema externo cuando se han invalidado correctamente las páginas a las que se hace referencia.

Existen dos métodos para invalidar explícitamente la caché:

* El método preferido es usar Sling Content Distribution (SCD) de Author.
* El otro método es utilizar la API de replicación para invocar el agente de replicación de vaciado de Dispatcher de publicación.

Los enfoques difieren en términos de disponibilidad de niveles, la capacidad de deduplicar eventos y la garantía de procesamiento de eventos. La tabla siguiente resume estas opciones:

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>N/A</th>
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
    <td>Es posible mediante la API de detección o habilitando el <a href="https://github.com/apache/sling-org-apache-sling-distribution-journal/blob/e18f2bd36e8b43814520e87bd4999d3ca77ce8ca/src/main/java/org/apache/sling/distribution/journal/impl/publisher/DistributedEventNotifierManager.java#L146-L149">modo de deduplicación</a>.</td>
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
       <li><p><strong>Del nivel de Author</strong>: elimina el contenido e invalida la caché (si se activa desde el nivel de Author de AEM en el agente de publicación).</p>
           <p><strong>Desde nivel de publicación</strong>: invalida solamente la caché (si se activa desde el nivel de publicación de AEM en el agente de vaciado o de vaciado solo de recursos).</p>
       </li>
     </ol>
     </td>
  </tr>
  </tbody>
</table>

Las dos acciones directamente relacionadas con la invalidación de la caché son Invalidación de la API de Sling Content Distribution (SCD) y Desactivación de la API de replicación.

Además, desde la tabla, puede observar lo siguiente:

* La API de SCD es necesaria cuando se debe garantizar cada evento, por ejemplo, la sincronización con un sistema externo que requiera un conocimiento preciso. Si hay un evento de actualización del nivel de publicación en el momento de la llamada de invalidación, se genera un evento adicional cuando cada nueva publicación procesa la invalidación.

* El uso de la API de replicación no es un caso de uso común, pero se puede utilizar en casos en los que la déclencheur para invalidar la caché proviene del nivel de publicación y no del de creación. Este método puede resultar útil si se ha configurado el TTL de Dispatcher.

En resumen, si desea invalidar la caché de Dispatcher, la opción recomendada es utilizar la acción Invalidar la API de SCD del autor. Además, también puede escuchar el evento para poder almacenar en déclencheur más acciones descendentes.

### Sling Content Distribution (SCD) {#sling-distribution}

>[!NOTE]
>Cuando utilice las instrucciones presentadas a continuación, pruebe el código personalizado en un entorno de desarrollo de AEM Cloud Service y no localmente.

Al utilizar la acción SCD de Autor, el patrón de implementación es el siguiente:

1. Desde Autor, escriba código personalizado para invocar la distribución de contenido de sling [API](https://sling.apache.org/documentation/bundles/content-distribution.html), pasando la acción de invalidación con una lista de rutas:

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

* (Opcionalmente) Ejecute la lógica empresarial en el método `invalidated(String[] paths, String packageId)` anterior.

>[!NOTE]
>
>La CDN de Adobe no se vacía cuando se invalida Dispatcher. La CDN administrada por Adobe respeta los TTL y, por lo tanto, no es necesario vaciarla.

### API de replicación {#replication-api}

A continuación se muestra el patrón de implementación al utilizar la acción de desactivación de la API de replicación:

1. En el nivel de publicación, llame a la API de replicación para almacenar en déclencheur el agente de replicación de vaciado de Dispatcher de publicación.

El extremo del agente de vaciado no se puede configurar, sino que está preconfigurado para indicar Dispatcher, lo que coincide con el servicio de publicación que se ejecuta junto con el agente de vaciado.

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
>The dispatcher's `invalidate.cache` API approach will no longer be supported since it addresses only a specific dispatcher node. AEM as a Cloud Service operates at the service level, not the individual node level and so the invalidation instructions in the [Invalidating Cached Pages From AEM](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=es) page are not longer valid for AEM as a Cloud Service.

The replication flush agent should be used. This can be done using the [Replication API](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/replication/Replicator.html). The flush agent endpoint is not configurable but pre-configured to point to the dispatcher, matched with the publish service running the flush agent. The flush agent can typically be triggered by OSGi events or workflows.

<!-- Need to find a new link and/or example -->
<!-- 
and for an example of flushing the cache, see the [API example page](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) (specifically the `CustomStep` example issuing a replication action of type ACTIVATE to all available agents). 

The diagram presented below illustrates this.

![CDN](assets/cdnd.png "CDN")

If there is a concern that the dispatcher cache is not clearing, contact [customer support](https://helpx.adobe.com/es/support.ec.html) who can flush the dispatcher cache if necessary.

The Adobe-managed CDN respects TTLs and thus there is no need fo it to be flushed. If an issue is suspected, [contact customer support](https://helpx.adobe.com/es/support.ec.html) support who can flush an Adobe-managed CDN cache as necessary. -->

## Bibliotecas del lado del cliente y coherencia de versiones {#content-consistency}

Las páginas están compuestas por HTML, JavaScript, CSS e imágenes. Se recomienda a los clientes que usen el [marco de bibliotecas del lado del cliente (clientlibs)](/help/implementing/developing/introduction/clientlibs.md) para importar recursos de JavaScript y CSS en páginas de HTML, teniendo en cuenta las dependencias entre bibliotecas JS.

El marco clientlibs proporciona administración automática de versiones. Esto significa que los desarrolladores pueden proteger los cambios realizados en las bibliotecas JS del control de código fuente y la versión más reciente estará disponible cuando un cliente publique su versión. Sin este flujo de trabajo, los desarrolladores deben cambiar manualmente HTML con referencias a la nueva versión de la biblioteca, lo que resulta especialmente oneroso si la misma biblioteca comparte muchas plantillas de HTML.

Cuando salen al mercado las nuevas versiones de las bibliotecas de, las páginas de referencia de HTML se actualizan con nuevos vínculos a esas versiones de biblioteca actualizadas. Una vez que la caché del explorador caduca para una página de HTML determinada, no preocupa que las bibliotecas antiguas se carguen desde la caché del explorador. El motivo es que ahora se garantiza que la página actualizada (de AEM) hace referencia a las nuevas versiones de las bibliotecas. Es decir, una página de HTML actualizada incluye todas las versiones de biblioteca más recientes.

El mecanismo detrás de esta capacidad es un hash serializado, que se anexa al vínculo de biblioteca del cliente. Garantiza una URL única con versiones para que el explorador almacene en caché el CSS/JS. El hash serializado solo se actualiza cuando cambia el contenido de la biblioteca de cliente. Lo que significa que si se producen actualizaciones no relacionadas (es decir, no se producen cambios en el css/js subyacente de la biblioteca del cliente) incluso con una nueva implementación, la referencia sigue siendo la misma. A su vez, garantiza menos interrupciones en la caché del explorador.

### Activación de las versiones de caché larga de las bibliotecas del lado del cliente: inicio rápido de AEM as a Cloud Service SDK {#enabling-longcache}

Las inclusiones clientlib predeterminadas en una página de HTML tienen el siguiente aspecto:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.css" type="text/css">
```

Cuando se habilita el control de versiones de clientlib estricto, se agrega una clave hash a largo plazo como selector a la biblioteca de cliente. Como resultado, la referencia clientlib tiene este aspecto:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.lc-7c8c5d228445ff48ab49a8e3c865c562-lc.css" type="text/css">
```

Las versiones de clientlib estrictas están habilitadas de forma predeterminada en todos los entornos de AEM as a Cloud Service.

Para habilitar las versiones clientlib estrictas en el Quickstart de SDK local, haga lo siguiente:

1. Vaya al Administrador de configuración de OSGi `<host>/system/console/configMgr`
1. Busque la configuración OSGi para el administrador de bibliotecas de Adobe Granite HTML:
   * Marque la casilla de verificación para habilitar las versiones estrictas.
   * En el campo etiquetado **Clave de caché de cliente a largo plazo**, escriba el valor de /.*;hash
1. Guarde los cambios. No es necesario guardar esta configuración en el control de código fuente, ya que AEM as a Cloud Service la habilita automáticamente en los entornos de desarrollo, fase y producción.
1. Cada vez que se cambia el contenido de la biblioteca de cliente, se genera una nueva clave hash y se actualiza la referencia de HTML.
