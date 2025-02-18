---
title: Cómo publica contenido el editor universal
description: Descubra cómo publica su contenido el Editor universal, en qué se diferencia del proceso en la consola Sitios y las consideraciones al desarrollar sus propias aplicaciones para trabajar con él.
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 0ee6689460ac0ecc5c025fb6a940d69a16699c85
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 25%

---


# Cómo publica contenido el editor universal {#publishing}

Descubra cómo publica su contenido el Editor universal, en qué se diferencia del proceso en la consola Sitios y las consideraciones al desarrollar sus propias aplicaciones para trabajar con él.

>[!TIP]
>
>Este artículo cubre los detalles del proceso de publicación del editor universal para el desarrollador. Para el autor de contenido, [el proceso de publicación del contenido se describe aquí.](/help/sites-cloud/authoring/universal-editor/publishing.md)

## Similitudes con el proceso de la consola Sites {#similarities}

Para los usuarios de [AEM Page Editor](/help/sites-cloud/authoring/page-editor/introduction.md) y [Sites Console,](/help/sites-cloud/authoring/sites-console/introduction.md) el proceso de publicación de contenido con el editor universal funciona como está acostumbrado: al publicarse en AEM, el contenido se replica desde el servicio de creación al de publicación (o a [el servicio de vista previa](/help/sites-cloud/authoring/sites-console/previewing-content.md) si está disponible y según las opciones que el autor elija al publicar).

## Diferencias {#differences}

Lo que hace que la publicación con el editor universal sea un poco diferente no es tanto el editor en sí, sino el alojamiento externo de la aplicación que el editor universal hace posible.

Cuando se aloja externamente, la aplicación web se preocupa de garantizar que el contenido se cargue desde el servicio de creación cuando los autores abran la aplicación dentro del editor y se cargue desde el servicio de publicación cuando los visitantes accedan a la aplicación.

## Detección del servicio en la aplicación {#detecting}

La determinación de si se debe acceder al autor o al servicio de publicación se puede realizar mediante una sencilla instrucción condicional en la aplicación para elegir el extremo de autor o publicación adecuado al detectar que se está abriendo dentro del editor.

Otra opción es implementar la aplicación en dos entornos diferentes que estén configurados de forma diferente, de modo que uno recupere su contenido del servicio de creación y otro que lo recupere del servicio de publicación. Para permitir que los autores abran la dirección URL publicada en el Editor universal, se puede crear un pequeño script para &quot;convertir&quot; la dirección URL del lado de publicación a su equivalente en el entorno de creación (por ejemplo, anteponiendo un subdominio `author`), de modo que los autores se redirijan automáticamente.

## Resumen {#summary}

El objetivo del Editor universal es no imponer ninguna pauta particular, de manera que la implementación pueda lograr sus objetivos de una manera totalmente disociada, manteniendo todo sencillo y sin complicaciones para la implementación.

Del mismo modo, el editor universal no establece ningún requisito sobre cómo debe proceder un proyecto en particular a la hora de determinar de qué servicio enviar el contenido. Más bien, permite varias posibilidades y permite al proyecto determinar qué solución es la mejor para sus propios requisitos.

## Recursos adicionales {#additional-resources}

Para obtener más información sobre los detalles técnicos del editor universal, consulte estos documentos para desarrolladores.

* [Introducción al editor universal](/help/implementing/universal-editor/introduction.md): descubra cómo el editor universal permite editar cualquier aspecto de los contenidos en varias implementaciones para ofrecer experiencias excepcionales, aumentar la velocidad de contenido y proporcionar una experiencia de desarrollador de última generación.
* [Introducción al editor universal en AEM](/help/implementing/universal-editor/getting-started.md): obtenga información sobre cómo acceder al editor universal y cómo instrumentar la primera aplicación de AEM para utilizarlo.
* [Arquitectura del editor universal](/help/implementing/universal-editor/architecture.md): obtenga información acerca de la arquitectura del editor universal y cómo fluyen los datos entre sus servicios y capas.
* [Atributos y tipos](/help/implementing/universal-editor/attributes-types.md): obtenga información acerca de los atributos y tipos de datos que requiere el editor universal.
* [Autenticación del editor universal](/help/implementing/universal-editor/authentication.md): obtenga información sobre cómo se autentica el editor universal.
