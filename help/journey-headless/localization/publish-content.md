---
title: Publicar contenido traducido
description: Aprenda a publicar el contenido localizado.
source-git-commit: 3ab886361dc01c943bd00025695d34a218b1aa41
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 0%

---

# Publicar contenido traducido {#publish-content}

Aprenda a publicar el contenido localizado.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido de localización AEM sin encabezado, [Traducir contenido,](configure-connector.md) ha aprendido a utilizar AEM proyectos de traducción para traducir su contenido sin encabezado. Ahora debería:

* Comprender qué es un proyecto de traducción.
* Poder crear nuevos proyectos de traducción.
* Utilice proyectos de traducción para traducir el contenido sin encabezado.

Ahora que la traducción inicial ha finalizado, este artículo le explica el siguiente paso para publicar ese contenido y qué hacer para actualizar sus traducciones a medida que cambia el contenido raíz del idioma subyacente.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo publicar contenido sin encabezado en AEM y cómo crear un flujo de trabajo continuo para mantener las traducciones actualizadas. Después de leer este documento, debe:

* Comprender el modelo de creación y publicación de AEM.
* Obtenga información sobre cómo publicar el contenido traducido.
* Puede implementar un modelo de actualización continua para el contenido traducido.

## Modelo de AEM Author-Publish {#author-publish}

Antes de publicar el contenido, es aconsejable comprender AEM modelo de creación y publicación. En sus términos más sencillos, AEM divide a los usuarios del sistema en dos grupos.

1. Aquellos que crean y administran el contenido y el sistema
1. Los que consumen el contenido del sistema.

Por lo tanto, AEM se separa físicamente en dos instancias.

1. La instancia **author** es el sistema donde los autores y administradores de contenido trabajan para crear y administrar contenido.
1. La instancia **publish** es el sistema que envía el contenido a los consumidores.

Una vez creado el contenido en la instancia de autor, debe transferirse a la instancia de publicación para que esté disponible para el consumo. El proceso de transferencia del autor a la publicación se llama **publicación**.

## Publicación del contenido traducido {#publishing}

Una vez que esté satisfecho con el estado del contenido traducido, puede publicarlo para que los servicios sin encabezado puedan consumirlo. La forma más sencilla de hacerlo es ir a la carpeta de recursos del proyecto.

```text
/content/dam/<your-project>/
```

En esta ruta tiene subcarpetas para cada idioma de traducción y puede elegir cuál publicar.

1. Vaya a **Navegación** -> **Assets** -> **Archivos** y abra la carpeta del proyecto.
1. Aquí podrá ver la carpeta raíz del idioma y todas las demás carpetas del idioma. Seleccione el idioma o los idiomas localizados que desee publicar.
   ![Seleccionar carpeta de idioma](assets/select-language-folder.png)
1. Toque o haga clic en **Administrar publicación**.
1. En la ventana **Administrar publicación**, asegúrese de que **Publicar** esté automáticamente seleccionado en **Acción** y de que **Ahora** esté seleccionado en **Programación**. Haga clic o pulse **Siguiente**.
   ![Administrar opciones de publicación](assets/manage-publication-options.png)
1. En la siguiente ventana **Administrar publicación**, confirme que las rutas adecuadas están seleccionadas. Toque o haga clic en **Publicar**.
   ![Administrar ámbito de publicación](assets/manage-publication-scope.png)
1. AEM confirma la acción de publicación con un mensaje emergente en la parte inferior de la pantalla.
   ![Pancarta publicada de recursos](assets/resources-published-message.png)

Ya se ha publicado su contenido sin encabezado localizado. Ahora puede ser accedido y consumido por sus servicios sin periféricos.

>[!TIP]
>
>Puede seleccionar varios elementos (es decir, carpetas de varios idiomas) al publicar para publicar varias localizaciones a la vez.

Existen opciones adicionales al publicar el contenido, como programar una publicación que está fuera del ámbito de este recorrido. Consulte la sección [Recursos adicionales](#additional-resources) al final del documento para obtener más información.

## Actualización del contenido traducido {#updating-translations}

La localización y la traducción rara vez son un ejercicio aislado. Normalmente, los autores de contenido siguen agregando y modificando el contenido en la raíz del idioma una vez completada la localización inicial. Esto significa que también deberá actualizar el contenido traducido.

Los requisitos específicos del proyecto definirán la frecuencia con la que deberá actualizar las traducciones y qué proceso de decisión se seguirá antes de realizar una actualización. Una vez que haya decidido actualizar sus traducciones, el proceso en AEM es muy sencillo. Como la traducción inicial se basó en un proyecto de traducción, también lo son las actualizaciones.

1. Vaya a **Navegación** -> **Recursos** -> **Archivos**. Recuerde que el contenido sin encabezado de AEM se almacena como recursos conocidos como fragmentos de contenido.
1. Seleccione la raíz de idioma del proyecto. En este caso, se ha seleccionado `/content/dam/wknd/en`.
1. Toque o haga clic en el selector de raíl y muestre el panel **Referencias**.
1. Toque o haga clic en **Textos en idiomas**.
1. Marque la casilla **Language Copies** .
1. Expanda la sección **Actualizar copias de idioma** en la parte inferior del panel de referencias.
1. En la lista desplegable **Proyecto**, seleccione **Agregar a un proyecto de traducción existente**.
1. En la lista desplegable **Existing Translation Project**, seleccione el proyecto creado para la traducción inicial.
1. Toque o haga clic en **Inicio**.

![Agregar elementos a un proyecto de traducción existente](assets/add-to-existing-project.png)

El contenido se agrega al proyecto de traducción existente. Para ver el proyecto de traducción:

1. Vaya a **Navegación** -&amp; **Proyectos**.
1. Toque o haga clic en el proyecto que acaba de actualizar.
1. Toque o haga clic en el idioma o en uno de los idiomas que ha actualizado.

Verá que se ha agregado una nueva tarjeta de trabajo al proyecto. En este ejemplo, se agregó otra traducción al español.

![Se ha añadido un trabajo de traducción adicional](assets/additional-translation-job.png)

Observará que las estadísticas que aparecen en la nueva tarjeta (número de recursos y fragmentos de contenido) son diferentes. Esto se debe a que AEM reconoce qué ha cambiado desde la última traducción y solo incluye contenido nuevo que debe traducirse (tanto contenido actualizado retraducido como traducción por primera vez de contenido nuevo).

A partir de este punto, [inicie y administre su trabajo de traducción igual que hizo el original.](translate-content.md#using-translation-project)

## ¿Fin del Recorrido? {#end-of-journey}

Felicitaciones! ¡Ha completado el recorrido de localización sin periféricos! Ahora debería:

* Obtenga información general sobre qué es la entrega de contenido sin encabezado.
* Tenga una comprensión básica AEM las funciones sin encabezado.
* Comprenda AEM funciones de localización y cómo se relacionan con contenido sin encabezado.
* Tener la capacidad de empezar a localizar su propio contenido sin encabezado.

Ahora está listo para localizar su propio contenido sin encabezado en AEM. Sin embargo, AEM es una herramienta potente y hay muchas opciones adicionales disponibles. Consulte algunos de los recursos adicionales disponibles en la siguiente sección para obtener más información sobre las funciones que ha visto en este recorrido.

## Recursos adicionales {#additional-resources}

* [Administración de proyectos de traducción](/help/sites-cloud/administering/translation/managing-projects.md) : conozca los detalles de los proyectos de traducción y las funciones adicionales, como los flujos de trabajo de traducción humana y los proyectos en varios idiomas.
* [Conceptos de creación](/help/sites-cloud/authoring/getting-started/concepts.md) : obtenga más información sobre el modelo de creación y publicación de AEM en más detalle. Este documento se centra en la creación de páginas en lugar de en los fragmentos de contenido, pero la teoría sigue aplicándose.
* [Publicación de páginas](/help/sites-cloud/authoring/fundamentals/publishing-pages.md) : obtenga información sobre las funciones adicionales disponibles al publicar contenido. Este documento se centra en la creación de páginas en lugar de en los fragmentos de contenido, pero la teoría sigue aplicándose.
