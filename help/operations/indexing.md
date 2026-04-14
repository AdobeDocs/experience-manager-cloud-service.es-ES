---
title: Búsqueda de contenido e indexación
description: Obtenga información acerca de la búsqueda de contenido y la indexación en AEM as a Cloud Service.
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
feature: Operations
role: Admin
source-git-commit: 54168b195bd234b0ca7932ca52c11056558dc53d
workflow-type: tm+mt
source-wordcount: '3321'
ht-degree: 14%

---

# Búsqueda de contenido e indexación {#indexing}

## Cambios en AEM as a Cloud Service {#changes-in-aem-as-a-cloud-service}

Con AEM as a Cloud Service, Adobe se aleja de un modelo de AEM centrado en instancias y se acerca a una vista basada en servicios con contenedores de AEM n-x, impulsada por canalizaciones de CI/CD en Cloud Manager. En lugar de configurar y mantener índices en instancias de AEM únicas, la configuración de índices debe especificarse antes de una implementación. Los cambios de configuración en la producción están incumpliendo las políticas de CI/CD. Lo mismo ocurre con los cambios de índice, ya que pueden afectar a la estabilidad y al rendimiento del sistema si no se especifican, prueban y reindexan antes de llevarlos a la producción.

A continuación se muestra una lista de los principales cambios en comparación con la versión 6.5 y versiones anteriores de AEM:

1. Los usuarios ya no tienen acceso al Administrador de índices de una sola instancia de AEM para depurar, configurar o mantener la indexación. Solo se utiliza para implementaciones y desarrollos locales.
1. Los usuarios no cambian los índices en una sola instancia de AEM, ni tienen que preocuparse por las comprobaciones de coherencia o la reindexación.
1. En general, los cambios de índice se inician antes de ir a producción para no eludir las puertas de enlace de calidad en las canalizaciones CI/CD de Cloud Manager y no tener impacto en los KPI empresariales en producción.
1. Todas las métricas relacionadas, incluido el rendimiento de búsqueda en producción, están disponibles para los clientes en tiempo de ejecución para proporcionar una vista integral de los temas de búsqueda e indexación.
1. Los clientes pueden configurar alertas según sus necesidades.
1. Los SRE supervisan el estado del sistema las 24 horas del día, los 7 días de la semana, y se toman medidas lo antes posible.
1. La configuración del índice se cambia mediante implementaciones. Los cambios en la definición del índice se configuran como otros cambios en el contenido.
1. En un nivel superior en AEM as a Cloud Service, con la introducción del [modelo de implementación móvil](#index-management-using-rolling-deployments), existen dos conjuntos de índices: uno para la versión antigua y otro para la nueva.
1. Los clientes pueden ver si el trabajo de indexación se ha completado en la página de creación de Cloud Manager y recibir una notificación cuando la nueva versión esté lista para admitir tráfico.

Restricciones:

* Actualmente, la administración de índices en AEM as a Cloud Service solo se admite para índices de tipo `lucene`. Esto significa que todas las personalizaciones de índice deben ser del tipo `lucene`. La propiedad `async` solo puede ser una de las siguientes: `[async]`, `[async,nrt]` o `[fulltext-async]`.
* Internamente, se pueden configurar y utilizar otros índices para las consultas. Por ejemplo, las consultas que se escriben en el índice `damAssetLucene` podrían, en AEM as a Cloud Service, ejecutarse con una versión Elasticsearch de este índice. Esta diferencia no es visible para el usuario. Sin embargo, algunas herramientas, como la característica `explain`, informan de un índice diferente. Para ver las diferencias entre los índices de Lucene y los de Elastic, consulte [la documentación de Elastic en Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/query/elastic.html). Los clientes no necesitan ni pueden configurar los índices de Elasticsearch directamente.
* Solo se admiten analizadores estándar (es decir, aquellos analizadores que se envían con el producto). No se admiten analizadores personalizados.
* No se admite la búsqueda por vectores de características similares (`useInSimilarity = true`).

>[!TIP]
>
>Para obtener más información sobre la indexación y las consultas de Oak, incluida una descripción detallada de las funciones de búsqueda avanzada e indexación, consulte la [documentación de Apache Oak](https://jackrabbit.apache.org/oak/docs/query/query.html).

## Usos {#how-to-use}

Las definiciones de índice se pueden clasificar en tres casos de uso principales, como se indica a continuación:

1. **Agregar** una nueva definición de índice personalizada.
2. **Actualice** una definición de índice existente agregando una nueva versión.
3. **Quitar** una definición de índice que ya no es necesaria.

Para los puntos 1 y 2 anteriores, debe crear una definición de índice como parte del código personalizado en la programación de versiones correspondiente de Cloud Manager. Para obtener más información, consulte la [Implementación en AEM as a Cloud Service](/help/implementing/deploying/overview.md).

Si es necesario realizar un cambio en la configuración del índice, asegúrese de que la configuración se ajusta a las directrices proporcionadas en la sección [Configuración del proyecto](#project-configuration). Realice las adaptaciones necesarias según corresponda.

## Configuración del proyecto

Los pasos para incorporarlo al proyecto son los siguientes:

1. Se recomienda encarecidamente utilizar la versión >= `1.3.2` del Jackrabbit `filevault-package-maven-plugin`. Si es necesario, actualice la versión en el nivel superior `pom.xml`:

   ```xml
   <plugin>
       <groupId>org.apache.jackrabbit</groupId>
           <artifactId>filevault-package-maven-plugin</artifactId>
           ...
           <version>1.3.2</version>
       ...
   </plugin>
   ```

2. Agregue lo siguiente al nivel superior `pom.xml`:

   ```xml
   <jackrabbit-packagetype>
       <options>   
           <immutableRootNodeNames>apps,libs,oak:index</immutableRootNodeNames>
       </options>
   </jackrabbit-packagetype>
   ```

   Este es un ejemplo del archivo `pom.xml` de nivel superior del proyecto con las configuraciones mencionadas anteriormente incluidas:

   Nombre de archivo: `pom.xml`

   ```xml
   <plugin>
       <groupId>org.apache.jackrabbit</groupId>
           <artifactId>filevault-package-maven-plugin</artifactId>
           ...
           <version>1.3.2</version>
           <configuration>
               ...
               <validatorsSettings>
                   <jackrabbit-packagetype>
                       <options>
                           <immutableRootNodeNames>apps,libs,oak:index</immutableRootNodeNames>
                       </options>
                   </jackrabbit-packagetype>
                   ...
               ...
   </plugin>
   ```

3. En `ui.apps/pom.xml` y `ui.apps.structure/pom.xml`, es necesario habilitar las opciones `allowIndexDefinitions` y `noIntermediateSaves` en `filevault-package-maven-plugin`. Habilitar `allowIndexDefinitions` permite definiciones de índice personalizadas, mientras que `noIntermediateSaves` garantiza que las configuraciones se agregan automáticamente.

   Nombres de archivo: `ui.apps/pom.xml` y `ui.apps.structure/pom.xml`

   ```xml
   <plugin>
       <groupId>org.apache.jackrabbit</groupId>
           <artifactId>filevault-package-maven-plugin</artifactId>
           <configuration>
               <allowIndexDefinitions>true</allowIndexDefinitions>
               <properties>
                   <cloudManagerTarget>none</cloudManagerTarget>
                   <noIntermediateSaves>true</noIntermediateSaves>
               </properties>
       ...
   </plugin>
   ```

4. Agregar un filtro para `/oak:index` en `ui.apps.structure/pom.xml`:

   ```xml
   <filters>
       ...
       <filter><root>/oak:index</root></filter>
   </filters>
   ```

>[!TIP]
>
>Para obtener más información sobre la estructura de paquetes necesaria para AEM as a Cloud Service, consulte [Estructura del proyecto AEM](/help/implementing/developing/introduction/aem-project-content-package-structure.md).

## Administración simplificada de índices mediante el índice de diferencias

La mayoría de los índices AEM se pueden configurar con Administración de índices simplificada.
Esto proporciona una forma sencilla de personalizar los índices predeterminados (OOTB) y definir índices personalizados mediante un archivo JSON.

>[!TIP]
>
>Hay una herramienta en línea que ayuda a configurar los índices AEM: [Herramientas de indexación de Oak](https://oak-indexing.github.io/oakTools/index.html). Tiene [una sección sobre administración simplificada de índices](https://oak-indexing.github.io/oakTools/simplified.html) con una guía paso a paso y herramientas adicionales para ayudar a convertir el índice personalizado a este nuevo formato.

Limitaciones: actualmente, la administración simplificada de índices no está disponible para los índices que incluyen `/apps`, `/libs`.
Se puede usar para todos los índices que tengan una propiedad `includedPaths` de, por ejemplo `/content`.
Para índices sin una propiedad `includedPaths`, o donde `includedPaths` contiene `/apps` o `/libs`,
considere la posibilidad de cambiar la consulta o utilizar el modo Configuraciones de índice heredadas que aparece a continuación.

La administración simplificada de índices puede personalizar los índices predeterminados existentes (OOTB) y agregar índices totalmente personalizados.
Con la administración simplificada de índices, no es necesario copiar definiciones ni definir versiones explícitamente.
Las personalizaciones de definición de índice se combinan automáticamente con el último índice predeterminado,
y se crea una nueva versión del índice cuando es necesario.

Para la mayoría de los índices, se pueden crear índices personalizados y personalizaciones de índices existentes mediante un paquete `diff.index`.
Para configurar un índice de este tipo, utilice la siguiente guía paso a paso.
El ejemplo siguiente personaliza el índice `damAssetLucene`
e introduce un índice totalmente personalizado al mismo tiempo.
El proceso es el siguiente:

1. Cree una nueva carpeta en el directorio `ui.apps` con el nombre `ui.apps/src/main/content/jcr_root/_oak_index/diff.index`.

2. Agregue un archivo de configuración `.content.xml` (es una configuración de marcador de posición necesaria, no una definición de índice normal) con el siguiente contenido: `ui.apps/src/main/content/jcr_root/_oak_index/diff.index/.content.xml`

   ```xml
   <?xml version="1.0" encoding="UTF-8"?><jcr:root
       xmlns:jcr="http://www.jcp.org/jcr/1.0"
       xmlns:nt="http://www.jcp.org/jcr/nt/1.0"
       jcr:primaryType="nt:unstructured"
       type="lucene" includedPaths="/same" queryPaths="/same" async="async">
   <diff.json jcr:primaryType="nt:file"/></jcr:root>
   ```

3. Cree un archivo de texto `diff.json` con el siguiente contenido.
En este ejemplo, personalizamos el índice predeterminado `damAssetLucene`
para indexar adicionalmente la propiedad denominada `test`. También definimos
un índice totalmente personalizado denominado `acme.testIndex` que indexa la propiedad `testing` en `nt:unstructured` nodos:

   `ui.apps/src/main/content/jcr_root/_oak_index/diff.index/diff.json`

   ```json
   {
       "damAssetLucene": {
           "indexRules": {
               "dam:Asset": {
                   "properties": {
                       "test": {
                           "name": "test",
                           "propertyIndex": true
                       }
                   }
               }
           }
       },
       "acme.testIndex": {
           "async": [ "async" ],
           "compatVersion": 2,
           "evaluatePathRestrictions": true,
           "includedPaths": [ "/content" ],
           "queryPaths": [ "/content" ],
           "selectionPolicy": "tag",
           "tags": [ "testing" ],
           "type": "lucene",
           "indexRules": {
               "nt:unstructured": {
                   "properties": {
                       "testing": {
                           "name": "testing",
                           "propertyIndex": true
                       }
                   }
               }
           }
       }
   }
   ```

4. Agregar una entrada al filtro FileVault en `ui.apps/src/main/content/META-INF/vault/filter.xml`:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <workspaceFilter version="1.0">
       ...
       <filter root="/oak:index/diff.index"/> 
   </workspaceFilter>
   ```

Después de aplicar los cambios, implemente la nueva aplicación con Cloud Manager.
Esta implementación inicia dos trabajos que agregan (y combinan, si es necesario)
las definiciones de índice para creación y publicación.
Antes del cambio, los repositorios subyacentes se reindexan utilizando las definiciones de índice actualizadas.

## Configuraciones de índice heredadas

Índices que no se pueden configurar mediante la administración simplificada de índices
Necesita utilizar el modo de configuración heredado.

La configuración de índice heredado se aplica solamente a los índices que no pueden tener una propiedad `includedPaths`
o que tengan una propiedad que deba cubrir `/apps`, `/libs` o `/`.
Algunos índices listos para usar cubren estas rutas:

* `cqPageLucene`: si necesita personalizar este índice,
considere migrar sus consultas para usar `cqPageContent` en su lugar,
que tiene un valor `includedPaths` de `/content` y una etiqueta.
* `ntBaseLucene`: la práctica recomendada es evitar cambiar este índice,
y, en su lugar, utilizando un índice totalmente personalizado con un prefijo como `acme.`,
que solo cubre las rutas requeridas.
Consulte la sección Administración simplificada de índices para obtener más información.

## Nombres de índice {#index-names}

Una definición de índice puede caer en una de las siguientes categorías:

1. Índice listo para usar (OOTB). Son índices predefinidos que proporciona AEM. Por ejemplo: `/oak:index/cqPageLucene-2` o `/oak:index/damAssetLucene-8`.

2. Personalizar un índice OOTB. Para personalizar un índice OOTB, anexe `-custom-` seguido de un número. Por ejemplo, `/oak:index/damAssetLucene-8-custom-1` es la personalización del índice OOTB `/oak:index/damAssetLucene-8`. Una personalización suele ser una copia del índice OOTB, además de propiedades adicionales que deben indizarse.

3. Índice totalmente personalizado: puede crear un índice completamente nuevo desde cero. Estos índices también deben finalizar con `-custom-` y un número de versión. Además, para evitar conflictos de nombres, utilice un prefijo en el nombre del índice. Por ejemplo: `/oak:index/acme.product-1-custom-2`, donde `acme.` es el prefijo.

>[!NOTE]
>
>Se desaconseja la introducción de nuevos índices en el tipo de nodo `dam:Asset` (especialmente índices de texto completo), ya que pueden entrar en conflicto con las características del producto OOTB, lo que provoca problemas de funcionamiento y rendimiento. En su lugar, la forma más adecuada de indexar consultas en el tipo de nodo `dam:Asset` es personalizar el índice `damAssetLucene-*`, agregando las propiedades adicionales. Estos cambios se combinarán automáticamente en una nueva versión del producto en versiones posteriores. Si tiene alguna duda, póngase en contacto con el Soporte técnico de Adobe.

## Preparación de la nueva definición de índice {#preparing-the-new-index-definition}

>[!NOTE]
>
>Al personalizar un índice predeterminado, como `damAssetLucene-8`, copie la última definición de índice lista para usarse de un *entorno de Cloud Service* con el Administrador de paquetes CRX DE (`/crx/packmgr/`) Cambie el nombre a `damAssetLucene-8-custom-1` (o posterior) y agregue las personalizaciones dentro del archivo XML. Si el índice en el entorno de nube es del tipo `elasticsearch`, se necesitan cambios adicionales: cambie la propiedad `type` a `lucene`, cambie la propiedad `async` a `[async,nrt]` y cambie la propiedad `similarityTags` a `true`. Esto garantiza que las configuraciones necesarias no se eliminen de forma involuntaria. Por ejemplo, el nodo `tika` bajo `/oak:index/damAssetLucene-8/tika` es necesario en el índice personalizado implementado en un entorno de AEM Cloud Service, pero no existe en el SDK local de AEM.

Para personalizar un índice OOTB, prepare un nuevo paquete que contenga la definición de índice personalizada. El nombre del índice debe seguir el patrón de nomenclatura:

`<indexName>-<productVersion>-custom-<customVersion>`

Para un índice completamente personalizado, prepare un nuevo paquete de definición de índice que contenga la definición de índice que siga este patrón de nomenclatura:

`<prefix>.<indexName>-<productVersion>-custom-<customVersion>`

Como se menciona en las secciones de limitaciones, el `type` de la definición de índice personalizada siempre debe establecerse en `lucene` aunque la definición de índice extraída mediante el Administrador de paquetes sea de un tipo diferente (por ejemplo `elasticsearch`).
La propiedad `async` también debe cambiarse en caso de que la definición de índice extraída esté establecida en `elastic-async`. La propiedad `async` debe establecerse en una de las siguientes: `[async]`, `[async,nrt]` o `[fulltext-async]` para la definición de índice personalizada.

<!--
 Alexandru: temporarily drafting this statement due to CQDOC-17701

The package from the above sample is built as `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`.
-->

>[!NOTE]
>
>Cualquier paquete de contenido que contenga definiciones de índice debe tener las siguientes propiedades establecidas en el archivo `properties.xml` del paquete de contenido. `properties.xml` se crea de manera predeterminada en un nuevo paquete y se encuentra en `<package_name>/META-INF/vault/properties.xml`:
>
> * `noIntermediateSaves=true`
>
> * `allowIndexDefinitions=true`

## Implementación de definiciones de índice personalizadas {#deploying-custom-index-definitions}

Para ilustrar la implementación de una versión personalizada del índice predeterminado `damAssetLucene-8`, proporcionaremos una guía paso a paso. En este ejemplo, se cambiará el nombre a `damAssetLucene-8-custom-1`. A continuación, el proceso es el siguiente:

1. Cree una nueva carpeta con el nombre de índice actualizado en el directorio `ui.apps`:
   * Ejemplo: `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/`

2. Agregue un archivo de configuración `.content.xml` con las configuraciones personalizadas dentro de la carpeta creada. A continuación se muestra un ejemplo de personalización:
Nombre de archivo: `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/.content.xml`

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:dam="http://www.day.com/dam/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0" xmlns:oak="http://jackrabbit.apache.org/oak/ns/1.0" xmlns:rep="internal"
       jcr:mixinTypes="[rep:AccessControllable]"
       jcr:primaryType="oak:QueryIndexDefinition"
       async="[async,nrt]"
       compatVersion="{Long}2"
       evaluatePathRestrictions="{Boolean}true"
       includedPaths="[/content/dam]"
       maxFieldLength="{Long}100000"
       type="lucene">
       <facets
           jcr:primaryType="nt:unstructured"
           secure="statistical"
           topChildren="100"/>
       <indexRules jcr:primaryType="nt:unstructured">
           <dam:Asset jcr:primaryType="nt:unstructured">
               <properties jcr:primaryType="nt:unstructured">
                   <cqTags
                       jcr:primaryType="nt:unstructured"
                       name="jcr:content/metadata/cq:tags"
                       nodeScopeIndex="{Boolean}true"
                       propertyIndex="{Boolean}true"
                       useInSpellcheck="{Boolean}true"
                       useInSuggest="{Boolean}true"/>
               </properties>
           </dam:Asset>
       </indexRules>
       <tika jcr:primaryType="nt:folder">
           <config.xml jcr:primaryType="nt:file"/>
       </tika>
   </jcr:root>
   ```

3. Agregar una entrada al filtro FileVault en `ui.apps/src/main/content/META-INF/vault/filter.xml`:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <workspaceFilter version="1.0">
       ...
       <filter root="/oak:index/damAssetLucene-8-custom-1"/> 
   </workspaceFilter>
   ```

4. Agregar un archivo de configuración para Apache Tika en: `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/tika/config.xml`:

   ```xml
   <properties>
       <detectors>
           <detector class="org.apache.tika.detect.TypeDetector"/>
       </detectors>
       <parsers>
           <parser class="org.apache.tika.parser.DefaultParser">
           <mime>text/plain</mime>
           </parser>
       </parsers>
       <service-loader initializableProblemHandler="ignore" dynamic="true"/>
   </properties>
   ```

5. Asegúrese de que la configuración cumpla las directrices proporcionadas en la sección [Configuración del proyecto](#project-configuration). Realice las adaptaciones necesarias según corresponda.

## Administración de índices mediante implementaciones móviles {#index-management-using-rolling-deployments}

### Qué es la administración de índices {#what-is-index-management}

La administración de índices consiste en añadir, quitar y cambiar índices. Cambiar la *definición* de un índice es rápido, pero la aplicación del cambio (a menudo llamado “creación de un índice” o, para los índices existentes, “reindexación”) requiere tiempo. No es instantáneo: el repositorio debe analizarse para indexar los datos.

### Qué son las implementaciones móviles {#what-are-rolling-deployments}

Una implementación móvil permite llevar a cabo actualizaciones sin tiempo de inactividad y proporciona reversiones rápidas. La versión antigua de la aplicación se ejecuta al mismo tiempo que la nueva.

### Áreas de solo lectura y de lectura-escritura {#read-only-and-read-write-areas}

Ciertas áreas del repositorio (partes de solo lectura) pueden ser diferentes en la versión antigua y en la nueva de la aplicación. Las áreas de solo lectura del repositorio suelen ser `/app` y `/libs`. En el siguiente ejemplo, se utiliza la cursiva para marcar las áreas de solo lectura, y la negrita para las de lectura-escritura.

* **/**
* */apps (solo lectura)*
* **/content**
* */libs (solo lectura)*
* **/oak:index**
* **/oak:index/acme.**
* **/jcr:system**
* **/system**
* **/var**

Las áreas de lectura-escritura del repositorio se comparten entre todas las versiones de la aplicación, mientras que, para cada versión de esta, hay un conjunto específico de `/apps` y `/libs`.

### Administración de índices sin implementaciones móviles {#index-management-without-rolling-deployments}

Durante el desarrollo o al utilizar instalaciones on-premise, los índices se pueden añadir, eliminar o cambiar durante la ejecución. Los índices se utilizan cuando están disponibles. Si todavía no se utiliza un índice en la versión antigua de la aplicación, se suele crear durante un tiempo de inactividad programado. Lo mismo ocurre cuando se elimina un índice o se cambia uno existente. Al eliminar un índice, deja de estar disponible cuando se elimina.

### Administración De Índices Con Implementaciones Móviles {#index-management-with-rolling-deployments}

Con las implementaciones móviles, no hay tiempo de inactividad. Durante algún tiempo durante una actualización, tanto la versión antigua (por ejemplo, la 1) de la aplicación, como la nueva (2), se ejecutan a la vez en el mismo repositorio. Si la versión 1 requiere que haya un determinado índice disponible, este no debe eliminarse en la 2. El índice debe eliminarse más adelante, por ejemplo, en la versión 3, momento en el que se garantiza que la versión 1 de la aplicación ya no se está ejecutando. Además, las aplicaciones deben escribirse de tal manera que la versión 1 funcione bien, incluso si la 2 se está ejecutando y hay índices de ella disponibles.

Una vez completada la actualización a la nueva versión, el sistema puede retirar los índices antiguos. Los índices antiguos suelen permanecer durante una semana para acelerar las reversiones (si fueran necesarias).

La tabla siguiente muestra cinco definiciones de índice: `cqPageLucene` se utiliza en ambas versiones, mientras que `damAssetLucene-custom-1` solo en la 2.

>[!NOTE]
>
>`<indexName>-custom-<customerVersionNumber>` es necesario para que AEM as a Cloud Service lo marque como reemplazo de un índice existente.

| Índice | Índice predeterminado | Uso en la versión 1 | Uso en la versión 2 |
|---|---|---|---|
| /oak:index/damAssetLucene-8 | Sí | Sí | No |
| /oak:index/damAssetLucene-8-custom-1 | Sí (personalizado) | No | Sí |
| /oak:index/acme.product-1-custom-1 | No | Sí | No |
| /oak:index/acme.product-1-custom-2 | No | No | Sí |
| /oak:index/cqPageLucene-2 | Sí | Sí | Sí |

El número de versión se incrementa cada vez que se cambia el índice. Para evitar que los nombres de índice personalizados entren en conflicto con los nombres de índice del propio producto, los índices personalizados y los cambios en los índices predeterminados deben terminar con `-custom-<number>`.

### Cambios en los índices predeterminados {#changes-to-out-of-the-box-indexes}

Después de que Adobe cambie un índice predeterminado como `damAssetLucene` o `cqPageLucene`, se crea un nuevo índice denominado `damAssetLucene-2` o `cqPageLucene-2`. O bien, si el índice ya se ha personalizado, la definición del índice personalizado se combina con los cambios en el índice predeterminado, como se muestra a continuación. La fusión de los cambios se produce de forma automática. Esto significa que no tiene que hacer nada si cambia un índice predeterminado. Sin embargo, es posible volver a personalizar el índice más adelante. En este caso, es importante utilizar la última versión (combinada) como línea de base.

| Índice | Índice predeterminado | Uso en la versión 2 | Uso en la versión 3 |
|---|---|---|---|
| /oak:index/damAssetLucene-1-custom-1 | Sí (personalizado) | Sí | No |
| /oak:index/damAssetLucene-2-custom-1 | Sí (se fusiona automáticamente desde damAssetLucene-1-custom-1 y damAssetLucene-2) | No | Sí |
| /oak:index/cqPageLucene-1 | Sí | Sí | No |
| /oak:index/cqPageLucene-2 | Sí | No | Sí |

Es importante tener en cuenta que los entornos pueden estar en diferentes versiones de AEM. Por ejemplo: el entorno `dev` está en la versión `X+1` mientras que stage y prod siguen en la versión `X` y esperan actualizarse a la versión `X+1` después de realizar las pruebas necesarias en `dev`. Si la versión `X+1` viene con una versión más reciente de un índice de producto que se ha personalizado y se requiere una nueva personalización de ese índice, la siguiente tabla explicará qué versiones deben establecerse en entornos basados en la versión de AEM:

| Entorno (versión de AEM) | Versión del índice del producto | Versión de índice personalizado existente | Nueva versión de índice personalizada |
|-----------------------------------|-----------------------|-------------------------------|----------------------------|
| Desarrollo (X+1) | damAssetLucene-11 | damAssetLucene-11-custom-1 | damAssetLucene-11-custom-2 |
| Fase (X) | damAssetLucene-10 | damAssetLucene-10-custom-1 | damAssetLucene-10-custom-2 |
| Producción (X) | damAssetLucene-10 | damAssetLucene-10-custom-1 | damAssetLucene-10-custom-2 |


### Limitaciones actuales {#current-limitations}

La administración de índices sólo se admite para índices de tipo `lucene`, con `compatVersion` establecido en `2`. Internamente, se pueden configurar otros índices y utilizarse para consultas, por ejemplo, índices Elasticsearch. Las consultas que se escriben en el índice `damAssetLucene` podrían, en AEM as a Cloud Service, ejecutarse con una versión Elasticsearch de este índice. Esta diferencia es invisible para el usuario de la aplicación, aunque algunas herramientas, como la característica `explain`, informa de un índice diferente. Para ver las diferencias entre los índices Lucene y Elasticsearch, consulte [la documentación de Elasticsearch en Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/query/elastic.html). Los clientes no pueden y no necesitan configurar los índices Elasticsearch directamente.

Solo se admiten analizadores integrados (es decir, aquellos analizadores que se envían con el producto). No se admiten analizadores personalizados.

Actualmente no se admite la indexación del contenido de `/oak:index`.

Para obtener el mejor rendimiento operativo, los índices no deben ser excesivamente grandes. El tamaño total de todos los índices puede utilizarse como guía. Si este tamaño aumenta más del 100 % después de agregar índices personalizados y de ajustar los índices estándar en un entorno de desarrollo, se deben ajustar las definiciones de índices personalizados. AEM as a Cloud Service puede evitar la implementación o eliminar índices que afectarían negativamente a la estabilidad y el rendimiento del sistema.

### Adición de un índice {#adding-an-index}

Para agregar un índice totalmente personalizado denominado `/oak:index/acme.product-1-custom-1`, para utilizarlo en una nueva versión de la aplicación y posteriormente, el índice debe configurarse de la siguiente manera:

`acme.product-1-custom-1`

Esta configuración funciona anteponiendo un identificador personalizado al nombre del índice, seguido de un punto (**`.`**). El identificador debe tener entre 2 y 5 caracteres de longitud.

Como en el caso anterior, esta configuración garantiza que el índice solo lo utilice la nueva versión de la aplicación.

### Cambio de un índice {#changing-an-index}

Cuando se cambia un índice existente, se debe añadir uno nuevo con la definición de índice modificada. Por ejemplo, considere que el índice existente `/oak:index/acme.product-1-custom-1` cambia. El índice antiguo se almacena en `/oak:index/acme.product-1-custom-1` y el nuevo, en `/oak:index/acme.product-1-custom-2`.

La versión antigua de la aplicación utiliza la siguiente configuración:

`/oak:index/acme.product-1-custom-1`

La nueva versión de la aplicación utiliza la siguiente configuración (modificada):

`/oak:index/acme.product-1-custom-2`

>[!NOTE]
>
>Es posible que las definiciones de índice de AEM as a Cloud Service no coincidan por completo con las de una instancia de desarrollo local. La instancia de desarrollo no tiene una configuración de Tika, mientras que las instancias de AEM as a Cloud Service sí la tienen. Si personaliza un índice con una configuración de Tika, manténgala.

### Anulación de un cambio {#undoing-a-change}

A veces, es necesario deshacer una modificación en una definición de índice, por ejemplo, debido a un error o porque la modificación ya no es necesaria. Por ejemplo, si la definición de índice `damAssetLucene-8-custom-3` contiene un error, es posible que desee volver a la definición anterior, `damAssetLucene-8-custom-2`. Para ello, cree un nuevo índice denominado `damAssetLucene-8-custom-4` que sea una copia del índice anterior, `damAssetLucene-8-custom-2`.

### Eliminación de un índice {#removing-an-index}

Lo siguiente solo se aplica a las personalizaciones de índices listos para usar (OOTB) y a índices totalmente personalizados. Tenga en cuenta que los índices OOTB originales no se pueden eliminar, ya que los utiliza AEM.

Para garantizar la integridad y estabilidad del sistema, las definiciones de índice deben tratarse como inmutables una vez implementadas. Si necesita eliminar un índice o una personalización personalizados, cree una nueva versión de ese índice con una definición que simule efectivamente la eliminación
(vea los ejemplos siguientes).

Una vez implementada una nueva versión de un índice, las consultas ya no utilizarán la versión anterior del mismo índice.
La versión anterior no se eliminará inmediatamente del entorno,
pero será elegible para la recolección de basura por un mecanismo de limpieza que se ejecuta periódicamente.
Después de un período de gracia diseñado para permitir la recuperación en caso de errores
(actualmente, 7 días contando desde que se eliminó la indexación, pero sujeto a cambios),
este mecanismo de limpieza eliminará los datos de índice no utilizados,
y deshabilitarán o eliminarán la versión antigua del índice del entorno.

A continuación, describimos los dos casos posibles: eliminación de las personalizaciones de un índice OOTB y eliminación de un índice totalmente personalizado.

#### Eliminación de personalizaciones de un índice predeterminado

Siga los pasos descritos en [Deshacer un cambio](#undoing-a-change-undoing-a-change) con las definiciones del índice OOTB como la nueva versión. Por ejemplo, si ya ha implementado `damAssetLucene-8-custom-3`, pero ya no necesita las personalizaciones y desea volver al índice predeterminado `damAssetLucene-8`, debe agregar un índice `damAssetLucene-8-custom-4` que contenga la definición de índice de `damAssetLucene-8`.

#### Eliminación de un índice totalmente personalizado

Siga los pasos descritos en [Deshacer un cambio](#undoing-a-change-undoing-a-change) con un índice ficticio como la nueva versión. Un índice ficticio nunca se utiliza para consultas y no contiene datos, por lo que el efecto es el mismo que si el índice no existiera. Para este ejemplo, puede ponerle el nombre `/oak:index/acme.product-1-custom-3`. Este nombre reemplaza el índice `/oak:index/acme.product-1-custom-2`. Un ejemplo de este índice ficticio es:

```xml
<acme.product-1-custom-3
        jcr:primaryType="oak:QueryIndexDefinition"
        async="async"
        compatVersion="2"
        includedPaths="/dummy"
        queryPaths="/dummy"
        type="lucene">
        <indexRules jcr:primaryType="nt:unstructured">
            <rep:root jcr:primaryType="nt:unstructured">
                <properties jcr:primaryType="nt:unstructured">
                    <dummy
                        jcr:primaryType="nt:unstructured"
                        name="dummy"
                        propertyIndex="{Boolean}true"/>
                </properties>
            </rep:root>
        </indexRules>
</acme.product-1-custom-3>
```

## Optimizaciones de índice y consulta {#index-query-optimizations}

Apache Jackrabbit Oak permite configuraciones de índice flexibles para gestionar de forma eficiente las consultas de búsqueda. Los índices son especialmente importantes para repositorios más grandes. Asegúrese de que todas las consultas estén respaldadas por un índice adecuado. Las consultas sin un índice adecuado pueden leer miles de nodos, que luego se registran como advertencia.

Consulte [este documento](query-and-indexing-best-practices.md) para obtener información sobre cómo se pueden optimizar las consultas y los índices.
