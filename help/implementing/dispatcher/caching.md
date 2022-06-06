---
title: Almacenamiento en caché en AEM as a Cloud Service
description: 'Almacenamiento en caché en AEM as a Cloud Service '
feature: Dispatcher
exl-id: 4206abd1-d669-4f7d-8ff4-8980d12be9d6
source-git-commit: 91a88cb02192defdd651ecb6d108d4540186d06e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Introducción {#intro}

El tráfico pasa a través de la CDN a una capa de servidor web Apache, que admite módulos, incluido el Dispatcher. Para aumentar el rendimiento, Dispatcher se utiliza principalmente como caché para limitar el procesamiento en los nodos de publicación.
Se pueden aplicar reglas a la configuración de Dispatcher para modificar cualquier configuración de caducidad de caché predeterminada, lo que resulta en el almacenamiento en caché en la CDN. Tenga en cuenta que Dispatcher también respeta los encabezados de caducidad de caché resultantes si `enableTTL` está habilitado en la configuración de Dispatcher, lo que implica que actualizará contenido específico incluso fuera del contenido que se está republicando.

Esta página también describe cómo se invalida la caché de Dispatcher, así como cómo funciona el almacenamiento en caché a nivel de explorador con respecto a las bibliotecas del lado del cliente.

## Almacenamiento en caché {#caching}

### HTML/Texto {#html-text}

* de forma predeterminada, el explorador lo almacena en caché durante cinco minutos, en función de la variable `cache-control` encabezado emitido por la capa de Apache. La CDN también respeta este valor.
* la configuración predeterminada de almacenamiento en caché de HTML/texto se puede deshabilitar definiendo la variable `DISABLE_DEFAULT_CACHING` en `global.vars`:

```
Define DISABLE_DEFAULT_CACHING
```

Esto puede resultar útil, por ejemplo, cuando la lógica empresarial requiere un ajuste preciso del encabezado de la página (con un valor basado en el día del calendario), ya que de forma predeterminada el encabezado de la página está establecido en 0. Dicho esto, **tenga cuidado al desactivar el almacenamiento en caché predeterminado.**

* se puede anular para todo el contenido de texto o HTML definiendo la variable `EXPIRATION_TIME` en `global.vars` uso de las AEM herramientas as a Cloud Service de SDK Dispatcher.
* se puede sobrescribir en un nivel más preciso, incluido el control de la CDN y la caché del navegador de forma independiente, con las siguientes directivas apache mod_headers :

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header set Cache-Control "max-age=200"
        Header set Surrogate-Control "max-age=3600"
        Header set Age 0
   </LocationMatch>
   ```

   >[!NOTE]
   >El encabezado Surrogate-Control se aplica a la CDN administrada por Adobe. Si utiliza un [CDN gestionada por el cliente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html?lang=en#point-to-point-CDN), es posible que se requiera un encabezado diferente en función de su proveedor de CDN.

   Tenga cuidado al configurar los encabezados de control de caché globales o los que coinciden con un regex amplio para que no se apliquen a contenido que pueda tener la intención de mantener privado. Considere la posibilidad de utilizar varias directivas para garantizar que las reglas se apliquen de forma precisa. Dicho esto, AEM as a Cloud Service eliminará el encabezado de la caché si detecta que se ha aplicado a lo que detecta que es inaccesible para Dispatcher, como se describe en la documentación de Dispatcher. Para obligar a los AEM a aplicar siempre los encabezados de almacenamiento en caché, se puede añadir la variable **always** como se indica a continuación:

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

   >[!NOTE]
   >Los demás métodos, incluido el [dispatcher-ttl AEM proyecto ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), no anulará correctamente los valores.

   >[!NOTE]
   >Tenga en cuenta que Dispatcher puede seguir almacenando en caché el contenido según su propio [reglas de almacenamiento en caché](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17497.html). Para que el contenido sea realmente privado, debe asegurarse de que Dispatcher no lo almacene en caché.

### Bibliotecas de cliente (js, css) {#client-side-libraries}

* al utilizar AEM marco de biblioteca del lado del cliente, el código JavaScript y CSS se generan de forma que los navegadores puedan almacenarlo en caché indefinidamente, ya que cualquier cambio se manifiesta como nuevos archivos con una ruta única.  En otras palabras, el HTML que hace referencia a las bibliotecas del cliente se producirá según sea necesario para que los clientes puedan experimentar contenido nuevo a medida que se publique. El control de caché se establece en &quot;inmutable&quot; o 30 días para los exploradores más antiguos que no respetan el valor &quot;inmutable&quot;.
* consulte la sección [Bibliotecas del lado del cliente y coherencia de la versión](#content-consistency) para obtener más información.

### Imágenes y cualquier contenido lo suficientemente grande como para almacenarse en blob. {#images}

El comportamiento predeterminado para los programas creados después de mediados de mayo de 2022 (específicamente, para los id de programa superiores a 65000) es almacenar en caché de forma predeterminada, respetando al mismo tiempo el contexto de autenticación de la solicitud. Los programas más antiguos (id de programa iguales o inferiores a 65000) no almacenan en caché el contenido del blob de forma predeterminada.

En ambos casos, los encabezados de almacenamiento en caché se pueden sobrescribir en un nivel granulado más preciso en la capa apache/dispatcher mediante el uso de apache `mod_headers` directivas, por ejemplo:

```
   <LocationMatch "^/content/.*\.(jpeg|jpg)$">
     Header set Cache-Control "max-age=222"
     Header set Age 0
   </LocationMatch>
```

Al modificar los encabezados de almacenamiento en caché en la capa de Dispatcher, tenga cuidado de no almacenar en caché demasiado ampliamente, vea la discusión en la sección HTML/texto [above](#html-text). Además, asegúrese de que los recursos que están destinados a ser guardados en privado (en lugar de en caché) no formen parte del `LocationMatch` filtros de directiva.

#### Nuevo comportamiento predeterminado de almacenamiento en caché {#new-caching-behavior}

La capa AEM establecerá los encabezados de caché en función de si el encabezado de caché ya se ha establecido y el valor del tipo de solicitud. Tenga en cuenta que si no se ha establecido ningún encabezado de control de caché, el contenido público se almacena en caché y el tráfico autenticado se establece en privado. Si se ha establecido un encabezado de control de caché, los encabezados de caché no se tocarán.

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

Cuando se recibe una solicitud de HEAD en la CDN de Adobe para un recurso que **not** en la caché, la solicitud se transforma y se recibe mediante la instancia de Dispatcher o AEM como una solicitud de GET. Si la respuesta se puede almacenar en caché, las solicitudes de HEAD posteriores se servirán desde la CDN. Si la respuesta no se puede almacenar en caché, las solicitudes de HEAD subsiguientes se pasarán a la instancia de Dispatcher o AEM durante un período de tiempo que depende de la variable `Cache-Control` TTL.

## Invalidación de caché de Dispatcher {#disp}

En general, no es necesario invalidar la caché de Dispatcher. En su lugar, debe confiar en que Dispatcher actualice su caché cuando el contenido se esté republicando y la CDN respete los encabezados de caducidad de la caché.

### Invalidación de caché de Dispatcher durante la activación/desactivación {#cache-activation-deactivation}

Al igual que las versiones anteriores de AEM, la publicación o cancelación de la publicación de páginas borrará el contenido de la caché de Dispatcher. Si se sospecha un problema de almacenamiento en caché, los clientes deben volver a publicar las páginas en cuestión y asegurarse de que haya un host virtual disponible que coincida con el host local de ServerAlias, que es necesario para la invalidación de la caché de Dispatcher.


Cuando la instancia de publicación recibe una nueva versión de una página o recurso del autor, utiliza el agente de vaciado para invalidar las rutas adecuadas en su despachante. La ruta actualizada se elimina de la caché de Dispatcher, junto con sus principales, hasta un nivel (puede configurarla con el [statfileslevel](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level)).

### Invalidación explícita de caché de Dispatcher {#explicit-invalidation}

En general, no es necesario invalidar manualmente el contenido en Dispatcher, pero es posible si es necesario.

>[!NOTE]
>Antes de AEM as a Cloud Service, había dos formas de invalidar la caché de Dispatcher.
>
>1. Invocar el agente de replicación, especificando el agente de vaciado del despachante de publicación
>2. Llamando directamente a la función `invalidate.cache` API (por ejemplo, `POST /dispatcher/invalidate.cache`)

>
>El de Dispatcher `invalidate.cache` Ya no se admitirá el enfoque de API, ya que se dirige únicamente a un nodo de Dispatcher específico. AEM as a Cloud Service funciona en el nivel de servicio, no en el nivel de nodo individual y, por lo tanto, las instrucciones de invalidación de la variable [Invalidación de páginas en caché de AEM](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html) La página ya no es válida para AEM as a Cloud Service.

Se debe utilizar el agente de vaciado de replicación. Esto se puede hacer utilizando la variable [API de replicación](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/replication/Replicator.html). El extremo del agente de vaciado no se puede configurar, pero está preconfigurado para apuntar al despachante, coincide con el servicio de publicación que ejecuta el agente de vaciado. Normalmente, el agente de vaciado se puede activar mediante eventos o flujos de trabajo OSGi.

<!-- Need to find a new link and/or example -->
<!-- 
and for an example of flushing the cache, see the [API example page](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) (specifically the `CustomStep` example issuing a replication action of type ACTIVATE to all available agents). 
-->

El diagrama que se muestra a continuación ilustra esto.

![CDN](assets/cdnd.png "CDN")

Si existe preocupación de que la caché de Dispatcher no se esté borrando, póngase en contacto con [asistencia al cliente](https://helpx.adobe.com/support.ec.html) quién puede vaciar la caché de Dispatcher si es necesario.

La CDN administrada por Adobe respeta los TTL y, por lo tanto, no es necesario vaciarla. Si se sospecha un problema, [póngase en contacto con el servicio de atención al cliente](https://helpx.adobe.com/support.ec.html) admiten quién puede vaciar una caché de CDN administrada por Adobe según sea necesario.

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
1. Guarde los cambios. Tenga en cuenta que no es necesario guardar esta configuración en el control de código fuente, ya que AEM as a Cloud Service habilitará automáticamente esta configuración en entornos de desarrollo, fase y producción.
1. Cada vez que se cambia el contenido de la biblioteca del cliente, se genera una nueva clave hash y se actualiza la referencia del HTML.
