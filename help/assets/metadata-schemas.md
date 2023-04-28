---
title: Los esquemas de metadatos definen el diseño de la página de propiedades de metadatos
description: El esquema de metadatos define el diseño de la página de propiedades y las propiedades de metadatos que se muestran para los recursos. Obtenga información sobre cómo crear un esquema de metadatos personalizado, editar un esquema de metadatos y aplicar un esquema de metadatos a los recursos.
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: 9e94afeb-1c54-4653-bf52-b0910c0cb6c1
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '2620'
ht-degree: 9%

---

# Esquemas de metadatos {#metadata-schemas}

Las organizaciones cuentan con un modelo de metadatos que mejora la detección de recursos, el uso, la interoperabilidad, etc. La aplicación de metadatos correcta es sacrosanta para mantener los flujos de trabajo y procesos basados en metadatos. Para adherirse a la estrategia y los estándares de metadatos de toda la organización, puede utilizar esquemas de metadatos que ayuden a los usuarios de DAM a alinearse. [!DNL Adobe Experience Manager] permite crear, mantener y aplicar esquemas de metadatos con métodos sencillos y flexibles.

En [!DNL Adobe Experience Manager Assets], los esquemas contienen campos específicos para la información específica que se va a rellenar. También contiene información de diseño para mostrar los campos de metadatos de forma sencilla. Las propiedades de metadatos incluyen título, descripción, tipos MIME, etiquetas y mucho más. Puede usar la variable [!UICONTROL Esquema de metadatos Forms] para modificar los esquemas existentes o añadir esquemas de metadatos personalizados.

Para ver y editar la página de propiedades de un recurso, siga estos pasos:

1. Haga clic en el **[!UICONTROL Ver propiedades]** en las acciones rápidas del mosaico de recursos en la vista de tarjeta. Como alternativa, seleccione un recurso y haga clic en **[!UICONTROL Propiedades]** ![ver propiedades](assets/do-not-localize/info-circle-icon.png) en la barra de herramientas.

1. Puede editar las distintas propiedades de metadatos editables en las pestañas disponibles. Sin embargo, no puede modificar el recurso [!UICONTROL Tipo] en el [!UICONTROL Básico] de la página de propiedades.

   ![Pestaña básica de Propiedades del recurso, donde no se puede cambiar el tipo de recurso](assets/asset-properties-basic-tab.png)

   *Figura: Pestaña Básico del recurso [!UICONTROL Propiedades].*

   Para modificar el tipo MIME de un recurso, utilice un formulario de esquema de metadatos personalizado o modifique un formulario existente. Consulte [Editar esquema de metadatos Forms](#edit-metadata-schema-forms) para obtener más información. Si modifica el esquema de metadatos de un tipo MIME, se modifica el diseño de página de propiedades de los recursos y todos los subtipos. Por ejemplo, modificar un esquema jpeg en `default/image` modifica únicamente el diseño de metadatos (propiedades del recurso) para los recursos con tipo MIME `image/jpeg`. Sin embargo, si edita el esquema predeterminado, los cambios modificarán el diseño de metadatos para todos los tipos de recursos.

## Formularios de esquema de metadatos {#default-metadata-schema-forms}

Para ver una lista de formularios o plantillas, consulte [!DNL Experience Manager] interfaz vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Esquemas de metadatos]**.

[!DNL Experience Manager] proporciona las siguientes plantillas de formulario de esquema de metadatos.

| Plantillas |  | Descripción |
|---|---|---|
| [!UICONTROL predeterminada] |  | Formulario de esquema de metadatos base para los recursos. |
|  | Los siguientes formularios secundarios heredan las propiedades de la variable [!UICONTROL default] formulario: |  |
|  | <ul><li>[!UICONTROL dm_video]</li></ul> | Formulario de esquema para vídeos de Dynamic Media. |
|  | <ul><li>[!UICONTROL imagen]</li></ul> | Formulario de esquema para imágenes con tipo MIME como `image/jpeg` y `image/png`. <br> La variable [!UICONTROL image] tiene las siguientes plantillas de formulario secundarias: <ul><li> [!UICONTROL jpeg]: Formulario de esquema para recursos con subtipo [!UICONTROL jpeg].</li> <li>[!UICONTROL tiff]: Formulario de esquema para los recursos con el TIFF de subtipo .</li></ul> |
|  | <ul><li>[!UICONTROL aplicación]</li></ul> | Formulario de esquema para recursos con tipo MIME como `application/pdf` y `application/zip`. <br>[!UICONTROL pdf]: Formulario de esquema para recursos con PDF de subtipo. |
|  | <ul><li>[!UICONTROL vídeo]</li></ul> | Formulario de esquema para recursos de vídeo con tipo MIME como `video/avi` y `video/mp4`. |
| [!UICONTROL colección] |  | Formulario de esquema para colecciones. |
| [!UICONTROL contentfragment] |  | Formulario de esquema para fragmentos de contenido. |
| [!UICONTROL formularios] |  | Este formulario de esquema está relacionado con [!DNL Adobe Experience Manager Forms]. |
| [!UICONTROL ugc_contentfragment] |  | Formulario de esquema para elementos de contenido generados por el usuario y recursos integrados en el Experience Manager desde medios sociales. |

>[!NOTE]
>
>Para ver los formularios secundarios de un formulario de esquema, haga clic en el nombre del formulario de esquema.

## Agregar un formulario de esquema de metadatos {#add-a-metadata-schema-form}

Para agregar un formulario de esquema de metadatos, siga estos pasos:

1. Para agregar una plantilla personalizada a la lista, haga clic en **[!UICONTROL Crear]** en la barra de herramientas.

   >[!NOTE]
   >
   >Se muestra un símbolo de bloqueo con las plantillas sin editar. Si personaliza una plantilla, no está bloqueada ![bloqueo cerrado](assets/do-not-localize/lock_closed_icon.svg).

1. En el cuadro de diálogo , proporcione el título del formulario de esquema y haga clic en **[!UICONTROL Crear]** para completar el proceso de creación del formulario.

## Edición de formularios de esquema de metadatos {#edit-metadata-schema-forms}

Puede editar un formulario de esquema de metadatos nuevo o existente. El formulario de esquema de metadatos incluye fichas y elementos de formulario en fichas. Puede asignar/configurar estos elementos de formulario a un campo dentro de un nodo de metadatos en el repositorio CRX. Puede agregar fichas o elementos de formulario al formulario de esquema de metadatos. Las fichas y los elementos de formulario derivados del elemento principal están en estado bloqueado. No se pueden modificar en el nivel secundario.

1. En el [!UICONTROL Esquema de metadatos Forms] página, seleccione un formulario y haga clic en **[!UICONTROL Editar]** en la barra de herramientas.

1. En el **[!UICONTROL Editor de formularios de esquema de metadatos]** personaliza el formulario de metadatos. Arrastre los componentes necesarios desde el **[!UICONTROL Generar formulario]** a una de las pestañas.

   ![Editor de esquemas de metadatos para personalizar la página Propiedades del recurso](assets/metadata-schema-editor.png)

   *Figura: A [!UICONTROL Editor de formularios de esquema de metadatos] página con pestañas disponibles.*

1. Para configurar un componente, selecciónelo y modifique sus propiedades en el **[!UICONTROL Configuración]** pestaña .

### Componentes dentro de [!UICONTROL Generar formulario] ficha {#components-within-the-build-form-tab}

La variable **[!UICONTROL Generar formulario]** lista los elementos de formulario que se utilizan en el formulario de esquema. La variable **[!UICONTROL Configuración]** proporciona los atributos de cada elemento que seleccione en la **[!UICONTROL Generar formulario]** pestaña . La tabla siguiente muestra los elementos de formulario disponibles en la **[!UICONTROL Generar formulario]** pestaña:

| Nombre del componente | Descripción |
| -------------------------------- | ----------------------------------------------------------------------------------- |
| [!UICONTROL Encabezado de sección] | Añada un encabezado de sección para ver una lista de componentes comunes. |
| [!UICONTROL Texto de una sola línea] | Agregue una propiedad de texto de una sola línea. Se almacena como una cadena. |
| [!UICONTROL Texto con varios valores] | Agregue una propiedad de texto de varios valores. Se almacena como una matriz de cadenas. |
| [!UICONTROL Número] | Añada un componente numérico. |
| [!UICONTROL Fecha] | Añada un componente de fecha. |
| [!UICONTROL Lista desplegable] | Añada una lista desplegable. |
| [!UICONTROL Etiquetas estándar] | Añadir una etiqueta. |
| [!UICONTROL Etiquetas inteligentes] | Añada a las capacidades de búsqueda de aumento añadiendo automáticamente etiquetas de metadatos. |
| [!UICONTROL Campo oculto] | Añada un campo oculto. Se envía como parámetro de POST cuando se guarda el recurso. |
| [!UICONTROL Recurso al que se hace referencia en] | Añada este componente para ver la lista de recursos a los que hace referencia el recurso. |
| [!UICONTROL Referencia de recursos] | Agregar para mostrar una lista de recursos que hacen referencia al recurso. |
| [!UICONTROL Referencias de productos] | Agregar para mostrar la lista de productos vinculados al recurso. |
| [!UICONTROL Metadatos de contexto] | Añadir para controlar la visualización de otras pestañas de metadatos en la página de propiedades de los recursos. |

<!-- TBD: Ratings are not available in Experience Manager as a Cloud Service. Removed via cqdoc-18089 ticket. 
| [!UICONTROL Asset Rating]        | Add to display options for rating the asset.                                       |
-->

#### Editar el componente de metadatos {#edit-the-metadata-component}

Para editar las propiedades de un componente de metadatos en el formulario, haga clic en el componente para editar todas las propiedades o un subconjunto de las siguientes en la **[!UICONTROL Configuración]** pestaña . Se recomienda asignar solo un campo a una propiedad determinada del esquema de metadatos. De lo contrario, el sistema selecciona el último campo añadido asignado a la propiedad.

**Etiqueta de campo**: Nombre de la propiedad de metadatos que se muestra en la página de propiedades del recurso.

**Asignar a propiedad**: Esta propiedad especifica la ruta relativa o el nombre del nodo de recurso donde se guarda en el repositorio CRX. Comienza con `./` para indicar que la ruta está en el nodo del recurso.

Los siguientes son ejemplos de valores válidos para una propiedad:

* `./jcr:content/metadata/dc:title`: Almacena el valor en el nodo de metadatos del recurso como propiedad `dc:title`.

* `./jcr:created`: Almacena la fecha y hora de creación de un recurso. Es una propiedad protegida. Si configura estas propiedades, Adobe recomienda marcarlas como Deshabilitar edición . De lo contrario, se produce el fallo “Error al modificar los recursos” al guardar las propiedades del recurso.

Para asegurarse de que el componente se muestra correctamente en el formulario de esquema de metadatos, la ruta de la propiedad no debe incluir espacios.

* **Marcador de posición**: Utilice esta propiedad para especificar el texto del marcador de posición correspondiente a la propiedad metadata.
* **Requerido**: Utilice esta propiedad para marcar una propiedad de metadatos como obligatoria en la página de propiedades.
* **Deshabilitar edición**: Utilice esta propiedad para no permitir ninguna edición en una propiedad de la página de propiedades.
* **Mostrar campo vacío en solo lectura**: Marque esta propiedad para mostrar una propiedad de metadatos en la página de propiedades aunque no tenga ningún valor. De forma predeterminada, cuando una propiedad de metadatos no tiene ningún valor, no aparece en la página de propiedades.
* **Mostrar lista ordenada**: Utilice esta propiedad para mostrar una lista ordenada de opciones.
* **Opciones**: Utilice esta propiedad para especificar opciones en una lista.
* **Descripción** : Utilice esta propiedad para añadir una breve descripción para el componente de metadatos.
* **Clase**: Clase de objeto a la que está asociada la propiedad.
* **Eliminar**: Haga clic en [!UICONTROL Eliminar] para eliminar un componente del formulario de esquema.

>[!NOTE]
>
>La variable [!UICONTROL Campo oculto] no incluye estos atributos. En su lugar, incluye propiedades como Nombre, Valor, Etiqueta de campo y Descripción. Los valores del componente Campo oculto se envían como parámetro de POST cada vez que se guarda el recurso. No se guarda como metadatos para el recurso.

Si selecciona la opción **[!UICONTROL Obligatorio]**, puede buscar recursos que no tengan metadatos obligatorios. En el panel **[!UICONTROL Filtros]**, expanda el predicado **[!UICONTROL Validación de metadatos]** y seleccione la opción **[!UICONTROL No válido]**. Los resultados de la búsqueda muestran los recursos que carecen de metadatos obligatorios configurados a través del formulario de esquema.

Si agrega el componente Metadatos contextuales a cualquier ficha de cualquier formulario de esquema, el componente aparece como una lista en la página de propiedades de los recursos a los que se aplica el esquema en particular. La lista incluye todas las demás fichas excepto la ficha a la que se aplicó el componente Metadatos contextuales . Actualmente, esta función proporciona funcionalidad básica para controlar la visualización de metadatos en función del contexto.

Para mostrar cualquier pestaña en la página de propiedades además de la pestaña donde se aplica el componente Metadatos contextuales , seleccione la pestaña de la lista. La pestaña se agrega a la página de propiedades.

### Especificar propiedades en un archivo JSON {#specify-properties-in-json-file}

En lugar de especificar propiedades para las opciones de la pestaña **[!UICONTROL Configuración]**, puede definir las opciones de un archivo JSON especificando los pares de clave-valor correspondientes. Especifique la ruta del archivo JSON en el campo **[!UICONTROL Ruta de JSON]**.

#### Agregar o eliminar una ficha del formulario de esquema {#add-delete-a-tab-in-the-schema-form}

El editor de esquemas permite agregar o eliminar una pestaña. El formulario de esquema predeterminado incluye la variable **[!UICONTROL Básico]**, **[!UICONTROL Avanzadas]** , **[!UICONTROL IPTC]** y **[!UICONTROL Extensión IPTC]** pestañas.

![Tabulaciones predeterminadas en el formulario Esquema de metadatos](assets/metadata-schema-form-tabs.png)

Haga clic en `+` para agregar una ficha a un formulario de esquema. De forma predeterminada, la nueva pestaña tiene el nombre `Unnamed-1`. Puede modificar el nombre desde el **[!UICONTROL Configuración]** pestaña . Haga clic en `X` para eliminar una pestaña.

![Adición o eliminación de una ficha mediante el Editor de esquemas de metadatos](assets/metadata-schema-form-new-tab.png)

## Eliminación de formularios de esquema de metadatos {#deleting-metadata-schema-forms}

Experience Manager permite eliminar solo los formularios de esquema personalizados. No permite eliminar los formularios o plantillas de esquema predeterminados. Sin embargo, puede eliminar cualquier cambio personalizado en estos formularios.

Para eliminar un formulario, seleccione un formulario y haga clic en el icono de eliminación.

>[!NOTE]
>
>Después de eliminar los cambios personalizados en un formulario predeterminado, el icono de bloqueo vuelve a aparecer antes de que aparezca en la interfaz del esquema de metadatos para indicar que el formulario ha vuelto a su estado predeterminado.

>[!NOTE]
>
>* Después de eliminar los cambios personalizados en un formulario predeterminado, el bloqueo ![bloqueo cerrado](assets/do-not-localize/lock_closed_icon.svg) vuelve a aparecer antes del formulario. Indica que el formulario se revierte a su estado predeterminado.
>* No se pueden eliminar los formularios de esquema de metadatos predeterminados en [!DNL Assets].


## Formularios de esquema para tipos MIME {#schema-forms-for-mime-types}

[!DNL Experience Manager] proporciona formularios predeterminados para varios tipos MIME predeterminados. Sin embargo, puede agregar formularios personalizados para recursos de varios tipos de MIME.

### Agregar nuevos formularios para tipos MIME {#adding-new-forms-for-mime-types}

Cree un formulario con el tipo de formulario correspondiente. Por ejemplo, para agregar una plantilla para la variable `image/png` subtipo, cree el formulario en los formularios de &quot;imagen&quot;. El título del formulario de esquema es el nombre del subtipo. En este caso, el título es `png`.

#### Usar una plantilla de esquema existente para varios tipos MIME {#use-an-existing-schema-template-for-various-mime-types}

Puede utilizar una plantilla existente para un tipo MIME diferente. Por ejemplo, use el `image/jpeg` formulario para activos de tipo MIME `image/png`.

En este caso, cree un nodo en `/etc/dam/metadataeditor/mimetypemappings` en el repositorio CRX. Especifique un nombre para el nodo y defina las siguientes propiedades:

| Nombre | Descripción | Tipo | Valor  |
|------|-------------|------|-------|
| `exposedmimetype` | Nombre del formulario existente a asignar | `String` | `image/jpeg` |
| `mimetypes` | Lista de tipos MIME que utilizan el formulario definido en la variable `exposedmimetype` attribute | `String` | `image/png` |

[!DNL Assets] asigna los siguientes tipos MIME y formularios de esquema:

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

## Conceder acceso a esquemas de metadatos {#grant-access-to-metadata-schemas}

La función Esquema de metadatos solo está disponible para los administradores. Sin embargo, los administradores pueden proporcionar acceso a los usuarios que no sean administradores modificando algunos permisos. Proporcione a los usuarios que no sean administradores permisos para crear, modificar y eliminar en el `/conf` carpeta.

## Aplicar metadatos específicos de carpetas {#applying-folder-specific-metadata}

[!DNL Assets] permite definir una variante de un esquema de metadatos y aplicarla a una carpeta específica.

Por ejemplo, puede definir una variante del esquema de metadatos predeterminado y aplicarla a una carpeta. Cuando se aplica el esquema modificado, anula el esquema de metadatos predeterminado original que se aplica a los recursos de la carpeta.

Solo los recursos cargados en la carpeta a la que se aplica este esquema se ajustan a los metadatos modificados definidos en el esquema de metadatos de la variante. [!DNL Assets] en otras carpetas donde se aplica el esquema original, siga ajustándose a los metadatos definidos en el esquema original.

La herencia de metadatos por recursos se basa en el esquema que se aplica a la carpeta de nivel superior de la jerarquía. Las subcarpetas aplican o heredan el mismo esquema. Si se aplica un esquema diferente en el nivel de subcarpeta, la herencia se detiene.

1. En [!DNL Experience Manager] interfaz, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Esquemas de metadatos]**. Se muestra la página **[!UICONTROL Formularios de esquema de metadatos]**.
1. Seleccione la casilla de verificación situada antes de un formulario, por ejemplo el formulario de metadatos predeterminado, y haga clic en el **[!UICONTROL Copiar]** y guárdelo como un formulario personalizado. Especifique un nombre personalizado para el formulario, por ejemplo `my_default`. También puede crear un formulario personalizado.

1. En el **[!UICONTROL Esquema de metadatos Forms]** seleccione `my_default` y, a continuación, haga clic en **[!UICONTROL Editar]**.
1. En el **[!UICONTROL Editor de esquemas de metadatos]** , agregue un campo de texto al formulario de esquema. Por ejemplo, agregue un campo con la etiqueta **[!UICONTROL Categoría]**.
1. Haga clic en **[!UICONTROL Guardar]**. El formulario modificado aparece en la lista **[!UICONTROL Esquema de metadatos Forms]** página.
1. Toque o haga clic **[!UICONTROL Aplicar a carpetas]** de la barra de herramientas para aplicar los metadatos personalizados a una carpeta.
1. Seleccione la carpeta en la que desea aplicar el esquema modificado y, a continuación, toque o haga clic en **[!UICONTROL Aplicar]**.
1. Si se ha aplicado el otro esquema de metadatos a la carpeta, aparece un mensaje en el que se advierte que está a punto de sobrescribir el esquema de metadatos existente. Haga clic en **Sobrescribir**.
1. Haga clic en **OK** para cerrar el mensaje de éxito.
1. Vaya a la carpeta a la que aplicó el esquema de metadatos modificado.

## Definición de metadatos obligatorios {#defining-mandatory-metadata}

Puede definir campos obligatorios a nivel de carpeta, que se aplican a los recursos que se cargan en la carpeta. Si carga recursos con metadatos que faltan para los campos obligatorios definidos anteriormente, en la vista Tarjeta aparecerá una indicación visual de los metadatos que faltan en los recursos.

>[!NOTE]
>
>Un campo de metadatos se puede definir como obligatorio en función del valor de otro campo. En la vista Tarjetas, el Experience Manager no muestra el mensaje de advertencia sobre la falta de metadatos para estos campos de metadatos obligatorios.

1. Haga clic en el logotipo del Experience Manager y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Esquemas de metadatos]**. Se muestra la página **[!UICONTROL Formularios de esquema de metadatos]**.
1. Guarde el formulario de metadatos predeterminado como un formulario personalizado. Por ejemplo, guárdelo como `my_default`.
1. Edite el formulario personalizado. Añada un campo obligatorio. Por ejemplo, agregue un **[!UICONTROL Categoría]** y haga que el campo sea obligatorio.
1. Haga clic en **[!UICONTROL Guardar]**. El formulario modificado aparece en la lista **[!UICONTROL Esquema de metadatos Forms]** página. Seleccione el formulario y, a continuación, toque o haga clic en **[!UICONTROL Aplicar a carpetas]** de la barra de herramientas para aplicar los metadatos personalizados a una carpeta.
1. Vaya a la carpeta y cargue algunos recursos con metadatos que faltan para el campo obligatorio que ha agregado al formulario personalizado. Se muestra un mensaje para los metadatos que faltan para el campo obligatorio en la vista de tarjeta del recurso.
1. (Opcional) Acceso `https://[server]:[port]/system/console/components/`. Configurar y habilitar `com.day.cq.dam.core.impl.MissingMetadataNotificationJob` que está desactivado de forma predeterminada. Establezca una frecuencia con la que el Experience Manager comprueba la validez de los metadatos en los recursos.

   Esta configuración agrega una propiedad de `hasValidMetadata` a `jcr:content` de los recursos. Con esta propiedad, el Experience Manager puede filtrar los resultados en una búsqueda.

   >[!NOTE]
   >
   >Si se agrega un recurso después de la comprobación programada, el recurso no se marca con `hasValidMetadata` hasta la siguiente comprobación programada. Los recursos no aparecen en los resultados de búsqueda intermedios.

   >[!CAUTION]
   >
   >Las comprobaciones de validación de metadatos requieren muchos recursos y pueden afectar al rendimiento del sistema. Programe las comprobaciones según corresponda. Si el servidor no puede lidiar con la carga, intente desactivar este trabajo

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de Recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con Assets](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos conectados](use-assets-across-connected-assets-instances.md)
* [Informes de Asset](asset-reports.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)
