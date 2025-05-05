---
title: Uso de la fusión de recursos de Sling en Adobe Experience Manager as a Cloud Service
description: La fusión de recursos de Sling proporciona servicios para acceder y combinar recursos
exl-id: 5b6e5cb5-4c6c-4246-ba67-6b9f752867f5
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 1%

---

# Usar la fusión de recursos de Sling en AEM as a Cloud Service {#using-the-sling-resource-merger-in-aem}

## Función {#purpose}

La fusión de recursos de Sling proporciona servicios para acceder y combinar recursos. Proporciona mecanismos de diferencia (diferenciación) para:

* **[Superposiciones](/help/implementing/developing/introduction/overlays.md)** de recursos usando las [rutas de búsqueda](/help/implementing/developing/introduction/overlays.md#search-paths).

* **Invalida** los cuadros de diálogo de componentes para la interfaz de usuario táctil (`cq:dialog`) mediante la jerarquía de tipo de recurso (mediante la propiedad `sling:resourceSuperType`).

Con la fusión de recursos de Sling, los recursos de superposición/anulación o las propiedades se combinan con los recursos/propiedades originales:

* El contenido de la definición personalizada tiene una prioridad mayor que la del original (es decir, *se superpone* o *lo invalida*).

* Si es necesario, [properties](#properties) se ha definido en la personalización para indicar cómo se utilizará el contenido combinado del original.

>[!CAUTION]
>
>La fusión de recursos de Sling y los métodos relacionados solo se pueden usar con la interfaz de usuario táctil (que es la única interfaz de usuario disponible para AEM as a Cloud Service).

### AEM Metas para la {#goals-for-aem}

AEM Los objetivos para utilizar la fusión de recursos de Sling en son los siguientes:

* asegúrese de que no se realicen cambios de personalización en `/libs`.
* reduzca la estructura que se replica desde `/libs`.

  Al utilizar la fusión de recursos de Sling, no se recomienda copiar toda la estructura de `/libs`, ya que esto haría que se retuviera demasiada información en la personalización (normalmente `/apps`). La duplicación de información aumenta innecesariamente las posibilidades de que se produzcan problemas cuando el sistema se actualiza de alguna manera.

>[!CAUTION]
>
>Usted ***no debe*** cambiar nada en la ruta de acceso `/libs`.
>
>Esto se debe a que el contenido de `/libs` se puede sobrescribir cada vez que se apliquen actualizaciones a la instancia.
>
>* Las superposiciones dependen de [las rutas de búsqueda](/help/implementing/developing/introduction/overlays.md#search-paths).
>
>* Las invalidaciones no dependen de las rutas de búsqueda, utilizan la propiedad `sling:resourceSuperType` para establecer la conexión.
>
>Sin embargo, las invalidaciones a menudo se definen en `/apps`, ya que la práctica recomendada en AEM as a Cloud Service es definir personalizaciones en `/apps`; esto se debe a que no debe cambiar nada en `/libs`.

### Propiedades {#properties}

La combinación de recursos proporciona las siguientes propiedades:

* `sling:hideProperties` ( `String` o `String[]`)

  Especifica la propiedad o lista de propiedades que se van a ocultar.

  El comodín `*` oculta todo.

* `sling:hideResource` (`Boolean`)

  Indica si los recursos deben estar completamente ocultos, incluidos sus elementos secundarios.

* `sling:hideChildren` ( `String` o `String[]`)

  Contiene el nodo secundario o la lista de nodos secundarios que se van a ocultar. Las propiedades del nodo se mantienen.

  El comodín `*` oculta todo.

* `sling:orderBefore` (`String`)

  Contiene el nombre del nodo del mismo nivel en el que el nodo actual debe colocarse delante de.

Estas propiedades afectan al modo en que la superposición/invalidación utiliza los recursos/propiedades correspondientes/originales (de `/libs`) (a menudo en `/apps`).

### Creación de la estructura {#creating-the-structure}

Para crear una superposición o invalidación, debe volver a crear el nodo original, con la estructura equivalente, en el destino (normalmente `/apps`). Por ejemplo:

* Superposición

   * La definición de la entrada de navegación para la consola Sitios, como se muestra en el carril, se define en:

     `/libs/cq/core/content/nav/sites/jcr:title`

   * Para superponer esto, cree el siguiente nodo:

     `/apps/cq/core/content/nav/sites`

     A continuación, actualice la propiedad `jcr:title` según sea necesario.

* Omitir

   * La definición del cuadro de diálogo táctil para la consola Textos se define en:

     `/libs/foundation/components/text/cq:dialog`

   * Para anular esto, cree el siguiente nodo, por ejemplo:

     `/apps/the-project/components/text/cq:dialog`

Para crear cualquiera de estos elementos, sólo es necesario volver a crear la estructura del esqueleto. Para simplificar la recreación de la estructura, todos los nodos intermedios pueden ser del tipo `nt:unstructured` (no tienen que reflejar el tipo de nodo original; por ejemplo, en `/libs`).

Por lo tanto, en el ejemplo de superposición anterior, se necesitan los siguientes nodos:

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
>Al utilizar la fusión de recursos de Sling (es decir, al trabajar con la interfaz de usuario táctil estándar), no se recomienda copiar toda la estructura de `/libs`, ya que se mantendría demasiada información en `/apps`. Esto puede causar problemas cuando el sistema se actualiza de alguna manera.

### Casos de uso {#use-cases}

Estas funciones, junto con las funciones estándar, permiten:

* **Agregar una propiedad**

  La propiedad no existe en la definición de `/libs`, pero es necesaria en la superposición/invalidación de `/apps`.

   1. Crear el nodo correspondiente en `/apps`
   1. Crear la nueva propiedad en este nodo &quot;

* **Redefinir una propiedad (no propiedades creadas automáticamente)**

  La propiedad está definida en `/libs`, pero se requiere un nuevo valor en la superposición/invalidación de `/apps`.

   1. Crear el nodo correspondiente en `/apps`
   1. Cree la propiedad coincidente en este nodo (en / `apps`)

      * La propiedad tendrá una prioridad basada en la configuración de Sling Resource Resolver.
      * Se admite el cambio del tipo de propiedad.

        Si utiliza un tipo de propiedad distinto del utilizado en `/libs`, se utilizará el tipo de propiedad definido.

  >[!NOTE]
  >
  >Se admite el cambio del tipo de propiedad.

* **Redefinir una propiedad creada automáticamente**

  De manera predeterminada, las propiedades creadas automáticamente (como `jcr:primaryType`) no están sujetas a una superposición/invalidación para garantizar que se respete el tipo de nodo que se encuentra actualmente en `/libs`. Para imponer una superposición o invalidación, debe volver a crear el nodo en `/apps`, ocultar explícitamente la propiedad y redefinirla:

   1. Cree el nodo correspondiente en `/apps` con el `jcr:primaryType` deseado
   1. Cree la propiedad `sling:hideProperties` en ese nodo, con el valor establecido en la propiedad creada automáticamente; por ejemplo, `jcr:primaryType`

      Esta propiedad, definida en `/apps`, tendrá ahora prioridad sobre la definida en `/libs`

* **Redefinir un nodo y sus elementos secundarios**

  El nodo y sus elementos secundarios se definen en `/libs`, pero se requiere una nueva configuración en la superposición/invalidación de `/apps`.

   1. Combine las acciones de:

      1. Ocultar tareas secundarias de un nodo (conservando las propiedades del nodo)
      1. Redefinir la propiedad o las propiedades

* **Ocultar una propiedad**

  La propiedad está definida en `/libs`, pero no es necesaria en la superposición/invalidación de `/apps`.

   1. Crear el nodo correspondiente en `/apps`
   1. Crear una propiedad `sling:hideProperties` de tipo `String` o `String[]`. Utilice esta opción para especificar las propiedades que se ocultarán o ignorarán. También se pueden utilizar caracteres comodín. Por ejemplo:

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **Ocultar un nodo y sus elementos secundarios**

  El nodo y sus elementos secundarios se definen en `/libs`, pero no son necesarios en la superposición/invalidación de `/apps`.

   1. Cree el nodo correspondiente en /apps
   1. Crear una propiedad `sling:hideResource`

      * tipo: `Boolean`
      * valor: `true`

* **Ocultar elementos secundarios de un nodo (conservando las propiedades del nodo)**

  El nodo, sus propiedades y sus elementos secundarios se definen en `/libs`. El nodo y sus propiedades son necesarios en la superposición/invalidación de `/apps`, pero algunos o todos los nodos secundarios no son necesarios en la superposición/invalidación de `/apps`.

   1. Cree el nodo correspondiente en `/apps`
   1. Crear la propiedad `sling:hideChildren`:

      * tipo: `String[]`
      * value: una lista de los nodos secundarios (tal como se definen en `/libs`) que se deben ocultar o omitir

      El comodín &ast; se puede usar para ocultar o ignorar todos los nodos secundarios.

* **Reordenar nodos**

  El nodo y sus hermanos se definen en `/libs`. Se requiere una nueva posición para que el nodo se vuelva a crear en la superposición/invalidación de `/apps`, donde la nueva posición se define en referencia al nodo del mismo nivel apropiado en `/libs`.

   * Usar la propiedad `sling:orderBefore`:

      1. Cree el nodo correspondiente en `/apps`
      1. Crear la propiedad `sling:orderBefore`:

         Esto especifica el nodo (como en `/libs`) antes del cual se debe colocar el nodo actual:

         * tipo: `String`
         * valor: `<before-SiblingName>`

### Invocar la fusión de recursos de Sling desde el código {#invoking-the-sling-resource-merger-from-your-code}

La fusión de recursos de Sling incluye dos proveedores de recursos personalizados: uno para superposiciones y otro para invalidaciones. Cada uno de ellos se puede invocar dentro del código utilizando un punto de montaje:

>[!NOTE]
>
>Al acceder al recurso, se recomienda utilizar el punto de montaje adecuado.
>
>Esto garantiza que se invoque la fusión de recursos de Sling y que se devuelva el recurso totalmente combinado (reduciendo la estructura que debe replicarse desde `/libs`).

* Superposición:

   * objetivo: combinar recursos en función de su ruta de búsqueda
   * punto de montaje: `/mnt/overlay`
   * uso: `mount point + relative path`
   * ejemplo:

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* Anular:

   * objetivo: combinar recursos en función de su supertipo
   * punto de montaje: `/mnt/overide`
   * uso: `mount point + absolute path`
   * ejemplo:

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

