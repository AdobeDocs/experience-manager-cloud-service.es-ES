---
title: Personalizar y ampliar fragmentos de contenido
description: Un fragmento de contenido amplía un recurso estándar.
translation-type: tm+mt
source-git-commit: 639bf1add463c0e62982a44ecdca834e2c7c53fe
workflow-type: tm+mt
source-wordcount: '1818'
ht-degree: 3%

---


# Personalizar y ampliar fragmentos de contenido{#customizing-and-extending-content-fragments}

En Adobe Experience Manager como Cloud Service, un fragmento de contenido extiende un recurso estándar; consulte:

* [Creación y administración de fragmentos](/help/assets/content-fragments/content-fragments.md) de contenido y creación de [páginas con fragmentos](/help/sites-cloud/authoring/fundamentals/content-fragments.md) de contenido para obtener más información sobre los fragmentos de contenido.

* [Administración de recursos](/help/assets/manage-digital-assets.md) para obtener más información sobre los recursos estándar.

<!-- Removing the extend-asset-editor article for now as I'm unsure of its accuracy. Hence commenting this link.
* [Managing Assets](/help/assets/manage-digital-assets.md) and [Customizing and Extending the Asset Editor](/help/assets/extend-asset-editor.md) for further information about standard assets.
-->

## Arquitectura {#architecture}

Las partes [constituyentes](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) básicas de un fragmento de contenido son:

* Un Fragmento *De Contenido*,
* consta de uno o varios elementos *de* contenido,
* y que pueden tener una o más variaciones *de contenido*.

Los fragmentos de contenido individuales se basan en modelos de fragmento de contenido:

* Los modelos de fragmento de contenido definen la estructura de un fragmento de contenido al crearlo.
* Un fragmento hace referencia al modelo; por lo tanto, los cambios en el modelo pueden/afectarán a cualquier fragmento dependiente.
* Los modelos están compuestos por tipos de datos.
* Las funciones para agregar nuevas variaciones, etc., deben actualizar el fragmento según corresponda.

   >[!NOTE]
   >
   >Para que pueda mostrar o procesar un fragmento de contenido, su cuenta debe tener `read` permisos para el modelo.

   >[!CAUTION]
   >
   >Cualquier cambio en un modelo de fragmento de contenido existente puede afectar a los fragmentos dependientes; esto puede llevar a propiedades huérfanas en esos fragmentos.

### Integración de sitios con recursos {#integration-of-sites-with-assets}

Content Fragment Management (CFM) es parte de AEM Assets como:

* Los fragmentos de contenido son recursos.
* Utilizan la funcionalidad de Recursos existente.
* Están totalmente integrados con Recursos (consolas de administración, etc.).

Los fragmentos de contenido se consideran una función de sitios como:

* Se utilizan al crear las páginas.

#### Asignación de fragmentos de contenido a recursos {#mapping-content-fragments-to-assets}

![fragmento de contenido a recursos](assets/content-fragment-to-assets.png)

Los fragmentos de contenido, basados en un modelo de fragmento de contenido, se asignan a un solo recurso:

* Todo el contenido se almacena bajo el `jcr:content/data` nodo del recurso:

   * Los datos del elemento se almacenan en el subnodo maestro:
      `jcr:content/data/master`

   * Las variaciones se almacenan bajo un subnodo que lleva el nombre de la variación:
p. ej. `jcr:content/data/myvariation`

   * Los datos de cada elemento se almacenan en el subnodo correspondiente como una propiedad con el nombre del elemento:
Por ejemplo, el contenido del elemento `text` se almacena como propiedad `text` en `jcr:content/data/master`

* Los metadatos y el contenido asociado se almacenan a continuación `jcr:content/metadata`excepto el título y la descripción, que no se consideran metadatos tradicionales y se almacenan en 
`jcr:content`

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

Se puede hacer referencia a los fragmentos de contenido desde AEM páginas, al igual que a cualquier otro tipo de recurso. AEM proporciona el componente **[principal Fragmento de](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)** contenido, un [componente que permite incluir fragmentos de contenido en las páginas](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-a-content-fragment-to-your-page). También puede ampliar este componente principal de fragmento **[de contenido](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/developing.html)** .

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
>Cuando se utiliza un fragmento de contenido en una página, se hace referencia al modelo de fragmento de contenido en el que se basa.
>
>Esto significa que si el modelo no se ha publicado en el momento de publicar la página, se marcará y el modelo se agregará a los recursos que se publicarán con la página.

### Integración con otros marcos {#integration-with-other-frameworks}

Los fragmentos de contenido se pueden integrar con:

* **Traducciones**

   Los fragmentos de contenido están totalmente integrados con el flujo de trabajo de traducción AEM. A nivel arquitectónico, esto significa:

   * Las traducciones individuales de un fragmento de contenido son en realidad fragmentos independientes; por ejemplo:

      * están situados bajo diferentes raíces lingüísticas; pero comparta exactamente la misma ruta relativa debajo de la raíz del idioma relevante:

         `/content/dam/<path>/en/<to>/<fragment>`

         vs.

         `/content/dam/<path>/de/<to>/<fragment>`
   * Además de las rutas basadas en reglas, no hay más conexión entre las distintas versiones de idioma de un fragmento de contenido; se gestionan como dos fragmentos independientes, aunque la interfaz de usuario proporciona los medios para desplazarse entre las variantes de idioma.
   >[!NOTE]
   >
   >El flujo de trabajo de traducción AEM funciona con `/content`:
   >
   >* Dado que los modelos de fragmentos de contenido residen en `/conf`, no se incluyen en dichas traducciones. Puede internacionalizar las cadenas de la interfaz de usuario.


* **Esquemas de metadatos**

   * Los fragmentos de contenido (re)utilizan los esquemas [de](/help/assets/metadata-schemas.md)metadatos, que se pueden definir con los recursos estándar.

   * CFM ofrece su propio esquema específico:

      `/libs/dam/content/schemaeditors/forms/contentfragment`

      esto se puede ampliar si es necesario.

   * El formulario de esquema correspondiente se integra con el editor de fragmentos.

## La Content Fragment Management API (API de administración de fragmentos de contenido) del lado del servidor {#the-content-fragment-management-api-server-side}

Puede utilizar la API del lado del servidor para acceder a los fragmentos de contenido; consulte:

[com.adobe.cq.dam.cfm](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/package-summary.html#package.description)

>[!CAUTION]
>
>Se recomienda encarecidamente utilizar la API del lado del servidor en lugar de acceder directamente a la estructura de contenido.

### Interfaces clave {#key-interfaces}

Las tres interfaces siguientes pueden servir como puntos de entrada:

* **Fragmento** de contenido ([ContentFragment](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

   Esta interfaz le permite trabajar con un fragmento de contenido de forma abstracta.

   La interfaz le proporciona los medios para:

   * Administrar datos básicos (por ejemplo, obtener nombre; get/set title/description)
   * Acceso a metadatos
   * Elementos de acceso:

      * Elementos de lista
      * Obtener elementos por nombre
      * Crear nuevos elementos (consulte [Advertencias](#caveats))

      * Acceso a datos de elementos (consulte `ContentElement`)
   * Variaciones de lista definidas para el fragmento
   * Crear nuevas variaciones globalmente
   * Administrar contenido asociado:

      * Colecciones de lista
      * Añadir colecciones
      * Eliminar colecciones
   * Acceso al modelo del fragmento

   Las interfaces que representan los elementos principales de un fragmento son:

   * **Elemento** de contenido ([ContentElement](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * Obtener datos básicos (nombre, título, descripción)
      * Obtener o definir contenido
      * Variaciones de acceso de un elemento:

         * Variaciones de lista
         * Obtener variaciones por nombre
         * Crear nuevas variaciones (consulte [Advertencias](#caveats))
         * Eliminar variaciones (consulte [Advertencias](#caveats))
         * Acceso a los datos de variación (consulte `ContentVariation`)
      * Método abreviado para resolver variaciones (aplicando alguna lógica adicional de reserva específica para la implementación si la variación especificada no está disponible para un elemento)
   * **Variación** de contenido ([ContentVariation](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * Obtener datos básicos (nombre, título, descripción)
      * Obtener o definir contenido
      * Sincronización simple, basada en la información modificada por última vez

   Las tres interfaces ( `ContentFragment`, `ContentElement`, `ContentVariation`) amplían la `Versionable` interfaz, que agrega capacidades de creación de versiones, necesarias para los fragmentos de contenido:

   * Crear nueva versión del elemento
   * Versiones de lista del elemento
   * Obtener el contenido de una versión específica del elemento con versiones







### Adaptación - Uso de adaptacióna() {#adapting-using-adaptto}

Se pueden adaptar los siguientes elementos:

* `ContentFragment` puede adaptarse a:

   * `Resource` - el recurso Sling subyacente; la actualización del subyacente `Resource` directamente requiere la reconstrucción del `ContentFragment` objeto.

   * `Asset` - la abstracción DAM `Asset` que representa el fragmento de contenido; la actualización `Asset` directa requiere la reconstrucción del `ContentFragment` objeto.

* `ContentElement` puede adaptarse a:

   * [`ElementTemplate`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/ElementTemplate.html) - para acceder a la información estructural del elemento.

* [`FragmentTemplate`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html)

* `Resource` puede adaptarse a:

   * `ContentFragment`

### Advertencias {#caveats}

Cabe señalar que:

* Toda la API está diseñada para **no** persistir los cambios automáticamente (a menos que se indique lo contrario en el JavaDoc de la API). Por lo tanto, siempre tendrá que transferir la resolución de recursos de la solicitud correspondiente (o la resolución que esté utilizando).

* Tareas que podrían requerir un esfuerzo adicional:

   * Se recomienda encarecidamente crear nuevas variaciones de `ContentFragment`. Esto garantiza que todos los elementos compartan esta variación y que las estructuras de datos globales apropiadas se actualicen según sea necesario para reflejar la variación recién creada en la estructura de contenido.

   * Al eliminar las variaciones existentes mediante un elemento, `ContentElement.removeVariation()`no se actualizarán las estructuras de datos globales asignadas a la variación. Para garantizar que estas estructuras de datos se mantengan sincronizadas, utilice `ContentFragment.removeVariation()` en su lugar, lo que elimina una variación de forma global.

## La Content Fragment Management API (API de administración de fragmentos de contenido) del lado del cliente {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>La API del lado del cliente es interna.

### Información adicional {#additional-information}

Consulte lo siguiente:

* `filter.xml`

   El `filter.xml` para la administración de fragmentos de contenido está configurado de modo que no se superponga con el paquete de contenido principal de Recursos.

## Editar sesiones {#edit-sessions}

>[!CAUTION]
>
>Tenga en cuenta esta información básica. Se supone que no debe cambiar nada aquí (ya que está marcado como un área ** privada en el repositorio), pero en algunos casos podría ayudar a entender cómo funcionan las cosas bajo el capó.

Editar un fragmento de contenido, que puede abarcar varias vistas (= páginas HTML), es atómico. Como estas funciones de edición atómica con varias vistas no son un concepto AEM típico, los fragmentos de contenido utilizan lo que se denomina sesión *de* edición.

Una sesión de edición se inicia cuando el usuario abre un fragmento de contenido en el editor. La sesión de edición finaliza cuando el usuario abandona el editor seleccionando **Guardar** o **Cancelar**.

Técnicamente, todas las ediciones se realizan en contenido *en directo* , al igual que con el resto de la edición AEM. Cuando se inicia la sesión de edición, se crea una versión del estado actual sin editar. Si un usuario cancela una edición, se restaura esa versión. Si el usuario hace clic en **Guardar**, no se realiza ninguna acción específica, ya que toda la edición se ejecutó en contenido en *directo* , por lo tanto todos los cambios se mantienen ya. Además, al hacer clic en **Guardar** se activará cierto procesamiento en segundo plano (como la creación de información de búsqueda de texto completo y/o el manejo de recursos de medios mixtos).

Existen algunas medidas de seguridad para los casos de borde; por ejemplo, si el usuario intenta salir del editor sin guardar o cancelar la sesión de edición. Además, hay disponible un guardado automático periódico para evitar la pérdida de datos.
Tenga en cuenta que dos usuarios pueden editar el mismo fragmento de contenido al mismo tiempo y, por lo tanto, sobrescribir los cambios entre sí. Para evitarlo, el fragmento de contenido debe bloquearse mediante la aplicación de la acción de *cierre* de compra de la administración de DAM en el fragmento.

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

Para crear un nuevo fragmento de contenido mediante programación, debe utilizar un`FragmentTemplate` recurso de modelo adaptado.

Por ejemplo:

```java
Resource modelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = modelRsc.adaptTo(FragmentTemplate.class);
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
