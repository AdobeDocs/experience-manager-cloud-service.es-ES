---
title: Publicación de contenido con el editor universal
description: Descubra cómo el editor universal publica contenido y cómo sus aplicaciones pueden gestionar el contenido publicado.
exl-id: aee34469-37c2-4571-806b-06c439a7524a
source-git-commit: 16f2922a3745f9eb72f7070c30134e5149eb78ce
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 55%

---


# Publicación de contenido con el editor universal {#publishing}

Descubra cómo el editor universal publica contenido y cómo sus aplicaciones pueden gestionar el contenido publicado.

{{universal-editor-status}}

## Similitudes con AEM {#similarities}

AEM AEM Para los usuarios de, el proceso de publicación de contenido con el editor universal funciona como está acostumbrado: al publicarse en el editor, el contenido se replica desde el nivel de creación al de publicación, en el de publicación, en el de publicación.

## Diferencias {#differences}

Lo que hace que la publicación con el editor universal sea un poco diferente no es tanto el editor en sí, sino el alojamiento externo de la aplicación que el editor universal hace posible.

Cuando se aloja de forma externa, la aplicación web debe garantizar que el contenido se cargue desde el nivel de creación cuando los autores abren la aplicación en el editor y se carga desde el nivel de publicación cuando los visitantes acceden a la aplicación.

## Detección del nivel en la aplicación {#detecting}

La determinación de si el nivel de autor o publicación debe ser acceso se puede realizar mediante una simple afirmación condicional en la aplicación para elegir el autor apropiado o el punto final de publicación al detectar que se está abriendo en el editor.

Otra opción es implementar la aplicación en dos entornos diferentes configurados de forma diferente, de modo que uno recupere su contenido del nivel de creación y otro que lo recupere del nivel de publicación. Para permitir que los autores abran la URL publicada en el Editor universal, se puede crear una pequeña secuencia de comandos para &quot;convertir&quot; la URL del lado de publicación a su equivalente en el entorno de creación (por ejemplo, anteponiendo una etiqueta `author` subdominio), de modo que los autores se redirijan automáticamente.

## Resumen {#summary}

El objetivo del Editor universal es no imponer ninguna pauta particular, de manera que la implementación pueda lograr sus objetivos de una manera totalmente disociada, manteniendo todo sencillo y sin complicaciones para la implementación.

Del mismo modo, el Editor universal no requiere requisitos sobre cómo un proyecto en particular debe determinar desde qué nivel enviar el contenido. Más bien, permite varias posibilidades y permite al proyecto determinar qué solución es la mejor para sus propios requisitos.
