---
title: Sistema de estilos
description: El sistema de estilos permite a un autor de plantillas definir clases de estilos en la política de contenido de un componente, de modo que un autor de contenido puede seleccionarlos al editar el componente en una página. Estos estilos pueden ser variaciones visuales alternativas de un componente, lo que hacen que este sea más flexible.
exl-id: 224928dd-e365-4f3e-91af-4d8d9f47efdd
source-git-commit: 635f4c990c27a7646d97ebd08b453c71133f01b3
workflow-type: tm+mt
source-wordcount: '1319'
ht-degree: 59%

---

# Sistema de estilos{#style-system}

El sistema de estilos permite a un autor de plantillas definir clases de estilos en la política de contenido de un componente, de modo que un autor de contenido puede seleccionarlos al editar el componente en una página. Estos estilos pueden ser variaciones visuales alternativas de un componente, por lo que el componente es más flexible.

Esto elimina la necesidad de desarrollar un componente personalizado para cada estilo o de personalizar el cuadro de diálogo del componente para habilitar dicha funcionalidad de estilo. AEM Esto conduce a componentes más reutilizables que se pueden adaptar rápida y fácilmente a las necesidades de los autores de contenido sin ningún tipo de desarrollo back-end de la parte superior de la pantalla.

## Caso práctico    {#use-case}

Los autores de plantillas no solo necesitan la capacidad de configurar el funcionamiento de los componentes para los autores de contenido, sino también de configurar una serie de variaciones visuales alternativas de un componente.

Del mismo modo, los autores de contenido no solo necesitan la capacidad de estructurar y organizar su contenido, sino también de seleccionar cómo se presenta visualmente.

El sistema de estilos proporciona una solución unificada a los requisitos del autor de plantillas y del autor de contenido:

* Los autores de plantillas pueden definir clases de estilo en la política de contenido de los componentes.
* Los autores de contenido pueden seleccionar estas clases de una lista desplegable al editar el componente en una página para que puedan aplicar los estilos correspondientes.

A continuación, la clase de estilo se inserta en el elemento envolvente de decoración del componente para que el desarrollador de componentes no tenga que preocuparse por administrar los estilos más allá de proporcionar sus reglas CSS.

## Información general {#overview}

Por lo general, el uso del sistema de estilos se realiza de la siguiente manera.

1. El diseñador web crea diferentes variaciones visuales de un componente.

1. Se proporciona al desarrollador de HTML la salida HTML de los componentes y las variaciones visuales deseadas que se van a implementar.

1. El desarrollador de HTML define las clases CSS que corresponden a cada variación visual y que deben insertarse en el elemento que ajusta los componentes.

1. El desarrollador de HTML implementa el código CSS correspondiente (y opcionalmente el código JS) para cada una de las variaciones visuales para que su aspecto se corresponda a como están definidas.

1. El desarrollador de AEM coloca el CSS proporcionado (y el JS opcional) en una [biblioteca de cliente](/help/implementing/developing/introduction/clientlibs.md) y la implementa.

1. El desarrollador de AEM o el creador de plantillas configuran las plantillas de página, editan la política de cada componente diseñado, añaden las clases CSS definidas, asignan nombres de usuario sencillos a cada estilo e indican los estilos que se pueden combinar.

1. El autor de páginas de AEM puede seleccionar los estilos diseñados en el editor de página a través del menú Estilo de la barra de herramientas del componente.

AEM Tenga en cuenta que solo los tres últimos pasos se llevan a cabo en la práctica en el ámbito de la. AEM Esto significa que todo el desarrollo del CSS y el Javascript necesarios se puede realizar sin necesidad de tener que realizar ninguna tarea de la aplicación de la aplicación de la manera más sencilla y sencilla

AEM En realidad, la implementación de los estilos solo requiere la implementación de la selección y la selección en los componentes de las plantillas deseadas.

En el diagrama siguiente, se ilustra la arquitectura del sistema de estilos.

![aem-style-system](/help/sites-cloud/authoring/assets/style-system-architecture.png)

## Uso {#use}

Para demostrar la función, utilizaremos como ejemplo la implementación por [WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=es) del [componente de título](https://www.adobe.com/go/aem_cmp_title_v2_es) del componente principal.

En las secciones siguientes [Como autor de contenido](#as-a-content-author) y [Como autor de plantillas](#as-a-template-author), se describe cómo probar la funcionalidad del sistema de estilos mediante el sistema de estilos de WKND.

Si desea utilizar el sistema de estilos para sus propios componentes, haga lo siguiente:

1. Instale el CSS como bibliotecas de cliente, tal como se describe en la sección [Información general](#overview).
1. Configure las clases CSS que desee poner a disposición de los autores de contenido como se describe en la sección [Como autor de plantillas](#as-a-template-author).
1. Los autores de contenido pueden utilizar los estilos como se describe en la sección [Como autor de contenido](#as-a-content-author).

### Como autor de contenido    {#as-a-content-author}

1. Después de instalar el proyecto WKND, vaya a la página de inicio maestra en inglés de WKND en `http://<host>:<port>/sites.html/content/wknd/language-masters/en` y edite la página.
1. Seleccione un componente del **Título** más abajo en la página

   ![Sistema de estilos para el autor](/help/sites-cloud/authoring/assets/style-system-author1.png)

1. Toque o haga clic en el botón **Estilos** de la barra de herramientas del componente **Lista** para abrir el menú Estilo y cambiar el aspecto del componente.

   ![Seleccionar estilos](/help/sites-cloud/authoring/assets/style-system-author2.png)

   >[!NOTE]
   >
   >En este ejemplo, los estilos **Colores** (**Negro**, **Blanco** y **Gris**) se excluyen mutuamente, mientras que las opciones **Estilo** (**Subrayado**, **Alinear a la derecha** y **Miniespaciado**) se pueden combinar. Esto se puede [configurar en la plantilla como el autor de la misma](#as-a-template-author).

### Como autor de plantillas    {#as-a-template-author}

1. Mientras edita la página de inicio maestra en inglés de WKND en `http://<host>:<port>/sites.html/content/wknd/language-masters/en`, edite la plantilla de la página a través de **Información de la página -> Editar plantilla**.

   ![Editar plantilla](/help/sites-cloud/authoring/assets/style-system-edit-template.png)

1. Edite la política del componente **Título** al tocar o hacer clic en el botón **Política** del componente.

   ![Editar política](/help/sites-cloud/authoring/assets/style-system-edit-policy.png)

1. En la pestaña Estilos de las propiedades, puede ver cómo se han configurado los estilos.

   ![Editar propiedades](/help/sites-cloud/authoring/assets/style-system-properties.png)

   * **Nombre de grupo:** Los estilos se pueden agrupar en el menú de estilo que verá el autor del contenido al configurar el estilo del componente.
   * **Los estilos se pueden combinar:** Permite seleccionar varios estilos dentro de ese grupo al mismo tiempo.
   * **Nombre de estilo:** Descripción del estilo que se mostrará al autor del contenido al configurar el estilo del componente.
   * **Clases CSS:** El nombre real de la clase CSS asociada al estilo.

   Utilice los controladores de arrastre para ordenar los grupos y los estilos dentro de los grupos. Utilice los iconos Agregar o Eliminar para agregar o quitar grupos o estilos dentro de los grupos.

>[!CAUTION]
>
>Las clases CSS, y cualquier código Javascript necesario, configuradas como propiedades de estilo de la política de un componente deben implementarse como [Bibliotecas de cliente](/help/implementing/developing/introduction/clientlibs.md) para trabajar.

## Configuración {#setup}

La versión 2 y versiones posteriores de los componentes principales están totalmente habilitadas para aprovechar el sistema de estilos y no requieren ninguna configuración adicional.

Los pasos siguientes solo son necesarios para habilitar el sistema de estilos para sus propios componentes personalizados o para [habilitar la pestaña opcional Estilos en el cuadro de diálogo Editar.](#enable-styles-tab-edit)

### Activar la pestaña Estilo en el cuadro de diálogo Diseño {#enable-styles-tab-design}

Para que un componente funcione con el sistema de estilos de AEM y se muestre la pestaña Estilo en el cuadro de diálogo de diseño, el desarrollador de componentes debe incluir la pestaña de estilo con la siguiente configuración del componente:

* `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_design/styletab"`
* `sling:resourceType = "granite/ui/components/coral/foundation/include"`

>[!NOTE]
Utiliza [superposiciones](/help/implementing/developing/introduction/overlays.md) mediante la fusión de recursos de [Sling](/help/implementing/developing/introduction/sling-resource-merger.md).

AEM AEM Con el componente configurado, los estilos configurados por los autores de la página se insertan automáticamente mediante el elemento de decoración que se ajusta automáticamente a todos los componentes editables, de forma que se puede crear una nueva página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página. El componente en sí no necesita hacer nada más para que esto suceda.

### Activar la pestaña Estilos en el cuadro de diálogo Editar {#enable-styles-tab-edit}

También hay disponible una pestaña Estilos opcional en el cuadro de diálogo Editar. A diferencia de la pestaña Cuadro de diálogo de diseño, la pestaña en el cuadro de diálogo Editar no es esencial para que funcione el sistema de estilos, pero es una interfaz alternativa opcional para que un autor de contenido defina estilos.

La pestaña Editar del cuadro de diálogo se puede incluir de forma similar a la pestaña Cuadro de diálogo de diseño:

* `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_edit/styletab"`
* `sling:resourceType = "granite/ui/components/coral/foundation/include"`

>[!NOTE]
Utiliza [superposiciones](/help/implementing/developing/introduction/overlays.md) mediante la fusión de recursos de [Sling](/help/implementing/developing/introduction/sling-resource-merger.md).

>[!NOTE]
>
La pestaña Estilos del cuadro de diálogo Editar no está activada de forma predeterminada.

### Estilos con nombres de elemento       {#styles-with-element-names}

Un desarrollador también puede configurar una lista de nombres de elemento permitidos para los estilos del componente con la propiedad matriz de cadenas `cq:styleElements`. A continuación, en la pestaña Estilos de la directiva dentro del cuadro de diálogo de diseño, el autor de la plantilla también puede elegir un nombre de elemento que se establecerá para cada estilo. Se establecerá el nombre del elemento del elemento envolvente.

Esta propiedad se establece en el nodo `cq:Component`. Por ejemplo:

* `/apps/<yoursite>/components/content/list@cq:styleElements=[div,section,span]`

>[!CAUTION]
>
Evite definir nombres de elementos para los estilos que se pueden combinar. Cuando se definen varios nombres de elemento, el orden de prioridad es:
>
1. HTL tiene prioridad sobre todo: `data-sly-resource="${'path/to/resource' @ decorationTagName='span'}`.
1. A continuación, entre diversos estilos activos, se toma el primer estilo de la lista de estilos configurados en la política del componente.
1. Finalmente, el componente de `cq:htmlTag`/ `cq:tagName` se considera como un valor de reserva.
>

Esta capacidad para definir nombres de estilo resulta útil para los componentes genéricos, como el contenedor de diseño o el componente Fragmento de contenido, a fin de darles un significado adicional.

Por ejemplo, permite que un contenedor de diseños reciba valores semánticos como `<main>`, `<aside>`, `<nav>`, etc.
