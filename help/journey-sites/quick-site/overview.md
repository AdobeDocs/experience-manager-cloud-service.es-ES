---
title: AEM Recorrido de creación rápida de sitios
description: Comience aquí para obtener un recorrido guiado a través de la herramienta de creación rápida de sitios AEM fácil de usar, para optimizar el desarrollo front-end de su sitio AEM y personalizar rápidamente su sitio sin conocimiento del servidor de AEM.
exl-id: b8218232-0298-4b16-9dab-fa59be592a24
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: ht
source-wordcount: '1030'
ht-degree: 100%

---

# AEM Recorrido de creación rápida de sitios {#quick-site-creation-journey}

Comience aquí para obtener un recorrido guiado a través de la herramienta de creación rápida de sitios AEM fácil de usar, para optimizar el desarrollo front-end de su sitio AEM y personalizar rápidamente su sitio sin conocimiento del servidor de AEM.

## Introducción {#introduction}

AEM Sites es un potente conjunto de herramientas para crear y administrar experiencias digitales. Los autores de contenido pueden crear fácilmente experiencias digitales mediante el editor de sitios y organizar el contenido mediante la consola de sitios, a la vez que pueden ver el contenido en su momento de publicación, tal y como lo enviará AEM a las audiencias en los distintos canales.

La herramienta Creación rápida de sitios de AEM permite a los usuarios que no son desarrolladores crear rápidamente un nuevo sitio desde cero mediante plantillas de sitio. Una vez creada, la herramienta de creación rápida de sitios también permite la personalización rápida del tema y el estilo del sitio AEM (JavaScript, CSS y recursos estáticos). Esto permite que el desarrollador del front-end, que no necesita ningún conocimiento de AEM, trabaje de forma independiente y paralela a los creadores de contenido. El administrador de AEM simplemente descarga el tema del sitio y lo proporciona al desarrollador de front-end que lo personaliza con sus herramientas favoritas y luego confirma los cambios en el repositorio de código de AEM, que luego se implementa.

Elimina cualquier conocimiento de desarrollador para la creación del sitio, suprime los requisitos de conocimientos de AEM para el desarrollo front-end y permite que el desarrollo del tema transcurra en paralelo con la creación de contenido. Con ello, la herramienta Creación rápida de sitios de AEM acelera enormemente el tiempo de respuesta del sitio. Asimismo, aumenta la agilidad de la personalización y la implementación.

## Información general en vídeo {#video-overview}

Para obtener una descripción general rápida de esta característica en acción, [puede ver esta introducción de cinco minutos.](https://www.youtube.com/watch?v=NQeQ1jZ7ZBw)

Este recorrido de documentación le llevará a través de todas las funciones del vídeo paso a paso y en detalle para que entienda el flujo de trabajo y pueda recrear el proceso en su propio entorno.

## Recorridos de documentación de AEM {#documentation-journeys}

[Un recorrido de documentación](/help/journey-documentation/documentation-journeys.md) une muchos temas y características diferentes y tal vez complicados. Proporciona una narrativa que ayuda al lector (que puede ser nuevo en AEM) a entender y resolver un problema empresarial de principio a fin, mientras asume un conocimiento previo mínimo de AEM.

Los recorridos de documentación están diseñados en torno a los principios de las prácticas recomendadas, basados en las últimas investigaciones de Adobe, la experiencia de implementación comprobada de los consultores de Adobe y los comentarios sobre los proyectos de los clientes.

Si desea saber cómo recomienda Adobe resolver los casos de sitios comerciales con AEM, los recorridos de AEM Sites son el punto de inicio.

## Audiencia {#audience}

Este recorrido describe los requisitos, pasos y enfoques para personalizar los temas de AEM Sites. Su audiencia principal es el desarrollador front-end, que no necesita saber de AEM. Sin embargo, para ilustrar todo el proceso, el recorrido incluye a los administradores, que se supone que tienen conocimientos básicos de AEM Sites y Cloud Manager. En la práctica, varias personas pueden desempeñar diversas funciones y este recorrido admite perspectivas tanto de administradores como de desarrolladores front-end.

| Grupo de usuarios | Descripción | Función en el recorrido |
|---|---|---|
| Desarrollador front-end | Personaliza el tema del sitio | Coge el tema proporcionado por el administrador de AEM y lo personaliza para que se pueda implementar en el sitio de AEM. |
| Autor de contenido | Crea y administra el contenido que se entrega como sitios | Los autores de contenido crean contenido en AEM que se procesa con el tema personalizado por el desarrollador front-end. |
| Administrador de AEM | Crea un nuevo sitio de AEM | El administrador de AEM crea un nuevo sitio basado en una plantilla y, a continuación, proporciona al desarrollador front-end un tema que se debe personalizar. |
| Administrador de Cloud Manager | Crea canalizaciones y concede acceso | El administrador de Cloud Manager crea la canalización front-end y concede acceso al desarrollador front-end para poder personalizar el repositorio de Git de AEM. |

## El Recorrido de creación rápida de sitios de AEM {#the-journey}

Explorará muchos temas en este recorrido. Los siguientes artículos le proporcionan conocimientos básicos sobre la creación y personalización de sitios de AEM mediante la herramienta Creación rápida de sitios y le permiten acceder a documentación técnica detallada.

|#|Artículo|Descripción|Función responsable|
|---|---|---|--|
|0|Recorrido de creación rápida de sitios de AEM|Este documento|Administradores de AEM y Cloud Manager|
|1|[Comprensión de Cloud Manager y el Flujo de trabajo de creación rápida de sitios](cloud-manager.md)|Obtenga información acerca de Cloud Manager y cómo vincula el nuevo proceso de creación rápida de sitios.|Administrador de AEM|
|2|[Creación de un sitio a partir de una plantilla](create-site.md)|Obtenga información sobre cómo crear rápidamente un nuevo sitio de AEM con una plantilla del sitio.|Administrador de AEM|
|3|[Configuración de la canalización](pipeline-setup.md)|Cree una canalización front-end para administrar la personalización del tema de su sitio.|Administrador de Cloud Manager|
|4|[Concesión de acceso al desarrollador front-end](grant-access.md)|Incorpore a los desarrolladores front-end en Cloud Manager para que tengan acceso al repositorio de Git y a la canalización del sitio de AEM.|Administrador de Cloud Manager|
|5|[Recuperación de información de acceso al repositorio de Git](retrieve-access.md)|Descubra cómo el desarrollador front-end utiliza Cloud Manager para acceder a la información del repositorio de Git.|Desarrollador front-end|
|6|[Personalización del tema del sitio](customize-theme.md)|Obtenga información sobre cómo se crea un tema de sitio, cómo personalizarlo y cómo probarlo con contenido de AEM en directo.|Desarrollador front-end|
|7|[Implementación del tema personalizado](deploy-theme.md)|Obtenga información sobre cómo implementar el tema del sitio mediante la canalización.|Desarrollador front-end|

## Siguientes pasos {#what-is-next}

Ya puede empezar su Recorrido de creación rápida de sitios de Adobe.

* Si es administrador de AEM o Cloud Manager, o si cumple las funciones de desarrollador y administrador front-end, o si simplemente desea comprender el proceso de extremo a extremo en AEM, comience al principio del recorrido con [Comprensión de Cloud Manager](cloud-manager.md), como se indica a continuación.
* Si solo es responsable del desarrollo front-end e interactuará con los administradores de AEM y Cloud Manager, puede saltar a [Recuperación de información de acceso al repositorio de Git](retrieve-access.md) para obtener acceso al repositorio de Git de AEM y comenzar a personalizar.
* Si ya comprende que AEM Sites y Cloud Manager trabajan juntos y quiere comenzar directamente con la configuración, puede [ir directamente a la creación de un sitio nuevo a partir de una plantilla.](create-site.md)

## Recursos adicionales {#additional-resources}

Consulte estos recursos adicionales para obtener más información sobre cómo las potentes funciones de AEM funcionan juntas.

* [Documentación técnica de AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=es): si ya tiene una comprensión sólida de AEM, puede que desee consultar directamente los documentos técnicos detallados.
* [Documentación de administración del sitio](/help/sites-cloud/administering/site-creation/create-site.md): consulte los documentos técnicos sobre la creación de sitios para obtener más información sobre las funciones de la herramienta Creación rápida de sitios.
