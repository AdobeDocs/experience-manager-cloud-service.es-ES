---
title: Referencia de predicados del generador de consultas
description: Referencia de predicado para la API de Query Builder en AEM as a Cloud Service.
exl-id: 77118ef7-4d29-470d-9c4b-20537a408940
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2270'
ht-degree: 1%

---

# Referencia de predicados del generador de consultas {#query-builder-predicate-reference}

## General {#general}

### raíz {#root}

El grupo de predicados raíz. Admite todas las funciones de un grupo y permite configurar parámetros de consulta globales.

El nombre &quot;root&quot; nunca se usa en una consulta; está implícito.

#### Propiedades {#properties-18}

* **`p.offset`**: número que indica el inicio de la página de resultados; es decir, cuántos elementos se omitirán.
* **`p.limit`**: número que indica el tamaño de página.
* **`p.guessTotal`** - recomendado: evite calcular el total del resultado completo, que puede resultar costoso. Un número que indica el total máximo que se va a contar hasta (por ejemplo, 1000, un número que proporciona a los usuarios comentarios suficientes sobre el tamaño aproximado y los números exactos para obtener resultados más pequeños). O bien, `true` para contar solamente hasta el mínimo necesario `p.offset` + `p.limit`.
* **`p.excerpt`** - si se establece en `true`, incluya un extracto de texto completo en el resultado.
* **`p.indexTag`**: si se establece, incluirá una opción de etiqueta de índice en la consulta (consulte [Etiqueta de índice de opciones de consulta](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#query-option-index-tag)).
* **`p.facetStrategy`**: si se establece en `oak`, Query Builder delegará la extracción de facetas a Oak (consulte [Facetas](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#facets)).
* **`p.hits`**: (solo para el servlet JSON) seleccione la forma en que se escriben las visitas como JSON, con estas estándar (ampliables mediante el servicio ResultHitWriter).
   * **`simple`** - elementos mínimos como `path`, `title`, `lastmodified`, `excerpt` (si están establecidos).
   * **`full`** - procesamiento JSON de sling del nodo, con `jcr:path` indicando la ruta de la visita. De forma predeterminada, solo enumera las propiedades directas del nodo, incluido un árbol más profundo con `p.nodedepth=N`, donde 0 significa todo el subárbol infinito. Agregue `p.acls=true` para incluir los permisos JCR de la sesión actual en el elemento de resultado dado (asignaciones: `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`).
   * **`selective`**: solo las propiedades especificadas en `p.properties`, que es una lista de rutas relativas separada por espacios (utilice `+` en las direcciones URL). Si la ruta de acceso relativa tiene una profundidad `>1`, estas propiedades se representan como objetos secundarios. La propiedad especial `jcr:path` incluye la ruta de la visita.

### grupo {#group}

Este predicado permite crear condiciones anidadas. Los grupos pueden contener grupos anidados. Todo en una consulta de Query Builder está implícito en un grupo raíz, que también puede tener `p.or` y `p.not` parámetros.

A continuación se muestra un ejemplo de cómo hacer coincidir una de las dos propiedades con un valor:

```text
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

Conceptualmente, es `(1_property` O `2_property)`.

El siguiente es un ejemplo para grupos anidados:

```text
fulltext=Management
group.p.or=true
group.1_group.path=/content/wknd/ch/de
group.1_group.type=cq:Page
group.2_group.path=/content/dam/wknd
group.2_group.type=dam:Asset
```

Busca el término **Administración** en las páginas de `/content/wknd/ch/de` o en los recursos de `/content/dam/wknd`.

Conceptualmente, es `fulltext AND ( (path AND type) OR (path AND type) )`. Estas uniones OR necesitan buenos índices por motivos de rendimiento.

#### Propiedades {#properties-6}

* **`p.or`** - si se establece en `true`, solo debe coincidir un predicado del grupo. El valor predeterminado es `false`, lo que significa que todos deben coincidir
* **`p.not`** - si se establece en `true`, anula el grupo (el valor predeterminado es `false`)
* **`<predicate>`** - agrega predicados anidados
* **`N_<predicate>`** - agrega varios predicados anidados al mismo tiempo, como `1_property, 2_property, ...`

### orderby {#orderby}

Este predicado permite ordenar los resultados. Si se requiere ordenar por varias propiedades, este predicado debe agregarse varias veces utilizando el prefijo numérico, como `1_orderby=first`, `2_oderby=second`.

#### Propiedades {#properties-13}

* **`orderby`**: bien el nombre de propiedad JCR indicado por una @ inicial, por ejemplo, `@jcr:lastModified` o `@jcr:content/jcr:title`, o bien otro predicado de la consulta, por ejemplo, `2_property`, en el que ordenar
* **`sort`** - dirección de ordenación, ya sea `desc` para descendente o `asc` para ascendente (predeterminado)
* **`case`**: si se establece en `ignore`, la ordenación no distingue entre mayúsculas y minúsculas, lo que significa que `a` va antes que `B`; si está vacía o se omite, la ordenación distingue entre mayúsculas y minúsculas, lo que significa que `B` va antes que `a`

## Predicados {#predicates}

### boolproperty {#boolproperty}

Este predicado coincide con las propiedades booleanas JCR. Solo acepta los valores `true` y `false`. Si el valor es `false`, coincide si la propiedad tiene el valor `false` o si no existe. Este predicado es útil para comprobar indicadores booleanos que solo se establecen cuando está habilitado.

El parámetro `operation` heredado no tiene significado.

Este predicado admite la extracción de facetas y proporciona contenedores para cada valor `true` o `false`, pero solo para las propiedades existentes.

#### Propiedades {#properties}

* **`boolproperty`** - ruta relativa a la propiedad, por ejemplo, `myFeatureEnabled` o `jcr:content/myFeatureEnabled`
* **`value`** - valor para comprobar la propiedad de, `true` o `false`

### contentfragment {#contentfragment}

Este predicado restringe el resultado a fragmentos de contenido.

* No admite el filtrado.
* No admite la extracción de facetas.

#### Propiedades {#properties-1}

* **`contentfragment`**: se puede usar con cualquier valor para buscar fragmentos de contenido.

### `dateComparison` {#datecomparison}

Este predicado compara dos propiedades de fecha JCR entre sí. Puede comprobar si son iguales, desiguales, mayores o mayores que o iguales.

Un predicado solo de filtrado y no puede utilizar un índice de búsqueda.

#### Propiedades {#properties-2}

* **`property1`** - ruta a la primera propiedad de fecha
* **`property2`** - ruta a la segunda propiedad de fecha
* **`operation`**
   * `=` para coincidencia exacta (predeterminado)
   * `!=` para comparación de desigualdad
   * `>` para `property1` mayor que `property2`
   * `>=` para `property1` mayor o igual que `property2`

### intervalo de fechas {#daterange}

Este predicado compara las propiedades de fecha JCR con un intervalo de fecha y hora. Utiliza el ISO8601
formato para fechas y horas (`YYYY-MM-DDTHH:mm:ss.SSSZ`) y también permite representaciones parciales, como `YYYY-MM-DD`. Alternativamente, la marca de tiempo se puede proporcionar como hora POSIX.

Puede buscar cualquier cosa entre dos marcas de tiempo, cualquier cosa más reciente o anterior a una fecha determinada, y también elegir entre intervalos inclusivos y abiertos.

Admite la extracción de facetas y proporciona los contenedores `today`, `this week`, `this month`, `last 3 months`, `this year`, `last year` y `earlier than last year`.

No admite el filtrado.

#### Propiedades {#properties-3}

* **`property`** - ruta relativa a una propiedad `DATE`, por ejemplo, `jcr:lastModified`
* **`lowerBound`** - límite de fecha inferior para comprobar la propiedad, por ejemplo, `2014-10-01`
* **`lowerOperation`** - `>` (más reciente) o `>=` (en o más reciente), se aplica a `lowerBound`. El valor predeterminado es `>`
* **`upperBound`** - límite superior para comprobar la propiedad de, por ejemplo, `2014-10-01T12:15:00`
* **`upperOperation`** - `<` (mayor) o `<=` (mayor o igual que antes), se aplica a `upperBound`. El valor predeterminado es `<`
* **`timeZone`**: ID de zona horaria que se utilizará cuando no se proporcione como cadena de fecha ISO-8601. El valor predeterminado es la zona horaria predeterminada del sistema.

### excludepaths {#excludepaths}

Este predicado excluye nodos del resultado donde su ruta coincida con una expresión regular.

Un predicado solo de filtrado y no puede utilizar un índice de búsqueda.

No admite la extracción de facetas.

#### Propiedades {#properties-4}

* **`excludepaths`**: expresión regular comparada con rutas de resultados, excluyendo las coincidentes del resultado.

### texto completo {#fulltext}

Busca términos en el índice de texto completo.

No admite el filtrado.

No admite la extracción de facetas.

#### Propiedades {#properties-5}

* **`fulltext`** - términos de búsqueda de texto completo
* **`relPath`**: ruta relativa a la búsqueda en la propiedad o subnodo. Esta propiedad es opcional.

### hasPermission {#haspermission}

Este predicado restringe el resultado a los elementos en los que la sesión actual tiene los [privilegios JCR](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges) especificados.

Un predicado solo de filtrado y no puede utilizar un índice de búsqueda. No admite la extracción de facetas.

#### Propiedades {#properties-7}

* **`hasPermission`**: todos los privilegios JCR separados por comas que debe tener la sesión de usuario actual para el nodo en cuestión. Por ejemplo, `jcr:write`, `jcr:modifyAccessControl`

### language {#language}

Este predicado encuentra páginas de AEM en un idioma específico. Examina tanto la propiedad de idioma de la página como la ruta de página que a menudo incluye el idioma o la configuración regional en una estructura de sitio de nivel superior.

Un predicado solo de filtrado y no puede utilizar un índice de búsqueda.

Admite la extracción de facetas y proporciona bloques para cada código de idioma único.

#### Propiedades {#properties-8}

* **`language`** - código de idioma ISO, por ejemplo, `de`

### recurso principal {#mainasset}

Este predicado comprueba si un nodo es un recurso principal DAM y no un subrecurso. Básicamente son todos los nodos que no están dentro de un nodo de subrecursos. No comprueba el tipo de nodo `dam:Asset`. Para usar este predicado, establezca `mainasset=true` o `mainasset=false`. No hay más propiedades.

Un predicado solo de filtrado y no puede utilizar un índice de búsqueda.

Admite la extracción de facetas y proporciona dos contenedores para recursos principales y secundarios.

#### Propiedades {#properties-9}

* **`mainasset`** - booleano, `true` para recursos principales, `false` para subrecursos

### memberOf {#memberof}

Este predicado encuentra elementos que son miembros de una [colección de recursos sling](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/resource/collection/ResourceCollection.html) específica.

Un predicado solo de filtrado y no puede utilizar un índice de búsqueda.

No admite la extracción de facetas.

#### Propiedades {#properties-10}

* **`memberOf`** - ruta de la colección de recursos de Sling

### nombre de nodo {#nodename}

Este predicado coincide con los nombres de nodo JCR.

Admite la extracción de facetas y proporciona bloques para cada nombre de nodo único (nombre de archivo).

#### Propiedades {#properties-11}

* **`nodename`** - patrón de nombre de nodo que permite caracteres comodín: `*` = cualquiera o ningún carácter, `?` = cualquier carácter, `[abc]` = solo caracteres entre corchetes

### notexpired {#notexpired}

Este predicado coincide con los elementos al comprobar si una propiedad de fecha JCR es mayor o igual que la hora actual del servidor. Se puede usar para comprobar un valor `expiresAt` y limitar los resultados únicamente a los valores que aún no han caducado (`notexpired=true`) o que ya han caducado (`notexpired=false`).

No admite el filtrado.

Admite la extracción de facetas del mismo modo que el predicado [`daterange`](#daterange).

#### Propiedades {#properties-12}

* **`notexpired`** - booleano, `true` para no caducado aún (fecha futura o igual), `false` para caducado (fecha pasada) (obligatorio)
* **`property`** - ruta relativa a la propiedad `DATE` que se va a comprobar (obligatorio)

### path {#path}

Este predicado busca dentro de una ruta determinada.

No admite la extracción de facetas.

#### Propiedades {#properties-14}

* **`path`**: define el patrón de ruta de acceso.
   * Según la propiedad `exact`, todo el subárbol coincide (como anexar `//*` en xpath, pero tenga en cuenta que no incluye la ruta de acceso base) o solo coincide una ruta de acceso exacta, que puede incluir caracteres comodín (`*`).
      * El valor predeterminado es `true`.
&lt;!—   * Si se establece la propiedad `self`, se buscará todo el subárbol, incluido el nodo base.—>
* **`exact`** - si `exact` es `true`, la ruta de acceso exacta debe coincidir, pero puede contener caracteres comodín simples (`*`), que coinciden con los nombres, pero no con `/`; si es `false` (predeterminado), se incluyen todos los descendientes (opcional).
* **`flat`**: busca solo los elementos secundarios directos (como anexar `/*` en xpath) (solo se usa si `exact` no es true, opcional).
* **`self`** - busca en el subárbol pero incluye el nodo base dado como ruta (sin comodines).
   * *Nota importante*: se ha identificado un problema con la propiedad `self` en la implementación actual del generador de consultas y es posible que su uso en consultas no produzca los resultados de búsqueda correctos. Tampoco es factible cambiar la implementación actual de la propiedad `self` porque podría romper las aplicaciones existentes que dependen de ella. Debido a esta funcionalidad, la propiedad `self` ya no se utiliza; se recomienda evitar usarla.

### propiedad {#property}

Este predicado coincide con las propiedades JCR y sus valores.

Admite la extracción de facetas y proporciona bloques para cada valor de propiedad único en los resultados.

#### Propiedades {#properties-15}

* **`property`** - ruta relativa a la propiedad, por ejemplo, `jcr:title`.
* **`value`**: valor para comprobar la propiedad; sigue el tipo de propiedad JCR a las conversiones de cadena.
* **`N_value`** - usar `1_value`, `2_value`, ... para buscar varios valores (combinado con `OR` de forma predeterminada, con `AND` si `and=true`).
* **`and`** - establecido en `true` para combinar varios valores (`N_value`) con `AND`
* **`operation`**
   * `equals` para la coincidencia exacta (predeterminado).
   * `unequals` para comparación de desigualdad.
   * `like` por usar la función xpath `jcr:like` (opcional).
   * `not` para los que no coinciden (por ejemplo, `not(@prop)` en xpath, se omite el parámetro value).
   * `exists` para la comprobación de existencia.
      * `true`: la propiedad debe existir.
      * `false` es el mismo que `not` y es el valor predeterminado.
* **`depth`**: número de niveles de comodín por debajo de los cuales puede existir la propiedad o ruta de acceso relativa (por ejemplo, `property=size depth=2` comprobaciones `node/size`, `node/*/size` y `node/*/*/size`).

### rangeProperty {#rangeproperty}

Este predicado compara una propiedad JCR con un intervalo. Se aplica a propiedades con tipos lineales como `LONG`, `DOUBLE` y `DECIMAL`. Para `DATE`, consulte el predicado [`daterange`](#daterange) que ha optimizado la entrada de formato de fecha.

Puede definir un límite inferior, un límite superior o ambos. La operación (por ejemplo, menor o menor o igual que) también se puede especificar individualmente para los límites inferior y superior.

No admite la extracción de facetas.

#### Propiedades {#properties-16}

* **`property`** - ruta relativa a la propiedad
* **`lowerBound`** - límite inferior de la propiedad check
* **`lowerOperation`** - `>` (predeterminado) o `>=`, se aplica a `lowerValue`
* **`upperBound`** - límite superior de la propiedad check
* **`upperOperation`** - `<` (predeterminado) o `<=`, se aplica a `lowerValue`
* **`decimal`** - `true` si la propiedad comprobada es de tipo Decimal

### relativedaterange {#relativedaterange}

Este predicado compara las propiedades `JCR DATE` con un intervalo de fecha y hora usando desplazamientos de tiempo en relación con la hora actual del servidor. Puede especificar `lowerBound` y `upperBound` mediante un valor de milisegundos o la sintaxis de Bugzilla `1s 2m 3h 4d 5w 6M 7y` (un segundo, dos minutos, tres horas, cuatro días, cinco semanas, seis meses, siete años). El prefijo `-` indica un desplazamiento negativo antes de la hora actual. Si solo especifica `lowerBound` o `upperBound`, el otro valor predeterminado es `0`, que representa la hora actual.

Por ejemplo:

* `upperBound=1h` (y no `lowerBound`) selecciona nada en la hora siguiente
* `lowerBound=-1d` (y no `upperBound`) selecciona nada en las últimas 24 horas
* `lowerBound=-6M` y `upperBound=-3M` seleccionaron cualquier elemento en los últimos 3 a seis meses
* `lowerBound=-1500` y `upperBound=5500` seleccionan cualquier valor entre 1500 milisegundos de antigüedad y 5500 milisegundos en el futuro
* `lowerBound=1d` y `upperBound=2d` seleccionan cualquier cosa pasado mañana

No tiene en cuenta los años bisiestos y todos los meses son 30 días.

No admite el filtrado.

Admite la extracción de facetas del mismo modo que el predicado [`daterange`](#daterange).

#### Propiedades {#properties-17}

* **`upperBound`** - límite de fecha superior en milisegundos o `1s 2m 3h 4d 5w 6M 7y` (un segundo, dos minutos, tres horas, cuatro días, cinco semanas, seis meses, siete años) en relación con el tiempo actual del servidor, use `-` para el desplazamiento negativo
* **`lowerBound`**: límite de fecha inferior en milisegundos o `1s 2m 3h 4d 5w 6M 7y` (un segundo, dos minutos, tres horas, cuatro días, cinco semanas, seis meses o siete años) en relación con el tiempo actual del servidor, use `-` para el desplazamiento negativo

### savedquery {#savedquery}

Este predicado incluye todos los predicados de una consulta del Generador de consultas persistente en la consulta actual como predicado de subgrupo.

No ejecuta una consulta adicional pero amplía la consulta actual.

Las consultas se pueden mantener mediante programación usando `QueryBuilder#storeQuery()`. El formato puede ser una propiedad `String` multilínea o un nodo `nt:file` que contenga la consulta como archivo de texto en formato de propiedades Java™.

No admite la extracción de facetas para los predicados de la consulta guardada.

#### Propiedades {#properties-19}

* **`savedquery`** - ruta de acceso a la consulta guardada (propiedad `String` o nodo `nt:file`)

### parecido {#similar}

Este predicado es una búsqueda de similitud que usa `rep:similar()` de JCR XPath.

No admite el filtrado y no admite la extracción de facetas.

#### Propiedades {#properties-20}

* **`similar`**: ruta de acceso absoluta al nodo para el que se buscarán nodos similares
* **`local`**: una ruta relativa a un nodo descendiente o `.` para el nodo actual (opcional, el valor predeterminado es `.`)

### etiqueta {#tag}

Este predicado busca contenido etiquetado con una o más etiquetas, especificando las rutas de título de las etiquetas.

Admite la extracción de facetas y proporciona bloques para cada etiqueta única, utilizando su ruta de título de etiqueta actual.

#### Propiedades {#properties-21}

* **`tag`**: ruta de título de etiqueta que se va a buscar, por ejemplo, `properties:orientation/landscape`
* **`N_value`** - usar `1_value`, `2_value`, ... para buscar varias etiquetas (combinadas con `OR` de forma predeterminada, con `AND` si `and=true`)
* **`property`** - propiedad (o ruta relativa a la propiedad) que se va a ver (valor predeterminado `cq:tags`)

### tagid {#tagid}

Este predicado busca contenido etiquetado con una o más etiquetas, especificando los ID de etiqueta.

Admite la extracción de facetas y proporciona bloques para cada etiqueta única, utilizando su ID de etiqueta actual.

#### Propiedades {#properties-22}

* **`tagid`**: id. de etiqueta que se debe buscar, por ejemplo, `properties:orientation/landscape`
* **`N_value`** - usar `1_value`, `2_value`, ... para comprobar si hay varios identificadores de etiqueta (combinados con `OR` de forma predeterminada, con `AND` si `and=true`)
* **`property`** - propiedad (o ruta relativa a la propiedad) que se va a ver (valor predeterminado `cq:tags`)

### tagsearch {#tagsearch}

Este predicado busca contenido etiquetado con una o más etiquetas especificando palabras clave. Primero busca las etiquetas que contienen estas palabras clave en sus títulos y luego restringe el resultado a solo los elementos etiquetados con estas palabras clave.

No admite la extracción de facetas.

#### Propiedades {#Properties-1}

* **`tagsearch`**: palabra clave para buscar en títulos de etiquetas
* **`property`**: propiedad (o ruta relativa a la propiedad) que se debe tener en cuenta (valor predeterminado `cq:tags`)
* **`lang`**: para buscar solo en un determinado título de etiqueta localizado (por ejemplo, `de`)
* **`all`**: valor booleano para buscar texto completo de etiqueta completo, es decir, todos los títulos, descripciones, etc. (tiene prioridad sobre `lang`)

### tipo {#type}

Este predicado restringe los resultados a un tipo de nodo JCR específico, ambos tipos de nodo principal o `mixin` tipos. También encuentra subtipos de ese tipo de nodo. Los índices de búsqueda del repositorio deben cubrir los tipos de nodo para una ejecución eficiente.

Admite la extracción de facetas y proporciona bloques para cada tipo único en los resultados.

#### Propiedades {#Properties-2}

* **`type`** - tipo de nodo o nombre `mixin` para buscar, por ejemplo, `cq:Page`
