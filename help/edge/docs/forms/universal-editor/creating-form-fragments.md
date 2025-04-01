---
title: Cómo crear fragmentos de formulario para la creación basada en WYSIWYG
description: Obtenga información sobre cómo crear fragmentos de formulario en el editor universal y añadirlos a formularios.
feature: Edge Delivery Services
role: Admin, User, Developer
hide: true
hidefromtoc: true
exl-id: 7b0d4c7f-f82f-407b-8e25-b725108f8455
source-git-commit: 615f4686fed0d17b7d7aa5cd86c545b11952d792
workflow-type: ht
source-wordcount: '1324'
ht-degree: 100%

---

# Creación y utilización de fragmentos de formulario de Edge Delivery Services en el editor universal

Los formularios suelen incluir secciones comunes como la información de contacto, detalles de identificación o acuerdos de consentimiento. Los desarrolladores de formularios crean estas secciones cada vez que generan un nuevo formulario, lo que resulta repetitivo y lleva tiempo.
Para eliminar esta duplicación de esfuerzos, el editor universal proporciona una forma de crear segmentos de formulario reutilizables, como, por ejemplo, paneles o grupos de campos, una sola vez y reutilizarlos en varios formularios. Estos segmentos reutilizables e independientes se denominan fragmentos de formulario. Por ejemplo, el mismo fragmento de contacto de emergencia se puede utilizar en diferentes secciones de un formulario, como, por ejemplo, para los detalles de contacto del empleado y el supervisor.

Al final del artículo, aprenderá a crear y utilizar fragmentos en formulario con el editor universal.

## Funciones de los fragmentos de formulario de Edge Delivery Services

* **Mantenimiento de la coherencia con los fragmentos de formulario**
Puede integrar fragmentos en diferentes formularios, lo que le ayuda a mantener diseños coherentes y contenido estandarizado. Con el enfoque &quot;cambiar una vez, reflejar en todas partes&quot;, cualquier actualización realizada en un fragmento se aplica automáticamente a todos los formularios.

* **Adición de fragmentos de formulario varias veces dentro del formulario**
Puede añadir un fragmento de formulario varias veces dentro de un formulario y configurar sus propiedades de enlace de datos a fuentes de datos o esquemas.

* **Utilización de fragmentos dentro de fragmentos**
Puede crear fragmentos de formularios anidados, lo que significa que puede añadir un fragmento en otro fragmento y tener una estructura anidada.

  >[!NOTE]
  >
  > No puede anidar un fragmento dentro de sí mismo, ya que esto puede causar referencias recursivas y un comportamiento no deseado, lo que provoca errores o problemas de procesamiento.

## Consideraciones al utilizar fragmentos de formulario de Edge Delivery Services

* Debe añadir la misma URL de GitHub en el fragmento y en el formulario en el que desea utilizar el fragmento.
* No puede editar un fragmento de formulario, que se inserta por referencia, desde un formulario. Para editarlo, modifique el fragmento de formulario independiente.

## Requisitos previos para crear fragmentos de formulario de Edge Delivery Services

* [Configure el repositorio de GitHub](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template) para establecer una conexión entre el entorno de AEM y el repositorio de GitHub.
* Si ya usa Edge Delivery Services, añada la versión más reciente del [bloque de formularios adaptables](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project) a su repositorio de GitHub.
* La instancia de autor de AEM Forms incluye una plantilla basada en Edge Delivery Services. Asegúrese de que la [última versión de los componentes principales](https://github.com/adobe/aem-core-forms-components) esté instalada en su entorno.
* Tenga a mano la URL de la instancia de autor de AEM Forms as a Cloud Service y el repositorio de GitHub.

## Uso de fragmentos de formulario de Edge Delivery Services

Puede crear fragmentos de formulario de Edge Delivery Services en el editor universal y añadir los fragmentos creados a los formularios de Edge Delivery Services. Puede realizar las siguientes acciones con fragmentos de formulario de Edge Delivery Services:

* [Creación de fragmentos de formulario](#creating-form-fragments)
* [Adición de fragmentos de formulario a un formulario](#adding-form-fragments-to-a-form)
* [Administración de fragmentos de formulario](#managing-form-fragments)

### Creación de fragmentos de formulario

Para crear un fragmento de formulario en el editor universal, realice los siguientes pasos:

1. Inicie sesión en la instancia de autor de AEM Forms as a Cloud Service.
1. Seleccione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.
1. Haga clic en **Crear > fragmento de formulario adaptable**.

   ![Crear fragmento](/help/edge/docs/forms/universal-editor/assets/create-fragment.png)

   Aparece el asistente **Crear fragmento de formulario adaptable**.
1. Seleccione la plantilla basada en Edge Delivery Services en la pestaña **Seleccionar plantilla** y haga clic en **[!UICONTROL Siguiente]**.
   ![Seleccionar plantilla de Edge Delivery Services](/help/edge/docs/forms/universal-editor/assets/create-form-fragment.png)

1. Especifique el título, el nombre, la descripción y las etiquetas del fragmento. Asegúrese de especificar un nombre único para el fragmento. Si ya existe otro fragmento con el mismo nombre, el fragmento no se creará.
1. Especifique la **URL de GitHub**. Por ejemplo, si el repositorio de GitHub se llama `edsforms`, está ubicado en la cuenta `wkndforms` y la URL es `https://github.com/wkndforms/edsforms`.

   ![Propiedades básicas](/help/edge/docs/forms/universal-editor/assets/fragment-basic-properties.png)

1. (Opcional) Haga clic para abrir la pestaña **modelo de formulario** y desde el menú desplegable **Seleccionar de**, seleccione uno de los siguientes modelos para el fragmento:

   ![Muestra el tipo de modelo en la pestaña Modelo de formulario](/help/edge/docs/forms/universal-editor/assets/select-fdm-for-fragment.png)

   * **Modelo de datos de formulario (FDM)**: integre objetos y servicios de modelo de datos desde las fuentes de datos en su fragmento. Elija Modelo de datos de formulario (FDM) si el formulario requiere leer y escribir datos de varias fuentes.

   * **Esquema JSON**: integre su formulario con un sistema back-end asociando un esquema JSON que defina la estructura de datos. Le permite añadir contenido dinámico mediante los elementos de esquema.
   * **Ninguno**: especifica que se cree el fragmento desde cero sin usar ningún modelo de formulario.

   >[!NOTE]
   >
   > Para aprender a integrar formularios o fragmentos con un modelo de datos de formulario (FDM) en el editor universal para utilizar diversas fuentes de datos back-end, [haga clic aquí](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md).

1. (Opcional) Especifique la **Fecha de publicación** o la **Fecha de cancelación de publicación** del fragmento en la pestaña **Avanzado**.

   ![Pestaña Avanzado](/help/edge/docs/forms/universal-editor/assets/advanced-properties-fragment.png)
1. Haga clic en **Crear** y aparecerá un asistente.

   ![Editar fragmento](/help/edge/docs/forms/universal-editor/assets/edit-fragment.png)

1. Haga clic en **Editar** y el fragmento creado con una plantilla predeterminada se abrirá en el editor universal para la creación.

   ![Fragmento del editor universal para la creación](/help/edge/docs/forms/universal-editor/assets/fragment-in-ue.png)

   En el modo de edición, puede añadir cualquier componente del formulario al fragmento. Para obtener información sobre cómo crear formularios en el editor universal, consulte el artículo [Introducción a Edge Delivery Services para AEM Forms con el editor universal](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg).

   La siguiente captura de pantalla muestra el `contact fragment` creado en el editor universal.

   ![Fragmento de contacto](/help/edge/docs/forms/universal-editor/assets/contact-fragment.png)

   Una vez creado el fragmento, puede [añadir el fragmento creado en Edge Delivery Services Forms](#adding-form-fragments-in-forms).

### Adición de fragmentos de formulario a un formulario

Vamos a crear un formulario `Employee Details` simple que incluya información sobre el empleado y sobre el supervisor. Puede usar el fragmento `Contact Details` en los paneles del empleado y el supervisor. Para utilizar el fragmento de formulario en su formulario, realice los siguientes pasos:

1. Abra el formulario en modo de edición. 
1. Añada el componente Fragmento de formulario al formulario.
1. Abra el explorador de contenido y vaya al componente **[!UICONTROL Formulario adaptable]** en el **Árbol de contenido**.
1. Vaya a la sección, donde desea añadir un fragmento. Por ejemplo, vaya al panel **Detalles del empleado**.

   ![Navegar hasta la sección](/help/edge/docs/forms/universal-editor/assets/navigate-to-section.png)

1. Haga clic en el icono de **[!UICONTROL Añadir]** y añada el componente **[!UICONTROL Fragmento de formulario]** en la lista **Componentes de formularios adaptables**.
   ![Añadir fragmento de formulario](/help/edge/docs/forms/universal-editor/assets/add-fragment.png)

   Al seleccionar el componente **[!UICONTROL Fragmento de formulario]**, el fragmento se añade a su formulario. Puede configurar las propiedades del fragmento añadido abriendo sus **Propiedades**. Por ejemplo, oculte el título del fragmento de sus **propiedades**.

   ![Configuración de las propiedades del fragmento](/help/edge/docs/forms/universal-editor/assets/fragment-properties.png)

1. Seleccione la **Referencia de fragmento** en la pestaña **Básico**. Aparecerán todos los fragmentos disponibles para su formulario, según el modelo del formulario.

   Por ejemplo, vaya a `/content/forms/af` y seleccione el fragmento `Contact Details`.

   ![Seleccionar fragmento](/help/edge/docs/forms/universal-editor/assets/select-fragment.png)

1. Haga clic en **[!UICONTROL Seleccionar]**.

   El fragmento de formulario se añade por referencia al formulario adaptable y se sincroniza con el fragmento de formulario independiente. Esto implica que cualquier modificación realizada en el fragmento de formulario adaptable se reflejará en todas las instancias en las que el fragmento se incorpore dentro de los formularios.

   ![Fragmento en formulario](/help/edge/docs/forms/universal-editor/assets/fragment-in-form.png)

   Puede obtener una vista previa del formulario para ver cómo aparece en el modo **Vista previa**.

   ![Vista previa](/help/edge/docs/forms/universal-editor/assets/preview-form-with-fragment.png)

   Del mismo modo, puede repetir los pasos 3 al 7 para insertar el fragmento `Contact Details` para el panel `Supervisor Details`.

   ![Formulario de detalles del empleado](/help/edge/docs/forms/universal-editor/assets/employee-detail-form-with-fragments.png)

### Administración de fragmentos de formulario

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
   <td><p>Abre el fragmento de formulario en el modo de edición.<br /> <br /> </p> </td>
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
   <td><p>Proporciona opciones para previsualizar el fragmento como HTML o realizar una vista previa personalizada combinando los datos de un archivo XML con el fragmento.<br /> </p> </td>
    </tr>
    <tr>
   <td><p>Descargar</p> </td>
   <td><p>Descarga el fragmento seleccionado.<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Iniciar revisión y Administrar revisión</p> </td>
   <td><p>Permite iniciar y administrar una revisión del fragmento seleccionado.<br /> <br />  </p> </td>
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
   <td><p>Compara dos fragmentos de formulario diferentes para obtener una vista previa.<br /> <br /> </p> </td>
    </tr>
    </tbody>
    </table>

## Prácticas recomendadas

* Asegúrese de que el nombre del fragmento sea único. El fragmento no se creará si hay un fragmento existente con el mismo nombre.
* Cualquier expresión, script o estilo de un fragmento de formulario independiente se conservará cuando se inserte por referencia o se incruste en un formulario.
* Al publicar un formulario, los fragmentos de formulario insertados por referencia dentro del formulario se publican automáticamente.

## Véase también

{{universal-editor-see-also}}
