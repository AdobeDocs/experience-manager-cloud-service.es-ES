---
title: Agente de detección de contenido
description: Aprenda a utilizar el agente de detección de contenido para ofrecer contenido de AEM relevante bajo demanda mediante mensajes naturales y conversacionales para una experiencia de detección optimizada y sin clics.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: 676300cd-b799-4c53-a58e-043e58a2cbc5
source-git-commit: 45c547a0a7372e5ebe23bd6b816798cd3b225872
workflow-type: tm+mt
source-wordcount: '2066'
ht-degree: 0%

---


# Agente de detección de contenido {#discovery-agent}

Como parte de [Content Advisor Agent de AEM,](/help/ai-in-aem/agents/content-advisor/overview.md) el agente de detección de contenido ofrece contenido de AEM bajo demanda mediante mensajes naturales y conversacionales para una experiencia de detección ágil y sin clics. Busca de forma inteligente en Assets, fragmentos de contenido, páginas de AEM Sites y Forms adaptable para ofrecer materiales relevantes como imágenes, vídeos, documentos de PDF, artículos y plantillas de formulario. Con el lenguaje natural, puede buscar contenido sin crear consultas complejas ni aplicar filtros en la interfaz de AEM Assets. En función de la solicitud, el agente devuelve resultados depurados junto con metadatos de recursos y direcciones URL de entrega, listos para incrustarse en otras aplicaciones.

Algunas de las ventajas clave del agente de detección de contenido son:

* **Detección unificada de contenido**: Acceda a todo tipo de contenido de AEM, como imágenes, vídeos, documentos de PDF, artículos, páginas y formularios, desde una sola interfaz de conversación.

* **Planificación de campañas más rápida**: Recopile rápidamente imágenes y formularios para las campañas de marketing en los canales de correo electrónico, web y social.

* **Productividad mejorada**: Reduzca el tiempo empleado en explorar repositorios o filtrar metadatos mediante búsquedas automatizadas basadas en la intención.

* **Uso coherente del contenido**: garantiza la reutilización de los recursos y fragmentos aprobados, manteniendo la coherencia de la marca en todos los canales.

>[!VIDEO](https://video.tv.adobe.com/v/3479983)

>[!IMPORTANT]
>
>Las respuestas generadas por IA pueden ser inexactas o engañosas. Asegúrese de volver a comprobar las correcciones y respuestas sugeridas.
>
>Consulte también [Directrices de usuario de IA generativa de Adobe Experience Cloud.](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html)

## Habilidades {#skills-discovery-agent}

El agente de detección de contenido ofrece las siguientes habilidades:

* **Detección de contenido en lenguaje natural**

  El agente de detección de contenido permite a los usuarios encontrar recursos relevantes, fragmentos de contenido, formularios adaptables y páginas de AEM Sites en Adobe Experience Manager (AEM) mediante simples mensajes de lenguaje natural, sin necesidad de consultas de búsqueda complejas.

* **Detección de recursos basados en metadatos**

  El agente de detección de contenido utiliza peticiones de datos en lenguaje natural para buscar recursos en función de los metadatos disponibles para los recursos en AEM. Los usuarios pueden detectar recursos mediante metadatos como etiquetas, ID de correo electrónico del autor o el editor, fechas de publicación o modificación, tipo MIME, tipo de recurso, estado, propiedades de metadatos personalizadas definidas en formularios de metadatos en la vista Assets o Admin, etc. Consulte [Casos de uso comunes e indicadores de ejemplo](#use-cases-prompts) para obtener una lista completa.

  También puede combinar varios filtros de metadatos en una sola solicitud para restringir los resultados de búsqueda.

* **Detección de contenido basado en carpetas:**\
  El agente de detección de contenido puede identificar recursos mediante la interpretación de peticiones de datos en lenguaje natural que hacen referencia a nombres de carpetas en AEM. Los usuarios solo pueden mencionar la carpeta en su solicitud, sin navegar manualmente por el repositorio, lo que reduce significativamente el número de clics necesarios para localizar el contenido correcto.

## Personas {#personas-content-discovery}

### Gestores de campaña {#campaign-managers}

El agente de detección de contenido permite a los administradores de campañas identificar y reutilizar rápidamente contenido de confianza y de alto rendimiento para su ideación.

### Especialistas en marketing de canal {#channel-marketers}

El agente de detección de contenido permite a los especialistas en marketing de canal encontrar de forma eficaz los recursos relevantes para crear experiencias coherentes y multicanal.

### Bibliotecarios de DAM {#dam-librarians}

Los bibliotecarios de DAM pueden marcar los recursos a los que les faltan los estándares de metadatos establecidos por la organización, lo que permite un control coherente y garantiza que los recursos permanezcan completos y listos para su uso en todos los canales.

### Agencias y socios {#agencies-partners}

Las agencias y socios pueden encontrar fácilmente activos aprobados por la marca dentro de Content Hub y reutilizarlos para acelerar el trabajo creativo sin salirse de los estándares de la marca.

## Cómo acceder a {#access}

Puede acceder al agente de detección de contenido en AEM mediante el asistente de IA. Inicie sesión en [`experience.adobe.com`](https://experience.adobe.com) y podrá empezar a interactuar con el Asistente de IA especificando el mensaje en lenguaje natural mediante el cuadro de búsqueda:

![Acceder al agente de detección de contenido](/help/ai-in-aem/agents/content-advisor/assets/access-discovery-agent.png)

Para obtener información sobre el extremo MCP para acceder al agente de detección de contenido, póngase en contacto con el Soporte técnico de Adobe.

## Casos de uso comunes e indicadores de ejemplo {#use-cases-prompts}

### Recursos {#discovery-agent-use-cases-assets}

**Detección de recursos basados en metadatos**

El agente de detección de contenido utiliza peticiones de datos en lenguaje natural para buscar recursos en función de los metadatos disponibles para los recursos en AEM. Los usuarios pueden descubrir los recursos mediante las siguientes propiedades de metadatos: Etiquetas, Creado por ID de correo electrónico, Modificado por ID de correo electrónico, Publicado por ID de correo electrónico, Fecha de creación, Fecha de modificación, Fecha de publicación, Tipo de MIME, Tipo de recurso, Estado, formato de archivo, tamaño de archivo, anchura de imagen, altura de imagen y varios filtros de metadatos en una sola solicitud.

El agente de detección de contenido también busca en las propiedades personalizadas disponibles en los esquemas de metadatos la vista Administrador y los formularios de metadatos de la vista Assets. Puede modificar los indicadores según corresponda para buscar los valores disponibles en esas propiedades de recursos personalizadas.

>[!NOTE]
>
>Para mejorar el rendimiento de la detección, indexe las propiedades de metadatos personalizadas relevantes. Las propiedades indexadas permiten al agente recuperar el contenido coincidente más rápido cuando los usuarios incluyen esas propiedades en sus indicadores.


Ejemplos de mensajes:

* **Búsqueda basada en etiquetas**: mostrar imágenes etiquetadas `office` en la carpeta `WKND`.
* **Buscar según el formato de archivo, el tipo de recurso, el estado del recurso y Publicado por el id. de correo electrónico**: mostrar imágenes en formato `.PNG` que sean `approved` y `published by <user email ID>`.
* **Buscar según el formato de archivo, el tipo de recurso, el estado del recurso y el ID creado por correo electrónico**: mostrar vídeos en formato `.mp4` que se hayan aprobado y `created by <user email ID>`.
* **Buscar según el formato de archivo, el tipo de recurso, el estado del recurso y la fecha de creación**: mostrar imágenes en formato `.PNG` creadas después del 1 de enero de 2025 y el `published by <user email ID>`
* **Búsqueda basada en el tipo MIME, la fecha de creación y la publicación por el ID de correo electrónico**: mostrar `image/jpeg` creado después de `January 1, 2025` y `published by <user email ID>`.
* **Buscar según el formato de archivo y las propiedades de metadatos personalizadas**: mostrar imágenes en formato `.JPEG` que tienen `Product SKU ID as <SKU value>`.

* **Buscar recursos sin metadatos**: mostrar los recursos creados en los últimos 90 días con `<Name of metadata property including custom properties>` está en blanco.

* **Busque recursos usando el tamaño de archivo, el ancho de imagen y el alto de imagen**: Muestre imágenes de más de 5 MB con un ancho superior a 2000 píxeles y un alto superior a 1200 píxeles.


**Detección de contenido basado en carpetas:**\
El agente de detección de contenido puede identificar recursos mediante la interpretación de peticiones de datos en lenguaje natural que hacen referencia a nombres de carpetas en AEM. Los usuarios solo pueden mencionar la carpeta en su solicitud, sin navegar manualmente por el repositorio, lo que reduce significativamente el número de clics necesarios para localizar el contenido correcto.

Ejemplos de mensajes:

* ¿Hay algún svg en la carpeta `WKND`?
* Mostrar recursos modificados después de `Nov 1 2025` en la carpeta `WKND`.
* Enumerar `lifestyle` imágenes en la carpeta `WKND`.

**Preguntas adicionales para habilitar la detección de contenido basado en carpetas**

Cuando se incluye un nombre de carpeta en una solicitud (sin la ruta de acceso completa del recurso), Content Discovery Agent busca primero una carpeta coincidente en la ruta de acceso raíz `/content/dam/<folder-name>`.

Si no se encuentra una carpeta coincidente en el nivel raíz, el agente sugiere rutas de carpeta alternativas en las que el nombre de carpeta especificado existe en el repositorio. Esto ayuda a los usuarios a identificar rápidamente la ubicación correcta sin explorar manualmente la estructura de carpetas.

Por ejemplo, no se encontró la ruta `/content/dam/<folder-name>`. ¿Querías decir uno de estos?

* Opción 1

* Opción 2

**Descubrimiento de recursos basado en formato**

El agente de detección de contenido puede identificar recursos que cumplen con requisitos de calidad específicos, como el formato de archivo, lo que permite a los usuarios localizar rápidamente imágenes de productos listas para su distribución y reutilización de alta calidad en todos los canales.

Mensaje de ejemplo:

Busque imágenes PNG de empaquetado de productos.

**Detección de contenido basado en la orientación**

El agente de detección de contenido puede filtrar recursos reconociendo atributos visuales, como la presencia de personas y la orientación de una imagen. Esto permite a los usuarios reducir rápidamente el contenido a los elementos visuales más relevantes sin aplicar manualmente varios filtros en AEM.

Mensaje de ejemplo:

Mostrar recursos con la persona en orientación horizontal.

**Expandiendo resultados de búsqueda**

Content Discovery Agent devuelve los 20 resultados más relevantes por tipo de contenido para una solicitud. Si hay disponibles resultados coincidentes adicionales, los usuarios pueden solicitar el siguiente conjunto si escriben un mensaje de seguimiento como `show me more`. A continuación, el agente recupera el siguiente conjunto de resultados de la búsqueda original, lo que permite a los usuarios explorar progresivamente conjuntos de resultados más grandes sin restringir el mensaje.

**Buscando recursos similares**

El agente de detección de contenido permite a los usuarios encontrar recursos similares a un resultado específico devuelto en los resultados de búsqueda. Una vez que el agente muestre los resultados principales de una solicitud, puede solicitar recursos similares haciendo referencia a la posición de un elemento en la lista de resultados. Por ejemplo, un mensaje como `find assets similar to the 3rd result` indica al agente que identifique y devuelva otros recursos relevantes relacionados con ese elemento. Esto ayuda a los usuarios a descubrir rápidamente el contenido relacionado sin crear un nuevo mensaje de búsqueda.

**Ordenando resultados de búsqueda**

El agente de detección de contenido permite a los usuarios ordenar los resultados de búsqueda directamente según sus indicaciones en lenguaje natural. Los usuarios pueden especificar criterios de ordenación, como fecha de modificación, fecha de creación o nombre del recurso, y elegir orden ascendente o descendente.

Ejemplos de mensajes:

* Buscar imágenes de montaña ordenadas por fecha de modificación en orden descendente (muestra primero los recursos modificados más recientemente).

* Mostrar imágenes de montaña ordenadas por nombre en orden ascendente (muestra los nombres de imagen que comienzan por la letra A primero seguida por B, etc.).

### Páginas de AEM Sites {#content-discovery-agent-aem-sites-pages}

El agente de detección de contenido ayuda a los usuarios a localizar rápidamente páginas relevantes de AEM Sites mediante la interpretación de indicaciones en lenguaje natural que hacen referencia a temas de páginas, campañas u otras palabras clave contextuales. El agente realiza una búsqueda de texto completo basada en las palabras clave del mensaje para identificar las páginas coincidentes en el repositorio de AEM, lo que elimina la necesidad de examinar manualmente la estructura de Sites.

Indicadores de ejemplo:

* Encuentre todas las páginas de AEM Sites para la campaña de verano.

* Busque páginas de AEM Sites con una temática de café.

### Fragmentos de contenido {#discovery-agent-use-cases-content-fragments}

Content Discovery Agent ayuda a los usuarios a localizar rápidamente los fragmentos de contenido adecuados mediante la interpretación de referencias en lenguaje natural a nombres de campañas, marcas de productos, estados de publicación y actividades de creación recientes. Permite a los equipos mostrar fragmentos listos para la campaña y ver contenido específico de la marca, todo sin examinar manualmente las carpetas o aplicar varios filtros en AEM.

Ejemplos de mensajes:

* Mostrar fragmentos de contenido para crear una campaña de ofertas WKND.

* Mostrar el fragmento de contenido para bebida americana.

* Mostrar todos los fragmentos de contenido publicados para bebidas WKND.

* Enumerar todos los fragmentos de contenido creados en las últimas 2 semanas.

### Formularios {#discovery-agent-use-cases-forms}

El agente de detección de contenido le ayuda a encontrar rápidamente formularios adaptables mediante peticiones de datos en lenguaje natural. Busca a través del contenido del formulario y los metadatos para encontrar coincidencias basadas en las palabras clave de sus peticiones de datos. Esto significa que puede descubrir correctamente formularios relevantes aunque los términos de búsqueda no estén en el título o la descripción del formulario.

Ejemplos de mensajes:

* Mostrar todos los formularios de solicitud de préstamo.
* Busque formularios para solicitar un agente.
* Buscar formularios de contacto.
* Estoy buscando formularios de incorporación de empleados.
* Muéstreme los formularios de solicitud de tarjeta de crédito.

Nota: Actualmente, la detección de formularios solo admite formularios de Edge Delivery Services y la búsqueda basada en etiquetas no está disponible para formularios en este momento.

## Resultados de la búsqueda {#discovery-agent-search-results}

### Recursos {#discovery-agent-search-results-assets}

El agente de detección de contenido devuelve los resultados principales de cada consulta, ordenados por relevancia para garantizar que las coincidencias exactas aparezcan primero. El agente combina consultas impulsadas por metadatos con búsquedas semánticas para ensamblar un conjunto específico de coincidencias probables y, a continuación, utiliza un LLM para clasificarlas en función de la intención del usuario. Este enfoque combinado ofrece resultados precisos según el contexto, sin depender completamente de una coincidencia de palabra clave directa.

Cada resultado incluye un nombre de recurso junto con metadatos de recurso clave como la ruta de recurso, el creador, la fecha de creación, el título, la descripción, el formato, el último modificador, la última fecha de modificación, el tamaño de archivo, las dimensiones, la [URL de Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) y las etiquetas asociadas. Si un recurso está en estado aprobado, los resultados también incluyen [Dynamic Media con la URL de OpenAPI](/help/assets/dynamic-media-open-apis-overview.md).

Puede hacer clic en la ruta del recurso para desplazarse sin problemas a la ubicación del recurso en AEM.

![Buscar recursos mediante el agente de detección de contenido](/help/ai-in-aem/agents/content-advisor/assets/search-results-discovery-agent.png)

Puede utilizar estos detalles del recurso para evaluar rápidamente si un recurso cumple los requisitos sin ir a cada recurso para ver estos detalles.

>[!NOTE]
>
>El campo [URL de Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) solo se muestra en los resultados de búsqueda si el recurso está publicado y usted tiene una licencia de Dynamic Media válida. Del mismo modo, el campo [Dynamic Media con la URL de OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) solo se muestra si tiene una licencia de Dynamic Media válida y Dynamic Media con OpenAPI está habilitado para su instancia de AEM as a Cloud Service.

### Fragmentos de contenido {#discovery-agent-search-results-content-fragments}

El agente de detección de contenido proporciona funciones de búsqueda de texto completo para fragmentos de contenido y devuelve los resultados principales que mejor coinciden con el mensaje especificado. Cada resultado incluye el nombre del fragmento de contenido junto con campos de metadatos clave como la ruta del fragmento de contenido, el creador, la fecha de creación, las variaciones, el último modificador y los campos de la última fecha de modificación.

![Buscar fragmentos de contenido mediante el agente de detección de contenido](/help/ai-in-aem/agents/content-advisor/assets/search-content-fragments-discovery-agent.png)

Puede hacer clic en la ruta del fragmento de contenido para desplazarse sin problemas a la ubicación del fragmento de contenido en AEM.

## Prácticas recomendadas de solicitud {#prompting-best-practices-discovery-agent}

Especifique detalles concisos en las indicaciones en lenguaje natural para que el agente pueda devolver resultados precisos y relevantes. Cuanto más claramente describa lo que está buscando, mejor podrá el agente refinar y reducir el resultado. Por ejemplo, puede hacer lo siguiente:

* Defina metadatos de recurso, como etiquetas, nombres de carpeta, fechas de creación, estados de publicación y nombres de autor en las peticiones de datos para filtrar recursos.

* Utilice metadatos específicos de su organización, como categorías (zapatillas, productos electrónicos), temporadas (otoño, primavera), eventos (Black Friday, lanzamiento del producto) y canales (web, correo electrónico, impresión) para filtrar aún más el contenido.

## Limitaciones {#limitations-discovery-agent}

* El agente de detección de contenido admite peticiones de datos basadas en dimensiones únicamente para tipos de formato de imagen y SVG. Por ejemplo, `Find images wider than 1080px`.

* Los administradores de Content Hub pueden acceder al agente de detección de contenido a través del portal de Content Hub; sin embargo, los resultados solo se recuperan de la instancia de autor de AEM. Actualmente, los usuarios de Content Hub Limited no pueden disfrutar de las ventajas de Content Discovery Agent (disponible próximamente).

* La función Buscar similares solo funciona para imágenes con [mejoras en las etiquetas inteligentes](/help/assets/ai-generated-metadata-assets-view.md).
