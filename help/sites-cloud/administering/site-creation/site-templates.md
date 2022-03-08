---
title: Plantillas de sitios
description: Descubra cómo se pueden utilizar AEM plantillas de sitio para predefinir la estructura del sitio y el contenido inicial para permitirle crear rápidamente sitios.
feature: Administering
role: Admin
exl-id: 42eec922-b02e-4f2c-8107-7336192919c7
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 1%

---

# Plantillas de sitios {#site-templates}

Descubra cómo se pueden utilizar AEM plantillas de sitio para predefinir la estructura del sitio y el contenido inicial para permitirle crear rápidamente sitios.

## Información general {#overview}

Es conveniente tener estructuras predefinidas disponibles para implementar rápidamente un nuevo sitio basado en un conjunto de estándares existentes. Las plantillas de sitio son una forma de combinar el contenido básico del sitio en un paquete conveniente y reutilizable.

Las plantillas de sitio generalmente contienen contenido y estructura base del sitio, así como información de estilo del sitio, conocida como [tema del sitio,](site-themes.md) para iniciar un nuevo sitio rápidamente. Los administradores seleccionan una plantilla de sitio en la que basar el sitio [durante el proceso de creación del sitio.](create-site.md)

Las plantillas son potentes porque se pueden reutilizar y personalizar. Y como puede tener varias plantillas disponibles en la instalación de AEM, tiene la flexibilidad de crear diferentes sitios para satisfacer diversas necesidades comerciales.

>[!NOTE]
>
>AEM plantillas de sitio no deben confundirse con [plantillas de página.](/help/sites-cloud/authoring/features/templates.md) Las plantillas de sitio definen la estructura general de un sitio. Una plantilla de página define la estructura y el contenido inicial de una página individual.
>
>AEM plantillas de sitio no deben confundirse con [AEM temas del sitio.](site-themes.md) AEM temas del sitio solo contienen la información de estilo de un sitio AEM. AEM plantillas de sitio definen la estructura del sitio y el contenido inicial, así como contienen un tema del sitio AEM para permitir [creación rápida del sitio.](create-site.md)

## Adición de una plantilla de sitio a AEM {#adding}

Puede agregar varias plantillas a AEM, que luego se pueden usar para [crear sitios.](create-site.md)

1. Inicie sesión en el entorno de creación de AEM y vaya a la consola Sitios .

   * `https://<your-author-environment>.adobeaemcloud.com/sites.html/content`

1. Toque o haga clic **Crear** en la parte superior derecha de la pantalla y en el menú desplegable , seleccione **Sitio a partir de una plantilla**.

   ![Creación de un sitio a partir de una plantilla](../assets/create-site-from-template.png)

1. En el asistente Crear sitio , toque o haga clic en **Importar** en la parte superior de la columna izquierda.

   ![Asistente de creación de sitios](../assets/site-creation-wizard.png)

1. En el explorador de archivos, busque la plantilla que desee utilizar y toque o haga clic en **Cargar**.

1. Una vez cargado, aparece en la lista de plantillas disponibles.

La plantilla se ha cargado y se puede usar en [crear sitios nuevos.](create-site.md)

Al seleccionar una plantilla existente, muestra información sobre la plantilla en la columna derecha.

![Seleccionar una plantilla](../assets/select-site-template.png)

## Estructura de la plantilla del sitio {#structure}

Las plantillas de sitio son simplemente paquetes con una estructura lógica que refleja claramente el propósito del contenido del paquete. Una plantilla de sitio tiene la siguiente estructura.

* `files`: Carpeta con el kit de interfaz de usuario, XD archivo y, posiblemente, otros archivos
* `previews`: Carpeta con capturas de pantalla de la plantilla del sitio
* `site`: Paquete de contenido del contenido que se copia para cada sitio creado a partir de esta plantilla, como plantillas de página, páginas, etc.
* `theme`: Fuentes de [tema del sitio](site-themes.md) para modificar el aspecto del sitio, incluidos CSS, JavaScript, etc.

## Plantilla de sitio estándar {#standard-site-template}

Adobe proporciona una plantilla de referencia de prácticas recomendadas que puede utilizar como base para crear sus propias plantillas. [La plantilla de sitio estándar está disponible en GitHub.](https://github.com/adobe/aem-site-template-standard)

[Última versión de la plantilla de sitio estándar](https://github.com/adobe/aem-site-template-standard/releases) se puede descargar y utilizar directamente para [crear nuevos sitios.](create-site.md)

## Desarrollo de plantillas de sitio {#developing-templates}

Adobe proporciona y AEM el Generador de plantillas de sitio como un conjunto de secuencias de comandos para la creación de nuevas plantillas de sitio.

[El Generador de plantillas de sitio AEM está disponible junto con la documentación de uso en GitHub.](https://github.com/adobe/aem-site-template-builder) Para personalizar el [tema del sitio](site-themes.md) y AEM conocimiento del desarrollador es necesario para personalizar la estructura y el contenido del sitio.
