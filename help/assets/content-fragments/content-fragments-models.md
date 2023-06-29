---
title: Modelos de fragmentos de contenido (recursos - fragmentos de contenido)
description: AEM Descubra cómo los modelos de fragmentos de contenido sirven de base para su contenido sin encabezado en la creación de fragmentos de contenido y cómo crear fragmentos de contenido con contenido estructurado.
exl-id: fd706c74-4cc1-426d-ab56-d1d1b521154b
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '2901'
ht-degree: 89%

---

# Modelos de fragmento de contenido {#content-fragment-models}

AEM Los modelos de fragmentos de contenido de la definición de la estructura de contenido para su contenido en la [fragmentos de contenido,](/help/assets/content-fragments/content-fragments.md) servir como base del contenido sin encabezado.

Para usar modelos de fragmentos de contenido, haga lo siguiente:

1. [Habilite la funcionalidad de modelos de fragmentos de contenido para la instancia.](/help/assets/content-fragments/content-fragments-configuration-browser.md)
1. [Cree](#creating-a-content-fragment-model) y [configure](#defining-your-content-fragment-model) sus modelos de fragmentos de contenido.
1. [Habilite los modelos de fragmento de contenido](#enabling-disabling-a-content-fragment-model) para usar al crear fragmentos de contenido
1. [Permita los modelos de fragmentos de contenido en las carpetas de recursos necesarias](#allowing-content-fragment-models-assets-folder) configurando **Políticas**.

## Creación de un modelo de fragmento de contenido {#creating-a-content-fragment-model}

1. Vaya a **Herramientas**, **General** y, a continuación, abra **Modelos de fragmentos de contenido**.
1. Vaya a la carpeta adecuada para su [configuración o subconfiguración](/help/assets/content-fragments/content-fragments-configuration-browser.md).
1. Use **Crear** para abrir el asistente.

   >[!CAUTION]
   >
   >Si [no se ha habilitado el uso de modelos de fragmentos de contenido](/help/assets/content-fragments/content-fragments-configuration-browser.md), la opción **Crear** no estará disponible.

1. Especifique el **Título del modelo**. También puede añadir **Etiquetas**, una **Descripción** y seleccionar **Habilitar modelo** para [activar el modelo](#enabling-disabling-a-content-fragment-model), si es necesario.

   ![Título y descripción](assets/cfm-models-02.png)

1. Use **Crear** para guardar el modelo vacío. Un mensaje indica el éxito de la acción. Puede seleccionar **Abrir** para editar de inmediato el modelo o **Listo** para volver a la consola.

## Definición del modelo de fragmento de contenido {#defining-your-content-fragment-model}

El modelo de fragmento de contenido define de manera efectiva la estructura de los fragmentos de contenido resultantes mediante una selección de **[Tipos de datos](#data-types)**. Con el editor de modelos puede añadir instancias de los tipos de datos y, a continuación, configurarlos para crear los campos obligatorios.

>[!CAUTION]
>
>Editar un modelo de fragmento de contenido existente puede afectar a los fragmentos dependientes.

1. Vaya a **Herramientas**, **General** y, a continuación, abra **Modelos de fragmentos de contenido**.

1. Vaya a la carpeta que contiene el modelo de fragmento de contenido.
1. Abra el modelo necesario para **Editar**; utilice la acción rápida o seleccione el modelo y, después, la acción en la barra de herramientas.

   Una vez abierto, el editor de modelos muestra lo siguiente:

   * A la izquierda: los campos ya definidos.
   * A la derecha: los **Tipos de datos** disponibles para crear campos (y **Propiedades** para su uso una vez creados los campos).

   >[!NOTE]
   >
   >Cuando un campo como **Requerido**, el **Etiqueta** indicado en el panel izquierdo está marcado con un asterisco (**&#42;**).

![propiedades](assets/cfm-models-03.png)

1. **Adición de un campo**

   * Arrastre un tipo de datos requerido a la ubicación requerida para un campo.

     ![Tipo de datos para el campo](assets/cfm-models-04.png)

   * Una vez añadido un campo al modelo, el panel derecho mostrará las **Propiedades** que se pueden definir para ese tipo de datos en particular. Aquí puede definir lo que se requiere para ese campo.

      * Muchas propiedades se explican por sí mismas; para obtener más información, consulte [Propiedades](#properties).
      * Escribir una **Etiqueta de campo** autocompletará el **Nombre de propiedad** si está vacío, y se puede actualizar de forma manual más tarde.

        >[!CAUTION]
        >
        >Al actualizar de forma manual la propiedad **Nombre de propiedad** para un tipo de datos, tenga en cuenta que los nombres solo deben contener caracteres latinos, dígitos numéricos y guiones bajos “_” como carácter especial.
        >
        >AEM Si los modelos creados en versiones anteriores de contienen caracteres no permitidos, elimine o actualice dichos caracteres.

     Por ejemplo:

     ![Propiedades de campo](assets/cfm-models-05.png)

1. **Eliminación de un campo**

   Seleccione el campo requerido y, a continuación, toque o haga clic en el icono de la papelera. Se le pedirá que confirme la acción.

   ![quitar](assets/cfm-models-06.png)

1. Añada todos los campos obligatorios y defina las propiedades relacionadas, según sea necesario. Por ejemplo:

   ![guardar](assets/cfm-models-07.png)

1. Seleccione **Guardar** para mantener la definición.

## Tipos de datos {#data-types}

Hay disponible una selección de tipos de datos para definir el modelo:

* **Texto de línea única**
   * Añada uno o más campos de una sola línea de texto; se puede definir la longitud máxima
* **Texto multilínea**
   * Un área de texto que puede ser Texto enriquecido, Texto sin formato o Markdown
* **Número**
   * Adición de uno o más campos numéricos
* **Booleana**
   * Adición de una casilla de verificación booleana
* **Fecha y hora**
   * Adición de una fecha u hora
* **Lista desglosada**
   * Adición de un conjunto de casillas de verificación, botones de opción o campos desplegables
* **Etiquetas**
   * Permite a los autores de fragmentos acceder y seleccionar áreas de etiquetas
* **Referencia de contenido**
   * Referencias a otros contenidos, de cualquier tipo; se pueden usar para [crear contenido anidado](#using-references-to-form-nested-content)
   * Si se hace referencia a una imagen, puede optar por mostrar una miniatura
* **Referencia a fragmento**
   * Referencias a otros fragmentos de contenido; se pueden usar para [crear contenido anidado](#using-references-to-form-nested-content)
   * El tipo de datos se puede configurar para que los autores de fragmentos puedan hacer lo siguiente:
      * Editar directamente el fragmento al que se hace referencia.
      * Crear un nuevo fragmento de contenido basado en el modelo apropiado
* **Objeto JSON**
   * Permite al autor del fragmento de contenido introducir la sintaxis JSON en los elementos correspondientes de un fragmento.
      * Para permitir que AEM almacene el JSON directo que ha copiado/pegado desde otro servicio.
      * El JSON se pasa y se genera como JSON en GraphQL.
      * Incluye resaltado de sintaxis JSON, autocompletado y resaltado de errores en el editor de fragmentos de contenido.
* **Marcador de posición de pestaña**
   * Permite la introducción de pestañas para utilizarlas al editar el contenido del fragmento de contenido.
Esto se muestra como un divisor en el editor de modelos, que separa las secciones de la lista de tipos de datos de contenido. Cada instancia representa el inicio de una nueva pestaña.
En el editor de fragmentos, cada instancia aparecerá como una pestaña.
     >[!NOTE]
     >
     >Este tipo de datos se utiliza exclusivamente para dar formato; el esquema AEM GraphQL lo ignora.

## Propiedades {#properties}

Muchas propiedades se explican por sí mismas; para otras, a continuación se proporcionan detalles adicionales:

* **Nombre de propiedad**

  Cuando actualice manualmente esta propiedad para un tipo de datos, tenga en cuenta que los nombres **deben** contener *solo* caracteres latinos, dígitos numéricos y guiones bajos “_” como carácter especial.

  >[!CAUTION]
  >
  >AEM Si los modelos creados en versiones anteriores de contienen caracteres no permitidos, elimine o actualice dichos caracteres.

* **Representar como**
Las distintas opciones para realizar/procesar el campo en un fragmento. A menudo, esta propiedad permite definir si el autor ve una sola instancia del campo o si se le permite crear varias instancias.

* **Etiqueta de campo**
Introducción de una **Etiqueta de campo** generará automáticamente un **Nombre de propiedad**, que se puede actualizar de forma manual si es necesario.

* **Validación**
La validación básica está disponible mediante mecanismos como la propiedad **Requerido**. Algunos tipos de datos tienen campos de validación adicionales. Consulte [Validación](#validation) para obtener más información.

* Para el tipo de datos **Texto multilínea** es posible definir el **tipo predeterminado** como el siguiente:

   * **Texto enriquecido**
   * **Markdown**
   * **Texto sin formato**

  Si no se especifica, el valor predeterminado **Texto enriquecido** es el empleado para este campo.

  Cambiar el **tipo predeterminado** en un modelo de fragmento de contenido solo surtirá efecto en un fragmento de contenido existente relacionado después de que dicho fragmento se abra en el editor y se guarde.

* **Único**
El contenido (para el campo específico) debe ser único en todos los fragmentos de contenido creados a partir del modelo actual.

  Se utiliza para garantizar que los autores de contenido no puedan repetir el contenido ya añadido en otro fragmento del mismo modelo.

  Por ejemplo, un campo de **Texto de una sola línea** llamado `Country` en el modelo de fragmentos de contenido no puede tener el valor `Japan` en dos fragmentos de contenido dependientes. Se emite una advertencia cuando se intenta la segunda instancia.

  >[!NOTE]
  >
  >La unicidad se garantiza por cada raíz de idioma.

  >[!NOTE]
  >
  >Las variaciones pueden tener el mismo valor *único* como variaciones del mismo fragmento, pero no del mismo valor que se utiliza en cualquier variación de otros fragmentos.

  >[!CAUTION]
  >
  >Si desea utilizar MSM (que crea copias de fragmentos de contenido), utilice cualquiera **Único** Las restricciones de deben eliminarse de cualquier tipo de datos utilizado en los respectivos modelos de fragmentos de contenido.

* Consulte **[Referencia de contenido](#content-reference)** para obtener más información acerca de ese tipo de datos específico y sus propiedades.

* Consulte **[Referencia a fragmento (fragmentos anidados)](#fragment-reference-nested-fragments)** para obtener más información acerca de ese tipo de datos específico y sus propiedades.

* **Traducible**

  Marcar la casilla de verificación **Traducible** en un campo del editor de modelos de fragmentos de contenido provocará lo siguiente:

   * Asegurará que el nombre de propiedad del campo se añade a la configuración de traducción y contexto `/content/dam/<sites-configuration>`, si no están presentes.
   * Para GraphQL: establecerá una propiedad `<translatable>` en el campo Fragmento de contenido en `yes`, para permitir que la consulta GraphQL filtre la salida JSON solo con contenido traducible.

## Validación {#validation}

Varios tipos de datos ahora incluyen la posibilidad de definir los requisitos de validación cuando el contenido se introduce en el fragmento resultante:

* **Texto de línea única**
   * Compare con un regex predefinido.
* **Número**
   * Compruebe si hay valores específicos.
* **Referencia de contenido**
   * Pruebe tipos de contenido específicos.
   * Solo se puede hacer referencia a los recursos con un tamaño de archivo especificado o más pequeño.
   * Solo se puede hacer referencia a las imágenes con un intervalo predefinido de anchura o altura (en píxeles).
* **Referencia a fragmento**
   * Pruebe un modelo de fragmento de contenido específico.

## Uso de referencias para formar contenido anidado {#using-references-to-form-nested-content}

Los fragmentos de contenido pueden formar contenido anidado mediante cualquiera de los siguientes tipos de datos:

* **[Referencia de contenido](#content-reference)**
   * Proporciona una sencilla referencia a otro contenido; de cualquier tipo.
   * Se puede configurar para una o varias referencias (en el fragmento resultante).

* **[Referencia a fragmento](#fragment-reference-nested-fragments)** (fragmentos anidados)
   * Hace referencia a otros fragmentos, según los modelos específicos definidos.
   * Permite incluir o recuperar datos estructurados.
     >[!NOTE]
     >
     >Este método reviste especial interés en conjunción con la [Entrega de contenido sin encabezado mediante fragmentos de contenido con GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).
   * Se puede configurar para una o varias referencias (en el fragmento resultante).

>[!NOTE]
>
>AEM tiene una protección contra recurrencias para lo siguiente:
>
>* Referencias de contenido
>  Esto evita que el usuario agregue una referencia al fragmento actual. Esto puede dar lugar a un cuadro de diálogo vacío del selector de referencia a fragmento.
>
>* Referencias a fragmento en GraphQL
>  Si crea una consulta profunda que devuelve varios fragmentos de contenido referenciados entre sí, devolverá un valor nulo en la primera ocurrencia.

### Referencia de contenido {#content-reference}

La referencia de contenido le permite procesar contenido de otra fuente; por ejemplo, imagen o fragmento de contenido.

Además de las propiedades estándar, puede especificar las siguentes:

* La **Ruta raíz** para cualquier contenido referenciado
* Los tipos de contenido a los que se puede hacer referencia
* Las limitaciones de los tamaños de archivo
* Si se hace referencia a una imagen:
   * Mostrar miniatura
   * Restricciones de imagen de altura y anchura

![Referencia del contenido](assets/cfm-content-reference.png)

### Referencia a fragmento (fragmentos anidados) {#fragment-reference-nested-fragments}

La referencia a fragmento hace referencia a uno o más fragmentos de contenido. Esta función es de especial interés cuando se recupera contenido para utilizarlo en la aplicación, ya que le permite recuperar datos estructurados con varias capas.

Por ejemplo:

* Un modelo que define los detalles de un empleado, entre los que se incluyen:
   * Una referencia al modelo que define al empleador (compañía).

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
>Esto reviste especial interés en conjunción con la [Entrega de contenido sin encabezado mediante fragmentos de contenido con GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).

Además de las propiedades estándar, puede definir las siguientes:

* **Procesar como**:

   * **Multicampo**: el autor del fragmento puede crear varias referencias individuales.

   * **fragmentreference**: permite al autor del fragmento seleccionar una sola referencia a un fragmento.

* **Tipo de modelo:**
sueden seleccionar varios modelos. Al crear el fragmento de contenido, se debe haber creado cualquier fragmento referenciado mediante estos modelos.

* **Ruta raíz:**
Esto especifica una ruta raíz para los fragmentos a los que se hace referencia.

* **Permitir creación de fragmentos**

  Esto permitirá al autor del fragmento crear un nuevo fragmento basado en el modelo adecuado.

   * **fragmentreferencecomposite**: permite al autor del fragmento crear un compuesto seleccionando varios fragmentos.

  ![Referencia a fragmento](assets/cfm-fragment-reference.png)

>[!NOTE]
>
>Existe un mecanismo de protección contra la recurrencia. Prohíbe que el usuario seleccione el fragmento de contenido actual en la Referencia a fragmento. Esto puede dar lugar a un cuadro de diálogo vacío del selector de referencia a fragmento.
>
>También existe una protección contra la recurrencia para las referencias a fragmento en GraphQL. Si crea una consulta profunda en dos fragmentos de contenido que se hacen referencia entre sí, devolverá un valor nulo.

## Modelo de fragmento de contenido: propiedades {#content-fragment-model-properties}

Puede editar las **Propiedades** de un modelo de fragmento de contenido:

* **Básico**
   * **Título de modelo**
   * **Etiquetas**
   * **Descripción**
   * **Cargar imagen**

## Activación o desactivación de un modelo de fragmento de contenido {#enabling-disabling-a-content-fragment-model}

Para tener un control total sobre el uso de los modelos de fragmentos de contenido, estos tienen un estado que puede configurar.

### Activación de un modelo de fragmento de contenido {#enabling-a-content-fragment-model}

Una vez creado un modelo, debe activarse para que:

* Esté disponible para seleccionarse al crear un nuevo fragmento de contenido.
* Se pueda hacer referencia a él desde un modelo de fragmento de contenido.
* Esté disponible para GraphQL y por lo tanto, se genere el esquema.

Para habilitar un modelo marcado como lo siguiente:

* **Borrador**: nuevo (nunca habilitado).
* **Desactivado**: se ha deshabilitado específicamente.

Utilice la opción **Habilitar** desde:

* La barra de herramientas superior, cuando se selecciona el Modelo requerido.
* La Acción rápida correspondiente (pase el ratón sobre el Modelo requerido).

![Activar un borrador o un modelo desactivado](assets/cfm-status-enable.png)

### Desactivación de un modelo de fragmento de contenido {#disabling-a-content-fragment-model}

Un modelo también se puede desactivar para que:

* El modelo ya no esté disponible como base para la creación de *nuevos* fragmentos de contenido.
* Sin embargo:
   * El esquema de GraphQL se siga generando y aún se pueda consultar (para evitar afectar a la API de JSON).
   * Cualquier fragmento de contenido basado en el modelo se puede consultar y devolver desde el extremo de GraphQL.
* Ya no se puede hacer referencia al modelo, pero las referencias existentes no se tocan y aún se pueden consultar y devolver desde el extremo GraphQL.

Para desactivar un modelo marcado como **Habilitado** utilice la opción **Deshabilitar** desde:

* La barra de herramientas superior, cuando se selecciona el Modelo requerido.
* La Acción rápida correspondiente (pase el ratón sobre el Modelo requerido).

![Desactivación de un modelo habilitado](assets/cfm-status-disable.png)

## Permitir modelos de fragmento de contenido en la carpeta de recursos {#allowing-content-fragment-models-assets-folder}

Para implementar el control de contenido, puede configurar las **Directivas** en la carpeta Recursos para controlar qué modelos de fragmento de contenido están permitidos para la creación de fragmentos en esa carpeta.

>[!NOTE]
>
>El mecanismo es similar a [permitir plantillas de página](/help/sites-cloud/authoring/features/templates.md#allowing-a-template-author) para una página, y sus elementos secundarios, en propiedades avanzadas de una página.

Para configurar las **Directivas** para **Modelos de fragmento de contenido permitidos**:

1. Navegar y abrir **Propiedades** para la carpeta de recursos necesaria.

1. Abra la pestaña **Directivas**, donde puede configurar lo siguiente:

   * **Heredado de`<folder>`**

     Las directivas se heredan automáticamente al crear nuevas carpetas secundarias; la directiva se puede reconfigurar (y la herencia se rompe) si las subcarpetas necesitan permitir modelos diferentes de la carpeta principal.

   * **Modelos de fragmento de contenido permitidos por ruta**

     Se pueden permitir varios modelos.

   * **Modelos de fragmento de contenido permitidos por etiquetas**

     Se pueden permitir varios modelos.

   ![Directiva del modelo de fragmento de contenido](assets/cfm-model-policy-assets-folder.png)

1. **Guardar** cualquier cambio.

Los modelos de fragmento de contenido permitidos para una carpeta se resuelven de la siguiente manera:
* Las **Directivas** para los **Modelos de fragmento de contenido permitidos**.
* Si está vacío, intente determinar la directiva utilizando las reglas de herencia.
* Si la cadena de herencia no proporciona un resultado, consulte la configuración de **Cloud Services** para esa carpeta (primero directamente y luego mediante herencia).
* Si ninguno de los anteriores proporciona ningún resultado, no hay modelos permitidos para esa carpeta.

## Eliminación de un modelo de fragmento de contenido {#deleting-a-content-fragment-model}

>[!CAUTION]
>
>La eliminación de un modelo de fragmento de contenido puede afectar a los fragmentos dependientes.

Para eliminar un modelo de fragmento de contenido, haga lo siguiente:

1. Vaya a **Herramientas**, **General** y, a continuación, abra **Modelos de fragmento de contenido**.

1. Vaya a la carpeta que contiene el modelo de fragmento de contenido.
1. Seleccione el modelo, seguido de **Eliminar** en la barra de herramientas.

   >[!NOTE]
   >
   >Si se hace referencia al modelo, se envía una advertencia. Tome las medidas adecuadas.

## Publicación de un modelo de fragmento de contenido {#publishing-a-content-fragment-model}

Los modelos de fragmento de contenido deben publicarse cuando se publican fragmentos de contenido dependientes, o antes de hacerlo.

Para publicar un modelo de fragmento de contenido, haga lo siguiente:

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

El mensaje le sugerirá que compruebe el panel [Referencias](/help/sites-cloud/authoring/getting-started/basic-handling.md#references) para investigar más a fondo:

![Modelo de fragmento de contenido en referencias](assets/cfm-model-references.png)

## Modelos de fragmento de contenido bloqueados (publicados) {#locked-published-content-fragment-models}

Esta funcionalidad proporciona control para los modelos de fragmento de contenido que se han publicado.

### Desafíos {#the-challenge}

* Los modelos de fragmentos de contenido determinan el esquema de las consultas de GraphQL en AEM.

   * Los esquemas de GraphQL de AEM se crean en cuanto se genera un modelo de fragmento de contenido y pueden existir en entornos de creación y publicación.

   * Los esquemas en la publicación son los más críticos, ya que proporcionan la base para la entrega en directo de contenido de fragmento de contenido en formato JSON.

* Pueden producirse problemas cuando se modifican los modelos de fragmento de contenido o, dicho de otro modo, se editan. Esto significa que el esquema cambia, lo que a su vez puede afectar a las consultas de GraphQL existentes.

* La adición de nuevos campos a un modelo de fragmento de contenido no debería (normalmente) tener ningún efecto perjudicial. Sin embargo, si se modifican los campos de datos existentes (por ejemplo, su nombre) o se eliminan las definiciones de campos, las consultas de GraphQL existentes se romperán al solicitar estos campos.

### Requisitos {#the-requirements}

* Para concienciar a los usuarios sobre los riesgos que se plantean al editar modelos que ya se utilizan para la entrega de contenido en directo (es decir, modelos que se han publicado).

* Además, para evitar cambios no deseados.

Cualquiera de estos factores podría generar consultas si se vuelven a publicar los modelos modificados.

### Solución {#the-solution}

Para solucionar estos problemas, los modelos de fragmentos de contenido son *bloqueados* en modo de SOLO LECTURA en el autor, tan pronto como se hayan publicado. Esto se indica mediante **Bloqueado**:

![Tarjeta del modelo de fragmento de contenido bloqueado](assets/cfm-model-locked.png)

Cuando el modelo es **Bloqueado** (en modo de SOLO LECTURA), puede ver el contenido y la estructura de los modelos, pero no puede editarlos.

Puede administrar modelos **Bloqueados** desde la consola o desde el editor de modelos:

* Consola

  Desde la consola, puede administrar el modo de SOLO LECTURA con las acciones **Desbloquear** y **Bloqueo** de la barra de herramientas:

  ![Barra de herramientas del modelo de fragmento de contenido bloqueado](assets/cfm-model-locked.png)

   * Puede **Desbloquear** un modelo para activar las ediciones.

     Si selecciona **Desbloquear**, se muestra una advertencia y debe confirmar la **Desbloquear** acción:
     ![Mensaje al desbloquear el modelo de fragmento de contenido](assets/cfm-model-unlock-message.png)

     A continuación, puede abrir el modelo para editarlo.

   * También puede **Bloquear** el modelo después.
   * Volver a publicar el modelo inmediatamente lo volverá a poner en modo **Bloqueado** (SOLO LECTURA).

* Editor de modelo

   * Cuando se abre un modelo bloqueado, se le advierte y se le presentan tres acciones: **Cancelar**, **Ver solo lectura**, **Editar**:

     ![Mensaje al ver un modelo de fragmento de contenido bloqueado](assets/cfm-model-editor-lock-message.png)

   * Si selecciona **Ver solo lectura** puede ver el contenido y la estructura del modelo.

     ![Ver solo lectura: modelo de fragmento de contenido bloqueado](assets/cfm-model-editor-locked-view-only.png)

   * Si selecciona **Editar** puede editar y guardar las actualizaciones:

     ![Editar: modelo de fragmento de contenido bloqueado](assets/cfm-model-editor-locked-edit.png)

     >[!NOTE]
     >
     >Puede que todavía haya una advertencia en la parte superior, pero es cuando el modelo ya está siendo utilizado por fragmentos de contenido existentes.

   * **Cancelar** lo lleva nuevamente a la consola.
