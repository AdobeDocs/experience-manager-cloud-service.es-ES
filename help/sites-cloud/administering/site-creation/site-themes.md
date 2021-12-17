---
title: Temas del sitio
description: Descubra cómo se pueden utilizar AEM temas del sitio para personalizar el estilo y el diseño del sitio.
feature: Administering
role: Admin
source-git-commit: 0b00d579886a106f5f66cfc54d90eab9563724cd
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 1%

---


# Temas del sitio {#site-themes}

Descubra cómo se pueden utilizar AEM temas del sitio para personalizar el estilo y el diseño del sitio.

## Información general {#overview}

Un tema de sitio AEM es un paquete que contiene CSS, JavaScript y recursos estáticos que definen el estilo del sitio AEM y cumplen con la estructura de un tema de sitio AEM.

Los sitios creados con plantillas AEM sitio permiten descargar, personalizar y redistribuir fácilmente los temas.

>[!NOTE]
>
>AEM temas del sitio no deben confundirse con [AEM plantillas de sitio.](site-templates.md) AEM temas del sitio solo contienen la información de estilo de un sitio AEM. AEM plantillas de sitio definen la estructura del sitio y el contenido inicial, así como contienen un tema del sitio AEM para permitir [creación rápida del sitio.](create-site.md)

## Uso de temas del sitio {#using-themes}

Los temas del sitio se utilizan de dos formas diferentes:

* Se utilizan como parte de una plantilla de sitio para definir el estilo cuando [crear un sitio.](create-site.md)
* Se descargan después de crear un sitio basado en una plantilla de sitio, por lo que un desarrollador de front-end puede personalizar aún más el estilo.

>[!TIP]
>
>Puede encontrar una descripción completa del proceso de crear un sitio a partir de una plantilla y personalizar su tema en la [Recorrido de creación rápida de sitios.](/help/journey-sites/quick-site/overview.md)

## Estructura del tema del sitio {#structure}

Los temas del sitio son simplemente paquetes con una estructura lógica que refleja claramente el propósito del contenido del paquete. Un tema del sitio tiene la siguiente estructura típica de un proyecto front-end.

* `src/main.ts`: El punto de entrada principal del tema de JS y CSS
* `src/site`: Archivos JS y CSS que se aplican a todo el sitio
* `src/components`: Archivos JS y CSS específicos de componentes AEM
* `src/resources`: Archivos estáticos como iconos, logotipos y fuentes

## Tema estándar del sitio {#standard-site-theme}

Adobe proporciona un tema de referencia de prácticas recomendadas que puede usar como base para crear su propio tema. [El tema estándar del sitio está disponible en GitHub.](https://github.com/adobe/aem-site-template-standard-theme-e2e)

## Desarrollo de temas del sitio {#developing-themes}

Adobe proporciona un Generador de temas AEM del sitio como un conjunto de secuencias de comandos para la creación de nuevos temas del sitio.

[El Generador de temas del sitio AEM está disponible junto con la documentación de uso de GitHub.](https://github.com/adobe/aem-site-theme-builder) Para personalizar el tema, se necesita una experiencia de desarrollo front-end.
