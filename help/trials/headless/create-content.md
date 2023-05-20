---
title: Creación de contenido sin encabezado
description: Utilice el modelo de fragmento de contenido que ha creado anteriormente para elaborar contenido que pueda utilizarse en la confección de páginas o como base para su contenido sin encabezado.
hidefromtoc: true
index: false
exl-id: d74cf5fb-4c4a-4363-a500-6e2ef6811e60
source-git-commit: ac94981e477e1fe8b883460ed9be009b4c1c088d
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 65%

---


# Creación de contenido sin encabezado {#create-content}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_create_content"
>title="Crear contenido nuevo"
>abstract="A partir del modelo que creó en el módulo anterior, aprenderá a generar contenido que podrá utilizar para la confección de páginas o como base de su contenido sin encabezado."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_create_content_guide"
>title="Lanzamiento de la consola de fragmentos de contenido"
>abstract="La creación de contenido coherente y de alta calidad que funcione sin problemas en todas las aplicaciones y sitios web lleva a buenas experiencias de cliente. Este módulo le guía a través de la creación de su primer fragmento de contenido para ilustrar cómo hacerlo realidad.<br><br>Inicie este módulo en una nueva pestaña haciendo clic en el botón de abajo y, a continuación, siga esta guía."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_create_content_guide_footer"
>title="¡Buen trabajo! En este módulo, ha aprendido a elaborar un fragmento de contenido basado en el modelo que ha creado anteriormente. Ahora comprende cómo los equipos de contenido pueden crear y administrar contenido para aplicaciones y sitios web independientes de los ciclos de desarrollo."
>abstract=""

## Creación de un fragmento de contenido {#create-fragment}

Los fragmentos de contenido representan su contenido sin encabezado y se basan en estructuras predefinidas, denominadas modelos de fragmento de contenido. Ya ha creado un modelo en un módulo anterior.

En este módulo creará un nuevo fragmento de contenido basado en ese modelo mediante la consola Fragmento de contenido. Considere la consola fragmento de contenido como una biblioteca de contenido sin encabezado. Utilícela para crear nuevos fragmentos de contenido y administrar los existentes.

1. Toque o haga clic en el botón **Crear** en la parte superior derecha de la consola.

1. Se abre el cuadro de diálogo **Nuevo fragmento de contenido**, en el que puede empezar a crearlo. **Ubicación** se rellena automáticamente con el lugar donde se guardará el nuevo contenido.

1. En el **Modelo de fragmento de contenido** , seleccione la opción **Aventura** Modelo de fragmento de contenido que creó anteriormente.

1. Añadir `Tuscany` como elemento descriptivo **Título** para el fragmento de contenido. Esto sirve para identificar el fragmento en la consola.

1. Toque o haga clic en **Crear y abrir**.

![Creación de un nuevo fragmento de contenido](assets/do-not-localize/create-content.png)

>[!TIP]
>
>Según la configuración del explorador, la nueva pestaña podría suprimirse mediante un bloqueador de ventanas emergentes. Si el nuevo fragmento no se abre después de hacer clic en **Crear y abrir**, compruebe la configuración de su explorador.

## Añadir contenido al fragmento de contenido {#add-content}

Una vez guardado y abierto el nuevo fragmento de contenido, el editor de fragmentos de contenido se abre en una nueva pestaña. Aquí puede añadir el contenido del nuevo fragmento.

1. El editor de fragmentos de contenido muestra los campos definidos en el modelo seleccionado. Aquí puede añadir contenido a cada campo para completar el fragmento de contenido. El progreso se guarda automáticamente.

1. Proporcione un **Título** para el fragmento introduciendo `Tuscan Adventure`.

1. Proporcione un **Descripción** para el fragmento, pegue el siguiente texto.

   ```text
   Visiting Tuscany on a bicycle is about experiencing the old world charm of Italy on your own terms. Your efforts on the climbs of Italy's rolling hills during this tour will be rewarded with sunny Mediterranean landscapes and unmatched Italian hospitality.  Tuscany’s natural wonders have always been a well of inspiration for arts and culture. Find out why as you explore the Italian countryside and coastline on bicycle.
   ```

1. Proporcione un **Precio** para el fragmento introduciendo `$700`.

1. Proporcione un **Imagen** que es representativo del viaje tocando o haciendo clic en **Añadir recurso** en el **Imagen** field.

1. En la ventana emergente del recurso, toque o haga clic en **Examinar recursos** para seleccionar entre un recurso existente en la biblioteca de recursos.

   ![Añadir recurso](assets/do-not-localize/add-asset.png)

1. El **Seleccionar recurso** se abre. Con el navegador de árbol del panel izquierdo, navegue hasta **Todos los recursos** > **aem-demo-assets** > **en** > **aventuras** > **ciclismo-toscana**.

1. El contenido del **ciclismo-toscana** Las carpetas se muestran a la derecha. Seleccionar la imagen `ADOBESTOCK_141786166.JPEG`.

1. Haga clic o pulse **Seleccionar**.

   ![Seleccionar recurso](assets/do-not-localize/select-asset.png)

1. La imagen seleccionada se muestra en el fragmento de contenido. El editor guarda automáticamente los cambios.

1. Una vez que haya terminado de añadir contenido, toque o haga clic en el botón **Publicar** en la parte superior derecha del editor. Esto hace que el fragmento de contenido esté disponible para su consumo en aplicaciones externas. A continuación seleccione **Ahora** de la lista desplegable. También puede programarlo para publicarlo más adelante.

   ![Publicar contenido](assets/do-not-localize/publish.png)

1. Aparece el cuadro de diálogo **Publicar fragmentos de contenido**. AEM realiza automáticamente una comprobación de referencia para asegurarse de que se publican todos los recursos necesarios para el fragmento de contenido. En este caso, también deberá publicar el modelo que ha creado. Haga clic o pulse **Publicar**.

   ![Publicación y comprobación de referencia](assets/do-not-localize/publish-confirm.png)

1. La publicación se confirma en un titular.

El contenido se publica y está listo para enviarse a su aplicación o sitio web como fragmento de contenido.
