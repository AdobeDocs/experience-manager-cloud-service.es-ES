---
title: Referencia de predicado del Generador de consultas
description: Referencia de predicado para la API de Consulta Builder.
translation-type: tm+mt
source-git-commit: 90b635cb31af910e08bdee7925cec0c7beb05318
workflow-type: tm+mt
source-wordcount: '2221'
ht-degree: 1%

---


# Referencia de predicado del Generador de consultas {#query-builder-predicate-reference}

## General {#general}

### raíz {#root}

Este es el grupo de predicados raíz. Admite todas las funciones de un grupo y permite establecer parámetros de consulta globales.

El nombre &quot;root&quot; nunca se usa en una consulta, es implícito.

#### Propiedades {#properties-18}

* **`p.offset`** - número que indica el inicio de la página de resultados, es decir, cuántos elementos se deben omitir
* **`p.limit`** - número que indica el tamaño de la página
* **`p.guessTotal`** - recomendado: evitar el cálculo del total del resultado completo, que puede resultar costoso; ya sea un número que indica el total máximo que se va a contar hasta (por ejemplo, 1000, un número que proporciona a los usuarios suficiente información sobre el tamaño aproximado y los números exactos para obtener resultados más pequeños) o  `true` para contar únicamente hasta el mínimo necesario  `p.offset` +  `p.limit`
* **`p.excerpt`** - si se establece en  `true`, incluya un fragmento de texto completo en el resultado
* **`p.hits`** - (solo para el servlet JSON) seleccione la forma en que se escriben las visitas como JSON, con estas visitas estándar (ampliables mediante el servicio ResultHitWriter):
   * **`simple`** - elementos mínimos como  `path`,  `title`,  `lastmodified`,  `excerpt` (si están configurados)
   * **`full`** - representación JSON sling del nodo, con  `jcr:path` indicación de la ruta de la visita: de forma predeterminada, solo lista las propiedades directas del nodo, incluya un árbol más profundo con  `p.nodedepth=N`, con 0 que significa todo el subárbol infinito; agregue  `p.acls=true` para incluir los permisos de JCR de la sesión actual en el elemento de resultado determinado (asignaciones:  `create` =  `add_node`,  `modify` =  `set_property`,  `delete` =  `remove`)
   * **`selective`** - solo las propiedades especificadas en  `p.properties`, que es una lista de rutas relativas separada por espacios (utilizada  `+` en direcciones URL); si la ruta relativa tiene una profundidad,  `>1` se representarán como objetos secundarios; la  `jcr:path` propiedad especial incluye la ruta de la visita

### grupo {#group}

Este predicado permite crear condiciones anidadas. Los grupos pueden contener grupos anidados. Todo lo que hay en una consulta del Generador de Consultas está implícito en un grupo raíz, que también puede tener `p.or` y `p.not` parámetros.

A continuación se muestra un ejemplo para hacer coincidir una de las dos propiedades con un valor:

```text
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

Conceptualmente es `(1_property` OR `2_property)`.

A continuación se muestra un ejemplo de grupos anidados:

```text
fulltext=Management
group.p.or=true
group.1_group.path=/content/wknd/ch/de
group.1_group.type=cq:Page
group.2_group.path=/content/dam/wknd
group.2_group.type=dam:Asset
```

Esto busca el término **Administración** dentro de las páginas en `/content/wknd/ch/de` o en los recursos en `/content/dam/wknd`.

Conceptualmente es `fulltext AND ( (path AND type) OR (path AND type) )`. Tenga en cuenta que dichas combinaciones O necesitan índices adecuados por motivos de rendimiento.

#### Propiedades {#properties-6}

* **`p.or`** - si se establece en  `true`, solo debe coincidir un predicado del grupo. De forma predeterminada, `false` significa que todos deben coincidir
* **`p.not`** - si se establece en  `true`, anula el grupo (el valor predeterminado es  `false`)
* **`<predicate>`** - agrega predicados anidados
* **`N_<predicate>`** - agrega varios predicados anidados del mismo tiempo, como  `1_property, 2_property, ...`

### orderby {#orderby}

Este predicado permite ordenar los resultados. Si se requiere ordenar por varias propiedades, este predicado debe agregarse varias veces utilizando el prefijo de número, como `1_orderby=first`, `2_oderby=second`.

#### Propiedades {#properties-13}

* **`orderby`** - bien el nombre de la propiedad JCR indicado por un @ inicial, por ejemplo  `@jcr:lastModified` o  `@jcr:content/jcr:title`, o bien otro predicado en la consulta, por ejemplo  `2_property`, en el que se debe ordenar
* **`sort`** - dirección de clasificación, ya sea  `desc` para descendencia o  `asc` para ascendente (predeterminado)
* **`case`** - si se establece en  `ignore` hará que la clasificación no distinga entre mayúsculas y minúsculas, lo que significa que  `a` viene antes  `B`; si está vacío o no está disponible, la clasificación distingue entre mayúsculas y minúsculas, lo que significa que  `B` se muestra antes  `a`

## Predicados {#predicates}

### boolproperty {#boolproperty}

Este predicado coincide con las propiedades booleanas de JCR. Sólo acepta los valores `true` y `false`. En el caso de `false`, coincidirá si la propiedad tiene el valor `false` o si no existe en absoluto. Esto puede resultar útil para comprobar si hay indicadores booleanos que solo se establecen cuando están activados.

El parámetro heredado `operation` no tiene significado.

Este predicado admite la extracción de facetas y proporciona bloques para cada valor `true` o `false`, pero sólo para las propiedades existentes.

#### Propiedades {#properties}

* **`boolproperty`** - ruta relativa a la propiedad, por ejemplo  `myFeatureEnabled` o  `jcr:content/myFeatureEnabled`
* **`value`** - valor para comprobar la propiedad  `true` o  `false`

### contentfragment {#contentfragment}

Este predicado restringe el resultado a los fragmentos de contenido.

* No admite el filtrado.
* No admite la extracción de facetas.

#### Propiedades {#properties-1}

* **`contentfragment`** - Se puede utilizar con cualquier valor para buscar fragmentos de contenido.

### `dateComparison` {#datecomparison}

Este predicado compara dos propiedades de fecha JCR entre sí. Puede probar si son iguales, desiguales, buenos o buenos que o iguales.

Se trata de un predicado de solo filtrado y no puede aprovechar un índice de búsqueda.

#### Propiedades {#properties-2}

* **`property1`** - ruta a la propiedad de la primera fecha
* **`property2`** - ruta a la propiedad de segunda fecha
* **`operation`**
   * `=` para coincidencia exacta (predeterminado)
   * `!=` para la comparación de desigualdad
   * `>` para  `property1` buenos  `property2`
   * `>=` para  `property1` buenos o iguales a  `property2`

### daterange {#daterange}

Este predicado coincide con las propiedades de fecha de JCR con un intervalo de fecha y hora. Utiliza la norma ISO8601
para fechas y horas (`YYYY-MM-DDTHH:mm:ss.SSSZ`) y permite también representaciones parciales, como `YYYY-MM-DD`. Como alternativa, la marca de tiempo se puede proporcionar como hora POSIX.

Puede buscar cualquier cosa entre dos marcas de hora, cualquier cosa nueva o anterior a una fecha determinada, y también elegir entre intervalos abiertos e inclusivos.

Soporta extracción de facetas y proporciona bloques `today`, `this week`, `this month`, `last 3 months`, `this year`, `last year` y `earlier than last year`.

No admite el filtrado.

#### Propiedades {#properties-3}

* **`property`** - ruta relativa a una  `DATE` propiedad, por ejemplo  `jcr:lastModified`
* **`lowerBound`** - límite de fecha inferior para la propiedad check, por ejemplo  `2014-10-01`
* **`lowerOperation`** -  `>` (más reciente) o  `>=` (en o más reciente), se aplica a la  `lowerBound`. El valor predeterminado es `>`
* **`upperBound`** - límite superior para la propiedad check, por ejemplo  `2014-10-01T12:15:00`
* **`upperOperation`** -  `<` (mayor) o  `<=` (mayor o menor), se aplica al  `upperBound`. El valor predeterminado es `<`
* **`timeZone`** - ID de huso horario que se utilizará cuando no se proporcione como una cadena de fecha ISO-8601. El valor predeterminado es la zona horaria predeterminada del sistema.

### excludepaths {#excludepaths}

Este predicado excluye los nodos del resultado donde su ruta coincide con una expresión normal.

Se trata de un predicado de solo filtrado y no puede aprovechar un índice de búsqueda.

No admite la extracción de facetas.

#### Propiedades {#properties-4}

* **`excludepaths`** - expresión regular comparada con rutas de resultados, excluyendo las coincidentes del resultado.

### texto completo {#fulltext}

Este predicado busca términos en el índice de texto completo.

No admite el filtrado.

No admite la extracción de facetas.

#### Propiedades {#properties-5}

* **`fulltext`** - los términos de búsqueda de texto completo
* **`relPath`** - la ruta relativa para buscar en la propiedad o subnodo. Esta propiedad es opcional.

### hasPermission {#haspermission}

Este predicado restringe el resultado a elementos en los que la sesión actual tiene los [privilegios JCR especificados.](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

Se trata de un predicado de solo filtrado y no puede aprovechar un índice de búsqueda. No admite la extracción de facetas.

#### Propiedades {#properties-7}

* **`hasPermission`** - privilegios JCR separados por comas que TODOS los usuarios deben tener en la sesión de usuario actual para el nodo en cuestión; por ejemplo  `jcr:write`,  `jcr:modifyAccessControl`

### language {#language}

Este predicado encuentra AEM páginas en un idioma específico. Esto observa tanto la propiedad de idioma de la página como la ruta de la página, que generalmente incluye el idioma o la configuración regional en una estructura de sitio de nivel superior.

Se trata de un predicado de solo filtrado y no puede aprovechar un índice de búsqueda.

Es compatible con la extracción de facetas y proporciona bloques para cada código de idioma único.

#### Propiedades {#properties-8}

* **`language`** - Código de idioma ISO, por ejemplo  `de`

### mainasset {#mainasset}

Este predicado comprueba si un nodo es un recurso principal DAM y no un subrecurso. Básicamente, son todos los nodos que no están dentro de un nodo de subrecursos. Tenga en cuenta que esto no comprueba el tipo de nodo `dam:Asset`. Para usar este predicado, simplemente configure `mainasset=true` o `mainasset=false`. No hay más propiedades.

Se trata de un predicado de solo filtrado y no puede aprovechar un índice de búsqueda.

Es compatible con la extracción de facetas y proporciona dos bloques para los recursos principales y secundarios.

#### Propiedades {#properties-9}

* **`mainasset`** - booleano,  `true` para recursos principales,  `false` para subrecursos

### miembroDe {#memberof}

Este predicado encuentra elementos que son miembros de una [colección de recursos sling](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/resource/collection/ResourceCollection.html) específica.

Se trata de un predicado de solo filtrado y no puede aprovechar un índice de búsqueda.

No admite la extracción de facetas.

#### Propiedades {#properties-10}

* **`memberOf`** - ruta de la colección de recursos de Sling

### nodename {#nodename}

Este predicado coincide con los nombres de nodo JCR.

Es compatible con la extracción de facetas y proporciona bloques para cada nombre de nodo único (nombre de archivo).

#### Propiedades {#properties-11}

* **`nodename`** - patrón de nombre de nodo que permite caracteres comodín:  `*` = cualquier carácter o no,  `?` = cualquier carácter,  `[abc]` = sólo caracteres entre corchetes

### notexpired {#notexpired}

Este predicado coincide con elementos comprobando si una propiedad de fecha JCR es buena o igual a la hora del servidor actual. Esto se puede usar para comprobar un valor `expiresAt` y limitar los resultados sólo a aquellos que aún no han caducado (`notexpired=true`) o que ya han caducado (`notexpired=false`).

No admite el filtrado.

Soporta la extracción de facetas de la misma manera que el predicado [`daterange`](#daterange).

#### Propiedades {#properties-12}

* **`notexpired`** - booleano,  `true` para no caducar aún (fecha futura o igual),  `false` para caducar (fecha anterior) (obligatorio)
* **`property`** - ruta relativa a la  `DATE` propiedad que se va a comprobar (requerido)

### path {#path}

Este predicado busca dentro de una ruta determinada.

No admite la extracción de facetas.

#### Propiedades {#properties-14}

* **`path`** - Define el patrón de ruta.
   * Según la propiedad `exact`, el subárbol completo coincidirá (como anexar `//*` en xpath, pero tenga en cuenta que esto no incluye la ruta de acceso base) o sólo coincidirá una ruta exacta, que puede incluir caracteres comodín (`*`).
      * El valor predeterminado es `true`
   * Si se establece la propiedad `self`, se buscará en todo el subárbol, incluido el nodo base.
* **`exact`** - si  `exact` lo es  `true`, la ruta exacta debe coincidir, pero puede contener caracteres comodín simples (`*`), que coincidan con nombres, pero no  `/`; si es  `false` (predeterminado), se incluyen todos los descendientes (opcional)
* **`flat`** - busca únicamente los elementos secundarios directos (como anexar  `/*` en xpath) (solo se utiliza si no  `exact` es verdadero, opcional)
* **`self`** - busca en el subárbol pero incluye el nodo base proporcionado como ruta (sin comodines)

### propiedad {#property}

Este predicado coincide con las propiedades JCR y sus valores.

Admite la extracción de facetas y proporciona bloques para cada valor de propiedad único en los resultados.

#### Propiedades {#properties-15}

* **`property`** - ruta relativa a la propiedad, por ejemplo  `jcr:title`
* **`value`** - valor para comprobar la propiedad; sigue el tipo de propiedad JCR a las conversiones de cadena
* **`N_value`** - usar  `1_value`,  `2_value`, ... para comprobar si hay varios valores (combinados  `OR` de forma predeterminada, con  `AND` if  `and=true`)
* **`and`** - definido como  `true` para combinar varios valores (`N_value`) con  `AND`
* **`operation`**
   * `equals` para coincidencia exacta (predeterminado)
   * `unequals` para la comparación de desigualdad
   * `like` para utilizar la función  `jcr:like` xpath (opcional)
   * `not` para no coincidir (por ejemplo,  `not(@prop)` en xpath, se omitirá el parámetro value)
   * `exists` para comprobación de existencia
      * `true` la propiedad debe existir
      * `false` es el mismo que  `not` y es el valor predeterminado
* **`depth`** - número de niveles comodín debajo de los cuales puede existir la propiedad/ruta relativa (por ejemplo,  `property=size depth=2` comprobará  `node/size`,  `node/*/size` y  `node/*/*/size`)

### rangeproperty {#rangeproperty}

Este predicado hace coincidir una propiedad JCR con un intervalo. Esto se aplica a propiedades con tipos lineales como `LONG`, `DOUBLE` y `DECIMAL`. Para `DATE` consulte el predicado [`daterange`](#daterange) que ha optimizado la entrada de formato de fecha.

Puede definir un límite inferior, un límite superior o ambos. La operación (por ejemplo, menor o menor que o igual que) también se puede especificar para los límites inferior y superior individualmente.

No admite la extracción de facetas.

#### Propiedades {#properties-16}

* **`property`** - ruta relativa a la propiedad
* **`lowerBound`** - límite inferior para la propiedad check
* **`lowerOperation`** -  `>` (predeterminado) o  `>=`, se aplica a la variable  `lowerValue`
* **`upperBound`** - límite superior para la propiedad check
* **`upperOperation`** -  `<` (predeterminado) o  `<=`, se aplica a la variable  `lowerValue`
* **`decimal`** -  `true` si la propiedad marcada es del tipo Decimal

### relativedaterange {#relativedaterange}

Este predicado hace coincidir `JCR DATE` propiedades con un intervalo de fecha y hora utilizando desplazamientos de tiempo en relación con la hora del servidor actual. Puede especificar `lowerBound` y `upperBound` utilizando un valor de milisegundos o la sintaxis de Bugzilla `1s 2m 3h 4d 5w 6M 7y` (un segundo, dos minutos, tres horas, cuatro días, cinco semanas, seis meses, siete años). Prefijo con `-` para indicar un desplazamiento negativo antes de la hora actual. Si sólo especifica `lowerBound` o `upperBound`, el otro valor predeterminado será `0`, lo que representa la hora actual.

Por ejemplo:

* `upperBound=1h` (y no  `lowerBound`) selecciona nada en la hora siguiente
* `lowerBound=-1d` (y no  `upperBound`) selecciona nada en las últimas 24 horas
* `lowerBound=-6M` y  `upperBound=-3M` selecciona cualquier cosa en los últimos 3 a 6 meses
* `lowerBound=-1500` y  `upperBound=5500` selecciona cualquier cosa entre 1500 milisegundos de antigüedad y 5500 milisegundos en el futuro
* `lowerBound=1d` y  `upperBound=2d` selecciona cualquier cosa pasado mañana

Tenga en cuenta que no toma en cuenta los años bisiestos y que todos los meses son 30 días.

No admite el filtrado.

Soporta la extracción de facetas de la misma manera que el predicado [`daterange`](#daterange).

#### Propiedades {#properties-17}

* **`upperBound`** - fecha superior enlazada en milisegundos o  `1s 2m 3h 4d 5w 6M 7y` (un segundo, dos minutos, tres horas, cuatro días, cinco semanas, seis meses, siete años) en relación con el tiempo actual del servidor, usar  `-` para compensación negativa
* **`lowerBound`** - fecha límite inferior en milisegundos o  `1s 2m 3h 4d 5w 6M 7y` (un segundo, dos minutos, tres horas, cuatro días, cinco semanas, seis meses, siete años) en relación con el tiempo actual del servidor, utilizar  `-` para compensación negativa

### savedquery {#savedquery}

Este predicado incluye todos los predicados de una consulta persistente del Generador de Consultas en la consulta actual como predicado de subgrupos.

Tenga en cuenta que esto no ejecutará una consulta adicional sino que extenderá la consulta actual.

Las consultas pueden persistir mediante programación mediante `QueryBuilder#storeQuery()`. El formato puede ser una propiedad multilínea `String` o un nodo `nt:file` que contenga la consulta como archivo de texto en formato de propiedades Java.

No admite la extracción de facetas para los predicados de la consulta guardada.

#### Propiedades {#properties-19}

* **`savedquery`** - ruta a la consulta guardada (`String` propiedad o  `nt:file` nodo)

### similar {#similar}

Este predicado es una búsqueda de similitudes que utiliza `rep:similar()` de JCR XPath.

No admite el filtrado y no admite la extracción de facetas.

#### Propiedades {#properties-20}

* **`similar`** - ruta absoluta al nodo para el cual encontrar nodos similares
* **`local`** - una ruta relativa a un nodo descendiente o  `.` para el nodo actual (opcional, el valor predeterminado es  `.`)

### tag {#tag}

Este predicado busca contenido etiquetado con una o varias etiquetas, especificando las rutas de título de etiqueta.

Es compatible con la extracción de facetas y proporciona bloques para cada etiqueta única, utilizando su ruta de título de etiqueta actual.

#### Propiedades {#properties-21}

* **`tag`** - ruta de título de etiqueta que se va a buscar, por ejemplo  `properties:orientation/landscape`
* **`N_value`** - usar  `1_value`,  `2_value`, ... para buscar varias etiquetas (combinadas  `OR` de forma predeterminada, con  `AND` if  `and=true`)
* **`property`** - propiedad (o ruta de acceso relativa a la propiedad) a la que mirar (predeterminado  `cq:tags`)

### tagid {#tagid}

Este predicado busca contenido etiquetado con una o varias etiquetas, especificando los ID de las etiquetas.

Es compatible con la extracción de facetas y proporciona bloques para cada etiqueta única, utilizando su ID de etiqueta actual.

#### Propiedades {#properties-22}

* **`tagid`** - ID de etiqueta que buscar, por ejemplo  `properties:orientation/landscape`
* **`N_value`** - usar  `1_value`,  `2_value`, ... para comprobar si hay varios ID de etiquetas (combinados  `OR` de forma predeterminada, con  `AND` if  `and=true`)
* **`property`** - propiedad (o ruta de acceso relativa a la propiedad) a la que mirar (predeterminado  `cq:tags`)

### tagsearch {#tagsearch}

Este predicado busca contenido etiquetado con una o varias etiquetas, especificando palabras clave. Primero buscará las etiquetas que contengan estas palabras clave en sus títulos y luego restringirá el resultado a sólo los elementos etiquetados con ellas.

No admite la extracción de facetas.

#### Propiedades {#Properties-1}

* **`tagsearch`** - palabra clave para buscar en títulos de etiquetas
* **`property`** - propiedad (o ruta relativa a la propiedad) que se debe considerar (predeterminado  `cq:tags`)
* **`lang`** - para buscar únicamente en un título de etiqueta localizado (p. ej.  `de`)
* **`all`** - valor booleano para buscar texto completo de etiqueta, es decir, todos los títulos, descripción, etc. (tiene prioridad sobre `lang`)

### tipo {#type}

Este predicado restringe los resultados a un tipo de nodo JCR específico, tanto tipos de nodo principal como tipos de mezcla. También se encontrarán subtipos de ese tipo de nodo. Tenga en cuenta que los índices de búsqueda del repositorio deben cubrir los tipos de nodos para una ejecución eficaz.

Es compatible con la extracción de facetas y proporciona bloques para cada tipo único en los resultados.

#### Propiedades {#Properties-2}

* **`type`** - tipo de nodo o nombre de mezcla para buscar, por ejemplo  `cq:Page`
