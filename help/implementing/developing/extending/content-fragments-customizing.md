---
title: Personalizar y ampliar fragmentos de contenido
description: Un fragmento de contenido amplía un recurso estándar.
exl-id: 58152d6e-21b6-4f45-a45c-0f46ee58825e
source-git-commit: 335d7760886fe8dc489335a050d3cb6d0d2652a1
workflow-type: tm+mt
source-wordcount: '1808'
ht-degree: 2%

---

# Personalizar y ampliar fragmentos de contenido{#customizing-and-extending-content-fragments}

En Adobe Experience Manager as a Cloud Service, un fragmento de contenido amplía un recurso estándar; consulte:

* [Creación y administración de ](/help/assets/content-fragments/content-fragments.md) fragmentos de contenido y  [creación de páginas con ](/help/sites-cloud/authoring/fundamentals/content-fragments.md) fragmentos de contenido para obtener más información sobre los fragmentos de contenido.

* [Administración de ](/help/assets/manage-digital-assets.md) recursos para obtener más información sobre los recursos estándar.

## Arquitectura {#architecture}

Las [partes constituyentes](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) básicas de un fragmento de contenido son:

* Un *fragmento de contenido*,
* formado por uno o más *elementos de contenido*,
* y que pueden tener una o más *Variaciones de contenido*.

Los fragmentos de contenido individuales se basan en modelos de fragmento de contenido:

* Los modelos de fragmento de contenido definen la estructura de un fragmento de contenido cuando se crea.
* Un fragmento hace referencia al modelo; por lo tanto, los cambios en el modelo pueden/afectarán a cualquier fragmento dependiente.
* Los modelos son tipos de datos integrados.
* Las funciones para agregar nuevas variaciones, etc., deben actualizar el fragmento en consecuencia.

   >[!NOTE]
   >
   >Para poder mostrar/procesar un fragmento de contenido, la cuenta debe tener `read` permisos para el modelo.

   >[!CAUTION]
   >
   >Cualquier cambio en un modelo de fragmento de contenido existente puede afectar a los fragmentos dependientes; esto puede llevar a propiedades huérfanas en esos fragmentos.

### Integración de sitios con recursos {#integration-of-sites-with-assets}

La administración de fragmentos de contenido (CFM) forma parte de AEM Assets como:

* Los fragmentos de contenido son recursos.
* Utilizan la funcionalidad de recursos existente.
* Están totalmente integrados con Assets (consolas de administración, etc.).

Los fragmentos de contenido se consideran una función de sitios como:

* Se utilizan al crear páginas.

#### Asignación de fragmentos de contenido a recursos {#mapping-content-fragments-to-assets}

![fragmento de contenido a recursos](assets/content-fragment-to-assets.png)

Los fragmentos de contenido, basados en un modelo de fragmento de contenido, se asignan a un único recurso:

* Todo el contenido se almacena en el nodo `jcr:content/data` del recurso:

   * Los datos del elemento se almacenan en el subnodo maestro:
      `jcr:content/data/master`

   * Las variaciones se almacenan en un subnodo que lleva el nombre de la variación:
p. ej. `jcr:content/data/myvariation`

   * Los datos de cada elemento se almacenan en el subnodo respectivo como una propiedad con el nombre del elemento:
Por ejemplo, el contenido del elemento `text` se almacena como propiedad `text` en `jcr:content/data/master`

* Los metadatos y el contenido asociado se almacenan debajo de `jcr:content/metadata`
Excepto el título y la descripción, que no se consideran metadatos tradicionales y se almacenan en 
`jcr:content`

#### Ubicación del recurso {#asset-location}

Al igual que con los recursos estándar, un fragmento de contenido se mantiene en:

`/content/dam`

#### Permisos de recursos {#asset-permissions}

Para obtener más información, consulte [Fragmento de contenido - Eliminar consideraciones](/help/assets/content-fragments/content-fragments-delete.md).

#### Integración de funciones {#feature-integration}

Para integrar con Assets core:

* La función Administración de fragmentos de contenido (CFM) se basa en el núcleo de recursos.

* CFM proporciona sus propias implementaciones para los elementos de las vistas de tarjeta, columna o lista; estos complementos en las implementaciones de renderización de contenido de Assets existentes.

* Se han ampliado varios componentes de Assets para adaptarse a los fragmentos de contenido.

### Uso de fragmentos de contenido en páginas {#using-content-fragments-in-pages}

>[!CAUTION]
>
>El componente [Fragmento de contenido forma parte de los componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html). Consulte [Desarrollo de componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html) para obtener más información.

Se puede hacer referencia a los fragmentos de contenido desde AEM páginas, igual que a cualquier otro tipo de recurso. AEM proporciona el **[componente principal del fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)**, un [componente que le permite incluir fragmentos de contenido en sus páginas](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-a-content-fragment-to-your-page). También puede ampliar este componente principal **[Fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html)**.

* El componente utiliza la propiedad `fragmentPath` para hacer referencia al fragmento de contenido real. La propiedad `fragmentPath` se gestiona de la misma manera que las propiedades similares de otros tipos de recursos; por ejemplo, cuando el fragmento de contenido se mueve a otra ubicación.

* El componente permite seleccionar la variación que se va a mostrar.

* Además, se puede seleccionar un rango de párrafos para restringir el resultado; por ejemplo, esto se puede utilizar para la salida de varias columnas.

* El componente permite el contenido intermedio:

   * Aquí el componente le permite colocar otros recursos (imágenes, etc.) entre los párrafos del fragmento al que se hace referencia.

   * Para el contenido intermedio, debe:

      * ser conscientes de la posibilidad de referencias inestables; el contenido intermedio (añadido al crear una página) no tiene relación fija con el párrafo al que está colocado, insertando un nuevo párrafo (en el editor de fragmentos de contenido) antes de que la posición del contenido intermedio pueda perder la posición relativa

      * tenga en cuenta los parámetros adicionales (como los filtros de variación y de párrafo) para configurar lo que se representa en la página

>[!NOTE]
>
>**Modelo de fragmento de contenido:**
>
>Cuando se utiliza un fragmento de contenido en una página, se hace referencia al modelo de fragmento de contenido en el que se basa.
>
>Esto significa que si el modelo no se ha publicado en el momento de publicar la página, se marcará y el modelo se añadirá a los recursos que se publicarán con la página.

### Integración con otros Marcos {#integration-with-other-frameworks}

Los fragmentos de contenido se pueden integrar con:

* **Traducciones**

   Los fragmentos de contenido están totalmente integrados con el [AEM flujo de trabajo de traducción](/help/sites-cloud/administering/translation/overview.md). A nivel arquitectónico, esto significa:

   * Las traducciones individuales de un fragmento de contenido son en realidad fragmentos independientes; por ejemplo:

      * están situadas bajo diferentes raíces lingüísticas; pero comparta exactamente la misma ruta relativa debajo de la raíz del idioma correspondiente:

         `/content/dam/<path>/en/<to>/<fragment>`

         vs.

         `/content/dam/<path>/de/<to>/<fragment>`
   * Además de las rutas basadas en reglas, no hay más conexión entre las distintas versiones de idioma de un fragmento de contenido; se gestionan como dos fragmentos independientes, aunque la interfaz de usuario proporciona los medios para desplazarse entre las variantes de idioma.
   >[!NOTE]
   >
   >El flujo de trabajo de traducción AEM funciona con `/content`:
   >
   >* Como los modelos de fragmento de contenido residen en `/conf`, no se incluyen en dichas traducciones. Puede internacionalizar las cadenas de la interfaz de usuario.


* **Esquemas de metadatos**

   * Los fragmentos de contenido (re)utilizan los [esquemas de metadatos](/help/assets/metadata-schemas.md), que se pueden definir con recursos estándar.

   * CFM proporciona su propio esquema específico:

      `/libs/dam/content/schemaeditors/forms/contentfragment`

      esto se puede ampliar si es necesario.

   * El formulario de esquema correspondiente se integra con el editor de fragmentos.

## La API de administración de fragmentos de contenido: del lado del servidor {#the-content-fragment-management-api-server-side}

Puede utilizar la API del lado del servidor para acceder a los fragmentos de contenido; consulte:

[com.adobe.cq.dam.cfm](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/package-summary.html#package.description)

>[!CAUTION]
>
>Se recomienda utilizar la API del lado del servidor en lugar de acceder directamente a la estructura de contenido.

### Interfaces clave {#key-interfaces}

Las tres interfaces siguientes pueden servir como puntos de entrada:

* **Fragmento de contenido**  ([fragmento de contenido](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

   Esta interfaz le permite trabajar con un fragmento de contenido de forma abstracta.

   La interfaz le proporciona los medios para:

   * Administrar datos básicos (por ejemplo, obtener nombre; get/set title/description)
   * Acceso a metadatos
   * Acceder a elementos:

      * Elementos de lista
      * Obtener elementos por nombre
      * Crear nuevos elementos (consulte [Advertencias](#caveats))

      * Acceso a datos de elementos (consulte `ContentElement`)
   * Variaciones de lista definidas para el fragmento
   * Crear nuevas variaciones globalmente
   * Administrar contenido asociado:

      * Enumerar colecciones
      * Agregar colecciones
      * Eliminar colecciones
   * Acceso al modelo del fragmento

   Las interfaces que representan los elementos principales de un fragmento son:

   * **Elemento de contenido**  ([ContentElement](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * Obtener datos básicos (nombre, título, descripción)
      * Obtener/Establecer contenido
      * Variaciones de acceso de un elemento:

         * Enumerar variaciones
         * Obtener variaciones por nombre
         * Crear nuevas variaciones (consulte [Advertencias](#caveats))
         * Eliminar variaciones (consulte [Advertencias](#caveats))
         * Acceso a los datos de variación (consulte `ContentVariation`)
      * Método abreviado para resolver variaciones (aplicar alguna lógica adicional de reserva específica de implementación si la variación especificada no está disponible para un elemento)
   * **Variación de contenido**  ([ContentVariation](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * Obtener datos básicos (nombre, título, descripción)
      * Obtener/Establecer contenido
      * Sincronización sencilla, basada en la información modificada por última vez

   Las tres interfaces ( `ContentFragment`, `ContentElement`, `ContentVariation`) amplían la interfaz `Versionable`, que agrega capacidades de versiones, necesarias para los fragmentos de contenido:

   * Crear una nueva versión del elemento
   * Enumerar versiones del elemento
   * Obtener el contenido de una versión específica del elemento con versiones







### Adaptación: Uso de adaptTo() {#adapting-using-adaptto}

Se puede adaptar lo siguiente:

* `ContentFragment` puede adaptarse a:

   * `Resource` - el recurso Sling subyacente; actualizar el subyacente  `Resource` directamente requiere la reconstrucción del  `ContentFragment` objeto.

   * `Asset` - la  `Asset` abstracción DAM que representa el fragmento de contenido; la actualización  `Asset` directa requiere la reconstrucción del  `ContentFragment` objeto.

* `ContentElement` puede adaptarse a:

   * [`ElementTemplate`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ElementTemplate.html) - para acceder a la información estructural del elemento.

* [`FragmentTemplate`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html)

* `Resource` puede adaptarse a:

   * `ContentFragment`

### Advertencias {#caveats}

Cabe señalar que:

* Toda la API está diseñada para **no** mantener los cambios automáticamente (a menos que se indique lo contrario en el JavaDoc de la API). Por lo tanto, siempre tendrá que confirmar la resolución del recurso de la solicitud correspondiente (o la resolución que esté utilizando).

* Tareas que pueden requerir un esfuerzo adicional:

   * Se recomienda crear nuevas variaciones a partir de `ContentFragment`. Esto garantiza que todos los elementos compartan esta variación y que las estructuras de datos globales apropiadas se actualicen según sea necesario para reflejar la variación recién creada en la estructura de contenido.

   * Si se eliminan variaciones existentes a través de un elemento mediante `ContentElement.removeVariation()`, no se actualizarán las estructuras de datos globales asignadas a la variación. Para garantizar que estas estructuras de datos se mantengan sincronizadas, utilice `ContentFragment.removeVariation()` en su lugar, lo que elimina una variación globalmente.

## La API de administración de fragmentos de contenido: del lado del cliente {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>La API del lado del cliente es interna.

### Información adicional {#additional-information}

Consulte lo siguiente:

* `filter.xml`

   El `filter.xml` para la administración de fragmentos de contenido está configurado de modo que no se superponga con el paquete de contenido principal de Assets.

## Editar sesiones {#edit-sessions}

>[!CAUTION]
>
>Tenga en cuenta esta información de antecedentes. Se supone que no debe cambiar nada aquí (ya que está marcado como *área privada* en el repositorio), pero en algunos casos podría ayudar a entender cómo funcionan las cosas bajo el capó.

La edición de un fragmento de contenido, que puede abarcar varias vistas (= páginas de HTML), es atómica. Como estas capacidades de edición atómica multivista no son un concepto AEM típico, los fragmentos de contenido utilizan lo que se denomina *sesión de edición*.

Una sesión de edición se inicia cuando el usuario abre un fragmento de contenido en el editor. La sesión de edición finaliza cuando el usuario abandona el editor seleccionando **Save** o **Cancel**.

Técnicamente, todas las ediciones se realizan en contenido *activo*, al igual que con el resto de la edición de AEM. Cuando se inicia la sesión de edición, se crea una versión del estado actual sin editar. Si un usuario cancela una edición, se restaura esa versión. Si el usuario hace clic en **Guardar**, no se hace nada específico, ya que toda la edición se ejecutó en contenido *activo*, por lo tanto todos los cambios se mantienen ya. Además, al hacer clic en **Guardar** se déclencheur el procesamiento en segundo plano (como la creación de información de búsqueda de texto completo y/o el manejo de recursos de medios mixtos).

Existen algunas medidas de seguridad para los casos extremos; por ejemplo, si el usuario intenta salir del editor sin guardar o cancelar la sesión de edición. Además, hay disponible un guardado automático periódico para evitar la pérdida de datos.
Tenga en cuenta que dos usuarios pueden editar el mismo fragmento de contenido simultáneamente y, por lo tanto, sobrescribir los cambios de los demás. Para evitarlo, es necesario bloquear el fragmento de contenido aplicando la acción *Checkout* de la administración de DAM en el fragmento.

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

Para crear un nuevo fragmento de contenido mediante programación, debe utilizar un
`FragmentTemplate` adaptado desde un recurso de modelo.

Por ejemplo:

```java
Resource modelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = modelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### Ejemplo: Especificación del intervalo de guardado automático {#example-specifying-the-auto-save-interval}

El [intervalo de guardado automático](/help/assets/content-fragments/content-fragments-managing.md#save-close-and-versions) (medido en segundos) se puede definir mediante el administrador de configuración (ConfMgr):

* Nodo: `<conf-root>/settings/dam/cfm/jcr:content`
* Nombre de propiedad: `autoSaveInterval`
* Tipo: `Long`

* Predeterminado: `600` (10 minutos); esto se define en `/libs/settings/dam/cfm/jcr:content`

Si desea establecer un intervalo de guardado automático de 5 minutos, debe definir la propiedad en el nodo ; por ejemplo:

* Nodo: `/conf/global/settings/dam/cfm/jcr:content`
* Nombre de propiedad: `autoSaveInterval`

* Tipo: `Long`

* Valor: `300` (5 minutos equivale a 300 segundos)

## Componentes para la creación de páginas {#components-for-page-authoring}

Para obtener más información, consulte

* [Componentes principales: componente de fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)  (recomendado)
