---
title: Personalización y ampliación de fragmentos de contenido
description: Un fragmento de contenido amplía un recurso estándar.
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14

---


# Personalización y ampliación de fragmentos de contenido{#customizing-and-extending-content-fragments}

En Adobe Experience Manager como servicio de nube, un fragmento de contenido amplía un recurso estándar; consulte:

* [Creación y administración de fragmentos](/help/assets/content-fragments/content-fragments.md) de contenido y creación de [páginas con fragmentos](/help/sites-cloud/authoring/fundamentals/content-fragments.md) de contenido para obtener más información sobre los fragmentos de contenido.

* [Administración de recursos](/help/assets/manage-digital-assets.md) y [personalización y ampliación del editor](/help/assets/extend-asset-editor.md) de recursos para obtener más información sobre los recursos estándar.

## Arquitectura {#architecture}

Las partes [constituyentes](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) básicas de un fragmento de contenido son:

* Un Fragmento *De Contenido*,
* consta de uno o varios elementos *de* contenido,
* y que pueden tener una o más variaciones *de contenido*.

Según el tipo de fragmento, también se utilizan modelos o la plantilla Fragmento **** simple:

>[!CAUTION]
>
>[Ahora se recomiendan modelos](/help/assets/content-fragments/content-fragments-models.md) de fragmentos de contenido para crear todos los fragmentos.
>
>Los modelos de fragmentos de contenido se utilizan en todos los ejemplos de WKND.

* Modelos de fragmento de contenido:

   * Se utiliza para definir fragmentos de contenido que contienen contenido estructurado.
   * Los modelos de fragmento de contenido definen la estructura de un fragmento de contenido al crearlo.
   * Un fragmento hace referencia al modelo; por lo tanto, los cambios en el modelo pueden/afectarán a cualquier fragmento dependiente.
   * Los modelos están compuestos por tipos de datos.
   * Las funciones para agregar nuevas variaciones, etc., deben actualizar el fragmento según corresponda.
   >[!NOTE]
   >
   >Para que pueda mostrar o procesar un fragmento de contenido, su cuenta debe tener permisos de lectura para el modelo.

   >[!CAUTION]
   >
   >Cualquier cambio en un modelo de fragmento de contenido existente puede afectar a los fragmentos dependientes; esto puede llevar a propiedades huérfanas en esos fragmentos.

* Plantilla de fragmento de contenido - Fragmento **** simple:

   * Se utiliza para definir fragmentos de contenido sencillos.

   * Esta plantilla define la estructura (básica, de solo texto) de un fragmento de contenido cuando se crea.

   * La plantilla se copia en el fragmento cuando se crea.

   * Las funciones para agregar nuevas variaciones, etc., deben actualizar el fragmento según corresponda.

   * La plantilla de fragmento de contenido (Fragmento **** simple) funciona de forma distinta a la de otros mecanismos de plantilla dentro del ecosistema de AEM (por ejemplo, plantillas de página, etc.). Por lo tanto, debe considerarse por separado.

   * Cuando se basa en la plantilla Fragmento **** simple, el tipo MIME del contenido se administra en el contenido real; esto significa que cada elemento y variación puede tener un tipo MIME diferente.

### Integración de sitios con recursos {#integration-of-sites-with-assets}

Content Fragment Management (CFM) forma parte de Recursos AEM como:

* Los fragmentos de contenido son recursos.
* Utilizan la funcionalidad de Recursos existente.
* Están totalmente integrados con Recursos (consolas de administración, etc.).

Los fragmentos de contenido se consideran una función de sitios como:

* Se utilizan al crear las páginas.

#### Asignación de fragmentos de contenido estructurado a recursos {#mapping-structured-content-fragments-to-assets}

![fragmento de contenido a recursos estructurados](assets/content-fragment-to-assets-structured.png)

Los fragmentos de contenido con contenido estructurado (es decir, basados en un modelo de fragmento de contenido) se asignan a un solo recurso:

* Todo el contenido se almacena bajo el `jcr:content/data` nodo del recurso:

   * Los datos del elemento se almacenan en el subnodo maestro:
      `jcr:content/data/master`

   * Las variaciones se almacenan bajo un subnodo que lleva el nombre de la variación:
p. ej. `jcr:content/data/myvariation`

   * Los datos de cada elemento se almacenan en el subnodo correspondiente como una propiedad con el nombre del elemento:
Por ejemplo, el contenido del elemento `text` se almacena como propiedad `text` en `jcr:content/data/master`

* Los metadatos y el contenido asociado se almacenan a continuación `jcr:content/metadata`excepto el título y la descripción, que no se consideran metadatos tradicionales y se almacenan en `jcr:content`

#### Asignación de fragmentos de contenido simples a recursos {#mapping-simple-content-fragments-to-assets}

![fragmento de contenido a recursos simple](assets/content-fragment-to-assets-simple.png)

Los fragmentos de contenido simple (basados en la plantilla Fragmento **** simple) se asignan a una composición compuesta por un recurso principal y subrecursos (opcionales):

* Toda la información que no sea de contenido de un fragmento (como título, descripción, metadatos, estructura) se administra exclusivamente en el recurso principal.
* El contenido del primer elemento de un fragmento se asigna a la representación original del recurso principal.

   * Las variaciones (si las hay) del primer elemento se asignan a otras representaciones del recurso principal.

* Los elementos adicionales (si existen) se asignan a subrecursos del recurso principal.

   * El contenido principal de estos elementos adicionales se asigna a la representación original del subactivo correspondiente.
   * Otras variaciones (si procede) de cualquier elemento adicional se relacionan con otras representaciones del subactivo correspondiente.

#### Ubicación del recurso {#asset-location}

Al igual que con los recursos estándar, un fragmento de contenido se incluye en:

`/content/dam`

#### Permisos de recursos {#asset-permissions}

Para obtener más información, consulte Fragmento [de contenido - Eliminar consideraciones](/help/assets/content-fragments/content-fragments-delete.md).

#### Integración de funciones {#feature-integration}

Para realizar la integración con el núcleo de recursos:

* La función Administración de fragmentos de contenido (CFM) se basa en el núcleo de recursos.

* CFM proporciona sus propias implementaciones para los elementos de las vistas de tarjeta/columna/lista; estos complementos se conectan a las implementaciones de representación de contenido de Recursos existentes.

* Se han ampliado varios componentes de Recursos para incluir fragmentos de contenido.

### Uso de fragmentos de contenido en páginas {#using-content-fragments-in-pages}

>[!CAUTION]
>
>El componente Fragmento [de contenido forma parte de los componentes](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)principales. Consulte [Desarrollo de componentes](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/developing.html) principales para obtener más detalles.

Se puede hacer referencia a los fragmentos de contenido desde páginas de AEM, al igual que a cualquier otro tipo de recurso. AEM proporciona el componente **[principal Fragmento de](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)**contenido, un[componente que permite incluir fragmentos de contenido en las páginas](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-a-content-fragment-to-your-page). También puede ampliar este componente principal de fragmento**[de contenido](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/developing.html)** .

* El componente utiliza la propiedad `fragmentPath` para hacer referencia al fragmento de contenido real. La `fragmentPath` propiedad se gestiona del mismo modo que otras propiedades similares de otros tipos de recursos; por ejemplo, cuando el fragmento de contenido se mueve a otra ubicación.

* El componente permite seleccionar la variación que se va a mostrar.

* Además, se puede seleccionar un rango de párrafos para restringir el resultado; por ejemplo, esto se puede utilizar para la salida de varias columnas.

* El componente permite contenido intermedio:

   * Aquí el componente permite colocar otros recursos (imágenes, etc.) entre los párrafos del fragmento al que se hace referencia.

   * Para el contenido intermedio debe:

      * ser conscientes de la posibilidad de referencias inestables; el contenido intermedio (agregado al crear una página) no tiene una relación fija con el párrafo al que está situado, insertando un nuevo párrafo (en el editor de fragmentos de contenido) antes de que la posición del contenido intermedio pueda perder la posición relativa

      * considere los parámetros adicionales (como los filtros de variante y párrafo) para configurar lo que se procesa en la página

>[!NOTE]
>
>**Modelo de fragmento de contenido:**
>
>Cuando se utiliza un fragmento de contenido basado en un modelo de fragmento de contenido en una página, se hace referencia al modelo. Esto significa que si el modelo no se ha publicado en el momento de publicar la página, se marcará y el modelo se agregará a los recursos que se publicarán con la página.
>
>**Plantilla de fragmento de contenido - Fragmento simple:**
>
>Cuando se utiliza un fragmento de contenido basado en la plantilla de fragmento de contenido Fragmento **** simple en una página, no hay referencia ya que la plantilla se copió al crear el fragmento.

### Integración con otros marcos {#integration-with-other-frameworks}

Los fragmentos de contenido se pueden integrar con:

* **Traducciones**

   Los fragmentos de contenido están totalmente integrados con el flujo de trabajo de traducción de AEM. A nivel arquitectónico, esto significa:

   * Las traducciones individuales de un fragmento de contenido son en realidad fragmentos independientes; por ejemplo:

      * están situados bajo diferentes raíces lingüísticas; pero comparta exactamente la misma ruta relativa debajo de la raíz del idioma relevante:

         `/content/dam/<path>/en/<to>/<fragment>`

         vs.

         `/content/dam/<path>/de/<to>/<fragment>`
   * Además de las rutas basadas en reglas, no hay más conexión entre las distintas versiones de idioma de un fragmento de contenido; se gestionan como dos fragmentos independientes, aunque la interfaz de usuario proporciona los medios para desplazarse entre las variantes de idioma.
   >[!NOTE]
   >
   >El flujo de trabajo de traducción de AEM funciona con `/content`:
   >
   >* Dado que los modelos de fragmentos de contenido residen en `/conf`, no se incluyen en dichas traducciones. Puede internacionalizar las cadenas de la interfaz de usuario.


* **Esquemas de metadatos**

   * Los fragmentos de contenido (re)utilizan los esquemas [de](/help/assets/metadata-schemas.md)metadatos, que se pueden definir con recursos estándar.

   * CFM ofrece su propio esquema específico:

      `/libs/dam/content/schemaeditors/forms/contentfragment`

      esto se puede ampliar si es necesario.

   * El formulario de esquema correspondiente se integra con el editor de fragmentos.

## La Content Fragment Management API (API de administración de fragmentos de contenido) del lado del servidor {#the-content-fragment-management-api-server-side}

Puede utilizar la API del lado del servidor para acceder a los fragmentos de contenido; consulte:

[com.adobe.cq.dam.cfm](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/ref/javadoc/com/adobe/cq/dam/cfm/package-frame.html)

>[!CAUTION]
>
>Se recomienda encarecidamente utilizar la API del lado del servidor en lugar de acceder directamente a la estructura de contenido.

### Interfaces clave {#key-interfaces}

Las tres interfaces siguientes pueden servir como puntos de entrada:

* **Fragmento** de contenido ([ContentFragment](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/ref/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

   Esta interfaz le permite trabajar con un fragmento de contenido de forma abstracta.

   La interfaz le proporciona los medios para:

   * Administrar datos básicos (por ejemplo, obtener nombre; get/set title/description)
   * Acceso a metadatos
   * Elementos de acceso:

      * Elementos de Lista
      * Obtener elementos por nombre
      * Crear nuevos elementos (consulte [Advertencias](#caveats))

      * Acceso a datos de elementos (consulte `ContentElement`)
   * Variaciones de Lista definidas para el fragmento
   * Crear nuevas variaciones globalmente
   * Administrar contenido asociado:

      * Colecciones de Lista
      * Añadir colecciones
      * Eliminar colecciones
   * Acceso al modelo o plantilla del fragmento
   Las interfaces que representan los elementos principales de un fragmento son:

   * **Elemento** de contenido ([ContentElement](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/ref/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * Obtener datos básicos (nombre, título, descripción)
      * Obtener o definir contenido
      * Variaciones de acceso de un elemento:

         * Variaciones de Lista
         * Obtener variaciones por nombre
         * Crear nuevas variaciones (consulte [Advertencias](#caveats))
         * Eliminar variaciones (consulte [Advertencias](#caveats))
         * Acceso a los datos de variación (consulte `ContentVariation`)
      * Método abreviado para resolver variaciones (aplicando alguna lógica adicional de reserva específica de implementación si la variación especificada no está disponible para un elemento)
   * **Variación** de contenido ([ContentVariation](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/ref/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * Obtener datos básicos (nombre, título, descripción)
      * Obtener o definir contenido
      * Sincronización simple, basada en la información modificada por última vez
   Las tres interfaces ( `ContentFragment`, `ContentElement`, `ContentVariation`) amplían la `Versionable` interfaz, que agrega capacidades de creación de versiones, necesarias para los fragmentos de contenido:

   * Crear nueva versión del elemento
   * Versiones de Lista del elemento
   * Obtener el contenido de una versión específica del elemento con versiones







### Adaptación - Uso de adaptacióna() {#adapting-using-adaptto}

Se pueden adaptar los siguientes elementos:

* `ContentFragment` puede adaptarse a:

   * `Resource` - el recurso Sling subyacente; la actualización del subyacente `Resource` directamente requiere la reconstrucción del `ContentFragment` objeto.

   * `Asset` - la abstracción DAM `Asset` que representa el fragmento de contenido; la actualización `Asset` directa requiere la reconstrucción del `ContentFragment` objeto.

* `ContentElement` puede adaptarse a:

   * `ElementTemplate` - para acceder a la información estructural del elemento.

* `Resource` puede adaptarse a:

   * `ContentFragment`

### Advertencias {#caveats}

Cabe señalar que:

* Toda la API está diseñada para **no** persistir los cambios automáticamente (a menos que se indique lo contrario en el JavaDoc de la API). Por lo tanto, siempre tendrá que transferir la resolución de recursos de la solicitud correspondiente (o la resolución que esté utilizando).

* Tareas que podrían requerir un esfuerzo adicional:

   * La creación o eliminación de nuevos elementos no actualizará la estructura de datos de fragmentos simples (según la plantilla Fragmento **** simple).

   * Cree nuevas variaciones desde `ContentFragment` para actualizar la estructura de datos.

   * La eliminación de las variaciones existentes no actualizará la estructura de datos.

## La Content Fragment Management API (API de administración de fragmentos de contenido) del lado del cliente {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>La API del lado del cliente es interna.

### Información adicional {#additional-information}

Consulte lo siguiente:

* `filter.xml`

   El `filter.xml` para la administración de fragmentos de contenido está configurado de modo que no se superponga con el paquete de contenido principal de Recursos.

## Editar sesiones {#edit-sessions}

Una sesión de edición se inicia cuando el usuario abre un fragmento de contenido en una de las páginas del editor. La sesión de edición finaliza cuando el usuario abandona el editor seleccionando **Guardar** o **Cancelar**.

### Requisitos {#requirements}

Los requisitos para controlar una sesión de edición son:

* Editar un fragmento de contenido, que puede abarcar varias vistas (= páginas HTML), debe ser atómico.

* La edición también debe ser *transaccional*; al final de la sesión de edición, los cambios se deben confirmar (guardar) o revertir (cancelar).

* Los casos perimetrales deben gestionarse correctamente; estas situaciones incluyen situaciones como cuando el usuario abandona la página introduciendo una dirección URL manualmente o utilizando la navegación global.

* Debe estar disponible un guardado automático periódico (cada x minutos) para evitar la pérdida de datos.

* Si dos usuarios editan un fragmento de contenido al mismo tiempo, no deben sobrescribir los cambios de los demás.

<!--
#### Processes {#processes}

The processes involved are:

* Starting a session

  * A new version of the content fragment is created.

  * Auto save is started.

  * Cookies are set; these define the currently edited fragment and that there is an edit session open.

* Finishing a session

  * Auto save is stopped.

  * Upon commit:

    * The last modified information is updated.

    * Cookies are removed.

  * Upon rollback:

    * The version of the content fragment that was created when the edit session was started is restored.

    * Cookies are removed.

* Editing

  * All changes (auto save included) are done on the active content fragment - not in a separated, protected area.

  * Therefore, those changes are reflected immediately on AEM pages that reference the respective content fragment

#### Actions {#actions}

The possible actions are:

* Entering a page

  * Check if an editing session is already present; by checking the respective cookie.

    * If one exists, verify that the editing session was started for the content fragment that is currently being edited

      * If the current fragment, reestablish the session.

      * If not, try to cancel editing for the previously edited content fragment and remove cookies (no editing session present afterwards).

    * If no edit session exists, wait for the first change made by the user (see below).

  * Check if the content fragment is already referenced on a page and display appropriate information if so.

* Content change

  * Whenever the user changes content and there is no edit session present, a new edit session is created (see [Starting a session](#processes)).

-->

* Salida de una página

   * Si hay una sesión de edición presente y los cambios no se han mantenido, se muestra un cuadro de diálogo de confirmación modal para notificar al usuario la pérdida potencial de contenido y permitirle permanecer en la página.

## Ejemplos {#examples}

### Ejemplo: Acceso a un fragmento de contenido existente {#example-accessing-an-existing-content-fragment}

Para conseguirlo, puede adaptar el recurso que representa la API a:

`com.adobe.cq.dam.cfm.ContentFragment`

Por ejemplo:

```java
// first, get the resource
Resource fragmentResource = resourceResolver.getResource("/content/dam/fragments/my-fragment");
// then adapt it
if (fragmentResource != null) {
    ContentFragment fragment = fragmentResource.adaptTo(ContentFragment.class);
    // the resource is now accessible through the API
}
```

### Ejemplo: Creación de un nuevo fragmento de contenido {#example-creating-a-new-content-fragment}

Para crear un nuevo fragmento de contenido mediante programación, debe utilizar un`FragmentTemplate` recurso de modelo o plantilla adaptado.

Por ejemplo:

```java
Resource templateOrModelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### Ejemplo: Especificación del intervalo de guardado automático {#example-specifying-the-auto-save-interval}

El intervalo [de guardado](/help/assets/content-fragments/content-fragments-managing.md#save-cancel-and-versions) automático (medido en segundos) se puede definir con el administrador de configuración (ConfMgr):

* Nodo: `<conf-root>/settings/dam/cfm/jcr:content`
* Nombre de propiedad: `autoSaveInterval`
* Tipo: `Long`

* Predeterminado: `600` (10 minutos); esto se define en `/libs/settings/dam/cfm/jcr:content`

Si desea establecer un intervalo de guardado automático de 5 minutos, debe definir la propiedad en el nodo; por ejemplo:

* Nodo: `/conf/global/settings/dam/cfm/jcr:content`
* Nombre de propiedad: `autoSaveInterval`

* Tipo: `Long`

* Valor: `300` (5 minutos equivale a 300 segundos)

## Componentes para la creación de páginas {#components-for-page-authoring}

Para obtener más información, consulte

* [Componentes principales - Componente](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html) de fragmento de contenido (recomendado)
