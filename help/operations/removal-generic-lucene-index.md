---
title: Eliminación del índice de lucene genérico
description: Eliminación del índice de lucene genérico
exl-id: fe0e00ac-f9c8-43cf-83c2-5a353f5eaeab
source-git-commit: bc7ef6567ad5baa4becd28a7e7d96bd6b579e1ad
workflow-type: tm+mt
source-wordcount: '1305'
ht-degree: 0%

---

# Eliminación del índice &quot;lucene genérico&quot;

El Adobe pretende eliminar el índice &quot;lucene genérico&quot; (`/oak:index/lucene-*`) de Adobe Experience Manager as a Cloud Service. Este índice ha quedado obsoleto desde AEM 6.5. En esta documentación se describe el impacto de esta decisión, junto con descripciones detalladas sobre cómo examinar si una instancia de AEM se ve afectada. Finalmente, contiene formas de cambiar las consultas para que funcionen sin que este índice esté presente.

## Fondo

En AEM, las consultas &quot;de texto completo&quot; son aquellas que utilizan las siguientes funciones:

* `jcr:contains()` en JCR XPATH
* `CONTAINS` en JCR-SQL2

Estas consultas no pueden devolver resultados sin utilizar un índice. A diferencia de una consulta que solo contiene restricciones de ruta o propiedad, una consulta que contiene una restricción de texto completo para la que no se puede encontrar ningún índice (y por lo tanto se realiza una travesía) siempre devolverá 0 resultados.

Índice &quot;lucene genérico&quot; (`/oak:index/lucene-*`) existe desde AEM 6.0 / Oak 1.0 para proporcionar una búsqueda de texto completo en la mayoría de la jerarquía de repositorios (algunas rutas, como `/jcr:system` y `/var` siempre se han excluido de esto) sin embargo, este índice se ha sustituido en gran medida por índices en tipos de nodo más específicos (por ejemplo `damAssetLucene-*` para el tipo de nodo dam:Asset) que admite búsquedas de texto completo y de propiedades.

En AEM 6.5, el índice &quot;lucene genérico&quot; se marcó como obsoleto (indica que se eliminará en versiones futuras) y, desde entonces, se ha registrado una ADVERTENCIA cuando se ha utilizado el índice:

```
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'search term') and isdescendantnode(a, '/content/mysite') /* xpath: /jcr:root/content/mysite//*[jcr:contains(.,"search term")] */ fullText="search" "term", path=/content/mysite//*). Please change the query or the index definitions.
```

En versiones AEM recientes, el índice &quot;lucene genérico&quot; se ha utilizado para admitir un número muy pequeño de funciones. Se están reformulando para utilizar otros índices o se están modificando para eliminar la dependencia de este índice.
Por ejemplo, las consultas de &quot;búsqueda de referencia&quot;, del formulario que se muestra a continuación, deben utilizar el índice en &quot;/oak:index/pathreference&quot; (que indexa únicamente los valores de propiedad String que coinciden con una expresión regular que busca rutas JCR). 

```
//*[jcr:contains(., '"/content/dam/mysite"')]
```

Para soportar volúmenes de datos de clientes más grandes, Adobe ya no creará el índice &quot;lucene genérico&quot; en entornos as a Cloud Service nuevos AEM y, a continuación, comenzará a eliminar el índice de los repositorios existentes. Ya hemos ajustado los costes de índice (a través de las propiedades &quot;costPerEntry&quot; y &quot;costPerExecution&quot;) para garantizar que otros índices (como `/oak:index/pathreference`) se utilizan con preferencia sobre `/oak:index/lucene-*` siempre que sea posible. 

Las aplicaciones de cliente que utilizan consultas que aún dependen de este índice deben actualizarse inmediatamente para aprovechar otros índices existentes (que pueden personalizarse si es necesario) o deben agregarse nuevos índices personalizados a la aplicación del cliente. Puede encontrar instrucciones completas para la administración de índices en AEM as a Cloud Service en la [documentación de indexación](/help/operations/indexing.md).

## ¿Cómo saber si su aplicación depende del índice &quot;lucene genérico&quot;?

El índice &quot;lucene genérico&quot; se utiliza actualmente como &quot;reserva&quot; si ningún otro índice de texto completo puede servir para una consulta. Cuando se utiliza este índice obsoleto, se registra un mensaje como este a nivel WARN:

```
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*). Please change the query or the index definitions.
```

En algunas circunstancias, Oak podría intentar usar otro índice de texto completo (como `/oak:index/pathreference`) para admitir la consulta de texto completo, pero si la cadena de consulta no coincide con la expresión regular en la definición del índice, se registrará un mensaje a nivel WARN y es probable que la consulta no devuelva resultados.

```
org.apache.jackrabbit.oak.query.QueryImpl Potentially improper use of index /oak:index/pathReference with queryFilterRegex (["']|^)/ to search for value "test"
```

Una vez eliminado el índice &quot;lucene genérico&quot;, se registrará un mensaje como se muestra a continuación a nivel WARN si una consulta de texto completo no puede localizar ninguna definición de índice adecuada:

```
org.apache.jackrabbit.oak.query.QueryImpl Fulltext query without index for filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*); no results will be returned
```

Si se registra alguno de estos elementos, es posible que tenga que volver a trabajar en la consulta para utilizar un índice de texto completo diferente o proporcionar un nuevo índice que admita la consulta. A continuación se proporcionan detalles sobre los tipos de dependencias que puede ver y cómo tratarlas.

## Posibles dependencias en el índice &quot;lucene genérico&quot;

### Publicación

#### Consultas de aplicaciones personalizadas

La fuente más común de consultas que utilizan el índice &quot;lucene genérico&quot; en Publish son las consultas de aplicaciones personalizadas.

En los casos más sencillos, estas pueden ser consultas sin ningún tipo de nodo especificado (lo que implica &#39;nt:base&#39;) o nt:base especificado explícitamente, como:

```
/jcr:root/content/mysite//*[jcr:contains(., 'search term')]
/jcr:root/content/mysite//element(*, nt:base)[jcr:contains(., 'search term')]
```

Acción requerida : Estas consultas se pueden modificar para que utilicen un tipo de nodo adecuado; por ejemplo, para devolver resultados que coincidan con páginas (o cualquiera de los &quot;agregados&quot; debajo del nodo cq:Page), la consulta podría convertirse en:

```
/jcr:root/content/mysite//element(*, cq:Page)[jcr:contains(., 'search term')]
```

En otros casos, una consulta puede especificar un tipo de nodo, pero contener una restricción de texto completo que no se puede controlar con otro índice de texto completo, como:

```
/jcr:root/content/dam//element(*, dam:Asset)[jcr:contains(jcr:content/metadata/@cq:tags, 'NewsTopics:cateogries/domestic'))]
```

En este caso, la consulta tiene el tipo de nodo &quot;dam:Asset&quot;, pero contiene una restricción de texto completo sobre el elemento relativo `jcr:content/metadata/@cq:tags` propiedad.

Esta propiedad no está marcada como &#39;analizada&#39; en el índice damAssetLucene (el índice de texto completo más usado para consultas con el tipo de nodo &quot;dam:Asset&quot;), por lo que este índice no se puede usar para esta consulta.

Como tal, la consulta vuelve al índice &quot;texto completo genérico&quot;, donde todas las propiedades incluidas están marcadas como analizadas por la coincidencia comodín en `/oak:index/lucene-2/indexRules/nt:base/properties/prop`.

Acción del cliente requerida : marcando el `jcr:content/metadata/@cq:tags` como &#39;analyzed&#39; en una versión personalizada del índice damAssetLucene hará que este índice gestione esta consulta y no se registrará ninguna WARN.

### Autor 

Además de las consultas en los servlets de aplicaciones para clientes, los componentes OSGI y las secuencias de comandos de renderización, puede haber una serie de usos específicos de autor del índice &quot;lucene genérico&quot;. 

#### Búsqueda de referencias

Históricamente, el índice &quot;lucene genérico&quot; se ha utilizado para admitir la &quot;búsqueda de referencia&quot; (búsqueda de contenido que contiene referencias a otra ruta de contenido). Estas consultas ya deberían haberse movido para utilizar el nuevo índice &quot;/oak:index/pathreference&quot;.
Acción del cliente requerida : no se requiere ninguna acción por parte del cliente.


#### Búsqueda del selector de campos de rutas

AEM incluye un componente de cuadro de diálogo personalizado (tipo de recurso Sling &quot;granite/ui/components/coral/foundation/form/pathfield&quot;) que proporciona un navegador (selector) para seleccionar otra ruta de AEM.  El selector de ruta predeterminado (que se utiliza cuando no hay ninguna propiedad personalizada &quot;pickerSrc&quot; definida en la estructura de contenido) representa una barra de búsqueda en el cuadro de diálogo emergente.
Los tipos de nodo con los que se puede buscar se pueden especificar mediante la propiedad &quot;nodeTypes&quot;.

Actualmente, si no hay ninguna propiedad &#39;nodeTypes&#39; presente, la consulta de búsqueda subyacente utilizará el tipo de nodo &#39;nt:base&#39; y, por lo tanto, es probable que utilice el índice &#39;lucene genérico&#39; (normalmente se registran los mensajes WARN que se muestran a continuación).

```
20.01.2022 18:56:06.412 *WARN* [127.0.0.1 [1642704966377] POST /mnt/overlay/granite/ui/content/coral/foundation/form/pathfield/picker.result.single.html HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') and isdescendantnode(a, '/content') /* xpath: /jcr:root/content//element(*, nt:base)[(jcr:contains(., 'test'))] order by @jcr:score descending */ fullText="test", path=/content//*). Please change the query or the index definitions.
```

Antes de eliminar &quot;lucene genérico&quot;, el componente pathfield se actualizará para que el cuadro de búsqueda esté oculto para los componentes que utilizan el selector predeterminado, que no proporcionan la propiedad &quot;nodeTypes&quot; .

| Selector de campo de ruta con búsqueda | Selector de campo de ruta sin búsqueda |
|---|---|
| ![Selector de campo de ruta con búsqueda](assets/index-pathfield-picker-with-search.png) | ![Selector de campo de ruta sin búsqueda](assets/index-pathfield-picker-without-search.png) |


Acción del cliente requerida : Si no se requiere ninguna búsqueda, no se requiere ninguna acción por parte del cliente.

Si el cliente desea conservar la funcionalidad de búsqueda dentro del selector de campos de rutas, se debe proporcionar una propiedad &quot;nodeTypes&quot; que enumere los tipos de nodos a los que desea realizar la consulta. Pueden especificarse como una lista de tipos de nodos separados por comas en una propiedad String .


>[!NOTE]
>El editor de modelos de fragmentos de contenido utiliza una ruta de acceso especializada con el tipo de recurso de Sling &quot;dam/cfm/models/editor/components/contentreference&quot;.
> * Actualmente realizan consultas sin tipos de nodos especificados, lo que resulta en que se registre una WARN debido al uso del índice &quot;lucene genérico&quot;.
> * Las instancias de estos componentes pronto pasará automáticamente a utilizar los tipos de nodos &quot;cq:Page&quot; y &quot;dam:Asset&quot; sin más acciones por parte del cliente.
> * Se puede añadir la propiedad &quot;nodeTypes&quot; para anular estos tipos de nodos predeterminados. 





## Línea de tiempo para eliminar &quot;lucene genérico&quot;

El Adobe adoptará un enfoque en dos fases para eliminar el índice &quot;lucene genérico&quot;.

**Fase 1** (inicio planificado para el 31 de enero de 2022): Ya no se crea &quot;/oak:index/lucene-*&quot; en los nuevos entornos as a Cloud Service AEM.

**Fase 2** (inicio planificado para el 31 de marzo de 2022) : Elimine el índice &quot;/oak:index/lucene-*&quot; de los nuevos entornos as a Cloud Service AEM.

Adobe supervisará los mensajes de registro mencionados anteriormente e intentará contactar con los clientes que siguen dependiendo del índice &quot;lucene genérico&quot;.

Como mitigación a corto plazo, si es necesario, el Adobe agregará definiciones de índice personalizadas directamente a los sistemas de clientes para evitar problemas funcionales o de rendimiento como resultado de la eliminación del índice &quot;lucene genérico&quot;.

En estos casos, se proporcionará al cliente la definición de índice actualizada y se le aconsejará que la incluya en futuras versiones de su aplicación a través de Cloud Manager.
