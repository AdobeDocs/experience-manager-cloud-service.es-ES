---
title: Personalización de contenido en una aplicación de ejemplo en React
description: Utilice una aplicación React de muestra para aprender a personalizar el contenido mediante la funcionalidad sin encabezado establecida en AEM as a Cloud Service.
hidefromtoc: true
index: false
exl-id: 32290ad4-d915-41b7-a073-2637eb38e978
feature: Headless
role: Admin, User, Developer
source-git-commit: f66ea281e6abc373e9704e14c97b77d82c55323b
workflow-type: ht
source-wordcount: '1017'
ht-degree: 100%

---


# Personalización de contenido en una aplicación de ejemplo en React {#customize-app}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_react_app"
>title="Personalización del contenido en una aplicación React de muestra"
>abstract="La versión de prueba de AEM sin encabezado viene con una aplicación React de muestra integrada, que puede personalizar."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_react_app_guide"
>title="Lanzamiento del editor de fragmentos de contenido"
>abstract="Ahora analicemos cómo funciona la creación de contenido sin encabezado. La versión de prueba de AEM sin encabezado viene con una aplicación React de muestra integrada, para que pueda ver lo fácil que es para cualquiera administrar contenidos de forma independiente sin dedicar tiempo al desarrollo.<br><br>Inicie este módulo en una nueva pestaña haciendo clic abajo y, a continuación, siga esta guía."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_react_app_guide_footer"
>title="En este módulo, ha aprendido a personalizar una aplicación React de muestra.<br><br>Tiempo de salida al mercado: ¡acelerado!<br>Ciclos de desarrollo: ¡reducidos!<br><br>Ahora comprende lo fácil que es administrar contenido sin encabezado para sitios web y aplicaciones que cuentan con funcionalidades de AEM sin encabezado."
>abstract=""

## Vista previa de la aplicación {#preview}

Empiece en el editor de fragmentos de contenido con la aplicación de muestra que se proporciona con la versión de prueba de AEM sin encabezado ya cargada. La aplicación de muestra cuenta con la tecnología de fragmentos de contenido que se entrega mediante GraphQL. Utilice el editor de fragmentos de contenido para familiarizarse con el editor previsualizando la aplicación de muestra.

1. Haga clic o pulse en el botón **Vista previa** en la parte superior derecha de la pantalla del editor.

1. La aplicación de muestra se abre en una nueva pestaña. La aplicación es para la marca ficticia de estilo de vida al aire libre WKND. Muévase hacia abajo por la página para desplazarse por el contenido de ejemplo.

1. Vuelva a la pestaña del explorador del editor de fragmentos de contenido para continuar.

![Vista previa de la aplicación](assets/do-not-localize/preview-app-1.png)

## Edición de un encabezado en la aplicación {#edit-app}

El editor de fragmentos de contenido muestra el diseño básico de la aplicación como un fragmento de contenido de página. Los **Paneles** representan diferentes páginas de la aplicación, cada una de las cuales es su propio fragmento de contenido. Al modificar estos fragmentos, puede cambiar el contenido de la aplicación.

1. Haga clic o pulse en **Ciclista de montaña en el Cañón** en la sección **Paneles**.

   ![Selección del panel de texto](assets/do-not-localize/edit-header-1.png)

1. El editor abre el panel de encabezado de la aplicación para el ciclista de montaña. Cada panel está formado por capas que representan diferentes imágenes y texto que componen la experiencia.

1. Seleccione la capa de texto **Capa de texto Ciclista de montaña en el Cañón** para abrir el detalle de la capa en el editor. La capa está formada por varios fragmentos de contenido que controlan el texto que se muestra en este panel de la aplicación.

1. Seleccione el elemento de texto **Título Ciclista de montaña en el Cañón**. Se abre el editor de fragmentos de contenido que muestra el contenido de este fragmento y le permite modificarlo.

1. Cambie el texto de `Your next great adventure is calling` a `Choose your own adventure`. El editor guarda automáticamente el cambio.

1. Haga clic o pulse en **Vista previa** en la parte superior derecha de la ventana para ver los cambios. La vista previa de la aplicación de demostración se abre en una nueva pestaña.

   ![Vista previa de la aplicación de demostración](assets/do-not-localize/edit-header-5-6.png)

Así de fácil es actualizar contenido dentro de una aplicación React cuando se integra en el CMS de AEM sin encabezado.

## Intercambio de una imagen en la aplicación {#change-image}

Ahora que ha modificado un titular en la aplicación, intente cambiar una imagen.

1. Vuelva a la pestaña del explorador del editor de fragmentos de contenido desde la vista previa.

1. Debe volver al lugar correcto en el editor de fragmentos de contenido. Las rutas de exploración en la parte superior izquierda del editor muestran dónde se encuentra en la jerarquía de contenido. Seleccione **Ciclista de montaña en el Cañón** en las rutas de exploración para volver a esa página.

   ![Rutas de exploración](assets/do-not-localize/swap-image-2.png)

1. Seleccione la capa de imagen **Ciclista de montaña: Ciclista**. Se abre el editor de fragmentos de contenido

1. Seleccione la **X** para eliminar la imagen del ciclista. La imagen desaparece y el editor muestra un error, ya que la imagen son datos requeridos para este modelo de fragmento de contenido.

   ![Quitar imagen del fragmento](assets/do-not-localize/swap-image-4.png)

1. Seleccione **Añadir recurso** y luego **Examinar recursos** en el menú emergente.

1. Se abre el cuadro de diálogo **Seleccionar recurso** y la ruta **sample-wknd-app** > **en** > **image-files** se selecciona automáticamente.

1. Seleccione la imagen `biker-yellow.png` y luego haga clic en **Seleccionar**.

1. La imagen del ciclista se reemplaza por la seleccionada. El editor guarda automáticamente los cambios.

1. Haga clic o pulse en **Vista previa** en la parte superior derecha de la ventana para ver los cambios. La vista previa de la aplicación de demostración se abre en una nueva pestaña. Haga clic en actualizar en el explorador y debería ver la nueva imagen del ciclista con pantalones cortos amarillos en la aplicación.

Es muy fácil actualizar imágenes y recursos en sus aplicaciones con el CMS de AEM sin encabezado.

## Adición de una referencia a un nuevo fragmento de contenido en la aplicación {#create-moment}

Ahora que ha actualizado la imagen del ciclista, vamos a ver cómo añadir contenido a una aplicación creando y haciendo referencia a un nuevo fragmento de contenido. Añada una llamada de producto administrada por un fragmento de contenido de “momento de ventas” al segundo panel de la aplicación.

![Ejemplo de un momento de ventas](assets/do-not-localize/example-shoppable-moment.png)

1. Vuelva a la pestaña del explorador del editor de fragmentos de contenido desde la pestaña de vista previa.

1. Debe volver al lugar correcto en el editor de fragmentos de contenido. Las rutas de exploración en la parte superior izquierda del editor muestran dónde se encuentra en la jerarquía de contenido. Haga clic o pulse en **Inicio de WKND** en las rutas de exploración para volver a esa página.

1. Seleccione el panel **Ciclista de montaña en WKND amarillo**.

1. Seleccione la capa **Ciclista de montaña: ventas**.

1. Para crear una nueva llamada en este panel, debe crear un nuevo fragmento de contenido en el momento de ventas. Seleccione el botón **+ Crear nuevo fragmento**.

   ![Adición de un momento de ventas](assets/do-not-localize/add-reference-1-5.png)

1. Primero debe elegir un modelo en el que basar el nuevo fragmento de contenido. Seleccione el modelo **Elemento de momento de ventas** de la lista desplegable **Modelo de fragmento de contenido**.

1. Asigne un nombre al fragmento de contenido. Por ejemplo, introduzca `Shorts` en el campo **Nombre**.

1. Seleccione **Crear y abrir**.

   ![Asigne un nombre al momento de ventas](assets/do-not-localize/add-reference-6-7-8.png)

1. El editor se abre para el nuevo fragmento de contenido.

1. Póngale un nombre al momento de ventas en el campo **Texto**, como `Yellow shorts`.

1. Defina valores para **X** e **Y**. Aquí es donde esta llamada debe superponerse en el panel. El editor guarda automáticamente los cambios en el fragmento

   * **X**: `-5`
   * **Y**: `-10`

1. Haga clic en **Vista previa** en la parte superior derecha de la ventana para ver los cambios. La vista previa de la aplicación de demostración se abre en una nueva pestaña. Haga clic en actualizar en el explorador para probar la posición y realizar los ajustes necesarios en el editor.

   ![Vista previa](assets/do-not-localize/add-reference-10-11-12.png)

Ahora ya sabe cómo crear contenido nuevo y hacer referencia a él como Fragmento de contenido en la aplicación sin necesidad de realizar ningún ciclo de desarrollo.
