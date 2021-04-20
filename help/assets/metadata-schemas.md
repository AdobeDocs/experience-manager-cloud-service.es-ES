---
title: Esquemas de metadatos
description: El esquema de metadatos define el diseño de la página de propiedades y las propiedades de metadatos que se muestran para los recursos. Obtenga información sobre cómo crear un esquema de metadatos personalizado, editar un esquema de metadatos y cómo aplicar un esquema de metadatos a los recursos.
contentOwner: AG
feature: Metadata
role: Business Practitioner,Administrator
translation-type: tm+mt
source-git-commit: 8093f6cec446223af58515fd8c91afa5940f9402
workflow-type: tm+mt
source-wordcount: '2513'
ht-degree: 15%

---


# Esquemas de metadatos {#metadata-schemas}

En Adobe Experience Manager (AEM) Assets, un esquema de metadatos define el diseño de la página de propiedades y las propiedades de metadatos que se muestran para los recursos que utilizan el esquema en particular. Las propiedades de metadatos incluyen título, descripción, tipos MIME, etiquetas, etc.

Puede utilizar el editor de Forms de esquemas de metadatos para modificar esquemas existentes o añadir esquemas de metadatos personalizados.

1. Para ver la página de propiedades de un recurso, toque o haga clic en el icono **[!UICONTROL Ver propiedades]** de Acciones rápidas en el mosaico del recurso en la vista de tarjeta. Como alternativa, seleccione el recurso en la interfaz de usuario y, a continuación, toque o haga clic en el icono **[!UICONTROL Propiedades]** de la barra de herramientas.
1. Edite varias propiedades de metadatos en las distintas pestañas. Sin embargo, no puede modificar el tipo de recurso en la página de propiedades.
Para modificar el tipo MIME de un recurso, utilice un formulario de esquema de metadatos personalizado o modifique un formulario existente. Consulte [Edición del esquema de metadatos Forms](#edit-metadata-schema-forms) para obtener más información. Si modifica el esquema de metadatos para un determinado tipo MIME, se modifican el diseño de la página de propiedades de los recursos con el tipo MIME actual y todos los subtipos de recursos. Por ejemplo, modificar un esquema jpeg en `default/image` solo modifica el diseño de metadatos (propiedades de recursos) para los recursos con tipo MIME `image/jpeg`. Sin embargo, si edita el esquema predeterminado, los cambios modificarán el diseño de metadatos para todos los tipos de recursos.

1. Para ver una lista de formularios/plantillas, haga clic en el logotipo de AEM y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de metadatos]**.
AEM proporciona las siguientes plantillas listas para usar:

   * **predeterminado**: Formulario de esquema de metadatos base para los recursos.

   Los siguientes formularios secundarios heredan las propiedades del formulario predeterminado:
i. **imagen**: Formulario de esquema para recursos con el tipo MIME &quot;image&quot;, por ejemplo, `image/jpeg`, `image/png`, etc.
El formulario &quot;imagen&quot; tiene las siguientes plantillas de formulario secundarias:
a. **jpeg**: Formulario de esquema para recursos con subtipo `jpeg`.
b. **tiff**: Formulario de esquema para los recursos con subtipo `tiff`.

   ii. **aplicación**: Formulario de esquema para recursos con tipo MIME  `application`, por ejemplo  `application/pdf`,  `application/zip`, etc.
a. **pdf**: Formulario de esquema para recursos con subtipo `pdf`.

   iii. **vídeo**: Formulario de esquema para recursos con tipo MIME  `video`, como  `video/avi`,  `video/mp4`, etc.

   * **colección**: Formulario de esquema para colecciones.
   * **contentfragment:** Formulario de esquema para fragmentos de contenido.


>[!NOTE]
>
>Para ver los formularios secundarios de un formulario de esquema, toque o haga clic en el nombre del formulario de esquema.

## Agregar un formulario de esquema de metadatos {#add-a-metadata-schema-form}

1. Para agregar una plantilla personalizada a la lista, haga clic en **[!UICONTROL Crear]** en la barra de herramientas.

   >[!NOTE]
   >
   >Las plantillas modificadas tienen un icono de bloqueo antes que ellas. Si personaliza cualquiera de las plantillas, desaparece el icono de bloqueo antes de la plantilla.

1. En el cuadro de diálogo, introduzca el título del formulario Esquema y, a continuación, haga clic en **[!UICONTROL Crear]** para completar el proceso de creación del formulario.

## Editar formularios de esquema de metadatos {#edit-metadata-schema-forms}

Puede editar un formulario de esquema de metadatos nuevo o existente. El formulario de esquema de metadatos incluye lo siguiente:

* Pestañas
* Elementos de formulario dentro de las pestañas.

Puede asignar/configurar estos elementos de formulario a un campo dentro de un nodo de metadatos en el repositorio CRX.

Puede agregar nuevas fichas o elementos de formulario al formulario de esquema de metadatos. Las fichas y los elementos de formulario derivados del elemento principal están en estado bloqueado. No se pueden modificar en el nivel secundario.

1. En la página Formularios de esquema, active la casilla de verificación situada antes de un formulario y, a continuación, haga clic en el **icono Editar** de la barra de herramientas.
1. En la página **[!UICONTROL Editor de esquemas de metadatos]**, personalice la página de propiedades del recurso arrastrando uno o varios componentes de la lista de tipos de componentes de la pestaña **[!UICONTROL Generar formulario]** a **[!UICONTROL Básico]**.
1. Para configurar un componente, selecciónelo y modifique sus propiedades en la pestaña **Settings**.

### Componentes dentro de la ficha Generar formulario {#components-within-the-build-form-tab}

La ficha **[!UICONTROL Generar formulario]** enumera los elementos de formulario que utiliza en el formulario de esquema. La pestaña **[!UICONTROL Settings]** proporciona los atributos de cada elemento que seleccione en la ficha **[!UICONTROL Generar formulario]**. La tabla siguiente muestra los elementos de formulario disponibles en la ficha **[!UICONTROL Generar formulario]**:

<table>
 <tbody>
  <tr>
   <td><strong>Nombre del componente</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>Sección de encabezado</td>
   <td>Añada un encabezado de sección para ver una lista de componentes comunes.</td>
  </tr>
  <tr>
   <td>Texto de una sola línea</td>
   <td>Agregue una propiedad de texto de una sola línea. Se almacena como una cadena.</td>
  </tr>
  <tr>
   <td>Texto con varios valores</td>
   <td>Agregue una propiedad de texto de varios valores. Se almacena como una matriz de cadenas.</td>
  </tr>
  <tr>
   <td>Número</td>
   <td>Añada un componente numérico.</td>
  </tr>
  <tr>
   <td>Fecha</td>
   <td>Añada un componente de fecha.</td>
  </tr>
  <tr>
   <td>Lista desplegable</td>
   <td>Añada una lista desplegable.</td>
  </tr>
  <tr>
   <td>Etiquetas estándar</td>
   <td>Añadir una etiqueta. </td>
  </tr>
  <tr>
   <td>Etiquetas inteligentes</td>
   <td>Agregue a las capacidades de búsqueda agregando automáticamente etiquetas de metadatos.<br /> </td>
  </tr>
  <tr>
   <td>Campo oculto</td>
   <td>Añada un campo oculto. Se envía como parámetro de POST cuando se guarda el recurso.</td>
  </tr>
  <tr>
   <td>Recurso al que se hace referencia en</td>
   <td>Añada este componente para ver la lista de recursos a los que hace referencia el recurso.</td>
  </tr>
  <tr>
   <td>Referencia de recursos</td>
   <td>Agregar para mostrar una lista de recursos que hacen referencia al recurso.</td>
  </tr>
  <tr>
   <td>Referencias de productos</td>
   <td>Agregar para mostrar la lista de productos vinculados al recurso.</td>
  </tr>
  <tr>
   <td>Clasificación del recurso</td>
   <td>Añada para mostrar las opciones de clasificación del recurso.</td>
  </tr>
  <tr>
   <td>Metadatos de contexto</td>
   <td>Añadir para controlar la visualización de otras pestañas de metadatos en la página de propiedades de los recursos.</td>
  </tr>
 </tbody>
</table>

#### Editar el componente de metadatos {#edit-the-metadata-component}

Para editar las propiedades de un componente de metadatos en el formulario, haga clic en el componente y edite todas o un subconjunto de las siguientes propiedades en la pestaña **[!UICONTROL Settings]**.

**Etiqueta** de campo: Nombre de la propiedad de metadatos que se muestra en la página de propiedades del recurso.

**Asignar a propiedad**: Esta propiedad especifica la ruta/nombre relativo al nodo de recurso donde se guarda en el repositorio CRX. Comienza con `./` porque indica que la ruta está bajo el nodo del recurso.

Los siguientes son los valores válidos para esta propiedad:

* . `/jcr:content/metadata/dc:title`: Almacena el valor en el nodo de metadatos del recurso como propiedad `dc:title`.

* . `/jcr:created`: Muestra la propiedad jcr en el nodo del recurso. Si configura estas propiedades en propiedades de vista, le recomendamos que las marque como Deshabilitar edición, ya que están protegidas. De lo contrario, se produce el fallo “Error al modificar los recursos” al guardar las propiedades del recurso.

Para asegurarse de que el componente se muestra correctamente en el formulario de esquema de metadatos, la ruta de la propiedad no debe incluir espacios.

**Marcador de posición**: Utilice esta propiedad para especificar el texto del marcador de posición correspondiente a la propiedad metadata.

**Requerido**: Utilice esta propiedad para marcar una propiedad de metadatos como obligatoria en la página de propiedades.

**Desactivar edición**: Utilice esta propiedad para hacer que una propiedad de metadatos no se pueda editar en la página Propiedades.

**Mostrar Campo Vacío En Solo** Lectura: Marque esta propiedad para mostrar una propiedad de metadatos en la página de propiedades aunque no tenga ningún valor. De forma predeterminada, cuando una propiedad de metadatos no tiene ningún valor, no aparece en la página de propiedades.

**Mostrar lista ordenada**: Utilice esta propiedad para mostrar una lista ordenada de opciones

**Opciones**: Utilice esta propiedad para especificar opciones en una lista

**Descripción** : Utilice esta propiedad para añadir una breve descripción para el componente de metadatos.

**Clase**: Clase de objeto a la que está asociada la propiedad.

**Eliminar**: Haga clic en para eliminar un componente del formulario de esquema.

>[!NOTE]
>
>El componente Campo oculto no incluye estos atributos. En su lugar, incluye propiedades como Nombre, Valor, Etiqueta de campo y Descripción. Los valores del componente Campo oculto se envían como parámetro de POST cada vez que se guarda el recurso. No se guarda como metadatos para el recurso.

Si selecciona la opción **[!UICONTROL Obligatorio]**, puede buscar recursos que no tengan metadatos obligatorios. En el panel **[!UICONTROL Filtros]**, expanda el predicado **[!UICONTROL Validación de metadatos]** y seleccione la opción **[!UICONTROL No válido]**. Los resultados de la búsqueda muestran los recursos que carecen de metadatos obligatorios configurados a través del formulario de esquema.

Si agrega el componente Metadatos contextuales a cualquier ficha de cualquier formulario de esquema, el componente aparece como una lista en la página de propiedades de los recursos a los que se aplica el esquema en particular. La lista incluye todas las demás fichas excepto la ficha a la que se aplicó el componente Metadatos contextuales . Actualmente, esta función proporciona funcionalidad básica para controlar la visualización de metadatos en función del contexto.

Para incluir cualquier pestaña en la página de propiedades además de la pestaña donde se aplica el componente Metadatos contextuales, seleccione la pestaña de la lista. La pestaña se agrega a la página de propiedades.

### Especificar propiedades en el archivo JSON {#specify-properties-in-json-file}

En lugar de especificar propiedades para las opciones de la pestaña **[!UICONTROL Configuración]**, puede definir las opciones de un archivo JSON especificando los pares de clave-valor correspondientes. Especifique la ruta del archivo JSON en el campo **[!UICONTROL Ruta de JSON]**.

#### Agregar y eliminar una pestaña del formulario de esquema {#add-delete-a-tab-in-the-schema-form}

El editor de esquemas permite agregar o eliminar una pestaña. El formulario de esquema predeterminado incluye las pestañas **[!UICONTROL Básico]**, **[!UICONTROL Avanzado]**, **[!UICONTROL IPTC]** y **[!UICONTROL Extensión IPTC]** de forma predeterminada.

Haga clic en `+` para agregar una nueva pestaña en un formulario de esquema. De forma predeterminada, la nueva pestaña tiene el nombre `Unnamed-1`. Puede modificar el nombre desde la pestaña **[!UICONTROL Settings]**. Haga clic en `X` para eliminar una pestaña.

## Eliminación de formularios de esquema de metadatos {#deleting-metadata-schema-forms}

AEM permite eliminar solo los formularios de esquema personalizados. No permite eliminar los formularios o plantillas de esquema predeterminados. Sin embargo, puede eliminar cualquier cambio personalizado en estos formularios.

Para eliminar un formulario, seleccione un formulario y haga clic en el icono de eliminación.

>[!NOTE]
>
>Después de eliminar los cambios personalizados en un formulario predeterminado, el icono de bloqueo vuelve a aparecer antes de que aparezca en la interfaz del esquema de metadatos para indicar que el formulario ha vuelto a su estado predeterminado.

>[!NOTE]
>
>No se pueden eliminar los formularios de esquema de metadatos predefinidos en AEM Assets.

## Formularios de esquema para tipos MIME {#schema-forms-for-mime-types}

AEM Assets proporciona formularios predeterminados para varios tipos de MIME predeterminados. Sin embargo, puede agregar formularios personalizados para recursos de varios tipos de MIME.

### Adición de nuevos formularios para tipos MIME {#adding-new-forms-for-mime-types}

Cree un nuevo formulario bajo el tipo de formulario correspondiente. Por ejemplo, para agregar una nueva plantilla para el subtipo **imagen/png**, cree el formulario en los formularios de “imagen”. El título del formulario de esquema es el nombre del subtipo. En este caso, el título es “png.**”**

#### Uso de una plantilla de esquema existente para varios tipos MIME {#using-an-existing-schema-template-for-various-mime-types}

Puede utilizar una plantilla existente para un tipo MIME diferente. Por ejemplo, utilice el formulario `image/jpeg` para los recursos de tipo MIME `image/png`.

En este caso, cree un nuevo nodo en `/etc/dam/metadataeditor/mimetypemappings` en el repositorio CRX. Especifique un nombre para el nodo y defina las siguientes propiedades:

| **Nombre** | **Descripción** | **Tipo** | **Value** |
|---|---|---|---|
| `exposedmimetype` | Nombre del formulario existente a asignar | Cadena | `image/jpeg` |
| `mimetypes` | Lista de tipos MIME que utilizan el formulario definido en el atributo `exposedmimetype` | Cadena | `image/png` |

AEM Assets asigna los siguientes tipos MIME y formularios de esquema:

| Formulario de esquema | Tipos MIME |
|---|---|
| image/jpeg | image/pjpeg |
| image/tiff | image/x-tiff |
| application/pdf | application/postscript |
| application/x-ImageSet | Multipart/Related; type=application/x-ImageSet |
| application/x-SpinSet | Multipart/Related; type=application/x-SpinSet |
| application/x-MixedMediaSet | Multipart/Related; type=application/x-MixedMediaSet |
| video/quicktime | video/x-quicktime |
| video/mpeg4 | video/mp4 |
| video/avi | video/avi, video/msvideo, video/x-msvideo |
| video/wmv | video/x-ms-wmv |
| video/flv | video/x-flv |

## Concesión de acceso a esquemas de metadatos {#granting-access-to-metadata-schemas}

La función Esquema de metadatos solo está disponible para los administradores. Sin embargo, los administradores pueden proporcionar acceso a los usuarios que no sean administradores modificando algunos permisos. Los usuarios que no sean administradores deben tener permisos de creación, modificación y eliminación en la carpeta `/conf`.

## Aplicación de metadatos específicos de carpetas {#applying-folder-specific-metadata}

AEM Assets permite definir una variante de un esquema de metadatos y aplicarla a una carpeta específica.

Por ejemplo, puede definir una variante del esquema de metadatos predeterminado y aplicarla a una carpeta. Cuando se aplica el esquema modificado, anula el esquema de metadatos predeterminado original que se aplica a los recursos de la carpeta.

Solo los recursos cargados en la carpeta a la que se aplica este esquema se ajustan a los metadatos modificados definidos en el esquema de metadatos de la variante.

Los recursos de otras carpetas donde se aplica el esquema original siguen ajustándose a los metadatos definidos en el esquema original.

La herencia de metadatos por recursos se basa en el esquema que se aplica a la carpeta de primer nivel de la jerarquía. En otras palabras, si una carpeta no contiene subcarpetas, los recursos de la carpeta heredan los metadatos del esquema aplicado a la carpeta.

Si la carpeta tiene una subcarpeta, los recursos de la subcarpeta heredan los metadatos del esquema aplicado en el nivel de subcarpeta si se aplica un esquema diferente en el nivel de subcarpeta. Sin embargo, si no se aplica ningún esquema o el mismo esquema en el nivel de subcarpeta, los recursos de subcarpeta heredan los metadatos del esquema aplicado en el nivel de carpeta principal.

1. Haga clic en el logotipo de AEM y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de metadatos]**. Se muestra la página **[!UICONTROL Formularios de esquema de metadatos]**.
1. Seleccione la casilla de verificación situada antes de un formulario, por ejemplo el formulario de metadatos predeterminado, y pulse o haga clic en el icono de copia y guárdelo como un formulario personalizado. Especifique un nombre personalizado para el formulario, por ejemplo `my_default`. También puede crear un formulario personalizado.

1. En la página **[!UICONTROL Metadata Schema Forms]**, seleccione el formulario `my_default` y, a continuación, haga clic en el icono **[!UICONTROL Edit]**.
1. En la página **[!UICONTROL Editor de esquemas de metadatos]**, agregue un campo de texto al formulario de esquema. Por ejemplo, agregue un campo con la etiqueta **[!UICONTROL Category]**.
1. Haga clic en **[!UICONTROL Guardar]**. El formulario modificado se muestra en la página **[!UICONTROL Forms]** del esquema de metadatos.
1. Pulse o haga clic **[!UICONTROL Aplicar a las carpetas]** en la barra de herramientas para aplicar los metadatos personalizados a una carpeta.
1. Seleccione la carpeta en la que desea aplicar el esquema modificado y, a continuación, pulse o haga clic en **[!UICONTROL Aplicar]**.
1. Si se ha aplicado el otro esquema de metadatos a la carpeta, aparece un mensaje en el que se advierte que está a punto de sobrescribir el esquema de metadatos existente. Haga clic en **Sobrescribir**.
1. Haga clic en **OK** para cerrar el mensaje de éxito.
1. Vaya a la carpeta a la que aplicó el esquema de metadatos modificado.

## Definición de metadatos obligatorios {#defining-mandatory-metadata}

Puede definir campos obligatorios a nivel de carpeta, que se aplican a los recursos que se cargan en la carpeta. Si carga recursos con metadatos que faltan para los campos obligatorios definidos anteriormente, en la vista Tarjeta aparecerá una indicación visual de los metadatos que faltan en los recursos.

>[!NOTE]
>
>Un campo de metadatos se puede definir como obligatorio en función del valor de otro campo. En la vista Tarjetas, AEM no muestra el mensaje de advertencia sobre la falta de metadatos para estos campos de metadatos obligatorios.

1. Haga clic en el logotipo de AEM y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de metadatos]**. Se muestra la página **[!UICONTROL Formularios de esquema de metadatos]**.
1. Guarde el formulario de metadatos predeterminado como un formulario personalizado. Por ejemplo, guárdelo como `my_default`.
1. Edite el formulario personalizado. Añada un campo obligatorio. Por ejemplo, agregue un campo **[!UICONTROL Category]** y haga que el campo sea obligatorio.
1. Haga clic en **[!UICONTROL Guardar]**. El formulario modificado se muestra en la página **[!UICONTROL Forms]** del esquema de metadatos. Seleccione el formulario y, a continuación, pulse o haga clic en **[!UICONTROL Aplicar a las carpetas]** en la barra de herramientas para aplicar los metadatos personalizados a una carpeta.
1. Vaya a la carpeta y cargue algunos recursos con metadatos que faltan para el campo obligatorio que ha agregado al formulario personalizado. Se muestra un mensaje para los metadatos que faltan para el campo obligatorio en la vista de tarjeta del recurso.
1. (Opcional) Acceda a `https://[server]:[port]/system/console/components/`. Configure y habilite el componente `com.day.cq.dam.core.impl.MissingMetadataNotificationJob` que está deshabilitado de forma predeterminada. Establezca una frecuencia con la que AEM compruebe la validez de los metadatos en los recursos.

   Esta configuración agrega una propiedad `hasValidMetadata` a `jcr:content` de recursos. Con esta propiedad, AEM filtrar los resultados en una búsqueda.

   >[!NOTE]
   >
   >Si se agrega un recurso después de la comprobación programada, el recurso no se marca con `hasValidMetadata` hasta la siguiente comprobación programada. Los recursos no aparecen en los resultados de búsqueda intermedios.

   >[!CAUTION]
   >
   >Las comprobaciones de validación de metadatos requieren muchos recursos y pueden afectar al rendimiento del sistema. Programe las comprobaciones según corresponda. Si el servidor no puede lidiar con la carga, intente desactivar este trabajo
