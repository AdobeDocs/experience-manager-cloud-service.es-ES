---
title: Esquema de metadatos de carpeta
description: Obtenga información sobre cómo crear un esquema de metadatos para las carpetas de recursos en [!DNL Experience Manager Assets]
contentOwner: AG
translation-type: tm+mt
source-git-commit: 3207151a76c51637551907d15a34f1a6b7450d02
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 10%

---


# Esquema de metadatos de carpeta {#folder-metadata-schema}

[!DNL Adobe Experience Manager Assets] le permite crear esquemas de metadatos para carpetas de recursos, que definen el diseño y los metadatos mostrados en las páginas de propiedades de las carpetas.

## Añadir un formulario de esquema de metadatos de carpeta {#add-a-folder-metadata-schema-form}

Utilice el editor de Forms de Esquema de metadatos de carpeta para crear y editar esquemas de metadatos para las carpetas.

1. Toque o haga clic en el logotipo [!DNL Experience Manager] y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Esquemas de metadatos de carpeta]**.
1. En la página de Forms Esquema de metadatos de la carpeta, toque o haga clic en **[!UICONTROL Crear]**.
1. Especifique un nombre para el formulario y toque/haga clic **[!UICONTROL Crear]**. El nuevo formulario de esquema se muestra en la página de Esquema Forms.

## Editar formularios de esquema de metadatos de carpeta {#edit-folder-metadata-schema-forms}

Puede editar un formulario de esquema de metadatos recién agregado o existente, que incluye lo siguiente:

* Pestañas
* Elementos de formulario dentro de las fichas.

Puede asignar/configurar estos elementos de formulario a un campo dentro de un nodo de metadatos en el repositorio de CRX. Puede agregar nuevas fichas o elementos de formulario al formulario de esquema de metadatos.

1. En la página Esquema Forms, seleccione el formulario que ha creado y, a continuación, toque o haga clic en el icono **[!UICONTROL Editar]** de la barra de herramientas.
1. En la página Editor de Esquemas de metadatos de carpeta, toque o haga clic en el icono **[!UICONTROL +]** para agregar una ficha al formulario. Para cambiar el nombre de la ficha, toque o haga clic en el nombre predeterminado y especifique el nuevo nombre en **[!UICONTROL Configuración]**.

   ![custom_tab](assets/custom_tab.png)

   Para agregar más fichas, toque o haga clic en el icono **[!UICONTROL +]**. Toque o haga clic **[!UICONTROL X]** para eliminar una ficha.

1. En la ficha activa, agregue uno o varios componentes de la ficha **[!UICONTROL Generar formulario]**.

   ![adding_components](assets/adding_components.png)

   Si crea varias fichas, toque o haga clic en una ficha concreta para agregar componentes.

1. Para configurar un componente, selecciónelo y modifique sus propiedades en la ficha **[!UICONTROL Configuración]**.

   Si es necesario, elimine un componente de la ficha **[!UICONTROL Configuración]**.

   ![configure_properties](assets/configure_properties.png)

1. Toque o haga clic **[!UICONTROL Guardar]** en la barra de herramientas para guardar los cambios.

### Componentes para generar formularios {#components-to-build-forms}

La ficha **[!UICONTROL Generar formulario]** lista elementos de formulario que se utilizan en el formulario de esquema de metadatos de la carpeta. La ficha **[!UICONTROL Configuración]** muestra los atributos de cada elemento seleccionado en la ficha **[!UICONTROL Generar formulario]**. Esta es una lista de los elementos de formulario disponibles en la ficha **[!UICONTROL Formulario de compilación]**:

<table>
 <tbody>
  <tr>
   <td><p><strong>Nombre del componente</strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p>Sección de encabezado</p> </td>
   <td><p> Añada un encabezado de sección para una lista de componentes comunes.</p> </td>
  </tr>
  <tr>
   <td><p>Texto de una sola línea</p> </td>
   <td><p> Añada una propiedad de texto de una sola línea. Se almacena como una cadena.</p> </td>
  </tr>
  <tr>
   <td><p>Texto con varios valores</p> </td>
   <td><p> Añada una propiedad de texto con varios valores. Se almacena como una matriz de cadenas.</p> </td>
  </tr>
  <tr>
   <td><p>Número</p> </td>
   <td><p> Añada un componente numérico.</p> </td>
  </tr>
  <tr>
   <td><p>Fecha</p> </td>
   <td><p> Añada un componente de fecha.</p> </td>
  </tr>
  <tr>
   <td><p>Lista desplegable</p> </td>
   <td><p> Añada una lista desplegable.</p> </td>
  </tr>
  <tr>
   <td><p>Etiquetas estándar</p> </td>
   <td><p> Añadir una etiqueta. </p> </td>
  </tr>
  <tr>
   <td><p>Campo oculto</p> </td>
   <td><p> Añada un campo oculto. Se envía como parámetro de POST cuando se guarda el recurso.</p> </td>
  </tr>
 </tbody>
</table>

### Edición de elementos de formulario {#editing-form-items}

Para editar las propiedades de los elementos de formulario, toque o haga clic en el componente y edite todo o un subconjunto de las siguientes propiedades en la ficha **[!UICONTROL Configuración]**.

**[!UICONTROL Etiqueta]** de campo: Nombre de la propiedad de metadatos que se muestra en la página de propiedades de la carpeta.

**[!UICONTROL Asignar a propiedad]**: Esta propiedad especifica la ruta relativa del nodo de la carpeta en el repositorio de CRX donde se guarda. Inicio con &quot;**./**&quot;, que indica que la ruta está bajo el nodo de la carpeta.

Los siguientes son los valores válidos para esta propiedad:

* `./jcr:content/metadata/dc:title`:: Almacena el valor en el nodo de metadatos de la carpeta como propiedad  `dc:title`.

* `./jcr:created`:: Almacena la fecha y hora de creación de un recurso. Es una propiedad protegida. Si configura estas propiedades, Adobe recomienda marcarlas como [!UICONTROL Deshabilitar Editar].

Para asegurarse de que el componente se muestra correctamente en el formulario de esquema de metadatos, no incluya ningún espacio en la ruta de la propiedad.

**[!UICONTROL Ruta]** JSON: Utilícelo para especificar la ruta del archivo JSON en la que se especifican pares de clave-valor para las opciones.

**[!UICONTROL Marcador de posición]**: Utilice esta propiedad para especificar el texto del marcador de posición correspondiente a la propiedad metadata.

**[!UICONTROL Opciones]**: Utilice esta propiedad para especificar opciones en una lista.

**[!UICONTROL Descripción]**: Utilice esta propiedad para agregar una breve descripción para el componente de metadatos.

**[!UICONTROL Clase]**: Clase de objeto con la que está asociada la propiedad.

## Eliminar formularios de esquema de metadatos de carpeta {#delete-folder-metadata-schema-forms}

Puede eliminar los formularios de esquema de metadatos de la carpeta desde la página de Forms Esquema de metadatos de la carpeta. Para eliminar un formulario, selecciónelo y toque o haga clic en el icono Eliminar de la barra de herramientas.

![delete_form](assets/delete_form.png)

## Asignar un esquema de metadatos de carpeta {#assign-a-folder-metadata-schema}

Puede asignar un esquema de metadatos de carpeta a una carpeta desde la página de Forms Esquema de metadatos de carpeta o al crear una carpeta.

Si configura un esquema de metadatos para una carpeta, la ruta al formulario de esquema se almacena en la propiedad `folderMetadataSchema` del nodo folder en .*/jcr:content*.

### Asignar a un esquema desde la página Esquema de metadatos de carpeta {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. Toque o haga clic en el logotipo [!DNL Experience Manager] y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** **[!UICONTROL Esquemas de metadatos de carpeta]**.
1. En la página Forms Esquema de metadatos de carpeta, seleccione el formulario de esquema que desea aplicar a una carpeta.
1. En la barra de herramientas, toque o haga clic en **[!UICONTROL Aplicar a carpetas]**.

1. Seleccione la carpeta en la que desea aplicar el esquema y toque o haga clic **[!UICONTROL Aplicar]**. Si ya se ha aplicado un esquema de metadatos a la carpeta, aparecerá un mensaje de advertencia para informarle de que va a sobrescribir el esquema de metadatos existente. Toque o haga clic **[!UICONTROL Sobrescribir]**.
1. Abra las propiedades de metadatos de la carpeta a la que ha aplicado el esquema de metadatos.

   ![folder_properties](assets/folder_properties.png)

   Para ver los campos de metadatos de la carpeta, pulse o haga clic en la pestaña **[!UICONTROL Metadatos de la carpeta]**.

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

### Asignar un esquema al crear una carpeta {#assign-a-schema-when-creating-a-folder}

Puede asignar un esquema de metadatos de carpeta al crear una carpeta. Si existe al menos un esquema de metadatos de carpeta en el sistema, se muestra una lista adicional en el cuadro de diálogo **[!UICONTROL Crear carpeta]**. Puede seleccionar el esquema que desee. De forma predeterminada, no hay ningún esquema seleccionado.

1. En la interfaz de usuario [!DNL Experience Manager Assets], toque o haga clic en **[!UICONTROL Crear]** desde la barra de herramientas.
1. Especifique un título y un nombre para la carpeta.
1. En la lista Esquema de metadatos de carpeta, seleccione el esquema que desee. A continuación, toque o haga clic en **[!UICONTROL Crear]**.

   ![select_esquema](assets/select_schema.png)

1. Abra las propiedades de metadatos de la carpeta a la que ha aplicado el esquema de metadatos.
1. Para ver los campos de metadatos de la carpeta, pulse o haga clic en la pestaña **[!UICONTROL Metadatos de la carpeta]**.

## Usar el esquema de metadatos de la carpeta {#use-the-folder-metadata-schema}

Abra las propiedades de una carpeta configurada con un esquema de metadatos de carpeta. Se muestra la pestaña **[!UICONTROL Metadatos de carpeta]** en la página de propiedades de la carpeta. Para ver el formulario de esquema de metadatos de la carpeta, seleccione esta pestaña.

Introduzca valores de metadatos en los distintos campos y toque o haga clic **[!UICONTROL Guardar]** para almacenar los valores. Los valores que especifique se almacenan en el nodo de la carpeta en el repositorio de CRX.

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)
