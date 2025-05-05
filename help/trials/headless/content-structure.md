---
title: Cree la estructura de contenido para la aplicación
description: Aprenda a utilizar modelos de fragmentos de contenido de AEM para crear su estructura de contenido, que sirve como base para su contenido sin encabezado.
hidefromtoc: true
index: false
exl-id: ace9b9f3-8bc6-4a36-a51c-ff60cdd339ce
feature: Headless
role: Admin, User, Developer
source-git-commit: c9cddf9f0e344a2a24ee1a608b3ea920e258f34a
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Cree la estructura de contenido para la aplicación {#content-structure}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview"
>title="Cree la estructura de contenido para la aplicación"
>abstract="A medida que siga esta serie de guías interactivas aprenderá a crear una estructura (conocida como el modelo de fragmento de contenido) que sirve como estructura base para su contenido sin encabezado."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide"
>title="Iniciar la consola del modelo"
>abstract="Vamos a explorar cómo crear un esquema reutilizable, llamado modelo de fragmento de contenido, para su contenido en Adobe Experience Manager as a Cloud Service. Vea el vídeo para entender por qué es importante este paso. <br><br>En este módulo de aprendizaje, utilizaremos un sitio de viajes como ejemplo y veremos cómo crear un modelo que represente un viaje.<br><br>Inicie este módulo en una nueva pestaña haciendo clic en el botón de abajo y siga esta guía."
>additional-url="https://video.tv.adobe.com/v/3436543/?captions=spa" text="Vídeo de introducción a la estructura de contenido"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide_footer"
>title="¡Enhorabuena! Ha aprendido a crear un modelo de fragmento de contenido para representar la estructura de sus datos sin encabezado y ha dado el primer paso para ofrecer contenido omnicanal de forma escalada y estándar."
>abstract=""

## Creación de un modelo {#create-model}

La consola de modelos de fragmentos de contenido se abre en una nueva pestaña. Considere la consola del modelo de fragmento de contenido como su biblioteca de modelos, donde crea nuevos y administra los existentes.

Para nuestro ejemplo, crearemos un modelo que represente la estructura de datos de un viaje que aparece en un sitio web de viajes. Un viaje que utilice este modelo se denomina **Aventura**.

1. En la esquina superior derecha de la pantalla, haga clic en **Crear** para empezar a crear un modelo de fragmento de contenido.

1. Se inicia el asistente Crear modelo, que le guiará a través de la creación del modelo. Proporcione la información obligatoria.

   * **Título del modelo**: esta es una breve descripción del modelo y normalmente indica el propósito del modelo. Puede llamar `Adventure` al nuevo modelo.
   * **Habilitar modelo**: esta opción está marcada de forma predeterminada y debe estar activada para poder crear fragmentos de contenido basados en este modelo.

1. Una vez rellenados los campos obligatorios, haga clic en **Crear** en la parte superior izquierda para crear el modelo.

1. El cuadro de diálogo **Correcto** confirma que se ha generado el modelo. Haga clic en **Abrir** en el cuadro de diálogo para abrir el nuevo modelo de fragmento de contenido en el editor en una nueva pestaña. Después, continúe con el siguiente paso para añadir campos de datos al modelo.

![Pasos dos y tres de la creación de un modelo de fragmento de contenido](assets/do-not-localize/create-model.png)

## Uso del editor de modelos {#configure-model}

Ahora tenemos un modelo llamado **Aventura**, pero no tiene detalles como duración, destino, actividades. Para poder utilizar el modelo, debe definir la estructura de sus datos.

El editor del modelo de fragmento de contenido es donde se configuran los tipos de datos y las propiedades que definen el contenido del modelo.

>[!TIP]
>
>Es importante seguir los esquemas de nomenclatura de las siguientes instrucciones, ya que se hace referencia a estos nombres específicos en módulos posteriores.

1. Arrastre un campo de **Texto de una sola línea** desde el panel **Tipos de datos** a la derecha del editor y suéltelo en el modelo de fragmento de contenido.

1. Una vez colocado el tipo de datos, la columna **Tipos de datos** se ha cambiado automáticamente a la pestaña **Propiedades**, donde puede definir los detalles del tipo de datos que acaba de situar. Para este primer campo, queremos almacenar el título del viaje o aventura. Especifique las siguientes propiedades.

   * **Procesar como:** **Campo de texto**. Cuando se crea una aventura, este campo almacena el título de la aventura.
   * **Etiqueta de campo:** `Title` esta es la etiqueta que se muestra para este campo al crear una nueva aventura.

1. Una vez definidas las propiedades del campo, puede volver a la pestaña **Tipos de datos** en el panel derecho y añadir campos adicionales arrastrando y soltando.

De este modo, puede añadir tantos campos como sea necesario al modelo para admitir el tipo de estructura de datos que necesite. Los tipos de campos de datos varían, pero el proceso de añadirlos al modelo sigue siendo el mismo.

Continúe en la siguiente sección para añadir los campos necesarios para completar y guardar el modelo **Aventura**

![Pasos uno, dos y tres para añadir campos al modelo](assets/do-not-localize/define-model-fields.png)

## Adición de campos al modelo {#additional-fields}

Ya tiene un campo para el título de la aventura. Ahora debe añadir campos para capturar la descripción, el precio y una imagen representativa de la aventura.

>[!TIP]
>
>El modelo **Aventura** se basa en el sitio de muestra de WKND para AEM. Puede [visitar el sitio WKND aquí](https://wknd.site/us/en/adventures/yosemite-backpacking.html) para ver el contenido que utiliza el modelo **Aventura**.

Siga los mismos pasos que se describen arriba para añadir estos campos adicionales. La única diferencia son las propiedades que debe establecer.

1. Añada un campo para almacenar la descripción de la aventura arrastrando y soltando un campo de **Texto de varias líneas** e introduzca las siguientes propiedades:

   * **Procesar como:** **Área de texto**. Cuando crea una aventura, este campo almacena una breve descripción del viaje.
   * **Etiqueta de campo:** `Description` esta es la etiqueta que se muestra para este campo al crear una nueva aventura.
   * **Tipo predeterminado**: **Texto sin formato**. El formato requerido para este ejemplo.

1. Añada un campo para almacenar el precio de la aventura arrastrando y soltando un campo de **Texto de una sola línea** e introduzca las siguientes propiedades:

   * **Procesar como:** **Campo de texto**. Cuando cree una aventura, este campo almacenará el precio del viaje.
   * **Etiqueta de campo:** `Price`. Esta es la etiqueta que se muestra para este campo al crear una nueva aventura.

1. Añada un campo para almacenar una imagen que represente el viaje. Las imágenes de AEM se almacenan como otro tipo de contenido denominado **Recursos**. Para crear un campo para ellos, debe arrastrar y soltar un campo de **Referencia de contenido** que haga referencia al recurso de la imagen.

   * **Procesar como:** **Referencia de contenido**. Cuando cree una aventura, este campo señalará al recurso de imagen que represente este viaje.
   * **Etiqueta de campo:** `Image` esta es la etiqueta que se muestra para este campo al crear una nueva aventura.
   * **Ruta raíz:** `/content/dam/aem-demo-assets/en`: especifica una ruta de punto de partida al buscar recursos con el Selector de recursos.

1. Después de añadir los campos necesarios para el modelo de fragmento de contenido, en la parte superior derecha de la ventana, haga clic en **Guardar**.

1. El modelo se guarda y se vuelve a la consola del modelo de fragmento de contenido.
