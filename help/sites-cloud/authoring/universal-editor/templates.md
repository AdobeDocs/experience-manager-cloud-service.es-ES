---
title: Plantillas para crear páginas editables con el editor universal
description: Aprenda a crear plantillas que se puedan utilizar para crear páginas editables con el editor universal, lo que ahorra tiempo y garantiza una marca coherente.
solution: Experience Manager Sites
feature: Authoring
role: User
exl-id: f0d60086-e92e-4492-ad50-bef84fed2a82
source-git-commit: bcf0940d3365ecde6788772d28d32f22f367816d
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 26%

---


# Plantillas para crear páginas editables con el editor universal {#page-templates}

Aprenda a crear plantillas que se puedan utilizar para crear páginas editables con el editor universal, lo que ahorra tiempo y garantiza una marca coherente.

>[!NOTE]
>
>[También hay plantillas disponibles para crear páginas que se pueden editar con el editor de páginas](/help/sites-cloud/authoring/page-editor/templates.md).

## ¿Qué son las plantillas de página? {#what-are}

La personalización de marca y el marketing suelen dictar diseños específicos para las páginas de contenido. También suele ser una realidad en la práctica que muchas de sus páginas compartirán la misma estructura y diseño. Para ahorrar tiempo a los autores de contenido, las páginas pueden crearse a partir de plantillas.

Las plantillas de página sirven como copias principales de los diseños de página. Al crear una página a partir de una plantilla, el contenido inicial de la plantilla se copia en la nueva página, lo que ayuda a predefinir el diseño básico y el contenido de la página para el autor del contenido, lo que le ahorra tiempo.

## Activación de plantillas de página {#enabling-templates}

Para utilizar plantillas para crear páginas editables con el editor universal, debe activar la opción.

Habilite primero las plantillas editables para la configuración del sitio.

1. Use la consola **Sitios** y [seleccione la raíz del sitio](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources).
1. Una vez seleccionada la raíz del sitio, toque o haga clic en el icono [**Propiedades**](/help/sites-cloud/authoring/sites-console/page-properties.md) de la barra de herramientas.
1. En la ficha **Avanzado** del cuadro de diálogo de propiedades, tome nota del valor del campo **Configuración de nube**.
1. En la navegación principal, elija **Herramientas** -> **General** -> **Explorador de configuración**.
1. En el **[Explorador de configuración](/help/implementing/developing/introduction/configurations.md)**, seleccione la configuración que anotó en el paso anterior y toque o haga clic en **Propiedades** en la barra de herramientas.
1. En la ventana **Propiedades de configuración**, marque la opción **Plantillas editables**.
1. Haga clic o pulse en **Guardar y cerrar**.

Una vez habilitada la configuración, debe permitir las plantillas para el sitio.

1. Use la consola **Sitios** y [seleccione la raíz del sitio](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources).
1. Una vez seleccionada la raíz del sitio, toque o haga clic en el icono [**Propiedades**](/help/sites-cloud/authoring/sites-console/page-properties.md) de la barra de herramientas.
1. En la ficha **Avanzado** del cuadro de diálogo de propiedades de la sección **Configuración de plantilla**, toque o haga clic en el botón **Agregar**.
1. En el nuevo campo vacío que aparece en **Plantillas permitidas**, agregue la ruta de acceso `/conf/<site>/settings/wcm/templates/.*`.
1. Haga clic o pulse en **Guardar y cerrar**.

Ahora puede utilizar plantillas para crear páginas para el sitio. Esta tarea solo debe realizarse una vez cada sitio o configuración donde desee utilizar plantillas al crear páginas editables con el editor universal.

## Creación de una nueva plantilla {#create-new}

Puede [crear una nueva página](/help/sites-cloud/authoring/sites-console/creating-pages.md) para que sirva como plantilla o usar una página existente como base de una plantilla.

1. Use la consola **Sites** para [navegar a la página nueva o existente](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources) que desee usar como plantilla y toque o haga clic para seleccionarla.

1. Una vez seleccionada la página, toque o haga clic en el icono [**Propiedades**](/help/sites-cloud/authoring/sites-console/page-properties.md) de la barra de herramientas.

1. En la ficha **Avanzado** del cuadro de diálogo de propiedades en la sección **Configuración de plantilla**, seleccione la opción **Usar página como plantilla**.

1. Haga clic o pulse en **Guardar y cerrar**.

La nueva página ahora se puede utilizar como plantilla al crear páginas nuevas.

## Creación de una página a partir de una plantilla {#creating-from-template}

Crear una página a partir de una plantilla editable con el editor universal es el mismo flujo de trabajo que [crear cualquier otra página](/help/sites-cloud/authoring/sites-console/creating-pages.md).

1. Use la consola **Sites** para [ir a la ubicación](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources) donde desea crear la nueva página.

1. Haga clic o pulse **Crear** -> **Página**.

1. En la ficha **Plantilla** del asistente **Crear página**, puede seleccionar en qué plantilla desea basar la nueva página. Pulse o haga clic en la plantilla deseada para seleccionarla y, a continuación, pulse o haga clic en **Siguiente**.

Complete el asistente como lo haría para cualquier otra página y habrá creado su nueva página basada en la plantilla seleccionada.

## Páginas y plantillas {#pages-vs-templates}

Las plantillas de página solo definen el contenido inicial de las páginas. Las páginas se pueden editar completamente con el editor universal.

* Las páginas creadas a partir de plantillas de página son copias independientes de la plantilla.
* Si la plantilla cambia, las páginas existentes basadas en esa plantilla no cambian.
* El autor de contenido puede modificar y actualizar el contenido de la página resultante según sea necesario sin restricciones impuestas por la plantilla.

## Plantillas editables {#editable-templates}

Las páginas creadas con [Editor de páginas](/help/sites-cloud/authoring/page-editor/introduction.md) también pueden basarse en plantillas. Tanto las plantillas utilizadas para crear páginas para el editor universal como el editor de páginas aprovechan las [plantillas editables](/help/implementing/developing/components/templates.md) de AEM.

Las plantillas utilizadas para crear páginas editables con el Editor de páginas utilizan todas las funciones de las plantillas editables. Las plantillas utilizadas para crear páginas editables con el editor universal solo utilizan la función de contenido inicial.
