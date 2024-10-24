---
title: Crear contenido sin encabezado
description: Utilice el modelo de fragmento de contenido que ha creado anteriormente para elaborar contenido que pueda utilizarse en la confección de páginas o como base para su contenido sin encabezado.
hidefromtoc: true
index: false
exl-id: d74cf5fb-4c4a-4363-a500-6e2ef6811e60
feature: Headless
role: Admin, User, Developer
source-git-commit: f66ea281e6abc373e9704e14c97b77d82c55323b
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 100%

---


# Crear contenido sin encabezado {#create-content}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_create_content"
>title="Crear contenido sin encabezado"
>abstract="A partir del modelo creado en el módulo anterior, aprenderá a crear contenido que puede utilizar para la confección de páginas o como base de su contenido sin encabezado."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_create_content_guide"
>title="Iniciar la consola de fragmentos de contenido"
>abstract="La creación de contenido coherente y de alta calidad que funcione sin problemas en todas las aplicaciones y sitios web lleva a buenas experiencias de cliente. Este módulo le guía a través de la creación de su primer contenido sin encabezado mediante la consola Fragmento de contenido.<br><br>Inicie este módulo en una nueva pestaña haciendo clic en el botón de abajo y, a continuación, siga esta guía."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_create_content_guide_footer"
>title="¡Buen trabajo! En este módulo, ha aprendido a elaborar un fragmento de contenido basado en el modelo que ha creado anteriormente. Ahora comprende cómo los equipos de contenido pueden crear y administrar contenido para aplicaciones y sitios web independientes de los ciclos de desarrollo."
>abstract=""

## Creación de un fragmento de contenido {#create-fragment}

Los fragmentos de contenido representan su contenido sin encabezado y se basan en estructuras predefinidas, denominadas modelos de fragmento de contenido. Ya ha creado un modelo en un módulo anterior.

En este módulo creará un nuevo fragmento de contenido basado en ese modelo mediante la consola de fragmentos de contenido. Considere la consola fragmento de contenido como una biblioteca de contenido sin encabezado. Utilícela para crear nuevos fragmentos de contenido y administrar los existentes.

La consola Fragmento de contenido se utiliza para crear y editar contenido sin encabezado en todos los canales de envío e independientemente del contexto, que puede ser el método más eficaz en muchos casos de creación. En un módulo posterior, exploraremos la edición de contenido sin encabezado en contexto e in situ.

1. Seleccione **Crear** en la parte superior derecha de la consola.

1. Se abre el cuadro de diálogo **Nuevo fragmento de contenido**, en el que puede empezar a crearlo. **Ubicación** se rellena automáticamente con el lugar donde se guarda el nuevo contenido.

1. En el desplegable **modelo de Fragmento de contenido**, seleccione el modelo de Fragmento de contenido **Aventura** que creó anteriormente.

1. Añada `Tuscany` como **Título** descriptivo para el Fragmento de contenido. Esto es para identificar el fragmento en la consola.

1. Seleccione **Crear y abrir**.

![Creación de un nuevo fragmento de contenido](assets/do-not-localize/create-content.png)

>[!TIP]
>
>Según la configuración del explorador, la nueva pestaña del explorador puede ser suprimida por un bloqueador de ventanas emergentes. Si el nuevo fragmento no se abre después de hacer clic en **Crear y abrir**, compruebe la configuración del explorador.

## Adición de contenido a su Fragmento de contenido {#add-content}

Una vez guardado y abierto el nuevo fragmento de contenido, el editor de fragmentos de contenido se abre en una nueva pestaña. Aquí puede añadir el contenido del nuevo fragmento.

1. El editor de fragmentos de contenido muestra los campos definidos en el modelo seleccionado. Aquí puede añadir contenido a cada campo para completar el fragmento de contenido. El progreso se guarda automáticamente.

1. Proporcione un **Título** para el fragmento introduciendo `Tuscan Adventure`.

1. Proporcione una **Descripción** para el fragmento pegando el siguiente texto.

   ```text
   Visiting Tuscany on a bicycle is about experiencing the old world charm of Italy on your own terms. Your efforts on the climbs of Italy's rolling hills during this tour are rewarded with sunny Mediterranean landscapes and unmatched Italian hospitality. Tuscany's natural wonders have always been a well of inspiration for arts and culture. Find out why as you explore the Italian countryside and coastline on bicycle.
   ```

1. Proporcione un **Precio** para el fragmento introduciendo `$700`.

1. Proporcione una **Imagen** que sea representativa del viaje pulsando o haciendo clic en **Añadir recurso** en el campo de **Imagen**.

1. En la ventana emergente del recurso, seleccione **Examinar recursos** para seleccionar un recurso existente en la biblioteca de recursos.

   ![Añadir recurso](assets/do-not-localize/add-asset.png)

1. Se abre el cuadro de diálogo de **Seleccionar recurso**. Con el navegador de árbol en el panel izquierdo, vaya a **Todos los recursos** > **aem-demo-assets** > **en** > **aventuras** > **ciclismo-toscana**.

1. El contenido de la carpeta **ciclismo-toscana** se muestra a la derecha. Seleccionar la imagen `ADOBESTOCK_141786166.JPEG`.

1. Seleccione **Seleccionar**.

   ![Seleccionar recurso](assets/do-not-localize/select-asset.png)

1. La imagen seleccionada se muestra en el fragmento de contenido. El editor guarda automáticamente los cambios.

1. Una vez que haya terminado de añadir contenido, seleccione **Publicar** en la parte superior derecha del editor. Esto hace que el fragmento de contenido esté disponible para su consumo en aplicaciones externas. Después, selecciona **Ahora** de la lista desplegable. También puede programarlo para publicarlo más adelante.

   ![Publicar contenido](assets/do-not-localize/publish.png)

1. Aparece el cuadro de diálogo **Publicar fragmentos de contenido**. AEM realiza automáticamente una comprobación de referencia para asegurarse de que se publican todos los recursos necesarios para el fragmento de contenido. En este caso, también deberá publicar el modelo que ha creado. Seleccione **Publicar**.

   ![Publicación y comprobación de referencia](assets/do-not-localize/publish-confirm.png)

1. La publicación se confirma en un titular.

El contenido se publica y está listo para enviarse a su aplicación o sitio web como fragmento de contenido.
