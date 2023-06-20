---
title: Personalizar y ampliar fragmentos de contenido
description: Un fragmento de contenido amplía un recurso estándar.
exl-id: 58152d6e-21b6-4f45-a45c-0f46ee58825e
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1808'
ht-degree: 3%

---

# Personalizar y ampliar fragmentos de contenido{#customizing-and-extending-content-fragments}

Dentro de Adobe Experience Manager as a Cloud Service, un fragmento de contenido amplía un recurso estándar; consulte:

* [Creación y administración de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/content-fragments.md) y [Creación de páginas con fragmentos de contenido](/help/sites-cloud/authoring/fundamentals/content-fragments.md) para obtener más información sobre fragmentos de contenido.

* [Administración de recursos](/help/assets/manage-digital-assets.md) para obtener más información sobre los recursos estándar.

## Arquitectura {#architecture}

Lo básico [partes constitutivas](/help/sites-cloud/administering/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) de un fragmento de contenido son:

* A *Fragmento de contenido*,
* compuesto por uno o más *Elementos de contenido*,
* y que pueden tener uno o más *Variaciones de contenido*.

Los fragmentos de contenido individuales se basan en modelos de fragmentos de contenido:

* Los modelos de fragmento de contenido definen la estructura de un fragmento de contenido cuando se crea.
* Un fragmento hace referencia al modelo, por lo que los cambios realizados en el modelo pueden afectar a cualquier fragmento dependiente.
* Los modelos son una compilación de tipos de datos.
* Las funciones para agregar nuevas variaciones, etc., deben actualizar el fragmento en consecuencia.

  >[!NOTE]
  >
  >Para que pueda mostrar/procesar un fragmento de contenido, su cuenta debe tener `read` permisos para el modelo.

  >[!CAUTION]
  >
  >Cualquier cambio en un modelo de fragmento de contenido existente puede afectar a los fragmentos dependientes, lo que puede generar propiedades huérfanas en esos fragmentos.

### Integración de Sites con Assets {#integration-of-sites-with-assets}

La administración de fragmentos de contenido (CFM) forma parte de AEM Assets como:

* Los fragmentos de contenido son recursos.
* Utilizan la funcionalidad existente de Assets.
* Están totalmente integrados con los recursos (Admin Console, etc.).

Los fragmentos de contenido se consideran una función de Sites como:

* Se utilizan para crear páginas.

#### Asignación de fragmentos de contenido a los recursos {#mapping-content-fragments-to-assets}

![fragmento de contenido a recursos](assets/content-fragment-to-assets.png)

Los fragmentos de contenido, basados en un modelo de fragmento de contenido, se asignan a un único recurso:

* Todo el contenido se almacena en `jcr:content/data` nodo del recurso:

   * Los datos del elemento se almacenan en el subnodo principal:
     `jcr:content/data/master`

   * Las variaciones se almacenan en un subnodo que lleva el nombre de la variación: por ejemplo, `jcr:content/data/myvariation`

   * Los datos de cada elemento se almacenan en el subnodo respectivo como una propiedad con el nombre del elemento: por ejemplo, el contenido del elemento `text` se almacena como propiedad `text` el `jcr:content/data/master`

* Los metadatos y el contenido asociado se almacenan a continuación `jcr:content/metadata`
Excepto el título y la descripción, que no se consideran metadatos tradicionales y se almacenan en `jcr:content`

#### Ubicación del recurso {#asset-location}

Al igual que con los recursos estándar, un fragmento de contenido se encuentra en:

`/content/dam`

#### Permisos de recursos {#asset-permissions}

Para obtener más información, consulte [Fragmento de contenido: Eliminar consideraciones](/help/sites-cloud/administering/content-fragments/content-fragments-delete.md).

#### Integración de funciones {#feature-integration}

Para integrar con el núcleo de Assets:

* La función Administración de fragmentos de contenido (CFM) se basa en el núcleo Recursos.

* CFM proporciona sus propias implementaciones para elementos en las vistas de tarjeta, columna o lista; estos se conectan a las implementaciones de representación de contenido de Assets existentes.

* Se han ampliado varios componentes de Assets para adaptarse a los fragmentos de contenido.

### Uso de fragmentos de contenido en páginas {#using-content-fragments-in-pages}

>[!CAUTION]
>
>El [El componente Fragmento de contenido forma parte de los componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=es). Consulte [Desarrollo de componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html) para obtener más información.

AEM Se puede hacer referencia a los fragmentos de contenido desde páginas de recursos de la misma manera que desde cualquier otro tipo de recurso. AEM proporciona el **[Componente principal del fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=es)** - a [que le permite incluir fragmentos de contenido en las páginas](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-a-content-fragment-to-your-page). También puede ampliar esta **[Fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html)** componente principal.

* El componente utiliza el `fragmentPath` para hacer referencia al fragmento de contenido real. El `fragmentPath` La propiedad de se gestiona de la misma manera que propiedades similares de otros tipos de recursos; por ejemplo, cuando el fragmento de contenido se mueve a otra ubicación.

* El componente le permite seleccionar la variación que se va a mostrar.

* Además, se puede seleccionar un rango de párrafos para restringir la salida; por ejemplo, esto se puede utilizar para la salida de varias columnas.

* El componente permite contenido intermedio:

   * Aquí el componente le permite colocar otros recursos (imágenes, etc.) entre los párrafos del fragmento al que se hace referencia.

   * Para el contenido intermedio, debe:

      * tenga en cuenta la posibilidad de referencias inestables; el contenido intermedio (añadido al crear una página) no tiene relación fija con el párrafo al que se coloca junto, insertando un nuevo párrafo (en el editor de fragmentos de contenido) antes de que la posición del contenido intermedio pueda perder la posición relativa

      * tenga en cuenta los parámetros adicionales (como los filtros de variación y de párrafo) para configurar lo que se procesa en la página

>[!NOTE]
>
>**Modelo de fragmento de contenido:**
>
>Cuando se utiliza un fragmento de contenido en una página, se hace referencia al modelo de fragmento de contenido en el que se basa.
>
>Esto significa que si el modelo no se ha publicado en el momento de publicar la página, se marcará y el modelo se añadirá a los recursos que se publicarán con la página.

### Integración con otros marcos {#integration-with-other-frameworks}

Los fragmentos de contenido se pueden integrar con:

* **Traducciones**

  Los fragmentos de contenido están totalmente integrados con el [AEM Flujo de trabajo de traducción](/help/sites-cloud/administering/translation/overview.md). A nivel arquitectónico, esto significa:

   * Las traducciones individuales de un fragmento de contenido son en realidad fragmentos independientes; por ejemplo:

      * se encuentran bajo diferentes raíces de idioma; pero comparten exactamente la misma ruta relativa debajo de la raíz de idioma relevante:

        `/content/dam/<path>/en/<to>/<fragment>`

        frente a

        `/content/dam/<path>/de/<to>/<fragment>`

   * Además de las rutas basadas en reglas, no hay ninguna conexión adicional entre las distintas versiones de idioma de un fragmento de contenido; se gestionan como dos fragmentos independientes, aunque la interfaz de usuario proporciona los medios para navegar entre las variantes de idioma.

  >[!NOTE]
  >
  >AEM El flujo de trabajo de traducción de funciona con `/content`:
  >
  >* Como residen los modelos de fragmento de contenido en `/conf`, no se incluyen en dichas traducciones. Puede internacionalizar las cadenas de interfaz de usuario.

* **Esquemas de metadatos**

   * Fragmentos de contenido (re)utilizar [esquemas de metadatos](/help/assets/metadata-schemas.md), que se puede definir con recursos estándar.

   * CFM proporciona su propio esquema específico:

     `/libs/dam/content/schemaeditors/forms/contentfragment`

     esto se puede ampliar si es necesario.

   * El formulario de esquema respectivo se integra con el editor de fragmentos.

## La API de administración de fragmentos de contenido: del lado del servidor {#the-content-fragment-management-api-server-side}

Puede utilizar la API del lado del servidor para acceder a sus fragmentos de contenido; consulte:

[com.adobe.cq.dam.cfm](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/package-summary.html#package.description)

>[!CAUTION]
>
>Se recomienda encarecidamente utilizar la API del lado del servidor en lugar de acceder directamente a la estructura de contenido.

### Interfaces clave {#key-interfaces}

Las tres interfaces siguientes pueden servir como puntos de entrada:

* **Fragmento de contenido** ([FragmentoDeContenido](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

  Esta interfaz le permite trabajar con un fragmento de contenido de forma abstracta.

  La interfaz de le proporciona los medios para lo siguiente:

   * Administrar datos básicos (por ejemplo, obtener nombre; obtener/establecer título/descripción)
   * Acceso a metadatos
   * Elementos de acceso:

      * Lista de elementos
      * Obtener elementos por nombre
      * Creación de nuevos elementos (consulte [Advertencias](#caveats))

      * Acceder a datos de elementos (consulte `ContentElement`)

   * Variaciones de lista definidas para el fragmento
   * Crear nuevas variaciones globalmente
   * Administrar contenido asociado:

      * Enumerar colecciones
      * Agregar colecciones
      * Eliminar colecciones

   * Acceso al modelo del fragmento

  Las interfaces que representan los elementos principales de un fragmento son:

   * **Elemento de contenido** ([ContentElement](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * Obtener datos básicos (nombre, título, descripción)
      * Obtener/establecer contenido
      * Variaciones de acceso de un elemento:

         * Variaciones de lista
         * Obtener variaciones por nombre
         * Crear nuevas variaciones (consulte [Advertencias](#caveats))
         * Eliminar variaciones (consulte [Advertencias](#caveats))
         * Acceso a datos de variación (consulte `ContentVariation`)

      * Método abreviado para resolver variaciones (aplicar alguna lógica de reserva adicional específica de la implementación si la variación especificada no está disponible para un elemento)

   * **Variación de contenido** ([ContentVariation](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * Obtener datos básicos (nombre, título, descripción)
      * Obtener/establecer contenido
      * Sincronización simple, basada en la información de la última modificación

  Las tres interfaces ( `ContentFragment`, `ContentElement`, `ContentVariation`) ampliar el `Versionable` La interfaz de, que agrega funcionalidades de versiones, necesarias para los fragmentos de contenido:

   * Crear nueva versión del elemento
   * Enumerar versiones del elemento
   * Obtener el contenido de una versión específica del elemento con versión

### Adaptación: uso de adaptTo() {#adapting-using-adaptto}

Se pueden adaptar las siguientes opciones:

* `ContentFragment` se puede adaptar a:

   * `Resource` : el recurso de Sling subyacente; actualizar el recurso de Sling subyacente `Resource` requiere directamente la reconstrucción de `ContentFragment` objeto.

   * `Asset` - el DAM `Asset` abstracción que representa el fragmento de contenido; actualizar el fragmento de contenido `Asset` requiere directamente la reconstrucción de `ContentFragment` objeto.

* `ContentElement` se puede adaptar a:

   * [`ElementTemplate`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ElementTemplate.html) - para acceder a la información estructural del elemento.

* [`FragmentTemplate`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html)

* `Resource` se puede adaptar a:

   * `ContentFragment`

### Advertencias {#caveats}

Cabe señalar que:

* Toda la API está diseñada para **no** mantener los cambios automáticamente (a menos que se indique lo contrario en el JavaDoc de la API). Por lo tanto, siempre tendrá que asignar el solucionador de recursos de la solicitud correspondiente (o el solucionador que esté utilizando).

* Tareas que pueden requerir un esfuerzo adicional:

   * Se recomienda encarecidamente crear nuevas variaciones de `ContentFragment`. Esto garantiza que todos los elementos compartan esta variación y que las estructuras de datos globales adecuadas se actualicen según sea necesario para reflejar la variación recién creada en la estructura de contenido.

   * Eliminación de variaciones existentes mediante un elemento, utilizando `ContentElement.removeVariation()`, no actualizará las estructuras de datos globales asignadas a la variación. Para asegurarse de que estas estructuras de datos se mantienen sincronizadas, utilice `ContentFragment.removeVariation()` en su lugar, elimina una variación de forma global.

## La API de administración de fragmentos de contenido: del lado del cliente {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>La API del lado del cliente es interna.

### Información adicional {#additional-information}

Consulte lo siguiente:

* `filter.xml`

  El `filter.xml` para la administración de fragmentos de contenido está configurada para que no se superponga con el paquete de contenido principal de Assets.

## Editar sesiones {#edit-sessions}

>[!CAUTION]
>
>Tenga en cuenta esta información básica. Se supone que no debe cambiar nada aquí (ya que está marcado como *zona privada* en el repositorio), pero en algunos casos puede ser útil comprender cómo funcionan las cosas bajo el capó.

La edición de un fragmento de contenido, que puede abarcar varias vistas (= páginas de HTML), es atómica. AEM Como estas funciones atómicas de edición de varias vistas no son un concepto típico de los fragmentos de contenido, utilizan lo que se denomina un elemento de edición de vista múltiple *sesión de edición*.

Se inicia una sesión de edición cuando el usuario abre un fragmento de contenido en el editor. La sesión de edición finaliza cuando el usuario abandona el editor seleccionando una de las siguientes opciones **Guardar** o **Cancelar**.

Técnicamente, todas las ediciones se realizan en *live* AEM contenido, al igual que con el resto de ediciones de la. Cuando se inicia la sesión de edición, se crea una versión del estado actual sin editar. Si un usuario cancela una edición, se restaura esa versión. Si el usuario hace clic en **Guardar**, no se realiza ninguna acción específica, ya que toda la edición se ejecutó el *live* contenido, por lo tanto todos los cambios ya se han mantenido. Además, hacer clic en **Guardar** almacenará en déclencheur algún procesamiento en segundo plano (como la creación de información de búsqueda de texto completo o la administración de recursos de medios mixtos).

Existen algunas medidas de seguridad para los casos extremos; por ejemplo, si el usuario intenta salir del editor sin guardar o cancelar la sesión de edición. Además, hay disponible un guardado automático periódico para evitar la pérdida de datos.
Tenga en cuenta que dos usuarios pueden editar el mismo fragmento de contenido simultáneamente y, por lo tanto, sobrescribir los cambios de los demás. Para evitarlo, el fragmento de contenido debe bloquearse aplicando el de la administración de DAM *Finalizar compra* acción en el fragmento.

## Ejemplos {#examples}

### Ejemplo: Acceso a un fragmento de contenido existente {#example-accessing-an-existing-content-fragment}

Para lograrlo, puede adaptar el recurso que representa la API a:

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
`FragmentTemplate` adaptado de un recurso de modelo.

Por ejemplo:

```java
Resource modelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = modelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### Ejemplo: Especificación del intervalo de guardado automático {#example-specifying-the-auto-save-interval}

El [intervalo de guardado automático](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#save-close-and-versions) (medido en segundos) se puede definir mediante el administrador de configuración (ConfMgr):

* Nodo: `<conf-root>/settings/dam/cfm/jcr:content`
* Nombre de la propiedad: `autoSaveInterval`
* Tipo: `Long`

* Predeterminado: `600` (10 minutos); se define en `/libs/settings/dam/cfm/jcr:content`

Si desea establecer un intervalo de guardado automático de 5 minutos, debe definir la propiedad en el nodo; por ejemplo:

* Nodo: `/conf/global/settings/dam/cfm/jcr:content`
* Nombre de la propiedad: `autoSaveInterval`

* Tipo: `Long`

* Valor: `300` (5 minutos equivalen a 300 segundos)

## Componentes para la creación de páginas {#components-for-page-authoring}

Para obtener más información, consulte lo siguiente

* [Componentes principales: componente Fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=es) (recomendado)
