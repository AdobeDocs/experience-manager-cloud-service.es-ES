---
title: Personalizar y ampliar fragmentos de contenido
description: Un fragmento de contenido amplía un recurso estándar. Descubra cómo puede personalizarlos.
exl-id: 58152d6e-21b6-4f45-a45c-0f46ee58825e
feature: Developing, Content Fragments
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1689'
ht-degree: 2%

---

# Personalizar y ampliar fragmentos de contenido{#customizing-and-extending-content-fragments}

Dentro de Adobe Experience Manager as a Cloud Service, un fragmento de contenido amplía un recurso estándar; consulte:

* [Creación y administración de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/overview.md) y [Creación de páginas con fragmentos de contenido](/help/sites-cloud/authoring/fragments/content-fragments.md) para obtener más información acerca de los fragmentos de contenido.

* [Administración de Assets](/help/assets/manage-digital-assets.md) para obtener más información sobre los recursos estándar.

## Arquitectura {#architecture}

Las [partes constitutivas](/help/sites-cloud/administering/content-fragments/overview.md#constituent-parts-of-a-content-fragment) básicas de un fragmento de contenido son las siguientes:

* Un *fragmento de contenido*
* Consiste en uno o más *elementos de contenido*
* Puede tener una o más *variaciones de contenido*

Los fragmentos de contenido individuales se basan en modelos de fragmentos de contenido:

* Los modelos de fragmento de contenido definen la estructura de un fragmento de contenido cuando se crea.
* Un fragmento hace referencia al modelo, por lo que los cambios realizados en el modelo pueden afectar a cualquier fragmento dependiente o no.
* Los modelos son una compilación de tipos de datos.
* Las funciones para agregar nuevas variaciones, etc., deben actualizar el fragmento en consecuencia.

  >[!NOTE]
  >
  >Para que pueda mostrar/procesar un fragmento de contenido, su cuenta debe tener `read` permisos para el modelo.

  >[!CAUTION]
  >
  >Cualquier cambio en un modelo de fragmento de contenido existente puede afectar a los fragmentos dependientes, lo que puede generar propiedades huérfanas en esos fragmentos.

### Integración de Sites con Assets {#integration-of-sites-with-assets}

La administración de fragmentos de contenido (CFM) forma parte de Adobe Experience Manager (AEM) Assets como:

* Los fragmentos de contenido son recursos.
* Utilizan la funcionalidad existente de Assets.
* Están totalmente integrados con Assets (Admin Consoles, etc.).

Los fragmentos de contenido se consideran una función de AEM Sites como:

* Se utilizan para crear páginas.

#### Asignación de fragmentos de contenido a Assets {#mapping-content-fragments-to-assets}

![fragmento de contenido a recursos](assets/content-fragment-to-assets.png)

Los fragmentos de contenido, basados en un modelo de fragmento de contenido, se asignan a un único recurso:

* Todo el contenido se almacena en el nodo `jcr:content/data` del recurso:

   * Los datos del elemento se almacenan en el subnodo maestro:
     `jcr:content/data/master`

   * Las variaciones se almacenan en un subnodo que lleva el nombre de la variación:
por ejemplo, `jcr:content/data/myvariation`

   * Los datos de cada elemento se almacenan en el subnodo respectivo como una propiedad con el nombre del elemento:
por ejemplo, el contenido del elemento `text` se almacena como propiedad `text` en `jcr:content/data/master`

* Los metadatos y el contenido asociado se almacenan debajo de `jcr:content/metadata`
Excepto el título y la descripción, que no se consideran metadatos tradicionales y se almacenan en `jcr:content`

#### Ubicación del recurso {#asset-location}

Al igual que con los recursos estándar, un fragmento de contenido se encuentra en:

`/content/dam`

#### Permisos de recursos {#asset-permissions}

Ver [Fragmento de contenido: eliminar consideraciones](/help/sites-cloud/administering/content-fragments/delete-considerations.md).

#### Integración de funciones {#feature-integration}

Para integrar con Assets Core:

* La función Administración de fragmentos de contenido (CFM) se basa en el núcleo de Assets.

* CFM proporciona sus propias implementaciones para elementos en las vistas de tarjeta, columna o lista; estos se conectan a las implementaciones existentes de representación de contenido de Assets.

* Varios componentes de Assets se han ampliado para adaptarse a los fragmentos de contenido.

### Uso de fragmentos de contenido en páginas {#using-content-fragments-in-pages}

>[!CAUTION]
>
>El componente [Fragmento de contenido forma parte de los componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=es). Consulte [Desarrollar componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html) para obtener más información.

Se puede hacer referencia a los fragmentos de contenido desde páginas de AEM, como cualquier otro tipo de recurso. AEM proporciona el **[componente principal de fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=es)**: un [componente que le permite incluir fragmentos de contenido en sus páginas](/help/sites-cloud/authoring/fragments/content-fragments.md#adding-a-content-fragment-to-your-page). También puede ampliar este **[fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html)** componente principal.

* El componente utiliza la propiedad `fragmentPath` para hacer referencia al fragmento de contenido real. La propiedad `fragmentPath` se administra de la misma manera que propiedades similares de otros tipos de recursos; por ejemplo, cuando el fragmento de contenido se mueve a otra ubicación.

* El componente permite seleccionar la variación que se desea mostrar.

* Además, se puede seleccionar un rango de párrafos para restringir la salida; por ejemplo, esto se puede utilizar para la salida de varias columnas.

* El componente permite contenido intermedio:

   * En este caso, el componente le permite colocar otros recursos (imágenes, etc.) entre los párrafos del fragmento al que se hace referencia.

   * Para contenido intermedio:

      * Tenga en cuenta la posibilidad de referencias inestables. El contenido intermedio (añadido al crear una página) no tiene relación fija con el párrafo situado junto a él. La inserción de un nuevo párrafo (en el editor de fragmentos de contenido) antes de la posición del contenido intermedio puede perder la posición relativa.

      * Tenga en cuenta los parámetros adicionales (como los filtros de variación y de párrafo) para configurar lo que se procesa en la página.

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

  Los fragmentos de contenido están totalmente integrados con el [flujo de trabajo de traducción de AEM](/help/sites-cloud/administering/translation/overview.md). A nivel arquitectónico, esto significa:

   * Las traducciones individuales de un fragmento de contenido son fragmentos independientes; por ejemplo:

      * se encuentran en diferentes raíces de idioma, pero comparten la ruta relativa debajo de la raíz de idioma correspondiente:

        `/content/dam/<path>/en/<to>/<fragment>`

        frente a

        `/content/dam/<path>/de/<to>/<fragment>`

   * Además de las rutas basadas en reglas, no hay otra conexión entre las diferentes versiones de idioma de un fragmento de contenido. Se gestionan como dos fragmentos independientes, aunque la interfaz de usuario proporciona los medios para navegar entre las variantes de idioma.

  >[!NOTE]
  >
  >El flujo de trabajo de traducción de AEM funciona con `/content`:
  >
  >* Como los modelos de fragmento de contenido residen en `/conf`, no se incluyen en dichas traducciones. Puede internacionalizar las cadenas de interfaz de usuario.

* **Esquemas de metadatos**

   * Los fragmentos de contenido utilizan y reutilizan los [esquemas de metadatos](/help/assets/metadata-schemas.md) que se pueden definir con recursos estándar.

   * CFM proporciona su propio esquema específico:

     `/libs/dam/content/schemaeditors/forms/contentfragment`

     esto se puede ampliar, si es necesario.

   * El formulario de esquema respectivo se integra con el editor de fragmentos.

## La API de administración de fragmentos de contenido: del lado del servidor {#the-content-fragment-management-api-server-side}

Puede utilizar la API del lado del servidor para acceder a sus fragmentos de contenido; consulte:

[com.adobe.cq.dam.cfm](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/package-summary.html#package.description)

>[!CAUTION]
>
>Adobe recomienda utilizar la API del lado del servidor en lugar de acceder directamente a la estructura de contenido.

### Interfaces clave {#key-interfaces}

Las tres interfaces siguientes pueden servir como puntos de entrada:

* **Fragmento de contenido** ([Fragmento de contenido](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

  Esta interfaz permite trabajar con un fragmento de contenido de forma abstracta.

  La interfaz de le proporciona los medios para lo siguiente:

   * Administrar datos básicos (por ejemplo, obtener nombre; obtener/establecer título/descripción)
   * Acceso a metadatos
   * Elementos de acceso:

      * Lista de elementos
      * Obtener elementos por nombre
      * Crear elementos (vea [Advertencias](#caveats))

      * Acceder a datos de elementos (consulte `ContentElement`)

   * Variaciones de lista definidas para el fragmento
   * Crear variaciones globalmente
   * Administrar contenido asociado:

      * Enumerar colecciones
      * Agregar colecciones
      * Quitar colecciones

   * Acceso al modelo del fragmento

  Las interfaces que representan los elementos principales de un fragmento son:

   * **Elemento de contenido** ([Elemento de contenido](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * Obtener datos básicos (nombre, título, descripción)
      * Obtener/establecer contenido
      * Variaciones de acceso de un elemento:

         * Variaciones de lista
         * Obtener variaciones por nombre
         * Crear variaciones (consulte [Advertencias](#caveats))
         * Eliminar variaciones (consulte [Advertencias](#caveats))
         * Datos de variación de acceso (consulte `ContentVariation`)

      * Método abreviado para resolver variaciones (aplicar alguna lógica de reserva adicional específica de la implementación si la variación especificada no está disponible para un elemento)

   * **Variación de contenido** ([Variación de contenido](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * Obtener datos básicos (nombre, título, descripción)
      * Obtener/establecer contenido
      * Sincronización simple, basada en la información de la última modificación

  Las tres interfaces ( `ContentFragment`, `ContentElement`, `ContentVariation`) amplían la interfaz `Versionable`, que agrega capacidades de versiones, necesarias para los fragmentos de contenido:

   * Crear una versión del elemento
   * Enumerar versiones del elemento
   * Obtener el contenido de una versión específica del elemento con versión

### Adaptación: uso de adaptTo() {#adapting-using-adaptto}

Se pueden adaptar las siguientes opciones:

* `ContentFragment` se puede adaptar a:

   * `Resource`: el recurso de Sling subyacente; la actualización de `Resource` subyacente requiere directamente la reconstrucción del objeto `ContentFragment`.

   * `Asset`: la abstracción de DAM `Asset` que representa el fragmento de contenido; actualizar `Asset` requiere directamente la reconstrucción del objeto `ContentFragment`.

* `ContentElement` se puede adaptar a:

   * [`ElementTemplate`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ElementTemplate.html) - para obtener acceso a la información estructural del elemento.

* [`FragmentTemplate`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html)

* `Resource` se puede adaptar a:

   * `ContentFragment`

### Advertencias {#caveats}

Cabe señalar lo siguiente:

* La API completa está diseñada para **no** mantener los cambios automáticamente (a menos que se indique lo contrario en el JavaDoc de la API). Por lo tanto, asigne siempre el solucionador de recursos de la solicitud correspondiente (o el solucionador que esté utilizando).

* Tareas que pueden requerir un esfuerzo adicional:

   * Adobe recomienda crear variaciones de `ContentFragment`. Esto garantiza que todos los elementos compartan esta variación y que las estructuras de datos globales adecuadas se actualicen según sea necesario para reflejar la nueva variación en la estructura de contenido.

   * Al eliminar las variaciones existentes mediante un elemento, mediante `ContentElement.removeVariation()`, no se actualizan las estructuras de datos globales asignadas a la variación. Para asegurarse de que estas estructuras de datos se mantienen sincronizadas, use `ContentFragment.removeVariation()` en su lugar, lo que elimina una variación de forma global.

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
>Tenga en cuenta esta información básica. Se supone que no debe cambiar nada aquí (ya que está marcado como un *área privada* en el repositorio), pero a veces puede ayudar comprender cómo funcionan las cosas bajo el capó.

La edición de un fragmento de contenido, que puede abarcar varias vistas (= páginas de HTML), es atómica. Como estas funciones atómicas de edición de varias vistas no son un concepto típico de AEM, los fragmentos de contenido utilizan lo que se denomina *sesión de edición*.

Se inicia una sesión de edición cuando el usuario abre un fragmento de contenido en el editor. La sesión de edición finaliza cuando el usuario abandona el editor seleccionando **Guardar** o **Cancelar**.

Técnicamente, todas las ediciones se realizan en contenido *live*, como con todas las demás ediciones de AEM. Cuando se inicia la sesión de edición, se crea una versión del estado actual sin editar. Si un usuario cancela una edición, se restaura esa versión. Si el usuario hace clic en **Guardar**, no se realiza ninguna acción específica, ya que la edición se ejecutó en contenido de *live*, por lo que todos los cambios ya se han mantenido. Además, hacer clic en **Guardar** déclencheur algunos procesos en segundo plano, como la creación de información de búsqueda de texto completo, la administración de recursos de medios mixtos o ambos.

Existen algunas medidas de seguridad para los casos extremos; por ejemplo, si el usuario intenta salir del editor sin guardar o cancelar la sesión de edición. Además, hay disponible un guardado automático periódico para evitar la pérdida de datos.
Dos usuarios pueden editar el mismo fragmento de contenido simultáneamente y, por lo tanto, sobrescribir los cambios de los demás. Para evitarlo, el fragmento de contenido debe bloquearse aplicando la acción *Checkout* de la administración DAM en el fragmento.

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

### Ejemplo: Creación de un fragmento de contenido {#example-creating-a-new-content-fragment}

Para crear un fragmento de contenido mediante programación, use un `FragmentTemplate` adaptado de un recurso de modelo.

Por ejemplo:

```java
Resource modelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = modelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### Ejemplo: Especificación del intervalo de guardado automático {#example-specifying-the-auto-save-interval}

El [intervalo de guardado automático](/help/sites-cloud/administering/content-fragments/managing.md#save-close-and-versions) (medido en segundos) se puede definir mediante el administrador de configuración (ConfMgr):

* Nodo: `<conf-root>/settings/dam/cfm/jcr:content`
* Nombre de propiedad: `autoSaveInterval`
* Tipo: `Long`

* Predeterminado: `600` (10 minutos); definido en `/libs/settings/dam/cfm/jcr:content`

Si desea establecer un intervalo de guardado automático de 5 minutos, defina la propiedad en el nodo.

Por ejemplo:

* Nodo: `/conf/global/settings/dam/cfm/jcr:content`
* Nombre de propiedad: `autoSaveInterval`

* Tipo: `Long`

* Valor: `300` (5 minutos equivalen a 300 segundos)

## Componentes para la creación de páginas {#components-for-page-authoring}

Para obtener más información, consulte

* [Componentes principales - Componente de fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=es) (recomendado)
