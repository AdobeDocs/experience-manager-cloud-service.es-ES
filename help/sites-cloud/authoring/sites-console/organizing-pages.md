---
title: Organización de páginas
description: AEM Aprenda a organizar su sitio web con la ayuda de los usuarios de.
exl-id: c57096ca-34fe-4b19-98e0-8f3cd43cf24e
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 67%

---


# Organización de páginas {#creating-and-organizing-pages}

AEM Aprenda a organizar su sitio web con la ayuda de los usuarios de. Una vez que sepa cómo organizar las páginas, puede [crear páginas nuevas](/help/sites-cloud/authoring/sites-console/creating-pages.md) y [administrar las páginas existentes](/help/sites-cloud/authoring/sites-console/managing-pages.md).

{{edge-delivery-authoring}}

## Organización del sitio {#organizing-your-site}

AEM Como creador, debe organizar el sitio dentro de la organización de. Esto implica crear y asignar un nombre a las páginas de contenido para que:

* Pueda encontrarlas con facilidad en el entorno de creación
* Los usuarios que visiten el sitio web puedan explorarlas fácilmente en el entorno de publicación

También puede usar [carpetas](#creating-a-new-folder) para organizar el contenido.

La estructura de un sitio web se puede considerar como un árbol que alberga las páginas de contenido. Los nombres de estas páginas de contenido se usan para formar las URL, y los títulos se muestran cuando se visualiza el contenido de la página.

A continuación se muestra un ejemplo del sitio [WKND Tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=es), donde se tiene acceso a un artículo sobre parques de patinaje (`la-skateparks`):

`http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

```xml
 /content
 /wknd
  /en
   /music
    /...
   /sports
    /la-skateparks
    /five-gyms-la
    /mountain-bike-routes
   /shopping
    /...
   /art
    /...
   /...
```

Esta estructura se puede ver desde la consola [**Sites**](/help/sites-cloud/authoring/sites-console/introduction.md), donde puede navegar por las páginas de su sitio web y realizar acciones en las páginas.

## Convenciones de nomenclatura de páginas {#page-naming-conventions}

Al crear una página, hay dos campos de claves:

* **[Título](#title)**:
   * Se muestra al usuario en la consola, en la parte superior del contenido de la página al editar. 
   * Este campo es obligatorio.
* **[Nombre](#name)**:
   * Se usa para generar la URI.
   * La entrada del usuario para este campo es opcional. Si no se especifica, el nombre se obtiene a partir del título. Consulte la siguiente sección [Restricciones de nombres de páginas y Prácticas recomendadas](#page-name-restrictions-and-best-practices) para obtener más detalles.

### Restricciones de nombres de páginas y prácticas recomendadas {#page-name-restrictions-and-best-practices}

El **título** y el **nombre** de la página se pueden crear por separado, pero están relacionados:

* Al crear una página, solo se precisa el campo **Título**. Si no se proporciona ningún **nombre** durante la creación de la página, AEM genera un nombre a partir de los 64 primeros caracteres del título (observe el conjunto de validación a continuación). Solo se utilizan los 64 primeros caracteres para ofrecer compatibilidad con la práctica recomendada de nombres de página cortos.
* Si el autor especifica manualmente un nombre de página, el límite de 64 caracteres no se aplica. Sin embargo, es posible que se produzcan otras limitaciones técnicas en la longitud del nombre de la página.

>[!TIP]
>
>Al definir un nombre de página, se recomienda que sea lo más corto y expresivo posible para que el lector pueda entenderlo con facilidad. Para obtener más información, consulte la [guía de estilo W3C](https://www.w3.org/Provider/Style/TITLE.html) para el elemento de `title`.
>
>Además, recuerde que algunos exploradores (por ejemplo, las versiones anteriores de IE) solo aceptan URL con una longitud determinada, por lo que también existen motivos técnicos para mantener los nombres de las páginas cortos. 

AEM AEM Al crear una página, [valida el nombre de la página según las convenciones ](/help/implementing/developing/introduction/naming-conventions.md) impuestas por el JCR y la aplicación de validación de datos (JCR) de la página de inicio de sesión (JCR) y de la página de inicio de sesión (JCR) de la página de inicio de sesión 1.

El mínimo permitido de caracteres es:

* `a` hasta `z`
* `A` hasta `Z`
* `0` hasta `9`
* `_` (guion bajo)
* `-` (guion/signo menos)

Para obtener toda la información sobre los caracteres permitidos, consulte las [convenciones de nomenclatura](/help/implementing/developing/introduction/naming-conventions.md).

>[!NOTE]
>
>Los nombres de las páginas están limitados a 150 caracteres.

### Título {#title}

AEM AEM Si proporciona solamente una página **Title** al crear una página, deriva la página **Name** de esta cadena y [valida el nombre según las convenciones](/help/implementing/developing/introduction/naming-conventions.md) impuestas por los criterios de y JCR. En el caso de que la página se haya creado, la página se convierte en una página con el nombre Name de esta cadena y se define como {JCR}.

Se acepta un campo de **Título** con caracteres no válidos, pero los caracteres no válidos se sustituirán en el nombre derivado. Por ejemplo:

| Título | Nombre derivado |
|---|---|
| Schön | `schoen.html` |
| SC%&amp;&#42;ç+ | `sc---c-.html` |

### Nombre {#name}

AEM AEM Cuando se proporciona una página **Name** al crear una página, [valida el nombre según las convenciones ](/help/implementing/developing/introduction/naming-conventions.md) impuestas por las normas de privacidad y JCR, y el nombre de la página se valida a través de las convenciones  impuestas por las normas de privacidad de la página y el JCR. No se pueden enviar caracteres no válidos desde el campo **Nombre**. Cuando detecta caracteres no válidos, el campo se resalta con un mensaje explicativo.

![Ejemplo de introducción de un nombre de página no válido](/help/sites-cloud/authoring/assets/organizing-invalid-name.png)

>[!TIP]
>
>Evite utilizar un código de dos letras como nombre de página, tal como se indica en la norma ISO-639-1, a menos que sea la raíz de un idioma.
>
>Consulte [Preparación de contenido para su traducción](/help/sites-cloud/administering/translation/preparation.md) para obtener más información.

## Plantillas {#templates}

AEM En la práctica, una [plantilla](/help/sites-cloud/authoring/page-editor/templates.md) es un tipo especializado de página que se usa como base para cualquier página nueva que se cree.

La plantilla define la estructura de una página, incluida una imagen en miniatura y otras propiedades. Por ejemplo, puede tener plantillas independientes para páginas de productos, mapas del sitio e información de contacto. Las plantillas están formadas por [componentes](#components).

AEM incluye varias plantillas listas para usar de forma predeterminada. Las plantillas disponibles dependen del sitio web individual. Los campos principales son:

* **Título**: el título mostrado en la página web resultante
* **Nombre** - Se usa al nombrar la página
* **Plantilla**: una lista de plantillas disponibles para usar al generar la nueva página

## Componentes {#components}

AEM [Componentes](/help/implementing/developing/components/overview.md) son los elementos proporcionados por los elementos para que pueda agregar tipos de contenido específicos. AEM El complemento incluye una serie de componentes predeterminados, denominados [componentes principales](/help/implementing/developing/components/overview.md#core-components), que proporcionan una funcionalidad completa. Algunos ejemplos de componentes son los siguientes:

* Texto
* Imagen
* Título
* Carrusel
* Y muchos más

Una vez que haya creado y abierto una página, puede [añadir contenido mediante los componentes](/help/sites-cloud/authoring/page-editor/edit-content.md#inserting-a-component) que están disponibles en el [explorador de componentes](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser).

>[!TIP]
>
>La [consola Componentes](/help/sites-cloud/authoring/components-console.md) aporta una visión general de los componentes de la instancia.
