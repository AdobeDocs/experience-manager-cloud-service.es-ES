---
title: Creación del etiquetado en aplicaciones de AEM
description: Trabajar mediante programación con etiquetas o ampliar etiquetas dentro de una aplicación de AEM personalizada
exl-id: a106dce1-5d51-406a-a563-4dea83987343
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 1%

---

# Creación del etiquetado en aplicaciones de AEM {#building-tagging-into-aem-applications}

Con el fin de trabajar mediante programación con etiquetas o ampliar etiquetas dentro de una aplicación de AEM personalizada, este documento describe el uso de la variable

* [API de etiquetado](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html)

que interactúa con el

* [Marco de etiquetado](tagging-framework.md)

Para obtener información relacionada con el etiquetado:

* Consulte [Uso de etiquetas](/help/sites-cloud/authoring/sites-console/tags.md) para obtener información sobre cómo etiquetar contenido como autor de contenido.
* Consulte Administración de etiquetas para conocer la perspectiva de un administrador sobre la creación y administración de etiquetas y sobre las etiquetas de contenido que se han aplicado.

## Información general sobre la API de etiquetado {#overview-of-the-tagging-api}

La implementación del [marco de etiquetado](tagging-framework.md) en AEM permite administrar las etiquetas y el contenido de las etiquetas mediante la API JCR. `TagManager` garantiza que las etiquetas introducidas como valores en la propiedad de matriz de cadenas `cq:tags` no se dupliquen, elimina `TagID`s que apuntan a etiquetas no existentes y actualiza `TagID`s para etiquetas movidas o combinadas. `TagManager` usa un detector de observación JCR que revierte cualquier cambio incorrecto. Las clases principales se encuentran en el paquete [com.day.cq.tagging](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html):

* `JcrTagManagerFactory` - devuelve una implementación basada en JCR de `TagManager`. Es la implementación de referencia de la API de etiquetado.
* `TagManager`: permite resolver y crear etiquetas por rutas y nombres.
* `Tag`: define el objeto de etiqueta.

### Obtener un TagManager basado en JCR {#getting-a-jcr-based-tagmanager}

Para recuperar una instancia de `TagManager`, necesita tener un JCR `Session` y llamar a `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

En el contexto típico de Sling, también puede adaptarse a `TagManager` desde `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Recuperación de un objeto Tag {#retrieving-a-tag-object}

Se puede recuperar un(a) `Tag` a través de `TagManager`, resolviendo una etiqueta existente o creando una:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

Para la implementación basada en JCR, que asigna `Tags` al JCR `Nodes`, puede utilizar directamente el mecanismo `adaptTo` de Sling si tiene el recurso (por ejemplo, `/content/cq:tags/default/my/tag`):

```java
Tag tag = resource.adaptTo(Tag.class);
```

Aunque una etiqueta solo se puede convertir *de* a un recurso (no a un nodo), una etiqueta se puede convertir *a* tanto a un nodo como a un recurso:

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>No es posible adaptarse directamente de `Node` a `Tag`, ya que `Node` no implementa el método Sling `Adaptable.adaptTo(Class)`.

### Obtención y configuración de etiquetas {#getting-and-setting-tags}

```java
// Getting the tags of a Resource:
Tag[] tags = tagManager.getTags(resource);

// Setting tags to a Resource:
tagManager.setTags(resource, tags);
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
>El `RangeIterator` válido que se va a usar es:
>
>`com.day.cq.commons.RangeIterator`

### Eliminación de etiquetas {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### Duplicación de etiquetas {#replicating-tags}

Es posible utilizar el servicio de replicación (`Replicator`) con etiquetas porque las etiquetas son del tipo `nt:hierarchyNode`:

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## El recolector de basura de etiquetas {#the-tag-garbage-collector}

El recolector de etiquetas es un servicio en segundo plano que limpia las etiquetas ocultas y no utilizadas. Las etiquetas ocultas y no utilizadas son etiquetas por debajo de `/content/cq:tags` que tienen una propiedad `cq:movedTo` y no se utilizan en un nodo de contenido. Tienen un recuento de cero. Al utilizar este proceso de eliminación diferida, no es necesario actualizar el nodo de contenido (es decir, la propiedad `cq:tags`) como parte de la operación de mover o combinar. Las referencias en la propiedad `cq:tags` se actualizan automáticamente cuando se actualiza la propiedad `cq:tags`, por ejemplo, a través del cuadro de diálogo de propiedades de página.

El recolector de elementos no utilizados se ejecuta de forma predeterminada una vez al día. Esto se puede configurar en:

`http://<host>:<port>/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector`

## Búsqueda de etiquetas y Listado de etiquetas {#tag-search-and-tag-listing}

La búsqueda de etiquetas y la lista de etiquetas funcionan de la siguiente manera:

* La búsqueda de `TagID` busca las etiquetas que tienen la propiedad `cq:movedTo` establecida en `TagID` y sigue a través de `cq:movedTo` `TagID`s.
* La búsqueda del título de etiqueta solo busca las etiquetas que no tienen una propiedad `cq:movedTo`.

## Etiquetas en diferentes idiomas {#tags-in-different-languages}

Una etiqueta `title` se puede definir en diferentes idiomas. A continuación, se agrega una propiedad sensible al idioma al nodo de etiquetas. Esta propiedad tiene el formato `jcr:title.<locale>`, por ejemplo, `jcr:title.fr` para la traducción al francés. `<locale>` debe ser una cadena de configuración regional ISO en minúsculas y usar guiones bajos (`_`) en lugar de guiones o guiones (`-`), por ejemplo: `de_ch`.

Por ejemplo, cuando se agrega la etiqueta **Animals** a la página **Productos**, el valor `stockphotography:animals` se agrega a la propiedad `cq:tags` del nodo `/content/wknd/en/products/jcr:content`. Se hace referencia a la traducción desde el nodo de etiqueta.

La API del lado del servidor ha localizado `title` métodos relacionados:

* [`com.day.cq.tagging.Tag`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/Tag.html)
   * `getLocalizedTitle(Locale locale)`
   * `getLocalizedTitlePaths()`
   * `getLocalizedTitles()`
   * `getTitle(Locale locale)`
   * `getTitlePath(Locale locale)`
* [`com.day.cq.tagging.TagManager`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/TagManager.html)
   * `canCreateTagByTitle(String tagTitlePath, Locale locale)`
   * `createTagByTitle(String tagTitlePath, Locale locale)`
   * `resolveByTitle(String tagTitlePath, Locale locale)`

En AEM, el idioma se puede obtener del idioma de la página o del idioma del usuario.

Para el etiquetado, la localización depende del contexto, ya que la etiqueta `titles` se puede mostrar en el idioma de la página, en el idioma del usuario o en cualquier otro idioma.

### Adición de un nuevo idioma al cuadro de diálogo Editar etiqueta {#adding-a-new-language-to-the-edit-tag-dialog}

El siguiente procedimiento describe cómo agregar un nuevo idioma (por ejemplo, finés) al cuadro de diálogo **Editar etiqueta**:

1. En **CRXDE**, edite la propiedad de varios valores `languages` del nodo `/content/cq:tags`.
1. Agregue `fi_fi`, que representa la configuración regional de Finlandia, y guarde los cambios.

El finés está ahora disponible en el cuadro de diálogo de etiquetas de las propiedades de página y en el cuadro de diálogo **Editar etiqueta** al editar una etiqueta en la consola **Etiquetado**.

>[!NOTE]
>
>El nuevo idioma debe ser uno de los idiomas reconocidos por AEM. Es decir, debe estar disponible como nodo debajo de `/libs/wcm/core/resources/languages`.
