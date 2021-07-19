---
title: Traducir contenido
description: Utilice el conector de traducción y las reglas para traducir el contenido sin encabezado.
source-git-commit: 016b1126effb96598c9700377291333fb326c292
workflow-type: tm+mt
source-wordcount: '1248'
ht-degree: 0%

---

# Traducir contenido {#translate-content}

Utilice el conector de traducción y las reglas para traducir el contenido sin encabezado.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido de localización AEM sin encabezado, [Configure Translation Rules](translation-rules.md) ha aprendido a utilizar AEM reglas de traducción para identificar su contenido de traducción. Ahora debería:

* Comprender lo que hacen las reglas de traducción.
* Puede definir sus propias reglas de traducción.

Ahora que sus reglas de conector y traducciones están configuradas, este artículo le guía por el siguiente paso de traducir su contenido sin encabezado.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo utilizar AEM proyectos de traducción junto con el conector y las reglas de traducción para traducir contenido. Después de leer este documento, debe:

* Comprender qué es un proyecto de traducción.
* Poder crear nuevos proyectos de traducción.
* Utilice proyectos de traducción para traducir el contenido sin encabezado.

## Creación de un proyecto de traducción {#creating-translation-project}

Los proyectos de traducción permiten administrar la traducción de contenido AEM sin encabezado. Un proyecto de traducción contiene el contenido que se traducirá a otros idiomas.

Cuando se añade contenido a un proyecto de traducción, se crea un trabajo de traducción para él. Los trabajos proporcionan comandos e información de estado que se utilizan para administrar los flujos de trabajo de traducción humana y traducción automática que se ejecutan en los recursos.

Para crear un proyecto de traducción:

1. Vaya a **Navegación** -> **Recursos** -> **Archivos**. Recuerde que el contenido sin encabezado de AEM se almacena como recursos conocidos como fragmentos de contenido.
1. Seleccione la raíz de idioma del proyecto. En este caso, se ha seleccionado `/content/dam/wknd/en`.
1. Toque o haga clic en el selector de raíl y muestre el panel **Referencias**.
1. Toque o haga clic en **Textos en idiomas**.
1. Marque la casilla **Language Copies** .
1. Expanda la sección **Actualizar copias de idioma** en la parte inferior del panel de referencias.
1. En la lista desplegable **Proyecto**, seleccione **Crear proyecto de traducción**.
1. Proporcione un título adecuado para el proyecto de traducción.
1. Toque o haga clic en **Inicio**.

![Crear un proyecto de traducción](assets/create-translation-project.png)

Recibe un mensaje que indica que el proyecto se creó.

>[!NOTE]
>
>Se da por hecho que la estructura de idioma necesaria para los idiomas de traducción ya se ha creado como parte de la [definición de la estructura de contenido.](getting-started.md#content-structure) Esto debería hacerse en colaboración con el arquitecto de contenido.

## Uso de un proyecto de traducción {#using-translation-project}

Al crear el proyecto de traducción, AEM evaluó el contenido sin encabezado en la ruta seleccionada, así como en función de las reglas que definió anteriormente. Basándose en esas reglas, extraía el contenido que requiere traducción en un nuevo proyecto de traducción.

Para ver el proyecto de traducción:

1. Vaya a **Navegación** -&amp; **Proyectos**.
1. Toque o haga clic en el proyecto creado en la sección anterior.

![Proyecto de traducción](assets/translation-project.png)

El proyecto se divide en varias tarjetas.

* **Resumen** : Esta tarjeta muestra la información básica del encabezado del proyecto, incluido el propietario, el idioma y el proveedor de traducción.
* **Trabajo de traducción** : Esta tarjeta muestra una descripción general del trabajo de traducción real, incluido el estado, el número de recursos, etc.
* **Equipo** : esta tarjeta muestra los usuarios que están colaborando en este proyecto de traducción. Este recorrido no tratará este tema.
* **Tareas** : tareas adicionales asociadas con la traducción del contenido, como hacer elementos o elementos de flujo de trabajo. Este recorrido no tratará este tema.

Para ver el detalle del contenido sin encabezado incluido en este proyecto:

1. Toque o haga clic en el botón de elipsis en la parte inferior de la tarjeta **Translation Job**.
1. La ventana **Trabajo de traducción** enumera todos los elementos del trabajo.
   ![Detalles del trabajo de traducción](assets/translation-job-detail.png)
1. Toque o haga clic en una línea para ver el detalle de esa línea, teniendo en cuenta que una línea puede representar varios elementos de contenido para traducir.
1. Toque o haga clic en la casilla de verificación de selección de un elemento de línea para ver más opciones, como la opción de eliminarlo del trabajo o verlo en las consolas Fragmentos de contenido o Recursos .

![Opciones de trabajo de traducción](assets/translation-job-options.png)

Normalmente, el contenido del trabajo de traducción se inicia en el estado **Borrador** como se indica en la columna **Estado** de la ventana **Trabajo de traducción**.

Para iniciar el trabajo de traducción, vuelva a la descripción general del proyecto de traducción y pulse o haga clic en el botón de cheurón en la parte superior de la tarjeta **Translation Job** y seleccione **Start**.

![Iniciar trabajo de traducción](assets/start-translation-job.png)

AEM ahora se comunica con la configuración de traducción y el conector para enviar el contenido al servicio de traducción. Puede ver el progreso de la traducción volviendo a la ventana **Translation Job** y viendo la columna **State** de las entradas.

![Trabajo de traducción aprobado](assets/translation-job-approved.png)

Las traducciones automáticas se devuelven automáticamente con un estado de **Aprobado**. La traducción humana permite una mayor interacción, pero está fuera del alcance de este recorrido.

## Revisión del contenido traducido {#reviewing}

[Como se ha visto anteriormente, el contenido traducido por máquina ](#using-translation-project)  regresa a AEM con el estado de  **** Aprobado, ya que se supone que como se utiliza la traducción automática, no se requiere ninguna intervención humana. Sin embargo, por supuesto que todavía es posible revisar el contenido traducido.

Simplemente vaya al trabajo de traducción completado y seleccione un elemento de línea tocando o haciendo clic en la casilla de verificación. El icono **Mostrar en fragmento de contenido** se muestra en la barra de herramientas.

![Mostrar en fragmento de contenido](assets/reveal-in-content-fragment.png)

Toque o haga clic en ese icono para abrir el fragmento de contenido traducido en su consola de editor para ver los detalles del contenido traducido.

![Un fragmento de contenido traducido](assets/translated-content-fragment.png)

Puede modificar el fragmento de contenido según sea necesario, siempre que tenga el permiso adecuado, pero la edición de fragmentos de contenido está fuera del ámbito de este recorrido. Consulte la sección [Recursos adicionales](#additional-resources) al final de este documento para obtener más información sobre este tema.

El trabajo del proyecto es reunir todos los recursos relacionados con una traducción en un solo lugar para facilitar el acceso y una visión general clara. Sin embargo, como puede ver viendo el detalle de un elemento traducido, las traducciones en sí mismas regresan a la carpeta de recursos del idioma de traducción. En nuestro ejemplo aquí

```text
/content/dam/wknd/es
```

Si va a esta carpeta a través de **Navegación** -> **Archivos** -> **Recursos**, verá el contenido traducido.

![Estructura de carpetas de contenido traducida](assets/translated-file-content.png)

AEM marco de traducción recibe las traducciones del conector de traducción y, a continuación, crea automáticamente la estructura de contenido en función de la raíz del idioma y utilizando las traducciones proporcionadas por el conector.

Es importante comprender que este contenido no se publica. Permanece en la instancia de creación de AEM hasta que decida que está listo para publicarse. Veremos cómo hacerlo en el siguiente paso del recorrido de localización.

## Traducción humana {#human-translation}

Si el servicio de traducción proporciona traducción humana, el proceso de revisión ofrece más opciones. Por ejemplo, las traducciones vuelven al proyecto con el estado **Borrador** y deben revisarse y aprobarse o rechazarse manualmente.

La traducción humana está fuera del alcance de este recorrido de localización. Consulte la sección [Recursos adicionales](#additional-resources) al final de este documento para obtener más información sobre este tema.

## Siguientes pasos {#what-is-next}

Ahora que ha completado esta parte del recorrido de localización sin encabezado, debe:

* Comprender qué es un proyecto de traducción.
* Poder crear nuevos proyectos de traducción.
* Utilice proyectos de traducción para traducir el contenido sin encabezado.

Aproveche este conocimiento y continúe con su recorrido de localización AEM sin encabezado revisando el documento [Publicar contenido traducido](publish-content.md), donde aprenderá a publicar el contenido traducido y a actualizar esas traducciones a medida que cambie su contenido raíz de idioma.

## Recursos adicionales {#additional-resources}

Aunque se recomienda pasar a la siguiente parte del recorrido de localización sin encabezado revisando el documento [Publicar contenido traducido,](publish-content.md) los siguientes son algunos recursos opcionales adicionales que profundizan en algunos conceptos mencionados en este documento, pero no es necesario que continúen en el recorrido sin encabezado.

* [Administración de proyectos de traducción](/help/sites-cloud/administering/translation/managing-projects.md) : conozca los detalles de los proyectos de traducción y las funciones adicionales, como los flujos de trabajo de traducción humana y los proyectos en varios idiomas.
