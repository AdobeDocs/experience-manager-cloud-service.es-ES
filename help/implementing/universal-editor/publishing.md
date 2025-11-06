---
title: Cómo publica contenido el editor universal
description: Descubra cómo el editor universal publica su contenido, en qué se diferencia del proceso realizado en la consola Sitios y las consideraciones a la hora de desarrollar sus propias aplicaciones para trabajar con él.
feature: Developing
role: Admin, Developer
exl-id: 60f0bb4a-ee60-4f73-83ae-8568735474ad
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 100%

---

# Cómo publica contenido el editor universal {#publishing}

Descubra cómo el editor universal publica su contenido, en qué se diferencia del proceso realizado en la consola Sitios y las consideraciones a la hora de desarrollar sus propias aplicaciones para trabajar con él.

>[!TIP]
>
>Este artículo explica los detalles del proceso de publicación del editor universal para el desarrollador. Para el autor de contenido, [el proceso de publicación de contenido se explica aquí.](/help/sites-cloud/authoring/universal-editor/publishing.md)

## Similitudes con el proceso de la consola Sitios {#similarities}

Para los usuarios del [Editor de páginas de AEM](/help/sites-cloud/authoring/page-editor/introduction.md) y la [consola Sitios](/help/sites-cloud/authoring/sites-console/introduction.md), el proceso de publicación de contenido con el editor universal funciona de la manera habitual: al publicarlo en AEM, el contenido se replica desde el servicio de creación al de publicación (o al [servicio de vista previa](/help/sites-cloud/authoring/sites-console/previewing-content.md) si está disponible y según las opciones que el autor elija para la publicación).

## Diferencias {#differences}

Lo que hace que la publicación con el editor universal sea un poco diferente no es tanto el editor en sí, sino el alojamiento externo de la aplicación que el editor universal hace posible.

Cuando se aloja de forma externa, la aplicación web debe garantizar que el contenido se cargue desde el servicio de creación cuando los autores abren la aplicación en el editor, y que se cargue desde el servicio de publicación cuando los visitantes acceden a la aplicación.

## Detección del servicio en la aplicación {#detecting}

La determinación de si se debe acceder al servicio de creación o de publicación se puede realizar mediante una simple afirmación condicional en la aplicación para elegir el autor apropiado o el punto final de publicación al detectar que se está abriendo en el editor.

Otra opción es implementar la aplicación en dos entornos diferentes configurados de forma distinta, de modo que uno recupere su contenido del servicio de creación y que el otro lo recupere del servicio de publicación. Para permitir que los autores abran la URL publicada en el editor universal, se puede crear un pequeño script para “convertir” la URL del lado de publicación a su equivalente en el entorno de creación (por ejemplo, anteponiendo un subdominio `author`), de modo que los autores se redirijan automáticamente.

## Resumen {#summary}

El objetivo del Editor universal es no imponer ninguna pauta particular, de manera que la implementación pueda lograr sus objetivos de una manera totalmente disociada, manteniendo todo sencillo y sin complicaciones para la implementación.

Del mismo modo, el editor universal no tiene ningún requisito sobre cómo un proyecto en particular debe determinar desde qué servicio enviar el contenido. En su lugar, habilita una serie de posibilidades y permite que sea el proyecto el que determine qué solución es la mejor para sus propios requisitos.

## Recursos adicionales {#additional-resources}

Para obtener más información sobre los detalles técnicos del editor universal, consulte estos documentos para desarrolladores.

* [Introducción al editor universal](/help/implementing/universal-editor/introduction.md): descubra cómo el editor universal permite editar cualquier aspecto de los contenidos en varias implementaciones para ofrecer experiencias excepcionales, aumentar la velocidad de contenido y proporcionar una experiencia de desarrollador de última generación.
* [Introducción al editor universal en AEM](/help/implementing/universal-editor/getting-started.md): obtenga información sobre cómo acceder al editor universal y cómo instrumentar la primera aplicación de AEM para utilizarlo.
* [Arquitectura del editor universal](/help/implementing/universal-editor/architecture.md): obtenga información acerca de la arquitectura del editor universal y cómo fluyen los datos entre sus servicios y capas.
* [Atributos y tipos](/help/implementing/universal-editor/attributes-types.md): obtenga información acerca de los atributos y tipos de datos que requiere el editor universal.
* [Autenticación del editor universal](/help/implementing/universal-editor/authentication.md): obtenga información sobre cómo se autentica el editor universal.
