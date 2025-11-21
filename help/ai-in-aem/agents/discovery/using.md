---
title: Información general de Discovery Agent
description: Aprenda a utilizar Discovery Agent para ofrecer contenido de AEM relevante bajo demanda mediante mensajes naturales y conversacionales para una experiencia de detección optimizada y sin clics.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: ab94d59ff93eb4cf29e15a8945063b8ae00c57e8
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 1%

---


# Agente de detección {#discovery-agent}

Discovery Agent ofrece contenido de AEM bajo demanda a través de mensajes naturales y conversacionales para una experiencia de detección optimizada y sin clics. Busca de forma inteligente en Assets, Fragmentos de contenido y Forms adaptable para ofrecer materiales relevantes como imágenes, vídeos, documentos de PDF, artículos y plantillas de formulario. Con el lenguaje natural, puede buscar contenido sin crear consultas complejas ni aplicar filtros en la interfaz de AEM Assets. En función de la solicitud, el agente devuelve resultados depurados junto con metadatos de recursos y direcciones URL de entrega, listos para incrustarse en otras aplicaciones.

Algunas de las ventajas clave de Discovery Agent son:

* **Detección unificada de contenido**: Acceda a todo tipo de contenido de AEM, como imágenes, vídeos, documentos de PDF, artículos y formularios, desde una sola interfaz de conversación.

* **Planificación de campañas más rápida**: Recopile rápidamente imágenes y formularios para las campañas de marketing en los canales de correo electrónico, web y social.

* **Productividad mejorada**: Reduzca el tiempo empleado en explorar repositorios o filtrar metadatos mediante búsquedas automatizadas basadas en la intención.

* **Uso coherente del contenido**: garantiza la reutilización de los recursos y fragmentos aprobados, manteniendo la coherencia de la marca en todos los canales.

>[!IMPORTANT]
>
>Las respuestas generadas por IA pueden ser inexactas o engañosas. Asegúrese de volver a comprobar las correcciones y respuestas sugeridas.
>
>Consulte también [Directrices de usuario de IA generativa de Adobe Experience Cloud](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html).

## Habilidades {#skills-discovery-agent}

El agente de detección proporciona las siguientes habilidades:

* **Detección de contenido en lenguaje natural**\
  Discovery Agent permite a los usuarios encontrar recursos, fragmentos de contenido y formularios adaptables relevantes en Adobe Experience Manager (AEM) mediante simples mensajes de lenguaje natural, sin necesidad de consultas de búsqueda complejas.

* **Descubrimiento de recursos basado en etiquetas**

  Discovery Agent utiliza indicadores en lenguaje natural para buscar recursos asociados con etiquetas específicas en el repositorio de AEM, lo que ayuda a los usuarios a acceder rápidamente al contenido organizado o no según la taxonomía de la organización.

* **Detección de contenido basado en carpetas:**\
  Discovery Agent puede identificar recursos mediante la interpretación de mensajes en lenguaje natural que hacen referencia a nombres de carpetas en AEM. Los usuarios solo pueden mencionar la carpeta en su solicitud, sin navegar manualmente por el repositorio, lo que reduce significativamente el número de clics necesarios para localizar el contenido correcto.

## Personas {#personas-discovery-agent}

### Gestores de campaña {#campaign-managers}

Discovery Agent permite a los administradores de Campaign identificar y reutilizar rápidamente contenido de confianza y de alto rendimiento para la ideación.

### Especialistas en marketing de canal {#channel-marketers}

Discovery Agent permite a los especialistas en marketing de canal encontrar de forma eficaz los recursos relevantes para crear experiencias coherentes y multicanal.

### Bibliotecarios de DAM {#dam-librarians}

Los bibliotecarios de DAM pueden marcar los recursos a los que les faltan los estándares de metadatos establecidos por la organización, lo que permite un control coherente y garantiza que los recursos permanezcan completos y listos para su uso en todos los canales.

### Agencias y socios {#agencies-partners}

Las agencias y los socios pueden encontrar fácilmente activos aprobados por la marca en Content Hub y reutilizarlos para acelerar el trabajo creativo sin salirse de los estándares de la marca.

## ¿Cómo acceder a Discovery Agent? {#access-discovery-agent}

Puede acceder a los agentes empresariales de AEM a través del asistente de IA. Inicie sesión en experience.adobe.com y podrá empezar a interactuar con el asistente de IA especificando el mensaje en lenguaje natural mediante el cuadro de búsqueda:

![Agente de detección de acceso](/help/ai-in-aem/agents/discovery/assets/access-discovery-agent.png)

Para obtener información sobre el extremo MCP para acceder a Discovery Agent, póngase en contacto con el Soporte técnico de Adobe.

## Casos de uso comunes e indicadores de ejemplo {#use-cases-prompts}

### Recursos {#discovery-agent-use-cases-assets}

**Descubrimiento de recursos basado en etiquetas**

Discovery Agent utiliza indicadores en lenguaje natural para buscar recursos asociados con etiquetas específicas en el repositorio de AEM, lo que ayuda a los usuarios a acceder rápidamente al contenido organizado según la taxonomía de su organización.

Mensaje de ejemplo:

Mostrar imágenes etiquetadas `office` en la carpeta `WKND`.

**Detección de contenido basado en carpetas:**\
Discovery Agent puede identificar recursos mediante la interpretación de mensajes en lenguaje natural que hacen referencia a nombres de carpetas en AEM. Los usuarios solo pueden mencionar la carpeta en su solicitud, sin navegar manualmente por el repositorio, lo que reduce significativamente el número de clics necesarios para localizar el contenido correcto.

Ejemplos de mensajes:

* ¿Hay algún svg en la carpeta `WKND`?
* Mostrar recursos modificados después de `Nov 1 2025` en la carpeta `WKND`.
* Enumerar `lifestyle` imágenes en la carpeta `WKND`.

**Detección de recursos basada en la resolución y el formato**

Discovery Agent puede identificar recursos que cumplen con requisitos de calidad específicos, como formato de archivo o resolución mínima, lo que permite a los usuarios localizar rápidamente imágenes de producto que estén listas para una entrega y reutilización de alta calidad en todos los canales.

Mensaje de ejemplo:

Encuentre imágenes PNG de empaquetado de productos de al menos 2000 píxeles de ancho.

**Detección de contenido basado en la orientación**

Discovery Agent puede filtrar recursos reconociendo atributos visuales, como la presencia de personas y la orientación de una imagen. Esto permite a los usuarios reducir rápidamente el contenido a los elementos visuales más relevantes sin aplicar manualmente varios filtros en AEM.

Mensaje de ejemplo:

Mostrar recursos con la persona en orientación horizontal.

### Fragmentos de contenido {#discovery-agent-use-cases-content-fragments}

Discovery Agent ayuda a los usuarios a localizar rápidamente los fragmentos de contenido adecuados al interpretar las referencias en lenguaje natural a los nombres de campañas, marcas de productos, estado de publicación y actividad de creación reciente. Permite a los equipos mostrar fragmentos listos para la campaña y ver contenido específico de la marca, todo sin examinar manualmente las carpetas o aplicar varios filtros en AEM.

Ejemplos de mensajes:

* Mostrar fragmentos de contenido para crear una campaña de ofertas WKND.

* Mostrar el fragmento de contenido para bebida americana.

* Mostrar todos los fragmentos de contenido publicados para bebidas WKND.

* Enumerar todos los fragmentos de contenido creados en las últimas 2 semanas.

### Formularios {#discovery-agent-use-cases-forms}

Discovery Agent le ayuda a encontrar rápidamente formularios adaptables mediante peticiones de datos en lenguaje natural. Busca a través del contenido del formulario y los metadatos para encontrar coincidencias basadas en las palabras clave de sus peticiones de datos. Esto significa que puede descubrir correctamente formularios relevantes aunque los términos de búsqueda no estén en el título o la descripción del formulario.

Ejemplos de mensajes:

* Mostrar todos los formularios de solicitud de préstamo.
* Busque formularios para solicitar un trabajo.
* Buscar formularios de contacto.
* Estoy buscando formularios de incorporación de empleados.
* Muéstreme los formularios de solicitud de tarjeta de crédito.

Nota: Actualmente, la detección de formularios solo admite formularios de Edge Delivery Services y la búsqueda basada en etiquetas no está disponible para formularios en este momento.

## Resultados de la búsqueda {#discovery-agent-search-results}

### Recursos {#discovery-agent-search-results-assets}

Discovery Agent devuelve los 20 resultados principales para cada consulta, ordenados por relevancia para garantizar que las coincidencias exactas aparezcan primero. El agente combina consultas impulsadas por metadatos con búsquedas semánticas para ensamblar un conjunto específico de coincidencias probables y, a continuación, utiliza un LLM para clasificarlas en función de la intención del usuario. Este enfoque combinado ofrece resultados precisos según el contexto, sin depender completamente de una coincidencia de palabra clave directa.

Cada resultado incluye un nombre de recurso junto con metadatos de recurso clave como la ruta de recurso, el creador, la fecha de creación, el título, la descripción, el formato, el último modificador, la última fecha de modificación, el tamaño de archivo, las dimensiones, la [URL de Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) y las etiquetas asociadas. Si un recurso está en estado aprobado, los resultados también incluyen [Dynamic Media con la URL de OpenAPI](/help/assets/dynamic-media-open-apis-overview.md).

Puede hacer clic en la ruta del recurso para desplazarse sin problemas a la ubicación del recurso en AEM.

![Buscar recursos mediante el agente de detección](/help/ai-in-aem/agents/discovery/assets/search-results-discovery-agent.png)

Puede utilizar estos detalles del recurso para evaluar rápidamente si un recurso cumple los requisitos sin ir a cada recurso para ver estos detalles.

>[!NOTE]
>
>El campo [URL de Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) solo se muestra en los resultados de búsqueda si el recurso está publicado y usted tiene una licencia de Dynamic Media válida. Del mismo modo, el campo [Dynamic Media con la URL de OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) solo se muestra si tiene una licencia de Dynamic Media válida y Dynamic Media con OpenAPI está habilitado para su instancia de AEM as a Cloud Service.

### Fragmentos de contenido {#discovery-agent-search-results-content-fragments}

Discovery Agent proporciona capacidades de búsqueda de texto completo para fragmentos de contenido, y devuelve los 20 mejores resultados que coinciden mejor con el mensaje especificado. Cada resultado incluye el nombre del fragmento de contenido junto con campos de metadatos clave como la ruta del fragmento de contenido, el creador, la fecha de creación, las variaciones, el último modificador y los campos de la última fecha de modificación.

![Buscar fragmentos de contenido mediante el agente de detección](/help/ai-in-aem/agents/discovery/assets/search-content-fragments-discovery-agent.png)

Puede hacer clic en la ruta del fragmento de contenido para desplazarse sin problemas a la ubicación del fragmento de contenido en AEM.

## Impulso de las prácticas recomendadas {#prompting-best-practices-discovery-agent}

Especifique detalles concisos en las indicaciones en lenguaje natural para que el agente pueda devolver resultados precisos y relevantes. Cuanto más claramente describa lo que está buscando, mejor podrá el agente refinar y reducir el resultado. Por ejemplo, puede hacer lo siguiente:

* Defina metadatos de recurso, como etiquetas, nombres de carpeta, fechas de creación, estados de publicación y nombres de autor en las peticiones de datos para filtrar recursos.

* Utilice metadatos específicos de su organización, como categorías (zapatillas, productos electrónicos), temporadas (otoño, primavera), eventos (Black Friday, lanzamiento del producto) y canales (web, correo electrónico, impresión) para filtrar aún más el contenido.

