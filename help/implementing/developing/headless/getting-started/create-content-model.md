---
title: Creación de modelos de fragmento de contenido Guía de inicio rápido sin encabezado
description: Defina la estructura del contenido que creará y servirá con AEM capacidades sin encabezado mediante modelos de fragmento de contenido.
translation-type: tm+mt
source-git-commit: e7ca6dc841ba777384be74021a27d523d530a956
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---


# Creación de modelos de fragmento de contenido Guía de inicio rápido sin encabezado {#creating-content-fragment-models}

Defina la estructura del contenido que creará y servirá con AEM capacidades sin encabezado mediante modelos de fragmento de contenido.

## ¿Qué son los modelos de fragmento de contenido? {#what-are-content-fragment-models}

[Ahora que ha creado una configuración, ](create-configuration.md) puede utilizarla para crear modelos de fragmento de contenido.

Los modelos de fragmento de contenido definen la estructura de los datos y el contenido que creará y administrará en AEM. Sirven como un tipo de andamiaje para el contenido. Al elegir crear contenido, los autores seleccionarán entre los modelos de fragmento de contenido que defina, que los guiarán en la creación de contenido.

## Cómo crear un modelo de fragmento de contenido {#how-to-create-a-content-fragment-model}

Un arquitecto de la información realizaría estas tareas sólo esporádicamente, ya que se necesitan nuevos modelos. Para los fines de esta guía de introducción, solo necesitamos crear un modelo.

1. Inicie sesión en AEM como Cloud Service y, en el menú principal, seleccione **Herramientas -> Recursos -> Modelos de fragmento de contenido**.
1. Toque o haga clic en la carpeta que se creó creando la configuración.

   ![La carpeta de modelos](../assets/models-folder.png)
1. Haga clic o pulse **Crear**.
1. Proporcione un **Título de modelo**, **Etiquetas** y **Descripción**. También puede seleccionar o deseleccionar **Enable model** para controlar si el modelo se activa inmediatamente tras la creación.

   ![Creación de un modelo](../assets/models-create.png)
1. En la ventana de confirmación, pulse o haga clic en **Abrir** para configurar el modelo.

   ![Ventana de confirmación](../assets/models-confirmation.png)
1. Con el **Editor del modelo de fragmento de contenido**, cree el modelo de fragmento de contenido arrastrando y soltando los campos de la columna **Tipos de datos**.

   ![Arrastrar y soltar campos](../assets/models-drag-and-drop.png)

1. Una vez colocado un campo, se deben configurar sus propiedades. El editor cambiará automáticamente a la pestaña **Properties** del campo añadido, donde puede proporcionar los campos obligatorios.

   ![Configuración de propiedades](../assets/models-configure-properties.png)
1. Cuando haya terminado de crear el modelo, toque o haga clic en **Guardar**. El modelo recién creado se guarda en modo **Borrador**.

   ![Modelo en modo borrador](../assets/models-draft.png)
1. El modelo debe estar habilitado para utilizarlo (si no está activado). Seleccione el modelo que acaba de crear y, a continuación, toque o haga clic en **Habilitar**.

   ![Activación del modelo](../assets/models-enable.png)
1. Confirme la activación del modelo tocando o haciendo clic en **Habilitar** en el cuadro de diálogo de confirmación.

   ![Activación del cuadro de diálogo de confirmación](../assets/models-enabling.png)
1. El modelo está ahora habilitado y listo para usar.

   ![Modelo habilitado](../assets/models-enabled.png)

El **Editor del modelo de fragmento de contenido** admite muchos tipos de datos diferentes, como campos de texto simples, referencias de recursos, referencias a otros modelos y datos JSON.

Puede crear varios modelos. Los modelos pueden hacer referencia a otros fragmentos de contenido. Utilice [configuraciones](create-configuration.md) para organizar los modelos.

## Pasos siguientes {#next-steps}

Ahora que ha definido las estructuras de los fragmentos de contenido creando modelos, puede pasar a la tercera parte de la guía de introducción y [crear carpetas donde almacenará los propios fragmentos.](create-assets-folder.md)

>[!TIP]
>
>Para obtener más información sobre los modelos de fragmento de contenido, consulte la [documentación de los modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md)
