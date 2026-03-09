---
title: Guía de solicitud del agente de modernización de Experience
description: En esta guía se proporcionan sugerencias para solicitar información de forma eficaz sobre Experience Modernization Agent y se describe lo que hacen sus habilidades.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: e2a9c55644c0d9542f6a299f0df30a3dfd4a55de
workflow-type: tm+mt
source-wordcount: '2696'
ht-degree: 0%

---


# Guía de solicitud del agente de modernización de Experience {#prompting-guide}

Experience Modernization Agent selecciona automáticamente la aptitud adecuada en función de las solicitudes en lenguaje natural. En esta guía se proporcionan sugerencias para conseguir una respuesta eficaz y se describe lo que hacen las aptitudes.

## Sugerencias generales {#general-tips}

### Algunas habilidades dependen de los resultados de otras habilidades. {#dependency}

* Dado que la importación masiva necesita la infraestructura de importación que crea la migración de páginas, migre al menos una página antes de ejecutar la importación masiva.
* Dado que el bloque CSS hace referencia a los tokens de diseño globales, complete el diseño de todo el sitio antes de aplicar estilo a bloques individuales.

### La IA sigue flujos de trabajo estructurados y formulará preguntas aclaratorias cuando necesite más información. {#workflows}

* Confíe en el proceso y responda a estas preguntas de calificación a medida que surjan.
* No intente cargar al principio todos los requisitos en el mensaje inicial.

### Cree archivos de marcado en el proyecto para documentar reglas, directrices, decisiones de diseño o restricciones específicas del proyecto. {#markdown-files}

* Estos archivos de marcado (por ejemplo, INSTRUCTIONS.md, CONTEXT.md) pueden incluir convenciones de nomenclatura de archivos, reglas de asignación de contenido o directrices de marca.
* Al iniciar una nueva conversación, pídale al agente que &quot;se caliente leyendo la documentación del proyecto&quot; para que cargue este contexto antes de continuar con las tareas.

### La ventana de contexto del agente no es infinita. {#limited-window}

* Durante las conversaciones largas, las instrucciones anteriores pueden compactarse u olvidarse.
* Si el agente parece haber perdido el contexto, recuérdele los puntos clave o borre la conversación y comience de nuevo con un mensaje de calentamiento para leer la documentación del proyecto.

### Utilice mensajes iterativos para restringir los resultados. {#iterate}

* Si algo no se ve bien (por ejemplo, color de fondo incorrecto en un bloque), pídale al agente que corrija el problema específico en lugar de empezar de nuevo.

## Habilidades de creación y migración de sitios {#site-migration}

El Agente de modernización de sitios ofrece muchas habilidades para crear nuevos sitios de Edge Delivery Services y migrar sitios web existentes. Cualquier nuevo sitio de Edge Delivery o proyecto de migración debe aprovechar estas habilidades.

### Migración de un sitio o una página a AEM {#migrate-a-site}

Utilice este mensaje cuando migre contenido de un sitio web existente a Edge Delivery Services.

#### Indicadores de ejemplo {#example-migrate}

* &quot;Migrar esta página: `https://example.com/about`
* &quot;Migrar estas páginas: URL1, URL2, URL3&quot;

#### Qué se debe saber {#wtk-migrate}

* La migración sigue un flujo de trabajo de siete pasos:
   1. El agente analiza la página de origen.
   1. Identifica la estructura de la sección.
   1. Realiza el análisis de creación.
   1. Asigna el contenido a variantes de bloque.
   1. Genera Markdown.
   1. Crea una infraestructura de importación.
   1. Previsualiza el resultado.
* El agente analiza las páginas utilizando una jerarquía de dos niveles:
   * Primero identifica los límites de la sección (cambios de fondo, desplazamientos de espaciado)
   * Luego identifica las secuencias de contenido dentro de cada sección.
* El análisis de creación sigue el modelo de [David.](https://www.aem.live/docs/davidsmodel)
   * Para cada secuencia de contenido, primero comprueba &quot;¿Puede un autor crear esto escribiendo normalmente?&quot;
   * Se prefiere el contenido predeterminado (encabezados, párrafos, listas e imágenes en línea) sobre los bloques.
* El agente intenta reutilizar bloques existentes de la biblioteca de bloques del repositorio antes de crear nuevos bloques.
   * Cuando el contenido no se puede asignar a un bloque existente, crea nuevas variantes de bloque.
   * Puede solicitar cambios, solicitar nuevas variantes o ajustar asignaciones de forma interactiva.
* Las variantes de bloque se rastrean con metadatos.
   * Al migrar varias páginas, el agente carga primero las variantes personalizadas existentes y las vuelve a utilizar cuando el estilo coincide (umbral de similitud del 70 % basado en el propósito, los colores, la tipografía, el espaciado y el diseño).
* El encabezado, la navegación y el pie de página se excluyen de la migración de páginas. Estas se gestionan mediante habilidades dedicadas.
* Cada migración crea una infraestructura de importación (plantillas de página, analizadores de bloques, transformadores) para futuras importaciones masivas.

### Importación masiva {#bulk-import}

Use este mensaje para importar muchas páginas de la misma plantilla después de completar una [migración inicial de una sola página.](#migrate-a-site)

#### Indicadores de ejemplo {#example-prompts-bulk-import}

* &quot;Ejecute la importación masiva en estas páginas: URL1, URL2, URL3&quot;.
* &quot;Ejecutar importación masiva en todas las páginas de productos&quot;.
* &quot;Importación masiva de estas páginas de blog: URL1, URL2&quot;.

#### Qué se debe saber {#wtk-bulk-import}

* La importación masiva depende de la infraestructura de importación creada durante una migración anterior de una sola página.
   * Esto incluye plantillas de página (estructura de sección), transformadores (limpieza DOM de todo el sitio) y analizadores (conversión de HTML a tabla específica del bloque).
* Debe migrar al menos una página representativa por plantilla antes de ejecutar la importación masiva.
* La importación masiva reutiliza la estructura y las asignaciones establecidas durante la migración de una sola página.
   * No deduce las plantillas desde cero.
* Los transformadores funcionan en todo el DOM antes y después del análisis. Los analizadores funcionan en el nivel de bloque individual.
* Todos los analizadores se validan antes de continuar con la importación masiva.
* Una plantilla corresponde a una configuración de importación masiva.
   * No se admite la combinación de plantillas en una sola ejecución.

#### Flujo de trabajo típico {#typical-workflow}

El flujo de trabajo recomendado es iterativo: primero realice la validación en un conjunto pequeño y, a continuación, amplíe.

1. **Ejecute primero una migración de una sola página.** - Migre una página representativa para la plantilla que planea importar en lotes.
   * Esto crea la infraestructura de importación necesaria.
1. **Ejecute la importación masiva en un pequeño conjunto de páginas.**: pida al agente que ejecute la importación masiva y proporcione una breve lista de direcciones URL que sigan la misma plantilla.
1. **Revise y perfeccione los resultados.** - Inspeccionar las páginas importadas.
   * Si algo parece incorrecto, pídale al agente que ajuste los analizadores, los transformadores o la lógica de importación.
1. **Aumentar escala.** - Cuando los resultados parezcan correctos, proporcione la lista completa de direcciones URL.
   * El agente reutilizará la misma lógica de importación y ejecutará la importación masiva a escala.

### Raspado de páginas web {#scraping-webpages}

Utilice este mensaje para extraer contenido, metadatos e imágenes de una URL de origen para su análisis o migración.

#### Indicadores de ejemplo {#example-scraping}

* &quot;Rasque esta página para su análisis: `https://example.com`&quot;
* &quot;Extraer contenido de `https://example.com/product`&quot;

#### Qué se debe saber {#wtk-scraping}

* Esta solicitud suele invocarse automáticamente como el primer paso de la migración de páginas.
* El contenido oculto mediante CSS se captura en si está presente en el DOM.
* Las imágenes cargadas de forma diferida y el contenido procesado del lado del cliente se gestionan desplazándose por la página en Chromium sin encabezado y dejando que se ejecuten los scripts.
* Las imágenes WebP/AVIF/SVG se convierten a PNG por compatibilidad.
* Se extraen los metadatos, incluidos el título, la descripción, las etiquetas de Open Graph, los datos estructurados JSON-LD y la URL canónica.
* Las imágenes en DOM son fijas.
   * la imagen de fondo se convierte en img.
   * Los elementos de imagen están desajustados
   * srcset se ha resuelto en src
   * Las direcciones URL relativas se convierten en absolutas
   * Los SVG en línea que se van a convertir en archivos img.
* Se generan rutas de documentos saneadas (en minúsculas sin extensión `.html`).
* Se obtienen los siguientes resultados:
   * `screenshot.png`
   * `cleaned.html` (sin scripts/estilos)
   * `metadata.json`
   * Carpeta `images/` con copias locales
* Los usuarios pueden preguntar por las dimensiones de la captura de pantalla y solicitar tamaños de dispositivo específicos (móvil, escritorio) para la extracción de contenido.
* La extracción de contenido en varios puntos de interrupción aumenta el tiempo de procesamiento.

### Migración de diseño {#design-migration}

Utilice este mensaje para extraer y aplicar el diseño visual de un sitio de origen a Edge Delivery Services.

#### Indicadores de ejemplo {#example-design}

* &quot;Migrar el diseño de `https://example.com`&quot;
* &quot;Extraer tokens de diseño&quot;
* &quot;Estilo del bloque de héroe&quot;

#### Qué se debe saber {#wtk-design}

* La migración del diseño tiene dos fases:
   1. La fase 1 (en todo el sitio) extrae lo siguiente en `styles/styles.css`:
      * Paleta de colores global y colores de énfasis
      * Sistema tipográfico (fuentes, tamaños, pesos)
      * Sistema de espaciado (relleno, márgenes, espacios)
      * Fondos de sección (claro, oscuro, de color)
      * Estilos de componente base (botones, vínculos e imágenes)
      * Salidas a
   1. La fase 2 migra estilos de bloque individuales y crea CSS específicos de bloque en `/blocks/{name}/{name}.css`.
* El estilo de bloque (fase 2) requiere que el diseño de todo el sitio (fase 1) se complete primero.
   * El sistema de diseño global proporciona propiedades personalizadas de CSS que bloquean la referencia a.
* Tiempo estimado:
   * Fase 1: 5-10 minutos
   * Fase 2: 10 a 15 minutos
* Las solicitudes ambiguas completan la migración de forma predeterminada (ambas fases).

### Crítica de bloques {#block-critique}

Utilice este mensaje para validar y perfeccionar bloques migrados individuales y garantizar la precisión visual con el sitio web original.

#### Indicadores de ejemplo {#example-block-critique}

* &quot;Bloque de héroes de la crítica&quot;
* &quot;Validar tarjetas personalizadas de bloque&quot;

#### Qué se debe saber {#wtk-block-critique}

* La crítica de bloques compara un bloque migrado con su origen y aplica correcciones CSS de forma iterativa hasta que se logra un 85% de similitud visual o se completan tres iteraciones.
* La aptitud requiere que el bloque se haya creado primero mediante la migración de páginas.
* Una crítica de bloque sigue un flujo de trabajo de seis pasos:
   1. Captura el bloque original de la página de origen mediante un selector XPath.
   1. Inicializa la sesión de crítica.
   1. Inspecciona el bloque original (capturas de pantalla, estilos, HTML).
   1. Inspecciona el bloque migrado.
   1. Compara elementos y genera una puntuación de similitud con correcciones CSS.
   1. Aplica correcciones y vuelve a inspeccionar hasta que se alcanza el objetivo del 85 %.
* Cada iteración muestra un informe crítico completo con todas las diferencias, aplica todas las correcciones CSS (priorizadas por el impacto visual), verifica en la vista previa, vuelve a inspeccionar y muestra las métricas de mejora.
* Use la crítica de bloque una vez completada la [migración de diseño](#design-migration).

### Crítica de página {#page-critique}

Utilice este mensaje para validar páginas migradas completas para la fidelidad visual de página completa con el sitio web original.

#### Indicadores de ejemplo {#example-page-critique}

* &quot;Crítica de la página Acerca de&quot;
* &quot;Validar la página migrada con `https://example.com/about`&quot;

#### Qué se debe saber {#wtk-page-critique}

* Crítica de página realiza una comparación visual de página completa entre la página original y la migrada, iterando hasta alcanzar un objetivo de similitud del 85 % o hasta completar tres iteraciones.
* Una crítica de página tiene un flujo de trabajo de cinco pasos:
   1. Inicializa una sesión crítica.
   1. Inspecciona todos los elementos de la página original.
   1. Inspecciona todos los elementos de la página migrada.
   1. Compara y genera una puntuación de similitud con correcciones CSS priorizadas.
   1. Aplica correcciones y vuelve a inspeccionar hasta que se alcanza el objetivo del 85 %.
* Una crítica de página necesita la dirección URL de la página de origen y la ruta migrada (por ejemplo, &quot;/about&quot;) como entrada.
* Utilice la crítica de página al validar la fidelidad general de la página o validar varios bloques simultáneamente.
* [Use la crítica de bloque](#block-critique) para la validación centrada en componentes específicos.
* Se recomienda el siguiente flujo de trabajo:
   1. Migrar una página.
   1. Aplique un diseño.
   1. Ejecutar una crítica de bloques en bloques de claves
   1. Ejecute una crítica de página de la aplicación para una validación completa.

### Migración de bloques Figma {#figma-block-migration}

Utilice este mensaje para migrar un bloque del diseño Figma a Edge Delivery Services.

Tenga en cuenta que debe configurar los detalles de Figma en [la consola de modernización de la experiencia](/help/ai-in-aem/agents/brand-experience/modernization/console.md) para utilizar esta solicitud.

#### Indicadores de ejemplo {#example-figma}

* &quot;Migrar el bloque `https://figma.com/design/{fileKey}?node-id={nodeId}` a Edge Delivery Services&quot;
* &quot;Migrar `{blockName}` de `https://figma.com/file/{fileKey}` a Edge Delivery Services&quot;

#### Qué se debe saber {#wtk-figma}

* Esta aptitud migra bloque a bloque, no páginas completas o archivos Figma completos.
* Para obtener los mejores resultados:
   * Seleccione el bloque específico que desea migrar en Figma y copie su vínculo (con `node-id`) o nombre.
   * Proporcione el parámetro `node-id` en la dirección URL para establecer como objetivo el bloque exacto.
* Al ejecutar esta aptitud, los siguientes pasos se realizan automáticamente en el entorno alojado:
   1. **Detección de estructuras de bloques**: el agente lee el nodo Figma para comprender las capas y los componentes.
   1. **Extracción de estilos global**: el agente extrae colores, tipografía y espaciado en `styles/styles.css` como propiedades personalizadas de CSS (tokens de diseño).
   1. **Creación de estilos específica del bloque**: el agente crea propiedades personalizadas CSS adicionales específicas del bloque que se está migrando.
   1. **Asignación a bloques existentes**: el agente identifica el bloque coincidente más cercano en la biblioteca de bloques del proyecto y crea una variante personalizada.
   1. **Generación de CSS**: el agente escribe estilos que hacen referencia a las propiedades personalizadas de CSS extraídas, lo que garantiza la coherencia del diseño.
   1. **Descarga de recursos**: el agente guarda imágenes e iconos de Figma en el espacio de trabajo del entorno alojado.
   1. **Generación de contenido de Edge Delivery Services**: el agente crea el archivo Markdown siguiendo la estructura de bloques EDS
   1. **Validación de salida**: el agente obtiene una vista previa del resultado y realiza una comparación visual con el diseño Figma original.
* La aptitud lee primero los metadatos (paso 1) para comprender la estructura y, a continuación, extrae el contexto de diseño detallado (pasos 2-5).
   * Este enfoque por fases evita problemas con archivos Figma grandes o complejos.
* Esta aptitud adopta un enfoque centrado en los estilos.
   * Todos los estilos se extraen como propiedades personalizadas de CSS (tokens de diseño) antes de escribir cualquier CSS.
   * Esto garantiza que el bloque migrado sea coherente con el sistema de diseño.
* La solicitud requiere la dirección URL de Figma (con `fileKey` y `node-id` opcional) o una clave de archivo de Figma directamente como entrada.

### Configuración de navegación {#navigation-setup}

Utilice este mensaje para configurar o migrar la navegación del sitio.

#### Indicadores de ejemplo {#example-navigation}

* &quot;Configurar la navegación desde `https://example.com`&quot;
* &quot;Corregir el menú de navegación&quot;

#### Qué se debe saber {#wtk-navigation}

* La navegación de Edge Delivery Services exige una estructura de tres secciones (aplicada por `header.js`):
   1. **Marca** (sección 1): logotipo y vínculo de marca principal
   1. **Secciones** (sección 2): menú de navegación principal con desplegables opcionales
   1. **Herramientas** (sección 3): vínculos de utilidad (suscripción, inicio de sesión, carro de compras)
* El contenido de navegación se encuentra en `nav.md`, en el directorio raíz.
* Las secciones están separadas por marcadores (`---`).
* Los elementos en negrita (`**Text**`) con listas anidadas crean listas desplegables.
* Los vínculos en la navegación pueden representarse como botones debido al comportamiento de ajuste automático de Document Authoring.
   * El bloque de encabezado incluye código para eliminar las clases de botón de los vínculos de navegación.

## Bloquear capacidades de desarrollo {#block-development-capabilities}

Estos indicadores se utilizan para crear y desarrollar bloques, proporcionando un valor continuo más allá de la creación inicial del sitio o la migración.

### Desarrollo de bloques {#block-development}

Utilice esta solicitud para crear bloques nuevos o modificar los existentes.

#### Indicadores de ejemplo {#example-block-development}

* &quot;Crear un bloque de testimonios&quot;
* &quot;Añadir una variante de fondo de vídeo al bloque a pantalla completa&quot;

#### Qué se debe saber {#wtk-block-development}

* El agente sigue el desarrollo impulsado por contenido (CDD), un proceso obligatorio para todo el desarrollo de Edge Delivery Services.
   * Preguntará por los modelos de contenido y probará el contenido antes de escribir el código.
* La filosofía del CD es que las necesidades del autor van antes que las del desarrollador.
   * Los modelos de contenido deben ser intuitivos para los autores, incluso si eso significa un código de decoración más complejo.
* La creación del contenido de prueba primero proporciona:
   * Capacidad de pruebas inmediatas
   * Vínculos de validación PR para comprobaciones PSI
   * Documentación viva para autores
   * Descubrimiento de casos excepcionales que no se tienen en cuenta los enfoques de código primero
* El agente buscará bloques similares en [Colección de bloques](https://www.aem.live/developer/block-collection) y [Grupo de bloques](https://www.aem.live/developer/block-party/) antes de implementarlos, para encontrar patrones y código reutilizable.
* Omita el CDD solo para ajustes triviales solo de CSS (pero identifique el contenido de prueba para su validación).

### Modelado de contenido {#content-modeling}

Utilice este mensaje para diseñar la estructura de tabla con la que trabajan los autores al crear contenido de bloque.

#### Indicadores de ejemplo {#example-modeling}

* &quot;Diseño de un modelo de contenido para un bloque de testimonios&quot;
* &quot;¿Cuál es el mejor modelo de contenido para este carrusel?&quot;

#### Qué se debe saber {#wtk-modeling}

* Edge Delivery Services tiene cuatro tipos de modelos canónicos:
   * **Independiente:** Elementos visuales/narrativos distintos (hero, blockquote)
      * Tabla única con contenido de bloque
   * **Colección:** Contenido semiestructurado repetido (tarjetas, carrusel)
      * Tabla con patrón de fila repetida
   * **Configuración:** contenido dinámico o controlado por API donde se muestran los controles de configuración (lista de blogs, resultados de búsqueda)
      * Tabla con filas de configuración clave-valor.
   * **Bloqueo automático:** Estructuras complejas que los autores crean como secciones/contenido predeterminado y luego se transforman (pestañas, incrustaciones de YouTube)
* Hay un límite de cuatro celdas por fila.
   * Agrupe los elementos relacionados en celdas.
* Para las diferencias de estilo, prefiera las variantes de bloque sobre las celdas de configuración.
* [Seguir la ley de Postel](https://en.wikipedia.org/wiki/Robustness_principle): Sea flexible con la estructura de entrada.
   * Un bloque a pantalla completa debe funcionar tanto si el contenido está en una celda, dividido en dos celdas o en filas independientes.
* Esta aptitud suele ser invocada automáticamente por el desarrollo impulsado por contenido durante la creación del bloque.

### Búsqueda de bloques de referencia {#reference-blocks}

Utilice este mensaje para buscar implementaciones existentes y utilizarlas como puntos de partida.

#### Indicadores de ejemplo {#example-reference}

* &quot;Buscar bloques similares a una tabla de precios&quot;
* &quot;¿Qué bloques están disponibles para los testimonios?&quot;
* &quot;Buscar grupo de bloques para una implementación de pestañas&quot;

#### Qué se debe saber {#wtk-reference}

* La [Colección de bloques](https://www.aem.live/developer/block-collection) se ha mantenido y analizado en Adobe por sus prácticas recomendadas, su excelente modelado de contenido, su alto rendimiento y su accesibilidad.
   * Se limita a bloques que se necesitan con frecuencia. Empiece aquí.
* [Block Party](https://www.aem.live/developer/block-party/) es impulsado por la comunidad y ofrece una variedad más amplia que incluye enfoques experimentales.
   * También incluye complementos de barra de tareas, herramientas de compilación (webpack, vite, sass) e integraciones.
   * Utilícelo cuando la colección de bloques no tenga lo que necesita.
* Piense en nombres alternativos al buscar
   * FAQ = acordeón
   * Galería = carrusel/presentación
   * Navegación = menú/encabezado
* La Parte del bloque sólo devuelve entradas aprobadas o revisadas.

### Buscando documentación {#searching-documentation}

Utilice este mensaje para encontrar información sobre las funciones de Edge Delivery Services o las directrices de implementación.

#### Indicadores de ejemplo {#example-documentation}

* &quot;¿Cómo implemento la carga diferida en Edge Delivery Services?&quot;
* &quot;Buscar metadatos de sección en los documentos&quot;

#### Qué se debe saber {#wtk-documentation}

* Busca específicamente en la documentación de [aem.live](https://aem.live) (documentos y publicaciones de blog).
* Utilice palabras clave específicas (&quot;decoración de bloques&quot;,&quot;complemento de barra de tareas&quot;,&quot;metadatos&quot;) en lugar de términos genéricos (&quot;aem&quot;,&quot;sitio web&quot;,&quot;cómo compilar&quot;).
* Para ejemplos de código e implementaciones de referencia, utilice &quot;buscar bloques de referencia&quot; en su lugar.
* Los diez resultados más relevantes devueltos de forma predeterminada.

### Pruebas {#testing}

Utilice este mensaje para validar los cambios del código antes de abrir una solicitud de extracción.

#### Indicadores de ejemplo {#example-testing}

* &quot;Probar el nuevo bloque de tarjetas&quot;
* &quot;Ejecute las pruebas antes de abrir una PR&quot;

#### Qué se debe saber {#wtk-testing}

* Las pruebas siguen una filosofía de &quot;valor frente a coste&quot; en la que se crean y mantienen pruebas cuando su valor supera el coste.
   * Las **pruebas de mantenimiento** (pruebas unitarias) son para utilidades con gran lógica, procesamiento de datos e integraciones de API. Son regresiones rápidas, fáciles de mantener y capturadas en el código reutilizado.
   * **Las pruebas de rendimiento** (pruebas del explorador) son para transformaciones DOM y validación visual. Utilice para validar la implementación, capturar capturas de pantalla para la revisión de PR y luego descartar.
* Las pruebas de desecho entran en `test/tmp/` y prueban contenido en `drafts/tmp/` (ambas ignoradas).
* Antes de abrir una PR, asegúrese de lo siguiente:
   * Las pruebas existentes se superan
   * Las pruebas unitarias se escriben para la nueva lógica
   * La validación del explorador ha finalizado
   * Se prueban todas las variantes
   * Se ha verificado el comportamiento interactivo
   * Pasadas de entintado

### Depuración {#debugging}

Utilice este mensaje para solucionar problemas con bloques, imágenes, CSS o vista previa.

#### Indicadores de ejemplo {#example-debugging}

* &quot;Depurar por qué las imágenes se muestran como :error&quot;
* &quot;Corregir que el bloque a pantalla completa no se procese&quot;
* &quot;¿Por qué no se muestran mis cambios en la vista previa?&quot;

#### Qué se debe saber {#wtk-debugging}

* Los problemas comunes tienen patrones conocidos:
   * **Imágenes que muestran &quot;about:error&quot;**: generalmente falta la llamada `createOptimizedPicture` en el bloque JS, o se llama antes de la reestructuración del DOM
   * **Bloques que no se representan**: Compruebe el formato del nombre del bloque en Markdown y compruebe que el bloque tiene `.js` y `.css` archivos en `blocks/`.
   * **CSS no se carga**: compruebe las rutas de archivo, compruebe que el archivo CSS existe y compruebe la ficha Red en el explorador.
   * **Los cambios no aparecen**: La sincronización de código tarda de 3 a 5 segundos. Actualice (Ctrl+Mayús+R).
* El agente comprueba cada capa de forma sistemática:
   1. Archivos Source
   1. Salida procesada
   1. Código de bloque
   1. Consola del explorador
* El agente puede comprobar las vistas previas locales en `http://localhost:3000`.
