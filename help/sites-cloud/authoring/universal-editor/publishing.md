---
title: Publicación de contenido con el editor universal
description: Descubra cómo el editor universal publica contenido y cómo sus aplicaciones pueden gestionar el contenido publicado.
exl-id: aee34469-37c2-4571-806b-06c439a7524a
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 64c257adc7e1f22531c0fe45b44b27ab4e0badb8
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 42%

---


# Publicación de contenido con el editor universal {#publishing}

Descubra cómo el editor universal publica contenido y cómo sus aplicaciones pueden gestionar el contenido publicado.

>[!TIP]
>
>El proceso de publicación que se describe aquí es la función predeterminada estándar del editor universal.
>
>El editor universal también admite [extensiones y extensibilidad de la interfaz de usuario](/help/implementing/universal-editor/extending.md) para permitir que los flujos de trabajo admitan el proceso de publicación, por lo que el flujo de publicación puede variar.

## Publicación de contenido desde el editor universal {#publishing-content}

Cuando usted, como autor de contenido, esté listo para publicar su contenido, solo tiene que tocar o hacer clic en el icono **Publicar** en la barra de herramientas del Editor universal.

![Páginas de publicación](assets/publish-menu.png)

1. En el Editor universal, pulse o haga clic en [el icono **Publicar** de la barra de herramientas del Editor universal.](/help/sites-cloud/authoring/universal-editor/navigation.md#publish)
1. Si tienes un [servicio de vista previa](/help/sites-cloud/authoring/sites-console/previewing-content.md) disponible, puedes elegir dónde publicar el contenido, ya sea en **Vista previa** o en **Publicar**.
1. La sección **Items** enumera el contenido que se incluye en la publicación, que incluye:
   * **Nuevos** elementos que aún no se han publicado.
   * **Modificado** contenido que se ha publicado, pero modificado desde la última publicación.
   * **Publicado** contenido que se ha publicado y no se ha modificado desde esa publicación.

   Pulse o haga clic en las casillas de verificación situadas junto a esos elementos para incluirlos o excluirlos de la publicación, según sea necesario. Pulse o haga clic en **Extender** para ver los elementos individuales incluidos en los totales de las tres categorías y para poder incluirlos o excluirlos individualmente.

   ![Publicar elementos](assets/publish-items.png)

   Pulse o haga clic en la flecha hacia atrás situada junto al encabezado **Elementos** para volver a la descripción general.

1. Pulse o haga clic en **Publicar** para publicar o en **Cancelar** para cancelar.

## Cancelar la publicación de contenido desde el editor universal {#unpublishing-content}

La cancelación de la publicación de contenido funciona de manera similar a la publicación de contenido. Cuando usted, como autor de contenido, esté listo para quitar contenido de la publicación, toque o haga clic en el icono de puntos suspensivos en la barra de herramientas del Editor universal y, a continuación, **Cancelar la publicación**.

Entonces tiene las mismas opciones para cancelar la publicación de contenido que tenía al [publicar contenido.](#publishing-content) incluida la cancelación de la publicación de una instancia de vista previa si está disponible y qué elementos se incluirán en la cancelación de la publicación.

## Publicar y cancelar la publicación desde la consola Sitios {#publishing-sites-console}

También puede publicar [desde la consola Sitios,](/help/sites-cloud/authoring/sites-console/publishing-pages.md), lo que puede resultar útil cuando desea publicar varias páginas de contenido o programar la publicación o cancelación de la publicación.

## Similitudes con el editor de páginas {#similarities}

Para los usuarios del [Editor de páginas de AEM](/help/sites-cloud/authoring/page-editor/introduction.md), el proceso para publicar contenido con el Editor universal funciona como está acostumbrado: al publicar en AEM, el contenido se replica desde el nivel de creación al de publicación.

## Diferencias {#differences}

Lo que hace que la publicación con el editor universal sea un poco diferente no es tanto el editor en sí, sino el alojamiento externo de la aplicación que el editor universal hace posible.

Cuando se aloja de forma externa, la aplicación web debe garantizar que el contenido se cargue desde el nivel de creación cuando los autores abren la aplicación en el editor y se carga desde el nivel de publicación cuando los visitantes acceden a la aplicación.

## Detección del nivel en la aplicación {#detecting}

La determinación de si el nivel de autor o publicación debe ser acceso se puede realizar mediante una simple afirmación condicional en la aplicación para elegir el autor apropiado o el punto final de publicación al detectar que se está abriendo en el editor.

Otra opción es implementar la aplicación en dos entornos diferentes configurados de forma diferente, de modo que uno recupere su contenido del nivel de creación y otro que lo recupere del nivel de publicación. Para permitir que los autores abran la dirección URL publicada en el Editor universal, se puede crear un pequeño script para &quot;convertir&quot; la dirección URL del lado de publicación a su equivalente en el entorno de creación (por ejemplo, anteponiendo un subdominio `author`), de modo que los autores se redirijan automáticamente.

## Resumen {#summary}

El objetivo del Editor universal es no imponer ninguna pauta particular, de manera que la implementación pueda lograr sus objetivos de una manera totalmente disociada, manteniendo todo sencillo y sin complicaciones para la implementación.

Del mismo modo, el Editor universal no requiere requisitos sobre cómo un proyecto en particular debe determinar desde qué nivel enviar el contenido. Más bien, permite varias posibilidades y permite al proyecto determinar qué solución es la mejor para sus propios requisitos.

## Recursos adicionales {#additional-resources}

Para aprender a crear contenido con el editor universal, consulte este documento.

* [Creación de contenido con el editor universal](authoring.md): aprenda lo fácil e intuitivo que es para los autores de contenido crearlo con el editor universal.

Para obtener más información sobre los detalles técnicos del editor universal, consulte estos documentos para desarrolladores.

* [Introducción al editor universal](/help/implementing/universal-editor/introduction.md): descubra cómo el editor universal permite editar cualquier aspecto de los contenidos en varias implementaciones para ofrecer experiencias excepcionales, aumentar la velocidad de contenido y proporcionar una experiencia de desarrollador de última generación.
* [Introducción al editor universal en AEM](/help/implementing/universal-editor/getting-started.md): obtenga información sobre cómo acceder al editor universal y cómo instrumentar la primera aplicación de AEM para utilizarlo.
* [Arquitectura del editor universal](/help/implementing/universal-editor/architecture.md): obtenga información acerca de la arquitectura del editor universal y cómo fluyen los datos entre sus servicios y capas.
* [Atributos y tipos](/help/implementing/universal-editor/attributes-types.md): obtenga información acerca de los atributos y tipos de datos que requiere el editor universal.
* [Autenticación del editor universal](/help/implementing/universal-editor/authentication.md): obtenga información sobre cómo se autentica el editor universal.
