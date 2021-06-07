---
title: Almacenamiento en caché en AEM as a Cloud Service
description: 'Almacenamiento en caché en AEM as a Cloud Service '
feature: Dispatcher
exl-id: 4206abd1-d669-4f7d-8ff4-8980d12be9d6
source-git-commit: a446efacb91f1a620d227b9413761dd857089c96
workflow-type: tm+mt
source-wordcount: '1530'
ht-degree: 1%

---

# Introducción {#intro}

El tráfico pasa a través de la CDN a una capa de servidor web Apache, que admite módulos, incluido el Dispatcher. Para aumentar el rendimiento, Dispatcher se utiliza principalmente como caché para limitar el procesamiento en los nodos de publicación.
Se pueden aplicar reglas a la configuración de Dispatcher para modificar cualquier configuración de caducidad de caché predeterminada, lo que resulta en el almacenamiento en caché en la CDN. Tenga en cuenta que Dispatcher también respeta los encabezados de caducidad de caché resultantes si `enableTTL` está habilitado en la configuración de Dispatcher, lo que implica que actualizará el contenido específico incluso fuera del contenido que se republica.

Esta página también describe cómo se invalida la caché de Dispatcher, así como cómo funciona el almacenamiento en caché a nivel de explorador con respecto a las bibliotecas del lado del cliente.

## Almacenamiento en caché {#caching}

### HTML/texto {#html-text}

* de forma predeterminada, el explorador almacena en caché durante cinco minutos, según el encabezado `cache-control` emitido por la capa Apache. La CDN también respeta este valor.
* la configuración predeterminada de almacenamiento en caché HTML/texto se puede deshabilitar definiendo la variable `DISABLE_DEFAULT_CACHING` en `global.vars`:

```
Define DISABLE_DEFAULT_CACHING
```

Esto puede resultar útil, por ejemplo, cuando la lógica empresarial requiere un ajuste preciso del encabezado de la página (con un valor basado en el día del calendario), ya que de forma predeterminada el encabezado de la página está establecido en 0. Dicho esto, **tenga cuidado al desactivar el almacenamiento en caché predeterminado.**

* se puede sobrescribir para todo el contenido HTML/texto definiendo la variable `EXPIRATION_TIME` en `global.vars` con las herramientas de Dispatcher del SDK de AEM as a Cloud Service.
* puede anularse en un nivel más fino mediante las siguientes directivas apache mod_headers :

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header set Cache-Control "max-age=200"
        Header set Age 0
   </LocationMatch>
   ```

   Tenga cuidado al configurar los encabezados de control de caché globales o los que coinciden con un regex amplio para que no se apliquen a contenido que pueda tener la intención de mantener privado. Considere la posibilidad de utilizar varias directivas para garantizar que las reglas se apliquen de forma precisa. Dicho esto, AEM como Cloud Service quitará el encabezado de la caché si detecta que se ha aplicado a lo que detecta que es inaccesible para Dispatcher, como se describe en la documentación de Dispatcher. Para obligar a los AEM a aplicar siempre el almacenamiento en caché, se puede añadir la opción &quot;siempre&quot; de la siguiente manera:

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header always set Cache-Control "max-age=200"
        Header set Age 0
   </LocationMatch>
   ```

   Debe asegurarse de que un archivo de `src/conf.dispatcher.d/cache` tiene la siguiente regla (que está en la configuración predeterminada):

   ```
   /0000
   { /glob "*" /type "allow" }
   ```

* Para evitar que se almacene contenido específico en caché, establezca el encabezado Cache-Control en *private*. Por ejemplo, lo siguiente impide que el contenido html de un directorio llamado **myfolder** se almacene en caché:

   ```
      <LocationMatch "/content/myfolder/.*\.(html)$">.  // replace with the right regex
      Header set Cache-Control “private”
     </LocationMatch>
   ```

   >[!NOTE]
   >Los demás métodos, incluido el [Dispatcher-ttl AEM proyecto ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), no anularán correctamente los valores.

### Bibliotecas de cliente (js, css) {#client-side-libraries}

* al utilizar AEM marco de biblioteca del lado del cliente, el código JavaScript y CSS se generan de forma que los navegadores puedan almacenarlo en caché indefinidamente, ya que cualquier cambio se manifiesta como nuevos archivos con una ruta única.  En otras palabras, el HTML que hace referencia a las bibliotecas de cliente se producirá según sea necesario para que los clientes puedan experimentar contenido nuevo a medida que se publique. El control de caché se establece en &quot;inmutable&quot; o 30 días para los exploradores más antiguos que no respetan el valor &quot;inmutable&quot;.
* consulte la sección [Bibliotecas del lado del cliente y coherencia de la versión](#content-consistency) para obtener más información.

### Imágenes y cualquier contenido lo suficientemente grande como para almacenarlo en blob {#images}

* de forma predeterminada, no está almacenado en caché
* puede establecerse en un nivel más fino mediante las siguientes directivas apache `mod_headers` :

   ```
      <LocationMatch "^/content/.*\.(jpeg|jpg)$">
        Header set Cache-Control "max-age=222"
        Header set Age 0
      </LocationMatch>
   ```

   Consulte la discusión en la sección html/text anterior para tener cuidado de no almacenar en caché demasiado ampliamente y también cómo forzar a AEM a que siempre aplique el almacenamiento en caché con la opción &quot;siempre&quot;.

   Es necesario asegurarse de que un archivo en `src/conf.dispatcher.d/`caché tiene la siguiente regla (que está en la configuración predeterminada):

   ```
   /0000
   { /glob "*" /type "allow" }
   ```

   Asegúrese de que los recursos destinados a ser guardados en privado en lugar de en caché no formen parte de los filtros de directiva LocationMatch.

   >[!NOTE]
   >Los demás métodos, incluido el [Dispatcher-ttl AEM proyecto ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), no anularán correctamente los valores.

### Otros tipos de archivos de contenido en el almacén de nodos {#other-content}

* sin caché predeterminada
* el valor predeterminado no se puede establecer con la variable `EXPIRATION_TIME` utilizada para los tipos de archivo html/text
* la caducidad de la caché se puede configurar con la misma estrategia LocationMatch descrita en la sección html/text especificando la regex adecuada

## Invalidación de caché de Dispatcher {#disp}

En general, no es necesario invalidar la caché de Dispatcher. En su lugar, debe confiar en que Dispatcher actualice su caché cuando el contenido se esté republicando y la CDN respete los encabezados de caducidad de la caché.

### Invalidación de caché de Dispatcher durante la activación/desactivación {#cache-activation-deactivation}

Al igual que las versiones anteriores de AEM, la publicación o cancelación de la publicación de páginas borrará el contenido de la caché de Dispatcher. Si se sospecha un problema de almacenamiento en caché, los clientes deben volver a publicar las páginas en cuestión.

Cuando la instancia de publicación recibe una nueva versión de una página o recurso del autor, utiliza el agente de vaciado para invalidar las rutas adecuadas en su despachante. La ruta actualizada se elimina de la caché del Dispatcher, junto con sus principales, hasta un nivel (puede configurarla con el [statfileslevel](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level).

### Invalidación explícita de caché de Dispatcher {#explicit-invalidation}

En general, no será necesario invalidar manualmente el contenido en Dispatcher, pero es posible si es necesario, tal y como se describe a continuación.

Antes de AEM como Cloud Service, había dos formas de invalidar la caché del despachante.

1. Invocar el agente de replicación, especificando el agente de vaciado del despachante de publicación
2. Llamar directamente a la API `invalidate.cache` (por ejemplo, `POST /dispatcher/invalidate.cache`)

El enfoque de la API `invalidate.cache` de Dispatcher ya no será compatible, ya que se dirige únicamente a un nodo de Dispatcher específico. AEM como Cloud Service funciona en el nivel de servicio, no en el nivel de nodo individual y, por lo tanto, las instrucciones de invalidación de la página [Invalidación de páginas en caché de AEM](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html) ya no son válidas para AEM como Cloud Service .
En su lugar, se debe utilizar el agente de vaciado de replicación. Esto se puede hacer mediante la API de replicación. La documentación de la API de replicación está disponible [aquí](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/replication/Replicator.html) y para ver un ejemplo de vaciado de la caché, consulte la [página de ejemplo de la API](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) específicamente el ejemplo `CustomStep` que emite una acción de replicación de tipo ACTIVATE a todos los agentes disponibles. El extremo del agente de vaciado no se puede configurar, pero está preconfigurado para apuntar al despachante, coincide con el servicio de publicación que ejecuta el agente de vaciado. Normalmente, el agente de vaciado se puede activar mediante eventos o flujos de trabajo OSGi.

El diagrama que se muestra a continuación ilustra esto.

![](assets/cdnd.png "CDNCDN")

Si existe preocupación de que la caché de Dispatcher no se esté borrando, póngase en contacto con [customer support](https://helpx.adobe.com/support.ec.html), que puede vaciar la caché de Dispatcher si es necesario.

La CDN administrada por Adobe respeta los TTL y, por lo tanto, no es necesario vaciarla. Si se sospecha un problema, [póngase en contacto con el servicio de asistencia al cliente](https://helpx.adobe.com/support.ec.html), que puede vaciar una caché de CDN administrada por Adobe según sea necesario.

## Bibliotecas de cliente y coherencia de la versión {#content-consistency}

Las páginas están compuestas de HTML, JavaScript, CSS e imágenes. Se recomienda a los clientes aprovechar el marco [Client-Side Libraries (clientlibs)](/help/implementing/developing/introduction/clientlibs.md) para importar recursos de JavaScript y CSS en páginas HTML, teniendo en cuenta las dependencias entre las bibliotecas JS.

El marco clientlibs proporciona administración automática de versiones, lo que significa que los desarrolladores pueden registrar cambios en las bibliotecas JS en control de código fuente y la última versión estará disponible cuando un cliente implemente su lanzamiento. Sin esto, los desarrolladores necesitarían cambiar manualmente HTML con referencias a la nueva versión de la biblioteca, lo que resulta especialmente oneroso si muchas plantillas HTML comparten la misma biblioteca.

Cuando se lanzan las nuevas versiones de las bibliotecas a la producción, las páginas HTML de referencia se actualizan con nuevos vínculos a esas versiones de las bibliotecas actualizadas. Una vez que la caché del explorador ha caducado para una página HTML determinada, no existe preocupación de que las bibliotecas antiguas se carguen desde la caché del explorador, ya que la página actualizada (desde AEM) ahora tiene la seguridad de hacer referencia a las nuevas versiones de las bibliotecas. En otras palabras, una página HTML actualizada incluirá todas las versiones más recientes de la biblioteca.

El mecanismo para esto es un hash serializado, que se adjunta al vínculo de la biblioteca del cliente, lo que garantiza una url única y versionada para que el explorador almacene en caché CSS/JS. El hash serializado solo se actualiza cuando cambia el contenido de la biblioteca del cliente. Esto significa que si se producen actualizaciones no relacionadas (es decir, no se producen cambios en el css/js subyacente de la biblioteca del cliente) incluso con una nueva implementación, la referencia permanece igual, lo que garantiza menos interrupciones en la caché del explorador.

### Activación de versiones de Longcache de bibliotecas del cliente: AEM como Cloud Service SDK Quickstart {#enabling-longcache}

La clientlib predeterminada incluye en una página HTML con un aspecto similar al siguiente ejemplo:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.css" type="text/css">
```

Cuando está habilitado el control de versiones de clientlib estricto, se agrega una clave hash a largo plazo como selector a la biblioteca del cliente. Como resultado, la referencia clientlib tiene este aspecto:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.lc-7c8c5d228445ff48ab49a8e3c865c562-lc.css" type="text/css">
```

El control de versiones de clientlib estricto está habilitado de forma predeterminada en todos los AEM como entornos de Cloud Service.

Para habilitar versiones clientlib estrictas en el SDK local Quickstart, realice las siguientes acciones:

1. Vaya al gestor de configuración OSGi `<host>/system/console/configMgr`
1. Busque la configuración OSGi para el Administrador de bibliotecas HTML de Adobe Granite:
   * Marque la casilla de verificación para activar el control estricto de versiones
   * En el campo denominado Long term client side cache key, introduzca el valor de /.*;hash
1. Guarde los cambios. Tenga en cuenta que no es necesario guardar esta configuración en el control de código fuente, ya que AEM como Cloud Service habilitará automáticamente esta configuración en entornos de desarrollo, fase y producción.
1. Cada vez que se cambia el contenido de la biblioteca del cliente, se genera una nueva clave hash y se actualiza la referencia HTML.
