---
title: Referencia de predicados del generador de consultas
description: Referencia de predicado para la API de Query Builder.
exl-id: 77118ef7-4d29-470d-9c4b-20537a408940
source-git-commit: d361ddc9a50a543cd1d5f260c09920c5a9d6d675
workflow-type: tm+mt
source-wordcount: '2246'
ht-degree: 2%

---

# Referencia de predicados del generador de consultas {#query-builder-predicate-reference}

## General {#general}

### raíz {#root}

El grupo de predicados raíz. Admite todas las funciones de un grupo y permite configurar parámetros de consulta globales.

El nombre &quot;root&quot; nunca se usa en una consulta; está implícito.

#### Propiedades {#properties-18}

* **`p.offset`** : número que indica el inicio de la página de resultados, es decir, cuántos elementos se deben omitir.
* **`p.limit`** : número que indica el tamaño de página.
* **`p.guessTotal`** - recomendado: evite calcular el total del resultado, que puede resultar costoso. Un número que indica el total máximo que se va a contar hasta (por ejemplo, 1000, un número que proporciona a los usuarios suficientes comentarios sobre el tamaño aproximado y los números exactos para obtener resultados más pequeños). O bien, `true` para contar solo hasta el mínimo necesario `p.offset` + `p.limit`.
* **`p.excerpt`** - si se configura como `true`, incluya un extracto de texto completo en el resultado.
* **`p.hits`** : (solo para el servlet JSON) seleccione la forma en que se escriben las visitas como JSON, con estas estándar (ampliables mediante el servicio ResultHitWriter).
   * **`simple`** - elementos mínimos como `path`, `title`, `lastmodified`, `excerpt` (si está configurado).
   * **`full`** - procesamiento JSON de sling del nodo, con `jcr:path` que indica la ruta de la visita. De forma predeterminada, solo enumera las propiedades directas del nodo, incluido un árbol más profundo con `p.nodedepth=N`, donde 0 significa todo el subárbol infinito. Añadir `p.acls=true` para incluir los permisos JCR de la sesión actual en el elemento de resultado dado (asignaciones: `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`).
   * **`selective`** - solo las propiedades especificadas en `p.properties`, que es un espacio separado (use `+` en la lista de direcciones URL) de rutas relativas. Si la ruta relativa tiene una profundidad `>1`, estas propiedades se representan como objetos secundarios. El especial `jcr:path` La propiedad incluye la ruta de la visita.

### grupo  {#group}

Este predicado permite crear condiciones anidadas. Los grupos pueden contener grupos anidados. Todo lo que hay en una consulta del Generador de consultas está implícito en un grupo raíz, que puede tener `p.or` y `p.not` también parámetros de.

A continuación se muestra un ejemplo de cómo hacer coincidir una de las dos propiedades con un valor:

```text
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

Conceptualmente, lo es `(1_property` O `2_property)`.

El siguiente es un ejemplo para grupos anidados:

```text
fulltext=Management
group.p.or=true
group.1_group.path=/content/wknd/ch/de
group.1_group.type=cq:Page
group.2_group.path=/content/dam/wknd
group.2_group.type=dam:Asset
```

Busca el término **Administración** dentro de páginas en `/content/wknd/ch/de` o en recursos en `/content/dam/wknd`.

Conceptualmente, lo es `fulltext AND ( (path AND type) OR (path AND type) )`. Estas uniones OR necesitan buenos índices por motivos de rendimiento.

#### Propiedades {#properties-6}

* **`p.or`** - si se configura como `true`, solo debe coincidir un predicado del grupo. El valor predeterminado es `false`, lo que significa que todos deben coincidir
* **`p.not`** - si se configura como `true`, anula el grupo (el valor predeterminado es `false`)
* **`<predicate>`** - añade predicados anidados
* **`N_<predicate>`** : añade varios predicados anidados al mismo tiempo, como `1_property, 2_property, ...`

### orderby {#orderby}

Este predicado permite ordenar los resultados. Si se requiere ordenar por varias propiedades, este predicado debe agregarse varias veces utilizando el prefijo numérico, como `1_orderby=first`, `2_oderby=second`.

#### Propiedades {#properties-13}

* **`orderby`** : nombre de propiedad JCR indicado por una @ inicial, por ejemplo `@jcr:lastModified` o `@jcr:content/jcr:title`u otro predicado de la consulta, por ejemplo `2_property`, según el orden
* **`sort`** - dirección del orden, ya sea `desc` para descendente o `asc` para ascendente (predeterminado)
* **`case`** - si se configura como `ignore`, no distingue entre mayúsculas y minúsculas, es decir, `a` va antes que `B`; si está vacío o no, la ordenación distingue entre mayúsculas y minúsculas, es decir `B` va antes que `a`

## Predicados {#predicates}

### boolproperty {#boolproperty}

Este predicado coincide con las propiedades booleanas JCR. Solo acepta los valores `true` y `false`. Si el valor es `false`, coincide si la propiedad tiene el valor `false`, o si no existe en absoluto. Este predicado es útil para comprobar indicadores booleanos que solo se establecen cuando está habilitado.

El heredado `operation` parámetro no tiene significado.

Este predicado admite la extracción de facetas y proporciona bloques para cada uno `true` o `false` , pero solo para las propiedades existentes.

#### Propiedades {#properties}

* **`boolproperty`** - ruta relativa a la propiedad, por ejemplo `myFeatureEnabled` o `jcr:content/myFeatureEnabled`
* **`value`** - valor para comprobar la propiedad, `true` o `false`

### contentfragment {#contentfragment}

Este predicado restringe el resultado a fragmentos de contenido.

* No admite el filtrado.
* No admite la extracción de facetas.

#### Propiedades {#properties-1}

* **`contentfragment`** : se puede utilizar con cualquier valor para comprobar fragmentos de contenido.

### `dateComparison` {#datecomparison}

Este predicado compara dos propiedades de fecha JCR entre sí. Puede comprobar si son iguales, desiguales, buenos o buenos que o iguales.

Un predicado solo de filtrado y no puede utilizar un índice de búsqueda.

#### Propiedades {#properties-2}

* **`property1`** - ruta a la primera propiedad de fecha
* **`property2`** - ruta a la segunda propiedad de fecha
* **`operation`**
   * `=` para coincidencia exacta (predeterminado)
   * `!=` para comparación de desigualdad
   * `>` para `property1` bueno que `property2`
   * `>=` para `property1` bueno que o igual a `property2`

### intervalo de fechas {#daterange}

Este predicado compara las propiedades de fecha JCR con un intervalo de fecha y hora. Utiliza el formato ISO8601 para las fechas y horas (`YYYY-MM-DDTHH:mm:ss.SSSZ`) y también permite representaciones parciales, como `YYYY-MM-DD`. Alternativamente, la marca de tiempo se puede proporcionar como hora POSIX.

Puede buscar cualquier cosa entre dos marcas de tiempo, cualquier cosa más reciente o anterior a una fecha determinada, y también elegir entre intervalos inclusivos y abiertos.

Admite la extracción de facetas y proporciona contenedores `today`, `this week`, `this month`, `last 3 months`, `this year`, `last year`, y `earlier than last year`.

No admite el filtrado.

#### Propiedades {#properties-3}

* **`property`** - ruta relativa a un `DATE` propiedad, por ejemplo `jcr:lastModified`
* **`lowerBound`** : límite de fecha inferior para la propiedad check, por ejemplo `2014-10-01`
* **`lowerOperation`** - `>` (más reciente) o `>=` (en o posterior), se aplica al `lowerBound`. El valor predeterminado es `>`
* **`upperBound`** : límite superior para comprobar la propiedad, por ejemplo `2014-10-01T12:15:00`
* **`upperOperation`** - `<` (anterior) o `<=` (en o anteriores), se aplica a `upperBound`. El valor predeterminado es `<`
* **`timeZone`** : ID de la zona horaria que se utilizará cuando no se proporcione como cadena de fecha ISO-8601. El valor predeterminado es la zona horaria predeterminada del sistema.

### excludepaths {#excludepaths}

Este predicado excluye nodos del resultado donde su ruta coincida con una expresión regular.

Un predicado solo de filtrado y no puede utilizar un índice de búsqueda.

No admite la extracción de facetas.

#### Propiedades {#properties-4}

* **`excludepaths`** : expresión regular comparada con las rutas de resultados, excluyendo las coincidentes del resultado.

### texto completo {#fulltext}

Busca términos en el índice de texto completo.

No admite el filtrado.

No admite la extracción de facetas.

#### Propiedades {#properties-5}

* **`fulltext`** - los términos de búsqueda de texto completo
* **`relPath`** : la ruta relativa a la búsqueda en la propiedad o subnodo. Esta propiedad es opcional.

### hasPermission {#haspermission}

Este predicado restringe el resultado a los elementos en los que la sesión actual tiene el especificado [Privilegios JCR.](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

Un predicado solo de filtrado y no puede utilizar un índice de búsqueda. No admite la extracción de facetas.

#### Propiedades {#properties-7}

* **`hasPermission`** - todos los privilegios JCR separados por comas que la sesión de usuario actual debe tener para el nodo en cuestión. Por ejemplo, `jcr:write`, `jcr:modifyAccessControl`

### language {#language}

AEM Este predicado encuentra páginas en un idioma específico para el usuario. Examina tanto la propiedad de idioma de la página como la ruta de página que a menudo incluye el idioma o la configuración regional en una estructura de sitio de nivel superior.

Un predicado solo de filtrado y no puede utilizar un índice de búsqueda.

Admite la extracción de facetas y proporciona bloques para cada código de idioma único.

#### Propiedades {#properties-8}

* **`language`** - Código de idioma ISO, por ejemplo `de`

### recurso principal {#mainasset}

Este predicado comprueba si un nodo es un recurso principal DAM y no un subrecurso. Básicamente son todos los nodos que no están dentro de un nodo de subrecursos. No comprueba la existencia de `dam:Asset` tipo de nodo. Para utilizar este predicado, establezca `mainasset=true` o `mainasset=false`. No hay más propiedades.

Un predicado solo de filtrado y no puede utilizar un índice de búsqueda.

Admite la extracción de facetas y proporciona dos contenedores para recursos principales y secundarios.

#### Propiedades {#properties-9}

* **`mainasset`** - booleano, `true` para los activos principales, `false` para subrecursos

### memberOf {#memberof}

Este predicado encuentra elementos que son miembros de un grupo específico [colección de recursos de sling](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

Un predicado solo de filtrado y no puede utilizar un índice de búsqueda.

No admite la extracción de facetas.

#### Propiedades {#properties-10}

* **`memberOf`** - ruta de la colección de recursos de Sling

### nombre de nodo {#nodename}

Este predicado coincide con los nombres de nodo JCR.

Admite la extracción de facetas y proporciona bloques para cada nombre de nodo único (nombre de archivo).

#### Propiedades {#properties-11}

* **`nodename`** - patrón de nombre de nodo que permite caracteres comodín: `*` = cualquier o ningún carácter, `?` = cualquier carácter, `[abc]` = solo caracteres entre corchetes

### notexpired {#notexpired}

Este predicado coincide con los elementos al comprobar si una propiedad de fecha JCR es buena o igual a la hora actual del servidor. Se puede utilizar para comprobar un `expiresAt` y limita los resultados únicamente a los valores que aún no han caducado (`notexpired=true`) o que ya han caducado (`notexpired=false`).

No admite el filtrado.

Admite la extracción de facetas del mismo modo que la variable [`daterange`](#daterange) predicado.

#### Propiedades {#properties-12}

* **`notexpired`** - booleano, `true` para todavía no caducado (fecha futura o igual), `false` para caducado (fecha en el pasado) (obligatorio)
* **`property`** - ruta relativa a `DATE` propiedad para comprobar (obligatorio)

### path {#path}

Este predicado busca dentro de una ruta determinada.

No admite la extracción de facetas.

#### Propiedades {#properties-14}

* **`path`** : define el patrón de ruta.
   * Según la variable `exact` propiedad, o bien todo el subárbol coincide (como anexar) `//*` en xpath, pero tenga en cuenta que no incluye la ruta base) o que solo coincide una ruta exacta, que puede incluir caracteres comodín (`*`).
      * El valor predeterminado es `true`.
&lt;!— * Si la variable `self`se establece, se busca en todo el subárbol, incluido el nodo base.—>
* **`exact`** - si `exact` es `true`, la ruta exacta debe coincidir, pero puede contener caracteres comodín simples (`*`), que coinciden con los nombres, pero no con `/`; si es `false` (predeterminado) se incluyen todos los descendientes (opcional).
* **`flat`** : busca solo los elementos secundarios directos (como anexar `/*` en xpath) (solo se utiliza si `exact` no es true, opcional).
* **`self`** : busca en el subárbol pero incluye el nodo base dado como ruta (sin comodines).
   * *Nota importante*: Se ha identificado un problema con `self` en la implementación actual del generador de consultas y su uso en consultas puede no producir resultados de búsqueda correctos. Cambiar la implementación actual de `self` tampoco es viable porque podría romper las aplicaciones existentes que dependen de ella. Debido a esta funcionalidad, `self` La propiedad de está en desuso, por lo que se recomienda evitar utilizarla.

### propiedad {#property}

Este predicado coincide con las propiedades JCR y sus valores.

Admite la extracción de facetas y proporciona bloques para cada valor de propiedad único en los resultados.

#### Propiedades {#properties-15}

* **`property`** - ruta relativa a la propiedad, por ejemplo `jcr:title`.
* **`value`** : valor para comprobar la propiedad; sigue el tipo de propiedad JCR a las conversiones de cadena.
* **`N_value`** - uso `1_value`, `2_value`, ... para buscar varios valores (combinados con `OR` de forma predeterminada, con `AND` if `and=true`).
* **`and`** - se establece en `true` para combinar varios valores (`N_value`) con `AND`
* **`operation`**
   * `equals` para la coincidencia exacta (valor predeterminado).
   * `unequals` para comparación de desigualdad.
   * `like` para usar el `jcr:like` función xpath (opcional).
   * `not` para que no haya coincidencia (por ejemplo, `not(@prop)` en xpath, el parámetro value se ignora).
   * `exists` para la comprobación de existencia.
      * `true` la propiedad debe existir.
      * `false` es igual que `not` y es el valor predeterminado.
* **`depth`** : número de niveles comodín por debajo de los cuales puede existir la propiedad o ruta relativa (por ejemplo, `property=size depth=2` cheques `node/size`, `node/*/size`, y `node/*/*/size`).

### rangeProperty {#rangeproperty}

Este predicado compara una propiedad JCR con un intervalo. Se aplica a propiedades con tipos lineales como `LONG`, `DOUBLE`, y `DECIMAL`. Para `DATE`, consulte la [`daterange`](#daterange) predicado que ha optimizado la entrada de formato de fecha.

Puede definir un límite inferior, un límite superior o ambos. La operación (por ejemplo, menor o menor o igual que) también se puede especificar individualmente para los límites inferior y superior.

No admite la extracción de facetas.

#### Propiedades {#properties-16}

* **`property`** - ruta relativa a la propiedad
* **`lowerBound`** - límite inferior para comprobar la propiedad
* **`lowerOperation`** - `>` (predeterminado) o `>=`, se aplica al `lowerValue`
* **`upperBound`** - límite superior de la propiedad check
* **`upperOperation`** - `<` (predeterminado) o `<=`, se aplica al `lowerValue`
* **`decimal`** - `true` si la propiedad activada es de tipo Decimal

### relativedaterange {#relativedaterange}

Este predicado coincide con `JCR DATE` propiedades para un intervalo de fecha y hora con desplazamientos de tiempo respecto a la hora del servidor actual. Puede especificar `lowerBound` y `upperBound` usando un valor de milisegundos o la sintaxis de Bugzilla `1s 2m 3h 4d 5w 6M 7y` (un segundo, dos minutos, tres horas, cuatro días, cinco semanas, seis meses, siete años). Prefijo con `-` para indicar un desplazamiento negativo antes de la hora actual. Si solo especifica `lowerBound` o `upperBound`, el otro toma el valor predeterminado `0`, que representa la hora actual.

Por ejemplo:

* `upperBound=1h` (y no `lowerBound`) selecciona cualquier cosa en la hora siguiente
* `lowerBound=-1d` (y no `upperBound`) selecciona cualquier cosa en las últimas 24 horas
* `lowerBound=-6M` y `upperBound=-3M` selecciona cualquier cosa en los últimos 3 a 6 meses
* `lowerBound=-1500` y `upperBound=5500` selecciona cualquier valor entre 1500 milisegundos y 5500 milisegundos en el futuro
* `lowerBound=1d` y `upperBound=2d` selecciona cualquier cosa pasado mañana

No tiene en cuenta los años bisiestos y todos los meses son 30 días.

No admite el filtrado.

Admite la extracción de facetas del mismo modo que la variable [`daterange`](#daterange) predicado.

#### Propiedades {#properties-17}

* **`upperBound`** - límite superior de fecha en milisegundos o `1s 2m 3h 4d 5w 6M 7y` (un segundo, dos minutos, tres horas, cuatro días, cinco semanas, seis meses, siete años) en relación con el tiempo de servidor actual, use `-` para desplazamiento negativo
* **`lowerBound`** : límite de fecha inferior en milisegundos o `1s 2m 3h 4d 5w 6M 7y` (un segundo, dos minutos, tres horas, cuatro días, cinco semanas, seis meses, siete años) en relación con el tiempo de servidor actual, use `-` para desplazamiento negativo

### savedquery {#savedquery}

Este predicado incluye todos los predicados de una consulta del Generador de consultas persistente en la consulta actual como predicado de subgrupo.

No ejecuta una consulta adicional pero amplía la consulta actual.

Las consultas se pueden mantener mediante programación usando `QueryBuilder#storeQuery()`. El formato puede ser de varias líneas `String` propiedad o un `nt:file` nodo que contiene la consulta como archivo de texto en formato de propiedades Java™.

No admite la extracción de facetas para los predicados de la consulta guardada.

#### Propiedades {#properties-19}

* **`savedquery`** - ruta a la consulta guardada (`String` property o `nt:file` node)

### parecido {#similar}

Este predicado es una búsqueda de similitud que utiliza XPath de JCR `rep:similar()`.

No admite el filtrado y no admite la extracción de facetas.

#### Propiedades {#properties-20}

* **`similar`** - ruta absoluta al nodo para el que se buscarán nodos similares
* **`local`** - una ruta relativa a un nodo descendiente o `.` para el nodo actual (opcional), el valor predeterminado es `.`)

### etiqueta {#tag}

Este predicado busca contenido etiquetado con una o más etiquetas, especificando las rutas de título de las etiquetas.

Admite la extracción de facetas y proporciona bloques para cada etiqueta única, utilizando su ruta de título de etiqueta actual.

#### Propiedades {#properties-21}

* **`tag`** - ruta del título de la etiqueta que se busca, por ejemplo `properties:orientation/landscape`
* **`N_value`** - uso `1_value`, `2_value`, ... para buscar varias etiquetas (combinadas con `OR` de forma predeterminada, con `AND` if `and=true`)
* **`property`** - propiedad (o ruta relativa a la propiedad) que se va a ver (valor predeterminado `cq:tags`)

### tagid {#tagid}

Este predicado busca contenido etiquetado con una o más etiquetas, especificando los ID de etiqueta.

Admite la extracción de facetas y proporciona bloques para cada etiqueta única, utilizando su ID de etiqueta actual.

#### Propiedades {#properties-22}

* **`tagid`** - ID de etiqueta que se busca, por ejemplo `properties:orientation/landscape`
* **`N_value`** - uso `1_value`, `2_value`, ... para comprobar si hay varios ID de etiqueta (combinados con `OR` de forma predeterminada, con `AND` if `and=true`)
* **`property`** - propiedad (o ruta relativa a la propiedad) que se va a ver (valor predeterminado `cq:tags`)

### tagsearch {#tagsearch}

Este predicado busca contenido etiquetado con una o más etiquetas especificando palabras clave. Primero busca las etiquetas que contienen estas palabras clave en sus títulos y luego restringe el resultado a solo los elementos etiquetados con estas palabras clave.

No admite la extracción de facetas.

#### Propiedades {#Properties-1}

* **`tagsearch`** : palabra clave para buscar en títulos de etiquetas
* **`property`** - propiedad (o ruta relativa a la propiedad) a tener en cuenta (predeterminado) `cq:tags`)
* **`lang`** : para buscar solo en un determinado título de etiqueta localizado (por ejemplo, `de`)
* **`all`** : valor booleano para buscar texto completo de etiqueta completo, es decir, todos los títulos, descripciones, etc. (tiene prioridad sobre `lang`)

### tipo {#type}

Este predicado restringe los resultados a un tipo de nodo JCR específico, ambos tipos de nodo principal o `mixin` tipos. También encuentra subtipos de ese tipo de nodo. Los índices de búsqueda del repositorio deben cubrir los tipos de nodo para una ejecución eficiente.

Admite la extracción de facetas y proporciona bloques para cada tipo único en los resultados.

#### Propiedades {#Properties-2}

* **`type`** - tipo de nodo o `mixin` nombre para buscar, por ejemplo `cq:Page`
