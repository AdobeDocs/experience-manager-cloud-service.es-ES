---
title: Plantillas de sitios
description: Descubra cómo se pueden utilizar las plantillas de sitio AEM para predefinir la estructura del sitio y el contenido inicial para permitirle crear sitios rápidamente.
feature: Administering
role: Admin
exl-id: 42eec922-b02e-4f2c-8107-7336192919c7
solution: Experience Manager Sites
source-git-commit: 4d45e7ef626ad0b46f5323263cca791b14f9732f
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 82%

---


# Plantillas de sitios {#site-templates}

Descubra cómo se pueden utilizar las plantillas de sitio AEM para predefinir la estructura del sitio y el contenido inicial para permitirle crear sitios rápidamente.

## Información general {#overview}

Es práctico tener estructuras predefinidas disponibles para implementar rápidamente un nuevo sitio basado en un conjunto de estándares existentes. Las plantillas de sitio son una forma de combinar el contenido básico del sitio en un paquete conveniente y reutilizable.

Las plantillas de sitio generalmente incluyen contenido y estructura base del sitio, así como información de estilo del sitio, conocida como [tema del sitio](site-themes.md), para poner en marcha un nuevo sitio rápidamente. Los administradores seleccionan una plantilla de sitio en la que basar el sitio [durante el proceso de creación del sitio.](create-site.md)

Las plantillas son eficaces, ya que se pueden reutilizar y personalizar. Y como puede tener varias plantillas disponibles en la instalación de AEM, tiene la flexibilidad de crear diferentes sitios para satisfacer diversas necesidades comerciales.

>[!NOTE]
>
>Las plantillas de sitio de AEM no deben confundirse con las [plantillas de página](/help/sites-cloud/authoring/page-editor/templates.md). Las plantillas de sitio definen la estructura general de un sitio. Una plantilla de página define la estructura y el contenido inicial de una página individual.
>
>Las plantillas de sitio de AEM no deben confundirse con los [temas de sitio de AEM.](site-themes.md) Los temas de sitio de AEM solo contienen la información de estilo de un sitio AEM. Las plantillas de sitio de AEM definen la estructura del sitio y el contenido inicial, y contienen un tema de sitio de AEM para permitir la [creación rápida del sitio.](create-site.md)

### Plantillas de sitio proporcionadas por Adobe {#adobe-templates}

{{adobe-templates}}

## Adición de una plantilla de sitio a AEM {#adding}

Puede agregar varias plantillas a AEM, que luego se pueden usar para [crear sitios.](create-site.md)

1. Inicie sesión en el entorno de creación de AEM y vaya a la consola Sites.

   * `https://<your-author-environment>.adobeaemcloud.com/sites.html/content`

1. Seleccione **Crear** en la parte superior derecha de la pantalla y en el menú desplegable, seleccione **Sitio a partir de una plantilla**.

   ![Creación de un sitio a partir de una plantilla](../assets/create-site-from-template.png)

1. En el asistente Crear sitio, seleccione **Importar** en la parte superior de la columna izquierda.

   ![Asistente de creación de sitios](../assets/site-creation-wizard.png)

1. En el explorador de archivos, busque la plantilla que desee usar y seleccione **Cargar**.

1. Una vez cargado, aparece en la lista de plantillas disponibles.

La plantilla se ha cargado y se puede usar en [crear sitios nuevos.](create-site.md)

Al seleccionar una plantilla existente, muestra información sobre la plantilla en la columna derecha.

![Seleccionar una plantilla](../assets/select-site-template.png)

## Estructura de la plantilla del sitio {#structure}

Las plantillas de sitio son simplemente paquetes con una estructura lógica que refleja claramente el propósito del contenido del paquete. Una plantilla de sitio tiene la siguiente estructura.

* `files`: carpeta con el kit de interfaz de usuario, XD archivo y, posiblemente, otros archivos
* `previews`: carpeta con capturas de pantalla de la plantilla del sitio.
* `site`: paquete de contenido del contenido que se copia para cada sitio creado a partir de esta plantilla, como plantillas de página, páginas, etc.
* `theme`: fuentes del [tema del sitio](site-themes.md) para modificar el aspecto del sitio, incluidos CSS, JavaScript, etc.

## Desarrollo de plantillas de sitio {#developing-templates}

Adobe proporciona el Generador de plantillas de sitio de AEM como un conjunto de scripts para la creación de nuevas plantillas de sitio. [El Generador de plantillas de sitio de AEM está disponible junto con la documentación de uso en GitHub.](https://github.com/adobe/aem-site-template-builder)
