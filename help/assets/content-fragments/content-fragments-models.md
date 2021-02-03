---
title: Modelos de fragmento de contenido
description: Los modelos de fragmentos de contenido se utilizan para crear fragmentos de contenido con contenido estructurado.
translation-type: tm+mt
source-git-commit: 3538c03a6a455cd22423ca5a4fd69c1fe57b3e5e
workflow-type: tm+mt
source-wordcount: '2156'
ht-degree: 7%

---


# Modelos de fragmento de contenido {#content-fragment-models}

Los modelos de fragmento de contenido definen la estructura del contenido para los [fragmentos de contenido](/help/assets/content-fragments/content-fragments.md).

Para utilizar los modelos de fragmento de contenido:

1. [Habilitar la funcionalidad del modelo de fragmentos de contenido para su instancia](/help/assets/content-fragments/content-fragments-configuration-browser.md)
1. [Cree](#creating-a-content-fragment-model) y  [configure](#defining-your-content-fragment-model) los modelos de fragmentos de contenido
1. [Habilite los ](#enabling-disabling-a-content-fragment-model) modelos de fragmento de contenido para utilizarlos al crear fragmentos de contenido para utilizarlos al crear fragmentos de contenido
1. [Para permitir los modelos de fragmento de contenido en las ](#allowing-content-fragment-models-assets-folder) carpetas de recursos necesarias, configure  **directivas**.

## Creación de un modelo de fragmento de contenido {#creating-a-content-fragment-model}

1. Vaya a **Herramientas**, **Recursos** y, a continuación, abra **Modelos de fragmento de contenido**.
1. Vaya a la carpeta correspondiente a su [configuración](/help/assets/content-fragments/content-fragments-configuration-browser.md).
1. Utilice **Crear** para abrir el asistente.

   >[!CAUTION]
   >
   >Si el [uso de modelos de fragmento de contenido no se ha habilitado](/help/assets/content-fragments/content-fragments-configuration-browser.md), la opción **Crear** no estará disponible.

1. Especifique el **Título del modelo**. También puede agregar **Etiquetas**, una **Descripción** y seleccionar **Habilitar modelo** para [habilitar el modelo](#enabling-disabling-a-content-fragment-model) si es necesario.

   ![título y descripción](assets/cfm-models-02.png)

1. Utilice **Crear** para guardar el modelo vacío. Un mensaje indicará el éxito de la acción, puede seleccionar **Abrir** para editar inmediatamente el modelo o **Listo** para volver a la consola.

## Definición del modelo de fragmento de contenido {#defining-your-content-fragment-model}

El modelo de fragmento de contenido define eficazmente la estructura de los fragmentos de contenido resultantes mediante una selección de **[tipos de datos](#data-types)**. Con el editor de modelos puede agregar instancias de los tipos de datos y luego configurarlas para crear los campos necesarios:

>[!CAUTION]
>
>La edición de un modelo de fragmento de contenido existente puede afectar a los fragmentos dependientes.

1. Vaya a **Herramientas**, **Recursos** y, a continuación, abra **Modelos de fragmento de contenido**.

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

   * Una vez agregado el campo al modelo, el panel derecho mostrará las **Propiedades** que se pueden definir para ese tipo de datos en particular. Aquí puede definir lo que se necesita para ese campo.

      * Muchas propiedades se explican por sí solas. Para obtener más información, consulte [Propiedades](#properties).
      * Al escribir una **etiqueta de campo** se completará automáticamente el **nombre de propiedad**, si está vacío, y se podrá actualizar manualmente después.

      Por ejemplo:

      ![propiedades de campo](assets/cfm-models-05.png)


1. **Quitar un campo**

   Seleccione el campo requerido y toque o haga clic en el icono de papelera. Se le solicitará que confirme la acción.

   ![elimina](assets/cfm-models-06.png)

1. Añada todos los campos obligatorios y defina las propiedades relacionadas, según sea necesario. Por ejemplo:

   ![save](assets/cfm-models-07.png)

1. Seleccione **Guardar** para mantener la definición.

## Tipos de datos {#data-types}

Hay disponible una selección de tipos de datos para definir el modelo:

* **Texto de línea única**
   * Añadir uno o varios campos de una sola línea de texto; se puede definir la longitud máxima
* **Texto multilínea**
   * Área de texto que puede ser Texto enriquecido, Texto sin formato o Marcado
* **Número**
   * Añadir uno o varios campos numéricos
* **Booleano**
   * Añadir una casilla de verificación booleana
* **Fecha y hora**
   * Añadir una fecha y/o hora
* **Enumeración**
   * Añadir un conjunto de casillas de verificación, botones de opción o campos desplegables
* **Etiquetas**
   * Permite a los autores de fragmentos acceder y seleccionar áreas de etiquetas
* **Referencia de contenido**
   * Referencias a otro contenido, de cualquier tipo; se puede utilizar para [crear contenido anidado](#using-references-to-form-nested-content)
* **Referencia al fragmento**
   * Hace referencia a otros fragmentos de contenido; se puede utilizar para [crear contenido anidado](#using-references-to-form-nested-content)
   * El tipo de datos se puede configurar para permitir que los autores de fragmentos:
      * Edite el fragmento al que se hace referencia directamente.
      * Crear un nuevo fragmento de contenido, basado en el modelo adecuado
* **Objeto JSON**
   * Permite al autor del fragmento de contenido introducir sintaxis JSON en los elementos correspondientes de un fragmento.
      * Para permitir que AEM almacene JSON directo que ha copiado/pegado desde otro servicio.
      * El JSON se pasará y se emitirá como JSON en GraphQL.
      * Incluye resaltado de sintaxis JSON, autocompletado y resaltado de errores en el editor de fragmentos de contenido.

## Propiedades {#properties}

Muchas propiedades se explican por sí mismas, para determinadas propiedades, a continuación se proporcionan más detalles:

* **Representar**
comoLas diversas opciones para realizar o procesar el campo en un fragmento. A menudo, esto le permite definir si el autor verá una sola instancia del campo o se le permitirá crear varias instancias.

* **Etiqueta de**
campoIntroducción de un 
**Field** Labelwill generará automáticamente un Nombre **de** propiedad, que se puede actualizar manualmente si es necesario.

* **La validación**
de ValidationBasic está disponible mediante mecanismos como la propiedad  **** Requiredproperty. Algunos tipos de datos tienen campos de validación adicionales. Consulte [Validación](#validation) para obtener más detalles.

* Para el tipo de datos **Texto multilínea** es posible definir el **tipo predeterminado** como:

   * **Texto enriquecido**
   * **Markdown**
   * **Texto sin formato**

   Si no se especifica, se utiliza el valor predeterminado **Texto enriquecido** para este campo.

   Cambiar el **tipo predeterminado** en un modelo de fragmento de contenido solo surtirá efecto en un fragmento de contenido existente relacionado después de que dicho fragmento se abra en el editor y se guarde.

* ****
UniqueContent (para el campo específico) debe ser único en todos los fragmentos de contenido creados a partir del modelo actual.

   Se utiliza para garantizar que los autores de contenido no puedan repetir contenido ya agregado en otro fragmento del mismo modelo.

   Por ejemplo, un campo **Texto de una sola línea** llamado `Country` en el Modelo de fragmentos de contenido no puede tener el valor `Japan` en dos fragmentos de contenido dependientes. Se emitirá una advertencia cuando se intente la segunda instancia.

   >[!NOTE]
   Se garantiza la unicidad por raíz de idioma.

   >[!NOTE]
   Las variaciones pueden tener el mismo valor *único* que las variaciones del mismo fragmento, pero no el mismo valor que se utiliza en cualquier variación de otros fragmentos.

* ****
TranslatableSi activa la casilla &quot;Translatable&quot; en un campo del editor de modelos CF, se activará la casilla

   * Asegúrese de que el nombre de propiedad del campo se agrega en la configuración de traducción, contexto `/content/dam/<tenant>`, si no está presente.
   * Para GraphQL: establezca una propiedad `<translatable>` en el campo Fragmento de contenido en `yes` para permitir el filtro de consulta GraphQL para la salida JSON con solo contenido traducible.

* Consulte **[Referencia de fragmento (fragmentos anidados)](#fragment-reference-nested-fragments)** para obtener más información sobre ese tipo de datos específico y sus propiedades.

## Validación {#validation}

Varios tipos de datos ahora incluyen la posibilidad de definir los requisitos de validación cuando se introduce contenido en el fragmento resultante:

* **Texto de línea única**
   * Comparar con un regex predefinido.
* **Número**
   * Compruebe si hay valores específicos.
* **Referencia de contenido**
   * Compruebe los tipos de contenido específicos.
   * Solo se puede hacer referencia a recursos de un tamaño de archivo especificado o más pequeño.
   * Solo se puede hacer referencia a las imágenes que se encuentran dentro de un intervalo predefinido de anchura y/o altura (en píxeles).
* **Referencia al fragmento**
   * Pruebe un modelo de fragmento de contenido específico.

<!--
  * Only predefined file types can be referenced.
  * No more than the predefined number of assets can be referenced. 
  * No more than the predefined number of fragments can be referenced.
-->

## Uso de referencias para formar contenido anidado {#using-references-to-form-nested-content}

Los fragmentos de contenido pueden formar contenido anidado mediante cualquiera de los siguientes tipos de datos:

* **[Referencia de contenido](#content-reference)**
   * Proporciona una referencia sencilla a otro contenido; de cualquier tipo.
   * Se puede configurar para una o varias referencias (en el fragmento resultante).

* **[Referencia](#fragment-reference-nested-fragments)**  de fragmento (fragmentos anidados)
   * Hace referencia a otros fragmentos, según los modelos específicos especificados.
   * Permite incluir o recuperar datos estructurados.

      >[!NOTE]
      Este método es de particular interés en conjunto con [Envío de contenido sin cabeza que utiliza fragmentos de contenido con GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).
   * Se puede configurar para una o varias referencias (en el fragmento resultante).

>[!NOTE]
AEM tiene una protección contra las recurrencias para:
* Referencias de contenido
Esto evita que el usuario agregue una referencia al fragmento actual. Esto puede llevar a un cuadro de diálogo de selección de referencia de fragmento vacío.

* Referencias de fragmento en GraphQL
Si crea una consulta profunda que devuelve varios fragmentos de contenido a los que se hace referencia, devolverá null en la primera incidencia.


### Referencia de contenido {#content-reference}

La Referencia de contenido le permite procesar contenido de otra fuente; por ejemplo, fragmento de imagen o contenido.

Además de las propiedades estándar, puede especificar:

* La **Ruta de raíz** para cualquier contenido al que se haga referencia.
* Tipos de contenido a los que se puede hacer referencia.
* Limitaciones para los tamaños de archivo.
* Restricciones de imagen.
   <!-- Check screenshot - might need update -->
   ![Referencia de contenido](assets/cfm-content-reference.png)

### Referencia de fragmento (fragmentos anidados) {#fragment-reference-nested-fragments}

La referencia de fragmento hace referencia a uno o varios fragmentos de contenido. Esta función es de particular interés cuando se recupera contenido para su uso en la aplicación, ya que le permite recuperar datos estructurados con varias capas.

Por ejemplo:

* Un modelo que define los detalles de un empleado; entre ellos se incluyen:
   * Referencia al modelo que define al empleador (compañía)

```xml
type EmployeeModel {
    name: String
    firstName: String
    company: CompanyModel
}

type CompanyModel {
    name: String
    street: String
    city: String
}
```

>[!NOTE]
Esto es de particular interés en conjunto con [Envío de contenido sin cabeza mediante fragmentos de contenido con GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).

Además de las propiedades estándar, puede definir:

* **Procesar como**:

   * **multicampo** : el autor del fragmento puede crear varias referencias individuales.

   * **fragmentación** : permite al autor del fragmento seleccionar una sola referencia a un fragmento

* **Modelo**
TipoSe pueden seleccionar varios modelos. Al crear el fragmento de contenido, debe haberse creado cualquier fragmento al que se hace referencia con estos modelos.

* **Ruta**
raízEspecifica una ruta raíz para los fragmentos a los que se hace referencia.

* **Permitir creación de fragmentos**

   Esto permitirá al autor del fragmento crear un nuevo fragmento basado en el modelo adecuado.

   * **fragmentreferencecomposite** : permite al autor del fragmento crear un compuesto seleccionando varios fragmentos

   <!-- Check screenshot - might need update -->
   ![Referencia al fragmento](assets/cfm-fragment-reference.png)

>[!NOTE]
Se ha establecido un mecanismo de protección contra las recurrencias. Prohíbe que el usuario seleccione el fragmento de contenido actual en la Referencia de fragmento. Esto puede llevar a un cuadro de diálogo de selección de referencia de fragmento vacío.
También existe una protección de periodicidad para las referencias de fragmento en GraphQL. Si crea una consulta profunda en dos fragmentos de contenido que se hacen referencia entre sí, devolverá null.

## Activación o desactivación de un modelo de fragmento de contenido {#enabling-disabling-a-content-fragment-model}

Para un control total sobre el uso de los modelos de fragmento de contenido, tienen un estado que puede establecer.

### Activación de un modelo de fragmento de contenido {#enabling-a-content-fragment-model}

Una vez creado un modelo, debe habilitarse para que:

* Está disponible para selección al crear un nuevo fragmento de contenido.
* Se puede hacer referencia desde un modelo de fragmento de contenido.
* Está disponible para GraphQL; así que se genera el esquema.

Para habilitar un modelo marcado como:

* **Borrador** : mew (nunca habilitado).
* **Deshabilitado** : se ha deshabilitado específicamente.

Utilice la opción **Habilitar** desde:

* La barra de herramientas superior, cuando se selecciona el modelo requerido.
* La acción rápida correspondiente (pase el ratón sobre el modelo requerido).

![Habilitar un modelo borrador o deshabilitado](assets/cfm-status-enable.png)

### Desactivación de un modelo de fragmento de contenido {#disabling-a-content-fragment-model}

También se puede desactivar un modelo para que:

* El modelo ya no está disponible como base para crear *nuevos* fragmentos de contenido.
* However:
   * El esquema GraphQL se sigue generando y sigue siendo cuestionable (para evitar afectar a la API JSON).
   * Cualquier fragmento de contenido basado en el modelo puede ser consultado y devuelto desde el extremo GraphQL.
* Ya no se puede hacer referencia al modelo, pero las referencias existentes se mantienen intactas y se pueden seguir consultando y devolviendo desde el extremo GraphQL.

Para deshabilitar un modelo marcado como **Habilitado**, utilice la opción **Deshabilitar** desde:

* La barra de herramientas superior, cuando se selecciona el modelo requerido.
* La acción rápida correspondiente (pase el ratón sobre el modelo requerido).

![Deshabilitar un modelo habilitado](assets/cfm-status-disable.png)

## Permitir modelos de fragmento de contenido en la carpeta de recursos {#allowing-content-fragment-models-assets-folder}

Para implementar la administración de contenido, puede configurar **Directivas** en la carpeta Recursos para controlar qué modelos de fragmento de contenido se permiten para la creación de fragmentos en esa carpeta.

>[!NOTE]
El mecanismo es similar a [permitir plantillas de página](/help/sites-cloud/authoring/features/templates.md#allowing-a-template-author) para una página, y sus elementos secundarios, en propiedades avanzadas de una página.

Para configurar las **directivas** para **Modelos de fragmento de contenido permitidos**:

1. Desplácese y abra **Propiedades** para la carpeta de recursos requerida.

1. Abra la ficha **Directivas**, donde puede configurar:

   * **Heredado de`<folder>`**

      Las directivas se heredan automáticamente al crear nuevas carpetas secundarias; la directiva se puede reconfigurar (y la herencia se rompe) si las subcarpetas necesitan permitir modelos diferentes a la carpeta principal.

   * **Modelos de fragmento de contenido permitidos por ruta**

      Se pueden permitir varios modelos.

   * **Modelos de fragmento de contenido permitidos por etiqueta**

      Se pueden permitir varios modelos.
   ![Directiva del modelo de fragmento de contenido](assets/cfm-model-policy-assets-folder.png)

1. **** Guarde los cambios.

Los modelos de fragmento de contenido permitidos para una carpeta se resuelven de la siguiente manera:
* Las **directivas** para **Modelos de fragmento de contenido permitidos**.
* Si está vacío, intente determinar la política utilizando las reglas de herencia.
* Si la cadena de herencia no proporciona un resultado, consulte la configuración **Cloud Services** de esa carpeta (también primero directamente y luego mediante herencia).
* Si ninguno de los anteriores arroja resultados, no hay modelos permitidos para esa carpeta.

## Eliminación de un modelo de fragmento de contenido {#deleting-a-content-fragment-model}

>[!CAUTION]
La eliminación de un modelo de fragmento de contenido puede afectar a los fragmentos dependientes.

Para eliminar un modelo de fragmento de contenido:

1. Vaya a **Herramientas**, **Recursos** y, a continuación, abra **Modelos de fragmento de contenido**.

1. Vaya a la carpeta que contiene el modelo de fragmentos de contenido.
1. Seleccione el modelo, seguido de **Eliminar** en la barra de herramientas.

   >[!NOTE]
   Si se hace referencia al modelo, se mostrará una advertencia. Tome las medidas adecuadas.

## Publicación de un modelo de fragmento de contenido {#publishing-a-content-fragment-model}

Los modelos de fragmentos de contenido deben publicarse cuando se publiquen fragmentos de contenido dependientes o antes de hacerlo.

Para publicar un modelo de fragmento de contenido:

1. Vaya a **Herramientas**, **Recursos** y, a continuación, abra **Modelos de fragmento de contenido**.

1. Vaya a la carpeta que contiene el modelo de fragmentos de contenido.
1. Seleccione el modelo, seguido de **Publicar** en la barra de herramientas.
El estado publicado se indicará en la consola.

   >[!NOTE]
   Si publica un fragmento de contenido para el que el modelo aún no se ha publicado, una lista de selección lo indicará y el modelo se publicará con el fragmento.

## Cancelación de la publicación de un modelo de fragmento de contenido {#unpublishing-a-content-fragment-model}

Los modelos de fragmentos de contenido se pueden cancelar si ningún fragmento hace referencia a ellos.

Para cancelar la publicación de un modelo de fragmento de contenido:

1. Vaya a **Herramientas**, **Recursos** y, a continuación, abra **Modelos de fragmento de contenido**.

1. Vaya a la carpeta que contiene el modelo de fragmentos de contenido.
1. Seleccione el modelo, seguido de **Cancelar la publicación** en la barra de herramientas.
El estado publicado se indicará en la consola.
