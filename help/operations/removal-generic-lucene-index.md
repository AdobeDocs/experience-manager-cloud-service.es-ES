---
title: Eliminación del índice Lucene genérico
description: Obtenga información acerca de la eliminación planificada de índices Lucene genéricos y cómo puede verse afectado.
exl-id: 3b966d4f-6897-406d-ad6e-cd5cda020076
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1349'
ht-degree: 0%

---

# Eliminación del índice Lucene genérico {#generic-lucene-index-removal}

El Adobe pretende eliminar el índice &quot;genérico Lucene&quot; (`/oak:index/lucene-*`) de Adobe Experience Manager as a Cloud Service. AEM Este índice ha quedado obsoleto desde la versión 6.5 de la. AEM En este documento se describe el impacto de esta decisión, junto con descripciones detalladas sobre cómo examinar si una instancia de se ve afectada. También contiene formas de cambiar las consultas para que sigan funcionando sin el índice Lucene genérico.

## Fondo {#background}

AEM En la práctica, las consultas de texto completo son las que utilizan las siguientes funciones:

* `jcr:contains()` en JCR XPATH
* `CONTAINS` en JCR-SQL2

Estas consultas no pueden devolver resultados sin utilizar un índice. A diferencia de las consultas que sólo contienen restricciones de ruta o de propiedad, una consulta que contiene una restricción de texto completo para la que no se puede encontrar ningún índice (y por lo tanto se realiza un recorrido) siempre devolverá cero resultados.

El índice Lucene genérico (`/oak:index/lucene-*`AEM ) existe desde la versión 6.0 / Oak 1.0 para proporcionar una búsqueda de texto completo en la mayor parte de la jerarquía del repositorio, aunque algunas rutas, como `/jcr:system` y `/var` siempre se han excluido de esto. Sin embargo, este índice ha sido reemplazado en gran medida por índices de tipos de nodos más específicos (por ejemplo, `damAssetLucene-*` para el `dam:Asset` tipo de nodo), que admiten búsquedas de texto completo y de propiedades.

AEM En la versión 6.5, el índice Lucene genérico se marcó como obsoleto, lo que indica que se eliminará en versiones futuras. Desde entonces, se ha registrado una ADVERTENCIA cuando el índice se ha utilizado como se muestra en el siguiente fragmento de registro:

```text
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'search term') and isdescendantnode(a, '/content/mysite') /* xpath: /jcr:root/content/mysite//*[jcr:contains(.,"search term")] */ fullText="search" "term", path=/content/mysite//*). Please change the query or the index definitions.
```

AEM En las últimas versiones de la aplicación, el índice Lucene genérico se ha utilizado para admitir un número muy pequeño de funciones. Se están reprocesando para utilizar otros índices o se están modificando para eliminar la dependencia de este índice.

Por ejemplo, las consultas de búsqueda de referencia, como en el ejemplo siguiente, deben utilizar ahora el índice en `/oak:index/pathreference`, que solo indexa `String` valores de propiedad que coinciden con una expresión regular que busca rutas JCR.

```text
//*[jcr:contains(., '"/content/dam/mysite"')]
```

Para admitir volúmenes de datos de clientes más grandes, Adobe AEM ya no creará el índice Lucene genérico en entornos as a Cloud Service nuevos. Además, la Adobe empezará a eliminar el índice de los repositorios existentes. [Ver la cronología](#timeline) al final de este documento para obtener más información.

El Adobe ya ha ajustado los costes de índice a través de la `costPerEntry` y `costPerExecution` para garantizar que otros índices como `/oak:index/pathreference` se utilizan con preferencia siempre que sea posible.

Las aplicaciones de cliente que utilizan consultas que aún dependen de este índice deben actualizarse inmediatamente para aprovechar otros índices existentes, que se pueden personalizar si es necesario. Como alternativa, se pueden añadir nuevos índices personalizados a la aplicación del cliente. AEM Puede encontrar las instrucciones completas para la administración de índices en as a Cloud Service en la [documentación de indexación.](/help/operations/indexing.md)

## ¿Se Ve Afectado? {#are-you-affected}

El índice Lucene genérico se utiliza actualmente como alternativa si ningún otro índice de texto completo puede servir a una consulta. Cuando se utiliza este índice obsoleto, se registra un mensaje como este en el nivel WARN:

```text
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*). Please change the query or the index definitions.
```

En algunas circunstancias, Oak podría intentar utilizar otro índice de texto completo (como `/oak:index/pathreference`) para admitir la consulta de texto completo, pero si la cadena de consulta no coincide con la expresión regular de la definición de índice, se registrará un mensaje en el nivel WARN y es probable que la consulta no devuelva resultados.

```text
org.apache.jackrabbit.oak.query.QueryImpl Potentially improper use of index /oak:index/pathReference with queryFilterRegex (["']|^)/ to search for value "test"
```

Una vez eliminado el índice Lucene genérico, se registrará un mensaje como se muestra a continuación en el nivel WARN si una consulta de texto completo no puede localizar ninguna definición de índice adecuada:

```text
org.apache.jackrabbit.oak.query.QueryImpl Fulltext query without index for filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*); no results will be returned
```

>[!IMPORTANT]
>
>**Acción del cliente requerida**
>
> Si se registra cualquiera de los mensajes de advertencia mencionados, es posible que tenga que volver a trabajar la consulta para utilizar un índice de texto completo diferente o proporcionar un nuevo índice que admita la consulta.
>
>En las secciones siguientes se proporcionan detalles de los tipos de dependencias que puede ver y cómo tratarlas.

## Dependencias potenciales en los índices genéricos de Lucene {#potential-dependencies}

AEM Existen varias áreas en las que las aplicaciones y las instalaciones de la pueden depender de índices Lucene genéricos, tanto en instancias de autor como de publicación.

### Instancia de publicación {#publish-instance}

#### Consultas de aplicación personalizadas {#custom-application-queries}

La fuente de consultas más común que utiliza el índice Lucene genérico en una instancia de publicación son las consultas de aplicación personalizadas.

En los casos más simples, estas podrían ser consultas sin tipo de nodo especificado, lo que implica `nt:base` o `nt:base` especificado explícitamente, como:

```text
/jcr:root/content/mysite//*[jcr:contains(., 'search term')]
/jcr:root/content/mysite//element(*, nt:base)[jcr:contains(., 'search term')]
```

>[!IMPORTANT]
>
>**Acción del cliente requerida**
>
>Las consultas mencionadas deben modificarse para utilizar un tipo de nodo adecuado, como se detalla en la sección siguiente.

Por ejemplo, las consultas se pueden modificar para que devuelvan resultados que coincidan con páginas o cualquiera de los agregados debajo de `cq:Page node`. Por lo tanto, la consulta podría convertirse en:

```text
/jcr:root/content/mysite//element(*, cq:Page)[jcr:contains(., 'search term')]
```

En otros casos, una consulta puede especificar un tipo de nodo pero contener una restricción de texto completo que no se puede controlar con otro índice de texto completo, como:

```text
/jcr:root/content/dam//element(*, dam:Asset)[jcr:contains(jcr:content/metadata/@cq:tags, 'NewsTopics:cateogries/domestic'))]
```

En este caso, la consulta tiene el valor `dam:Asset` tipo de nodo, pero contiene una restricción de texto completo en el elemento relativo `jcr:content/metadata/@cq:tags` propiedad.

Esta propiedad no está marcada como analizada en la variable `damAssetLucene` índice, que es el índice de texto completo que se utiliza más comúnmente para consultas contra el `dam:Asset` tipo de nodo. Por lo tanto, este índice no se puede utilizar para esta consulta.

De este modo, la consulta vuelve al índice de texto completo genérico, donde todas las propiedades incluidas se marcan como analizadas por la coincidencia de comodín en `/oak:index/lucene-2/indexRules/nt:base/properties/prop`.

>[!IMPORTANT]
>
>**Acción del cliente requerida**
>
>Marcando el `jcr:content/metadata/@cq:tags` propiedad tal como se analiza en una versión personalizada de `damAssetLucene` index hará que este índice administre esta consulta y no se registrará ningún ADVERTENCIA.

### Ejemplo de autor {#author-instance}

Además de las consultas en los servlets de la aplicación del cliente, los componentes OSGi y los scripts de procesamiento, puede haber una serie de usos específicos del autor del índice Lucene genérico.

#### Búsqueda de referencia {#reference-search}

Históricamente, el índice Lucene genérico se ha utilizado para admitir la búsqueda de referencia o la búsqueda de contenido que contenga referencias a otra ruta de contenido. Estas consultas ya deberían haberse actualizado para utilizar el nuevo `/oak:index/pathreference` índice.

#### Búsqueda del selector de campos de ruta {#picker-search}

AEM incluye un componente de cuadro de diálogo personalizado con el tipo de recurso de Sling `granite/ui/components/coral/foundation/form/pathfield`AEM , que proporciona un explorador o selector para seleccionar otra ruta de acceso de la. El selector de campos de ruta predeterminado, que se utiliza cuando no hay ningún campo personalizado `pickerSrc` se define en la estructura de contenido, representa una barra de búsqueda en el cuadro de diálogo emergente.

Los tipos de nodo con los que se puede buscar se pueden especificar utilizando el `nodeTypes` propiedad.

En este momento, si no `nodeTypes` está presente, la consulta de búsqueda subyacente utilizará el `nt:base` tipo de nodo y, por lo tanto, es probable que utilice el índice Lucene genérico, registrando normalmente mensajes WARN similares a los siguientes.

```text
20.01.2022 18:56:06.412 *WARN* [127.0.0.1 [1642704966377] POST /mnt/overlay/granite/ui/content/coral/foundation/form/pathfield/picker.result.single.html HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') and isdescendantnode(a, '/content') /* xpath: /jcr:root/content//element(*, nt:base)[(jcr:contains(., 'test'))] order by @jcr:score descending */ fullText="test", path=/content//*). Please change the query or the index definitions.
```

Antes de la eliminación del índice Lucene genérico, la variable `pathfield` El componente se actualizará para que el cuadro de búsqueda esté oculto para los componentes que utilizan el selector predeterminado, que no proporciona un `nodeTypes` propiedad.

| Selector de campos de ruta con búsqueda | Selector de campos de ruta sin búsqueda |
|---|---|
| ![Selector de campos de ruta con búsqueda](assets/index-pathfield-picker-with-search.png) | ![Selector de campos de ruta sin búsqueda](assets/index-pathfield-picker-without-search.png) |

>[!IMPORTANT]
>
>**Acción del cliente requerida**
>
>Si el cliente desea conservar la funcionalidad de búsqueda dentro del selector de campos de ruta, una `nodeTypes` debe proporcionar una lista con los tipos de nodo con los que desea realizar una consulta. Se pueden especificar como una lista de tipos de nodo separados por comas en una `String` propiedad. Si no se requiere ninguna búsqueda, no se requiere ninguna acción por parte del cliente.

>[!NOTE]
>
>El Editor del modelo de fragmentos de contenido utiliza campos de ruta especializados con el tipo de recurso Sling `dam/cfm/models/editor/components/contentreference`.
> * En la actualidad, estos realizan consultas sin especificar tipos de nodo, lo que da como resultado que se registre un ADVERTENCIA debido al uso del índice Lucene genérico.
> * Las instancias de estos componentes pronto utilizarán de forma predeterminada `cq:Page` y `dam:Asset` tipos de nodo sin más acción del cliente.
> * El `nodeTypes` se puede agregar la propiedad para anular estos tipos de nodos predeterminados.


## Cronología para la eliminación genérica de Lucene {#timeline}

Adobe adoptará un enfoque en dos fases para eliminar el índice Lucene genérico.

* **Fase 1** (inicio planificado el 31 de enero de 2022): Ya no se crea `/oak:index/lucene-*` AEM en nuevos entornos as a Cloud Service de la.
* **Fase 2** (inicio previsto para el 31 de marzo de 2022): Eliminar `/oak:index/lucene-*` AEM índice de entornos as a Cloud Service existentes de la.

El Adobe supervisará los mensajes de registro mencionados anteriormente e intentará ponerse en contacto con los clientes que sigan dependiendo del índice Lucene genérico.

Como mitigación a corto plazo, Adobe agregará definiciones de índice personalizadas directamente a los sistemas de los clientes para evitar problemas funcionales o de rendimiento como resultado de la eliminación del índice Lucene genérico según sea necesario.

En estos casos, se proporcionará al cliente la definición de índice actualizada y se le aconsejará que la incluya en futuras versiones de su aplicación mediante Cloud Manager.
