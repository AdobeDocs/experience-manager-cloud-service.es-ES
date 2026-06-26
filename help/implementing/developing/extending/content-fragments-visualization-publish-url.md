---
title: 'Fragmentos de contenido visual: Entregar con la URL de publicación'
description: Utilice la URL de publicación para enviar fragmentos de contenido visual.
feature: Developing, Content Fragments
role: Admin, Developer
source-git-commit: 65d8d29ba13b0c5d8360aad4bc0742bd7f625922
workflow-type: tm+mt
source-wordcount: '1438'
ht-degree: 0%

---

# Fragmentos de contenido visual: enviar con la dirección URL de publicación {#visual-content-fragments-deliver-with-the-publish-url}

Cuando se publica un fragmento de contenido basado en un modelo con una o varias plantillas de HTML adjuntas, el HTML procesado de ese fragmento está disponible a través del nivel de publicación de Adobe Experience Manager (AEM) as a Cloud Service en una URL con esta estructura:

```html
https://publish-p<programId>-e<envId>.adobeaemcloud.com/adobe/stable/previewtemplates/contentFragments/<templateId>/<fragmentId>/<variation>.html
```

Esta URL devuelve un *documento HTML independiente* (que incluye CSS y estructura en línea) que se puede incrustar en cualquier contexto web.

## Técnicas de incrustación: información general {#embedding-techniques-overview}

Existen tres métodos distintos para consumir HTML a partir de un fragmento de contenido visual en una página host. Cada uno de ellos tiene características distintas en cuanto al aislamiento de estilos, el comportamiento del diseño, la accesibilidad y la complejidad.

| | Elemento en línea | iframe | Elemento personalizado + DOM de sombra |
|--- |--- |--- |--- |
| Mecanismo | `fetch()` en la dirección URL, inserte el HTML de respuesta en un `<div>` a través de `innerHTML` | `<iframe src="publishURL">` | Defina un elemento personalizado, `fetch()` para HTML, e inyéctelo en una raíz de DOM en la sombra adjunta |
| Aislamiento de estilo | Ninguno: el fragmento CSS se filtra en la página host y el CSS host afecta al fragmento | Completo: contexto de exploración independiente, aislamiento CSS completo | Fuerte: los bloques de límite DOM de la sombra alojan la cascada CSS; los estilos de fragmento permanecen encapsulados |
| Participación de diseño | Completo: el contenido forma parte del flujo normal del documento y responde al tamaño de la Estructura/cuadrícula/contenedor | Ninguno: iframe tiene dimensiones fijas; requiere un cambio de tamaño automático explícito de `width`/`height` o basado en JS | Completo: el elemento personalizado participa en el flujo normal del documento host como cualquier otro elemento DOM |
| Accesibilidad (a11y) | Óptimo: el contenido se encuentra en el árbol principal del DOM, totalmente transitable por los lectores de pantalla y la tecnología de asistencia | Moderado: el contexto de exploración independiente puede confundir la navegación del lector de pantalla; requiere el atributo `title` | Bueno: el contenido se encuentra en el mismo documento; el DOM en la sombra se puede recorrer mediante tecnologías de asistencia modernas |
| SEO | Incorrecto: el contenido cargado mediante JS `fetch()` no está indizado por la mayoría de los rastreadores | Deficiente: el contenido del iframe no se suele indexar en el contexto de la página principal | Deficiente: igual que en línea; el contenido recuperado por JS no se puede rastrear |
| JavaScript runtime | Compartido: mismo contexto de ventana/documento; riesgo de conflictos de scripts si el fragmento contiene `<script>` etiquetas | Aislado: contexto de ventana independiente; sin riesgo de colisión | Compartido: el mismo contexto de ventana pero con ámbito DOM; los scripts dentro de la raíz central se ejecutan en el contexto host. |
| Compatibilidad con orígenes cruzados | Requiere encabezados CORS en la dirección URL de publicación (el servicio los configura) | Funciona de forma nativa: los iframes cargan contenido de origen cruzado sin CORS | Requiere encabezados CORS en la dirección URL de publicación (igual que en línea) |
| Complejidad de implementación | Mínimo: algunas líneas de JS | Trivial: no se requiere JS; HTML puro | Baja: ~20 líneas de JS para la definición de elemento personalizado, reutilizable en toda la página |
| Más adecuado para | Prototipado, contenido de confianza del mismo origen, contextos en los que la integración del diseño es crítica y los conflictos de CSS son manejables | Inserción rápida, contenido en zona protegida, escenarios de origen cruzado en los que CORS no está disponible, contenido que debe estar completamente aislado | Uso en producción: equilibra el aislamiento, la participación en el diseño y la accesibilidad (recomendado para componentes principales de AEM y sitios externos). |

### Elemento en línea (fetch + innerHTML) {#inline-element-fetch-and-innerhtml}

El enfoque más sencillo:

1. Recuperación de la URL de publicación
1. inyectar HTML en un elemento contenedor

Un ejemplo de incrustación de elementos en línea:

```html
<div id="cf-container"></div>
<script>
  fetch("<publish-url>")
    .then(r => r.ok ? r.text() : Promise.reject(r.status))
    .then(html => {
      document.getElementById("cf-container").innerHTML = html;
    })
    .catch(err => console.error("Failed to load fragment", err));
</script>
```

Cuándo usar:

* Creación rápida de prototipos para páginas de prueba de concepto
* Contextos del mismo origen en los que controla tanto la página host como los estilos de fragmento
* Cuando la flexibilidad máxima del diseño es más importante que la encapsulación de estilos

>[!CAUTION]
>
>**Riesgo de colisión de CSS**
>
>Los estilos en línea del fragmento (incluidos sus bloques de `<style>`, las declaraciones de fuentes y los selectores de elementos) se combinan en la cascada de la página host.
>
>Esto puede provocar invalidaciones de estilo no deseadas en ambas direcciones.
>
>Utilice esta técnica únicamente cuando pueda tolerar o gestionar activamente estos conflictos.

### iframe {#iframe}

Cargue la dirección URL de publicación directamente como `src` de un `<iframe>`. No se necesita JavaScript.

Un ejemplo de incrustación de iframe:

```iframe
<iframe
  src="<publish-url>"
  title="Content Fragment Preview"
  width="100%"
  height="600"
  frameborder="0"
  style="border: none;"
></iframe>
```

También puede cambiar automáticamente el tamaño del iframe (esto es opcional).

Para cambiar dinámicamente el tamaño del iframe a su altura de contenido (evitando las barras de desplazamiento), utilice un patrón `postMessage` o una biblioteca apropiada.

Un ejemplo de enfoque ligero es:

```iframe
<iframe id="cf-iframe" src="<publish-url>" title="Content Fragment Preview"
  width="100%" frameborder="0" style="border:none; overflow:hidden;"
  onload="this.style.height = this.contentDocument.documentElement.scrollHeight + 'px';"
></iframe>
```

>[!WARNING]
>
>El enfoque de cambio de tamaño automático de `onload` anterior solo funciona para iframes de **same-origin**.
>
>Para las direcciones URL de publicación de **origen cruzado**, necesita una solución basada en `postMessage` o establecer una altura fija.

Cuándo usar:

* Bloque incrustado de Edge Delivery Services (la integración predeterminada; consulte la sección siguiente)
* Contextos en los que el aislamiento completo de CSS/JS es crítico
* Incrustación de origen cruzado donde CORS no está configurado
* Integración rápida con código cero (simplemente pegue la dirección URL)

### Elemento personalizado + DOM de sombra (recomendado) {#custom-element-and-shadow-dom-recommended}

Defina un elemento personalizado `<cf-visualization>` reutilizable que obtenga la URL de publicación e inserte el HTML en una raíz DOM en la sombra encapsulada.

Este elemento proporciona:

* Aislamiento del DOM de sombra
   * El marcado y los estilos del fragmento se encapsulan en una raíz en la sombra, lo que evita conflictos con la cascada CSS de la página host.
* Participación de diseño en línea
   * El contenido procesado participa en el flujo normal del documento host, respondiendo al tamaño del contenedor y a los contextos de Estructura/Cuadrícula sin gestión manual de dimensiones.
* Contexto de navegación único
   * No se crea ningún contexto de documento secundario; el contenido del fragmento comparte el tiempo de ejecución de JavaScript de la página y las tecnologías de asistencia lo pueden recorrer por completo.
* Sobrecarga mínima
   * Una sola llamada `fetch` recupera el HTML procesado previamente desde el nivel de publicación. No se requiere un marco de procesamiento del lado del cliente.

>[!IMPORTANT]
>
>Este es el enfoque recomendado para el uso en producción y es la técnica utilizada por los componentes principales de AEM.

Para definir el elemento personalizado, incluya el siguiente script una vez por página. Todas las `<cf-visualization>` instancias de la página utilizarán esta definición:

```javascript
<script>
  class CfVisualization extends HTMLElement {
    connectedCallback() {
      const src = this.getAttribute("src");
      if (!src) return;

      const shadow = this.attachShadow({ mode: "open" });

      fetch(src)
        .then((r) => (r.ok ? r.text() : Promise.reject(r.status)))
        .then((html) => {
          shadow.innerHTML = html;
        })
        .catch((err) => {
          console.error("cf-visualization: failed to load", src, err);
        });
    }
  }

  if (!customElements.get("cf-visualization")) {
    customElements.define("cf-visualization", CfVisualization);
  }
</script>
```

Para utilizar el elemento personalizado:

```html
<cf-visualization src="<publish-url>"></cf-visualization>
```

Cuándo usar:

* Páginas de AEM Sites que utilizan componentes principales (este es el comportamiento integrado)
* Sitios web externos/de terceros que necesitan una integración limpia y reutilizable
* Cualquier contexto en el que necesite aislamiento de estilos y participación en el flujo de diseño

## Integración con Edge Delivery Services (bloque incrustado) {#integration-with-edge-services-embed-block}

En Edge Delivery Services, la dirección URL de publicación se consume a través de un **[bloque incrustado](https://sidekick-library--aem-block-collection--adobe.aem.page/tools/sidekick/library.html?plugin=blocks&path=/block-collection/embed&index=0)**, que lo procesa como un `<iframe>`.

1. Asegúrese de que el bloque incrustado exista en el proyecto.

   Si el proyecto EDS aún no incluye el bloque incrustado, cópielo del repositorio de recopilación de bloques de aem:

   ```cmdline
   # From the aem-block-collection repo, copy blocks/embed/ into your project's blocks/ directory
   cp -r aem-block-collection/blocks/embed/ your-eds-project/blocks/embed/
   ```

1. Crear la incrustación en el editor de creación de documentos (en Edge Delivery Services)

   En Document Authoring, los bloques se representan como tablas. Para agregar una incrustación de fragmento de contenido visual:

   | incrustar |
   |--- |
   | (pegue la URL de publicación como hipervínculo) |

   Alternativamente, si el proyecto o Sidekick está configurado con el bloque Incrustar en su biblioteca de bloques, puede insertarlo mediante el menú de barra diagonal y pegar la URL de publicación en el contenido del bloque.

1. Resultado

   El bloque incrustado procesa la dirección URL de publicación dentro de un `<iframe>`. El contenido del fragmento se carga en aislamiento CSS completo dentro del diseño de página EDS.

## Integración: AEM Sites con componentes principales {#integration-aem-sites-with-core-components}

El componente principal Fragmento de contenido (`core/wcm/components/contentfragment/v1/contentfragment`) tiene compatibilidad integrada para representar fragmentos de contenido visual mediante la técnica [Elemento del cliente + DOM de sombra](#custom-element-and-shadow-dom-recommended).

Cómo funciona:

* Modo de autor:

  Cuando `displayMode` del componente está establecido en `vcf`, la clientlib de creación (`vcfRenderer.js`) recupera el HTML del fragmento de la API de vista previa y lo procesa en línea en el lienzo de creación.

  Un ejemplo de punto final de vista previa de autor es:

  ```html
  GET /adobe/sites/cf/fragments/{fragmentId}/preview?templateId={templateId}&variation={variation}
  ```

* Modo de publicación:

  En la página publicada (`wcmmode.disabled`), la plantilla HTL procesa un script en línea que se obtiene de la dirección URL de publicación e inserta la HTML en una raíz DOM en la sombra.

  Un ejemplo de fragmento de contenido visual del componente principal (templates.html):

  ```html
  <div class="cmp-contentfragment cmp-contentfragment--vcf"
     data-cmp-contentfragment-id="{fragmentId}"
     data-cmp-contentfragment-vcf-template="{templateId}"
     data-cmp-contentfragment-variation="{variation}">
    <!-- Only rendered when wcmmode.disabled (publish) -->
    <div data-vcf-url="{vcfPublishUrl}" class="cmp-contentfragment__vcf-loader" style="display:none"></div>
    <script>
        (function() {
            var script = document.currentScript;
            var loader = script.previousElementSibling;
            var el = script.parentElement;
            if (!el || !loader) return;
            var url = loader.dataset.vcfUrl;
            if (!url) return;
            loader.remove();
            var shadow = el.attachShadow({ mode: "open" });
            var body = document.createElement("body");
            body.style.display = "none";
            shadow.appendChild(body);
            fetch(url)
                .then(function(r) { return r.ok ? r.text() : Promise.reject(r.status); })
                .then(function(html) {
                    body.innerHTML = html;
                    body.style.display = "";
                });
        })();
    </script>
  </div>
  ```

  Formato de URL de publicación:

  El modelo Sling (`ContentFragmentImpl`) crea la dirección URL de publicación con el siguiente patrón:

  ```html
  /adobe/experimental/previewtemplates-expires-20260301/contentFragments/{templateId}/{fragmentId}/{variation}.html
  ```

  Esta URL relativa se resuelve en el host de publicación durante la ejecución.

## Integración con sitios externos {#integration-with-external-sites}

Para los sitios web que no son de AEM, use la técnica [Elemento del cliente + DOM de sombra](#custom-element-and-shadow-dom-recommended). Esto le proporciona una integración declarativa y limpia sin dependencias de marco de trabajo.

Un ejemplo es:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Product Page</title>
</head>
<body>
  <h1>Product Details</h1>
  <p>Some host-page content here...</p>

  <!-- Embed the Content Fragment visualization -->
  <cf-visualization
    src="https://publish-p12345-e67890.adobeaemcloud.com/adobe/experimental/previewtemplates-expires-20260301/contentFragments/product_template/abc-123/master.html"
  ></cf-visualization>

  <p>More host-page content below the fragment...</p>

  <!-- Custom Element definition (include once) -->
  <script>
    class CfVisualization extends HTMLElement {
      connectedCallback() {
        const src = this.getAttribute("src");
        if (!src) return;
        const shadow = this.attachShadow({ mode: "open" });
        fetch(src)
          .then(r => r.ok ? r.text() : Promise.reject(r.status))
          .then(html => { shadow.innerHTML = html; })
          .catch(err => console.error("cf-visualization: failed to load", src, err));
      }
    }
    if (!customElements.get("cf-visualization")) {
      customElements.define("cf-visualization", CfVisualization);
    }
  </script>
</body>
</html>
```

>[!NOTE]
>
>Puede colocar varios elementos `<cf-visualization>` en la misma página con distintas direcciones URL `src`. La definición del elemento personalizado solo debe incluirse una vez.

## CORS y consideraciones de seguridad {#cors-and-security-considerations}

| Inquietud | Detalles |
|--- |--- |
| CORS | El servicio de visualización de fragmentos de contenido configura CORS en la ruta `/adobe/**` con orígenes permitidos configurables.<br>Las técnicas [Elemento en línea (fetch + innerHTML)](/help/implementing/developing/extending/content-fragments-visualization-publish-url.md#inline-element-fetch-and-innerhtml) 1 y [Elemento cliente + Shadow DOM](/help/implementing/developing/extending/content-fragments-visualization-publish-url.md#custom-element-and-shadow-dom-recommended) (que utilizan `fetch()`) requieren que el origen de la página host esté en la lista de permitidos. <br>La técnica [iFrame](/help/implementing/developing/extending/content-fragments-visualization-publish-url.md#iframe) no requiere CORS. |
| CSP/X-Frame-Options | El servicio no establece encabezados de `Content-Security-Policy` o `X-Frame-Options` en el HTML publicado. Si la CDN o Dispatcher agregan estos encabezados, compruebe que permiten el acceso de tramas (para [iFrame](/help/implementing/developing/extending/content-fragments-visualization-publish-url.md#iframe)) o `fetch()` (para DOM en línea/en la sombra) desde los orígenes del host. |
| Confianza de contenido | El HTML publicado se procesa previamente a partir de los datos de fragmento de contenido creados usando [plantillas Handlebars](/help/implementing/developing/extending/content-fragments-visualization-templates.md) administradas por el servicio. No incluye scripts generados por el usuario. Sin embargo, al igual que con cualquier inyección de HTML interno, asegúrese de confiar en el origen. |

### Elija la técnica adecuada {#choose-the-appropriate-technique}

Utilice lo siguiente como guía de decisión para ayudarle a elegir la técnica adecuada:

| Escenario | Solución |
|--- |--- |
| ¿Necesita JavaScript cero y aislamiento total? | Iframe |
| ¿Necesita participación en el flujo de diseño con aislamiento de estilo? | Elemento personalizado + DOM de sombra (recomendado) |
| ¿Necesita el prototipo más rápido, el mismo origen y los conflictos de CSS son aceptables? | Elemento en línea |
| ¿Incrustar en Edge Delivery Services? | Bloque de incrustación (iframe debajo del capó) |
| ¿Incrustar en páginas de AEM Sites? | Componente principal (DOM en la sombra, integrado) |


## Recursos adicionales {#additional-resources}

Hay recursos adicionales disponibles:

* [Documentación de fragmentos de contenido de AEM](/help/sites-cloud/administering/content-fragments/overview.md)

<!-- CQDOC-23650 - add link when docs are stable; not experimental -->

<!--
* [Content Fragment Visualization Templates APIs (experimental)](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/sites/cvt/#)
-->
