---
title: Uso de plantillas de página con el editor universal
description: Aprenda a crear y utilizar plantillas de página con el editor universal.
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 773ce75975f4dcc2c5310422bcc377b487ebec25
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 2%

---


# Uso de plantillas de página con el editor universal {#page-templates}

Aprenda a crear y utilizar plantillas de página con el editor universal.

>[!NOTE]
>
>Esta función estará disponible en una próxima versión de AEM as a Cloud Service.

## ¿Qué son las plantillas de página? {#what-are}

Las directrices de marca y marketing suelen dictar diseños específicos para las páginas de contenido. También suele ser una realidad práctica que muchas de las páginas compartirán la misma estructura y diseño. Para ahorrar tiempo a los autores de contenido, se pueden crear páginas a partir de plantillas.

Las plantillas de página sirven como copias maestras de los diseños de página. Al crear una página a partir de una plantilla, el contenido de la plantilla se copia en la nueva página, lo que ayuda a predefinir el diseño y el contenido inicial de la página para el autor del contenido, lo que les ahorra tiempo.

## Creación de una plantilla de página {#creating}

Puede crear una plantilla de página creando una página nueva o utilizando una página existente para que sirva como plantilla. En ambos casos, utiliza la consola [**Sitios**.](/help/sites-cloud/authoring/sites-console/introduction.md)

### Creación de una nueva plantilla {#create-new}

1. Use la consola **Sitios** para desplazarse a la ubicación en la que desea crear la nueva página que servirá como plantilla y [cree la página como lo haría con cualquier otra.](/help/sites-cloud/authoring/sites-console/creating-pages.md)

1. Una vez creada la página y que vuelva a la consola, selecciónela y, a continuación, toque o haga clic en el icono [**Propiedades**](/help/sites-cloud/authoring/sites-console/page-properties.md) de la barra de herramientas.

1. En la ficha **Avanzado** del cuadro de diálogo de propiedades de la sección **Configuración de plantilla**, seleccione la opción **Usar como plantilla**.

1. En el campo **Nombre de plantilla**, proporcione un nombre descriptivo.

   * Este es el nombre que mostrará la creación de nuevas páginas de contenido y usted selecciona una plantilla en la que basar la nueva página.

1. Haga clic o pulse en **Guardar y cerrar**.

La nueva página ahora se puede utilizar como plantilla al crear páginas nuevas.

### Uso de una página existente como plantilla {#existing-page}

1. Use la consola **Sites** para [navegar a la ubicación de la página](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources) que desee usar como plantilla.

1. Seleccione la página y, a continuación, toque o haga clic en el icono [**Propiedades**](/help/sites-cloud/authoring/sites-console/page-properties.md) de la barra de herramientas.

1. En la ficha **Avanzado** del cuadro de diálogo de propiedades de la sección **Configuración de plantilla**, seleccione la opción **Usar como plantilla**.

1. En el campo **Nombre de plantilla**, proporcione un nombre descriptivo.

   * Este es el nombre que mostrará la creación de nuevas páginas de contenido y usted selecciona una plantilla en la que basar la nueva página.

1. Haga clic o pulse en **Guardar y cerrar**.

La página seleccionada ahora se puede utilizar como plantilla al crear páginas nuevas.

## Creación de una página a partir de una plantilla {#creating-from-template}

Crear una página a partir de una plantilla para usarla con el editor universal es el mismo flujo de trabajo que al [crear la página como lo haría con cualquier otro.](/help/sites-cloud/authoring/sites-console/creating-pages.md)

1. Use la consola **Sitios** para [ir a la ubicación](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources) donde desea crear la nueva página.

1. Haga clic o pulse **Crear** -> **Página**.

1. En la ficha **Plantilla** del asistente **Crear página**, puede seleccionar en qué plantilla desea basar la nueva página. Pulse o haga clic en la plantilla que desee para seleccionarla y, a continuación, pulse o haga clic en **Siguiente**.

Complete el asistente como lo haría para cualquier otra página y ha creado la nueva página basada en la plantilla seleccionada.

## Editor universal y editor de páginas {#page-vs-universal}

AEM Las plantillas de página para el Editor universal resuelven el mismo problema que las [plantillas de página para el Editor de página de la página de la:](/help/sites-cloud/authoring/page-editor/templates.md) para poder reutilizar el contenido y crear páginas rápidamente basándose en un conjunto de diseños predefinidos. Sin embargo, resuelven el problema de maneras muy diferentes. Si usa el editor de páginas, tenga en cuenta estas diferencias.

* Las páginas creadas a partir de plantillas de páginas para el Editor universal son copias independientes de la plantilla.
* Por lo tanto, si la plantilla cambia, las páginas resultantes no cambian.
* El autor del contenido puede modificar y actualizar el contenido de la página resultante según sea necesario sin restricciones de la plantilla.
