---
title: Creación del etiquetado en aplicaciones de AEM
description: Trabajo mediante programación con etiquetas o ampliación de etiquetas dentro de una aplicación AEM personalizada
exl-id: a106dce1-5d51-406a-a563-4dea83987343
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 1%

---

# Creación del etiquetado en aplicaciones de AEM {#building-tagging-into-aem-applications}

Para trabajar mediante programación con etiquetas o ampliar etiquetas dentro de una aplicación de AEM personalizada, este documento describe el uso de la variable

* [API de etiquetado](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html)

que interactúa con el

* [Marco de etiquetado](tagging-framework.md)

Para información relacionada con el etiquetado:

* Consulte [Uso de etiquetas](/help/sites-cloud/authoring/features/tags.md) para obtener información sobre el etiquetado de contenido como autor de contenido.
* Consulte Administración de etiquetas para conocer la perspectiva de un administrador sobre la creación y administración de etiquetas, así como sobre las etiquetas de contenido que se han aplicado.

## Información general sobre la API de etiquetado {#overview-of-the-tagging-api}

La aplicación del [marco de etiquetado](tagging-framework.md) en AEM permite la administración de etiquetas y contenido de etiquetas mediante la API de JCR. `TagManager` garantiza que las etiquetas se introduzcan como valores en la variable `cq:tags` la propiedad matriz de cadenas no está duplicada, elimina `TagID`s señala a etiquetas y actualizaciones no existentes `TagID`s para etiquetas movidas o combinadas. `TagManager` utiliza un oyente de observación JCR que revierte cualquier cambio incorrecto. Las clases principales se encuentran en la [com.day.cq.tagging](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html) paquete:

* `JcrTagManagerFactory` - devuelve una implementación basada en JCR de un `TagManager`. Es la implementación de referencia de la API de etiquetado.
* `TagManager` : permite resolver y crear etiquetas por rutas y nombres.
* `Tag` - define el objeto tag .

### Obtención de un TagManager basado en JCR {#getting-a-jcr-based-tagmanager}

Para recuperar un `TagManager` , debe tener un JCR `Session` y para llamar a `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

En el contexto típico de Sling, también puede adaptarse a un `TagManager` de la variable `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Recuperación de un objeto Tag {#retrieving-a-tag-object}

A `Tag` se puede recuperar mediante la variable `TagManager`, resolviendo una etiqueta existente o creando una nueva:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

Para la implementación basada en JCR, que asigna `Tags` en JCR `Nodes`, puede utilizar directamente el `adaptTo` mecanismo si tiene el recurso (por ejemplo, `/content/cq:tags/default/my/tag`):

```java
Tag tag = resource.adaptTo(Tag.class);
```

Mientras que una etiqueta solo puede convertirse *from* un recurso (no un nodo), una etiqueta puede convertirse *a* un nodo y un recurso:

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>Adaptación directa desde `Node` a `Tag` no es posible, porque `Node` no implementa el Sling `Adaptable.adaptTo(Class)` método.

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
>El `RangeIterator` para usar es:
>
>`com.day.cq.commons.RangeIterator`

### Eliminación de tags {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### Duplicación de etiquetas {#replicating-tags}

Es posible utilizar el servicio de replicación (`Replicator`) con etiquetas porque las etiquetas son de tipo `nt:hierarchyNode`:

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## El recolector de residuos de etiquetas {#the-tag-garbage-collector}

El recolector de residuos de etiquetas es un servicio de fondo que limpia las etiquetas que están ocultas y que no se utilizan. Las etiquetas ocultas y no utilizadas son las siguientes `/content/cq:tags` que tienen un `cq:movedTo` y no se utilizan en un nodo de contenido. Tienen un recuento de cero. Al utilizar este proceso de eliminación diferido, el nodo de contenido (es decir, el `cq:tags` ) no tiene que actualizarse como parte de la operación move o merge . Las referencias en la variable `cq:tags` se actualiza automáticamente cuando `cq:tags` se actualiza, por ejemplo, a través del cuadro de diálogo de propiedades de página.

El recolector de residuos de etiquetas se ejecuta de forma predeterminada una vez al día. Esto se puede configurar en:

`http://<host>:<port>/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector`

## Búsqueda de etiquetas y Lista de etiquetas {#tag-search-and-tag-listing}

La búsqueda de etiquetas y la lista de etiquetas funcionan de la siguiente manera:

* La búsqueda de `TagID` busca las etiquetas que tienen la propiedad `cq:movedTo` configure como `TagID` y sigue la `cq:movedTo` `TagID`s.
* La búsqueda del título de la etiqueta solo busca las etiquetas que no tienen un `cq:movedTo` propiedad.

## Etiquetas en diferentes idiomas {#tags-in-different-languages}

Una etiqueta `title` puede definirse en diferentes idiomas. A continuación, se agrega una propiedad que distingue entre idiomas al nodo de etiqueta . Esta propiedad tiene el formato `jcr:title.<locale>`, por ejemplo, `jcr:title.fr` para la traducción al francés. `<locale>` debe ser una cadena de configuración regional ISO en minúscula y usar un guion bajo (`_`) en lugar de guión (`-`), por ejemplo: `de_ch`.

Por ejemplo, cuando la variable **Animales** se agrega a la variable **Productos** page, el valor `stockphotography:animals` se añade a la propiedad `cq:tags` del nodo `/content/wknd/en/products/jcr:content`. Se hace referencia a la traducción desde el nodo tag .

La API del lado del servidor se ha localizado `title`Métodos relacionados:

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

En AEM, el idioma se puede obtener desde el idioma de la página o desde el idioma del usuario.

Para el etiquetado, la localización depende del contexto como etiqueta `titles` se puede mostrar en el idioma de la página, en el idioma del usuario o en cualquier otro idioma.

### Adición de un nuevo idioma al cuadro de diálogo Editar etiqueta {#adding-a-new-language-to-the-edit-tag-dialog}

El siguiente procedimiento describe cómo añadir un nuevo idioma (por ejemplo, finés) al **Edición de etiquetas** diálogo:

1. En **CRXDE**, editar la propiedad de varios valores `languages` del nodo `/content/cq:tags`.
1. Agregar `fi_fi`, que representa la configuración regional finlandesa, y guarde los cambios.

El finés ahora está disponible en el cuadro de diálogo de etiquetas de las propiedades de página y en el **Editar etiqueta** al editar una etiqueta en el **Etiquetado** consola.

>[!NOTE]
>
>El nuevo idioma debe ser uno de los idiomas AEM reconocidos, es decir, debe estar disponible como nodo a continuación `/libs/wcm/core/resources/languages`.
