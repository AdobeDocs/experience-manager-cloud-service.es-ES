---
title: Esquema de metadatos de carpeta
description: Obtenga información sobre cómo crear esquemas de metadatos para carpetas de recursos en  [!DNL Experience Manager Assets]
contentOwner: AG
feature: Metadata
role: User, Admin
exl-id: c86760ed-169d-40f7-91a4-8aee449b286c
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1066'
ht-degree: 10%

---

# Esquema de metadatos de carpeta {#folder-metadata-schema}

[!DNL Adobe Experience Manager Assets] le permite crear esquemas de metadatos para carpetas de recursos, que definen el diseño y los metadatos mostrados en las páginas de propiedades de la carpeta.

## Agregar un formulario de esquema de metadatos de carpeta {#add-a-folder-metadata-schema-form}

Utilice el editor de Forms del Esquema de metadatos de carpeta para crear y editar esquemas de metadatos para carpetas.

1. Seleccione el logotipo de [!DNL Experience Manager] y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de metadatos de carpeta]**.
1. En la página Forms del esquema de metadatos de carpeta, seleccione **[!UICONTROL Crear]**.
1. Especifique un nombre para el formulario y seleccione **[!UICONTROL Crear]**. El nuevo formulario de esquema aparece en la página Esquema: Forms.

## Editar formularios de esquema de metadatos de carpeta {#edit-folder-metadata-schema-forms}

Puede editar un formulario de esquema de metadatos recién agregado o existente, que incluya lo siguiente:

* Pestañas
* Elementos de formulario dentro de pestañas.

Puede asignar o configurar estos elementos de formulario a un campo dentro de un nodo de metadatos en el repositorio de CRX. Puede agregar nuevas pestañas o elementos de formulario al formulario de esquema de metadatos.

1. En la página Schema Forms, seleccione el formulario que ha creado y, a continuación, seleccione el icono **[!UICONTROL Edit]** en la barra de herramientas.
1. En la página Editor de esquemas de metadatos de carpeta, seleccione el icono **[!UICONTROL +]** para agregar una pestaña al formulario. Para cambiar el nombre de la ficha, seleccione el nombre predeterminado y especifique el nuevo nombre en **[!UICONTROL Configuración]**.

   ![ficha_personalizada](assets/custom_tab.png)

   Para agregar más fichas, seleccione el icono **[!UICONTROL +]**. Seleccione **[!UICONTROL X]** para eliminar una ficha.

1. En la ficha activa, agregue uno o más componentes desde la ficha **[!UICONTROL Generar formulario]**.

   ![agregar_componentes](assets/adding_components.png)

   Si crea varias pestañas, seleccione una pestaña en particular para añadir componentes.

1. Para configurar un componente, selecciónelo y modifique sus propiedades en la ficha **[!UICONTROL Configuración]**.

   Si es necesario, elimine un componente de la ficha **[!UICONTROL Configuración]**.

   ![configurar_propiedades](assets/configure_properties.png)

1. Seleccione **[!UICONTROL Guardar]** en la barra de herramientas para guardar los cambios.

### Componentes para crear formularios {#components-to-build-forms}

La pestaña **[!UICONTROL Generar formulario]** enumera los elementos de formulario que usa en el formulario de esquema de metadatos de la carpeta. La ficha **[!UICONTROL Configuración]** muestra los atributos de cada elemento que seleccione en la ficha **[!UICONTROL Generar formulario]**. Esta es una lista de los elementos de formulario disponibles en la ficha **[!UICONTROL Generar formulario]**:

<table>
 <tbody>
  <tr>
   <td><p><strong>Nombre del componente</strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p>Encabezado de sección</p> </td>
   <td><p> Añada un encabezado de sección para una lista de componentes comunes.</p> </td>
  </tr>
  <tr>
   <td><p>Texto de una sola línea</p> </td>
   <td><p> Agregue una propiedad de texto de una sola línea. Se almacena como una cadena.</p> </td>
  </tr>
  <tr>
   <td><p>Texto con varios valores</p> </td>
   <td><p> Agregue una propiedad de texto de varios valores. Se almacena como una matriz de cadenas.</p> </td>
  </tr>
  <tr>
   <td><p>Número</p> </td>
   <td><p> Añada un componente de número.</p> </td>
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
   <td><p> Añada una etiqueta. </p> </td>
  </tr>
  <tr>
   <td><p>Campo oculto</p> </td>
   <td><p> Agregue un campo oculto. Se envía como parámetro POST cuando se guarda el recurso.</p> </td>
  </tr>
 </tbody>
</table>

### Edición de elementos de formulario {#editing-form-items}

Para editar las propiedades de los elementos del formulario, seleccione el componente y edite todas o un subconjunto de las siguientes propiedades en la ficha **[!UICONTROL Configuración]**. Se recomienda asignar solo un campo a una propiedad determinada en el esquema de metadatos. De lo contrario, el sistema selecciona el último campo añadido asignado a la propiedad.

**[!UICONTROL Etiqueta de campo]**: nombre de la propiedad de metadatos que se muestra en la página de propiedades de la carpeta.

**[!UICONTROL Asignar a propiedad]**: esta propiedad especifica la ruta relativa del nodo de carpeta en el repositorio de CRX donde se guarda. Comienza con &quot;**./**&quot;, que indica que la ruta de acceso se encuentra bajo el nodo de la carpeta.

Los siguientes son ejemplos de valores válidos para una propiedad:

* `./jcr:content/metadata/dc:title`: almacena el valor en el nodo de metadatos de la carpeta como la propiedad `dc:title`.

* `./jcr:created`: almacena la fecha y hora de creación de un recurso. Es una propiedad protegida. Si configura estas propiedades, Adobe recomienda marcarlas como [!UICONTROL Deshabilitar edición].

Para asegurarse de que el componente se muestra correctamente en el formulario de esquema de metadatos, no incluya un espacio en la ruta de la propiedad.

**[!UICONTROL Ruta de acceso JSON]**: utilícela para especificar la ruta de acceso del archivo JSON donde se especifican pares clave-valor para las opciones.

**[!UICONTROL Marcador de posición]**: utilice esta propiedad para especificar el texto de marcador de posición relevante con respecto a la propiedad de metadatos.

**[!UICONTROL Opciones]**: utilice esta propiedad para especificar opciones en una lista.

**[!UICONTROL Descripción]**: utilice esta propiedad para agregar una descripción breve para el componente de metadatos.

**[!UICONTROL Clase]**: clase de objeto a la que está asociada la propiedad.

## Eliminar formularios de esquema de metadatos de carpeta {#delete-folder-metadata-schema-forms}

Puede eliminar formularios de esquema de metadatos de carpeta desde la página de Forms Esquema de metadatos de carpeta. Para eliminar un formulario, selecciónelo y seleccione el icono Eliminar de la barra de herramientas.

![eliminar_formulario](assets/delete_form.png)

## Asignar un esquema de metadatos de carpeta {#assign-a-folder-metadata-schema}

Puede asignar un esquema de metadatos de carpeta a una carpeta desde la página de Forms Esquema de metadatos de carpeta o al crear una carpeta.

Si configura un esquema de metadatos para una carpeta, la ruta al formulario de esquema se almacena en la propiedad `folderMetadataSchema` del nodo de carpeta en */jcr:content*.

### Asignar a un esquema desde la página Esquema de metadatos de carpeta {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. Seleccione el logotipo de [!DNL Experience Manager] y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]**> **[!UICONTROL Esquemas de metadatos de carpeta]**.
1. En la página Forms del esquema de metadatos de carpeta, seleccione el formulario de esquema que desee aplicar a una carpeta.
1. En la barra de herramientas, seleccione **[!UICONTROL Aplicar a las carpetas]**.

1. Seleccione la carpeta en la que desea aplicar el esquema y, a continuación, seleccione **[!UICONTROL Aplicar]**. Si ya se ha aplicado un esquema de metadatos en la carpeta, un mensaje de advertencia le informa de que está a punto de sobrescribir el esquema de metadatos existente. Seleccione **[!UICONTROL Sobrescribir]**.
1. Abra las propiedades de metadatos de la carpeta a la que aplicó el esquema de metadatos.

   ![propiedades_de_carpeta](assets/folder_properties.png)

   Para ver los campos de metadatos de la carpeta, seleccione la ficha **[!UICONTROL Metadatos de la carpeta]**.

   ![propiedades_metadatos_carpeta](assets/folder_metadata_properties.png)

### Asignar un esquema al crear una carpeta {#assign-a-schema-when-creating-a-folder}

Puede asignar un esquema de metadatos de carpeta al crear una carpeta. Si existe al menos un esquema de metadatos de carpeta en el sistema, se mostrará una lista adicional en el cuadro de diálogo **[!UICONTROL Crear carpeta]**. Puede seleccionar el esquema deseado. De forma predeterminada, no se selecciona ningún esquema.

1. En la interfaz de usuario [!DNL Experience Manager Assets], seleccione **[!UICONTROL Crear]** en la barra de herramientas.
1. Especifique un título y un nombre para la carpeta.
1. En la lista Esquema de metadatos de carpeta, seleccione el esquema deseado. A continuación, seleccione **[!UICONTROL Crear]**.

   ![select_schema](assets/select_schema.png)

1. Abra las propiedades de metadatos de la carpeta a la que aplicó el esquema de metadatos.
1. Para ver los campos de metadatos de la carpeta, seleccione la ficha **[!UICONTROL Metadatos de la carpeta]**.

## Usar el esquema de metadatos de carpeta {#use-the-folder-metadata-schema}

Abra las propiedades de una carpeta configurada con un esquema de metadatos de carpeta. Se muestra la pestaña **[!UICONTROL Metadatos de carpeta]** en la página de propiedades de la carpeta. Para ver el formulario de esquema de metadatos de la carpeta, seleccione esta pestaña.

Escriba valores de metadatos en los distintos campos y seleccione **[!UICONTROL Guardar]** para almacenar los valores. Los valores especificados se almacenan en el nodo folder del repositorio de CRX.

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con recursos](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos de red](use-assets-across-connected-assets-instances.md)
* [Informes de recurso](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)
* [Publicación de recursos en AEM y Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
