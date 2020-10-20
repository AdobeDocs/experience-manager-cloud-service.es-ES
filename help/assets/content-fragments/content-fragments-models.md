---
title: Modelos de fragmento de contenido
description: Los modelos de fragmentos de contenido se utilizan para crear fragmentos de contenido con contenido estructurado.
translation-type: tm+mt
source-git-commit: 69756d6831678151b0e8eb73db81113d49f17447
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 22%

---


# Modelos de fragmento de contenido{#content-fragment-models}

Los modelos de fragmentos de contenido definen la estructura del contenido para los fragmentos [de](/help/assets/content-fragments/content-fragments.md)contenido.

## Enable Content Fragment Models {#enable-content-fragment-models}

>[!CAUTION]
>
>Si no habilita los modelos **de fragmentos** de contenido, la opción **Crear** no estará disponible para crear nuevos modelos.

Para habilitar los modelos de fragmentos de contenido debe:

* Habilitar el uso de modelos de fragmentos de contenido en el navegador de configuración
* Aplicar la configuración a la carpeta Assets

### Habilitar modelos de fragmento de contenido en el navegador de configuración {#enable-content-fragment-models-in-configuration-browser}

Para [crear un nuevo modelo](#creating-a-content-fragment-model) de fragmento de contenido, primero **debe** activarlo mediante el explorador [de configuración:](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)

1. Vaya a **Herramientas**, **General**, luego abra el **Explorador de configuración**.
2. Seleccione la ubicación adecuada para el sitio web.
3. Utilice **Crear** para abrir el cuadro de diálogo, donde:

   1. Especifique un **título**.
   2. Seleccione Modelos **de fragmento de contenido** para habilitar su uso.

   ![configuración](assets/cfm-models-01.png)

4. Seleccione **Crear** para guardar la definición.

### Aplicar la configuración a la carpeta de recursos {#apply-the-configuration-to-your-assets-folder}

Cuando la configuración **global** está habilitada para modelos de fragmentos de contenido, cualquier modelo que creen los usuarios se puede utilizar en cualquier carpeta de recursos.

Para utilizar otras configuraciones (es decir, excluyendo global) con una carpeta de Assets comparable, debe definir la conexión. Para ello, seleccione la **configuración** adecuada en la pestaña **Cloud Services** de las **Propiedades de carpeta** de la carpeta correspondiente.

## Creación de un modelo de fragmento de contenido {#creating-a-content-fragment-model}

1. Vaya a **Herramientas**, **Recursos** y, a continuación, abra Modelos **de fragmento de contenido**.
1. Vaya a la carpeta correspondiente a su [configuración](#enable-content-fragment-models).
1. Utilice **Crear** para abrir el asistente.

   >[!CAUTION]
   >
   >Si no se ha habilitado [el](#enable-content-fragment-models)uso de modelos de fragmentos de contenido, la opción **Crear** no estará disponible.

1. Especifique el **Título del modelo**. También puede agregar una **descripción** si fuera necesario.

   ![título y descripción](assets/cfm-models-02.png)

1. Utilice **Crear** para guardar el modelo vacío. Un mensaje indicará el éxito de la acción, puede seleccionar **Abrir** para editar inmediatamente el modelo o **Listo** para volver a la consola.

## Definición del modelo de fragmento de contenido {#defining-your-content-fragment-model}

El modelo de fragmento de contenido define eficazmente la estructura de los fragmentos de contenido resultantes. Con el editor de modelos puede agregar y configurar los campos obligatorios:

>[!CAUTION]
>
>La edición de un modelo de fragmento de contenido existente puede afectar a los fragmentos dependientes.

1. Vaya a **Herramientas**, **Recursos** y, a continuación, abra Modelos **de fragmento de contenido**.

1. Vaya a la carpeta que contiene el modelo de fragmentos de contenido.
1. Abra el modelo requerido para **Editar**; utilice la acción rápida o seleccione el modelo y, a continuación, la acción de la barra de herramientas.

   Una vez abierto, el editor de modelos muestra:

   * left: campos ya definidos
   * right: **Tipos de datos** disponibles para crear campos (y **Propiedades** para su uso una vez creados los campos)

   >[!NOTE]
   >
   >Cuando un campo es **obligatorio**, la **etiqueta** indicada en el panel izquierdo se marca con un asterisco (*****).

   ![propiedades](assets/cfm-models-03.png)

1. **Para Añadir un campo**

   * Arrastre un tipo de datos requerido a la ubicación requerida para un campo:

   ![tipo de datos al campo](assets/cfm-models-04.png)

   * Una vez agregado el campo al modelo, el panel derecho mostrará las **propiedades** que se pueden definir para ese tipo de datos en particular. Aquí puede definir lo que se necesita para ese campo. Por ejemplo:

   ![propiedades de campo](assets/cfm-models-05.png)

   >[!NOTE]
   Para el tipo de datos **Texto multilínea** es posible definir el **tipo predeterminado** como:
   * **Texto enriquecido**
   * **Markdown**
   * **Texto sin formato**

   Si no se especifica, se utiliza el valor predeterminado **Texto** enriquecido para este campo.
   Cambiar el **tipo predeterminado** en un modelo de fragmento de contenido solo surtirá efecto en un fragmento de contenido existente relacionado después de que dicho fragmento se abra en el editor y se guarde.

1. **Quitar un campo**

   Seleccione el campo requerido y toque o haga clic en el icono de papelera. Se le solicitará que confirme la acción.

   ![elimina](assets/cfm-models-06.png)

1. Después de agregar todos los campos obligatorios y definir las propiedades, utilice **Guardar** para mantener la definición. Por ejemplo:

   ![save](assets/cfm-models-07.png)

## Eliminación de un modelo de fragmento de contenido {#deleting-a-content-fragment-model}

>[!CAUTION]
La eliminación de un modelo de fragmento de contenido puede afectar a los fragmentos dependientes.

Para eliminar un modelo de fragmento de contenido:

1. Vaya a **Herramientas**, **Recursos** y, a continuación, abra Modelos **de fragmento de contenido**.

1. Vaya a la carpeta que contiene el modelo de fragmentos de contenido.
1. Seleccione el modelo, seguido de **Eliminar** de la barra de herramientas.

   >[!NOTE]
   Si se hace referencia al modelo, se mostrará una advertencia. Tome las medidas adecuadas.

## Publicación de un modelo de fragmento de contenido {#publishing-a-content-fragment-model}

Los modelos de fragmentos de contenido deben publicarse cuando se publiquen fragmentos de contenido dependientes o antes de hacerlo.

Para publicar un modelo de fragmento de contenido:

1. Vaya a **Herramientas**, **Recursos** y, a continuación, abra Modelos **de fragmento de contenido**.

1. Vaya a la carpeta que contiene el modelo de fragmentos de contenido.
1. Seleccione el modelo, seguido de **Publicar** en la barra de herramientas.

   >[!NOTE]
   Si publica un fragmento de contenido para el que el modelo aún no se ha publicado, una lista de selección lo indicará y el modelo se publicará con el fragmento.
