---
title: Almacenamiento en caché en AEM as a Cloud Service
description: 'Almacenamiento en caché en AEM as a Cloud Service '
translation-type: tm+mt
source-git-commit: 0e414de936267cb4648c3078720b198e00c4a3cb
workflow-type: tm+mt
source-wordcount: '1479'
ht-degree: 1%

---


# Introducción {#intro}

El tráfico pasa a través de la CDN a una capa de servidor web apache, que admite módulos, incluido el despachante. Para aumentar el rendimiento, el despachante se utiliza principalmente como caché para limitar el procesamiento en los nodos de publicación.
Se pueden aplicar reglas a la configuración del despachante para modificar cualquier configuración de caducidad de caché predeterminada, lo que resulta en almacenamiento en caché en CDN. Tenga en cuenta que el despachante también respeta los encabezados de caducidad de caché resultantes si `enableTTL` está habilitado en la configuración del despachante, lo que implica que actualizará contenido específico incluso fuera del contenido que se está republicando.

En esta página también se describe cómo se invalida la caché del despachante, así como cómo funciona la caché a nivel del explorador con respecto a las bibliotecas del lado del cliente.

## Almacenamiento en caché {#caching}

### HTML/Texto {#html-text}

* de forma predeterminada, el explorador almacena en caché durante cinco minutos, según el encabezado de control de caché emitido por la capa apache. La CDN también respeta este valor.
* se puede anular para todo el contenido HTML/Texto definiendo la variable `EXPIRATION_TIME` en `global.vars` mediante el uso de la AEM como herramienta de Dispatcher de SDK para Cloud Service.
* se puede anular en un nivel más fino mediante las siguientes directivas apache mod_headers:

   ```
   <LocationMatch "\.(html)$">
        Header set Cache-Control "max-age=200"
        Header set Age 0
   </LocationMatch>
   ```

   Tenga cuidado al configurar encabezados de control de caché globales o aquéllos que coinciden con un regex amplio, de modo que no se apliquen al contenido que pueda tener la intención de mantener como privado. Considere la posibilidad de utilizar varias directivas para garantizar que las reglas se apliquen de manera precisa. Dicho esto, AEM como Cloud Service quitará el encabezado de la memoria caché si detecta que se ha aplicado a lo que detecta que el despachante no puede almacenar en caché, tal como se describe en la documentación del despachante. Para obligar a AEM a aplicar siempre almacenamiento en caché, se puede agregar la opción &quot;siempre&quot; de la siguiente manera:

   ```
   <LocationMatch "\.(html)$">
        Header always set Cache-Control "max-age=200"
        Header set Age 0
   </LocationMatch>
   ```

   Debe asegurarse de que un archivo de `src/conf.dispatcher.d/cache` tiene la siguiente regla (que está en la configuración predeterminada):

   ```
   /0000
   { /glob "*" /type "allow" }
   ```

* Para evitar que se almacene en caché contenido específico, establezca el encabezado Cache-Control en *private*. Por ejemplo, lo siguiente impediría que el contenido HTML de un directorio llamado **myfolder** se almacene en caché:

   ```
      <LocationMatch "/myfolder/.*\.(html)$">.  // replace with the right regex
      Header set Cache-Control “private”
     </LocationMatch>
   ```

   >[!NOTE]
   >Los demás métodos, incluido el proyecto [dispatcher-ttl AEM ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), no anularán correctamente los valores.

### Bibliotecas de cliente (js,css) {#client-side-libraries}

* al utilizar AEM marco de biblioteca del cliente, el código JavaScript y CSS se genera de forma que los navegadores pueden almacenarlo en caché indefinidamente, ya que cualquier cambio se manifiesta como nuevos archivos con una ruta única.  En otras palabras, el HTML que hace referencia a las bibliotecas de cliente se producirá según sea necesario para que los clientes puedan experimentar contenido nuevo a medida que se publica. El control de caché se establece en &quot;inmutable&quot; o en 30 días para los exploradores más antiguos que no respetan el valor &quot;inmutable&quot;.
* consulte la sección [Bibliotecas del lado del cliente y coherencia de la versión](#content-consistency) para obtener más detalles.

### Imágenes y cualquier contenido lo suficientemente grande almacenado en el almacenamiento de blob {#images}

* de forma predeterminada, no en caché
* puede establecerse en un nivel más fino mediante las siguientes directivas apache `mod_headers`:

   ```
      <LocationMatch "^\.*.(jpeg|jpg)$">
        Header set Cache-Control "max-age=222"
        Header set Age 0
      </LocationMatch>
   ```

   Consulte la discusión en la sección html/text de arriba para tener cuidado de no almacenar demasiado en caché y también para forzar a AEM a aplicar siempre la caché con la opción &quot;siempre&quot;.

   Es necesario asegurarse de que un archivo en `src/conf.dispatcher.d/`caché tiene la siguiente regla (que se encuentra en la configuración predeterminada):

   ```
   /0000
   { /glob "*" /type "allow" }
   ```

   Asegúrese de que los recursos destinados a ser guardados en privado en lugar de en caché no forman parte de los filtros de directiva LocationMatch.

   >[!NOTE]
   >Los demás métodos, incluido el proyecto [dispatcher-ttl AEM ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), no anularán correctamente los valores.

### Otros tipos de archivos de contenido en el almacén de nodos {#other-content}

* sin caché predeterminada
* el valor predeterminado no se puede establecer con la variable `EXPIRATION_TIME` utilizada para los tipos de archivo html/text
* la caducidad de la caché se puede establecer con la misma estrategia LocationMatch descrita en la sección html/text especificando el regex adecuado

## Invalidación de caché de despachante {#disp}

En general, no será necesario invalidar la caché del despachante. En su lugar, debe confiar en que el despachante actualice su caché cuando se vuelva a publicar el contenido y en que la CDN respete los encabezados de caducidad de la caché.

### Invalidación de caché de despachante durante la Activación/desactivación {#cache-activation-deactivation}

Al igual que las versiones anteriores de AEM, las páginas de publicación o cancelación de publicación borrarán el contenido de la caché del despachante. Si se sospecha un problema de almacenamiento en caché, los clientes deben volver a publicar las páginas en cuestión.

Cuando la instancia de publicación recibe una nueva versión de una página o recurso del autor, utiliza el agente de vaciado para invalidar las rutas adecuadas en su distribuidor. La ruta de acceso actualizada se elimina de la memoria caché del despachante, junto con sus elementos principales, hasta un nivel (puede configurarla con el [nivel de archivo de estado](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level).

### Invalidez de caché de despachante explícita {#explicit-invalidation}

En general, no será necesario invalidar manualmente el contenido en el despachante, pero es posible si es necesario, tal como se describe a continuación.

Antes de AEM como Cloud Service, había dos maneras de invalidar la caché del despachante.

1. Invocar el agente de replicación, especificando el agente de vaciado del despachante de publicación
2. Llamando directamente a la API `invalidate.cache` (por ejemplo, `POST /dispatcher/invalidate.cache`)

Ya no se admitirá el método de API `invalidate.cache` del despachante, ya que solo se dirige a un nodo de despachante específico. AEM como Cloud Service funciona en el nivel de servicio, no en el nivel de nodo individual, por lo que las instrucciones de invalidación de la página [Invalidación de páginas en caché de AEM](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/page-invalidate.html) ya no son válidas para AEM como Cloud Service.
En su lugar, debe utilizarse el agente de vaciado de replicación. Esto se puede hacer con la API de replicación. La documentación de la API de replicación está disponible [aquí](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/Replicator.html) y para ver un ejemplo de vaciado de la caché, consulte la [página de ejemplo de la API](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) específicamente el ejemplo `CustomStep` que emite una acción de replicación de tipo ACTIVATE a todos los agentes disponibles. El extremo del agente de vaciado no se puede configurar pero está preconfigurado para que apunte al despachante, junto con el servicio de publicación que ejecuta el agente de vaciado. Normalmente, el agente de vaciado puede activarse mediante eventos o flujos de trabajo OSGi.

El diagrama que se presenta a continuación ilustra esto.

![](assets/cdnd.png "CDNCDN")

Si existe la preocupación de que la memoria caché del despachante no esté borrando, póngase en contacto con [Asistencia al cliente](https://helpx.adobe.com/support.ec.html) quién puede vaciar la memoria caché del despachante si es necesario.

La CDN gestionada por el Adobe respeta los TTL y, por lo tanto, no es necesario vaciarla. Si se sospecha un problema, [póngase en contacto con el soporte técnico](https://helpx.adobe.com/support.ec.html) para que pueda vaciar una caché de CDN administrada por Adobe según sea necesario.

## Bibliotecas del lado del cliente y coherencia de la versión {#content-consistency}

Las páginas están compuestas de HTML, JavaScript, CSS e imágenes. Se recomienda a los clientes aprovechar el marco [de bibliotecas del lado del cliente (clientlibs)](/help/implementing/developing/introduction/clientlibs.md) para importar recursos de JavaScript y CSS en páginas HTML, teniendo en cuenta las dependencias entre bibliotecas de JS.

El módulo clientlibs proporciona administración automática de versiones, lo que significa que los desarrolladores pueden registrar cambios en las bibliotecas JS en el control de código fuente y la última versión estará disponible cuando un cliente implemente su versión. Sin esto, los desarrolladores necesitarían cambiar manualmente HTML con referencias a la nueva versión de la biblioteca, lo que resulta especialmente oneroso si muchas plantillas HTML comparten la misma biblioteca.

Cuando las nuevas versiones de las bibliotecas se publican en producción, las páginas HTML de referencia se actualizan con nuevos vínculos a esas versiones de biblioteca actualizadas. Una vez que la caché del explorador ha caducado para una página HTML determinada, no hay problema de que las bibliotecas antiguas se carguen desde la caché del explorador, ya que la página actualizada (desde AEM) ahora está garantizada para hacer referencia a las nuevas versiones de las bibliotecas. En otras palabras, una página HTML actualizada incluirá todas las versiones de biblioteca más recientes.

El mecanismo para esto es un hash serializado, que se anexa al vínculo de la biblioteca del cliente, lo que garantiza una dirección URL única y con versiones para que el explorador almacene en caché CSS/JS. El hash serializado solo se actualiza cuando cambia el contenido de la biblioteca del cliente. Esto significa que si se producen actualizaciones no relacionadas (es decir, no se producen cambios en los css/js subyacentes de la biblioteca del cliente) incluso con una nueva implementación, la referencia permanece igual, lo que garantiza una menor interrupción en la caché del explorador.

### Activación de versiones Longcache de bibliotecas del lado del cliente: AEM como un inicio rápido del SDK del Cloud Service {#enabling-longcache}

La clientlib predeterminada incluye en una página HTML un aspecto similar al siguiente ejemplo:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.css" type="text/css">
```

Cuando está habilitado el control de versiones clientlib estricto, se agrega una clave hash a largo plazo como selector a la biblioteca del cliente. Como resultado, la referencia clientlib tiene este aspecto:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.lc-7c8c5d228445ff48ab49a8e3c865c562-lc.css" type="text/css">
```

El control de versiones de clientlib estricto está habilitado de forma predeterminada en todos los AEM como entornos de Cloud Service.

Para habilitar el control de versiones estrictas de clientlib en el SDK local Quickstart, realice las siguientes acciones:

1. Vaya al Administrador de configuración de OSGi `<host>/system/console/configMgr`
1. Busque el Administrador de biblioteca HTML de OSGi para Adobe Granite:
   * Marque la casilla de verificación para habilitar el control estricto de versiones
   * En el campo rotulado Clave de caché del lado del cliente a largo plazo, introduzca el valor de /.*;hash
1. Guarde los cambios. Tenga en cuenta que no es necesario guardar esta configuración en el control de código fuente, ya que AEM como Cloud Service habilitará automáticamente esta configuración en entornos de desarrollo, etapa y producción.
1. Cada vez que se cambia el contenido de la biblioteca del cliente, se genera una nueva clave hash y se actualiza la referencia HTML.
