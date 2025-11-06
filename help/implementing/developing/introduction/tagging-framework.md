---
title: Marco de trabajo de etiquetado de AEM
description: Etiquete contenido y utilice la infraestructura de Etiquetado de AEM para categorizarlo y organizarlo.
exl-id: 25418d44-aace-4e73-be1a-4b1902f40403
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1559'
ht-degree: 0%

---

# El marco de etiquetado de AEM {#aem-tagging-framework}

El etiquetado permite clasificar y organizar el contenido. Las etiquetas se pueden clasificar por un área de nombres y una taxonomía. Para obtener información detallada sobre el uso de etiquetas:

* Consulte [Uso de etiquetas](/help/sites-cloud/authoring/sites-console/tags.md) para obtener información sobre cómo etiquetar contenido como autor de contenido.
* Consulte Administración de etiquetas para conocer la perspectiva de un administrador sobre la creación y administración de etiquetas y sobre las etiquetas de contenido que se han aplicado.

Este artículo se centra en el marco de trabajo subyacente que admite el etiquetado en AEM y en cómo utilizarlo como desarrollador.

## Introducción {#introduction}

Para etiquetar contenido y utilizar la infraestructura de etiquetado de AEM:

* La etiqueta debe existir como un nodo de tipo [`cq:Tag`](#cq-tag-node-type) bajo el [nodo raíz de taxonomía](#taxonomy-root-node).
* El nodo de contenido etiquetado `NodeType` debe incluir el mixin [`cq:Taggable`](#taggable-content-cq-taggable-mixin).
* [`TagID`](#tagid) se agrega a la propiedad [`cq:tags`](#cq-tags-property) del nodo de contenido y se resuelve en un nodo de tipo [`cq:Tag`](#cq-tag-node-type).

## cq:Tag tipo de nodo {#cq-tag-node-type}

La declaración de una etiqueta se captura en el repositorio en un nodo de tipo `cq:Tag.`

* Una etiqueta puede ser una palabra simple (por ejemplo, `sky`) o representar una taxonomía jerárquica (por ejemplo, `fruit/apple`, es decir, tanto la fruta genérica como la manzana más específica).
* Las etiquetas se identifican con un(a) `TagID` único(a).
* Una etiqueta tiene información meta opcional, como un título, títulos localizados y una descripción. El título debe mostrarse en las interfaces de usuario en lugar de `TagID`, cuando esté presente.

El marco de etiquetado también restringe a los autores y visitantes del sitio a utilizar únicamente etiquetas específicas predefinidas.

### Características de etiquetas {#tag-characteristics}

* El tipo de nodo es `cq:Tag`.
* El nombre de nodo es un componente de [`TagID`](#tagid).
* [`TagID`](#tagid) siempre incluye un [área de nombres](#tag-namespace).
* La propiedad `jcr:title` (el Título que se mostrará en la interfaz de usuario) es opcional.
* La propiedad `jcr:description` es opcional.
* Cuando contiene nodos secundarios, se denomina [etiqueta contenedora](#container-tags).
* La etiqueta se almacena en el repositorio debajo de una ruta base denominada [nodo raíz de taxonomía](#taxonomy-root-node).

### ID de etiqueta {#tagid}

Un(a) `TagID` identifica una ruta que se resuelve en un nodo de etiqueta en el repositorio.

Normalmente, `TagID` es un método abreviado `TagID` que comienza con el espacio de nombres o puede ser un `TagID` absoluto que comienza desde el [nodo raíz de taxonomía](#taxonomy-root-node).

Cuando se etiqueta contenido, si aún no existe, la propiedad [`cq:tags`](#cq-tags-property) se agrega al nodo de contenido y `TagID` se agrega al valor de matriz `String` de la propiedad.

`TagID` consta de un [espacio de nombres](#tag-namespace) seguido del `TagID` local. [Las etiquetas de contenedor](#container-tags) tienen subetiquetas que representan un orden jerárquico en la taxonomía. Las subetiquetas se pueden usar para hacer referencia a etiquetas como cualquier `TagID` local. Por ejemplo, se permite etiquetar contenido con `fruit`, incluso si es una etiqueta contenedora con subetiquetas, como `fruit/apple` y `fruit/banana`.

### Nodo raíz de taxonomía {#taxonomy-root-node}

El nodo raíz de taxonomía es la ruta base para todas las etiquetas del repositorio. El nodo raíz de taxonomía debe *no* ser un nodo de tipo `cq:Tag`.

En AEM, la ruta de acceso base es `/content/cq:tags` y el nodo raíz es del tipo `cq:Folder`.

### Área de nombres de etiqueta {#tag-namespace}

Las áreas de nombres permiten agrupar cosas. El caso de uso más típico es tener un área de nombres por sitio (por ejemplo, pública frente a interna) o por aplicación más grande (por ejemplo, Sites o Assets), pero las áreas de nombres se pueden utilizar para otras necesidades. Los espacios de nombres se utilizan en la interfaz de usuario para mostrar únicamente el subconjunto de etiquetas (es decir, las etiquetas de un determinado espacio de nombres) que se aplica al contenido actual.

El área de nombres de la etiqueta es el primer nivel del subárbol de taxonomía, que es el nodo inmediatamente inferior al [nodo raíz de taxonomía](#taxonomy-root-node). Un área de nombres es un nodo de tipo `cq:Tag` cuyo primario no es un tipo de nodo `cq:Tag`.

Todas las etiquetas tienen un área de nombres. Si no se especifica ningún espacio de nombres, la etiqueta se asigna al espacio de nombres predeterminado, que es `TagID` `default`, es decir, `/content/cq:tags/default`. El título predeterminado es `Standard Tags` en estos casos.

### Etiquetas de contenedor {#container-tags}

Una etiqueta contenedora es un nodo de tipo `cq:Tag` que contiene cualquier número y tipo de nodos secundarios, lo que permite mejorar el modelo de etiqueta con metadatos personalizados.

Además, las etiquetas de contenedor (o superetiquetas) en una taxonomía sirven como subsuma de todas las subetiquetas. Por ejemplo, el contenido etiquetado con `fruit/apple` también se considera etiquetado con `fruit`. Es decir, si busca contenido etiquetado con `fruit`, también encontrará el contenido etiquetado con `fruit/apple`.

### Resolver TagID {#resolving-tagids}

Si el identificador de etiqueta contiene dos puntos (`:`), los dos puntos separan el área de nombres de la etiqueta o subtaxonomía, que después se separan con barras diagonales normales (`/`). Si el ID de etiqueta no tiene dos puntos, el área de nombres predeterminada es implícita.

La ubicación estándar y única de las etiquetas está por debajo de `/content/cq:tags`.

Las etiquetas que hacen referencia a rutas de acceso no existentes o que no apuntan a un nodo `cq:Tag` se consideran no válidas y se omiten.

En la tabla siguiente se muestran algunos `TagID` de muestra, sus elementos y cómo se resuelve `TagID` en una ruta de acceso absoluta del repositorio:

| `TagID` | Espacio de nombres | ID local | Etiquetas de contenedor | Etiqueta de hoja | Ruta de etiqueta absoluta del repositorio |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`,`apple` | `braeburn` | `content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | (ninguno) | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | (ninguno) | (ninguno) | (ninguno) | `/content/cq:tags/dam` |
| `content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `content/cq:tags/category/car` |

### Localización del título de la etiqueta {#localization-of-tag-title}

Cuando la etiqueta incluye la cadena de título opcional `jcr:title`, es posible localizar el título para mostrarlo agregando la propiedad `jcr:title.<locale>`.

Para obtener más información, consulte lo siguiente:

* [Las etiquetas en diferentes idiomas](tagging-applications.md#tags-in-different-languages) describen el uso de las API como desarrollador
* Administración de etiquetas en diferentes idiomas, que describen el uso de la consola de etiquetado como administrador

### Control de acceso {#access-control}

Las etiquetas existen como nodos en el repositorio bajo el [nodo raíz de taxonomía](#taxonomy-root-node). Permitir o denegar a los autores y visitantes del sitio la creación de etiquetas en un área de nombres determinada se puede lograr estableciendo ACL adecuados en el repositorio.

La denegación de permisos de lectura para determinadas etiquetas o áreas de nombres controla la capacidad de aplicar etiquetas a contenido específico.

Una práctica típica incluye:

* Permitiendo el acceso de escritura de grupo/función `tag-administrators` a todas las áreas de nombres (agregar/modificar en `/content/cq:tags`). Este grupo incluye AEM de forma predeterminada.
* Permite a los usuarios/autores acceder a todas las áreas de nombres que deben poder leerlas (principalmente todas).
* Permitir que los usuarios y los autores escriban en las áreas de nombres en las que los usuarios y los autores deben definir libremente las etiquetas (`add_node` en `/content/cq:tags/some_namespace`)

## Contenido etiquetable: cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

Para que los desarrolladores de aplicaciones adjunten el etiquetado a un tipo de contenido, el registro del nodo ([CND](https://jackrabbit.apache.org/jcr/node-type-notation.html)) debe incluir el mixin `cq:Taggable` o el mixin `cq:OwnerTaggable`.

El mixin `cq:OwnerTaggable`, que hereda de `cq:Taggable`, tiene la intención de indicar que el propietario/autor puede clasificar el contenido. En AEM, solo es un atributo del nodo `cq:PageContent`. El marco de etiquetado no requiere el mixin `cq:OwnerTaggable`.

>[!NOTE]
>
>Se recomienda habilitar solamente etiquetas en el nodo de nivel superior de un elemento de contenido agregado (o en su nodo `jcr:content`). Algunos ejemplos son:
>
>* Páginas (`cq:Page`) donde el nodo `jcr:content`es del tipo `cq:PageContent`, que incluye el mixin `cq:Taggable`.
>* Assets (`cq:Asset`) donde el nodo `jcr:content/metadata` siempre tiene la mezcla `cq:Taggable`.

### Notación de tipo de nodo (CND) {#node-type-notation-cnd}

Las definiciones del tipo de nodo existen en el repositorio como archivos CDN. La notación CDN se define como parte de [documentación JCR](https://jackrabbit.apache.org/jcr/node-type-notation.html).

Las definiciones esenciales para los tipos de nodo incluidos en AEM son las siguientes:

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

## Propiedad cq:tags {#cq-tags-property}

La propiedad `cq:tags` es una matriz `String` que se usa para almacenar uno o más `TagID` cuando los autores o visitantes del sitio los aplican al contenido. La propiedad solo tiene significado cuando se agrega a un nodo que se define con el mixin [`cq:Taggable`](#taggable-content-cq-taggable-mixin).

>[!NOTE]
>
>Para utilizar la funcionalidad de etiquetado de AEM, las aplicaciones desarrolladas personalizadas no deben definir propiedades de etiquetas distintas de `cq:tags`.

## Mover y combinar etiquetas {#moving-and-merging-tags}

A continuación se describen los efectos que se producen en el repositorio al mover o combinar etiquetas mediante la consola Etiquetado.

Cuando la etiqueta A se mueve o se combina con la etiqueta B en `/content/cq:tags`:

* La etiqueta A no se elimina y recibe una propiedad `cq:movedTo`.
   * `cq:movedTo` señala a la etiqueta B.
   * Esta propiedad significa que la etiqueta A se ha movido o combinado en la etiqueta B.
   * Al mover la etiqueta B, se actualiza esta propiedad en consecuencia.
   * Por lo tanto, la etiqueta A está oculta y solo se mantiene en el repositorio para que pueda resolver los ID de etiqueta en los nodos de contenido que apuntan a la etiqueta A.
   * El recolector de elementos no utilizados de etiquetas elimina las etiquetas como la etiqueta A una vez que los nodos de contenido no las señalan.
   * Un valor especial para la propiedad `cq:movedTo` es `nirvana`, que se aplica cuando se elimina la etiqueta, pero no se puede quitar del repositorio porque hay subetiquetas con un `cq:movedTo` que se deben conservar.

     >[!NOTE]
     >
     >La propiedad `cq:movedTo` solo se agrega a la etiqueta movida o combinada si se cumple cualquiera de estas condiciones:
     >
     > 1. La etiqueta se utiliza en el contenido (lo que significa que tiene una referencia). OR
     > 1. La etiqueta tiene elementos secundarios que ya se han movido.
     >
* La etiqueta B se crea (si hay un movimiento) y recibe una propiedad `cq:backlinks`.
   * `cq:backlinks` mantiene las referencias en la otra dirección. Es decir, mantiene una lista de todas las etiquetas que se han movido o combinado con la etiqueta B.
   * Esta funcionalidad es necesaria principalmente para mantener las propiedades de `cq:movedTo` actualizadas cuando la etiqueta B se mueve, combina o elimina, o cuando la etiqueta B está activada, en cuyo caso todas sus etiquetas de backlinks también deben activarse.

     >[!NOTE]
     >
     >La propiedad `cq:backlinks` solo se agrega a la etiqueta movida o combinada si se cumple cualquiera de estas condiciones:
     >
     > 1. La etiqueta se utiliza en el contenido (lo que significa que tiene una referencia), o
     > 1. La etiqueta tiene elementos secundarios que ya se han movido.

La lectura de una propiedad `cq:tags` de un nodo de contenido implica la siguiente resolución:

1. Si no hay ninguna coincidencia en `/content/cq:tags`, no se devuelve ninguna etiqueta.
1. Si la etiqueta tiene una propiedad `cq:movedTo` establecida, se sigue el identificador de etiqueta al que se hace referencia.
   * Este paso se repite siempre que la etiqueta seguida tenga la propiedad `cq:movedTo`.
1. Si la etiqueta seguida no tiene una propiedad `cq:movedTo`, se leerá la etiqueta.

Para publicar el cambio cuando se haya movido o combinado una etiqueta, se debe replicar el nodo `cq:Tag` y todos sus backlinks. Esta replicación se realiza automáticamente cuando la etiqueta se activa en la consola de administración de etiquetas.

Las actualizaciones posteriores de la propiedad `cq:tags` de la página limpian automáticamente las referencias antiguas. La limpieza se activa porque la resolución de una etiqueta desplazada a través de la API devuelve la etiqueta de destino, proporcionando así el ID de etiqueta de destino.
