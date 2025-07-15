---
title: Temas del sitio
description: Descubra cómo se pueden utilizar los temas del sitio de AEM para personalizar el estilo y el diseño del sitio para proyectos de creación tradicionales de AEM con envío de publicación.
feature: Administering
role: Admin
exl-id: 53d4afb3-d091-47a1-ba12-5bcec99f46b9
solution: Experience Manager Sites
source-git-commit: 9efba01add46c09e9839da6bb96b138d48018e54
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 67%

---


# Temas del sitio {#site-themes}

{{traditional-aem}}

Descubra cómo se pueden utilizar los temas del sitio de AEM para personalizar el estilo y el diseño del sitio para proyectos de creación tradicionales de AEM con envío de publicación.

## Información general {#overview}

Un tema del sitio de AEM es un paquete que contiene CSS, JavaScript y recursos estáticos que definen el estilo del sitio de AEM y cumplen la estructura de un tema de sitio de AEM.

Los sitios creados con plantillas de sitio de AEM permiten descargar, personalizar y volver a implementar fácilmente los temas para los proyectos de creación tradicionales de AEM con [envío de publicación.](/help/sites-cloud/authoring/author-publish.md)

>[!NOTE]
>
>Los temas del sitio de AEM no deben confundirse con las [plantillas de sitio de AEM](site-templates.md). Los temas del sitio de AEM solo contienen la información de estilo de un sitio de AEM. Las plantillas de sitio de AEM definen la estructura del sitio y el contenido inicial, y contienen un tema de sitio de AEM para permitir la [creación rápida del sitio.](create-site.md)

## Uso de temas del sitio {#using-themes}

Los temas del sitio se utilizan de dos formas:

* Se emplean como parte de una plantilla del sitio para definir el estilo cuando se [crea un sitio.](create-site.md)
* Se descargan después de crear un sitio basado en una plantilla del sitio, para que un desarrollador front-end pueda personalizar aún más el estilo.

>[!TIP]
>
>Puede encontrar una descripción completa del proceso de crear un sitio a partir de una plantilla y personalizar su tema en el [Recorrido de creación rápida de sitios.](/help/journey-sites/quick-site/overview.md)

## Estructura del tema del sitio {#structure}

Los temas del sitio no son más que paquetes con una estructura lógica que refleja con claridad el propósito del contenido del paquete. Para un proyecto front-end típico, Adobe recomienda la siguiente estructura para un tema del sitio:

* `src/theme.ts`: el punto de entrada principal del tema de JS y CSS
* `src/site`: archivos JS y CSS que se aplican a todo el sitio
* `src/components`: archivos JS y CSS específicos de componentes de AEM
* `src/resources`: archivos estáticos como iconos, logotipos y fuentes

Según las necesidades específicas del proyecto, la estructura del tema puede variar siempre que se conserve el punto de entrada principal `src/theme.ts`.

## Tema estándar del sitio {#standard-site-theme}

Adobe proporciona un tema de referencia de prácticas recomendadas que puede usar como base para crear su propio tema. [El tema estándar del sitio está disponible en GitHub.](https://github.com/adobe/aem-site-template-standard/tree/main/theme)

## Desarrollo de temas del sitio {#developing-themes}

Adobe proporciona un Generador de temas del sitio de AEM como un conjunto de scripts para la creación de nuevos temas del sitio.

[El Generador de temas del sitio de AEM está disponible junto con la documentación de uso en GitHub.](https://github.com/adobe/aem-site-theme-builder) Para personalizar el tema, se necesita una experiencia de desarrollo front-end.
