---
title: Configurar formularios de búsqueda
description: Configuración de Search Forms para Adobe Experience Manager as a Cloud Service.
exl-id: b06649c4-cc91-44e3-8699-00e90140b90d
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2036'
ht-degree: 10%

---

# Configurar formularios de búsqueda {#configuring-search-forms}

Adobe Experience Manager as a Cloud Service viene con un potente mecanismo de [búsqueda](/help/sites-cloud/authoring/search.md).

En combinación con esto, también hay un conjunto de opciones predefinidas para ayudarle a filtrar su contenido. Contienen facetas predefinidas como **Fecha de modificación**, **Estado de publicación** o **Estado de Live Copy** para ayudarle a explorar en profundidad los recursos que necesita.

![uso de búsqueda y filtro](assets/csf-usage.png)

Juntos, estos objetivos le ayudan a localizar su contenido de forma rápida y sencilla desde:

* [Buscar y filtrar](/help/sites-cloud/authoring/search.md#search-and-filter)
* [Selector de carril](/help/sites-cloud/authoring/basic-handling.md#rail-selector)
* el [explorador Assets](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#assets-browser) (al editar páginas)

>[!NOTE]
>
>Puede configurar el servicio [Búsqueda de contenido e indexación](/help/operations/indexing.md) subyacente.

Con **Buscar en Forms**, puede personalizar y ampliar estos paneles según sus necesidades específicas.

**Search Forms** proporciona una selección predeterminada de [predicados](#predicates-and-their-settings) que puede combinar y definir. Se puede acceder a los [cuadros de diálogo para configurar estos formularios](#configuring-your-search-forms) a través de:

* **Herramientas**
   * **General**
      * **Buscar en Forms**

## Forms predeterminado {#default-forms}

Cuando acceda por primera vez a la consola **Buscar en Forms**, verá que todas las configuraciones tienen un símbolo de candado. Esto indica que la configuración correspondiente es la predeterminada (predeterminada) y no se puede eliminar. Una vez que haya personalizado y guardado una configuración, el bloqueo desaparecerá. Volverá a aparecer cuando [elimine su configuración personalizada](#deleting-a-configuration-to-reinstate-the-default), en cuyo caso se restablecerá el valor predeterminado (y el indicador de candado).

![configurar información general de formularios de búsqueda](assets/csf-overview.png)

Las configuraciones predeterminadas disponibles (enumeradas alfabéticamente) son las siguientes:

* **Carril de búsqueda de administración de Assets**
* **Editor de páginas (búsqueda de documentos)**
* **Editor de páginas (búsqueda de fragmentos de experiencias)**
* **Editor de páginas (búsqueda de imágenes)**
* **Editor de páginas (búsqueda de manuscritos)**
* **Editor de páginas (búsqueda de páginas)**
* **Editor de páginas (búsqueda de párrafos)**
* **Editor de páginas (búsqueda de productos)**
* **Editor de páginas (búsqueda de Scene7)**
* **Editor de páginas (búsqueda de vídeos)**
* **Carril de búsqueda del administrador del proyecto**
* **Carril de búsqueda de traducción del proyecto**
* **Carril de búsqueda de administración de sitios**
* **Carril de búsqueda de administración de fragmentos**
* **Carril de búsqueda de administración de Stock**
* **Carril de búsqueda de modelos de fragmentos de contenido**
* **Carril de búsqueda del administrador del proyecto**
* **Carril de búsqueda de traducción del proyecto**

>[!NOTE]
>
>Para obtener más información acerca de los formularios de búsqueda relacionados con recursos, consulte [Assets - Facetas de búsqueda](/help/assets/search-facets.md).


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
   <td>Funciones de búsqueda y filtrado en el explorador de sitios al mostrar datos con análisis. Los filtros de búsqueda de Analytics se cargan para coincidir con las columnas de Analytics personalizadas asignadas.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Estado de aprobación</td>
   <td>Buscar según el estado de aprobación.</td>
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
   <td>Buscar recursos desprotegidos por un usuario específico.</td>
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
   <td>Permite a un autor buscar/filtrar páginas que tienen un componente específico en él. Por ejemplo, una galería de imágenes.<br /> </td>
   <td>
    <ul>
     <li>Marcador de posición</li>
     <li>Nombre de propiedad*</li>
     <li>Profundidad de la propiedad</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Intervalo de fecha</td>
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
   <td>Buscar recursos en función del estado de caducidad.</td>
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
   <td>Busque recursos en función del tipo de archivo/mime.</td>
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
     <li>Nombre de la propiedad</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Grupo</td>
   <td>Predicado de búsqueda de grupo (solo se usa dentro del Predicado de perspectivas).</td>
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
   <td>Busque según una selección de parámetros de Insights.</td>
   <td>Este es un predicado complejo compuesto por varios predicados:
    <ul>
     <li>Grupo</li>
     <li>Intervalo</li>
     <li>Opciones</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Miembro de colección</td>
   <td>Buscar recursos que sean miembros de una colección</td>
   <td>
    <ul>
     <li>Descripción</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Propiedad con valores múltiples</td>
   <td>Buscar en varios valores de una propiedad especificada.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Marcador de posición</li>
     <li>Nombre de propiedad*</li>
     <li>Compatibilidad con delimitadores</li>
     <li>Delimitadores de entrada</li>
     <li>Ignorar mayúsculas y minúsculas</li>
     <li>Descripción</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Opciones</td>
   <td><p>Las opciones son nodos de contenido creados por el usuario.</p> <p>Consulte <a href="#addinganoptionspredicate">Agregar un predicado de opciones</a> para obtener más información.</p> </td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Nombre de propiedad*</li>
     <li>Selección única</li>
     <li>Añadir opciones</li>
     <li>Manual</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Propiedad Options</td>
   <td>Busque una o más propiedades de la opción.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Nombre de propiedad*</li>
     <li>Ruta del nodo de opciones</li>
     <li>Profundidad de la propiedad</li>
     <li>Selección única</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Estado de la página</td>
   <td>Filtrar páginas según su estado.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Nombre de propiedad de publicación*</li>
     <li>Nombre de propiedad de páginas bloqueadas*</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Ruta</td>
   <td>Filtre según una ruta específica. Puede especificar varias rutas como opciones.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Añadir rutas de búsqueda</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Navegador de rutas</td>
   <td>Proporcione un navegador de rutas para buscar en una ruta raíz predefinida.</td>
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
   <td>Busque en una propiedad especificada.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Marcador de posición</li>
     <li>Nombre de la propiedad</li>
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
   <td>Busque recursos que se encuentren dentro de un rango especificado. En el panel Buscar, puede especificar los valores mínimo y máximo del rango.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Nombre de propiedad*</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Clasificación</td>
   <td>Buscar recursos según su clasificación promedio.<br /> </td>
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
   <td>Un predicado de búsqueda común que amplía el predicado de intervalo con la capacidad del control deslizante. El valor de la propiedad buscada debe estar entre los límites del control deslizante.</td>
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
   <td>Busque según el estado de aprobación y cierre de compra.</td>
   <td>Este es un predicado complejo compuesto por varios predicados:
    <ul>
     <li>Estado de aprobación</li>
     <li>Estado de extracción</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Etiquetas</td>
   <td>Busque en función de las etiquetas.</td>
   <td>
    <ul>
     <li>Lavel de campo</li>
     <li>Marcador de posición</li>
     <li>Nombre de propiedad*</li>
     <li>Mostrar la opción de hacer coincidir todas las etiquetas</li>
     <li>Ruta de etiquetas raíz</li>
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
>Esta información es solo para referencia; no debe cambiar `/libs`.

<!--
>* Search predicates related only to siteadmin (classic UI) are located under:
> `/libs/cq/gui/components/siteadmin/admin/searchpanel/searchpredicates`
>   * These are deprecated and only available for backward compatibility.
>
-->

### Configuración de predicado {#predicate-settings}

En función del predicado, hay una selección de opciones disponibles para la configuración, entre las que se incluyen:

* **Etiqueta de campo**

  La etiqueta que aparecerá como encabezado contraíble o como etiqueta de campo del predicado.

* **Descripción**

  Detalles descriptivos del usuario.

* **Marcador de posición**

  Texto vacío o el marcador de posición del predicado en caso de que no se introduzca ningún texto de filtrado.

* **Nombre de propiedad**

  Propiedad en la que se va a buscar. Utiliza una ruta relativa y los caracteres comodín `*/*/*` especifican la profundidad de la propiedad en relación con el nodo `jcr:content` (cada asterisco representa un nivel de nodo).

  Si desea buscar únicamente en un nodo secundario de primer nivel del recurso que tiene la propiedad `x` en el nodo `jcr:content`, utilice `*/jcr:content/x`

* **Profundidad de propiedad**

  Profundidad máxima para buscar esa propiedad dentro de los recursos. Por lo tanto, se puede realizar una búsqueda de esa propiedad en un recurso y en elementos secundarios recursivos hasta que el nivel de los elementos secundarios sea igual a la profundidad especificada.

* **Valor de propiedad**

  El valor de la propiedad como cadena absoluta o como lenguaje de expresión; por ejemplo, `cq:Page` o

  `${empty requestPathInfo.suffix ? "/content" : requestPathInfo.suffix}`.

* **Texto de intervalo**

  La etiqueta del campo de intervalo en el predicado **Date Range**.

* **Ruta de opción**

  El usuario puede seleccionar la ruta mediante el Explorador de rutas en la pestaña de configuración de predicado. Después de seleccionar el icono **+** se usa para agregar la selección a la lista de opciones válidas (a continuación, el icono **-** que se quitará si es necesario).

  Las opciones son nodos de contenido creados por el usuario que tienen la siguiente estructura:

  `(jcr:primaryType = nt:unstructured, value (String), jcr:title (String))`

* **Ruta del nodo de opciones**
Igual que en la práctica **Ruta de opciones**, solo que esto se encuentra en el campo de predicado común y el otro es específico para los recursos.

* **Selección única**
Si se selecciona, las opciones se representan como casillas de verificación que permiten solo una selección. Si se selecciona por error, se puede anular la selección de una casilla de verificación.

* **Nombre(s) de propiedad de publicación y Live Copy**
Las etiquetas de las casillas de verificación de publicación y Live Copy para el predicado específico de Sites.

* &ast; en las etiquetas de campo de la ficha **Configuración** significa que los campos son obligatorios y, si se deja en blanco, aparecerá un mensaje de error.

## Configuración de Search Forms {#configuring-your-search-forms}

### Creación/apertura de una configuración personalizada {#creating-opening-a-customized-configuration}

1. Vaya a **Herramientas**, **General**, **Buscar en Forms**.

1. Seleccione la configuración que desee personalizar.
1. Use el icono **Editar** para abrir la configuración y actualizarla.
1. Si hay una nueva personalización, probablemente quiera [agregar nuevos campos de predicado y definir la configuración](#add-edit-a-predicate-field-and-define-field-settings) según sea necesario. Si ya existe una personalización, puede seleccionar un campo existente y [actualizar la configuración](#add-edit-a-predicate-field-and-define-field-settings).
1. Seleccione **Listo** para guardar la configuración. Los cambios se podrán ver la próxima vez que se utilice la configuración.

   >[!NOTE]
   >
   >Las configuraciones personalizadas se almacenan (según corresponda) en:
   >
   >* `/apps/cq/gui/content/facets/<option>`
   >* `/apps/commerce/gui/content/facets/<option>`

### Adición o edición de un campo de predicado y definición de la configuración del campo {#add-edit-a-predicate-field-and-define-field-settings}

Puede añadir o editar campos y definir o actualizar su configuración:

1. [Abra la configuración personalizada](#creating-opening-a-customized-configuration) para actualizarla.
1. Si desea agregar un nuevo campo, abra la ficha **Seleccionar predicado** y arrastre el predicado requerido a la ubicación requerida. Por ejemplo, el **Predicado de intervalo de fechas**:

   ![agregar un predicado](assets/csf-add-predicate.png)

1. En función de si:

   * Va a añadir un nuevo campo:

     Después de agregar el predicado, se abre la ficha **Configuración** y se muestran las propiedades que se pueden definir.

   * Desea actualizar un predicado existente:

     Seleccione el campo de predicado (a la derecha) y, a continuación, abra la ficha **Configuración**.

   Por ejemplo, la configuración del **Predicado de intervalo de fechas**:

   ![modificar predicado](assets/csf-modify-predicate.png)

1. Realice los cambios según sea necesario y confirme con **Listo**. Los cambios se podrán ver la próxima vez que se utilice la configuración.

### Previsualización de la configuración de búsqueda {#previewing-the-search-configuration}

1. Seleccione el icono Vista previa:

   ![icono de vista previa](assets/csf-preview-icon.png)

1. Muestra los formularios de búsqueda tal y como se muestran (totalmente expandidos) en la columna Buscar de la consola adecuada.

   ![formulario de vista previa](assets/csf-preview-form.png)

1. **Cierre** la vista previa para devolver y finalizar la configuración.

### Eliminación de un campo de predicado {#deleting-a-predicate-field}

1. [Abra la configuración personalizada](#creating-opening-a-customized-configuration) para actualizarla.
1. Seleccione el campo de predicado (a la derecha), abra la ficha **Configuración** y, a continuación, seleccione el icono **Eliminar** (abajo a la izquierda).

   ![icono de eliminación](assets/csf-delete-icon.png)

1. Un cuadro de diálogo solicitará confirmación de la acción de eliminación.

1. Confirme este y cualquier otro cambio con **Listo**.

### Eliminación de una configuración (para restablecer los valores predeterminados) {#deleting-a-configuration-to-reinstate-the-default}

Una vez que haya personalizado una configuración, esto anulará los valores predeterminados. Puede restablecer la configuración predeterminada eliminando la configuración personalizada.

>[!NOTE]
>
>No puede eliminar las configuraciones predeterminadas.

La eliminación de una configuración personalizada se realiza desde la consola:

1. Seleccione la configuración necesaria (por ejemplo, **Editor de páginas (búsqueda de párrafos)**) y, a continuación, el icono **Eliminar** de la barra de herramientas:

   ![restaurar predeterminado](assets/csf-restore-default.png)

1. La configuración personalizada se elimina y se restaura el valor predeterminado (esto se indica con la reaparición del símbolo de candado en la consola).

### Adición de predicados de opciones {#adding-options-predicates}

Los predicados de opciones (Options, Options, Property) permiten configurar un elemento para buscarlo. Normalmente se utilizan para buscar algo directamente debajo de la página; por ejemplo, una propiedad en el nodo de la página.

El siguiente ejemplo (para buscar según la plantilla utilizada para crear una página), ilustra los pasos involucrados:

1. Cree el nodo que define la propiedad en la que se va a buscar.

   Necesita un nodo raíz que contenga definiciones de las opciones individuales que deben estar disponibles para el usuario.

   Los nodos de las opciones individuales necesitan las propiedades:

   * `jcr:title`: etiqueta de campo que se mostrará en el carril de búsqueda
   * `value`: el valor de propiedad en el que se va a buscar

   ![Definición de predicado](assets/csf-options-predicate-01.png)

   >[!NOTE]
   >
   >Usted ***no debe*** cambiar nada en la ruta de acceso `/libs`.
   >
   >Esto se debe a que el contenido de `/libs` se sobrescribirá la próxima vez que actualice la instancia (y es posible que se sobrescriba al aplicar una revisión o un paquete de características).
   >
   >El método recomendado para la configuración y otros cambios es:
   >
   >1. Vuelva a crear el elemento requerido, tal como existe en `/libs`, en `/apps`. En este caso de:
   >1. `/libs/cq/gui/content/common/options/predicates`
   >1. Realizar cambios en `/apps.`

1. Abra la consola **Buscar en Forms** y seleccione la configuración que desee actualizar. Por ejemplo, **Carril de búsqueda de administración de sitios**. Luego selecciona **Editar**.

1. Dependiendo de la configuración, agregue **Options** u **Options Property** a la configuración.
1. Actualice los campos, en particular:

   * **Nombre de propiedad**

     Especifica la propiedad del nodo que se va a buscar en los nodos de destino. Por ejemplo:

     `jcr:content/cq:template`

   * **Ruta del nodo de opción**

     Seleccione la ruta donde se guardan las opciones. Por ejemplo:

     `/apps/cq/gui/content/common/options/predicates/templatetype`

   ![Predicados de opción](assets/csf-options-predicate-02.png)

1. Seleccione **Listo** para guardar la configuración.
1. Vaya a la consola adecuada (en este ejemplo, **Sitios**) y abra el carril **Buscar - Filtros**. Los formularios de búsqueda recién definidos, junto con las distintas opciones, están visibles. Seleccione la opción necesaria para ver los resultados de búsqueda.

   ![opciones en uso](assets/csf-options-usage.png)


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
   <td>Permisos de lectura y escritura en el nodo <code>/apps </code>.</td>
  </tr>
  <tr>
   <td>Eliminar</td>
   <td>Permisos de lectura, escritura y eliminación en el nodo <code>/apps</code></td>
  </tr>
  <tr>
   <td>Vista previa</td>
   <td>Permisos de lectura, escritura y eliminación en el nodo <code>/var/dam/content</code>.<br /> Permisos de lectura y escritura en el nodo <code>/apps</code>.</td>
  </tr>
 </tbody>
</table>
