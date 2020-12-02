---
title: Creación de etiquetas en aplicaciones AEM
description: Trabajar mediante programación con etiquetas o ampliar etiquetas dentro de una aplicación AEM personalizada
translation-type: tm+mt
source-git-commit: ce55065c3ae6a2350ed06811af76477df7c11291
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---


# Generación de etiquetado en aplicaciones AEM {#building-tagging-into-aem-applications}

Para trabajar mediante programación con etiquetas o ampliar etiquetas dentro de una aplicación de AEM personalizada, este documento describe el uso de la variable

* [API de etiquetado](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html)

que interactúa con el

* [Marco de etiquetado](tagging-framework.md)

Para obtener información relacionada con el etiquetado:

* Consulte [Uso de etiquetas](/help/sites-cloud/authoring/features/tags.md) para obtener información sobre el etiquetado de contenido como autor de contenido.
* Consulte Administración de etiquetas para conocer la perspectiva de un administrador sobre la creación y la administración de etiquetas, así como sobre las etiquetas de contenido que se han aplicado.

## Información general sobre la API de etiquetado {#overview-of-the-tagging-api}

La implementación del [marco de etiquetado](tagging-framework.md) en AEM permite la administración de etiquetas y contenido de etiquetas mediante la API de JCR. `TagManager` garantiza que las etiquetas introducidas como valores en la propiedad de matriz de  `cq:tags` cadenas no se dupliquen, elimina las etiquetas  `TagID`que apuntan a etiquetas no existentes y actualiza las etiquetas  `TagID`que se han movido o combinado. `TagManager` utiliza un detector de observación JCR que revierte los cambios incorrectos. Las clases principales están en el paquete [com.day.cq.tagging](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/package-summary.html):

* `JcrTagManagerFactory` - devuelve una implementación basada en JCR de un  `TagManager`. Es la implementación de referencia de la API de etiquetado.
* `TagManager` - permite resolver y crear etiquetas por rutas y nombres.
* `Tag` - define el objeto tag.

### Obtención de un TagManager basado en JCR {#getting-a-jcr-based-tagmanager}

Para recuperar una instancia `TagManager`, necesita tener un JCR `Session` y llamar a `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

En el contexto Sling típico también puede adaptarse a un `TagManager` desde el `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Recuperación de un objeto Tag {#retrieving-a-tag-object}

Se puede recuperar un `Tag` mediante el `TagManager`, resolviendo una etiqueta existente o creando una nueva:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

Para la implementación basada en JCR, que asigna `Tags` a JCR `Nodes`, puede utilizar directamente el mecanismo `adaptTo` de Sling si tiene el recurso (por ejemplo, `/content/cq:tags/default/my/tag`):

```java
Tag tag = resource.adaptTo(Tag.class);
```

Mientras que una etiqueta solo puede convertirse *desde* un recurso (no un nodo), una etiqueta puede convertirse *a* tanto en un nodo como en un recurso:

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>No es posible la adaptación directa de `Node` a `Tag`, ya que `Node` no implementa el método Sling `Adaptable.adaptTo(Class)`.

### Obtención y configuración de etiquetas {#getting-and-setting-tags}

```java
// Getting the tags of a Resource:
Tag[] tags = tagManager.getTags(resource);

// Setting tags to a Resource:
tagManager.setTags(resource, tags);
```

### Búsqueda de tags {#searching-for-tags}

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
>El `RangeIterator` válido para usar es:
>
>`com.day.cq.commons.RangeIterator`

### Eliminación de tags {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### Replicando etiquetas {#replicating-tags}

Es posible utilizar el servicio de replicación (`Replicator`) con etiquetas porque las etiquetas son de tipo `nt:hierarchyNode`:

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## El recolector de elementos no utilizados de etiquetas {#the-tag-garbage-collector}

El recolector de elementos no utilizados de etiquetas es un servicio de fondo que limpia las etiquetas que están ocultas y no se usan. Las etiquetas ocultas y no utilizadas son etiquetas inferiores a `/content/cq:tags` que tienen una propiedad `cq:movedTo` y no se utilizan en un nodo de contenido. Tienen un recuento de cero. Al utilizar este proceso de eliminación diferido, el nodo de contenido (es decir, la propiedad `cq:tags`) no tiene que actualizarse como parte de la operación de mover o combinar. Las referencias de la propiedad `cq:tags` se actualizan automáticamente cuando se actualiza la propiedad `cq:tags`, por ejemplo, a través del cuadro de diálogo de propiedades de página.

El recolector de elementos no utilizados de etiquetas se ejecuta de forma predeterminada una vez al día. Puede configurarse en:

`http://<host>:<port>/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector`

## Búsqueda de etiquetas y listado de etiquetas {#tag-search-and-tag-listing}

La búsqueda de etiquetas y la lista de etiquetas funcionan de la siguiente manera:

* La búsqueda de `TagID` busca las etiquetas que tienen la propiedad `cq:movedTo` establecida en `TagID` y sigue a través de `cq:movedTo` `TagID`s.
* La búsqueda del título de la etiqueta solo busca las etiquetas que no tienen una propiedad `cq:movedTo`.

## Etiquetas en diferentes idiomas {#tags-in-different-languages}

Se puede definir una etiqueta `title` en distintos idiomas. A continuación, se agrega una propiedad que distingue entre lenguajes al nodo de etiquetas. Esta propiedad tiene el formato `jcr:title.<locale>`, por ejemplo: `jcr:title.fr` para la traducción al francés. `<locale>` debe ser una cadena de configuración regional ISO en minúscula y utilizar el guion bajo (`_`) en lugar del guion/guion (`-`), por ejemplo:  `de_ch`.

Por ejemplo, cuando se agrega la etiqueta **Animals** a la página **Products**, el valor `stockphotography:animals` se agrega a la propiedad `cq:tags` del nodo `/content/wknd/en/products/jcr:content`. Se hace referencia a la traducción desde el nodo de etiqueta.

La API del lado del servidor ha localizado los métodos relacionados con `title`:

* [`com.day.cq.tagging.Tag`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/Tag.html)
   * `getLocalizedTitle(Locale locale)`
   * `getLocalizedTitlePaths()`
   * `getLocalizedTitles()`
   * `getTitle(Locale locale)`
   * `getTitlePath(Locale locale)`
* [`com.day.cq.tagging.TagManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/TagManager.html)
   * `canCreateTagByTitle(String tagTitlePath, Locale locale)`
   * `createTagByTitle(String tagTitlePath, Locale locale)`
   * `resolveByTitle(String tagTitlePath, Locale locale)`

En AEM, el idioma se puede obtener desde el idioma de la página o desde el idioma del usuario.

Para el etiquetado, la localización depende del contexto, ya que la etiqueta `titles` se puede mostrar en el idioma de la página, en el idioma del usuario o en cualquier otro idioma.

### Añadir un nuevo idioma en el cuadro de diálogo Editar etiqueta {#adding-a-new-language-to-the-edit-tag-dialog}

El siguiente procedimiento describe cómo agregar un nuevo idioma (por ejemplo, finés) al cuadro de diálogo **Editar etiqueta**:

1. En **CRXDE**, edite la propiedad de varios valores `languages` del nodo `/content/cq:tags`.
1. Añada `fi_fi`, que representa la configuración regional finlandesa, y guarde los cambios.

El finés ahora está disponible en el cuadro de diálogo de etiquetas de las propiedades de página y en el cuadro de diálogo **Editar etiqueta** al editar una etiqueta en la consola **Etiquetado**.

>[!NOTE]
>
>El nuevo idioma debe ser uno de los idiomas AEM reconocidos, es decir, debe estar disponible como nodo por debajo de `/libs/wcm/core/resources/languages`.
