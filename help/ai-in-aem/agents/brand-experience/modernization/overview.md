---
title: Información general de Experience Modernization Agent
description: Descubra cómo Experience Modernization Agent incorpora nuevos sitios web en Edge Delivery Services con la ayuda de IA.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: c23a6f55-2ba8-4290-b7e8-06cad5de0fc8
source-git-commit: 84fed5a82d6c23cd51d9796eb644121c6ef06a29
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 0%

---


# Información general de Experience Modernization Agent {#experience-modernization-agent}

Descubra cómo Experience Modernization Agent incorpora sitios web en Edge Delivery Services con la ayuda de IA.

## Introducción {#introduction}

[Como parte de Brand Experience Agent,](/help/ai-in-aem/agents/brand-experience/overview.md) Experience Modernization Agent acelera la incorporación a Edge Delivery Services al automatizar las migraciones de sitios web y la configuración de sitios básicos.

Combina [habilidades de creación y migración del sitio](#creation-migration) para la incorporación inicial al sitio web y [capacidades de desarrollo de bloques](#block-development) para admitir la creación del sitio y los flujos de trabajo de migración. Además, ofrece la [consola de modernización de experiencias](#console) como un entorno de desarrollo asistido por IA basado en la web disponible directamente para usted. Aunque los usuarios pueden operar el agente directamente a través de esa consola, los desarrolladores conservan el control total sobre lo que se envía.

Para migraciones complejas o de alta prioridad, Adobe ofrece el modelo de entrega de [ingeniero de resultados del agente (AOE)](#aoe-delivery), un servicio dirigido por ingenieros y diseñado para ofrecer sitios de Edge Delivery listos para la producción mediante Experience Modernization Agent.

## Ventajas {#benefits}

Experience Modernization Agent acelera el tiempo de obtención de valor para la adopción de [Edge Delivery Services](/help/edge/overview.md) y le ofrece la agilidad para adaptar la experiencia web de su marca.

* **Alta velocidad**: la automatización de IA administra el trabajo de migración repetitiva (importación de contenido, asignación de bloques, aplicación de sistema de diseño), comprimiendo las escalas de tiempo de migración en comparación con los enfoques tradicionales
* **Centrada en la eficiencia**: la automatización reduce el trabajo repetitivo, lo que permite a los equipos centrarse en el trabajo de implementación de mayor valor
* **Accesible para cualquier persona**: Las solicitudes en lenguaje natural hacen que los cambios en el sitio web sean accesibles para los usuarios menos técnicos, con vista previa en vivo para validar los cambios al instante
* **Gobernanza empresarial**: los desarrolladores mantienen una autoridad total sobre lo que se activa a través de los flujos de trabajo de revisión integrados con GitHub
* **Flexibilidad posterior a la migración**: permite a los equipos ampliar y perfeccionar los sitios migrados mediante patrones de Edge Delivery Services

## Habilidades de creación y migración de sitios {#creation-migration}

Experience Modernization Agent ofrece habilidades para crear nuevos sitios de Edge Delivery Services y migrar sitios web existentes. Se recomienda utilizar estas habilidades en cualquier nuevo sitio o migración de Edge Delivery Services.

* Acelera la creación de sitios web y las migraciones de meses a semanas o días, lo que reduce drásticamente el tiempo de respuesta para la adopción de Edge Delivery Services
* Admite migraciones de una amplia gama de plataformas CMS, AEM heredados o sistemas de diseño (como Figma) a proyectos Edge Delivery Services con capacidad de producción
* Admite prácticas recomendadas para el rendimiento, la accesibilidad y el diseño interactivo, en consonancia con las directrices de Edge Delivery Services

Las habilidades detalladas incluyen migración de páginas, importación masiva, extracción de diseño, configuración de navegación y raspado web.

## Bloquear capacidades de desarrollo {#block-development}

Experience Modernization Agent aprovecha las funciones generales de desarrollo de Edge Delivery Services que sirven a diversas tareas de desarrollo, proporcionando un valor continuo más allá de la creación o migración inicial del sitio.

* Sigue la metodología de desarrollo impulsado por contenido (CDD) para modelos de contenido de fácil creación
* Aprovecha [Block Collection](https://www.aem.live/developer/block-collection) y [Block Party](https://www.aem.live/developer/block-party/) para encontrar implementaciones de referencia y prácticas recomendadas
* Admite flujos de trabajo de prueba y depuración para validar cambios antes de la implementación

Las funciones detalladas incluyen desarrollo de bloques, modelado de contenido, detección de bloques de referencia, pruebas y depuración.

## Consola de modernización de Experience {#console}

El agente de modernización de experiencias proporciona un entorno de desarrollo asistido por IA basado en la web para Edge Delivery Services, expuesto como interfaz web en [`aemcoder.adobe.io`.](https://aemcoder.adobe.io)

* La consola no requiere ninguna configuración local para que los usuarios empiecen a solicitar cambios inmediatamente en lenguaje natural.
* Realice rápidamente tareas diarias de desarrollo de experiencias mientras previsualiza mediante la vista previa en directo de AEM y sincroniza el contenido con AEM.
* La consola admite la administración empresarial a través de flujos de trabajo de revisión estándar de GitHub.

La consola de modernización de experiencias de autoservicio suele estar disponible. Los usuarios interesados pueden solicitar acceso para garantizar una experiencia de incorporación fluida.

Empiece a usar la consola de modernización de Experience Platform

* Si está modernizando su sitio mediante la creación de documentos de destino, [comience aquí.](/help/ai-in-aem/agents/brand-experience/modernization/getting-started.md)
* Si está modernizando su sitio mediante la creación de AEM de destino, [comience aquí.](/help/ai-in-aem/agents/brand-experience/modernization/getting-started-aem-authoring.md)

## Ingeniero de resultados del agente (AOE) Delivery {#aoe-delivery}

Para migraciones complejas o resultados acelerados, Adobe ofrece la entrega de ingeniero de resultados del agente (AOE). Se trata de un servicio opcional en el que los ingenieros de Adobe gestionan Experience Modernization Agent en su nombre, combinando la automatización de la IA con directrices de expertos para ofrecer resultados a escala y listos para la producción. Para obtener más información sobre la entrega AOE, consulte el documento [Entrega AOE del agente de modernización de experiencias.](/help/ai-in-aem/agents/brand-experience/modernization/aoe-delivery.md)

Si está interesado en el modelo AOE para la próxima migración:

* Póngase en contacto con su representante de Adobe o con el equipo de la cuenta para iniciar el ámbito y la programación.
* Adobe confirmará la idoneidad, estimará la participación y propondrá un plan de participación.

## Limitaciones {#limitations}

Los siguientes casos de uso requieren un esfuerzo de implementación adicional además de las habilidades de Experience Modernization Agent.

La habilidad de raspado no admite las siguientes fuentes.

* Fuentes protegidas o de intranet, como contenido detrás de la autenticación, VPN o firewalls a los que no se puede acceder
* Contenido dinámico complejo, como contenido que requiere una interacción sofisticada del usuario, para aparecer en el DOM.
   * El contenido procesado del lado del cliente es compatible si se puede acceder al contenido a través de una dirección URL específica.
   * También se admiten elementos ocultos mediante CSS pero presentes en el DOM como pestañas, acordeones o carruseles.

El agente no admite los siguientes destinos.

* Entornos de publicación de AEM en los que los sitios utilizan envíos basados en HTL
   * Las aptitudes se dirigen únicamente a Edge Delivery Services.
* Patrones de envío sin encabezado, como envío solo de API o basado en SPA (por ejemplo, Next.js)

Los siguientes requisitos no están cubiertos por las habilidades de automatización dedicadas y requieren un esfuerzo manual.

* Perfección estricta de píxeles
   * Solo se automatiza la fidelidad práctica del diseño
* Integraciones de datos/servicios de terceros del lado del servidor o del cliente
* Integraciones de las funciones de comercio o búsqueda
* Capa de datos o segmentación/experimentación de MarTech
* Aislamiento de fragmentos de contenido/experiencia
* Herencia de varios sitios (MSM)
* Funcionalidad personalizada (por ejemplo, calculadoras, configuradores)
* Lógica empresarial personalizada

## Próximos pasos {#next-steps}

Comience migrando un sitio con el documento [Introducción al agente de modernización de experiencias.](/help/ai-in-aem/agents/brand-experience/modernization/getting-started.md)
