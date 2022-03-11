---
title: Introducción a la traducción de AEM Sites
description: Obtenga información sobre cómo organizar el contenido de AEM Sites y cómo funcionan AEM herramientas de traducción.
index: true
hide: false
hidefromtoc: false
exl-id: 9bfc3995-ac8e-488e-b68f-9e1b5b4a3176
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '1412'
ht-degree: 0%

---

# Introducción a la traducción a AEM Sites {#getting-started}

Obtenga información sobre cómo organizar el contenido de AEM Sites y cómo funcionan AEM herramientas de traducción.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido de traducción de AEM Sites, [Obtenga información sobre el contenido de AEM Sites y cómo traducirlo en AEM](learn-about.md) ha aprendido la teoría básica de AEM Sites y ahora debería:

* Comprender los conceptos básicos de la creación de contenido de AEM Sites.
* Familiarícese con cómo AEM admite la traducción.

Este artículo se basa en estos aspectos básicos para que pueda comprender cómo AEM almacena y administra el contenido y cómo puede utilizar AEM herramientas de traducción para traducir dicho contenido.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo empezar a traducir contenido de sitios en AEM. Después de leer, debe:

* Comprender la importancia de la estructura de contenido para la traducción.
* Comprender cómo AEM almacena contenido.
* Familiarícese con AEM herramientas de traducción.

## Requisitos y requisitos previos {#requirements-prerequisites}

Antes de comenzar a traducir el contenido de AEM, existen varios requisitos.

### Conocimiento {#knowledge}

* Experiencia en la traducción de contenido en un CMS
* Experiencia utilizando las funciones básicas de un CMS a gran escala
* Tener un conocimiento práctico de AEM manipulación básica
* Comprensión del servicio de traducción que utiliza
* Tenga una comprensión básica del contenido que está traduciendo

>[!TIP]
>
>Si no está familiarizado con el uso de un CMS a gran escala como AEM, considere la posibilidad de revisar la [Gestión básica](/help/sites-cloud/authoring/getting-started/basic-handling.md) documentación antes de continuar. La documentación de Gestión básica no forma parte del recorrido, por lo que debe volver a esta página cuando haya terminado.

### Herramientas {#tools}

* Acceso a espacio aislado para probar la traducción del contenido
* Credenciales para conectarse al servicio de traducción preferido
* Sea miembro de `project-administrators` grupo en AEM

## Almacenamiento AEM contenido {#content-in-aem}

Para el especialista en traducción, no es importante comprender en profundidad cómo AEM administra el contenido. Sin embargo, familiarizarse con los conceptos básicos y la terminología será útil, ya que más adelante utilizará AEM herramientas de traducción. Lo más importante es que debe comprender su propio contenido y cómo está estructurado para traducirlo de forma eficaz.

### Consola Sitios {#sites-console}

La consola Sitios proporciona una descripción general de la estructura del contenido, lo que facilita la navegación por el contenido y la administración al crear páginas nuevas, mover y copiar páginas, así como publicar contenido.

Para acceder a la consola Sitios :

1. En el menú de navegación global, toque o haga clic en **Navegación** -> **Sitios**.
1. La consola Sitios se abre en el nivel superior del contenido.
1. Asegúrese de que la variable **Vista de columna** se selecciona mediante el selector de vista situado en la parte superior derecha de la ventana.

   ![Selección de la vista de columna](assets/selecting-column-view.png)

1. Al tocar o hacer clic en un elemento de una columna, se muestra el contenido debajo de él en la jerarquía de la columna de la derecha.

   ![Jerarquía de contenido](assets/sites-console-hierarchy.png)

1. Al tocar o hacer clic en la casilla de verificación de un elemento de una columna, se selecciona ese elemento y se muestran los detalles del elemento seleccionado en la columna de la derecha, así como varias acciones disponibles para el elemento seleccionado en la barra de herramientas de arriba.

   ![Selección de contenido](assets/sites-console-selection.png)

1. Al tocar o hacer clic en el selector de raíl en la parte superior izquierda, también puede mostrar la variable **Árbol de contenido** para ver un árbol de información general del contenido.

   ![Vista del árbol de contenido](assets/sites-console-content-tree.png)

Con estas sencillas herramientas, puede navegar de forma intuitiva por la estructura de contenido.

>[!NOTE]
>
>El arquitecto de contenido suele definir la estructura de contenido, mientras que los autores de contenido crean el contenido dentro de esa estructura.
>
>Como especialista en traducción, es importante comprender simplemente cómo navegar por esa estructura y comprender dónde se encuentra el contenido.

### Editor de página {#page-editor}

La consola Sitios le permite desplazarse por el contenido y proporciona una descripción general de su estructura. Para ver los detalles de una página individual, debe utilizar el editor de sitios.

Para editar una página:

1. Utilice la consola Sitios para localizar y seleccionar una página. Recuerde que debe tocar o hacer clic en la casilla de verificación de una página individual para seleccionarla.

   ![Selección de una página para editar](assets/sites-editor-select-page.png)

1. Toque . **Editar** en la barra de herramientas.
1. El editor de sitios se abre con la página seleccionada cargada para su edición en una nueva ficha del explorador.
1. Si toca o pasa el ratón por encima del contenido, se muestran selectores para componentes individuales. Los componentes son los bloques de creación de arrastrar y soltar que conforman la página.

   ![Edición de una página](assets/sites-editor-title.png)

Puede volver a la consola Sitios volviendo a esa pestaña en el explorador en cualquier momento. Con el editor de sitios puede ver rápidamente el contenido de la página, tal y como lo verán los autores de contenido y la audiencia.

>[!NOTE]
>
>Los autores de contenido crean el contenido del sitio mediante el editor de sitios.
>
>Como especialista en traducción, es importante comprender simplemente cómo ver los detalles de ese contenido con el editor de sitios.

## La estructura es clave {#content-structure}

AEM contenido depende de su estructura. AEM impone pocos requisitos a la estructura de contenido, pero tener en cuenta la jerarquía de contenido como parte de la planificación del proyecto puede hacer que la traducción sea mucho más sencilla.

>[!TIP]
>
>Planifique la traducción al principio del proyecto de AEM. Trabaje en estrecha colaboración con el director del proyecto y los arquitectos de contenido desde el principio.
>
>Un administrador de proyectos de internacionalización puede ser una persona independiente, cuya responsabilidad es definir qué contenido debe traducirse y qué no, y qué contenido traducido pueden modificar los productores de contenido regionales o locales.

## Estructura de contenido recomendada {#recommended-structure}

Como se recomendó anteriormente, trabaje con su arquitecto de contenido para determinar la estructura de contenido adecuada para su propio proyecto. Sin embargo, lo siguiente es una estructura probada, simple e intuitiva que es bastante efectiva.

Defina una carpeta base para su proyecto en `/content`.

```text
/content/<your-project>
```

El idioma en el que se crea el contenido se denomina raíz del idioma. En nuestro ejemplo es inglés y debería estar por debajo de este camino.

```text
/content/<your-project>/en
```

Todo el contenido del proyecto que pueda ser necesario localizar debe colocarse bajo la raíz del idioma.

```text
/content/<your-project>/en/<your-project-content>
```

Las traducciones deben crearse como carpetas del mismo nivel a lo largo de la raíz del idioma con su nombre de carpeta que represente el código de idioma ISO-2 del idioma. Por ejemplo, el alemán tendría la siguiente ruta.

```text
/content/<your-project>/de
```

>[!NOTE]
>
>Por lo general, el arquitecto de contenido es responsable de crear estas carpetas de idioma. Si no se crean, AEM podrá crear más adelante trabajos de traducción.

La estructura final puede tener un aspecto similar al siguiente.

```text
/content
    |- your-project
        |- en
            |- some
            |- exciting
            |- sites
            |- content
        |- de
        |- fr
        |- it
        |- ...
    |- another-project
    |- ...
```

Debe tomar nota de la ruta específica del contenido, ya que será necesaria más adelante para configurar la traducción.

>[!NOTE]
>
>Generalmente es responsabilidad del arquitecto de contenido definir la estructura de contenido, a menudo en colaboración con el especialista en traducción.
>
>Se detalla aquí para que sea completo.

## AEM herramientas de traducción {#translation-tools}

Ahora que comprende la consola y el editor del sitio y la importancia de la estructura del contenido, podemos ver cómo traducir el contenido. Las herramientas de traducción en AEM son bastante poderosas, pero son simples de entender a un alto nivel.

* **Conector de traducción** - El conector es el vínculo entre AEM y el servicio de traducción que utiliza.
* **Reglas de traducción** - Las reglas definen qué contenido bajo rutas particulares se debe traducir.
* **Proyectos de traducción** - Los proyectos de traducción reúnen contenido que debe tratarse como un esfuerzo de traducción único y rastrean el progreso de la traducción, interconectándose con el conector para transmitir el contenido a traducir y recibirlo de nuevo desde el servicio de traducción.

Generalmente, solo se configura un conector una vez para la instancia y las reglas por proyecto. A continuación, utilice proyectos de traducción para traducir su contenido y mantener sus traducciones actualizadas de forma continua.

## Siguientes pasos {#what-is-next}

Ahora que ha completado esta parte del recorrido de traducción de AEM Sites, debe:

* Comprender la importancia de la estructura de contenido para la traducción.
* Comprender cómo AEM almacena contenido.
* Familiarícese con AEM herramientas de traducción.

Aproveche este conocimiento y continúe con su recorrido de traducción de AEM Sites revisando el documento [Configuración del conector de traducción](configure-connector.md) donde aprenderá a conectar AEM a un servicio de traducción.|

## Recursos adicionales {#additional-resources}

Aunque se recomienda pasar a la siguiente parte del recorrido de traducción revisando el documento [Configuración del conector de traducción](configure-connector.md) los siguientes son algunos recursos opcionales adicionales que profundizan en algunos conceptos mencionados en este documento, pero no son necesarios para continuar en el recorrido.

* [Gestión básica de AEM](/help/sites-cloud/authoring/getting-started/basic-handling.md) : Conozca los conceptos básicos de la interfaz de usuario de AEM para poder navegar cómodamente y realizar tareas esenciales como encontrar el contenido.
* [Identificación del contenido para traducir](/help/sites-cloud/administering/translation/rules.md) : Aprenda cómo las reglas de traducción identifican el contenido que necesita traducción.
* [Configuración del marco de integración de traducción](/help/sites-cloud/administering/translation/integration-framework.md) - Aprenda a configurar el marco de integración de traducción para integrarlo con servicios de traducción de terceros.
* [Administración de proyectos de traducción](/help/sites-cloud/administering/translation/managing-projects.md) - Aprenda a crear y administrar proyectos de traducción automática y humana en AEM.
