---
title: AEM marco de etiquetado
description: Etiquete el contenido y aproveche la infraestructura de etiquetado de AEM para clasificarlo y organizarlo.
translation-type: tm+mt
source-git-commit: 4bf023068aa69fb6b69c6f2443703ea2bbbf7d42
workflow-type: tm+mt
source-wordcount: '1567'
ht-degree: 0%

---


# El marco de etiquetado de AEM {#aem-tagging-framework}

El etiquetado permite categorizar y organizar el contenido. Las etiquetas se pueden clasificar mediante una Área de nombres y una taxonomía. Para obtener información detallada sobre el uso de etiquetas:

* Consulte [Uso de etiquetas](/help/sites-cloud/authoring/features/tags.md) para obtener información sobre el etiquetado de contenido como autor de contenido.
* Consulte Administración de etiquetas para conocer la perspectiva de un administrador sobre la creación y la administración de etiquetas, así como sobre las etiquetas de contenido que se han aplicado.

Este artículo se centra en el marco subyacente que admite el etiquetado en AEM y en cómo aprovecharlo como desarrollador.

## Introducción {#introduction}

Para etiquetar contenido y aprovechar la infraestructura de etiquetado de AEM:

* La etiqueta debe existir como un nodo de tipo [`cq:Tag`](#cq-tag-node-type) en el nodo raíz de la taxonomía [taxonomía.](#taxonomy-root-node)
* El `NodeType` nodo de contenido etiquetado debe incluir la mezcla [`cq:Taggable`](#taggable-content-cq-taggable-mixin).
* El [`TagID`](#tagid) se agrega a la propiedad [`cq:tags`](#cq-tags-property) del nodo de contenido y se resuelve en un nodo de tipo [`cq:Tag`.](#cq-tag-node-type)

## cq:Tipo de nodo de etiqueta {#cq-tag-node-type}

La declaración de una etiqueta se captura en el repositorio en un nodo de tipo `cq:Tag.`

* Una etiqueta puede ser una palabra simple (p. ej. `sky`) o representan una taxonomía jerárquica (p. ej. `fruit/apple`, lo que significa tanto la fruta genérica como la manzana más específica).
* Las etiquetas se identifican mediante un `TagID` único.
* Una etiqueta tiene información meta opcional, como un título, títulos localizados y una descripción. El título debe mostrarse en las interfaces de usuario en lugar de `TagID`, cuando esté presente.

El marco de etiquetado también permite restringir el uso de visitantes predefinidos y específicos por parte de los autores y del sitio.

### Características de la etiqueta {#tag-characteristics}

* El tipo de nodo es `cq:Tag`.
* El nombre del nodo es un componente de [`TagID`.](#tagid)
* El [`TagID`](#tagid) siempre incluye una [Área de nombres.](#tag-namespace)
* La propiedad `jcr:title` (el Título que se mostrará en la interfaz de usuario) es opcional.
* La propiedad `jcr:description` es opcional.
* Cuando contiene nodos secundarios, se denomina una etiqueta [contenedor.](#container-tags)
* La etiqueta se almacena en el repositorio debajo de una ruta de acceso base denominada nodo [raíz de taxonomía.](#taxonomy-root-node)

### ID de etiqueta {#tagid}

Un `TagID` identifica una ruta que se resuelve en un nodo de etiqueta en el repositorio.

Generalmente, `TagID` es un método abreviado `TagID` que comienza con la Área de nombres o puede ser un valor absoluto `TagID` que comienza en el nodo raíz de la taxonomía [.](#taxonomy-root-node)

Cuando se etiqueta contenido, si no existe todavía, la propiedad [`cq:tags`](#cq-tags-property) se agrega al nodo de contenido y el valor `TagID` se agrega al valor de matriz `String` de la propiedad.

El `TagID` consiste en una [Área de nombres](#tag-namespace) seguida del `TagID` local. [Los ](#container-tags) etiquetas de contenedor tienen subetiquetas que representan un orden jerárquico en la taxonomía. Las subetiquetas se pueden usar para hacer referencia a etiquetas igual que cualquier `TagID` local. Por ejemplo, se permite etiquetar contenido con `fruit`, aunque sea una etiqueta de contenedor con subetiquetas, como `fruit/apple` y `fruit/banana`.

### Nodo raíz de taxonomía {#taxonomy-root-node}

El nodo raíz de taxonomía es la ruta base para todas las etiquetas del repositorio. El nodo raíz de taxonomía debe *no* ser un nodo de tipo `cq:Tag`.

En AEM, la ruta de acceso base es `/content/cq:tags` y el nodo raíz es de tipo `cq:Folder`.

### Área de nombres de etiquetas {#tag-namespace}

Las Áreas de nombres permiten agrupar cosas. El caso de uso más típico es tener una Área de nombres por sitio (por ejemplo, pública o interna) o por aplicación más grande (por ejemplo, sitios o recursos), pero las Áreas de nombres se pueden utilizar para otras diversas necesidades. Las Áreas de nombres se utilizan en la interfaz de usuario para mostrar únicamente el subconjunto de etiquetas (es decir, las etiquetas de una determinada Área de nombres) que se aplica al contenido actual.

La Área de nombres de la etiqueta es el primer nivel del subárbol de taxonomía, que es el nodo inmediatamente inferior al nodo raíz de la taxonomía [.](#taxonomy-root-node) Una Área de nombres es un nodo de tipo  `cq:Tag` cuyo principal no es un tipo de  `cq:Tag` nodo.

Todas las etiquetas tienen una Área de nombres. Si no se especifica ninguna Área de nombres, la etiqueta se asigna a la Área de nombres predeterminada, que es `TagID` `default`, es decir, `/content/cq:tags/default`.  El Título se establece de forma predeterminada en `Standard Tags`en estos casos.

### Etiquetas de contenedor {#container-tags}

Una etiqueta contenedor es un nodo de tipo `cq:Tag` que contiene cualquier número y tipo de nodos secundarios, lo que permite mejorar el modelo de etiquetas con metadatos personalizados.

Además, las etiquetas de contenedor (o superetiquetas) de una taxonomía sirven de subsuma de todas las subetiquetas: por ejemplo, el contenido etiquetado con `fruit/apple` también se considera etiquetado con `fruit`, es decir, si busca contenido que se acaba de etiquetar con `fruit` también encontrará el contenido etiquetado con `fruit/apple`.

### Resolución de TagID {#resolving-tagids}

Si el ID de etiqueta contiene dos puntos (`:`), los dos puntos separan la Área de nombres de la etiqueta o subtaxonomía, que se separan con barras normales (`/`). Si el ID de etiqueta no tiene dos puntos, se da a entender la Área de nombres predeterminada.

La ubicación estándar y única de las etiquetas es inferior a `/content/cq:tags`.

Las etiquetas que hacen referencia a rutas o rutas no existentes que no apuntan a un nodo `cq:Tag` se consideran no válidas y se omiten.

La siguiente tabla muestra algunos ejemplos `TagID`s, sus elementos y cómo `TagID` se resuelve en una ruta absoluta en el repositorio:

| `TagID` | Espacio de nombres | ID local | Etiquetas de contenedor | Etiqueta de hoja | Ruta de la etiqueta absoluta del repositorio |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`,`apple` | `braeburn` | `content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | (ninguno) | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | (ninguno) | (ninguno) | (ninguno) | `/content/cq:tags/dam` |
| `content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `content/cq:tags/category/car` |

### Localización del título de la etiqueta {#localization-of-tag-title}

Cuando la etiqueta incluye la cadena de título opcional `jcr:title`, es posible localizar el título para la visualización agregando la propiedad `jcr:title.<locale>`.

Para obtener más información, consulte:

* [Etiquetas en distintos idiomas ](tagging-applications.md#tags-in-different-languages) que describen el uso de las API como desarrollador
* Administración de etiquetas en distintos idiomas, que describe el uso de la consola de etiquetado como administrador

### Control de acceso {#access-control}

Las etiquetas existen como nodos en el repositorio bajo el nodo raíz de la taxonomía [taxonomía.](#taxonomy-root-node) Permitir o denegar a los autores y visitantes del sitio la creación de etiquetas en una Área de nombres determinada se puede lograr estableciendo las ACL adecuadas en el repositorio.

La denegación de permisos de lectura para determinadas etiquetas o Áreas de nombres controlará la capacidad de aplicar etiquetas a contenido específico.

Una práctica típica incluye:

* Permitir el acceso de escritura de grupo/rol `tag-administrators` a todas las Áreas de nombres (agregar/modificar en `/content/cq:tags`). Este grupo viene con AEM lista para usar.
* Permitir que los usuarios/autores lean el acceso a todas las Áreas de nombres que deberían ser legibles para ellos (en su mayoría, todas).
* Permitir que los usuarios/autores escriban acceso a esas Áreas de nombres en las que los usuarios/autores deben definir las etiquetas libremente (`add_node` en `/content/cq:tags/some_namespace`)

## Contenido etiquetable: cq:Mezclador etiquetable {#taggable-content-cq-taggable-mixin}

Para que los desarrolladores de aplicaciones puedan adjuntar el etiquetado a un tipo de contenido, el registro del nodo ([CND](https://jackrabbit.apache.org/node-type-notation.html)) debe incluir la mezcla `cq:Taggable` o la mezcla `cq:OwnerTaggable`.

La mezcla `cq:OwnerTaggable`, que hereda de `cq:Taggable`, está pensada para indicar que el propietario/autor puede clasificar el contenido. En AEM, es sólo un atributo del nodo `cq:PageContent`. El marco de etiquetado no requiere la mezcla `cq:OwnerTaggable`.

>[!NOTE]
>
>Se recomienda habilitar únicamente etiquetas en el nodo de nivel superior de un elemento de contenido agregado (o en su nodo `jcr:content`). Algunos ejemplos son:
>
>* Páginas (`cq:Page`) donde el nodo `jcr:content`es de tipo `cq:PageContent`, que incluye la mezcla `cq:Taggable`.
>* Recursos (`cq:Asset`) donde el nodo `jcr:content/metadata` siempre tiene la mezcla `cq:Taggable`.


### Notación de tipo de nodo (CND) {#node-type-notation-cnd}

Existen definiciones de tipo de nodo en el repositorio como archivos CND. La notación CND se define como parte de la documentación [JCR.](https://jackrabbit.apache.org/node-type-notation.html).

Las definiciones esenciales para los tipos de nodos incluidos en la AEM son las siguientes:

```xml
[cq:Tag] > mix:title, nt:base
    orderable
    - * (undefined) multiple
    - * (undefined)
    + * (nt:base) = cq:Tag version

[cq:Taggable]
    mixin
    - cq:tags (string) multiple

[cq:OwnerTaggable] > cq:Taggable
    mixin
```

## cq:tags (propiedad) {#cq-tags-property}

La propiedad `cq:tags` es una matriz `String` utilizada para almacenar uno o más `TagID`s cuando los autores o visitantes del sitio los aplican al contenido. La propiedad sólo tiene significado cuando se agrega a un nodo definido con la mezcla [`cq:Taggable`](#taggable-content-cq-taggable-mixin).

>[!NOTE]
>
>Para aprovechar AEM funcionalidad de etiquetado, las aplicaciones desarrolladas personalizadas no deben definir propiedades de etiquetas distintas de `cq:tags`.

## Mover y combinar etiquetas {#moving-and-merging-tags}

A continuación, se muestra una descripción de los efectos del repositorio al mover o combinar etiquetas mediante la consola de etiquetado.

Cuando la etiqueta A se mueve o combina en la etiqueta B en `/content/cq:tags`:

* La etiqueta A no se elimina y recibe una propiedad `cq:movedTo`.
   * `cq:movedTo` apunta a la etiqueta B.
   * Esta propiedad significa que la etiqueta A se ha movido o combinado en la etiqueta B.
   * Al mover la etiqueta B se actualizará esta propiedad como corresponda.
   * La etiqueta A se oculta por lo tanto y solo se mantiene en el repositorio para resolver los ID de etiquetas de los nodos de contenido que apuntan a la etiqueta A.
   * El recolector de elementos no utilizados de etiquetas elimina etiquetas como la etiqueta A cuando ya no hay más nodos de contenido que apunten a ellas.
   * Un valor especial para la propiedad `cq:movedTo` es `nirvana`, que se aplica cuando se elimina la etiqueta pero no se puede eliminar del repositorio porque hay subetiquetas con `cq:movedTo` que se deben conservar.

      >[!NOTE]
      >
      >La propiedad `cq:movedTo` solo se agrega a la etiqueta movida o combinada si se cumple alguna de estas condiciones:
      >
      > 1. La etiqueta se utiliza en el contenido (es decir, tiene una referencia). O
      > 1. La etiqueta tiene elementos secundarios que ya se han movido.


* La etiqueta B se crea (en caso de movimiento) y recibe una propiedad `cq:backlinks`.
   * `cq:backlinks` mantiene las referencias en la otra dirección, es decir, mantiene una lista de todas las etiquetas que se han movido a la etiqueta B o que se han combinado con ella.
   * Esto es necesario principalmente para mantener las propiedades `cq:movedTo` actualizadas cuando la etiqueta B se mueve/combina/elimina también o cuando se activa la etiqueta B, en cuyo caso también se deben activar todas sus etiquetas de vínculos atrasados.

      >[!NOTE]
      >
      >La propiedad `cq:backlinks` solo se agrega a la etiqueta movida o combinada si se cumple alguna de estas condiciones:
      >
      > 1. La etiqueta se utiliza en el contenido (es decir, tiene una referencia). O
      > 1. La etiqueta tiene elementos secundarios que ya se han movido.


La lectura de una propiedad `cq:tags` de un nodo de contenido implica la siguiente resolución:

1. Si no hay coincidencia en `/content/cq:tags`, no se devuelve ninguna etiqueta.
1. Si la etiqueta tiene una propiedad `cq:movedTo` establecida, se sigue la ID de etiqueta a la que se hace referencia.
   * Este paso se repite siempre que la etiqueta seguida tenga una propiedad `cq:movedTo`.
1. Si la etiqueta seguida no tiene una propiedad `cq:movedTo`, se lee la etiqueta.

Para publicar el cambio cuando una etiqueta se ha movido o combinado, se debe replicar el nodo `cq:Tag` y todos sus vínculos atrasados. Esto se realiza automáticamente cuando la etiqueta se activa en la consola de administración de etiquetas.

Las actualizaciones posteriores a la propiedad `cq:tags` de la página limpian automáticamente las referencias antiguas. Esto se activa porque al resolver una etiqueta movida a través de la API se devuelve la etiqueta de destino, proporcionando así el ID de la etiqueta de destino.
