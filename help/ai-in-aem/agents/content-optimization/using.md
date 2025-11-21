---
title: Agente de optimización de contenido
description: Aprenda a utilizar el agente de optimización de contenido para transformar la forma en que los usuarios refinan y adaptan los recursos mediante la aplicación de instrucciones en lenguaje natural para crear variaciones preparadas para el canal.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: ab94d59ff93eb4cf29e15a8945063b8ae00c57e8
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 0%

---


# Agente de optimización de contenido {#content-optimization-agent}

El agente de optimización de contenido transforma la forma en que los usuarios refinan y adaptan los recursos mediante la aplicación de instrucciones en lenguaje natural para crear variaciones preparadas para el canal. Tanto si genera nuevas representaciones como si ajusta las propiedades visuales, cambia los fondos o prepara recursos para canales digitales específicos, el agente interpreta la intención del usuario y realiza automáticamente tareas de edición complejas. Funciona sin problemas con Discovery Agent, tomando los recursos que encuentra y produciendo variaciones optimizadas usando [Dynamic Media principal con capacidades OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) que satisfacen los requisitos de marca, canal y campaña sin esfuerzo manual de diseño.

Algunas de las ventajas clave de la optimización de contenido son:

* **Transformación de recursos sin esfuerzo**: convierte mensajes conversacionales sencillos en operaciones de imagen precisas, como cambiar el tamaño, el enfoque, la duplicación o el cambio de color, lo que elimina la necesidad de herramientas de edición especializadas.

* **Salidas optimizadas para el canal**: produce rápidamente representaciones adaptadas para plataformas específicas como historias de Instagram, banners web u otros puntos de contacto de marketing, lo que garantiza que los recursos estén listos para su uso inmediato.

* **Mejora de Creative a escala**: Aplica ajustes y mejoras visuales, como cambios de fondo o superposiciones gráficas, para admitir flujos de trabajo creativos de gran volumen sin ralentizar a los equipos.

* **[Colaboración perfecta con Discovery Agent](/help/ai-in-aem/agents/discovery/using.md)**: se basa en los recursos identificados por Discovery Agent, lo que permite la recuperación y optimización de recursos de un extremo a otro a través de una conversación natural.

>[!IMPORTANT]
>
>Las respuestas generadas por IA pueden ser inexactas o engañosas. Asegúrese de volver a comprobar las correcciones y respuestas sugeridas.
>
>Consulte también [Directrices de usuario de IA generativa de Adobe Experience Cloud](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html).

## Requisitos previos {#prerequisites-content-optimization-agent}

Para generar variaciones u optimizaciones para los recursos de imagen. Debe tener:

* Una licencia válida de Dynamic Media

* Dynamic Media con OpenAPI habilitado en el entorno de AEM as a Cloud Service.

* Los recursos en [estado aprobado](/help/assets/manage-organize-assets-view.md#manage-asset-status) en su entorno de AEM as a Cloud Service.


## Habilidades {#skills-content-optimization-agent}

El agente de optimización de contenido proporciona las siguientes habilidades:

* **Comprenda la intención a través del lenguaje natural**

  El agente de optimización de contenido interpreta la intención del usuario a partir de las indicaciones del lenguaje natural, teniendo en cuenta el contexto de canal, campaña y audiencia para determinar las acciones de optimización más relevantes.

* **Genera variantes de contenido dinámico**

  El agente de optimización de contenido crea variantes optimizadas como direcciones URL dinámicas adaptadas a diferentes canales y tipos de formato.

* **Optimiza el contenido de la imagen**

  El Agente de optimización de contenido aplica mejoras como conversión de formato, ajustes de resolución, recorte y enfoque para mejorar la calidad de la imagen.

* **Optimización de recursos de múltiples variantes**

  El agente de optimización de contenido puede generar varias variaciones de imagen optimizadas a partir de los recursos devueltos por el agente de detección utilizando un único mensaje en lenguaje natural, lo que permite a los usuarios producir representaciones preparadas para el canal de forma rápida y eficaz.

## Personas {#personas-content-optimization-agent}

Los especialistas en marketing de canal, la persona clave para el agente de optimización de contenido, pueden seleccionar el contenido de origen de alta resolución adecuado y solicitar formatos optimizados adaptados a sus canales y segmentos de audiencia.

Los especialistas en marketing regional y los trabajadores de la agencia también pueden utilizar el agente de optimización de contenido para generar rápidamente variaciones de imagen preparadas para el canal que admitan una producción de contenido más rápida y coherente.


## ¿Cómo acceder al agente de optimización de contenido? {#access-content-optimization-agent}

Puede acceder a los agentes empresariales de AEM a través del asistente de IA. Inicie sesión en experience.adobe.com y podrá empezar a interactuar con el Asistente de IA especificando el mensaje en lenguaje natural mediante el campo `Ask AI Assistant anything`:

![Agente de detección de acceso](/help/ai-in-aem/agents/discovery/assets/access-discovery-agent.png)

## Casos de uso comunes e indicadores de ejemplo {#use-cases-prompts}

Use las solicitudes de optimización de contenido buscando los recursos adecuados en [Discovery Agent](/help/ai-in-aem/agents/discovery/using.md). Una vez que aparecen las imágenes relevantes, los usuarios pueden generar variantes optimizadas o específicas del canal para uno o varios recursos directamente a partir de los resultados de búsqueda. Este flujo de trabajo garantiza entradas de alta calidad y mejores resultados de optimización de forma consistente. [Ver la lista completa de optimizaciones disponibles](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/).

* **Creación de representación de alta resolución**

  El agente puede generar nuevas representaciones de un recurso con una resolución y un nivel de calidad especificados, lo que facilita la preparación de variaciones preparadas para el canal sin necesidad de realizar ediciones manuales.


  Mensaje de ejemplo:

  Crear una representación de `2000px` como `JPEG` con la calidad `80%`.

  Busque el recurso correcto mediante [Discovery agent](/help/ai-in-aem/agents/discovery/using.md) y, a continuación, utilice las indicaciones siguientes en caso de que se produzcan varios resultados de búsqueda:

  Para el tercer resultado de búsqueda, cree una representación de `2000px` como `JPEG` con la calidad `80%`.

  OR

  Para `Asset ID`, genere una representación de 2000px como `JPEG` con la calidad `80%`

* **Mejora de imagen**

  El agente puede aplicar mejoras visuales, como el enfoque, para garantizar que los recursos tengan un aspecto nítido y bien definido antes de utilizarse en todas las campañas.

  Mensaje de ejemplo:

  Enfocar la imagen.


* **Ajustes de color de fondo**

  El agente puede actualizar o reemplazar los colores de fondo en recursos transparentes, admitiendo esquemas de color específicos de la marca o temas visuales impulsados por campañas.

  Mensaje de ejemplo:

  Cambiar el color de fondo de `PNG` a `#ff8932`.

* **Transformaciones de orientación**

  El agente puede voltear o reflejar imágenes para alinearlas con las necesidades de diseño o la dirección creativa, sin requerir herramientas de edición externas.

  Mensaje de ejemplo:

  Reflejar la imagen horizontalmente.

* **Representaciones optimizadas para el canal**

  El agente puede producir representaciones adaptadas a los requisitos específicos de la plataforma, como Historias de Instagram, lo que garantiza que los recursos cumplan automáticamente las directrices de formato, proporción y calidad.

  Mensaje de ejemplo:

  Crear una representación para un artículo de `Instagram`.

* **Superposiciones de marcas y generación compuesta**

  El agente puede aplicar gráficos promocionales, superposiciones o distintivos a recursos existentes con una colocación precisa, lo que permite la creación rápida de compuestos listos para su campaña.

  Mensaje de ejemplo:

  Superponga la imagen con `30%` gráficos de descuento sobre el titular promocional, colocándolo `100px` desde el centro.

  >[!NOTE]
  >
  >Las posiciones de superposición pueden no ser precisas.


## Resultados de optimización {#content-optimization-agent-results}

Cuando especifica un mensaje de optimización, el agente de optimización de contenido devuelve el recurso mejorado junto con cómodas opciones de acceso basadas en el tipo de recurso:

* **Imágenes**: La respuesta incluye una vista previa en miniatura y opciones para abrir la URL de Dynamic Media o descargar la imagen optimizada.

* **Documentos de PDF**: la respuesta incluye una vista previa en miniatura y opciones para abrir la dirección URL de Dynamic Media o descargar el archivo optimizado.

* **Vídeos**: La respuesta proporciona opciones para abrir la dirección URL de Dynamic Media o descargar el vídeo optimizado.

![Resultados de optimización de contenido](/help/ai-in-aem/agents/content-optimization/assets/download-content-optimization.png)

Estos resultados facilitan la revisión de la salida optimizada y su uso inmediato en todos los canales o flujos de trabajo descendentes.

<!--


## Prompting best Practices {#prompting-best-practices-content-optimization-agent}

The following are some of the prompting best practices:

* Be explicit about the enhancement you want the Content Optimization Agent to apply. Clearly state the transformation or adjustment you expect. Precise instructions help the agent produce accurate and predictable results. For example, Instead of `Make it good quality`, specify `Create a JPEG image with 90% quality`.

* Provide detailed parameters whenever possible. The more context you give, such as dimensions, format, quality, placement, or color values, the more tailored the output is.

-->
