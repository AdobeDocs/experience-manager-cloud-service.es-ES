---
title: Edge Side incluye
description: La CDN administrada por Adobe ahora es compatible con Edge Side Includes (ESI), un lenguaje de marcado para el ensamblado de contenido web dinámico a nivel de Edge.
feature: Dispatcher
exl-id: 35093477-2788-4f69-80a9-899f43567cae
role: Admin
source-git-commit: d70a8030ca6687b1839adc0ce1becdf366ec7170
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Edge Side incluye {#edge-side-includes}

La velocidad de entrega de contenido se beneficia de almacenar las páginas en caché de forma agresiva, lo que se logra mediante la configuración de encabezados de caché con valores de tiempo de vida (TTL) altos. Esto puede resultar difícil cuando las páginas incluyen contenido dinámico, que debe actualizarse con frecuencia o que es posible que no se pueda almacenar en caché. Afortunadamente, hay estrategias en las que la página del HTML contenedor se puede almacenar en caché con un TTL alto, lo que aplaza la captura de los fragmentos de contenido más dinámicos para un momento posterior, ya sea mediante JavaScript del lado del cliente o en la CDN. Este último enfoque es un estándar denominado Edge AEM Side Includes (ESI), que es compatible con los sitios procesados con la publicación de la. El HTML incluye etiquetas ESI que indican a la CDN que aplace el servicio de la página al explorador hasta que evalúe esas etiquetas y recupere contenido adicional más dinámico (TTL inferior) del origen (o la caché de CDN si su TTL no ha caducado).

Algunos casos de uso en los que Edge Side Includes puede resultar útil:

* Mostrar el nombre de un usuario final u otra información que sea única para un usuario final.
* Mostrar una lista de información reciente, como artículos de noticias o precios de acciones.

## Sintaxis ESI {#esi-syntax}

La sintaxis de ESI es la siguiente, si una página principal `/content/page.html` incluye un fragmento `content/snippets/mysnippet.html`.

```
<html>
  <head>
      <title>My Site</title>
  </head>
  <body>
    <div id="content">
      <esi:include src="/content/snippets/mysnippet.html" />
    </div>
  </body>
</html>
```

Consulte la [especificación ESI](https://www.w3.org/TR/esi-lang/) para obtener detalles.

### Consideraciones {#esi-syntax-considerations}

* Se admiten las siguientes etiquetas ESI: incluir, comentar, eliminar.
* Las etiquetas ESI se procesan en la CDN de forma secuencial en lugar de simultánea, por lo que muchas etiquetas ESI de una página con TTL bajos pueden añadir latencia a la experiencia del usuario final.
* La profundidad máxima de ESI: incluir procesamiento es 5.
* El máximo total de ESI: incluir fragmentos de procesamiento es de 256.


## Configuración de Apache {#esi-apache}

Si tiene páginas con etiquetas ESI, debe declarar las siguientes propiedades en la configuración de Apache:

```
<LocationMatch "/parent-pages/*content/page.html">
   # disable dispatcher compression
   SetEnv no-gzip 1
   # enable esi processing 
   Header set x-aem-esi "on"
   # enable edgeCDN compression
   Header set x-aem-compress "on"

   # typically the main page is cached at the CDN
   Header always set Cache-Control "max-age=300"
 </LocationMatch>


<LocationMatch "/content/snippets/mysnippet.html">
  SetEnv no-gzip 1

  # typically the included page is either set to a lower TTL than the parent page, or not cached at all, as these 2 commented declarations show, respectively:
  #Header always set Cache-Control "no-cache"
  #Header always set Cache-Control "max-age=50"
 </LocationMatch> 
```

Las propiedades configuradas tienen el siguiente comportamiento:

| Propiedad | Comportamiento |
|-----------|--------------------------|
| **no-gzip** | Si se establece en 1, la página HTML se transmite de Apache a la CDN sin comprimir. Esto es necesario para ESI, ya que el contenido debe enviarse a CDN sin comprimir para que CDN pueda ver y evaluar las etiquetas ESI.<br/><br/>Tanto la página principal como los fragmentos incluidos deben establecer no-gzip en 1.<br/><br/>Esta configuración anula cualquier configuración de compresión que Apache podría haber utilizado de otra manera, según los valores `Accept-Encoding` de la solicitud. |
| **x-aem-esi** | Si se establece en &quot;activado&quot;, la CDN evaluará las etiquetas ESI de la página del HTML principal.  De forma predeterminada, el encabezado no está establecido. |
| **x-aem-compress** | Si se establece en &quot;Activado&quot;, la CDN comprimirá el contenido de la CDN al explorador. Dado que la transmisión de la página principal de Apache a CDN debe estar sin comprimir para que ESI funcione (`no-gzip` establecido en 1), esto puede reducir la latencia.<br/><br/>Si no se establece este encabezado, cuando la red de distribución de contenido (CDN) recupere contenido del origen sin comprimir, también servirá contenido al cliente sin comprimir. Por lo tanto, es necesario establecer este encabezado si `no-gzip` está establecido en 1 (requerido para ESI) y se desea servir contenido comprimido desde la CDN al explorador. |

## Sling Dynamic Include {#esi-sdi}

Aunque no es obligatorio, [Sling Dynamic Include](https://sling.apache.org/documentation/bundles/dynamic-includes.html) (SDI) se puede usar para generar fragmentos de ESI que se interpretan en la CDN.
