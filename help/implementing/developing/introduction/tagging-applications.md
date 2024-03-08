---
title: Creación del etiquetado en aplicaciones de AEM
description: AEM Trabajar mediante programación con etiquetas o ampliar etiquetas dentro de una aplicación de personalizada
exl-id: a106dce1-5d51-406a-a563-4dea83987343
source-git-commit: 53a66eac5ca49183221a1d61b825401d4645859e
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 1%

---

# Creación del etiquetado en aplicaciones de AEM {#building-tagging-into-aem-applications}

AEM Con el fin de trabajar mediante programación con etiquetas o ampliar etiquetas dentro de una aplicación de personalizada, este documento describe el uso de

* [API de etiquetado](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html)

que interactúa con el

* [Marco de etiquetado](tagging-framework.md)

Para obtener información relacionada con el etiquetado:

* Consulte [Uso de etiquetas](/help/sites-cloud/authoring/sites-console/tags.md) para obtener información sobre cómo etiquetar contenido como autor de contenido.
* Consulte Administración de etiquetas para conocer la perspectiva de un administrador sobre la creación y administración de etiquetas y sobre las etiquetas de contenido que se han aplicado.

## Información general sobre la API de etiquetado {#overview-of-the-tagging-api}

La implementación de la [marco de etiquetado](tagging-framework.md) AEM en permite la administración de etiquetas y contenido de etiquetas mediante la API de JCR. `TagManager` garantiza que las etiquetas introducidas como valores en la `cq:tags` la propiedad de matriz de cadenas no está duplicada, elimina `TagID`s que apuntan a etiquetas y actualizaciones no existentes `TagID`es para etiquetas movidas o combinadas. `TagManager` utiliza un oyente de observación JCR que revierte cualquier cambio incorrecto. Las clases principales se encuentran en la [com.day.cq.tagging](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html) paquete:

* `JcrTagManagerFactory` - devuelve una implementación basada en JCR de un `TagManager`. Es la implementación de referencia de la API de etiquetado.
* `TagManager` : permite resolver y crear etiquetas por rutas y nombres.
* `Tag` : define el objeto de etiqueta.

### Obtener un TagManager basado en JCR {#getting-a-jcr-based-tagmanager}

Para recuperar un `TagManager` Por ejemplo, necesita tener un JCR `Session` y para llamar a `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

En el contexto típico de Sling, también puede adaptarse a un `TagManager` desde el `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Recuperación de un objeto Tag {#retrieving-a-tag-object}

A `Tag` se puede recuperar mediante la variable `TagManager`, ya sea resolviendo una etiqueta existente o creando una:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

Para la implementación basada en JCR, que asigna `Tags` en JCR `Nodes`, puede utilizar directamente el de Sling `adaptTo` mecanismo si tiene el recurso (por ejemplo, como `/content/cq:tags/default/my/tag`):

```java
Tag tag = resource.adaptTo(Tag.class);
```

Mientras que una etiqueta solo se puede convertir *de* Como recurso (no nodo), se puede convertir una etiqueta *hasta* un nodo y un recurso:

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>Adaptación directa desde `Node` hasta `Tag` no es posible, ya que `Node` no implementa el Sling `Adaptable.adaptTo(Class)` método.

### Obtención y configuración de etiquetas {#getting-and-setting-tags}

```java
// Getting the tags of a Resource:
Tag[] tags = tagManager.getTags (resource);

// Setting tags to a Resource:
tagManager.setTags (resource, tags);
```

### Búsqueda de etiquetas {#searching-for-tags}

```java
// Searching for the Resource objects that are tagged with the tag object:
Iterator<Resource> it = tag.find();

// Retrieving the usage count of the tag object:
long count = tag.getCount();

// Searching for the Resource objects that are tagged with the tagID String:
 RangeIterator<Resource> it = tagManager.find(tagID);
```

>[!NOTE]
>
>El válido `RangeIterator` para usar es:
>
>`com.day.cq.commons.RangeIterator`

### Eliminación de etiquetas {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### Duplicación de etiquetas {#replicating-tags}

Es posible utilizar el servicio de replicación (`Replicator`) con etiquetas porque son del tipo `nt:hierarchyNode`:

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## El recolector de basura de etiquetas {#the-tag-garbage-collector}

El recolector de etiquetas es un servicio en segundo plano que limpia las etiquetas ocultas y no utilizadas. Las etiquetas ocultas y no utilizadas son las siguientes `/content/cq:tags` que tienen un `cq:movedTo` y no se utilizan en un nodo de contenido. Tienen un recuento de cero. Al utilizar este proceso de eliminación diferida, el nodo de contenido (es decir, el `cq:tags` ) no tiene que actualizarse como parte de la operación de movimiento o combinación. Las referencias en la variable `cq:tags` Las propiedades de se actualizan automáticamente cuando `cq:tags` La propiedad de se actualiza, por ejemplo, a través del cuadro de diálogo Propiedades de página.

El recolector de elementos no utilizados se ejecuta de forma predeterminada una vez al día. Esto se puede configurar en:

`http://<host>:<port>/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector`

## Búsqueda de etiquetas y Listado de etiquetas {#tag-search-and-tag-listing}

La búsqueda de etiquetas y la lista de etiquetas funcionan de la siguiente manera:

* La búsqueda de `TagID` busca las etiquetas que tienen la propiedad `cq:movedTo` establezca en `TagID` y sigue el `cq:movedTo` `TagID`s.
* La búsqueda de título de etiqueta solo busca las etiquetas que no tienen un `cq:movedTo` propiedad.

## Etiquetas en diferentes idiomas {#tags-in-different-languages}

Una etiqueta `title` puede definirse en diferentes idiomas. A continuación, se agrega una propiedad sensible al idioma al nodo de etiquetas. Esta propiedad tiene el formato `jcr:title.<locale>`, por ejemplo, `jcr:title.fr` para la traducción al francés. `<locale>` debe ser una cadena de configuración regional ISO en minúsculas y utilizar guiones bajos (`_`) en lugar de guion/guión (`-`), por ejemplo: `de_ch`.

Por ejemplo, cuando la variable **Animales** se agrega a la etiqueta **Productos** página, el valor `stockphotography:animals` se añade a la propiedad `cq:tags` del nodo `/content/wknd/en/products/jcr:content`. Se hace referencia a la traducción desde el nodo de etiqueta.

La API del lado del servidor se ha localizado `title`Métodos relacionados con:

* [`com.day.cq.tagging.Tag`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/Tag.html)
   * `getLocalizedTitle(Locale locale)`
   * `getLocalizedTitlePaths ()`
   * `getLocalizedTitles ()`
   * `getTitle(Locale locale)`
   * `getTitlePath(Locale locale)`
* [`com.day.cq.tagging.TagManager`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/TagManager.html)
   * `canCreateTagByTitle(String tagTitlePath, Locale locale)`
   * `createTagByTitle(String tagTitlePath, Locale locale)`
   * `resolveByTitle(String tagTitlePath, Locale locale)`

AEM En la práctica, el idioma se puede obtener en el idioma de la página o en el idioma del usuario.

Para el etiquetado, la localización depende del contexto como etiqueta `titles` puede mostrarse en el idioma de la página, en el idioma del usuario o en cualquier otro idioma.

### Adición de un nuevo idioma al cuadro de diálogo Editar etiqueta {#adding-a-new-language-to-the-edit-tag-dialog}

En el siguiente procedimiento se describe cómo agregar un nuevo idioma (por ejemplo, finés) al **Edición de etiquetas** diálogo:

1. Entrada **CRXDE**, edite la propiedad de varios valores `languages` del nodo `/content/cq:tags`.
1. Añadir `fi_fi`, que representa la configuración regional finlandesa, y guarde los cambios.

El finés está ahora disponible en el cuadro de diálogo de etiquetas de las propiedades de página y en la **Editar etiqueta** diálogo al editar una etiqueta en la **Etiquetado** consola.

>[!NOTE]
>
>AEM El nuevo idioma debe ser uno de los idiomas reconocidos por la comunidad de idiomas de los que se dispone en la. Es decir, debe estar disponible como nodo debajo de `/libs/wcm/core/resources/languages`.
