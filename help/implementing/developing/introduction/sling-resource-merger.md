---
title: Uso de la fusión de recursos Sling en Adobe Experience Manager como Cloud Service
description: La fusión de recursos de Sling proporciona servicios para acceder a los recursos y combinarlos
translation-type: tm+mt
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 2%

---


# Usar la fusión de recursos de Sling en AEM as a Cloud Service {#using-the-sling-resource-merger-in-aem}

## Función {#purpose}

La fusión de recursos de Sling proporciona servicios para acceder a los recursos y combinarlos. Proporciona mecanismos diferentes (de diferenciación) para:

* **[](/help/implementing/developing/introduction/overlays.md)** Superposiciones de recursos que utilizan las rutas [ de ](/help/implementing/developing/introduction/overlays.md#search-paths)búsqueda.

* **** Información general sobre los cuadros de diálogo de componentes para la IU táctil (`cq:dialog`), mediante la jerarquía de tipos de recursos (mediante la propiedad  `sling:resourceSuperType`).

Con la fusión de recursos de Sling, los recursos y/o propiedades de superposición/anulación se combinan con los recursos/propiedades originales:

* El contenido de la definición personalizada tiene una prioridad mayor que la del original (es decir, *se superpone* o *lo reemplaza*).

* Cuando sea necesario, [propiedades](#properties) definidas en la personalización, indique cómo se utilizará el contenido combinado del original.

<!-- Still links to reference material in 6.5 -->

>[!CAUTION]
>
>La fusión de recursos de Sling y los métodos relacionados solo se pueden usar con la IU táctil (que es la única IU disponible para AEM como Cloud Service).

### Objetivos para AEM {#goals-for-aem}

Los objetivos para utilizar la fusión de recursos Sling en AEM son:

* asegúrese de que los cambios de personalización no se realicen en `/libs`.
* reduzca la estructura que se replica desde `/libs`.

   Al utilizar la fusión de recursos de Sling no se recomienda copiar toda la estructura de `/libs`, ya que esto provocaría que se retuviera demasiada información en la personalización (generalmente `/apps`). La duplicación de información aumenta innecesariamente la posibilidad de problemas cuando el sistema se actualiza de alguna manera.

>[!CAUTION]
>
>Usted ***no debe*** cambiar nada en la ruta `/libs`.
>
>Esto se debe a que el contenido de `/libs` puede sobrescribirse cada vez que se apliquen actualizaciones a la instancia.
>
>* Las superposiciones dependen de [rutas de búsqueda](/help/implementing/developing/introduction/overlays.md#search-paths).
   >
   >
* Las anulaciones no dependen de las rutas de búsqueda, sino que utilizan la propiedad `sling:resourceSuperType` para realizar la conexión.
>
>
Sin embargo, las sobrescrituras se definen generalmente en `/apps`, ya que lo más recomendable en AEM como Cloud Service es definir las personalizaciones en `/apps`; esto se debe a que no debe cambiar nada en `/libs`.

### Propiedades {#properties}

La combinación de recursos proporciona las siguientes propiedades:

* `sling:hideProperties` (  `String` o  `String[]`)

   Especifica la propiedad, o lista de propiedades, que se va a ocultar.

   El comodín `*` oculta todo.

* `sling:hideResource` ( `Boolean`)

   Indica si los recursos deben estar completamente ocultos, incluidos sus elementos secundarios.

* `sling:hideChildren` (  `String` o  `String[]`)

   Contiene el nodo secundario, o lista de nodos secundarios, que se va a ocultar. Se mantendrán las propiedades del nodo.

   El comodín `*` oculta todo.

* `sling:orderBefore` (  `String`)

   Contiene el nombre del nodo del mismo nivel en el que se debe colocar el nodo actual delante de.

Estas propiedades afectan al modo en que los recursos/propiedades correspondientes/originales (de `/libs`) se utilizan en la superposición/sobrescritura (a menudo en `/apps`).

### Creación de la estructura {#creating-the-structure}

Para crear una superposición o sobrescritura, debe volver a crear el nodo original, con la estructura equivalente, en el destino (generalmente `/apps`). Por ejemplo:

* Superposición

   * La definición de la entrada de navegación para la consola Sitios, como se muestra en el carril, se define en:

      `/libs/cq/core/content/nav/sites/jcr:title`

   * Para superponer esto, cree el nodo siguiente:

      `/apps/cq/core/content/nav/sites`

      A continuación, actualice la propiedad `jcr:title` según sea necesario.

* Omitir

   * La definición del cuadro de diálogo táctil para la consola Textos se define en:

      `/libs/foundation/components/text/cq:dialog`

   * Para omitir esto, cree el nodo siguiente, por ejemplo:

      `/apps/the-project/components/text/cq:dialog`

Para crear cualquiera de estos elementos solo necesita volver a crear la estructura del esqueleto. Para simplificar la recreación de la estructura, todos los nodos intermediarios pueden ser del tipo `nt:unstructured` (no tienen que reflejar el tipo de nodo original; por ejemplo, en `/libs`).

Por lo tanto, en el ejemplo de superposición anterior, se necesitan los nodos siguientes:

```shell
/apps
  /cq
    /core
      /content
        /nav
          /sites
```

>[!NOTE]
>
>Cuando se utiliza la fusión de recursos Sling (es decir, cuando se trata de la IU estándar con capacidad táctil), no se recomienda copiar toda la estructura de `/libs`, ya que se obtendría demasiada información en `/apps`. Esto puede causar problemas cuando el sistema se ha actualizado de alguna manera.

### Casos de uso {#use-cases}

Estos, junto con la funcionalidad estándar, le permiten:

* **Añadir una propiedad**

   La propiedad no existe en la definición `/libs`, pero se requiere en la superposición/sobrescritura `/apps`.

   1. Cree el nodo correspondiente dentro de `/apps`
   1. Cree la nueva propiedad en este nodo &quot;

* **Redefinir una propiedad (no propiedades creadas automáticamente)**

   La propiedad se define en `/libs`, pero se requiere un nuevo valor en la superposición/sobrescritura `/apps`.

   1. Cree el nodo correspondiente dentro de `/apps`
   1. Cree la propiedad coincidente en este nodo (en / `apps`)

      * La propiedad tendrá una prioridad basada en la configuración de Sling Resource Resolver.
      * Se admite el cambio del tipo de propiedad.

         Si utiliza un tipo de propiedad diferente al utilizado en `/libs`, se utilizará el tipo de propiedad que defina.
   >[!NOTE]
   >
   >Se admite el cambio del tipo de propiedad.

* **Redefinición de una propiedad creada automáticamente**

   De forma predeterminada, las propiedades creadas automáticamente (como `jcr:primaryType`) no están sujetas a una superposición o anulación para garantizar que se respete el tipo de nodo que se encuentra actualmente en `/libs`. Para imponer una superposición/sobrescritura, debe volver a crear el nodo en `/apps`, ocultar explícitamente la propiedad y redefinirla:

   1. Cree el nodo correspondiente en `/apps` con el `jcr:primaryType` deseado
   1. Cree la propiedad `sling:hideProperties` en ese nodo, con el valor establecido en el de la propiedad creada automáticamente; por ejemplo, `jcr:primaryType`

      Esta propiedad, definida en `/apps`, ahora tendrá prioridad sobre la definida en `/libs`

* **Redefinir un nodo y sus elementos secundarios**

   El nodo y sus elementos secundarios se definen en `/libs`, pero se requiere una nueva configuración en la superposición/sobrescritura `/apps`.

   1. Combinar acciones de:

      1. Ocultar elementos secundarios de un nodo (manteniendo las propiedades del nodo)
      1. Redefinir propiedades

* **Ocultar una propiedad**

   La propiedad se define en `/libs`, pero no es necesaria en la superposición/anulación `/apps`.

   1. Cree el nodo correspondiente dentro de `/apps`
   1. Cree una propiedad `sling:hideProperties` de tipo `String` o `String[]`. Utilice esta opción para especificar las propiedades que se van a ocultar o ignorar. También se pueden utilizar comodines. Por ejemplo:

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **Ocultar un nodo y sus elementos secundarios**

   El nodo y sus elementos secundarios se definen en `/libs`, pero no se requieren en la superposición/sobrescritura `/apps`.

   1. Cree el nodo correspondiente en /apps
   1. Crear una propiedad `sling:hideResource`

      * tipo: `Boolean`
      * seleccionado: `true`

* **Ocultar elementos secundarios de un nodo (manteniendo las propiedades del nodo)**

   El nodo, sus propiedades y sus elementos secundarios se definen en `/libs`. El nodo y sus propiedades son obligatorios en la superposición/sobrescritura `/apps`, pero algunos o todos los nodos secundarios no son necesarios en la superposición/sobrescritura `/apps`.

   1. Cree el nodo correspondiente en `/apps`
   1. Cree la propiedad `sling:hideChildren`:

      * tipo: `String[]`
      * value: una lista de nodos secundarios (como se define en `/libs`) para ocultar/ignorar

      &amp;ast; comodín; puede utilizarse para ocultar o ignorar todos los nodos secundarios.


* **Reordenar nodos**

   El nodo y sus hermanos se definen en `/libs`. Se requiere una nueva posición para que el nodo se vuelva a crear en la superposición/sobrescritura `/apps`, donde la nueva posición se define en referencia al nodo del mismo nivel apropiado en `/libs`.

   * Utilice la propiedad `sling:orderBefore`:

      1. Cree el nodo correspondiente en `/apps`
      1. Cree la propiedad `sling:orderBefore`:

         Esto especifica el nodo (como en `/libs`) en el que se debe colocar el nodo actual antes de:

         * tipo: `String`
         * seleccionado: `<before-SiblingName>`

### Invocación de la fusión de recursos Sling desde su código {#invoking-the-sling-resource-merger-from-your-code}

La fusión de recursos de Sling incluye dos proveedores de recursos personalizados: uno para superposiciones y otro para anulaciones. Cada una de ellas se puede invocar en el código mediante un punto de montaje:

>[!NOTE]
>
>Al acceder al recurso, se recomienda utilizar el punto de montaje adecuado.
>
>Esto garantiza que se invoque la fusión de recursos Sling y se devuelva el recurso completamente combinado (lo que reduce la estructura que debe replicarse desde `/libs`).

* Superposición:

   * propósito: combinar recursos en función de su ruta de búsqueda
   * punto de montaje: `/mnt/overlay`
   * usage: `mount point + relative path`
   * ejemplo:

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* Omitir:

   * propósito: combinar recursos en función de su supertipo
   * punto de montaje: `/mnt/overide`
   * uso: `mount point + absolute path`
   * ejemplo:

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

<!--
### Example of Usage {#example-of-usage}

Some examples are covered:

* Overlay:

    * [Customizing the Consoles](/help/sites-developing/customizing-consoles-touch.md)
    * [Customizing Page Authoring](/help/sites-developing/customizing-page-authoring-touch.md)

* Override:

    * [Configuring your Page Properties](/help/sites-developing/page-properties-views.md#configuring-your-page-properties)
-->
