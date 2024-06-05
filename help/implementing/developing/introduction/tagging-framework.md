---
title: Marco de trabajo de etiquetado de AEM
description: AEM Etiquete el contenido y utilice la infraestructura de etiquetado de la para categorizarlo y organizarlo.
exl-id: 25418d44-aace-4e73-be1a-4b1902f40403
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1562'
ht-degree: 0%

---

# AEM El marco de etiquetado de {#aem-tagging-framework}

El etiquetado permite clasificar y organizar el contenido. Las etiquetas se pueden clasificar por un área de nombres y una taxonomía. Para obtener información detallada sobre el uso de etiquetas:

* Consulte [Uso de etiquetas](/help/sites-cloud/authoring/sites-console/tags.md) para obtener información sobre cómo etiquetar contenido como autor de contenido.
* Consulte Administración de etiquetas para conocer la perspectiva de un administrador sobre la creación y administración de etiquetas y sobre las etiquetas de contenido que se han aplicado.

AEM Este artículo se centra en el marco de trabajo subyacente que admite el etiquetado en los entornos de y en cómo utilizarlo como desarrollador.

## Introducción {#introduction}

AEM Para etiquetar contenido y utilizar la infraestructura de etiquetado de:

* La etiqueta debe existir como nodo de tipo [`cq:Tag`](#cq-tag-node-type) en el [nodo raíz de taxonomía.](#taxonomy-root-node)
* El nodo de contenido etiquetado es `NodeType` debe incluir el [`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin.
* El [`TagID`](#tagid) se añade al nodo de contenido [`cq:tags`](#cq-tags-property) y se resuelve en un nodo de tipo [`cq:Tag`.](#cq-tag-node-type)

## cq:Tipo de nodo de etiqueta {#cq-tag-node-type}

La declaración de una etiqueta se captura en el repositorio en un nodo de tipo `cq:Tag.`

* Una etiqueta puede ser una palabra simple (por ejemplo, `sky`) o representan una taxonomía jerárquica (por ejemplo, `fruit/apple`, es decir, tanto la fruta genérica como la manzana más específica).
* Las etiquetas se identifican mediante una variable única `TagID`.
* Una etiqueta tiene información meta opcional, como un título, títulos localizados y una descripción. El título debe mostrarse en las interfaces de usuario en lugar de en el `TagID`, cuando esté presente.

El marco de etiquetado también restringe a los autores y visitantes del sitio a utilizar únicamente etiquetas específicas predefinidas.

### Características de etiquetas {#tag-characteristics}

* El tipo de nodo es `cq:Tag`.
* El nombre del nodo es un componente del [`TagID`.](#tagid)
* El [`TagID`](#tagid) siempre incluye un [namespace.](#tag-namespace)
* El `jcr:title` (el Título que se mostrará en la interfaz de usuario) es opcional.
* El `jcr:description` La propiedad es opcional.
* Cuando contiene nodos secundarios, se denomina [etiqueta contenedora.](#container-tags)
* La etiqueta se almacena en el repositorio bajo una ruta base denominada [nodo raíz de taxonomía.](#taxonomy-root-node)

### ID de etiqueta {#tagid}

A `TagID` identifica una ruta que se resuelve en un nodo de etiqueta del repositorio.

Normalmente, la variable `TagID` es una abreviatura `TagID` empezando por el área de nombres o puede ser un valor absoluto `TagID` a partir de [nodo raíz de taxonomía.](#taxonomy-root-node)

Cuando se etiqueta contenido, si aún no existe, la variable [`cq:tags`](#cq-tags-property) se agrega al nodo de contenido y la propiedad `TagID` se añade a la propiedad de `String` valor de matriz.

El `TagID` consiste en un [namespace](#tag-namespace) seguido del local `TagID`. [Etiquetas de contenedor](#container-tags) tienen subetiquetas que representan un orden jerárquico en la taxonomía. Las subetiquetas se pueden utilizar para hacer referencia a las etiquetas como cualquier etiqueta local `TagID`. Por ejemplo, al etiquetar contenido con `fruit` se permite, incluso si es una etiqueta contenedora con subetiquetas, como `fruit/apple` y `fruit/banana`.

### Nodo raíz de taxonomía {#taxonomy-root-node}

El nodo raíz de taxonomía es la ruta base para todas las etiquetas del repositorio. El nodo raíz de taxonomía debe *no* ser un nodo de tipo `cq:Tag`.

AEM En el caso de los usuarios, la ruta base es `/content/cq:tags` y el nodo raíz es del tipo `cq:Folder`.

### Área de nombres de etiqueta {#tag-namespace}

Las áreas de nombres permiten agrupar cosas. El caso de uso más típico es tener un área de nombres por sitio (por ejemplo, público frente a interno) o por aplicación más grande (por ejemplo, Sites o Assets), pero las áreas de nombres se pueden utilizar para otras necesidades. Los espacios de nombres se utilizan en la interfaz de usuario para mostrar únicamente el subconjunto de etiquetas (es decir, las etiquetas de un determinado espacio de nombres) que se aplica al contenido actual.

El área de nombres de la etiqueta es el primer nivel del subárbol de taxonomía, que es el nodo situado inmediatamente debajo de [nodo raíz de taxonomía.](#taxonomy-root-node) Un área de nombres es un nodo de tipo `cq:Tag` cuyo elemento principal no es un `cq:Tag` tipo de nodo.

Todas las etiquetas tienen un área de nombres. Si no se especifica ningún área de nombres, la etiqueta se asigna al área de nombres predeterminada, que es `TagID` `default`, es decir, `/content/cq:tags/default`. El título predeterminado es `Standard Tags`en tales casos.

### Etiquetas de contenedor {#container-tags}

Una etiqueta contenedora es un nodo de tipo `cq:Tag` que contenga cualquier número y tipo de nodos secundarios, lo que permite mejorar el modelo de etiquetas con metadatos personalizados.

Además, las etiquetas de contenedor (o superetiquetas) en una taxonomía sirven como subsuma de todas las subetiquetas. Por ejemplo, contenido etiquetado con `fruit/apple` se considera etiquetado con `fruit`, también. Es decir, buscar contenido etiquetado con `fruit` también encontraría el contenido etiquetado con `fruit/apple`.

### Resolver TagID {#resolving-tagids}

Si el ID de etiqueta contiene dos puntos (`:`), los dos puntos separan el área de nombres de la etiqueta o subtaxonomía, que luego se separan con barras diagonales normales (`/`). Si el ID de etiqueta no tiene dos puntos, el área de nombres predeterminada es implícita.

A continuación, se muestra la ubicación estándar y exclusiva de las etiquetas `/content/cq:tags`.

Etiquetas que hacen referencia a rutas no existentes o que no apuntan a una ruta `cq:Tag` Los nodos de se consideran no válidos y se ignoran.

La siguiente tabla muestra algunos ejemplos `TagID`s, sus elementos y cómo `TagID` se resuelve en una ruta absoluta en el repositorio:

| `TagID` | Espacio de nombres | ID local | Etiquetas de contenedor | Etiqueta de hoja | Ruta de etiqueta absoluta del repositorio |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`,`apple` | `braeburn` | `content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | (ninguno) | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | (ninguno) | (ninguno) | (ninguno) | `/content/cq:tags/dam` |
| `content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `content/cq:tags/category/car` |

### Localización del título de la etiqueta {#localization-of-tag-title}

Cuando la etiqueta incluye la cadena de título opcional `jcr:title`, es posible localizar el título para mostrarlo añadiendo la propiedad `jcr:title.<locale>`.

Para obtener más información, consulte lo siguiente:

* [Etiquetas en diferentes idiomas](tagging-applications.md#tags-in-different-languages) describa el uso de las API como desarrollador
* Administración de etiquetas en diferentes idiomas, que describen el uso de la consola de etiquetado como administrador

### Control de acceso {#access-control}

Las etiquetas existen como nodos en el repositorio en la variable [nodo raíz de taxonomía.](#taxonomy-root-node) Permitir o denegar a los autores y visitantes del sitio la creación de etiquetas en un área de nombres determinada se puede lograr estableciendo ACL adecuados en el repositorio.

La denegación de permisos de lectura para determinadas etiquetas o áreas de nombres controla la capacidad de aplicar etiquetas a contenido específico.

Una práctica típica incluye:

* Permitir el `tag-administrators` acceso de escritura de grupo/función a todas las áreas de nombres (agregar/modificar en `/content/cq:tags`). AEM Este grupo incluye a los usuarios que ya están preparados para su uso en el momento de la compra.
* Permite a los usuarios/autores acceder a todas las áreas de nombres que deben poder leerlas (principalmente todas).
* Permitir a usuarios/autores escribir acceso a aquellas áreas de nombres en las que los usuarios/autores deben poder definir libremente las etiquetas (`add_node` bajo `/content/cq:tags/some_namespace`)

## Contenido etiquetable : cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

Para que los desarrolladores de aplicaciones adjunten el etiquetado a un tipo de contenido, el registro del nodo ([CND](https://jackrabbit.apache.org/jcr/node-type-notation.html)) debe incluir el `cq:Taggable` mixin o el `cq:OwnerTaggable` mixin.

El `cq:OwnerTaggable` mixin, que hereda de `cq:Taggable`, tiene la intención de indicar que el propietario/autor puede clasificar el contenido. AEM En el caso de los informes, solo es un atributo de la variable `cq:PageContent` nodo. El `cq:OwnerTaggable` El marco de etiquetado no requiere el mixin.

>[!NOTE]
>
>Se recomienda habilitar solo las etiquetas en el nodo de nivel superior de un elemento de contenido agregado (o en su `jcr:content` node). Algunos ejemplos son:
>
>* Páginas (`cq:Page`) donde la variable `jcr:content`el nodo es del tipo `cq:PageContent`, que incluye el `cq:Taggable` mixin.
>* Recursos (`cq:Asset`) donde la variable `jcr:content/metadata` El nodo siempre tiene el `cq:Taggable` mixin.

### Notación de tipo de nodo (CND) {#node-type-notation-cnd}

Las definiciones del tipo de nodo existen en el repositorio como archivos CDN. La notación CDN se define como parte de la variable [Documentación de JCR](https://jackrabbit.apache.org/jcr/node-type-notation.html).

AEM Las definiciones esenciales para los tipos de nodo incluidos en la lista de nombres de dominio son las siguientes:

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

## propiedad cq:tags {#cq-tags-property}

El `cq:tags` La propiedad es un `String` matriz utilizada para almacenar uno o más `TagID`Es cuando los autores o visitantes del sitio los aplican al contenido. La propiedad solo tiene significado cuando se agrega a un nodo que se define con la variable [`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin.

>[!NOTE]
>
>AEM Para utilizar la funcionalidad de etiquetado de etiquetas, las aplicaciones desarrolladas personalizadas no deben definir propiedades de etiquetas distintas de `cq:tags`.

## Mover y combinar etiquetas {#moving-and-merging-tags}

A continuación se describen los efectos que se producen en el repositorio al mover o combinar etiquetas mediante la consola Etiquetado.

Cuando la etiqueta A se mueva o combine en la etiqueta B en `/content/cq:tags`:

* La etiqueta A no se elimina y recibe un `cq:movedTo` propiedad.
   * `cq:movedTo` apunta a la etiqueta B.
   * Esta propiedad significa que la etiqueta A se ha movido o combinado en la etiqueta B.
   * Al mover la etiqueta B, se actualiza esta propiedad en consecuencia.
   * Por lo tanto, la etiqueta A está oculta y solo se mantiene en el repositorio para que pueda resolver los ID de etiqueta en los nodos de contenido que apuntan a la etiqueta A.
   * El recolector de elementos no utilizados de etiquetas elimina las etiquetas como la etiqueta A una vez que los nodos de contenido no las señalan.
   * Un valor especial para `cq:movedTo` la propiedad es `nirvana`, que se aplica cuando se elimina la etiqueta, pero no se puede eliminar del repositorio porque hay subetiquetas con un `cq:movedTo` eso debe mantenerse.

     >[!NOTE]
     >
     >El `cq:movedTo` La propiedad solo se añade a la etiqueta movida o combinada si se cumple cualquiera de estas condiciones:
     >
     > 1. La etiqueta se utiliza en el contenido (lo que significa que tiene una referencia). OR
     > 1. La etiqueta tiene elementos secundarios que ya se han movido.
     >
* La etiqueta B se crea (si hay un movimiento) y recibe un `cq:backlinks` propiedad.
   * `cq:backlinks` mantiene las referencias en la otra dirección. Es decir, mantiene una lista de todas las etiquetas que se han movido o combinado con la etiqueta B.
   * Esta funcionalidad es necesaria principalmente para mantener `cq:movedTo` propiedades actualizadas cuando la etiqueta B se mueve, combina o elimina, o cuando la etiqueta B está activada, en cuyo caso todas sus etiquetas de backlinks deben activarse también.

     >[!NOTE]
     >
     >El `cq:backlinks` La propiedad solo se añade a la etiqueta movida o combinada si se cumple cualquiera de estas condiciones:
     >
     > 1. La etiqueta se utiliza en el contenido (lo que significa que tiene una referencia), o
     > 1. La etiqueta tiene elementos secundarios que ya se han movido.

Leer un `cq:tags` La propiedad de un nodo de contenido implica la siguiente resolución:

1. Si no hay ninguna coincidencia en `/content/cq:tags`, no se devuelve ninguna etiqueta.
1. Si la etiqueta tiene un `cq:movedTo` establecida, se sigue el ID de etiqueta al que se hace referencia.
   * Este paso se repite siempre que la etiqueta seguida tenga un `cq:movedTo` propiedad.
1. Si la etiqueta seguida no tiene un `cq:movedTo` propiedad, se lee la etiqueta.

Para publicar el cambio cuando se haya movido o combinado una etiqueta, la variable `cq:Tag` nodo y todos sus backlinks deben ser replicados. Esta replicación se realiza automáticamente cuando la etiqueta se activa en la consola de administración de etiquetas.

Actualizaciones posteriores en la página `cq:tags` limpie automáticamente las referencias antiguas. La limpieza se activa porque la resolución de una etiqueta desplazada a través de la API devuelve la etiqueta de destino, proporcionando así el ID de etiqueta de destino.
