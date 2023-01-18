---
title: Crear la estructura de contenido para la aplicación
description: Aprenda a crear la estructura que sirve como base para todo el contenido sin encabezado mediante AEM modelos de fragmento de contenido.
hidefromtoc: true
index: false
exl-id: ace9b9f3-8bc6-4a36-a51c-ff60cdd339ce
source-git-commit: bcab02cbd84955ecdc239d4166ae38e5f79b3264
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# Crear la estructura de contenido para la aplicación {#content-structure}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview"
>title="Cree la estructura de contenido para la aplicación"
>abstract="A medida que sigue esta serie de guías interactivas, aprenderá a crear una estructura (conocida como el modelo de fragmento de contenido) que sirva de base para su contenido sin encabezado."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide"
>title="Iniciar la consola del modelo"
>abstract="Vamos a explorar cómo crear un esquema reutilizable, llamado modelo de fragmento de contenido, para su contenido en Adobe Experience Manager as a Cloud Service. Vea el vídeo para comprender por qué este es un paso importante. <br><br>Inicie este módulo en una nueva pestaña haciendo clic en el botón de abajo y siga esta guía."
>additional-url="https://video.tv.adobe.com/v/3413261" text="Vídeo introductorio de la estructura de contenido"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide_footer"
>title="¡Enhorabuena! Ha aprendido a crear un modelo de fragmento de contenido para representar la estructura de sus datos sin encabezado y ha dado el primer paso para ofrecer contenido omnicanal de forma escalada y estándar."
>abstract=""

## Crear un modelo {#create-model}

Al hacer clic en **Iniciar la consola del modelo** arriba abre la consola de modelos de fragmento de contenido en una nueva pestaña.

![La consola del modelo de fragmento de contenido](assets/content-structure/content-fragment-model-console.png)

Considere la consola del modelo de fragmento de contenido como su biblioteca de modelos, donde crea nuevos modelos y gestiona los modelos existentes. La consola empieza vacía, así que vamos a crear un nuevo modelo.

1. En la consola del modelo de fragmento de contenido, haga clic en el botón **Crear** en la parte superior derecha de la pantalla para comenzar a crear un modelo de fragmento de contenido.

1. Se inicia el asistente Crear modelo, que le guía.

   ![Asistente del modelo de fragmento de contenido](assets/content-structure/model-wizard.png)

   Proporcione la información obligatoria.

   * **Título de modelo** - Esta es una breve descripción del modelo y normalmente indica el propósito del modelo.
   * **Habilitar modelo** - Esta opción está activada de forma predeterminada y debe estar activada para poder crear fragmentos de contenido basados en este modelo.

1. Una vez rellenados los campos obligatorios, haga clic en **Crear** en la parte superior izquierda para crear el modelo.

1. La variable **Correcto** confirma que se creó el modelo.

   ![Cuadro de diálogo de éxito para crear un nuevo modelo de fragmento de contenido](assets/content-structure/success.png)

## Agregar campos al modelo {#configure-model}

Para poder utilizar el modelo, debe definir la estructura de sus datos.

1. Haga clic en **Apertura** en el **Correcto** del paso anterior para abrir el nuevo modelo en el editor del modelo de fragmento de contenido, donde puede definir sus campos.

1. Arrastre un campo desde la **Tipos de datos** a la derecha del editor y suéltelo en el modelo de fragmento de contenido.

   ![Añadir un tipo de datos](assets/content-structure/drop-fields.png)

1. Una vez colocado el tipo de datos, la variable **Tipos de datos** se ha cambiado automáticamente a **Propiedades** , donde puede definir los detalles del tipo de datos que acaba de colocar.

   ![La pestaña Propiedades del campo de datos](assets/content-structure/data-type-properties.png)

1. Una vez añadidos todos los campos necesarios para el modelo de fragmento de contenido, haga clic en **Guardar** en la parte superior derecha de la ventana.

El modelo se guarda y se vuelve a la consola del modelo de fragmento de contenido, donde puede agregar más modelos según sea necesario.

![Módulo completado](assets/content-structure/content-fragment-model-console-populated.png)
