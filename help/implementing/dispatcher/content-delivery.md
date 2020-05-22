---
title: Envío de contenido
description: 'Envío de contenido '
translation-type: tm+mt
source-git-commit: a07de761dd9aedb3469f256e08ecf05b2102889d
workflow-type: tm+mt
source-wordcount: '2268'
ht-degree: 1%

---


# Enviar contenido en AEM as a Cloud Service {#content-delivery}

La página actual detalla el envío de contenido del servicio de publicación en AEM como un servicio de nube. El envío de contenido del servicio de publicación incluye:

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

Las secciones a continuación proporcionan buenos detalles sobre el envío de contenido, incluida la configuración de CDN y el almacenamiento en caché.

La información sobre la replicación del servicio de creación al servicio de publicación está disponible [aquí](/help/operations/replication.md).

## CDN {#cdn}

AEM as Cloud Service se suministra con una CDN integrada. Su principal propósito es reducir la latencia mediante la entrega de contenido procesable desde los nodos CDN en el borde, cerca del explorador. Está completamente administrado y configurado para un rendimiento óptimo de las aplicaciones AEM.

En total, AEM oferta dos opciones:

1. CDN gestionado por AEM: CDN incorporado de AEM. Se trata de una opción estrechamente integrada que no requiere una gran inversión de los clientes en el soporte de la integración de CDN con AEM.
1. CDN gestionado por el cliente apunta a CDN gestionado por AEM: el cliente señala su propia CDN a la CDN integrada de AEM. El cliente aún tendrá que administrar su propia CDN, pero la inversión en la integración con AEM es moderada.

La primera opción debe satisfacer la mayoría de los requisitos de seguridad y rendimiento del cliente. Además, requiere un esfuerzo mínimo del cliente.

La segunda opción se permitirá caso por caso. La decisión se basa en cumplir ciertos requisitos previos, como el hecho de que el cliente tenga una integración heredada con su proveedor de CDN que sea difícil de abandonar.

A continuación se presenta una matriz de decisiones para comparar las dos opciones. Encontrará información más detallada en las secciones siguientes.

| Detalles | CDN gestionado por AEM | CDN gestionado por el cliente señala a CDN de AEM |
|---|---|---|
| **Esfuerzo del cliente** | Ninguno, está completamente integrado. Solo es necesario que señale CNAME a la CDN gestionada por AEM. | Moderar la inversión de los clientes. El cliente debe administrar su propia CDN. |
| **Requisitos previos** | Ninguna | CDN existente que resulta oneroso de reemplazar. Debe mostrar una prueba de carga correcta antes de activarse. |
| **Experiencia de CDN** | Ninguna | Requiere al menos un recurso de ingeniería a tiempo parcial con conocimientos detallados de CDN que puedan configurar la CDN del cliente. |
| **Seguridad** | Administrado por Adobe. | Administrado por Adobe (y opcionalmente por el cliente en su propia CDN). |
| **Actuación** | Optimizado por Adobe. | Se beneficiará de algunas funciones de CDN de AEM, pero posiblemente de un pequeño rendimiento debido al salto adicional. **Nota**: Evita que la CDN del cliente pase a la CDN de Adobe lista para usar (probablemente sea eficaz). |
| **Almacenamiento en caché** | Admite encabezados de caché aplicados al despachante. | Admite encabezados de caché aplicados al despachante. |
| **Funciones de compresión de imágenes y vídeo** | Puede trabajar con Adobe Dynamic Media. | Puede trabajar con Adobe Dynamic Media o con una solución de vídeo/imagen CDN administrada por el cliente. |

### CDN gestionado por AEM  {#aem-managed-cdn}

La preparación para el envío de contenido mediante la CDN integrada de Adobe es sencilla, tal como se describe a continuación:

1. Proporcionará el certificado SSL firmado y la clave secreta a Adobe compartiendo un vínculo a un formulario seguro que contenga esta información. Coordine con la asistencia al cliente esta tarea.
   **Nota:** Aem como servicio de nube no admite certificados de dominio validados (DV).
1. Debe informar a la asistencia al cliente:
   * qué dominio personalizado debe asociarse con un determinado entorno, tal como se define en la identificación del programa y en la identificación del entorno.
   * si se necesita una lista blanca de IP para restringir el tráfico a un entorno determinado.
1. El servicio de asistencia al cliente coordinará con usted la temporización de un registro DNS CNAME, señalando a su FQDN `cdn.adobeaemcloud.com`.
1. Se le notificará cuando los certificados SSL caduquen para que pueda volver a enviar los nuevos certificados SSL.

**Restricción del tráfico**

De forma predeterminada, para una configuración de CDN administrada de Adobe, todo el tráfico público puede llegar al servicio de publicación, tanto para entornos de producción como de no producción (desarrollo y fase). Si desea limitar el tráfico al servicio de publicación para un entorno determinado (por ejemplo, limitar el ensayo por un rango de direcciones IP), debe trabajar con la asistencia al cliente para configurar estas restricciones.

### CDN de cliente apunta a CDN gestionado por AEM {#point-to-point-CDN}

Compatible si desea utilizar la CDN existente, pero no puede satisfacer los requisitos de una CDN administrada por el cliente. En este caso, usted administra su propia CDN, pero señala a la CDN administrada de Adobe.

Tenga en cuenta que:

1. Debe tener una CDN existente.
1. Debes administrarlo.
1. Debe ser capaz de configurar la CDN para que funcione con Aem como un servicio de nube; consulte las instrucciones de configuración a continuación.
1. Debe contar con expertos en ingeniería de CDN que estén disponibles en caso de que surjan problemas relacionados.
1. Debe realizar y superar correctamente una prueba de carga antes de ir a producción.

Instrucciones de configuración:

1. Configure el `X-Forwarded-Host` encabezado con el nombre de dominio.
1. Establezca el encabezado Host con el dominio de origen, que es la entrada de CDN de Adobe. El valor debe proceder de Adobe.
1. Envíe el encabezado SNI al origen. Al igual que el encabezado Host, el encabezado sni debe ser el dominio de origen.
1. Establezca el `X-Edge-Key`, que es necesario para enrutar el tráfico correctamente a los servidores AEM. El valor debe proceder de Adobe.

Antes de aceptar el tráfico activo, debe validar con el servicio de asistencia al cliente de Adobe que el enrutamiento de tráfico de extremo a extremo funciona correctamente.

## Almacenamiento en caché {#caching}

El almacenamiento en caché en CDN se puede configurar mediante reglas de despachante. Tenga en cuenta que el despachante también respeta los encabezados de caducidad de caché resultantes si `enableTTL` está activado en la configuración del despachante, lo que implica que actualizará el contenido específico incluso fuera del contenido que se está republicando.

### HTML/Texto {#html-text}

* de forma predeterminada, el explorador almacena en caché durante cinco minutos, según el encabezado de control de caché emitido por la capa apache. La CDN también respeta este valor.
* se puede anular para todo el contenido HTML/Texto definiendo la `EXPIRATION_TIME` variable en `global.vars` el uso de AEM como herramienta de distribución del SDK de Cloud Service.
* se puede anular en un nivel más fino mediante las siguientes directivas apache mod_headers:

```
<LocationMatch "\.(html)$">
        Header set Cache-Control "max-age=200"
</LocationMatch>
```

Debe asegurarse de que un archivo debajo `src/conf.dispatcher.d/cache` tiene la siguiente regla (que está en la configuración predeterminada):

```
/0000
{ /glob "*" /type "allow" }
```

* Tenga en cuenta que otros métodos, incluido el proyecto [](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/)Dispatcher-ttl AEM ACS Commons, no anularán correctamente los valores.

### Bibliotecas de cliente (js, css) {#client-side-libraries}

* al utilizar el marco de trabajo de biblioteca del cliente de AEM, el código JavaScript y CSS se genera de forma que los navegadores pueden almacenarlo en caché indefinidamente, ya que cualquier cambio se manifiesta como nuevos archivos con una ruta única.  En otras palabras, el HTML que hace referencia a las bibliotecas de cliente se producirá según sea necesario para que los clientes puedan experimentar contenido nuevo a medida que se publica. El control de caché se establece en &quot;inmutable&quot; o en 30 días para los exploradores más antiguos que no respetan el valor &quot;inmutable&quot;.
* consulte la sección Bibliotecas del lado del [cliente y coherencia](#content-consistency) de la versión para obtener más detalles.

### Imágenes y cualquier contenido lo suficientemente grande como para almacenarse en el almacenamiento blob {#images}

* de forma predeterminada, no en caché
* puede establecerse a un nivel más preciso mediante las siguientes directivas de apache `mod_headers` :

```
<LocationMatch "^.*.jpeg$">
    Header set Cache-Control "max-age=222"
</LocationMatch>
```

Es necesario asegurarse de que un archivo en src/conf.dispatcher.d/cache tiene la siguiente regla (que se encuentra en la configuración predeterminada):

```
/0000
{ /glob "*" /type "allow" }
```

Asegúrese de que los recursos destinados a ser guardados en privado en lugar de en caché no forman parte de los filtros de directiva LocationMatch.

* Tenga en cuenta que otros métodos, incluido el proyecto [](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/)Dispatcher-ttl AEM ACS Commons, no anularán correctamente los valores.

### Otros tipos de archivos de contenido en el almacén de nodos {#other-content}

* sin caché predeterminada
* el valor predeterminado no se puede establecer con la `EXPIRATION_TIME` variable utilizada para los tipos de archivo html/texto
* la caducidad de la caché se puede establecer con la misma estrategia LocationMatch descrita en la sección html/text especificando el regex adecuado

## Dispatcher {#disp}

El tráfico pasa por un servidor web apache, que admite módulos, incluido el despachante. El despachante se utiliza principalmente como caché para limitar el procesamiento en los nodos de publicación con el fin de aumentar el rendimiento.

Como se describe en la sección de almacenamiento en caché de CDN, se pueden aplicar reglas a la configuración del despachante para modificar cualquier configuración de caducidad de caché predeterminada.

El resto de esta sección describe consideraciones relacionadas con la invalidación de la caché del despachante. Para la mayoría de los clientes, no debería ser necesario invalidar la caché del despachante, en lugar de depender de que el despachante actualice su caché cuando se vuelva a publicar el contenido, y de que la CDN respete los encabezados de caducidad de la caché.

### Invalidación de caché de despachante durante la Activación/desactivación {#cache-activation-deactivation}

Al igual que las versiones anteriores de AEM, la publicación o cancelación de publicaciones borrará el contenido de la caché del despachante. Si se sospecha un problema de almacenamiento en caché, los clientes deben volver a publicar las páginas en cuestión.

Cuando la instancia de publicación recibe una nueva versión de una página o recurso del autor, utiliza el agente de vaciado para invalidar las rutas adecuadas en su distribuidor. La ruta de acceso actualizada se elimina de la caché del despachante, junto con sus elementos principales, hasta un nivel (puede configurarla con el [nivel](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level)statfiles).

### invalidación explícita de la caché del despachante {#explicit-invalidation}

En general, no será necesario invalidar manualmente el contenido en el despachante, pero es posible si es necesario, tal como se describe a continuación.

Antes de AEM como servicio de nube, había dos formas de invalidar la caché del despachante.

1. Invocar el agente de replicación, especificando el agente de vaciado del despachante de publicación
2. Llamar directamente a la `invalidate.cache` API (por ejemplo, `POST /dispatcher/invalidate.cache`)

Ya no se admitirá el enfoque de la API `invalidate.cache` del despachante, ya que solo se dirige a un nodo de despachante específico. AEM como servicio de nube funciona en el nivel de servicio, no en el nivel de nodo individual, por lo que las instrucciones de invalidación de la página [Invalidar páginas en caché de AEM](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/page-invalidate.html) ya no son válidas para AEM como servicio de nube.
En su lugar, debe utilizarse el agente de vaciado de replicación. Esto se puede hacer con la API de replicación. La documentación de la API de replicación está disponible [aquí](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/Replicator.html) y para ver un ejemplo de vaciado de la caché, consulte la página [de ejemplo de la](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) API específicamente el `CustomStep` ejemplo de cómo emitir una acción de replicación de tipo ACTIVATE a todos los agentes disponibles. El extremo del agente de vaciado no se puede configurar pero está preconfigurado para que apunte al despachante, junto con el servicio de publicación que ejecuta el agente de vaciado. Normalmente, el agente de vaciado puede activarse mediante eventos o flujos de trabajo OSGi.

El diagrama que se presenta a continuación ilustra esto.

![](assets/cdnd.png "CDNCDN")

Si existe la preocupación de que la caché del despachante no se esté borrando, póngase en contacto con el servicio de asistencia [](https://helpx.adobe.com/support.ec.html) al cliente, que puede vaciar la caché del despachante si es necesario.

La CDN administrada por Adobe respeta los TTL y, por lo tanto, no es necesario vaciarla. Si se sospecha un problema, [póngase en contacto con el servicio de asistencia](https://helpx.adobe.com/support.ec.html) al cliente para que pueda vaciar una caché de CDN administrada por Adobe según sea necesario.

## Bibliotecas de cliente y coherencia de versiones {#content-consistency}

Las páginas están compuestas de HTML, JavaScript, CSS e imágenes. Se recomienda a los clientes que aprovechen el marco de bibliotecas de cliente (clientlibs) para importar recursos de JavaScript y CSS en páginas HTML, teniendo en cuenta las dependencias entre bibliotecas de JS.

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

1. Vaya al Administrador de configuración de OSGi `<host>/system/console/configMgr`
1. Busque la configuración OSGi para Adobe Granite HTML Library Manager:
   * Marque la casilla de verificación para habilitar el control estricto de versiones
   * En el campo rotulado Clave de caché del lado del cliente a largo plazo, introduzca el valor de /.*;hash
1. Guarde los cambios. Tenga en cuenta que no es necesario guardar esta configuración en el control de código fuente, ya que AEM como servicio de nube habilitará automáticamente esta configuración en entornos de desarrollo, fase y producción.
1. Cada vez que se cambia el contenido de la biblioteca del cliente, se genera una nueva clave hash y se actualiza la referencia HTML.
