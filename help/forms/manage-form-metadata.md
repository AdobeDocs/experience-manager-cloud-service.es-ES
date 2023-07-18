---
title: Administración de metadatos
seo-title: Manage [!DNL AEM Forms] metadata
description: Los metadatos facilitan la categorización y organización de los recursos y ayudan a los usuarios que buscan un recurso específico.
seo-description: Metadata allows for easier categorization and organization of assets and helps users who are looking for a specific asset.
exl-id: 8527246a-37f0-4d43-a49e-1c76c265514e
source-git-commit: b6dcb6308d1f4af7a002671f797db766e5cfe9b5
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 96%

---

# Adición, eliminación o edición de metadatos de un formulario adaptable {#manage-form-metadata}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-65/forms/manage-administer-aem-forms/manage-form-metadata.html) |
| AEM as a Cloud Service | Este artículo |

Los metadatos facilitan la categorización y organización de los recursos y ayudan a los usuarios que buscan un recurso específico.

[!DNL AEM Forms], de forma predeterminada, ofrece un conjunto definido de metadatos para cada tipo de recurso. Más allá de los metadatos predeterminados, puede agregar metadatos personalizados a cada tipo de recurso. [!DNL AEM Forms] también le ofrece los medios adecuados para crear, administrar e intercambiar todos estos metadatos de forma eficaz en sus formularios.

<!-- If you are a developer or a site owner, you can customize Forms Portal, the end-user interface for [!DNL AEM Forms] to reflect the metadata you are using in your organization. For more information abouts Forms Portal, see [Introduction to publishing forms on a portal](introduction-publishing-forms.md). -->

## Metadatos en [!DNL AEM Forms] {#metadata-in-aem-forms}

En [!DNL AEM Forms], la lista de propiedades de metadatos asociadas a un recurso depende de su tipo. Además, si añade cualquier propiedad de metadatos personalizada, se añade a todos los recursos del tipo en el que se añadieron los metadatos personalizados.

### Tipos de recursos {#asset-types}

Los siguientes tipos de recursos son compatibles con [!DNL AEM Forms]:

* Plantillas de formulario (formularios XFA)
* Formularios PDF
* Documento (PDF planos)
* Formularios adaptables
* Modelo de datos de formularios
* XFS

#### Amplia lista de metadatos {#extensive-list-of-metadata}

A continuación se ofrece una amplia lista de propiedades de metadatos compatibles con [!DNL AEM Forms]:

<table>
 <tbody> 
  <tr> 
   <td><strong>Nombre de la propiedad</strong></td> 
   <td><strong>Tipo de recurso</strong></td> 
   <td><strong>Descripción</strong><br /> </td> 
  </tr> 
  <tr> 
   <td>Título</td> 
   <td>Todos excepto el recurso</td> 
   <td>Nombre para mostrar del recurso.<br /> </td> 
  </tr> 
  <tr> 
   <td>Descripción</td> 
   <td>Todos excepto el recurso</td> 
   <td>Descripción del recurso. El usuario puede especificar este valor.<br /> </td> 
  </tr> 
  <tr> 
   <td>Tipo</td> 
   <td>Todos</td> 
   <td><p>Un valor de solo lectura que especifica el tipo de recurso. Puede tener uno de los siguientes valores:</p> 
    <ul> 
     <li>Plantilla de formulario</li> 
     <li>Formulario PDF, formulario PDF (acróformulario) o formulario PDF (firmado)</li> 
     <li>Documento, documento (firmado)</li> 
     <li>Formulario adaptable</li> 
     <li>Modelo de datos de formulario</li>
     <li>Recurso</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Creado</td> 
   <td>Todos</td> 
   <td>Un valor de solo lectura que especifica la hora de creación del recurso.</td> 
  </tr> 
  <tr> 
   <td>Fecha de última modificación</td> 
   <td>Todos</td> 
   <td>Un valor de solo lectura que especifica la hora en la que se modificó el recurso por última vez.</td> 
  </tr> 
  <tr> 
   <td>Autor</td> 
   <td>Todos excepto el recurso</td> 
   <td><p>Un valor de solo lectura que se calcula automáticamente según el tipo de formulario.</p> 
    <ul> 
     <li>PDF/Plantilla de formulario/Documento: recuperado del archivo binario cargado.</li> 
     <li>Formulario adaptable: Usuario que ha iniciado sesión en el momento de la creación del formulario.</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Estado</td> 
   <td>Todos excepto el recurso</td> 
   <td><p> Un valor de solo lectura que define uno de los siguientes estados de un formulario:</p> 
    <ul> 
     <li>Sin valor: Si un formulario nunca se ha publicado.</li> 
     <li>Publicado: Cuando se publica un formulario.</li> 
     <li>Modificado: Cuando se modifica un formulario después de publicarse una vez.</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Fecha de última publicación</td> 
   <td>Todos excepto el recurso</td> 
   <td>Un valor de solo lectura que especifica la hora en que se publicó el formulario por última vez.</td> 
  </tr> 
  <tr> 
   <td>Tiempo de actividad/inactividad de la publicación</td> 
   <td>Todos excepto el recurso</td> 
   <td><p>Hora a la que está programado que el formulario se publique/se cancele su publicación automáticamente. El usuario establece este valor al editar los metadatos.</p> 
    <ul> 
     <li>El tiempo de actividad/inactividad de la publicación debe superar la fecha actual. </li> 
     <li>El tiempo de inactividad de la publicación debe ser posterior al tiempo de actividad. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>URL de envío</td> 
   <td><p>Plantilla de formulario</p> <p>Formulario PDF</p> </td> 
   <td><p>Para configurar una dirección URL especificada por el usuario para enviar datos de formulario a un servlet.</p> <p>La URL de envío se puede configurar utilizando cualquiera de los siguientes métodos, enumerados por orden de prioridad:</p> 
    <ul> 
     <li>Especifique una URL de envío directamente en una plantilla de formulario mediante el botón Enviar HTTP al crear un formulario XFA en AEM Forms Designer.</li> 
     <li>En la interfaz de usuario de AEM Forms, seleccione un formulario y especifique una URL de envío al editar las propiedades de los metadatos.</li> 
     <!-- <li>In Forms Portal, edit the Search &amp; Lister component and specify a submit URL under the Form Link tab.</li> -->
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Perfil de procesamiento HTML</td> 
   <td>Plantilla de formulario</td> 
   <td>El perfil de procesamiento HTML utilizado al procesar una plantilla de formulario en formato HTML.</td> 
  </tr> 
  <tr> 
   <td>Formato de procesamiento</td> 
   <td><p>Plantilla de formulario</p> <p>Formulario adaptable</p> </td> 
   <td><p>Esta opción permite al usuario especificar el formato de procesamiento del formulario cuando se publican los formularios:</p> 
    <ul> 
     <li>HTML</li> 
     <li>PDF</li> 
     <li>Ambas</li> 
    </ul> <p>Esta opción se utiliza para restringir el formato de procesamiento de los formularios solo en el Portal de Forms donde sean visibles para el usuario final.</p> </td> 
  </tr> 
  <tr> 
   <td>Etiquetas</td> 
   <td>Todos excepto el recurso</td> 
   <td>Etiquetas asociadas al formulario para facilitar una búsqueda rápida y sencilla.</td> 
  </tr> 
  <tr> 
   <td>Referencias</td> 
   <td><p>Formulario adaptable</p> <p>Plantilla de formulario</p> <p>Recurso</p> </td> 
   <td><p>Lista de recursos (otros formularios o recursos) con los que está relacionado este formulario. Estos recursos pueden clasificarse en las dos categorías siguientes:</p> 
    <ul> 
     <li>Hace referencia: Recursos a los que hace referencia el formulario actual.</li> 
     <li>Le hacen referencia: Recursos que hacen referencia al recurso actual.</li> 
    </ul> <p>Estos recursos se muestran como enlaces y se puede acceder a sus metadatos directamente haciendo clic en ellos.<br /> </p> </td> 
  </tr> 
  <tr> 
   <td>Selección del modelo de formulario (XDP/XSD)</td> 
   <td>Formulario adaptable</td> 
   <td><p>Especifica qué modelo de formulario se utiliza durante la creación del formulario adaptable. Esta propiedad puede tener los siguientes valores:</p> 
    <ul> 
      <li>Modelo de datos de formulario </li>
      <li>Esquema: Un XML del esquema JSON</li>
     <!-- <li>Form template: A form template is selected from the ones existing in the repository. This value can be updated.</li> 
     <li>XML schema: An XSD file is uploaded. This value can be updated.</li> -->
     <li>Ninguno</li> 
    </ul> 
    <div>
      Un modelo de formulario una vez seleccionado puede actualizarse, pero no quitarse. 
    </div> </td> 
  </tr> 
 </tbody> 
</table>

## Ver metadatos de formulario {#view-form-metadata}

Los recursos tienen valores de propiedad existentes, que se pueden ver en modo de solo lectura. Estos metadatos se originan cuando se carga o crea el formulario.

1. Vaya a la ubicación del recurso cuyos metadatos desea ver.

1. Abra la página de propiedades mediante uno de los métodos siguientes:

   * Haga clic en el icono **[!UICONTROL Propiedades]** ![Propiedades](assets/Smock_Info_18_N.svg) en Acciones rápidas.

     >[!NOTE]
     >
     >Las Acciones rápidas son los elementos de acción que se muestran sobre una miniatura al pasar el ratón por encima.

   * Seleccione el formulario y haga clic en el icono **[!UICONTROL Propiedades]** ![Propiedades](assets/Smock_Info_18_N.svg) que aparece en la barra de herramientas.
   * Vaya a la página de detalles del formulario haciendo clic en la miniatura del formulario cuando no esté en el modo de selección. A continuación, haga clic en el icono del ojo ![Propiedades](assets/Smock_Info_18_N.svg) en la parte superior derecha y, luego, haga clic en Propiedades en la lista debajo.

1. La página de propiedades que se abre muestra un esquema que contiene solo las propiedades de metadatos que contienen algún valor.

   <!-- The properties page has a toolbar containing two action icons:

    * Edit: ![Edit](assets/Smock_Edit_18_N.svg) Edit the metadata property values
    * View: ![aem6forms_eye_viewon](assets/aem6forms_eye_viewon.png) Navigate to the form details page, which opens the form in the preview mode. -->

   La parte de contenido se divide en dos partes:

   * El panel izquierdo contiene una miniatura del formulario
   * El panel derecho contiene propiedades de metadatos en modo de solo lectura, distribuidas entre varias pestañas.

## Añadir/actualizar valores de metadatos de formulario {#add-update-form-metadata-values}

Puede editar el valor de las propiedades de metadatos existentes o agregar nuevos valores a un campo de propiedad de metadatos existente (por ejemplo, cuando un campo de metadatos está en blanco).

<!-- ### Update metadata property values {#update-metadata-property-values}

1. Follow the steps mentioned in the previous section to open the properties page where existing metadata of the selected form can be viewed.  

1. From the toolbar, click the Edit icon ![Edit](assets/Smock_Edit_18_N.svg) to change the mode of the page from read-only to read/write.  

1. The properties page that opens holds a schema that contains a mix of editable input fields and static text.  

1. The properties displayed in static text are the ones that you cannot edit.  

1. You can navigate to other tabs to find input fields for metadata properties placed under them.

   This page has a toolbar containing two action icons different from those in view mode:

    * Cancel: ![aem6forms_close](assets/aem6forms_close.svg_w24.png) Cancel any changes made to metadata property values so far
    * Done: ![aem6forms_check](assets/aem6forms_check.png) Save all the changes made to metadata property values so far

   Both these actions direct the user back to read-only mode of the properties page containing the updated values.-->

### Actualizar la miniatura del formulario {#update-the-form-thumbnail}

El panel izquierdo de la página de propiedades muestra la miniatura del formulario. De forma predeterminada, la miniatura que se muestra es la que se genera en el momento de crear el formulario (formulario adaptable) o en el momento de cargar el formulario.

Para todos los tipos de formulario, tiene la opción de cargar una imagen haciendo clic en **[!UICONTROL Cargar imagen]** y buscando un archivo de imagen desde el directorio local. La imagen seleccionada se utiliza como miniatura en lugar de la predeterminada.

Para los formularios adaptables, se ofrece una funcionalidad adicional, que permite al usuario generar una miniatura como instantánea de la vista previa actual del formulario adaptable. Como [!DNL AEM Forms] también es compatible con la creación de formularios adaptables, la vista previa del formulario adaptable puede cambiar cada vez que cambia el formulario adaptable. Esta funcionalidad para generar una miniatura le ayuda a obtener una nueva miniatura para el formulario adaptable en función del estado de vista previa actual. Haga clic en **[!UICONTROL Generar vista previa]** para llevar a cabo esta acción.

>[!NOTE]
>
>* Utilice una imagen cuadrada para la miniatura. Si utiliza una imagen que no sea cuadrada y ve la miniatura en la vista de lista, la miniatura aparece recortada.
>* Una vez que se carga o genera una nueva imagen, la miniatura se reemplaza por esta imagen y no se puede restablecer a la imagen anterior.
>

## Añadir metadatos personalizados {#add-custom-metadata}

Aparte de los metadatos predeterminados, [!DNL AEM Forms] es compatible con nuevos metadatos personalizados.

Se ofrece una herramienta (Editor de esquemas de metadatos) para definir el esquema para el diseño de metadatos; es decir, el diseño de lo que aparece en la página **[!UICONTROL Propiedades]** de un formulario. El Editor de esquemas de metadatos le permite agregar o modificar un esquema personalizado para sus recursos.

[!DNL AEM Forms] expone los esquemas de metadatos de los tipos de formularios compatibles en esta herramienta. De este modo, puede acceder a estos esquemas y utilizar la funcionalidad que se ofrece en el Editor de esquemas de metadatos para agregar propiedades personalizadas.

### Ir al Editor de esquemas de metadatos {#navigate-the-metadata-schema-editor}

1. Vaya a **[!UICONTROL Herramientas > Recursos > Esquemas de metadatos]**.

1. Haga clic en **[!UICONTROL formularios]**, en los formularios de esquema enumerados.

1. En la lista que se abre, haga clic en el tipo de recurso para el que desea agregar metadatos personalizados.

   >[!NOTE]
   >
   >Estos esquemas contienen propiedades de metadatos que se aportan de forma predeterminada y no se deben modificar/editar (seleccionando la casilla de verificación y haciendo clic en Editar en la barra de herramientas) para evitar problemas de funcionamiento.

1. Cualquier tipo de recurso en el que se haga clic abre una lista que contiene la opción `extendedmetadata`. Edite este esquema.

1. Seleccione la casilla de verificación que aparece junto a `extendedmetadata` y, a continuación, haga clic en el icono Editar ![Editar](assets/Smock_Edit_18_N.svg), que aparece en la barra de herramientas.

1. [!DNL AEM Forms] abre el Editor de esquemas de metadatos/creador de formularios del tipo de recurso seleccionado (en este caso, formulario adaptable).

   Editor de metadatos

   1. El panel izquierdo contiene secciones con pestañas en las que se colocan los campos y el panel derecho muestra todos los componentes de la interfaz de usuario disponibles y las propiedades del campo seleccionado en el panel izquierdo.

   1. La sección bloqueada no se puede editar y contiene campos para todas las propiedades de metadatos que se ofrecen de forma predeterminada.

   1. Para agregar pestañas adicionales, haga clic en el símbolo +.

   1. Puede agregar un campo personalizado del tipo deseado arrastrando el componente de campo desde la sección **[!UICONTROL Crear formulario]**, en la página de esquema.
   1. Las especificaciones para este campo se pueden indicar en la sección **[!UICONTROL Configuración]** después de hacer clic en el campo.

### Añadir propiedad de metadatos personalizada en el editor de esquemas {#add-custom-metadata-property-in-schema-editor}

1. Vaya a la pestaña (existente o nueva) donde desee agregar la propiedad personalizada.

1. Arrastre un componente del tipo deseado desde la sección **[!UICONTROL Crear formulario]** al panel izquierdo y colóquelo en una ubicación conveniente.

   >[!NOTE]
   >
   >No puede mover las secciones bloqueadas, pero puede colocar su componente en cualquiera de los espacios vacíos.

1. Haga clic en un componente que acabe de arrastrar. En la pestaña Configuración que se abre en el panel derecho, rellene los campos siguientes:

   1. Especifique una Etiqueta de campo para utilizarla como nombre para mostrar encima del campo colocado en el esquema (por ejemplo: Departamento)
   1. En el campo Asignar a propiedad, puede ver un valor rellenado previamente **&#39;./jcr:content/metadata/default&#39;**. Cambie el &#39;**predeterminado**&#39; a un nombre de propiedad deseado, que se utiliza para almacenar la propiedad en el repositorio crx (por ejemplo: &#39;./jcr:content/metadata/department&#39;)

      >[!NOTE]
      >
      >No cambie el prefijo &#39;./jcr:content/metadata/&#39;, ya que define la ruta donde se almacena la propiedad.
      >
      >Además, el nombre de la propiedad debe ser único para evitar escribir valores para dos o más propiedades en la misma ubicación del repositorio. Por lo tanto, se recomienda cambiar el valor “default”.

   1. Rellene otras configuraciones según sea necesario. Por ejemplo: seleccione la opción Obligatorio si desea que el campo sea obligatorio.
   1. Para eliminar un campo que haya añadido, seleccione el campo y, a continuación, haga clic en el icono Eliminar ![Eliminar](assets/Smock_Delete_18_N.svg).

1. Si es necesario, siga los pasos 1-3 para agregar otra propiedad.
1. Haga clic en **[!UICONTROL Guardar]** después de realizar todos los cambios.

   Ha añadido correctamente una propiedad de metadatos personalizada.

Todos los formularios adaptables de [!DNL AEM Forms] ahora contienen esta propiedad de metadatos adicional. Puede editarlo desde la página de propiedades.
