---
title: Crear fragmentos de formulario para la creación basada en WYSIWYG
description: Obtenga información sobre cómo crear fragmentos de formulario en el Editor universal y agregarlos a formularios.
feature: Edge Delivery Services
role: Admin, User, Developer
hide: true
hidefromtoc: true
source-git-commit: 62c58ceb2d2d659bad591b3eba1bfd924f2a848b
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 15%

---


# Crear y utilizar fragmentos de formulario de Edge Delivery Services en el editor universal

Forms suele incluir secciones comunes como información de contacto, detalles de identificación o acuerdos de consentimiento. Los desarrolladores de formularios crean estas secciones cada vez que crean un nuevo formulario, lo que resulta repetitivo y lleva tiempo.
Para eliminar esta duplicación de esfuerzos, Universal Editor proporciona una forma de crear segmentos de formulario reutilizables, como paneles o grupos de campos, una sola vez y reutilizarlos en varios formularios. Estos segmentos reutilizables, modulares e independientes se denominan fragmentos de formulario. Por ejemplo, el mismo fragmento de contacto de emergencia se puede utilizar en diferentes secciones de un formulario, como para los detalles de contacto del empleado y el supervisor.

Al final del artículo, aprenderá a crear y utilizar fragmentos en formularios con el Editor universal.

## Funciones de los fragmentos de formularios Edge Delivery Services

* **Mantener la coherencia con los fragmentos de formulario**
Puede integrar fragmentos en diferentes formularios, lo que le ayuda a mantener diseños coherentes y contenido estandarizado. Con el enfoque &quot;cambiar una vez, reflejar en todas partes&quot;, cualquier actualización realizada en un fragmento se aplica automáticamente a todos los formularios.

* **Agregando fragmentos de formulario varias veces dentro del formulario**
Puede agregar un fragmento de formulario varias veces dentro de un formulario y configurar sus propiedades de enlace de datos a fuentes de datos o esquemas.

* **Uso de fragmentos dentro de fragmentos**
Puede crear fragmentos de formulario anidados, lo que significa que puede agregar un fragmento en otro fragmento y tener una estructura anidada.

  >[!NOTE]
  >
  > No puede anidar un fragmento dentro de sí mismo, ya que esto puede causar referencias recursivas y un comportamiento no deseado, lo que provoca errores o problemas de procesamiento.

## Consideraciones al utilizar fragmentos de formulario de Edge Delivery Services

* Debe agregar la misma URL de GitHub en el fragmento y en el formulario en el que desea utilizar el fragmento.
* No puede editar un fragmento de formulario, que se inserte por referencia, desde un formulario. Para editarlo, modifique el fragmento de formulario independiente.

## Requisitos previos para crear fragmentos de formulario de Edge Delivery Services

* [Configure su repositorio de GitHub](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template) para establecer una conexión entre su entorno de AEM y el repositorio de GitHub.
* Si ya usa Edge Delivery Services, añada la versión más reciente del [bloque de formularios adaptables](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project) a su repositorio de GitHub.
* La instancia de autor de AEM Forms incluye una plantilla basada en Edge Delivery Services. Asegúrese de que la [última versión de los componentes principales](https://github.com/adobe/aem-core-forms-components) esté instalada en su entorno.
* Tenga a mano la URL de la instancia de autor de AEM Forms as a Cloud Service y el repositorio de GitHub.

## Uso de fragmentos de formulario Edge Delivery Services

Puede crear fragmentos de formulario de Edge Delivery Services en el Editor universal y agregar los fragmentos creados a los formularios de Edge Delivery Services. Puede realizar las siguientes acciones con fragmentos de formularios Edge Delivery Services Forms:

* [Creación de fragmentos de formulario](#creating-form-fragments)
* [Agregar fragmentos de formulario a un formulario](#adding-form-fragments-to-a-form)
* [Administrar fragmentos de formulario](#managing-form-fragments)

### Creación de fragmentos de formulario

Para crear un fragmento de formulario en el Editor universal, realice los siguientes pasos:

1. Inicie sesión en la instancia de autor de AEM Forms as a Cloud Service.
1. Seleccione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.
1. Haga clic en **Crear > fragmento de formulario adaptable**.

   ![Crear fragmento](/help/edge/docs/forms/universal-editor/assets/create-fragment.png)

   Aparece el asistente **Crear fragmento de formulario adaptable**.
1. Seleccione la plantilla basada en Servicios de entrega perimetral de **Seleccionar plantilla** y haga clic en **[!UICONTROL Siguiente]**.
   ![Seleccionar plantilla de Edge Delivery Services](/help/edge/docs/forms/universal-editor/assets/create-form-fragment.png)

1. Especifique el título, el nombre, la descripción y las etiquetas del fragmento. Asegúrese de especificar un nombre único para el fragmento. Si ya existe otro fragmento con el mismo nombre, el fragmento no se creará.
1. Especifique la **URL de GitHub**. Por ejemplo, si el repositorio de GitHub se llama `edsforms` y se encuentra en la cuenta `wkndforms`, la dirección URL es `https://github.com/wkndforms/edsforms`.

   ![propiedades básicas](/help/edge/docs/forms/universal-editor/assets/fragment-basic-properties.png)

1. (Opcional) Haga clic para abrir la ficha **Modelo de formulario** y, en el menú desplegable **Seleccionar de**, seleccione uno de los siguientes modelos para el fragmento:

   ![Muestra el tipo de modelo en la pestaña Modelo de formulario](/help/edge/docs/forms/universal-editor/assets/select-fdm-for-fragment.png)

   * **Modelo de datos de formulario (FDM)**: integre objetos y servicios de modelo de datos de fuentes de datos en el fragmento. Elija Modelo de datos de formulario (FDM) si el formulario requiere leer y escribir datos de varias fuentes.

   * **Esquema JSON**: integre el formulario con un sistema backend al asociar un esquema JSON que define la estructura de datos. Permite añadir contenido dinámico mediante los elementos de esquema.
   * **Ninguno**: especifica que se cree el fragmento desde cero sin usar ningún modelo de formulario.

   >[!NOTE]
   >
   > Para aprender a integrar formularios o fragmentos con un modelo de datos de formulario (FDM) en el editor universal para usar diversas fuentes de datos back-end, [haga clic aquí](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md).

1. (Opcional) Especifique la **Fecha de publicación** o la **Fecha de cancelación de publicación** del fragmento en la pestaña **Avanzadas**.

   ![Ficha avanzada](/help/edge/docs/forms/universal-editor/assets/advanced-properties-fragment.png)
1. Haga clic en **Crear** y aparecerá un asistente.

   ![Editar fragmento](/help/edge/docs/forms/universal-editor/assets/edit-fragment.png)

1. Haga clic en **Editar** y el fragmento creado con una plantilla predeterminada se abrirá en el Editor universal para la creación.

   ![Fragmento en el editor universal para la creación](/help/edge/docs/forms/universal-editor/assets/fragment-in-ue.png)

   En el modo de edición, puede agregar cualquier componente de formulario al fragmento. Para aprender a crear un fragmento en el editor universal, consulte el artículo de [Introducción a Edge Delivery Services para AEM Forms con el editor universal](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg).

   La siguiente captura de pantalla muestra `contact fragment` creado en el editor universal.

   ![Fragmento de contacto](/help/edge/docs/forms/universal-editor/assets/contact-fragment.png)

   Una vez creado el fragmento, puede [agregar el fragmento creado en Edge Delivery Services Forms](#adding-form-fragments-in-forms).

### Agregar fragmentos de formulario a un formulario

Vamos a crear un formulario `Employee Details` simple que incluya información sobre el empleado y el supervisor. Puede usar el fragmento `Contact Details` en los paneles empleado y supervisor. Para utilizar el fragmento de formulario en el formulario, realice los siguientes pasos:

1. Abra el formulario en modo de edición.
1. Agregue el componente Fragmento de formulario al formulario.
1. Abra el explorador de contenido y vaya al componente **[!UICONTROL Formulario adaptable]** en el **Árbol de contenido**.
1. Vaya a la sección, donde desea agregar un fragmento. Por ejemplo, vaya al panel **Detalles del empleado**.

   ![Vaya a la sección](/help/edge/docs/forms/universal-editor/assets/navigate-to-section.png)

1. Haga clic en el icono **[!UICONTROL Agregar]** y agregue el componente **[!UICONTROL Fragmento de formulario]** de la lista **Componentes de formulario adaptable**.
   ![Agregar fragmento de formulario](/help/edge/docs/forms/universal-editor/assets/add-fragment.png)

   Al seleccionar el componente **[!UICONTROL Fragmento de formulario]**, el fragmento se agrega al formulario. Puede configurar las propiedades del fragmento agregado abriendo sus **Propiedades**. Por ejemplo, oculte el título del fragmento de sus **propiedades**.

   ![Configurando propiedades del fragmento](/help/edge/docs/forms/universal-editor/assets/fragment-properties.png)

1. Seleccione la **Referencia de fragmento** en la pestaña **Básico**. Aparecerán todos los fragmentos disponibles para el formulario, según el modelo del formulario.

   Por ejemplo, vaya a `/content/forms/af` y seleccione el fragmento `Contact Details`.

   ![Seleccionar fragmento](/help/edge/docs/forms/universal-editor/assets/select-fragment.png)

1. Haga clic en **[!UICONTROL Seleccionar]**.

   El fragmento de formulario se agrega por referencia al formulario y permanece sincronizado con el fragmento de formulario independiente. Esto implica que cualquier modificación realizada en el fragmento se reflejará en todas las instancias en las que el fragmento se incorpore a los formularios.

   ![Fragmento en formulario](/help/edge/docs/forms/universal-editor/assets/fragment-in-form.png)

   Puede obtener una vista previa del formulario para ver cómo aparece en el modo **Vista previa**.

   ![Previsualizar](/help/edge/docs/forms/universal-editor/assets/preview-form-with-fragment.png)

   Del mismo modo, puede repetir los pasos 3 al 7 para insertar el fragmento `Contact Details` para el panel `Supervisor Details`.

   ![Formulario de detalles del empleado](/help/edge/docs/forms/universal-editor/assets/employee-detail-form-with-fragments.png)

### Administrar fragmentos de formulario

Puede realizar varias operaciones en los fragmentos de formulario mediante la interfaz de usuario de AEM Forms.

1. Inicie sesión en la instancia de autor de AEM Forms as a Cloud Service.
1. Seleccione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.

1. Seleccione un fragmento de formulario y la barra de herramientas mostrará las siguientes operaciones que puede realizar en el fragmento seleccionado.

   ![Administrar fragmento](/help/edge/docs/forms/universal-editor/assets/manage-fragment.png)

   <table>
    <tbody>
    <tr>
   <td><p><strong>Operación</strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
    </tr>
    <tr>
   <td><p>Editar</p> </td>
   <td><p>Abre el fragmento de formulario en modo de edición.<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Propiedades</p> </td>
   <td><p>Proporciona opciones para modificar las propiedades del fragmento de formulario.<br /> <br /> </p> </td>
    </tr>
    <td><p>Copiar</p> </td>
   <td><p> Proporciona opciones para copiar el fragmento de formulario y pegarlo en la ubicación deseada. <br /> <br /> </p> </td>
    </tr>
   <tr>
   <td><p>Vista previa</p> </td>
   <td><p>Proporciona opciones para obtener una vista previa del fragmento como HTML o realizar una vista previa personalizada combinando datos de un archivo XML con el fragmento. <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Descargar</p> </td>
   <td><p>Descarga el fragmento seleccionado.<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Iniciar revisión/Administrar revisión</p> </td>
   <td><p>Permite iniciar y administrar una revisión del fragmento seleccionado.<br /> <br /> </p> </td>
    </tr>
    <!--<tr>
   <td><p>Add Dictionary</p> </td>
   <td><p>Generates a dictionary for localizing the selected fragment. For more information, see <a>Localizing Adaptive Forms</a>.<br /> <br /> </p> </td>
    </tr>-->
    <tr>
   <td><p>Publicar o cancelar la publicación</p> </td>
   <td><p>Publica/cancela la publicación del fragmento seleccionado.<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Eliminar</p> </td>
   <td><p>Elimina el fragmento seleccionado.<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Comparar</p> </td>
   <td><p>Compara dos fragmentos de formulario diferentes con fines de vista previa.<br /> <br /> </p> </td>
    </tr>
    </tbody>
    </table>

## Prácticas recomendadas

* Asegúrese de que el nombre del fragmento sea único. El fragmento no se creará si hay un fragmento existente con el mismo nombre.
* Cualquier expresión, script o estilo de un fragmento de formulario independiente se conservará cuando se inserte por referencia o se incruste en un formulario.
* Al publicar un formulario, los fragmentos de formulario insertados por referencia dentro del formulario se publican automáticamente.

## Véase también

{{universal-editor-see-also}}