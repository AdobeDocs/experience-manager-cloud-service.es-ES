---
title: 'Creación de modelos de fragmentos de contenido: configuración sin encabezado'
description: Defina la estructura del contenido que creará y servirá con las capacidades sin encabezado de AEM mediante modelos de fragmentos de contenido.
exl-id: 8e3e4d00-34d3-4d4f-bc3a-43b8a322b986
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 97%

---

# Creación de modelos de fragmentos de contenido: configuración sin encabezado {#creating-content-fragment-models}

Defina la estructura del contenido que creará y servirá con las capacidades sin encabezado de AEM mediante modelos de fragmentos de contenido.

## ¿Qué son los modelos de fragmentos de contenido? {#what-are-content-fragment-models}

[Ahora que ha creado una configuración,](create-configuration.md) puede utilizarla para generar modelos de fragmentos de contenido.

Los modelos de fragmentos de contenido definen la estructura de los datos y el contenido que creará y administrará en AEM. Sirven como una especie de andamiaje para el contenido. Al elegir crear contenido, los autores elegirán entre los modelos de fragmentos de contenido que defina, que los guiarán en la creación de contenido.

## Cómo crear un modelo de fragmento de contenido {#how-to-create-a-content-fragment-model}

Un arquitecto de la información realizaría estas tareas solo de forma esporádica, a medida que se necesiten nuevos modelos. Para los fines de esta guía de introducción, solo necesitamos crear un modelo.

1. Inicie sesión en AEM as a Cloud Service y, en el menú principal, seleccione **Herramientas**, **General**, **Modelos de fragmentos de contenido**.
1. Toque o haga clic en la carpeta que se formó al crear la configuración.

   ![La carpeta de modelos](../assets/models-folder.png)
1. Haga clic o pulse en **Crear**.
1. Proporcione un **Título de modelo**, **Etiquetas** y una **Descripción**. También puede seleccionar o anular la selección de **Habilitar modelo** para controlar si el modelo se activa inmediatamente tras la creación.

   ![Creación de un modelo](../assets/models-create.png)
1. En la ventana de confirmación, pulse o haga clic en **Abrir** para configurar el modelo.

   ![Ventana de confirmación](../assets/models-confirmation.png)
1. Con el **Editor del modelo de fragmento de contenido**, cree su modelo de fragmento de contenido arrastrando y soltando campos de la columna **Tipos de datos**.

   ![Arrastre y coloque campos](../assets/models-drag-and-drop.png)

1. Una vez colocado un campo, se deben configurar sus propiedades. El editor cambiará automáticamente a la pestaña **Propiedades** para el campo añadido, donde puede proporcionar los campos obligatorios.

   ![Configure las propiedades](../assets/models-configure-properties.png)

1. Cuando haya terminado de crear el modelo, toque o haga clic en **Guardar**.

1. El modo del modelo recién creado depende de si ha seleccionado **Activar modelo** al crearlo:
   * Seleccionado: el nuevo modelo ya estará **Habilitado**
   * No seleccionado: el nuevo modelo se crea en modo **Borrador**

1. Si aún no lo está, el modelo debe estar **Habilitado** para utilizarlo.
   1. Seleccione el modelo que acaba de crear y, a continuación, toque o haga clic en **Habilitar**.

      ![Activación del modelo](../assets/models-enable.png)
   1. Confirme la activación del modelo tocando o haciendo clic en **Habilitar** en el cuadro de diálogo de confirmación.

      ![Activación del cuadro de diálogo de confirmación](../assets/models-enabling.png)
1. El modelo está ahora habilitado y listo para usarse.

   ![Modelo habilitado](../assets/models-enabled.png)

El **Editor del modelo de fragmentos de contenido** admite muchos tipos de datos diferentes, como campos de texto simples, referencias de recursos, referencias a otros modelos y datos JSON.

Puede crear varios modelos. Los modelos pueden hacer referencia a otros fragmentos de contenido. Use [configuraciones](create-configuration.md) para organizar los modelos.

## Siguientes pasos {#next-steps}

Ahora que ya ha definido las estructuras de los fragmentos de contenido creando modelos, puede pasar a la tercera parte de la guía de introducción y [crear las carpetas donde almacenará los fragmentos.](create-assets-folder.md)

>[!TIP]
>
>Para obtener información detallada acerca de los modelos de fragmento de contenido, consulte la [Documentación de modelos de fragmento de contenido](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)
