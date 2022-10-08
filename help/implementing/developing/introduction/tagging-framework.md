---
title: Marco de trabajo de etiquetado de AEM
description: Etiquete contenido y aproveche la infraestructura de etiquetado de AEM para categorizarla y organizarla.
exl-id: 25418d44-aace-4e73-be1a-4b1902f40403
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '1570'
ht-degree: 0%

---

# El marco de etiquetado de AEM {#aem-tagging-framework}

El etiquetado permite categorizar y organizar el contenido. Las etiquetas se pueden clasificar mediante un área de nombres y una taxonomía. Para obtener información detallada sobre el uso de etiquetas:

* Consulte [Uso de etiquetas](/help/sites-cloud/authoring/features/tags.md) para obtener información sobre el etiquetado de contenido como autor de contenido.
* Consulte Administración de etiquetas para conocer la perspectiva de un administrador sobre la creación y administración de etiquetas, así como sobre las etiquetas de contenido que se han aplicado.

Este artículo se centra en el marco subyacente que admite el etiquetado en AEM y cómo aprovecharlo como desarrollador.

## Introducción {#introduction}

Para etiquetar contenido y aprovechar la infraestructura AEM Tagging :

* La etiqueta debe existir como nodo de tipo [`cq:Tag`](#cq-tag-node-type) en el [nodo raíz de taxonomía.](#taxonomy-root-node)
* El nodo de contenido etiquetado `NodeType` debe incluir el [`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin.
* La variable [`TagID`](#tagid) se agrega al nodo de contenido [`cq:tags`](#cq-tags-property) y se resuelve en un nodo de tipo [`cq:Tag`.](#cq-tag-node-type)

## cq:Tag Node Type {#cq-tag-node-type}

La declaración de una etiqueta se captura en el repositorio en un nodo de tipo `cq:Tag.`

* Una etiqueta puede ser una palabra simple (por ejemplo, `sky`) o representan una taxonomía jerárquica (por ejemplo, `fruit/apple`, es decir, tanto la fruta genérica como la manzana más específica).
* Las etiquetas se identifican mediante una `TagID`.
* Una etiqueta tiene información meta opcional, como un título, títulos localizados y una descripción. El título debe mostrarse en las interfaces de usuario en lugar del `TagID`, cuando esté presente.

El marco de etiquetado también permite restringir el uso de etiquetas predefinidas específicas por parte de los autores y visitantes del sitio.

### Características de las etiquetas {#tag-characteristics}

* El tipo de nodo es `cq:Tag`.
* El nombre del nodo es un componente de la variable [`TagID`.](#tagid)
* La variable [`TagID`](#tagid) siempre incluye un [espacio de nombres.](#tag-namespace)
* La variable `jcr:title` (el Título que se mostrará en la interfaz de usuario) es opcional.
* La variable `jcr:description` es opcional.
* Cuando contiene nodos secundarios, se denomina [contenedor .](#container-tags)
* La etiqueta se almacena en el repositorio debajo de una ruta base denominada [nodo raíz de taxonomía.](#taxonomy-root-node)

### ID de etiqueta {#tagid}

A `TagID` identifica una ruta que se resuelve en un nodo de etiqueta en el repositorio.

Normalmente, la variable `TagID` es una taquigrafía `TagID` comenzando por el espacio de nombres o puede ser un valor absoluto `TagID` a partir de [nodo raíz de taxonomía.](#taxonomy-root-node)

Cuando el contenido está etiquetado, si aún no existe, la variable [`cq:tags`](#cq-tags-property) se añade al nodo de contenido y a la variable `TagID` se agrega a la variable `String` valor de matriz.

La variable `TagID` consiste en un [namespace](#tag-namespace) seguido por el `TagID`. [Etiquetas de contenedor](#container-tags) tienen subetiquetas que representan un orden jerárquico en la taxonomía. Las subetiquetas se pueden usar para hacer referencia a las etiquetas del mismo modo que cualquier etiqueta local `TagID`. Por ejemplo, etiquetar contenido con `fruit` está permitido, incluso si es una etiqueta contenedora con subetiquetas, como `fruit/apple` y `fruit/banana`.

### Nodo raíz de taxonomía {#taxonomy-root-node}

El nodo raíz de taxonomía es la ruta base para todas las etiquetas del repositorio. El nodo raíz de taxonomía debe *not* ser un nodo de tipo `cq:Tag`.

En AEM, la ruta base es `/content/cq:tags` y el nodo raíz es del tipo `cq:Folder`.

### Área de nombres de la etiqueta {#tag-namespace}

Los espacios de nombres permiten agrupar las cosas. El caso de uso más típico es tener un área de nombres por sitio (por ejemplo, pública frente a interna) o por aplicación más grande (por ejemplo, Sitios o Recursos), pero las áreas de nombres se pueden usar para otras necesidades. Los espacios de nombres se utilizan en la interfaz de usuario para mostrar solo el subconjunto de etiquetas (es decir, etiquetas de un determinado espacio de nombres) que se aplica al contenido actual.

El espacio de nombres de la etiqueta es el primer nivel del subárbol de taxonomía, que es el nodo inmediatamente inferior al [nodo raíz de taxonomía.](#taxonomy-root-node) Un área de nombres es un nodo de tipo `cq:Tag` cuyo padre no es un `cq:Tag` tipo de nodo.

Todas las etiquetas tienen un espacio de nombres. Si no se especifica ningún espacio de nombres, la etiqueta se asigna al espacio de nombres predeterminado, que es `TagID` `default`, es decir, `/content/cq:tags/default`.  El valor predeterminado de Título es `Standard Tags`en tales casos.

### Etiquetas de contenedor {#container-tags}

Una etiqueta contenedora es un nodo de tipo `cq:Tag` que contenga cualquier número y tipo de nodos secundarios, lo que permite mejorar el modelo de etiquetas con metadatos personalizados.

Además, las etiquetas de contenedor (o superetiquetas) de una taxonomía sirven como subsuma de todas las subetiquetas: por ejemplo, contenido etiquetado con `fruit/apple` se considera que está etiquetado con `fruit` también, es decir, buscar contenido que solo esté etiquetado con `fruit` también encontrará el contenido etiquetado con `fruit/apple`.

### Resolución de TagID {#resolving-tagids}

Si el ID de etiqueta contiene dos puntos (`:`), los dos puntos separan el área de nombres de la etiqueta o subtaxonomía, que luego se separan con barras inclinadas normales (`/`). Si el ID de etiqueta no tiene dos puntos, se da a entender el espacio de nombres predeterminado.

La ubicación estándar y única de las etiquetas es inferior a `/content/cq:tags`.

Etiquetas que hacen referencia a rutas o rutas no existentes que no apuntan a una `cq:Tag` se consideran no válidos y se ignoran.

La siguiente tabla muestra algunos ejemplos `TagID`s, sus elementos y cómo `TagID` responde a una ruta absoluta en el repositorio:

| `TagID` | Espacio de nombres | ID local | Etiquetas de contenedores | Etiqueta de hoja | Ruta de etiqueta absoluta del repositorio |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`,`apple` | `braeburn` | `content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | (ninguno) | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | (ninguno) | (ninguno) | (ninguno) | `/content/cq:tags/dam` |
| `content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `content/cq:tags/category/car` |

### Localización del título de la etiqueta {#localization-of-tag-title}

Cuando la etiqueta incluye la cadena de título opcional `jcr:title`, es posible localizar el título para mostrar añadiendo la propiedad `jcr:title.<locale>`.

Para obtener más información, consulte:

* [Etiquetas en diferentes idiomas,](tagging-applications.md#tags-in-different-languages) que describe el uso de las API como desarrollador
* Administración de etiquetas en diferentes idiomas, que describe el uso de la consola Etiquetado como administrador

### Control de acceso {#access-control}

Las etiquetas existen como nodos en el repositorio en el [nodo raíz de taxonomía.](#taxonomy-root-node) Permitir o denegar a autores y visitantes del sitio la creación de etiquetas en un espacio de nombres determinado se puede lograr estableciendo las ACL adecuadas en el repositorio.

La denegación de permisos de lectura para determinadas etiquetas o áreas de nombres controla la capacidad de aplicar etiquetas a contenido específico.

Una práctica habitual incluye:

* Permitiendo el `tag-administrators` acceso de escritura de grupo/función a todas las áreas de nombres (añadir/modificar en `/content/cq:tags`). Este grupo viene con AEM listo para usar.
* Permitir que los usuarios/autores lean acceso a todas las áreas de nombres que deberían ser legibles para ellos (en su mayoría, todas).
* Permitir que los usuarios/autores escriban acceso a las áreas de nombres en las que los usuarios/autores deben definir las etiquetas libremente (`add_node` under `/content/cq:tags/some_namespace`)

## Contenido etiquetable : cq:Mezcla etiquetable {#taggable-content-cq-taggable-mixin}

Para que los desarrolladores de aplicaciones puedan adjuntar etiquetas a un tipo de contenido, el registro del nodo ([CND](https://jackrabbit.apache.org/node-type-notation.html)) debe incluir el `cq:Taggable` mezcla o `cq:OwnerTaggable` mixin.

La variable `cq:OwnerTaggable` mixin, que hereda de `cq:Taggable`, está pensado para indicar que el contenido puede ser clasificado por el propietario/autor. En AEM, solo es un atributo de la variable `cq:PageContent` nodo . La variable `cq:OwnerTaggable` la mezcla no es necesaria para el marco de etiquetado.

>[!NOTE]
>
>Se recomienda habilitar únicamente las etiquetas en el nodo de nivel superior de un elemento de contenido agregado (o en su `jcr:content` nodo ). Algunos ejemplos son:
>
>* Páginas (`cq:Page`) donde la variable `jcr:content`el nodo es de tipo `cq:PageContent`, que incluye el `cq:Taggable` mixin.
>* Recursos (`cq:Asset`) donde la variable `jcr:content/metadata` el nodo siempre tiene la variable `cq:Taggable` mixin.


### Anotación de tipo de nodo (CND) {#node-type-notation-cnd}

Las definiciones de Tipo de nodo existen en el repositorio como archivos CND. La notación CND se define como parte del [Documentación de JCR.](https://jackrabbit.apache.org/node-type-notation.html).

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

## cq:tags (propiedad) {#cq-tags-property}

La variable `cq:tags` la propiedad es `String` matriz utilizada para almacenar una o más `TagID`s cuando los autores o los visitantes del sitio los aplican al contenido. La propiedad solo tiene significado cuando se agrega a un nodo que se define con la variable [`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin.

>[!NOTE]
>
>Para aprovechar AEM funcionalidad de etiquetado, las aplicaciones desarrolladas a medida no deben definir propiedades de etiqueta que no sean `cq:tags`.

## Mover y combinar etiquetas {#moving-and-merging-tags}

A continuación, se describen los efectos en el repositorio al mover o combinar etiquetas mediante la consola Etiquetado.

Cuando la etiqueta A se mueve o combina en la etiqueta B debajo de `/content/cq:tags`:

* La etiqueta A no se elimina y recibe una `cq:movedTo` propiedad.
   * `cq:movedTo` apunta a la etiqueta B.
   * Esta propiedad significa que la etiqueta A se ha movido o combinado en la etiqueta B.
   * Al mover la etiqueta B se actualizará esta propiedad según corresponda.
   * Por lo tanto, la etiqueta A está oculta y solo se mantiene en el repositorio para resolver los ID de etiqueta en los nodos de contenido que apuntan a la etiqueta A.
   * El recolector de residuos de etiquetas elimina etiquetas como la etiqueta A una vez que más nodos de contenido no señalan a ellas.
   * Un valor especial para la variable `cq:movedTo` la propiedad es `nirvana`, que se aplica cuando se elimina la etiqueta, pero no se puede eliminar del repositorio porque hay subetiquetas con un `cq:movedTo` eso debe mantenerse.

      >[!NOTE]
      >
      >La variable `cq:movedTo` solo se agrega a la etiqueta movida o combinada si se cumple cualquiera de estas condiciones:
      >
      > 1. La etiqueta se utiliza en el contenido (lo que significa que tiene una referencia). O
      > 1. La etiqueta tiene elementos secundarios que ya se han movido.

* La etiqueta B se crea (en caso de un movimiento) y recibe una `cq:backlinks` propiedad.
   * `cq:backlinks` mantiene las referencias en la otra dirección, es decir, mantiene una lista de todas las etiquetas que se han movido a la etiqueta B o que se han combinado con ella.
   * Esto es necesario principalmente para mantener `cq:movedTo` propiedades actualizadas cuando la etiqueta B también se mueve, combina o elimina, o cuando la etiqueta B está activada, en cuyo caso todas sus etiquetas backlinks también deben activarse.

      >[!NOTE]
      >
      >La variable `cq:backlinks` solo se agrega a la etiqueta movida o combinada si se cumple cualquiera de estas condiciones:
      >
      > 1. La etiqueta se utiliza en el contenido (lo que significa que tiene una referencia). O
      > 1. La etiqueta tiene elementos secundarios que ya se han movido.


Leer un `cq:tags` la propiedad de un nodo de contenido implica la siguiente resolución:

1. Si no hay coincidencia en `/content/cq:tags`, no devuelve ninguna etiqueta.
1. Si la etiqueta tiene un `cq:movedTo` conjunto de propiedades, se sigue el ID de etiqueta al que se hace referencia.
   * Este paso se repite siempre y cuando la etiqueta siguiente tenga una `cq:movedTo` propiedad.
1. Si la etiqueta siguiente no tiene un valor `cq:movedTo` , se lee la etiqueta .

Para publicar el cambio cuando una etiqueta se ha movido o combinado, la variable `cq:Tag` y todos sus vínculos secundarios deben replicarse. Esto se realiza automáticamente cuando la etiqueta está activada en la consola de administración de etiquetas.

Actualizaciones posteriores en el informe `cq:tags` limpie automáticamente las referencias antiguas. Esto se activa porque la resolución de una etiqueta movida a través de la API devuelve la etiqueta de destino, proporcionando así el ID de etiqueta de destino.
