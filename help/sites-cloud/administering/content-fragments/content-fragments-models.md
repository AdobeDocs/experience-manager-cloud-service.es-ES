---
title: Modelos de fragmento de contenido
description: Descubra cómo los modelos de fragmentos de contenido sirven de base para los fragmentos de contenido en AEM. Permiten crear contenido estructurado para utilizarlo en envíos sin encabezado o en la creación de páginas.
source-git-commit: a06024b4d4b6e5e750ed4c1e27f55283513b78a2
workflow-type: tm+mt
source-wordcount: '2908'
ht-degree: 7%

---

# Modelos de fragmento de contenido {#content-fragment-models}

Los modelos de fragmento de contenido de AEM definen la estructura del contenido del [fragmentos de contenido](/help/sites-cloud/administering/content-fragments/content-fragments.md). Pueden utilizarse para la creación de páginas o como base para el contenido sin encabezado.

Para usar modelos de fragmento de contenido:

1. [Habilitar la funcionalidad del modelo de fragmento de contenido para la instancia](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md)
1. [Crear](#creating-a-content-fragment-model)y [configure](#defining-your-content-fragment-model), los modelos de fragmento de contenido
1. [Habilitar los modelos de fragmento de contenido](#enabling-disabling-a-content-fragment-model) para usar al crear fragmentos de contenido para utilizarlos al crear fragmentos de contenido
1. [Permitir los modelos de fragmento de contenido en las carpetas de recursos necesarias](#allowing-content-fragment-models-assets-folder) configurando **Políticas**.

## Creación de un modelo de fragmento de contenido {#creating-a-content-fragment-model}

1. Vaya a **Herramientas**, **General** y, a continuación, abra **Modelos de fragmento de contenido**.
1. Vaya a la carpeta adecuada para su [configuración o subconfiguración](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md).
1. Uso **Crear** para abrir el asistente.

   >[!CAUTION]
   >
   >Si [no se ha habilitado el uso de modelos de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md), la opción **Crear** no estará disponible.

1. Especifique el **Título del modelo**. También puede agregar **Etiquetas**, **Descripción** y seleccione **Habilitar modelo** a [activar el modelo](#enabling-disabling-a-content-fragment-model) si es necesario.

   ![título y descripción](assets/cfm-models-02.png)

1. Uso **Crear** para guardar el modelo vacío. Un mensaje indicará el éxito de la acción; puede seleccionar **Apertura** para editar inmediatamente el modelo, o **Listo** para volver a la consola.

## Definición del modelo de fragmento de contenido {#defining-your-content-fragment-model}

El modelo de fragmento de contenido define efectivamente la estructura de los fragmentos de contenido resultantes mediante una selección de **[Tipos de datos](#data-types)**. Con el editor de modelos puede añadir instancias de los tipos de datos y, a continuación, configurarlas para crear los campos obligatorios:

>[!CAUTION]
>
>Editar un modelo de fragmento de contenido existente puede afectar a los fragmentos dependientes.

1. Vaya a **Herramientas**, **General** y, a continuación, abra **Modelos de fragmento de contenido**.

1. Vaya a la carpeta que contiene el modelo de fragmento de contenido.
1. Abra el modelo necesario para **Editar**; utilice la acción rápida o seleccione el modelo y, a continuación, la acción en la barra de herramientas.

   Una vez abierto, el editor de modelos muestra:

   * a la izquierda: campos ya definidos
   * right: **Tipos de datos** disponibles para crear campos (y **Propiedades** para su uso una vez creados los campos)

   >[!NOTE]
   >
   >Cuando un campo es **obligatorio**, la **etiqueta** indicada en el panel izquierdo se marca con un asterisco (**&#42;**).

![propiedades](assets/cfm-models-03.png)

1. **Adición de un campo**

   * Arrastre un tipo de datos requerido a la ubicación requerida para un campo:

      ![tipo de datos a campo](assets/cfm-models-04.png)

   * Una vez agregado un campo al modelo, el panel derecho mostrará la variable **Propiedades** que se puede definir para ese tipo de datos en particular. Aquí puede definir lo que se requiere para ese campo.

      * Muchas propiedades se explican por sí mismas; para obtener más información, consulte [Propiedades](#properties).
      * Escribir un **Etiqueta de campo** completará automáticamente el **Nombre de propiedad**  - si está vacío, y se puede actualizar manualmente posteriormente.

         >[!CAUTION]
         >
         >Al actualizar manualmente la propiedad **Nombre de propiedad** para un tipo de datos, tenga en cuenta que los nombres solo deben contener caracteres latinos, dígitos numéricos y guiones bajos &quot;_&quot; como caracteres especiales.
         >
         >Si los modelos creados en versiones anteriores de AEM contienen caracteres no permitidos, elimine o actualice dichos caracteres.
      Por ejemplo:

      ![propiedades del campo](assets/cfm-models-05.png)


1. **Eliminación de un campo**

   Seleccione el campo requerido y, a continuación, toque o haga clic en el icono de la papelera. Se le solicitará que confirme la acción.

   ![elimina](assets/cfm-models-06.png)

1. Agregue todos los campos obligatorios y defina las propiedades relacionadas, según sea necesario. Por ejemplo:

   ![save](assets/cfm-models-07.png)

1. Select **Guardar** para mantener la definición.

## Tipos de datos {#data-types}

Hay disponible una selección de tipos de datos para definir el modelo:

* **Texto de línea única**
   * Añada uno o más campos de una sola línea de texto; se puede definir la longitud máxima
* **Texto multilínea**
   * Área de texto que puede ser Texto enriquecido, Texto sin formato o Marcado
* **Número**
   * Agregar uno o más campos numéricos
* **Boolean**
   * Agregar una casilla de verificación booleana
* **Fecha y hora**
   * Agregar una fecha y/o hora
* **Lista desglosada**
   * Agregar un conjunto de casillas de verificación, botones de opción o campos desplegables
* **Etiquetas**
   * Permite a los autores de fragmentos acceder y seleccionar áreas de etiquetas
* **Referencia de contenido**
   * Referencias a otros contenidos, de cualquier tipo; se puede usar para [crear contenido anidado](#using-references-to-form-nested-content)
   * Si se hace referencia a una imagen, puede optar por mostrar una miniatura
* **Referencia al fragmento**
   * Referencias a otros fragmentos de contenido; se puede usar para [crear contenido anidado](#using-references-to-form-nested-content)
   * El tipo de datos se puede configurar para que los autores de fragmentos puedan:
      * Edite directamente el fragmento al que se hace referencia.
      * Cree un nuevo fragmento de contenido basado en el modelo apropiado
* **Objeto JSON**
   * Permite al autor del fragmento de contenido introducir la sintaxis JSON en los elementos correspondientes de un fragmento.
      * Para permitir que AEM almacene el JSON directo que ha copiado/pegado desde otro servicio.
      * El JSON se pasará y se emitirá como JSON en GraphQL.
      * Incluye resaltado de sintaxis JSON, autocompletado y resaltado de errores en el editor de fragmentos de contenido.
* **Marcador de posición de pestaña**
   * Permite la introducción de fichas para utilizarlas al editar el contenido del fragmento de contenido.
Esto se mostrará como un divisor en el editor de modelos, separando secciones de la lista de tipos de datos de contenido. Cada instancia representa el inicio de una nueva pestaña.
En el editor de fragmentos, cada instancia aparecerá como una pestaña.

      >[!NOTE]
      >
      >Este tipo de datos se utiliza exclusivamente para dar formato; el esquema AEM GraphQL lo ignora.

## Propiedades {#properties}

Muchas propiedades se explican por sí mismas; para determinadas propiedades, a continuación se proporcionan detalles adicionales:

* **Nombre de propiedad**

   Cuando actualice manualmente esta propiedad para un tipo de datos, tenga en cuenta que los nombres **must** contain *only* Caracteres latinos, dígitos numéricos y guiones bajos &quot;_&quot; como caracteres especiales.

   >[!CAUTION]
   >
   >Si los modelos creados en versiones anteriores de AEM contienen caracteres no permitidos, elimine o actualice dichos caracteres.

* **Representar como**
Las distintas opciones para realizar/procesar el campo en un fragmento. A menudo, esto le permite definir si el autor verá una sola instancia del campo o si se le permitirá crear varias instancias.

* **Etiqueta de campo**
Introducción de un 
**Etiqueta de campo** generará automáticamente un **Nombre de propiedad**, que se puede actualizar manualmente si es necesario.

* **Validación**
La validación básica está disponible mediante mecanismos como **Requerido** propiedad. Algunos tipos de datos tienen campos de validación adicionales. Consulte [Validación](#validation) para obtener más información.

* Para el tipo de datos **Texto multilínea** es posible definir el **tipo predeterminado** como:

   * **Texto enriquecido**
   * **Markdown**
   * **Texto sin formato**

   Si no se especifica, el valor predeterminado **Texto enriquecido** se utiliza para este campo.

   Cambiar el **tipo predeterminado** en un modelo de fragmento de contenido solo surtirá efecto en un fragmento de contenido existente relacionado después de que dicho fragmento se abra en el editor y se guarde.

* **Único**
El contenido (para el campo específico) debe ser único en todos los fragmentos de contenido creados a partir del modelo actual.

   Se utiliza para garantizar que los autores de contenido no puedan repetir el contenido ya añadido en otro fragmento del mismo modelo.

   Por ejemplo, una **Texto de una sola línea** campo llamado `Country` en el modelo de fragmento de contenido no puede tener el valor `Japan` en dos fragmentos de contenido dependientes. Se emitirá una advertencia cuando se intente la segunda instancia.

   >[!NOTE]
   >
   >La unicidad se garantiza por cada raíz de idioma.

   >[!NOTE]
   >
   >Las variaciones pueden tener el mismo valor *único* como variaciones del mismo fragmento, pero no del mismo valor que se utiliza en cualquier variación de otros fragmentos.

* Consulte **[Referencia de contenido](#content-reference)** para obtener más información sobre ese tipo de datos específico y sus propiedades.

* Consulte **[Referencia de fragmento (fragmentos anidados)](#fragment-reference-nested-fragments)** para obtener más información sobre ese tipo de datos específico y sus propiedades.

* **Traducible**

   Marque la **Translatable** en un campo del editor del modelo de fragmento de contenido:

   * Asegúrese de que el nombre de propiedad del campo se agrega a la configuración de traducción, contexto `/content/dam/<sites-configuration>`, si no está presente.
   * Para GraphQL: establezca un `<translatable>` en el campo Fragmento de contenido para `yes`, para permitir el filtro de consulta de GraphQL para la salida JSON con solo contenido traducible.

## Validación {#validation}

Varios tipos de datos ahora incluyen la posibilidad de definir los requisitos de validación cuando el contenido se introduce en el fragmento resultante:

* **Texto de línea única**
   * Compare con un regex predefinido.
* **Número**
   * Compruebe si hay valores específicos.
* **Referencia de contenido**
   * Pruebe tipos de contenido específicos.
   * Solo se puede hacer referencia a los recursos con un tamaño de archivo especificado o más pequeño.
   * Solo se puede hacer referencia a las imágenes con un intervalo predefinido de anchura y/o altura (en píxeles).
* **Referencia al fragmento**
   * Pruebe un modelo de fragmento de contenido específico.

## Uso de referencias para formar contenido anidado {#using-references-to-form-nested-content}

Los fragmentos de contenido pueden formar contenido anidado mediante cualquiera de los siguientes tipos de datos:

* **[Referencia de contenido](#content-reference)**
   * Proporciona una sencilla referencia a otro contenido; de cualquier tipo.
   * Se puede configurar para una o varias referencias (en el fragmento resultante).

* **[Referencia de fragmento](#fragment-reference-nested-fragments)** (Fragmentos anidados)
   * Hace referencia a otros fragmentos, según los modelos específicos especificados.
   * Permite incluir o recuperar datos estructurados.

      >[!NOTE]
      >
      >Este método reviste especial interés en conjunción con [Entrega de contenido sin objetivos mediante fragmentos de contenido con GraphQL](/help/sites-cloud/administering/content-fragments/content-fragments-graphql.md).
   * Se puede configurar para una o varias referencias (en el fragmento resultante).

>[!NOTE]
>
>AEM tiene una protección contra recurrencias para:
>
>* Referencias de contenido
   >  Esto evita que el usuario agregue una referencia al fragmento actual. Esto puede dar lugar a un cuadro de diálogo vacío del selector de referencia de fragmento.
>
>* Referencias de fragmento en GraphQL
   >  Si crea una consulta profunda que devuelve varios fragmentos de contenido a los que se hace referencia entre sí, devolverá un valor nulo en la primera incidencia.


### Referencia de contenido {#content-reference}

La referencia de contenido le permite procesar contenido de otra fuente; por ejemplo, imagen o fragmento de contenido.

Además de las propiedades estándar, puede especificar:

* La variable **Ruta raíz** para cualquier contenido referenciado
* Tipos de contenido a los que se puede hacer referencia
* Limitaciones de los tamaños de archivo
* Si se hace referencia a una imagen:
   * Mostrar miniatura
   * Restricciones de imagen de altura y anchura

![Referencia de contenido](assets/cfm-content-reference.png)

### Referencia de fragmento (fragmentos anidados) {#fragment-reference-nested-fragments}

La Referencia de fragmento hace referencia a uno o más fragmentos de contenido. Esta función es de especial interés cuando se recupera contenido para utilizarlo en la aplicación, ya que le permite recuperar datos estructurados con varias capas.

Por ejemplo:

* Un modelo que define los detalles de un empleado; entre ellos se incluyen:
   * Referencia al modelo que define al empleador (empresa)

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
>
>Esto reviste especial interés en conjunción con [Entrega de contenido sin objetivos mediante fragmentos de contenido con GraphQL](/help/sites-cloud/administering/content-fragments/content-fragments-graphql.md).

Además de las propiedades estándar, puede definir:

* **Procesar como**:

   * **multifield** - el autor del fragmento puede crear varias referencias individuales,

   * **referencia de fragmentación** : permite al autor del fragmento seleccionar una sola referencia a un fragmento

* **Tipo de modelo**
Se pueden seleccionar varios modelos. Al crear el fragmento de contenido, se debe crear cualquier fragmento referenciado mediante estos modelos.

* **Ruta raíz**
Esto especifica una ruta raíz para los fragmentos a los que se hace referencia.

* **Permitir creación de fragmentos**

   Esto permitirá al autor del fragmento crear un nuevo fragmento basado en el modelo adecuado.

   * **fragmentación referencecomposite** : permite al autor del fragmento crear un compuesto seleccionando varios fragmentos

   ![Referencia al fragmento](assets/cfm-fragment-reference.png)

>[!NOTE]
>
>Existe un mecanismo de protección contra la recurrencia. Prohíbe que el usuario seleccione el fragmento de contenido actual en la Referencia de fragmento. Esto puede dar lugar a un cuadro de diálogo vacío del selector de referencia de fragmento.
>
>También existe una protección contra las recurrencias para las referencias de fragmento en GraphQL. Si crea una consulta profunda en dos fragmentos de contenido que se hacen referencia entre sí, devolverá un valor nulo.

## Modelo de fragmento de contenido: propiedades {#content-fragment-model-properties}

Puede editar el **Propiedades** de un modelo de fragmento de contenido:

* **Básico**
   * **Título de modelo**
   * **Etiquetas**
   * **Descripción**
   * **Cargar imagen**

## Activación o desactivación de un modelo de fragmento de contenido {#enabling-disabling-a-content-fragment-model}

Para obtener un control total sobre el uso de los modelos de fragmento de contenido, estos tienen un estado que puede establecer.

### Activación de un modelo de fragmento de contenido {#enabling-a-content-fragment-model}

Una vez creado un modelo, debe activarse para que:

* Está disponible para selección al crear un nuevo fragmento de contenido.
* Se puede hacer referencia desde un modelo de fragmento de contenido.
* Está disponible para GraphQL; por lo tanto, se genera el esquema .

Para habilitar un modelo marcado como:

* **Borrador** : mew (nunca habilitado).
* **Desactivado** : se ha deshabilitado específicamente.

Utilice la variable **Habilitar** desde:

* La barra de herramientas superior, cuando se selecciona el Modelo requerido.
* La Acción rápida correspondiente (pase el ratón sobre el Modelo requerido).

![Activar un borrador o un modelo desactivado](assets/cfm-status-enable.png)

### Desactivación de un modelo de fragmento de contenido {#disabling-a-content-fragment-model}

Un modelo también se puede desactivar para que:

* El modelo ya no está disponible como base para la creación de *new* Fragmentos de contenido.
* However:
   * El esquema de GraphQL se sigue generando y aún se puede consultar (para evitar afectar a la API de JSON).
   * Cualquier fragmento de contenido basado en el modelo se puede consultar y devolver desde el extremo de GraphQL.
* Ya no se puede hacer referencia al modelo, pero las referencias existentes no se tocan y aún se pueden consultar y devolver desde el extremo GraphQL.

Para desactivar un modelo marcado como **Habilitado** utilice el **Deshabilitar** desde:

* La barra de herramientas superior, cuando se selecciona el Modelo requerido.
* La Acción rápida correspondiente (pase el ratón sobre el Modelo requerido).

![Desactivación de un modelo habilitado](assets/cfm-status-disable.png)

## Permitir modelos de fragmento de contenido en la carpeta de recursos {#allowing-content-fragment-models-assets-folder}

Para implementar el control de contenido, puede configurar **Políticas** en la carpeta Assets para controlar qué modelos de fragmento de contenido están permitidos para la creación de fragmentos en esa carpeta.

>[!NOTE]
>
>El mecanismo es similar a [permitir plantillas de página](/help/sites-cloud/authoring/features/templates.md#allowing-a-template-author) para una página, y sus elementos secundarios, en propiedades avanzadas de una página.

Para configurar la variable **Políticas** para **Modelos de fragmento de contenido permitidos**:

1. Navegar y abrir **Propiedades** para la carpeta de recursos necesaria.

1. Abra el **Políticas** , donde puede configurar:

   * **Heredado de`<folder>`**

      Las directivas se heredan automáticamente al crear nuevas carpetas secundarias; la directiva se puede reconfigurar (y la herencia se rompe) si las subcarpetas necesitan permitir modelos diferentes de la carpeta principal.

   * **Modelos de fragmento de contenido permitidos por ruta**

      Se pueden permitir varios modelos.

   * **Modelos de fragmento de contenido permitidos por etiqueta**

      Se pueden permitir varios modelos.
   ![Política del modelo de fragmento de contenido](assets/cfm-model-policy-assets-folder.png)

1. **Guardar** cualquier cambio.

Los modelos de fragmento de contenido permitidos para una carpeta se resuelven de la siguiente manera:
* La variable **Políticas** para **Modelos de fragmento de contenido permitidos**.
* Si está vacío, intente determinar la directiva utilizando las reglas de herencia.
* Si la cadena de herencia no proporciona un resultado, consulte la **Cloud Services** configuración para esa carpeta (primero directamente y luego mediante herencia).
* Si ninguno de los anteriores proporciona ningún resultado, no hay modelos permitidos para esa carpeta.

## Eliminación de un modelo de fragmento de contenido {#deleting-a-content-fragment-model}

>[!CAUTION]
>
>La eliminación de un modelo de fragmento de contenido puede afectar a los fragmentos dependientes.

Para eliminar un modelo de fragmento de contenido:

1. Vaya a **Herramientas**, **General** y, a continuación, abra **Modelos de fragmento de contenido**.

1. Vaya a la carpeta que contiene el modelo de fragmento de contenido.
1. Seleccione el modelo, seguido de **Eliminar** en la barra de herramientas.

   >[!NOTE]
   >
   >Si se hace referencia al modelo, se envía una advertencia. Tome las medidas adecuadas.

## Publicación de un modelo de fragmento de contenido {#publishing-a-content-fragment-model}

Los modelos de fragmento de contenido deben publicarse cuando se publican fragmentos de contenido dependientes, o antes de hacerlo.

Para publicar un modelo de fragmento de contenido:

1. Vaya a **Herramientas**, **General** y, a continuación, abra **Modelos de fragmento de contenido**.

1. Vaya a la carpeta que contiene el modelo de fragmento de contenido.
1. Seleccione el modelo, seguido de **Publicación** en la barra de herramientas.
El estado publicado se indica en la consola.

   >[!NOTE]
   >
   >Si publica un fragmento de contenido para el que el modelo aún no se ha publicado, una lista de selección lo indicará y el modelo se publicará con el fragmento.

## Cancelación de la publicación de un modelo de fragmento de contenido {#unpublishing-a-content-fragment-model}

Los modelos de fragmento de contenido se pueden cancelar si ningún fragmento hace referencia a ellos.

Para cancelar la publicación de un modelo de fragmento de contenido:

1. Vaya a **Herramientas**, **General** y, a continuación, abra **Modelos de fragmento de contenido**.

1. Vaya a la carpeta que contiene el modelo de fragmento de contenido.
1. Seleccione el modelo, seguido de **Cancelar la publicación** en la barra de herramientas.
El estado publicado se indica en la consola.

Si intenta cancelar la publicación de un modelo que actualmente utiliza uno o varios fragmentos, una advertencia de error le informará de lo siguiente:

![Mensaje de error del modelo de fragmento de contenido al cancelar la publicación de un modelo que está en uso](assets/cfm-model-unpublish-error.png)

El mensaje le sugerirá que compruebe el [Referencias](/help/sites-cloud/authoring/getting-started/basic-handling.md#references) para investigar más a fondo:

![Modelo de fragmento de contenido en referencias](assets/cfm-model-references.png)

## Modelos de fragmento de contenido bloqueados (publicados) {#locked-published-content-fragment-models}

Esta función proporciona control para los modelos de fragmento de contenido que se han publicado.

### El reto {#the-challenge}

* Los modelos de fragmento de contenido determinan el esquema de las consultas de GraphQL en AEM.

   * AEM esquemas de GraphQL se crean en cuanto se crea un modelo de fragmento de contenido y pueden existir en entornos de autor y publicación.

   * Los esquemas en la publicación son los más críticos, ya que proporcionan la base para la entrega en directo de contenido de fragmento de contenido en formato JSON.

* Pueden producirse problemas cuando se modifican los modelos de fragmento de contenido o, dicho de otro modo, se editan. Esto significa que el esquema cambia, lo que a su vez puede afectar a las consultas de GraphQL existentes.

* La adición de nuevos campos a un modelo de fragmento de contenido no debería (normalmente) tener ningún efecto perjudicial. Sin embargo, si se modifican los campos de datos existentes (por ejemplo, su nombre) o se eliminan las definiciones de campos, las consultas de GraphQL existentes se romperán al solicitar estos campos.

### Los requisitos {#the-requirements}

* Para concienciar a los usuarios sobre los riesgos que se plantean al editar modelos que ya se utilizan para la entrega de contenido en directo (es decir, modelos que se han publicado).

* Además, para evitar cambios no deseados.

Cualquiera de estos factores podría generar consultas si se vuelven a publicar los modelos modificados.

### La solución {#the-solution}

Para solucionar estos problemas, los modelos de fragmentos de contenido *bloqueado* en modo READ-ONLY en el autor, tan pronto como se hayan publicado. Esto se indica mediante **Bloqueado**:

![Tarjeta del modelo de fragmento de contenido bloqueado](assets/cfm-model-locked.png)

Cuando el modelo es **Bloqueado** (en modo READ-ONLY), puede ver el contenido y la estructura de los modelos, pero no puede editarlos.

Puede administrar **Bloqueado** modelos desde la consola o desde el editor de modelos:

* Consola

   Desde la consola, puede administrar el modo READ-ONLY con el **Desbloquear** y **Bloqueo** acciones de la barra de herramientas:

   ![Barra de herramientas del modelo de fragmento de contenido bloqueado](assets/cfm-model-locked.png)

   * Puede **Desbloquear** un modelo para activar ediciones.

      Si selecciona **Desbloquear** se mostrará una advertencia y debe confirmar la variable **Desbloquear** acción:
      ![Mensaje al desbloquear el modelo de fragmento de contenido](assets/cfm-model-unlock-message.png)

      A continuación, puede abrir el modelo para editarlo.

   * También puede **Bloqueo** el modelo después.
   * Volver a publicar el modelo inmediatamente lo volverá a poner en **Bloqueado** (SOLO LECTURA).

* Editor de modelo

   * Al abrir un modelo bloqueado, se le avisará y se le presentarán tres acciones: **Cancelar**, **Ver solo lectura**, **Editar**:

      ![Mensaje al ver un modelo de fragmento de contenido bloqueado](assets/cfm-model-editor-lock-message.png)

   * Si selecciona **Ver solo lectura** puede ver el contenido y la estructura del modelo:

      ![Ver solo lectura: modelo de fragmento de contenido bloqueado](assets/cfm-model-editor-locked-view-only.png)

   * Si selecciona **Editar** puede editar y guardar las actualizaciones:

      ![Editar: modelo de fragmento de contenido bloqueado](assets/cfm-model-editor-locked-edit.png)

      >[!NOTE]
      >
      >Puede que todavía haya una advertencia en la parte superior, pero es cuando el modelo ya está siendo utilizado por fragmentos de contenido existentes.

   * **Cancelar** le devolverá a la consola.
