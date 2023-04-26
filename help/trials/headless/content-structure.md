---
title: Creación de la estructura de contenidos de la aplicación
description: Aprenda a utilizar AEM modelos de fragmento de contenido para crear su estructura de contenido, que sirve como base para su contenido sin encabezado.
hidefromtoc: true
index: false
exl-id: ace9b9f3-8bc6-4a36-a51c-ff60cdd339ce
source-git-commit: 7134951a588eae3ee0c7c11abea17a34eac21474
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 37%

---


# Creación de la estructura de contenidos de la aplicación {#content-structure}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview"
>title="Cree la estructura de contenido para la aplicación"
>abstract="A medida que sigue esta serie de guías interactivas, aprenderá a crear una estructura (conocida como el modelo de fragmento de contenido) que sirva como estructura base para el contenido sin encabezado."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide"
>title="Lanzamiento de la consola del modelo"
>abstract="Vamos a explorar cómo crear un esquema reutilizable, llamado modelo de fragmento de contenido, para su contenido en Adobe Experience Manager as a Cloud Service. Vea el vídeo para comprender por qué este es un paso importante. <br><br>En este módulo de aprendizaje utilizaremos un sitio de viajes como ejemplo y veremos cómo crear un modelo que represente un viaje. Nos referiremos a este modelo en módulos posteriores, por lo que asegúrese de seguir el esquema de nomenclatura indicado.<br><br>Inicie este módulo en una nueva pestaña haciendo clic en el botón de abajo y siga esta guía."
>additional-url="https://video.tv.adobe.com/v/3413261/?captions=spa" text="Vídeo de introducción a la estructura de contenido"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide_footer"
>title="¡Enhorabuena! Ha aprendido a crear un modelo de fragmento de contenido para representar la estructura de sus datos sin encabezado y ha dado el primer paso para ofrecer contenido omnicanal de forma escalada y estándar."
>abstract=""

## Creación de un modelo {#create-model}

La consola de modelos de fragmentos de contenido se abre en una nueva pestaña. Considere la consola del modelo de fragmento de contenido como su biblioteca de modelos, donde crea nuevos y administra los existentes.

Para nuestro ejemplo, crearemos un modelo que represente la estructura de datos de un viaje que aparece en un sitio web de viajes. Nos referiremos a un viaje en este modelo como un **Aventura.**

1. Haga clic en el botón **Crear** en la parte superior derecha de la pantalla para comenzar a generar un modelo de fragmento de contenido.

1. Se inicia el asistente Crear modelo , que le guiará a través de la creación del modelo. Proporcione la información obligatoria.

   * **Título del modelo**: esta es una breve descripción del modelo y normalmente indica el propósito del modelo. Llamaremos a nuestro nuevo modelo `Adventure`.
   * **Habilitar modelo**: esta opción está marcada de forma predeterminada y debe estar activada para poder crear fragmentos de contenido basados en este modelo.

1. Una vez rellenados los campos obligatorios, haga clic en **Crear** en la parte superior izquierda para crear el modelo.

1. El cuadro de diálogo **Correcto** confirma que se ha generado el modelo. Haga clic en **Abrir** en el cuadro de diálogo para abrir el nuevo modelo de fragmento de contenido en el editor en una nueva pestaña. Después, continúe con el siguiente paso para añadir campos de datos al modelo.

![Pasos dos y tres de la creación de un modelo de fragmento de contenido](assets/do-not-localize/create-model.png)

## Uso del Editor de modelos {#configure-model}

Ahora tenemos un modelo llamado **Aventura** para representar viajes en un sitio web de viajes, pero no tiene detalles como duración, destino, actividades, etc. Para poder utilizar el modelo, debe definir la estructura de sus datos.

El editor del modelo de fragmento de contenido es donde se configuran los tipos de datos y las propiedades que definen el contenido del modelo.

>[!TIP]
>
>Añadiremos algunos campos importantes para la variable **Aventura**. En módulos posteriores usaremos y agregaremos al modelo, por lo que siga el esquema de nomenclatura tal y como se proporciona.

1. Arrastre un **Texto de una sola línea** del campo **Tipos de datos** a la derecha del editor y suéltelo en el modelo de fragmento de contenido.

1. Una vez colocado el tipo de datos, la columna **Tipos de datos** se ha cambiado automáticamente a la pestaña **Propiedades**, donde puede definir los detalles del tipo de datos que acaba de situar. Para este primer campo, queremos almacenar el título del viaje o aventura. Introduzca las siguientes propiedades.

   * **Procesar como:** **Campo de texto** - Cuando se crea una aventura, este campo almacena el título de la aventura.
   * **Etiqueta de campo:** `Title` - Esta es la etiqueta que se muestra para este campo al crear una nueva aventura.

1. Una vez definidas las propiedades del campo, puede volver a la función **Tipos de datos** en el panel derecho y añada campos adicionales arrastrando y soltando.

De este modo, puede agregar tantos campos como sea necesario al modelo para admitir el tipo de estructura de datos que necesite. Los tipos de campos de datos varían, pero el proceso de agregarlos al modelo sigue siendo el mismo.

Continúe en la siguiente sección para añadir los campos necesarios para completar y guardar el **Aventura** model

![Pasos uno, dos y tres para añadir campos al modelo](assets/do-not-localize/define-model-fields.png)

## Adición de campos al modelo {#additional-fields}

Ya tienes un campo para el título de la aventura. Ahora debe añadir campos para capturar la descripción, el precio y una imagen representativa del viaje.

>[!TIP]
>
>La variable **Aventura** se basa en el sitio de muestra de WKND para AEM. Puede [visite el sitio aquí](https://wknd.site/us/en/adventures/yosemite-backpacking.html) para obtener más información sobre él si lo desea, pero no es necesario que estos módulos de aprendizaje lo conozcan.

Siga los mismos pasos que se describen arriba para agregar estos campos adicionales. La única diferencia son las propiedades que debe establecer.

1. Añada un campo para almacenar la descripción de la aventura arrastrando y soltando una **Texto de varias líneas** e introduzca las siguientes propiedades:

   * **Procesar como:** **Área de texto** - Cuando crea una aventura, este campo almacena una breve descripción del viaje.
   * **Etiqueta de campo:** `Description` - Esta es la etiqueta que se muestra para este campo al crear una nueva aventura.

1. Añada un campo para almacenar el precio de la aventura arrastrando y soltando una **Texto de una sola línea** e introduzca las siguientes propiedades:

   * **Procesar como:** **Campo de texto** - Cuando crea una aventura, este campo almacenará el precio del viaje.
   * **Etiqueta de campo:** `Price` - Esta es la etiqueta que se muestra para este campo al crear una nueva aventura.

1. Agregue un campo para almacenar una imagen que represente el viaje. Las imágenes de AEM se almacenan como otro tipo de contenido denominado **Recursos**. Para crear un campo para ellos, debe arrastrar y soltar un **Referencia de contenido** campo que hace referencia al recurso de la imagen.

   * **Procesar como:** **Referencia de contenido** - Cuando cree una aventura, este campo señalará al recurso de imagen que representa este viaje.
   * **Etiqueta de campo:** `Image` - Esta es la etiqueta que se muestra para este campo al crear una nueva aventura.

1. Una vez añadidos todos los campos necesarios para el modelo de fragmento de contenido, haga clic en **Guardar** en la parte superior derecha de la ventana.

1. El modelo se guarda y se vuelve a la consola del modelo de fragmento de contenido.
