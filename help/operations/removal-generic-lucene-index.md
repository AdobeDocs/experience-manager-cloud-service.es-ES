---
title: Eliminación del índice de Lucene genérico
description: Obtenga información sobre la eliminación planificada de los índices genéricos de Lucene y cómo puede verse afectado.
exl-id: 3b966d4f-6897-406d-ad6e-cd5cda020076
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1349'
ht-degree: 0%

---

# Eliminación del índice de Lucene genérico {#generic-lucene-index-removal}

Adobe intends to remove the &quot;generic Lucene&quot; index (`/oak:index/lucene-*`) from Adobe Experience Manager as a Cloud Service. Este índice ha quedado obsoleto desde AEM 6.5. En este documento se describe el impacto de esta decisión, junto con descripciones detalladas sobre cómo examinar si una instancia de AEM se ve afectada. También contiene formas de cambiar las consultas para que sigan funcionando sin el índice genérico de Lucene.

## Fondo {#background}

En AEM, las consultas de texto completo son aquellas que utilizan las siguientes funciones:

* `jcr:contains()` en JCR XPATH
* `CONTAINS` in JCR-SQL2

Such queries cannot return results without using an index. A diferencia de una consulta que solo contiene restricciones de ruta o propiedad, una consulta que contiene una restricción de texto completo para la que no se puede encontrar ningún índice (y por lo tanto se realiza una travesía) siempre devolverá cero resultados.

El índice genérico de Lucene (`/oak:index/lucene-*`) existe desde AEM 6.0 / Oak 1.0 para proporcionar una búsqueda de texto completo en la mayoría de la jerarquía del repositorio, aunque algunas rutas, como `/jcr:system` y `/var` siempre se han excluido de esto. Sin embargo, este índice se ha sustituido en gran medida por índices en tipos de nodo más específicos (por ejemplo `damAssetLucene-*` para el `dam:Asset` tipo de nodo), que admite tanto búsquedas de texto completo como de propiedades.

En AEM 6.5, el índice genérico de Lucene se marcó como obsoleto, indicando que se eliminaría en futuras versiones. Desde entonces, se ha registrado una ADVERTENCIA cuando se ha utilizado el índice como se ilustra en el siguiente fragmento de registro:

```text
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'search term') and isdescendantnode(a, '/content/mysite') /* xpath: /jcr:root/content/mysite//*[jcr:contains(.,"search term")] */ fullText="search" "term", path=/content/mysite//*). Please change the query or the index definitions.
```

En versiones AEM recientes, el índice genérico de Lucene se ha utilizado para admitir un número muy pequeño de funciones. Se están reformulando para utilizar otros índices o se están modificando para eliminar la dependencia de este índice.

Por ejemplo, las consultas de búsqueda de referencia, como en el ejemplo siguiente, ahora deben utilizar el índice en `/oak:index/pathreference`, que solo indexa `String` valores de propiedad que coinciden con una expresión regular que busca rutas JCR.

```text
//*[jcr:contains(., '"/content/dam/mysite"')]
```

Para soportar volúmenes de datos de clientes más grandes, Adobe ya no creará el índice genérico de Lucene en los nuevos entornos as a Cloud Service AEM. Additionally, Adobe will begin removing the index from existing repositories. [See the timeline](#timeline) at the end of this document for more details.

El Adobe ya ha ajustado los costes de índice a través del `costPerEntry` y `costPerExecution` propiedades para garantizar que otros índices como `/oak:index/pathreference` se utilizan con preferencia siempre que sea posible.

Las aplicaciones de cliente que utilizan consultas que aún dependen de este índice deben actualizarse inmediatamente para aprovechar otros índices existentes, que pueden personalizarse si es necesario. Alternativamente, se pueden agregar nuevos índices personalizados a la aplicación del cliente. Puede encontrar instrucciones completas para la administración de índices en AEM as a Cloud Service en la [documentación de indexación.](/help/operations/indexing.md)

## ¿Estás Afectado? {#are-you-affected}

El índice genérico de Lucene se utiliza actualmente como alternativa si ningún otro índice de texto completo puede servir una consulta. Cuando se utiliza este índice obsoleto, se registra un mensaje como este a nivel WARN:

```text
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*). Please change the query or the index definitions.
```

En algunas circunstancias, Oak podría intentar usar otro índice de texto completo (como `/oak:index/pathreference`) para admitir la consulta de texto completo, pero si la cadena de consulta no coincide con la expresión regular en la definición del índice, se registrará un mensaje a nivel WARN y es probable que la consulta no devuelva resultados.

```text
org.apache.jackrabbit.oak.query.QueryImpl Potentially improper use of index /oak:index/pathReference with queryFilterRegex (["']|^)/ to search for value "test"
```

Once the generic Lucene index has been removed, a message as shown below will be logged at WARN level if a full text query is not able to locate any suitable index definition:

```text
org.apache.jackrabbit.oak.query.QueryImpl Fulltext query without index for filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*); no results will be returned
```

>[!IMPORTANT]
>
>**Acción del cliente requerida**
>
> Si se registra cualquiera de los mensajes de advertencia mencionados anteriormente, es posible que tenga que volver a trabajar en la consulta para utilizar un índice de texto completo diferente o proporcionar un nuevo índice para admitir la consulta.
>
>Details of the types of dependencies you might see and how to address them are provided in the following sections.

## Dependencias potenciales de los índices de Lucene genéricos {#potential-dependencies}

Hay varias áreas en las que las aplicaciones y las instalaciones de AEM pueden depender de los índices genéricos de Lucene tanto en las instancias de autor como de publicación.

### Instancia de publicación {#publish-instance}

#### Consultas de aplicaciones personalizadas {#custom-application-queries}

La fuente más común de consultas que utilizan el índice genérico de Lucene en una instancia de publicación son las consultas de aplicación personalizadas.

En los casos más sencillos, estas pueden ser consultas sin ningún tipo de nodo especificado, lo que implica `nt:base` o `nt:base` especificado explícitamente, como:

```text
/jcr:root/content/mysite//*[jcr:contains(., 'search term')]
/jcr:root/content/mysite//element(*, nt:base)[jcr:contains(., 'search term')]
```

>[!IMPORTANT]
>
>**Acción del cliente requerida**
>
>Las consultas mencionadas anteriormente deben modificarse para utilizar un tipo de nodo adecuado, tal como se detalla en la sección siguiente.

Por ejemplo, las consultas se pueden modificar para devolver resultados que coincidan con las páginas o cualquiera de los agregados debajo de la variable `cq:Page node`. Por lo tanto, la consulta podría convertirse en:

```text
/jcr:root/content/mysite//element(*, cq:Page)[jcr:contains(., 'search term')]
```

En otros casos, una consulta puede especificar un tipo de nodo pero contener una restricción de texto completo que no se puede controlar con otro índice de texto completo, como:

```text
/jcr:root/content/dam//element(*, dam:Asset)[jcr:contains(jcr:content/metadata/@cq:tags, 'NewsTopics:cateogries/domestic'))]
```

En este caso, la consulta tiene la variable `dam:Asset` tipo de nodo, pero contiene una restricción de texto completo sobre el `jcr:content/metadata/@cq:tags` propiedad.

Esta propiedad no está marcada como analizada en la variable `damAssetLucene` índice, que es el índice de texto completo más utilizado para las consultas con el `dam:Asset` tipo de nodo. Por lo tanto, este índice no se puede usar para esta consulta.

Como tal, la consulta vuelve al índice de texto completo genérico donde todas las propiedades incluidas están marcadas como analizadas por la coincidencia comodín en `/oak:index/lucene-2/indexRules/nt:base/properties/prop`.

>[!IMPORTANT]
>
>**Acción del cliente requerida**
>
>Marcar la variable `jcr:content/metadata/@cq:tags` tal como se analiza en una versión personalizada de la variable `damAssetLucene` index hará que esta consulta sea manejada por este índice, y no se registrará ninguna WARN.

### Instancia de autor {#author-instance}

Además de las consultas en los servlets de aplicaciones para clientes, los componentes OSGi y las secuencias de comandos de renderización, puede haber una serie de usos específicos de autor del índice Lucene genérico.

#### Reference Search {#reference-search}

Historically the generic Lucene index has been used to support reference search or searching for content which contains references to another content path. Such queries should already have updated to use the new `/oak:index/pathreference` index.

#### Búsqueda del selector de campos de ruta {#picker-search}

AEM incluye un componente de diálogo personalizado con el tipo de recurso Sling `granite/ui/components/coral/foundation/form/pathfield`, que proporciona un navegador o selector para seleccionar otra ruta de AEM. El selector de campos de ruta predeterminado, que se utiliza cuando no hay `pickerSrc` se define en la estructura de contenido y representa una barra de búsqueda en el cuadro de diálogo emergente.

Los tipos de nodo con los que se puede buscar se pueden especificar utilizando la variable `nodeTypes` propiedad.

En la actualidad, si no `nodeTypes` está presente, la consulta de búsqueda subyacente utilizará la variable `nt:base` tipo de nodo y, por lo tanto, es probable que utilice el índice genérico de Lucene, registrando normalmente mensajes WARN similares a los siguientes.

```text
20.01.2022 18:56:06.412 *WARN* [127.0.0.1 [1642704966377] POST /mnt/overlay/granite/ui/content/coral/foundation/form/pathfield/picker.result.single.html HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') and isdescendantnode(a, '/content') /* xpath: /jcr:root/content//element(*, nt:base)[(jcr:contains(., 'test'))] order by @jcr:score descending */ fullText="test", path=/content//*). Please change the query or the index definitions.
```

Antes de eliminar el índice genérico de Lucene, la variable `pathfield` se actualizará para que el cuadro de búsqueda esté oculto para los componentes que utilicen el selector predeterminado, que no proporcionan una variable `nodeTypes` propiedad.

| Selector de campos de ruta con búsqueda | Selector de campos de ruta sin búsqueda |
|---|---|
| ![Path Field Picker with Search](assets/index-pathfield-picker-with-search.png) | ![Selector de campos de ruta sin búsqueda](assets/index-pathfield-picker-without-search.png) |

>[!IMPORTANT]
>
>**Acción del cliente requerida**
>
>Si el cliente desea conservar la funcionalidad de búsqueda dentro del selector de campos de ruta, una `nodeTypes` debe proporcionarse una propiedad que enumere los tipos de nodo a los que desea realizar la consulta. These can be specified as a comma-separated list of node types in a `String` property. Si no se requiere ninguna búsqueda, no se requiere ninguna acción por parte del cliente.

>[!NOTE]
>
>The Content Fragment Model Editor uses a specialized path fields with the Sling resource type `dam/cfm/models/editor/components/contentreference`.
> * Actualmente realizan consultas sin tipos de nodos especificados, lo que resulta en que se registre una WARN debido al uso del índice Lucene genérico.
> * Instances of these components will soon automatically default to using `cq:Page` and `dam:Asset` node types without further customer action.
> * La variable `nodeTypes` para anular estos tipos de nodo predeterminados.


## Cronología de eliminación de Lucene genérica {#timeline}

Adobe will take a two-phase approach to remove the generic Lucene index.

* **Fase 1** (inicio previsto: 31 de enero de 2022): Ya no se crea `/oak:index/lucene-*` en los nuevos entornos as a Cloud Service AEM.
* **Fase 2** (inicio previsto: 31 de marzo de 2022): Eliminar `/oak:index/lucene-*` índice de entornos as a Cloud Service AEM existentes.

Adobe supervisará los mensajes de registro mencionados anteriormente e intentará contactar con los clientes que siguen dependiendo del índice genérico de Lucene.

Como mitigación a corto plazo, el Adobe agregará definiciones de índices personalizadas directamente a los sistemas de clientes para evitar problemas funcionales o de rendimiento como resultado de la eliminación del índice Lucene genérico según sea necesario.

En estos casos, se proporcionará al cliente la definición de índice actualizada y se le aconsejará que la incluya en futuras versiones de su aplicación a través de Cloud Manager.
