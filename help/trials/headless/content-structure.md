---
title: Creación de la estructura de contenidos de la aplicación
description: Aprenda a crear la estructura que sirve como base para todo el contenido sin encabezado mediante los modelos de fragmento de contenido de AEM.
hidefromtoc: true
index: false
exl-id: ace9b9f3-8bc6-4a36-a51c-ff60cdd339ce
source-git-commit: 741fadcffc496cb1c32d1943f7759e8d70cf92ff
workflow-type: ht
source-wordcount: '477'
ht-degree: 100%

---


# Creación de la estructura de contenidos de la aplicación {#content-structure}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview"
>title="Cree la estructura de contenido para la aplicación"
>abstract="A medida que siga esta serie de guías interactivas aprenderá a crear la estructura (conocida como el modelo de fragmentos de contenido) que sirve como base para su contenido sin encabezado."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide"
>title="Lanzamiento de la consola del modelo"
>abstract="Vamos a explorar cómo crear un esquema reutilizable, llamado modelo de fragmento de contenido, para su contenido en Adobe Experience Manager as a Cloud Service. Vea el vídeo para comprender por qué este es un paso importante. <br><br>Inicie este módulo en una nueva pestaña haciendo clic en el botón de abajo y siga esta guía."
>additional-url="https://video.tv.adobe.com/v/3413261/?captions=spa" text="Vídeo de introducción a la estructura de contenido"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide_footer"
>title="¡Enhorabuena! Ha aprendido a crear un modelo de fragmento de contenido para representar la estructura de sus datos sin encabezado y ha dado el primer paso para ofrecer contenido omnicanal de forma escalada y estándar."
>abstract=""

## Creación de un modelo {#create-model}

La consola de modelos de fragmentos de contenido se abre en una nueva pestaña. Considere la consola del modelo de fragmento de contenido como su biblioteca de modelos, donde crea nuevos y administra los existentes.

1. Haga clic en el botón **Crear** en la parte superior derecha de la pantalla para comenzar a generar un modelo de fragmento de contenido.

1. Se inicia el asistente Crear modelo, que le guía. Proporcione la información obligatoria.

   * **Título del modelo**: esta es una breve descripción del modelo y normalmente indica el propósito del modelo.
   * **Habilitar modelo**: esta opción está marcada de forma predeterminada y debe estar activada para poder crear fragmentos de contenido basados en este modelo.

1. Una vez rellenados los campos obligatorios, haga clic en **Crear** en la parte superior izquierda para crear el modelo.

1. El cuadro de diálogo **Correcto** confirma que se ha generado el modelo. Haga clic en **Abrir** en el cuadro de diálogo para abrir el nuevo modelo de fragmento de contenido en el editor en una nueva pestaña. Después, continúe con el siguiente paso para añadir campos de datos al modelo.

![Pasos dos y tres de la creación de un modelo de fragmento de contenido](assets/do-not-localize/create-model-2-3.png)

## Adición de campos al modelo {#configure-model}

Para poder utilizar el modelo, debe definir la estructura de sus datos. El editor del modelo de fragmento de contenido es donde se configuran los tipos de datos y las propiedades que definen el contenido del modelo.

1. Arrastre un campo desde el panel **Tipos de datos** a la derecha del editor y suéltelo en el modelo de fragmento de contenido.

1. Una vez colocado el tipo de datos, la columna **Tipos de datos** se ha cambiado automáticamente a la pestaña **Propiedades**, donde puede definir los detalles del tipo de datos que acaba de situar.

1. Una vez añadidos todos los campos necesarios para el modelo de fragmento de contenido, haga clic en **Guardar** en la parte superior derecha de la ventana.

1. El modelo se guarda y se vuelve a la consola del modelo de fragmento de contenido.

![Pasos uno, dos y tres para añadir campos al modelo](assets/do-not-localize/define-model-fields-1-2-3.png)
