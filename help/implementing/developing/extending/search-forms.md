---
title: Configurar formularios de búsqueda
description: Configuración de la búsqueda de Forms para Adobe Experience Manager as a Cloud Service.
exl-id: b06649c4-cc91-44e3-8699-00e90140b90d
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '2043'
ht-degree: 17%

---

# Configurar formularios de búsqueda {#configuring-search-forms}

Adobe Experience Manager as a Cloud Service viene con un [Buscar](/help/sites-cloud/authoring/getting-started/search.md) mecanismo.

En combinación con esto, también hay un conjunto de opciones predefinidas para ayudarle a filtrar el contenido. Estas contienen facetas predefinidas como **Fecha de modificación**, **Estado de publicación** o **Estado de Live Copy** para ayudarle a explorar en profundidad rápidamente los recursos que necesita.

![uso de búsqueda y filtro](assets/csf-usage.png)

Juntos, estos elementos pretenden ayudarle a localizar su contenido de forma rápida y sencilla desde:

* [Buscar y filtrar](/help/sites-cloud/authoring/getting-started/search.md#search-and-filter)
* [Selector de carril](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)
* el [Navegador de recursos](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser) (al editar páginas)

>[!NOTE]
>
>Puede configurar el subyacente [Búsqueda de contenido e indexación](/help/operations/indexing.md) servicio.

Uso **Buscar en Forms**, puede personalizar y ampliar estos paneles según sus necesidades específicas.

La variable **Buscar en Forms** proporcione una selección predeterminada de [predicados](#predicates-and-their-settings) que puede combinar y definir. La variable [cuadros de diálogo para configurar estos formularios](#configuring-your-search-forms) se puede acceder a través de:

* **Herramientas**
   * **General**
      * **Formularios de búsqueda**

## Forms predeterminado {#default-forms}

Al acceder por primera vez a la variable **Buscar en Forms** puede ver que todas las configuraciones tienen un símbolo de candado. Esto indica que la configuración correspondiente es la configuración predeterminada (predeterminada) y no se puede eliminar. Una vez que haya personalizado y guardado, desaparecerá una configuración del bloqueo. Volverá a aparecer al [eliminar la configuración personalizada](#deleting-a-configuration-to-reinstate-the-default), en cuyo caso se restablecerá el valor predeterminado (y el indicador del cerrojo).

![configuración de la información general de formularios de búsqueda](assets/csf-overview.png)

Las configuraciones predeterminadas (enumeradas alfabéticamente) disponibles son:

* **Carril de búsqueda de administración de recursos**
* **Editor de páginas (búsqueda de documentos)**
* **Editor de página (búsqueda de fragmentos de experiencias)**
* **Editor de páginas (búsqueda de imágenes)**
* **Editor de páginas (búsqueda de manuscritos)**
* **Editor de páginas (búsqueda de páginas)**
* **Editor de páginas (búsqueda de párrafos)**
* **Editor de páginas (búsqueda de productos)**
* **Editor de páginas (búsqueda de Scene7)**
* **Editor de páginas (búsqueda de vídeos)**
* **Carril de búsqueda de administración de proyecto**
* **Carril de búsqueda de traducción del proyecto**
* **Carril de búsqueda de administración de sitios**
* **Carril de búsqueda de administración de fragmentos de código**
* **Carril de búsqueda de administración de Stock**
* **Carril de búsqueda de modelos de fragmentos de contenido**
* **Carril de búsqueda de administración de proyecto**
* **Carril de búsqueda de traducción del proyecto**

>[!NOTE]
>
>Para obtener más información sobre los formularios de búsqueda relacionados con los recursos, consulte [Recursos: facetas de búsqueda](/help/assets/search-facets.md)


## Predicados y su configuración {#predicates-and-their-settings}

### Predicados {#predicates}

Los siguientes predicados están disponibles, según la configuración:

<table>
 <tbody>
  <tr>
   <th>Predicado</th>
   <th>Función</th>
   <th>Configuración</th>
  </tr>
  <tr>
   <td>Análisis</td>
   <td>Funciones de búsqueda/filtro en el navegador Sitios al mostrar datos con tecnología de análisis. Los filtros de búsqueda de Analytics se cargan para que coincidan con las columnas de análisis personalizado asignadas.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Estado de aprobación</td>
   <td>Busque según el estado de aprobación.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Nombre de propiedad*</li>
     <li>Descripción</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Autor</td>
   <td>Buscar según el autor.</td>
   <td>
    <ul>
     <li>Marcador de posición</li>
     <li>Nombre de propiedad*</li>
     <li>Descripción</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Extraído por</td>
   <td>Buscar recursos extraídos por un usuario específico.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Marcador de posición</li>
     <li>Descripción</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Estado de extracción</td>
   <td>Busque recursos con un estado de cierre de compra específico.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Nombre de propiedad*</li>
     <li>Descripción</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Componentes</td>
   <td>Permite que un autor busque o filtre páginas que tengan un componente específico en él. Por ejemplo, una galería de imágenes.<br /> </td>
   <td>
    <ul>
     <li>Marcador de posición</li>
     <li>Nombre de propiedad*</li>
     <li>Profundidad de la propiedad</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Intervalo de fechas</td>
   <td>Busque recursos creados dentro de un intervalo especificado para una propiedad de fecha. En el panel Buscar, puede especificar las fechas de inicio y finalización.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Marcador de posición</li>
     <li>Nombre de propiedad*</li>
     <li>Texto de intervalo (desde)*</li>
     <li>Texto de intervalo (hasta)*</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Estado de caducidad</td>
   <td>Busque recursos en función del estado de caducidad.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Nombre de propiedad*</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Tamaño del archivo</td>
   <td>Filtre los recursos en función de su tamaño.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Nombre de propiedad*</li>
     <li>Ruta de opción</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Tipo de archivo</td>
   <td>Buscar recursos en función del tipo de archivo/mime.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li> 
     <li>Nombre de propiedad*</li>
     <li>Ruta de tipo MIME</li>
     <li>Descripción</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Texto completo</td>
   <td>Predicado de búsqueda para búsquedas de texto completo. Se asigna con el operador "jcr:contains".</td>
   <td>
    <ul>
     <li>Marcador de posición</li>
     <li>Nombre de propiedad</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Agrupar</td>
   <td>predicado de búsqueda para grupo (solo utilizado dentro del predicado de perspectivas).</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Filtro oculto</td>
   <td>Un filtro de propiedad y valor, no visible para el usuario.</td>
   <td>
    <ul>
     <li>Nombre de propiedad*</li>
     <li>Valor de propiedad*</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Perspectivas</td>
   <td>Busque según una selección de parámetros de perspectivas.</td>
   <td>Este es un predicado complejo compuesto por varios predicados:
    <ul>
     <li>Agrupar</li>
     <li>Intervalo</li>
     <li>Opciones</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Miembro de la colección</td>
   <td>Buscar recursos que sean miembros de una colección</td>
   <td>
    <ul>
     <li>Descripción</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Propiedad con valores múltiples</td>
   <td>Busque varios valores de una propiedad especificada.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Marcador de posición</li>
     <li>Nombre de propiedad*</li>
     <li>Compatibilidad con el delimitador</li>
     <li>Delimitadores de entrada</li>
     <li>Ignorar mayúsculas y minúsculas</li>
     <li>Descripción</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Opciones</td>
   <td><p>Las opciones son nodos de contenido creados por el usuario.</p> <p>Consulte <a href="#addinganoptionspredicate">Adición de un predicado de opciones</a> para obtener más información.</p> </td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Nombre de propiedad*</li>
     <li>Una sola selección</li>
     <li>Agregar opciones</li>
     <li>Manual</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Opciones Propiedad</td>
   <td>Busque una o varias propiedades de la opción .</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Nombre de propiedad*</li>
     <li>Ruta del nodo de opciones</li>
     <li>Profundidad de la propiedad</li>
     <li>Una sola selección</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Estado de la página</td>
   <td>Filtre las páginas según su estado.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Nombre de la propiedad de publicación*</li>
     <li>Nombre de la propiedad de páginas bloqueadas*</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Ruta </td>
   <td>Filtre según la ruta específica. Se pueden especificar varias rutas como opciones.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Añadir rutas de búsqueda</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Navegador de rutas</td>
   <td>Proporcione un explorador de rutas para buscar en una ruta raíz predefinida.</td>
   <td>
    <ul>
     <li>Marcador de posición</li>
     <li>Ruta raíz</li>
     <li>Descripción</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Ruta oculta</td>
   <td>Un filtro en la ruta, no visible para el usuario.</td>
   <td>
    <ul>
     <li>Nombre de propiedad (`path`)</li>
     <li>Valor de propiedad (`/content/dam`)</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Propiedad</td>
   <td>Buscar en una propiedad especificada.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Marcador de posición</li>
     <li>Nombre de propiedad</li>
     <li>Búsqueda parcial</li>
     <li>Ignorar mayúsculas y minúsculas</li>
     <li>Descripción</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Estado de publicación</td>
   <td>Filtre los recursos en función de su estado de publicación.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Nombre de propiedad*</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Intervalo</td>
   <td>Busque recursos que se encuentren dentro de un intervalo especificado. En el panel Buscar, puede especificar valores mínimos y máximos para el intervalo.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Nombre de propiedad*</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Clasificación</td>
   <td>Busque recursos según su clasificación promedio.<br /> </td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Nombre de propiedad*</li>
     <li>Ruta de opción</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Fecha relativa</td>
   <td>Filtre los recursos en función de la fecha relativa de su creación. Por ejemplo, hace 1 semana, hace 1 mes.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Nombre de propiedad*</li>
     <li>Fecha relativa</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Intervalo del regulador</td>
   <td>Un predicado de búsqueda común que amplía el predicado de intervalo con la capacidad de deslizador. El valor de la propiedad en la que se busca debe estar entre los límites del control deslizante.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Nombre de propiedad*</li>
     <li>Ruta del nodo de opciones</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Estado</td>
   <td>Busque según la aprobación y el estado de cierre de compra.</td>
   <td>Este es un predicado complejo compuesto por varios predicados:
    <ul>
     <li>Estado de aprobación</li>
     <li>Estado de extracción</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Etiquetas</td>
   <td>Buscar según etiquetas.</td>
   <td>
    <ul>
     <li>Lavandería de campo</li>
     <li>Marcador de posición</li>
     <li>Nombre de propiedad*</li>
     <li>Mostrar la opción de hacer coincidir todas las etiquetas</li>
     <li>Ruta de las etiquetas raíz</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Plantillas</td>
   <td>Busque según la plantilla seleccionada.</td>
   <td>
    <ul>
     <li>Marcador de posición</li>
     <li>Nombre de propiedad*</li>
     <li>Descripción</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Estado de traducción</td>
   <td>Busque según el estado de traducción.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
    </ul> 
   </td>
  </tr>
 </tbody>
</table>

<!--
  <tr>
   <td>Date ???</td>
   <td>Slider-based search of assets based on a date property.</td>
   <td>
    <ul>
     <li>Field Label</li>
     <li>Property Name*</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Asset Last Modified ?????</td>
   <td>Date the asset was last modified.<br /> </td>
   <td>A customized predicate, based on the Date Predicate.</td>
  </tr>
  <tr>
   <td>Range Options ???</td>
   <td>A specific search predicate for Assets and the same as common Slider Predicate. Is still available due to backward compatibilty issues.</td>
   <td>
    <ul>
     <li>Field Label</li>
     <li>Property Name*</li>
     <li>Option Path</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Tag </td>
   <td>Search assets based on tags. You can configure the Path property to populate various tags in the Tags list.</td>
   <td>
    <ul>
     <li>Field Label</li>
     <li>Property Name*</li>
     <li>Option Path</li>
     <li>Description</li>
    </ul> </td>
  </tr>
-->

>[!NOTE]
>
>Los predicados de búsqueda comunes se definen en:
>  `/libs/cq/gui/components/common/admin/customsearch/searchpredicates`
>
>Esta información es solo de referencia, no debe realizar cambios en `/libs`.

<!--
>* Search predicates related only to siteadmin (classic UI) are located under:
> `/libs/cq/gui/components/siteadmin/admin/searchpanel/searchpredicates`
>   * These are deprecated and only available for backward compatibility.
>
-->

### Predicar configuración {#predicate-settings}

En función del predicado, hay una selección de opciones disponibles para la configuración, entre las que se incluyen:

* **Etiqueta de campo**

   Etiqueta que aparecerá como encabezado contraíble o como etiqueta de campo del predicado.

* **Descripción**

   Detalles descriptivos para el usuario.

* **Marcador de posición**

   Texto vacío o el marcador de posición del predicado en caso de que no se introduzca ningún texto de filtrado.

* **Nombre de propiedad**

   La propiedad en la que se va a buscar. Utiliza una ruta relativa y los caracteres comodín `*/*/*` especifique la profundidad de la propiedad en relación con la variable `jcr:content` (cada asterisco representa un nivel de nodo).

   Si desea buscar solo en un nodo secundario de primer nivel del recurso que tenga la variable `x` en la variable `jcr:content` uso de nodos `*/jcr:content/x`

* **Profundidad de la propiedad**

   Profundidad máxima para buscar esa propiedad dentro de los recursos. Por lo tanto, se puede realizar una búsqueda en esa propiedad en un recurso y en elementos secundarios recursivos hasta que el nivel de elementos secundarios sea igual a la profundidad especificada.

* **Valor de propiedad**

   El valor de la propiedad como una cadena absoluta o como lenguaje de expresión; por ejemplo, `cq:Page` o

   `${empty requestPathInfo.suffix ? "/content" : requestPathInfo.suffix}`.

* **Texto de rango**

   Etiqueta del campo de rango de la variable **Intervalo de fechas** predicado.

* **Ruta de opción**

   El usuario puede seleccionar la ruta utilizando el explorador de rutas en la pestaña de configuración del predicado. Después de seleccionar la variable **+** se utiliza para añadir la selección a la lista de opciones válidas (a continuación, la variable **-** para quitar si es necesario).

   Las opciones son nodos de contenido creados por el usuario, con la siguiente estructura:

   `(jcr:primaryType = nt:unstructured, value (String), jcr:title (String))`

* **Ruta del nodo de opciones**
Efectivamente igual que la variable 
**Ruta de opciones**, solo esto se hace en el campo predicado común y el otro es específico para los recursos.

* **Selección única**
Si se selecciona, las opciones se representan como casillas de verificación que permiten una sola selección. Si se selecciona por error, se puede anular la selección de una casilla de verificación.

* **Nombre de propiedades de publicación y Live Copy**
Etiquetas para las casillas de verificación de publicación y Live Copy para el predicado específico de Sitios.

* &amp;ast; en las etiquetas de campo de la **Configuración** significa que los campos son obligatorios y, si se dejan en blanco, aparece un mensaje de error.

## Configuración de la búsqueda Forms {#configuring-your-search-forms}

### Creación/apertura de una configuración personalizada {#creating-opening-a-customized-configuration}

1. Vaya a **Herramientas**, **General**, **Buscar en Forms**.

1. Seleccione la configuración que desee personalizar.
1. Utilice la variable **Editar** para abrir la configuración y actualizarla.
1. Si desea realizar una nueva personalización [agregar nuevos campos de predicado y definir la configuración](#add-edit-a-predicate-field-and-define-field-settings) según sea necesario. Si una personalización existente, puede seleccionar un campo existente y [actualizar la configuración](#add-edit-a-predicate-field-and-define-field-settings).
1. Select **Listo** para guardar la configuración. Los cambios se pueden ver la próxima vez que se utilice la configuración.

   >[!NOTE]
   >
   >Las configuraciones personalizadas se almacenan (según corresponda) en:
   >
   >* `/apps/cq/gui/content/facets/<option>`
   >* `/apps/commerce/gui/content/facets/<option>`


### Agregar o editar un campo predicado y definir la configuración de campo {#add-edit-a-predicate-field-and-define-field-settings}

Puede añadir o editar campos y definir/actualizar su configuración:

1. [Abra la configuración personalizada](#creating-opening-a-customized-configuration) para actualizar.
1. Si desea agregar un nuevo campo, abra el **Seleccionar predicado** y arrastre el predicado necesario a la ubicación requerida. Por ejemplo, la variable **Predicado de intervalo de fechas**:

   ![agregar un predicado](assets/csf-add-predicate.png)

1. Dependiendo de si:

   * Se está agregando un nuevo campo:

      Después de agregar el predicado, **Configuración** se abrirá y mostrará las propiedades que se pueden definir.

   * Desea actualizar un predicado existente:

      Seleccione el campo de predicado (a la derecha) y, a continuación, abra el **Configuración** pestaña .
   Por ejemplo, la configuración de la variable **Predicado de intervalo de fechas**:

   ![modificar predicado](assets/csf-modify-predicate.png)

1. Realice los cambios según sea necesario y confirme con **Listo**. Los cambios se pueden ver la próxima vez que se utilice la configuración.

### Vista previa de la configuración de búsqueda {#previewing-the-search-configuration}

1. Seleccione el icono Vista previa :

   ![icono de vista previa](assets/csf-preview-icon.png)

1. Se mostrarán los formularios de búsqueda tal como se mostrarán (completamente expandidos) en la columna Buscar de la consola adecuada.

   ![formulario de vista previa](assets/csf-preview-form.png)

1. **Cerrar** la vista previa para devolver y finalizar la configuración.

### Eliminación de un campo predicado {#deleting-a-predicate-field}

1. [Abra la configuración personalizada](#creating-opening-a-customized-configuration) para actualizar.
1. Seleccione el campo de predicado (a la derecha) y abra el **Configuración** y, a continuación, seleccione **Eliminar** (abajo a la izquierda).

   ![icono eliminar](assets/csf-delete-icon.png)

1. Un cuadro de diálogo solicitará la confirmación de la acción de eliminar.

1. Confirme este y cualquier otro cambio con **Listo**.

### Eliminación de una configuración (para restablecer el valor predeterminado) {#deleting-a-configuration-to-reinstate-the-default}

Una vez que haya personalizado una configuración, esto anulará los valores predeterminados. Puede restablecer la configuración predeterminada eliminando la configuración personalizada.

>[!NOTE]
>
>No puede eliminar las configuraciones predeterminadas.

La eliminación de una configuración personalizada se realiza desde la consola:

1. Seleccione la configuración requerida (por ejemplo, **Editor de páginas (búsqueda de párrafos)**) y luego la variable **Eliminar** en la barra de herramientas:

   ![restaurar predeterminado](assets/csf-restore-default.png)

1. La configuración personalizada se eliminará y se restablecerá el valor predeterminado (esto se indica con la reaparición del símbolo de candado en la consola).

### Adición de predicados de opciones {#adding-options-predicates}

Los predicados de opciones (Opciones, Propiedad Options) permiten configurar un elemento que se va a buscar. Normalmente se utilizan para buscar algo directamente debajo de la página; por ejemplo, una propiedad en el nodo de página.

El siguiente ejemplo (para buscar según la plantilla utilizada para crear una página) ilustra los pasos involucrados:

1. Cree el nodo que define la propiedad en la que se buscará.

   Necesitará un nodo raíz que contenga definiciones de las opciones individuales para que esté disponible para el usuario.

   Los nodos de las opciones individuales necesitan las propiedades:

   * `jcr:title` - la etiqueta de campo que se mostrará en el carril de búsqueda
   * `value` : el valor de propiedad en el que se va a buscar

   ![Definición del predicado](assets/csf-options-predicate-01.png)

   >[!NOTE]
   >
   >You ***must*** no cambie nada en la variable `/libs` ruta.
   >
   >Esto se debe a que el contenido de `/libs` se sobrescribe la próxima vez que actualice la instancia (y puede sobrescribirse al aplicar una corrección o un paquete de funciones).
   >
   >El método recomendado para la configuración y otros cambios es:
   >
   >1. Volver a crear el elemento necesario, ya que existe en `/libs`, en `/apps`. En este caso, de:
   >1. `/libs/cq/gui/content/common/options/predicates`
   >1. Realice cambios dentro de `/apps.`


1. Abra el **Buscar en Forms** y seleccione la configuración que desea actualizar. Por ejemplo, **Carril de búsqueda del administrador de sitios**. A continuación, seleccione **Editar**.

1. En función de la configuración, añada un **Opciones** o **Propiedad Options** a la configuración.
1. Actualice los campos, en particular:

   * **Nombre de propiedad**

      Especifique la propiedad node que se buscará en los nodos de destino. Por ejemplo:

      `jcr:content/cq:template`

   * **Ruta del nodo de opción**

      Seleccione la ruta en la que se guardan las opciones. Por ejemplo:

      `/apps/cq/gui/content/common/options/predicates/templatetype`
   ![Predicados de opciones](assets/csf-options-predicate-02.png)

1. Select **Listo** para guardar la configuración.
1. Vaya a la consola adecuada (en este ejemplo, **Sitios**) y abra el **Buscar - Filtros** carril. Se verán los formularios de búsqueda recién definidos, junto con las distintas opciones. Seleccione la opción requerida para ver los resultados de la búsqueda.

   ![opciones que se están utilizando](assets/csf-options-usage.png)


## Permisos de usuario {#user-permissions}

En la tabla siguiente se enumeran los permisos necesarios para realizar acciones de edición, eliminación y vista previa en formularios de búsqueda.

<table>
 <thead>
  <tr>
   <td><strong>Acción</strong></td>
   <td><strong>Permisos</strong></td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>Editar </td>
   <td>Permisos de lectura y escritura en la variable <code>/apps </code>nodo .</td>
  </tr>
  <tr>
   <td>Eliminar</td>
   <td>Permisos de lectura, escritura y eliminación en <code>/apps</code> node</td>
  </tr>
  <tr>
   <td>Previsualizar</td>
   <td>Permisos de lectura, escritura y eliminación en <code>/var/dam/content</code> nodo .<br /> Permisos de lectura y escritura en la variable <code>/apps</code> nodo .</td>
  </tr>
 </tbody>
</table>
