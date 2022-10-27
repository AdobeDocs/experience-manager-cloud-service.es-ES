---
title: Referencia de predicados del generador de consultas
description: Referencia de predicado para la API de Query Builder.
exl-id: 77118ef7-4d29-470d-9c4b-20537a408940
source-git-commit: 3c7e6d2213e059b1b8a90feea4672a4436873a01
workflow-type: tm+mt
source-wordcount: '2268'
ht-degree: 2%

---

# Referencia de predicados del generador de consultas {#query-builder-predicate-reference}

## General {#general}

### root {#root}

Este es el grupo de predicados raíz. Admite todas las funciones de un grupo y permite configurar parámetros de consulta globales.

El nombre &quot;root&quot; nunca se utiliza en una consulta, está implícito.

#### Propiedades {#properties-18}

* **`p.offset`** - número que indica el inicio de la página de resultados, es decir, cuántos elementos se deben omitir
* **`p.limit`** - número que indica el tamaño de la página
* **`p.guessTotal`** - recomendado: evite calcular el total del resultado completo, que puede resultar costoso; bien un número que indica el total máximo que se va a contar (por ejemplo, 1000, un número que proporciona a los usuarios suficientes comentarios sobre el tamaño aproximado y los números exactos para obtener resultados más pequeños) o `true` para contar únicamente hasta el mínimo necesario `p.offset` + `p.limit`
* **`p.excerpt`** - si está configurado como `true`, incluir extracto de texto completo en el resultado
* **`p.hits`** : (solo para el servlet JSON) seleccione la forma en que se escriben las visitas como JSON, con estas visitas estándar (ampliables mediante el servicio ResultHitWriter):
   * **`simple`** - artículos mínimos como `path`, `title`, `lastmodified`, `excerpt` (si está configurado)
   * **`full`** - renderización JSON de sling del nodo, con `jcr:path` indicando la ruta de la visita: de forma predeterminada, solo enumera las propiedades directas del nodo, incluya un árbol más profundo con `p.nodedepth=N`, con 0 que significa todo el subárbol infinito; add `p.acls=true` para incluir los permisos JCR de la sesión actual en el elemento de resultado dado (asignaciones: `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`)
   * **`selective`** - solo las propiedades especificadas en `p.properties`, que es un espacio separado (utilice `+` en direcciones URL) lista de rutas relativas; si la ruta relativa tiene una profundidad `>1` se representarán como objetos secundarios; el especial `jcr:path` incluye la ruta de acceso de la visita

### grupo  {#group}

Este predicado permite generar condiciones anidadas. Los grupos pueden contener grupos anidados. Todo en una consulta de Query Builder está implícito en un grupo raíz, que puede tener `p.or` y `p.not` también.

A continuación se muestra un ejemplo para hacer coincidir una de las dos propiedades con un valor:

```text
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

Conceptualmente `(1_property` O `2_property)`.

El siguiente es un ejemplo para grupos anidados:

```text
fulltext=Management
group.p.or=true
group.1_group.path=/content/wknd/ch/de
group.1_group.type=cq:Page
group.2_group.path=/content/dam/wknd
group.2_group.type=dam:Asset
```

Esto busca el término **Administración** dentro de las páginas `/content/wknd/ch/de` o en activos en `/content/dam/wknd`.

Conceptualmente `fulltext AND ( (path AND type) OR (path AND type) )`. Tenga en cuenta que estas uniones O necesitan buenos índices por motivos de rendimiento.

#### Propiedades {#properties-6}

* **`p.or`** - si está configurado como `true`, solo debe coincidir un predicado del grupo. De forma predeterminada, `false`, lo que significa que todos deben coincidir
* **`p.not`** - si está configurado como `true`, anula el grupo (el valor predeterminado es `false`)
* **`<predicate>`** - agrega predicados anidados
* **`N_<predicate>`** - añade varios predicados anidados del mismo tiempo, como `1_property, 2_property, ...`

### orderby {#orderby}

Este predicado permite ordenar los resultados. Si se requiere ordenar por varias propiedades, este predicado debe agregarse varias veces utilizando el prefijo numérico, como `1_orderby=first`, `2_oderby=second`.

#### Propiedades {#properties-13}

* **`orderby`** - o bien el nombre de la propiedad JCR se indica mediante una @ inicial, por ejemplo `@jcr:lastModified` o `@jcr:content/jcr:title`, u otro predicado de la consulta, por ejemplo `2_property`, sobre el que ordenar
* **`sort`** - orden de dirección, `desc` para descendiente o `asc` para ascendente (predeterminado)
* **`case`** - si está configurado como `ignore` distinguirá entre mayúsculas y minúsculas en la clasificación, lo que significa `a` es anterior `B`; si está vacío o no se tiene en cuenta, la ordenación distingue entre mayúsculas y minúsculas, lo que significa `B` es anterior `a`

## Predicados {#predicates}

### boolproperty {#boolproperty}

Este predicado coincide con las propiedades booleanas de JCR. Solo acepta los valores `true` y `false`. En el caso de `false`, coincidirá si la propiedad tiene el valor `false` o si no existe en absoluto. Esto puede resultar útil para comprobar los indicadores booleanos que solo se establecen cuando están activados.

El `operation` no tiene significado.

Este predicado admite la extracción de facetas y proporciona contenedores para cada `true` o `false` , pero solo para propiedades existentes.

#### Propiedades {#properties}

* **`boolproperty`** - ruta relativa a la propiedad, por ejemplo `myFeatureEnabled` o `jcr:content/myFeatureEnabled`
* **`value`** - valor para comprobar la propiedad, `true` o `false`

### contentfragment {#contentfragment}

Este predicado restringe el resultado a fragmentos de contenido.

* No admite el filtrado.
* No admite la extracción de facetas.

#### Propiedades {#properties-1}

* **`contentfragment`** - Se puede utilizar con cualquier valor para comprobar si hay fragmentos de contenido.

### `dateComparison` {#datecomparison}

Este predicado compara dos propiedades de fecha JCR entre sí. Puede comprobar si son iguales, desiguales, buenos o buenos que o iguales.

Se trata de un predicado de solo filtrado y no puede aprovechar un índice de búsqueda.

#### Propiedades {#properties-2}

* **`property1`** - ruta a la propiedad de primera fecha
* **`property2`** - ruta a la propiedad de segunda fecha
* **`operation`**
   * `=` para coincidencia exacta (predeterminado)
   * `!=` para comparación de desigualdad
   * `>` para `property1` bueno que `property2`
   * `>=` para `property1` bueno que o igual a `property2`

### daterange {#daterange}

Este predicado coincide con las propiedades de fecha de JCR con respecto a un intervalo de fecha y hora. Utiliza el formato ISO8601 para fechas y horas (`YYYY-MM-DDTHH:mm:ss.SSSZ`) y permite también representaciones parciales, como `YYYY-MM-DD`. Alternativamente, la marca de tiempo se puede proporcionar como hora POSIX.

Puede buscar cualquier cosa entre dos marcas de tiempo, cualquier cosa más reciente o anterior que una fecha determinada, y también elegir entre intervalos abiertos e inclusivos.

Admite la extracción de facetas y proporciona contenedores `today`, `this week`, `this month`, `last 3 months`, `this year`, `last year`y `earlier than last year`.

No admite el filtrado.

#### Propiedades {#properties-3}

* **`property`** - ruta relativa a un `DATE` propiedad, por ejemplo `jcr:lastModified`
* **`lowerBound`** - fecha inferior enlazada para comprobar la propiedad, por ejemplo `2014-10-01`
* **`lowerOperation`** - `>` (más reciente) o `>=` (en o más reciente), se aplica a la variable `lowerBound`. El valor predeterminado es `>`
* **`upperBound`** - límite superior para comprobar la propiedad, por ejemplo `2014-10-01T12:15:00`
* **`upperOperation`** - `<` (más antiguo) o `<=` (en o más años), se aplica a la variable `upperBound`. El valor predeterminado es `<`
* **`timeZone`** - ID de la zona horaria que se utilizará cuando no se proporcione como cadena de fecha ISO-8601. El valor predeterminado es la zona horaria predeterminada del sistema.

### excludepaths {#excludepaths}

Este predicado excluye los nodos del resultado donde su ruta coincide con una expresión regular.

Se trata de un predicado de solo filtrado y no puede aprovechar un índice de búsqueda.

No admite la extracción de facetas.

#### Propiedades {#properties-4}

* **`excludepaths`** : la expresión regular coincide con las rutas de resultados, excluyendo las coincidentes del resultado.

### texto completo {#fulltext}

Este predicado busca términos en el índice de texto completo.

No admite el filtrado.

No admite la extracción de facetas.

#### Propiedades {#properties-5}

* **`fulltext`** - los términos de búsqueda de texto completo
* **`relPath`** - la ruta relativa para buscar en la propiedad o subnodo. Esta propiedad es opcional.

### hasPermission {#haspermission}

Este predicado restringe el resultado a elementos en los que la sesión actual tiene el valor especificado [Privilegios JCR.](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

Se trata de un predicado de solo filtrado y no puede aprovechar un índice de búsqueda. No admite la extracción de facetas.

#### Propiedades {#properties-7}

* **`hasPermission`** - privilegios JCR separados por comas que la sesión de usuario actual debe tener ALL para el nodo en cuestión; por ejemplo `jcr:write`, `jcr:modifyAccessControl`

### language {#language}

Este predicado encuentra AEM páginas en un idioma específico. Esto examina tanto la propiedad idioma de la página como la ruta de la página, que a menudo incluye el idioma o la configuración regional en una estructura de sitio de nivel superior.

Se trata de un predicado de solo filtrado y no puede aprovechar un índice de búsqueda.

Admite la extracción de facetas y proporciona contenedores para cada código de idioma único.

#### Propiedades {#properties-8}

* **`language`** - Código de idioma ISO, por ejemplo `de`

### mainasset {#mainasset}

Este predicado comprueba si un nodo es un activo principal de DAM y no un subactivo. Básicamente se trata de todos los nodos que no están dentro de un nodo de subrecursos. Tenga en cuenta que esto no comprueba la existencia de `dam:Asset` tipo de nodo. Para usar este predicado, simplemente configure `mainasset=true` o `mainasset=false`. No hay más propiedades.

Se trata de un predicado de solo filtrado y no puede aprovechar un índice de búsqueda.

Admite la extracción de facetas y proporciona dos bloques para los recursos principales y secundarios.

#### Propiedades {#properties-9}

* **`mainasset`** - booleano, `true` para los activos principales, `false` para subactivos

### memberOf {#memberof}

Este predicado encuentra elementos que son miembros de un [colección de recursos de sling](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

Se trata de un predicado de solo filtrado y no puede aprovechar un índice de búsqueda.

No admite la extracción de facetas.

#### Propiedades {#properties-10}

* **`memberOf`** - ruta de la recopilación de recursos de Sling

### nodename {#nodename}

Este predicado coincide con los nombres de nodos JCR.

Admite la extracción de facetas y proporciona contenedores para cada nombre de nodo único (nombre de archivo).

#### Propiedades {#properties-11}

* **`nodename`** - patrón de nombre de nodo que permite comodines: `*` = cualquier carácter o no, `?` = cualquier char, `[abc]` = solo caracteres entre corchetes

### notexpired {#notexpired}

Este predicado coincide con elementos comprobando si una propiedad de fecha JCR es buena o igual a la hora del servidor actual. Se puede utilizar para activar un `expiresAt` y limite los resultados solo a aquellos que aún no hayan caducado (`notexpired=true`) o que ya han caducado (`notexpired=false`).

No admite el filtrado.

Admite la extracción de facetas del mismo modo que el [`daterange`](#daterange) predicado.

#### Propiedades {#properties-12}

* **`notexpired`** - booleano, `true` para no caducar todavía (fecha futura o igual), `false` caducado (fecha en el pasado) (obligatorio)
* **`property`** - ruta relativa al `DATE` propiedad que se va a comprobar (obligatorio)

### path {#path}

Este predicado busca dentro de una ruta determinada.

No admite la extracción de facetas.

#### Propiedades {#properties-14}

* **`path`** - Define el patrón de ruta.
   * Según el `exact` , coincidirá todo el subárbol (como anexar `//*` en xpath, pero tenga en cuenta que esto no incluye la ruta base) o solo coincide una ruta exacta, que puede incluir caracteres comodín (`*`).
      * El valor predeterminado es `true`

<!---   * If the `self`property is set, the entire subtree including the base node will be searched.--->
* **`exact`** - si `exact` es `true`, la ruta exacta debe coincidir, pero puede contener comodines simples (`*`), que coinciden con los nombres, pero no con `/`; si es `false` (predeterminado) se incluyen todos los descendientes (opcional)
* **`flat`** - busca solo los elementos secundarios directos (como anexar `/*` en xpath (solo se usa si `exact` no es verdadero, opcional)
* **`self`** - busca en el subárbol pero incluye el nodo base dado como ruta (sin comodines).
   * *Nota importante*: Se ha identificado un problema con `self` en la implementación actual de querybuilder y utilizarla en consultas puede no producir resultados de búsqueda correctos. Cambio de la implementación actual de `self` tampoco es factible, ya que podría romper las aplicaciones existentes que dependen de ella. Debido a esto, `self` se ha desaprobado y se recomienda evitar usarla.

### propiedad {#property}

Este predicado coincide con las propiedades JCR y sus valores.

Admite la extracción de facetas y proporciona bloques para cada valor de propiedad único en los resultados.

#### Propiedades {#properties-15}

* **`property`** - ruta relativa a la propiedad, por ejemplo `jcr:title`
* **`value`** - valor para comprobar la propiedad; sigue al tipo de propiedad JCR a las conversiones de cadena
* **`N_value`** - use `1_value`, `2_value`, ... para comprobar si hay varios valores (combinados con `OR` de forma predeterminada, con `AND` if `and=true`)
* **`and`** - se configura como `true` para combinar varios valores (`N_value`) con `AND`
* **`operation`**
   * `equals` para coincidencia exacta (predeterminado)
   * `unequals` para comparación de desigualdad
   * `like` para usar la variable `jcr:like` función xpath (opcional)
   * `not` para que no coincida (por ejemplo, `not(@prop)` en xpath, se ignorará value param)
   * `exists` para la comprobación de existencia
      * `true` la propiedad debe existir
      * `false` es igual que `not` y es el valor predeterminado
* **`depth`** - número de niveles comodín debajo de los cuales puede existir la propiedad/ruta relativa (por ejemplo, `property=size depth=2` comprobará `node/size`, `node/*/size` y `node/*/*/size`)

### rangeproperty {#rangeproperty}

Este predicado coincide con una propiedad JCR respecto a un intervalo. Esto se aplica a propiedades con tipos lineales como `LONG`, `DOUBLE` y `DECIMAL`. Para `DATE` consulte la [`daterange`](#daterange) predicado que ha optimizado la entrada de formato de fecha.

Puede definir un límite inferior, un límite superior o ambos. La operación (por ejemplo, menor o menor que o igual a) también se puede especificar individualmente para los límites inferior y superior.

No admite la extracción de facetas.

#### Propiedades {#properties-16}

* **`property`** - ruta relativa a la propiedad
* **`lowerBound`** - límite inferior para comprobar la propiedad
* **`lowerOperation`** - `>` (predeterminado) o `>=`, se aplica al `lowerValue`
* **`upperBound`** - límite superior para comprobar la propiedad
* **`upperOperation`** - `<` (predeterminado) o `<=`, se aplica al `lowerValue`
* **`decimal`** - `true` si la propiedad marcada es del tipo Decimal

### relativedaterange {#relativedaterange}

Este predicado coincide con `JCR DATE` propiedades frente a un intervalo de fecha y hora utilizando desplazamientos de tiempo relativos a la hora actual del servidor. Puede especificar `lowerBound` y `upperBound` uso de un valor milisegundo o de la sintaxis Bugzilla `1s 2m 3h 4d 5w 6M 7y` (un segundo, dos minutos, tres horas, cuatro días, cinco semanas, seis meses, siete años). Prefijo con `-` para indicar un desplazamiento negativo antes de la hora actual. Si solo especifica `lowerBound` o `upperBound`, el otro tendrá el valor predeterminado `0`, que representan la hora actual.

Por ejemplo:

* `upperBound=1h` (y no `lowerBound`) selecciona cualquier cosa en la hora siguiente
* `lowerBound=-1d` (y no `upperBound`) selecciona cualquier cosa en las últimas 24 horas
* `lowerBound=-6M` y `upperBound=-3M` selecciona cualquier cosa en los últimos 3 a 6 meses
* `lowerBound=-1500` y `upperBound=5500` selecciona cualquier valor entre 1500 milisegundos de antigüedad y 5500 milisegundos en el futuro
* `lowerBound=1d` y `upperBound=2d` selecciona cualquier cosa a partir de mañana

Tenga en cuenta que no toma años bisiestos en consideración y que todos los meses son 30 días.

No admite el filtrado.

Admite la extracción de facetas del mismo modo que el [`daterange`](#daterange) predicado.

#### Propiedades {#properties-17}

* **`upperBound`** - límite de fecha superior en milisegundos o `1s 2m 3h 4d 5w 6M 7y` (un segundo, dos minutos, tres horas, cuatro días, cinco semanas, seis meses, siete años) en relación con el tiempo actual del servidor, utilice `-` para compensación negativa
* **`lowerBound`** - límite de fecha inferior en milisegundos o `1s 2m 3h 4d 5w 6M 7y` (un segundo, dos minutos, tres horas, cuatro días, cinco semanas, seis meses, siete años) en relación con el tiempo actual del servidor, utilice `-` para compensación negativa

### savedquery {#savedquery}

Este predicado incluye todos los predicados de una consulta de Query Builder persistente en la consulta actual como un predicado de subgrupo.

Tenga en cuenta que esto no ejecutará una consulta adicional sino que extenderá la consulta actual.

Las consultas se pueden mantener mediante programación mediante `QueryBuilder#storeQuery()`. El formato puede ser multilínea `String` propiedad o `nt:file` que contiene la consulta como archivo de texto en formato de propiedades de Java.

No admite la extracción de facetas para los predicados de la consulta guardada.

#### Propiedades {#properties-19}

* **`savedquery`** - ruta a la consulta guardada (`String` propiedad o `nt:file` node)

### similar {#similar}

Este predicado es una búsqueda de similitudes usando JCR XPath&#39;s `rep:similar()`.

No admite el filtrado y no admite la extracción de facetas.

#### Propiedades {#properties-20}

* **`similar`** - ruta absoluta al nodo para el que encontrar nodos similares
* **`local`** - una ruta relativa a un nodo descendiente o `.` para el nodo actual (opcional, el valor predeterminado es `.`)

### etiqueta {#tag}

Este predicado busca contenido etiquetado con una o más etiquetas, especificando las rutas de título de las etiquetas.

Admite la extracción de facetas y proporciona bloques para cada etiqueta única, utilizando la ruta de título de etiqueta actual.

#### Propiedades {#properties-21}

* **`tag`** - ruta de título de etiqueta que se va a buscar, por ejemplo `properties:orientation/landscape`
* **`N_value`** - use `1_value`, `2_value`, ... para comprobar si hay varias etiquetas (combinadas con `OR` de forma predeterminada, con `AND` if `and=true`)
* **`property`** - propiedad (o ruta relativa a la propiedad) a ver (valor predeterminado) `cq:tags`)

### tagid {#tagid}

Este predicado busca contenido etiquetado con una o más etiquetas, especificando los ID de las etiquetas.

Admite la extracción de facetas y proporciona bloques para cada etiqueta única, utilizando su ID de etiqueta actual.

#### Propiedades {#properties-22}

* **`tagid`** - ID de etiqueta que se debe buscar, por ejemplo `properties:orientation/landscape`
* **`N_value`** - use `1_value`, `2_value`, ... para comprobar si hay varios ID de etiqueta (combinados con `OR` de forma predeterminada, con `AND` if `and=true`)
* **`property`** - propiedad (o ruta relativa a la propiedad) a ver (valor predeterminado) `cq:tags`)

### tagsearch {#tagsearch}

Este predicado busca contenido etiquetado con una o más etiquetas, especificando palabras clave. Primero buscará las etiquetas que contengan estas palabras clave en sus títulos y luego restringirá el resultado a solo los elementos etiquetados con ellas.

No admite la extracción de facetas.

#### Propiedades {#Properties-1}

* **`tagsearch`** - palabra clave para buscar en títulos de etiquetas
* **`property`** - propiedad (o ruta relativa a la propiedad) que se debe tener en cuenta (predeterminado) `cq:tags`)
* **`lang`** - para buscar solo en un título de etiqueta localizado (por ejemplo, `de`)
* **`all`** - valor booleano para buscar todo el texto completo de la etiqueta, es decir, todos los títulos, descripción, etc. (tiene prioridad sobre `lang`)

### type {#type}

Este predicado restringe los resultados a un tipo de nodo JCR específico, tanto tipos de nodo primario como tipos de mezcla. También se encontrarán subtipos de ese tipo de nodo. Tenga en cuenta que los índices de búsqueda del repositorio deben cubrir los tipos de nodos para una ejecución eficiente.

Admite la extracción de facetas y proporciona contenedores para cada tipo único en los resultados.

#### Propiedades {#Properties-2}

* **`type`** - tipo de nodo o nombre de mezcla para buscar, por ejemplo `cq:Page`
