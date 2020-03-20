---
title: Entrega de contenido
description: 'Entrega de contenido '
translation-type: tm+mt
source-git-commit: d1c953e1caf440f18e488f07a32bcf5bc3880f67

---


# Distribución de contenido en AEM como un servicio en la nube {#content-delivery}

La entrega de contenido del servicio de publicación incluye:

* CDN (normalmente administrado por Adobe)
* Distribuidor de AEM
* Publicación de AEM

El flujo de datos es el siguiente:

1. La dirección URL se agrega al explorador
1. Solicitud realizada a CDN asignada en DNS a ese dominio
1. Si el contenido se almacena completamente en caché en CDN, CDN lo proporciona al explorador
1. Si el contenido no se almacena completamente en caché, la CDN llama (proxy inverso) al distribuidor
1. Si el contenido se almacena completamente en la caché del despachante, el despachante lo proporciona a la CDN
1. Si el contenido no se almacena completamente en la caché, el despachante llama (proxy inverso) a la publicación de AEM
1. El navegador procesa el contenido, que también puede almacenarlo en caché, según los encabezados

El tipo de contenido HTML/texto está configurado para caducar después de 300 segundos (5 minutos) en la capa del despachante, un umbral que respetan tanto la caché del despachante como la CDN. Durante las redistribuciones del servicio de publicación, la caché del despachante se borra y se calienta posteriormente antes de que los nuevos nodos de publicación acepten el tráfico.

Las secciones a continuación proporcionan buenos detalles sobre la entrega de contenido, incluida la configuración de CDN y el almacenamiento en caché de despachantes.

La información sobre la replicación del servicio de creación al servicio de publicación está disponible [aquí](/help/operations/replication.md).

>[!NOTE]
>El tráfico pasa por un servidor web apache, que admite módulos, incluido el despachante. El despachante se utiliza principalmente como caché para limitar el procesamiento en los nodos de publicación con el fin de aumentar el rendimiento.

## CDN {#cdn}

AEM ofrece tres opciones:

1. CDN gestionado por Adobe: CDN incorporado de AEM. Esta es la opción recomendada, ya que está completamente integrada.
1. CDN de cliente apunta a CDN gestionado por Adobe: el cliente señala su propia CDN a la CDN integrada de AEM. Si la primera opción no es viable, esta es la siguiente opción preferida, ya que aún aprovecha la integración de AEM con su CDN predeterminado. Los clientes seguirán siendo responsables de administrar su propia CDN.
1. CDN administrada por el cliente: El cliente trae su propia CDN y es totalmente responsable de administrarla.

>[!CAUTION]
>La primera opción es muy recomendable. Adobe no se responsabiliza del resultado de cualquier error de configuración si elige la segunda opción.

Las opciones segunda y tercera se permitirán caso por caso. Esto implica cumplir ciertos requisitos previos, incluyendo, entre otros, el hecho de que el cliente tenga una integración heredada con su proveedor de CDN, lo cual es difícil de deshacer.

### CDN gestionado por Adobe {#adobe-managed-cdn}

La preparación para la entrega de contenido mediante la CDN integrada de Adobe es sencilla, tal como se describe a continuación:

1. Proporcionará el certificado SSL firmado y la clave secreta a Adobe compartiendo un vínculo a un formulario seguro que contenga esta información. Coordine esta tarea con la asistencia al cliente.
Nota: Aem como servicio de nube no admite certificados de dominio validados (DV).
1. El servicio de asistencia al cliente coordinará con usted la temporización de un registro DNS CNAME, señalando a su FQDN `adobe-aem.map.fastly.net`.
1. Se le notificará cuando los certificados SSL caduquen para que pueda volver a enviar los nuevos certificados SSL.

De forma predeterminada, para una configuración de CDN administrada de Adobe, todo el tráfico público puede llegar al servicio de publicación, tanto para los entornos de producción como para los de no producción (desarrollo y fase). Si desea limitar el tráfico al servicio de publicación para un entorno determinado (por ejemplo, limitar el ensayo por un rango de direcciones IP), debe trabajar con la asistencia al cliente para configurar estas restricciones.

### CDN de cliente apunta a CDN gestionada por Adobe {#point-to-point-CDN}

Compatible si desea utilizar la CDN existente, pero no puede satisfacer los requisitos de una CDN administrada por el cliente. En este caso, usted administra su propia CDN, pero señala a la CDN administrada de Adobe.

Tenga en cuenta que debe:

1. Debe tener una CDN existente.
1. Usted lo administrará.
1. Debe ser capaz de configurar CDN para que funcione con Aem como un servicio de nube; consulte las instrucciones de configuración a continuación.
1. Dispone de expertos en ingeniería de CDN que están disponibles en caso de que surjan problemas relacionados.
1. Debe realizar y superar correctamente una prueba de carga antes de ir a producción.

Instrucciones de configuración:

1. Configure el `X-Forwarded-Host` encabezado con el nombre de dominio.
1. Establezca el encabezado Host con el dominio de origen, que es la entrada de CDN de Adobe. El valor debe proceder de Adobe.
1. Envíe el encabezado SNI al origen. Al igual que el encabezado Host, el encabezado sni debe ser el dominio de origen.
1. Establezca el `X-Edge-Key`, que es necesario para enrutar el tráfico correctamente a los servidores AEM. El valor debe proceder de Adobe.

### CDN gestionado por el cliente {#customer-managed-cdn}

Compatible si necesita utilizar la CDN existente.  En este caso, puede administrar su propia CDN, señalándola a AEM.

Puede administrar su propia CDN, siempre que:

1. Tiene una CDN existente.
1. Debe ser una CDN admitida. Actualmente, se admite Akamai. Si su organización desea administrar una CDN no admitida actualmente, póngase en contacto con el servicio de asistencia al cliente.
1. Usted lo administrará.
1. Debe ser capaz de configurar CDN para que funcione con Aem como un servicio de nube; consulte las instrucciones de configuración a continuación.
1. Dispone de expertos en ingeniería de CDN que están disponibles en caso de que surjan problemas relacionados.
1. Debe proporcionar listas blancas de nodos CDN al Administrador de nube, tal como se describe en las instrucciones de configuración.
1. Debe realizar y superar correctamente una prueba de carga antes de ir a producción.

Instrucciones de configuración:

1. Proporcione la lista blanca del proveedor de CDN a Adobe llamando a la API de creación/actualización de entorno con una lista de CIDR para la lista blanca.
1. Configure el `X-Forwarded-Host` encabezado con el nombre de dominio.
1. Establezca el encabezado Host con el dominio de origen, que es Aem como ingreso al servicio de nube. El valor debe proceder de Adobe.
1. Envíe el encabezado SNI al origen. El encabezado SNI debe ser el dominio de origen.
1. Establezca `X-Edge-Key` lo que se necesita para enrutar el tráfico correctamente a los servidores AEM. El valor debe proceder de Adobe.

Antes de aceptar el tráfico activo, debe validar con el servicio de asistencia al cliente de Adobe que el enrutamiento de tráfico de extremo a extremo funciona correctamente.

### Almacenamiento en caché {#caching}

El proceso de almacenamiento en caché sigue las reglas que se presentan a continuación.

### HTML/Texto {#html-text}

* de forma predeterminada, el explorador almacena en caché durante 5 minutos, según el encabezado de control de caché emitido por la capa apache. La CDN también respeta este valor.
* se puede anular para todo el contenido HTML/Texto definiendo la `EXPIRATION_TIME` variable en `global.vars` el uso de AEM como herramienta de distribución del SDK de Cloud Service.

Debe asegurarse de que un archivo debajo `src/conf.dispatcher.d/cache` tiene la siguiente regla:

```
/0000
{ /glob "*" /type "allow" }
```

* puede anularse en un nivel más fino mediante las directivas apache mod_headers. Por ejemplo:

```
<LocationMatch "\.(html)$">
        Header set Cache-Control "max-age=200 s-maxage=200"
</LocationMatch>
```

Debe asegurarse de que un archivo debajo `src/conf.dispatcher.d/cache` tiene la siguiente regla:

```
/0000
{ /glob "*" /type "allow" }
```

* Tenga en cuenta que otros métodos, incluido el proyecto [](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/)Dispatcher-ttl AEM ACS Commons, no anularán correctamente los valores.

### Bibliotecas de cliente (js, css) {#client-side-libraries}

* al utilizar el marco de trabajo de biblioteca del cliente de AEM, el código JavaScript y CSS se genera de forma que los navegadores pueden almacenarlo en caché indefinidamente, ya que cualquier cambio se manifiesta como nuevos archivos con una ruta única.  En otras palabras, el HTML que hace referencia a las bibliotecas de cliente se producirá según sea necesario para que los clientes puedan experimentar contenido nuevo a medida que se publica. El control de caché se establece en &quot;inmutable&quot; o en 30 días para los exploradores más antiguos que no respetan el valor &quot;inmutable&quot;.
* consulte la sección Bibliotecas del lado del [cliente y coherencia](#content-consistency) de la versión para obtener más detalles.

### Imágenes {#images}

* no almacenado en caché

### Otros tipos de contenido {#other-content}

* sin caché predeterminada
* puede ser anulado por apache `mod_headers`. Por ejemplo:

```
<LocationMatch "\.(css|js)$">
    Header set Cache-Control "max-age=500 s-maxage=500"
</LocationMatch>
```

*Otros métodos para configurar los encabezados de caché también pueden funcionar

Antes de aceptar el tráfico activo, los clientes deben validar con el servicio de asistencia al cliente de Adobe que el enrutamiento de tráfico de extremo a extremo funciona correctamente.

## Dispatcher {#disp}

El tráfico pasa por un servidor web apache, que admite módulos, incluido el despachante. El despachante se utiliza principalmente como caché para limitar el procesamiento en los nodos de publicación con el fin de aumentar el rendimiento.

El contenido de tipo HTML/texto se establece con encabezados de caché que corresponden a una caducidad de 300 segundos (5 minutos).

El resto de esta sección describe consideraciones relacionadas con la invalidación de la caché del despachante.

### Invalidación de caché de despachantes durante la activación/desactivación {#cache-activation-deactivation}

Al igual que las versiones anteriores de AEM, la publicación o cancelación de publicaciones borrará el contenido de la caché del despachante. Si se sospecha un problema de almacenamiento en caché, los clientes deben volver a publicar las páginas en cuestión.

Cuando la instancia de publicación recibe una nueva versión de una página o recurso del autor, utiliza el agente de vaciado para invalidar las rutas adecuadas en su distribuidor. La ruta de acceso actualizada se elimina de la caché del despachante, junto con sus elementos principales, hasta un nivel (puede configurarla con el [nivel](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level)statfiles).

### invalidación explícita de la caché del despachante {#explicit-invalidation}

En general, no será necesario invalidar manualmente el contenido en el despachante, pero es posible si es necesario, tal como se describe a continuación.

Antes de AEM como servicio de nube, había dos formas de invalidar la caché del despachante.

1. Invocar el agente de replicación, especificando el agente de vaciado del despachante de publicación
2. Llamar directamente a la `invalidate.cache` API (por ejemplo, `POST /dispatcher/invalidate.cache`)

Ya no se admitirá el `invalidate.cache` método, ya que solo se dirige a un nodo de distribuidor específico.
AEM como servicio de nube funciona en el nivel de servicio, no en el nivel de nodo individual, por lo que las instrucciones de invalidación de la página [Invalidar páginas en caché de AEM](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/page-invalidate.html) no son válidas para AEM como servicio de nube.
En su lugar, debe utilizarse el agente de vaciado de replicación. Esto se puede hacer con la API de replicación. La documentación de la API de replicación está disponible [aquí](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/Replicator.html) y para ver un ejemplo de vaciado de la caché, consulte la página [de ejemplo de la](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) API específicamente el `CustomStep` ejemplo de cómo emitir una acción de replicación de tipo ACTIVATE a todos los agentes disponibles. El extremo del agente de vaciado no se puede configurar pero está preconfigurado para que apunte al despachante, junto con el servicio de publicación que ejecuta el agente de vaciado. El agente de vaciado generalmente se puede activar mediante eventos o flujos de trabajo de OSGi.

El diagrama siguiente ilustra esto.

![](assets/cdnc.png "CDNCDN")

Si existe la preocupación de que la caché del despachante no esté borrando, póngase en contacto con el servicio de asistencia al cliente, el cual puede vaciar la caché del despachante si es necesario.

La CDN administrada por Adobe respeta los TTL y, por lo tanto, no es necesario vaciarla. Si se sospecha un problema, póngase en contacto con el servicio de asistencia al cliente para que pueda vaciar una caché de CDN administrada por Adobe según sea necesario.

## Bibliotecas de cliente y coherencia de versiones {#content-consistency}

Las páginas están compuestas por HTML, JavaScript, CSS e imágenes. Se recomienda a los clientes que aprovechen el marco de bibliotecas de cliente (clientlibs) para importar recursos de JavaScript y CSS en páginas HTML, teniendo en cuenta las dependencias entre bibliotecas de JS.

El módulo clientlibs proporciona administración automática de versiones, lo que significa que los desarrolladores pueden registrar cambios en las bibliotecas JS en el control de código fuente y la última versión estará disponible cuando un cliente implemente su versión. Sin esto, los desarrolladores necesitarían cambiar manualmente HTML con referencias a la nueva versión de la biblioteca, lo que resulta especialmente oneroso si muchas plantillas HTML comparten la misma biblioteca.

Cuando las nuevas versiones de las bibliotecas se publican en producción, las páginas HTML de referencia se actualizan con nuevos vínculos a esas versiones de biblioteca actualizadas. Una vez que la caché del navegador ha caducado para una página HTML determinada, no hay problema de que las bibliotecas antiguas se carguen desde la caché del navegador, ya que la página actualizada (desde AEM) ahora está garantizada para hacer referencia a las nuevas versiones de las bibliotecas. En otras palabras, una página HTML actualizada incluirá todas las versiones de biblioteca más recientes.

El mecanismo para esto es un hash serializado, que se anexa al vínculo de la biblioteca del cliente, lo que garantiza una dirección URL única y con versiones para que el explorador almacene en caché CSS/JS. El hash serializado solo se actualiza cuando cambia el contenido de la biblioteca del cliente. Esto significa que si se producen actualizaciones no relacionadas (es decir, no se producen cambios en los css/js subyacentes de la biblioteca del cliente) incluso con una nueva implementación, la referencia permanece igual, lo que garantiza una menor interrupción en la caché del explorador.

### Activación de las versiones Longcache de las bibliotecas del lado del cliente: AEM como inicio rápido del SDK del servicio de nube {#enabling-longcache}

La clientlib predeterminada incluye en una página HTML un aspecto similar al siguiente ejemplo:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.css" type="text/css">
```

Cuando está habilitado el control de versiones clientlib estricto, se agrega una clave hash a largo plazo como selector a la biblioteca del cliente. Como resultado, la referencia clientlib tiene este aspecto:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.lc-7c8c5d228445ff48ab49a8e3c865c562-lc.css" type="text/css">
```

El control de versiones de clientlib estricto está habilitado de forma predeterminada en todos los entornos de AEM como servicio de nube.

Para habilitar el control de versiones estrictas de clientlib en el SDK local Quickstart, realice las siguientes acciones:

1. Vaya al Administrador de configuración de OSGi <host>/system/console/configMgr
1. Busque la configuración OSGi para Adobe Granite HTML Library Manager:
   * Marque la casilla de verificación para habilitar el control estricto de versiones
   * En el campo rotulado Clave de caché del lado del cliente a largo plazo, introduzca el valor de /.*;hash
1. Guarde los cambios. Tenga en cuenta que no es necesario guardar esta configuración en el control de código fuente, ya que AEM como servicio de nube habilitará automáticamente esta configuración en entornos de desarrollo, fase y producción.
1. Cada vez que se cambia el contenido de la biblioteca del cliente, se genera una nueva clave hash y se actualiza la referencia HTML.
