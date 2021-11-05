---
title: AEM Recorrido de creación rápida de sitios
description: Comience aquí para obtener un recorrido guiado a través de la herramienta de creación rápida de sitios AEM fácil de usar, para optimizar el desarrollo front-end de su sitio AEM y personalizar rápidamente su sitio sin AEM conocimiento del servidor.
source-git-commit: efeb97d4bd7e7c11ec2c0ba1244a32b8b9affdab
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 1%

---


# AEM Recorrido de creación rápida de sitios {#quick-site-creation-journey}

Comience aquí para obtener un recorrido guiado a través de la herramienta de creación rápida de sitios AEM fácil de usar, para optimizar el desarrollo front-end de su sitio AEM y personalizar rápidamente su sitio sin AEM conocimiento del servidor.

>[!CAUTION]
>
>La herramienta Creación rápida de sitios es actualmente una vista previa técnica. Está disponible con fines de ensayo y evaluación y no está pensado para su uso en producción a menos que se acuerde con la asistencia al Adobe.

## Introducción {#introduction}

AEM Sites es un potente conjunto de herramientas para crear y administrar experiencias digitales. Los autores de contenido pueden crear fácilmente experiencias digitales mediante el editor de sitios y organizar el contenido mediante la consola de sitios, a la vez que pueden ver el contenido en directo tal y como se enviará AEM a las audiencias en los distintos canales.

La AEM herramienta de creación rápida de sitios permite a los usuarios que no son desarrolladores crear rápidamente un nuevo sitio desde cero mediante plantillas de sitio. Una vez creada, la herramienta de creación rápida de sitios también permite la personalización rápida del tema y el estilo del sitio AEM (JavaScript, CSS y recursos estáticos). Esto permite que el desarrollador del front-end, que no necesita ningún conocimiento de AEM, trabaje de forma independiente y paralela a los creadores de contenido. El administrador de AEM simplemente descarga el tema del sitio y lo proporciona al desarrollador de front-end que lo personaliza con sus herramientas favoritas y luego confirma los cambios en el repositorio de código de AEM, que luego se implementa.

Al eliminar cualquier conocimiento del desarrollador para la creación del sitio, eliminar los requisitos de conocimientos AEM para el desarrollo del front-end y permitir que el desarrollo del tema se realice en paralelo con la creación de contenido, la herramienta de creación rápida del sitio de AEM acelera enormemente el tiempo de respuesta del sitio y aumenta la agilidad de la personalización y la implementación del sitio.

## recorridos de documentación de AEM {#documentation-journeys}

[Un Recorrido de documentación](/help/journey-documentation/home.md) une muchos temas y características diferentes y tal vez complicados al proporcionar una narrativa que ayuda al lector, que puede ser nuevo en AEM, entender y resolver un problema de negocios de principio a fin, mientras asume un mínimo de conocimiento previo o AEM.

Los Recorridos de documentación están diseñados en torno a los principios de las mejores prácticas, basados en las últimas investigaciones del Adobe, la experiencia de implementación comprobada de los consultores de Adobe y los comentarios de los proyectos de los clientes.

Si desea saber cómo recomienda Adobe resolver los casos comerciales del sitio con AEM, los Recorridos de AEM Sites son el punto de inicio.

## Audience {#audience}

Este recorrido describe los requisitos, pasos y enfoques para personalizar los temas de AEM Sites. Su audiencia principal es el desarrollador de front-end, que no necesita saber AEM. Sin embargo, para ilustrar todo el proceso, el recorrido incluye a los administradores, que se supone que tienen conocimientos básicos de AEM Sites y Cloud Manager. En la práctica, varias personas pueden desempeñar varias funciones y este recorrido admite perspectivas tanto de administradores como de desarrolladores de front-end.

| Grupo de usuarios | Descripción | Función en el Recorrido |
|---|---|---|
| Desarrollador front-end | Personaliza el tema del sitio | Toma el tema proporcionado por el administrador de AEM y lo personaliza para que se pueda implementar en el sitio de AEM. |
| Autor de contenido | Crea y administra el contenido que se entrega como sitios | Los autores de contenido crean contenido en AEM que se representa con el tema personalizado por el desarrollador de front-end. |
| Administrador de AEM | Crea un nuevo sitio AEM | El administrador de AEM crea un nuevo sitio basado en una plantilla y, a continuación, proporciona al desarrollador del front-end un tema que se debe personalizar. |
| Administrador de Cloud Manager | Crea canalizaciones y concede acceso | El administrador de Cloud Manager crea la canalización de front-end y concede acceso al desarrollador de front-end para poder realizar personalizaciones en el repositorio de Git de AEM. |

## El Recorrido de creación rápida AEM sitio {#the-journey}

Explorará muchos temas en este recorrido. Los siguientes artículos le proporcionan conocimientos básicos sobre la creación y personalización de sitios AEM mediante la herramienta de creación rápida de sitios y le permiten acceder a documentación técnica detallada.

|#|Artículo|Descripción|Función responsable| |—|—|—|—| |0|AEM Recorrido de creación rápida del sitio|Este documento|Administradores de AEM y Cloud Manager| |1|[Comprender Cloud Manager y el flujo de trabajo de creación rápida de sitios](cloud-manager.md)|Obtenga información sobre Cloud Manager y cómo vincula el nuevo proceso de creación rápida de sitios.|AEM administrador| |2|[Crear sitio a partir de una plantilla](create-site.md)|Obtenga información sobre cómo crear rápidamente un nuevo sitio AEM con una plantilla de sitio.|AEM administrador| |3|[Configurar la canalización](pipeline-setup.md)|Cree una canalización front-end para administrar la personalización del tema del sitio.|Administrador de Cloud Manager| |4|[Conceder acceso al desarrollador de front-end](grant-access.md)|Incorpore a los desarrolladores de front-end en Cloud Manager para que tengan acceso al repositorio de Git de su sitio AEM y a la canalización.|Administrador de Cloud Manager| |5|[Recuperar información de acceso al repositorio de Git](retrieve-access.md)|Obtenga información sobre cómo el desarrollador de front-end utiliza Cloud Manager para acceder a la información del repositorio de Git.|Desarrollador front-end| |6|[Personalizar el tema del sitio](customize-theme.md)|Obtenga información sobre cómo se crea un tema de sitio, cómo personalizarlo y cómo probarlo con contenido AEM en directo.|Desarrollador front-end| |7|[Implementar el tema personalizado](deploy-theme.md)|Obtenga información sobre cómo implementar el tema del sitio mediante la canalización.|Desarrollador front-end|

## Siguientes pasos {#what-is-next}

Ya está listo para empezar a usar el recorrido de creación rápida del sitio de Adobe.

* Si es administrador de AEM o Cloud Manager, o si cumple las funciones de desarrollador y administrador del front-end, o si simplemente desea comprender el proceso de extremo a extremo en AEM, comience al principio del recorrido con [Comprender Cloud Manager](cloud-manager.md) como se indica a continuación.
* Si solo es responsable del desarrollo del front-end e interactuará con los administradores de AEM y Cloud Manager, puede omitir directamente a [Recuperar información de acceso al repositorio de Git](retrieve-access.md) para obtener acceso al repositorio de Git de AEM y comenzar a personalizar.
* Si ya comprende que AEM Sites y Cloud Manager trabajan juntos y desean comenzar directamente con la configuración, puede [vaya directamente a la creación de un sitio nuevo desde una plantilla.](create-site.md)

## Recursos adicionales {#additional-resources}

Consulte estos recursos adicionales para obtener más información sobre cómo funcionan juntas AEM potentes funciones.

* [AEM documentación técnica as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=es) - Si ya tiene una comprensión firme de AEM, puede que desee consultar directamente los documentos técnicos detallados.
* [Documentación de administración del sitio](/help/sites-cloud/administering/site-creation/create-site.md) - Consulte los documentos técnicos sobre la creación de sitios para obtener más información sobre las funciones de la herramienta de creación rápida de sitios.
