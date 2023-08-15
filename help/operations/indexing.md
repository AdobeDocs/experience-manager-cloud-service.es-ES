---
title: Búsqueda de contenido e indexación
description: AEM Obtenga información acerca de la búsqueda de contenido y la indexación en as a Cloud Service.
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '2324'
ht-degree: 34%

---

# Búsqueda de contenido e indexación {#indexing}

## Cambios en AEM as a Cloud Service {#changes-in-aem-as-a-cloud-service}

Con AEM as a Cloud Service, Adobe se aleja de un modelo de AEM centrado en instancias y se acerca a una vista basada en servicios con contenedores de AEM n-x, impulsada por canalizaciones de CI/CD en Cloud Manager. En lugar de configurar y mantener los índices en instancias de AEM únicas, la configuración de Índice debe especificarse antes de una implementación. Los cambios de configuración en la producción están violando de forma clara las políticas CI/CD. Lo mismo ocurre con los cambios de índice, ya que pueden afectar a la estabilidad y al rendimiento del sistema si no se especifican, se prueban y se reindexan antes de llevarlos a la producción.

A continuación se muestra una lista de los principales cambios en comparación con la versión 6.5 y versiones anteriores de AEM:

1. AEM Los usuarios ya no tienen acceso al Administrador de índices de una sola instancia de para depurar, configurar o mantener la indexación. Solo se utiliza para implementaciones y desarrollos locales.
1. AEM Los usuarios no cambian los índices en una sola instancia de ni tienen que preocuparse por las comprobaciones de coherencia o la reindexación.
1. En general, los cambios de índice se inician antes de ir a producción para no eludir las puertas de enlace de calidad en las canalizaciones CI/CD de Cloud Manager y no tener impacto en los KPI empresariales en producción.
1. Todas las métricas relacionadas, incluido el rendimiento de búsqueda en producción, están disponibles para los clientes en tiempo de ejecución para proporcionar una vista integral de los temas de Búsqueda e Indexación.
1. Los clientes pueden configurar alertas según sus necesidades.
1. Los SRE supervisan el estado del sistema las 24 horas del día, los 7 días de la semana, y se toman medidas lo antes posible.
1. La configuración del índice se cambia mediante implementaciones. Los cambios en la definición del índice se configuran como otros cambios en el contenido.
1. AEM A un alto nivel sobre el as a Cloud Service de la, con la introducción de la [modelo de implementación móvil](#index-management-using-rolling-deployments)Sin embargo, existen dos conjuntos de índices: uno para la versión antigua y otro para la nueva.
1. Los clientes pueden ver si el trabajo de indexación se ha completado en la página de creación de Cloud Manager y recibe una notificación cuando la nueva versión está lista para admitir tráfico.

Restricciones:

* En la actualidad, la administración de índices en AEM as a Cloud Service solo se admite para índices de tipo `lucene`.
* Solo se admiten analizadores estándar (es decir, aquellos analizadores que se envían con el producto). No se admiten analizadores personalizados.
* Internamente, se pueden configurar y utilizar otros índices para las consultas. Por ejemplo, las consultas que se escriben en relación con el índice `damAssetLucene`, en Skyline, podrían ejecutarse con una versión Elasticsearch de este. Esta diferencia no suele ser visible para la aplicación y el usuario; sin embargo, algunas herramientas, como `explain` informe de funciones con un índice diferente. Para ver las diferencias entre los índices de Lucene y los de Elastic, consulte [la documentación de Elastic en Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/query/elastic.html). Los clientes no necesitan ni pueden configurar índices de Elasticsearch directamente.
* Buscar por vectores de funciones similares (`useInSimilarity = true`) no es compatible.

## Usos {#how-to-use}

Las definiciones de índice se pueden clasificar en tres casos de uso principales, como se indica a continuación:

1. **Añadir** una nueva definición de índice personalizada.
2. **Actualizar** Añada una definición de índice existente mediante la adición de una nueva versión.
3. **Eliminar** una definición de índice que ya no es necesaria.

Para los puntos 1 y 2 anteriores, debe crear una nueva definición de índice como parte del código personalizado en la programación de versiones correspondiente de Cloud Manager. Para obtener más información, consulte la [AEM Implementación en el as a Cloud Service de](/help/implementing/deploying/overview.md) documentación.

## Nombres de índice {#index-names}

Una definición de índice puede caer en una de las siguientes categorías:

1. Índice listo para usar (OOTB). Por ejemplo: `/oak:index/cqPageLucene-2` o `/oak:index/damAssetLucene-8`.

2. Personalizar un índice OOTB. Se indican añadiendo `-custom-` seguido de un identificador numérico para el nombre del índice original. Por ejemplo: `/oak:index/damAssetLucene-8-custom-1`.

3. Índice totalmente personalizado: Es posible crear un índice completamente nuevo desde cero. Su nombre debe tener un prefijo para evitar conflictos de nombres. Por ejemplo: `/oak:index/acme.product-1-custom-2`, donde el prefijo es `acme.`

## Preparación de la nueva definición de índice {#preparing-the-new-index-definition}

>[!NOTE]
>
>Si personaliza un índice predeterminado, como `damAssetLucene-8`, copie la última definición de índice lista para usarse de un *entorno de Cloud Service* con el Administrador de paquetes CRX DE (`/crx/packmgr/`). Cambiarle el nombre a `damAssetLucene-8-custom-1` (o superior) y agregue las personalizaciones dentro del archivo XML. Esto garantiza que las configuraciones necesarias no se eliminen de forma involuntaria. Por ejemplo, el nodo `tika` bajo `/oak:index/damAssetLucene-8/tika` es necesario en el índice personalizado del servicio en la nube. No existe en el SDK de la nube.

Para las personalizaciones de un índice OOTB, prepare un nuevo paquete que contenga la definición del índice real que siga este patrón de nomenclatura:

`<indexName>-<productVersion>-custom-<customVersion>`

Para un índice completamente personalizado, prepare un nuevo paquete de definición de índice que contenga la definición de índice que siga este patrón de nomenclatura:

`<prefix>.<indexName>-<productVersion>-custom-<customVersion>`

<!-- Alexandru: temporarily drafting this statement due to CQDOC-17701

The package from the above sample is built as `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`. -->

>[!NOTE]
>
>Cualquier paquete de contenido que contenga definiciones de índice debe tener las siguientes propiedades establecidas en el archivo de propiedades del paquete de contenido, ubicado en `<package_name>/META-INF/vault/properties.xml`:
>
> * `noIntermediateSaves=true`
>
> * `allowIndexDefinitions=true`

## Implementación de definiciones de índice personalizadas {#deploying-custom-index-definitions}

Para ilustrar la implementación de una versión personalizada del índice predeterminado `damAssetLucene-8`, le proporcionaremos una guía paso a paso. En este ejemplo, cambiaremos el nombre a `damAssetLucene-8-custom-1`. A continuación, el proceso es el siguiente:

1. Cree una nueva carpeta con el nombre de índice actualizado en la `ui.apps` directorio:
   * Ejemplo: `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/`

2. Añadir un archivo de configuración `.content.xml` con las configuraciones personalizadas dentro de la carpeta recién creada. A continuación se muestra un ejemplo de personalización: Nombre de archivo: `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/.content.xml`

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

3. Añada una entrada al filtro FileVault en `ui.apps/src/main/content/META-INF/vault/filter.xml`:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <workspaceFilter version="1.0">
       ...
       <filter root="/oak:index/damAssetLucene-8-custom-1"/> 
   </workspaceFilter>
   ```

4. Añada un archivo de configuración para Apache Tika en: `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/tika/config.xml`:

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

5. Asegúrese de que la configuración de se ajusta a las directrices proporcionadas en la [Configuración del proyecto](#project-configuration) sección. Realice las adaptaciones necesarias según corresponda.

## Configuración del proyecto

Se recomienda encarecidamente utilizar la versión >= `1.3.2` del Conejo `filevault-package-maven-plugin`. Los pasos para incorporarlo al proyecto son los siguientes:

1. Actualice la versión en el nivel superior `pom.xml`:

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

   Este es un ejemplo del nivel superior del proyecto `pom.xml` con las configuraciones mencionadas incluidas:

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

3. Entrada `ui.apps/pom.xml` y `ui.apps.structure/pom.xml` es necesario habilitar la variable `allowIndexDefinitions` y `noIntermediateSaves` opciones en la `filevault-package-maven-plugin`. Habilitando `allowIndexDefinitions` permite definiciones de índice personalizadas, mientras que `noIntermediateSaves` garantiza que las configuraciones se añadan automáticamente.

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

4. Añadir un filtro para `/oak:index` in `ui.apps.structure/pom.xml`:

   ```xml
   <filters>
       ...
       <filter><root>/oak:index</root></filter>
   </filters>
   ```

Después de agregar la nueva definición de índice, implemente la nueva aplicación mediante Cloud Manager. Esta implementación inicia dos trabajos, responsables de agregar (y combinar si es necesario) las definiciones de índice a MongoDB y Azure Segment Store para su creación y publicación, respectivamente. Antes del cambio, los repositorios subyacentes se someten a una reindexación con las definiciones de índice actualizadas.

>[!TIP]
>
>Para obtener más información sobre la estructura de paquetes necesaria para AEM as a Cloud Service, consulte el documento [Estructura del proyecto de AEM](/help/implementing/developing/introduction/aem-project-content-package-structure.md).

## Administración de índices mediante implementaciones móviles {#index-management-using-rolling-deployments}

### Qué es la administración de índices {#what-is-index-management}

La administración de índices consiste en añadir, quitar y cambiar índices. Cambiar la *definición* de un índice es rápido, pero la aplicación del cambio (a menudo llamado “creación de un índice” o, para los índices existentes, “reindexación”) requiere tiempo. No es instantáneo: el repositorio debe analizarse para indexar los datos.

### Qué son las implementaciones móviles {#what-are-rolling-deployments}

Una implementación móvil puede reducir el tiempo de inactividad. También permite llevar a cabo actualizaciones sin tiempo de inactividad y proporciona reversiones rápidas. La versión antigua de la aplicación se ejecuta al mismo tiempo que la nueva.

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

Una vez completada la actualización a la nueva versión, el sistema puede retirar los índices antiguos. Es posible que los índices antiguos se mantengan durante algún tiempo para acelerar las reversiones (si fueran necesarias).

La tabla siguiente muestra cinco definiciones de índice: `cqPageLucene` se utiliza en ambas versiones, mientras que `damAssetLucene-custom-1` solo en la 2.

>[!NOTE]
>
>El `<indexName>-custom-<customerVersionNumber>` AEM es necesario para que el as a Cloud Service de la lo marque como reemplazo de un índice existente.

| Índice | Índice predeterminado | Uso en la versión 1 | Uso en la versión 2 |
|---|---|---|---|
| /oak:index/damAssetLucene | Sí | Sí | No |
| /oak:index/damAssetLucene-custom-1 | Sí (personalizado) | No | Sí |
| /oak:index/acme.product-custom-1 | No | Sí | No |
| /oak:index/acme.product-custom-2 | No | No | Sí |
| /oak:index/cqPageLucene | Sí | Sí | Sí |

El número de versión se incrementa cada vez que se cambia el índice. Para evitar que los nombres de índice personalizados entren en conflicto con los nombres de índice del propio producto, los índices personalizados y los cambios en los índices predeterminados deben terminar con `-custom-<number>`.

### Cambios en los índices predeterminados {#changes-to-out-of-the-box-indexes}

Después del Adobe, se cambia un índice predeterminado como &quot;damAssetLucene&quot; o &quot;cqPageLucene&quot;, un nuevo índice denominado `damAssetLucene-2` o `cqPageLucene-2` se ha creado. O bien, si el índice ya se ha personalizado, la definición del índice personalizado se combina con los cambios en el índice predeterminado, como se muestra a continuación. La fusión de los cambios se produce de forma automática. Esto significa que no tiene que hacer nada si cambia un índice predeterminado. Sin embargo, es posible volver a personalizar el índice más adelante.

| Índice | Índice predeterminado | Uso en la versión 2 | Uso en la versión 3 |
|---|---|---|---|
| /oak:index/damAssetLucene-custom-1 | Sí (personalizado) | Sí | No |
| /oak:index/damAssetLucene-2-custom-1 | Sí (se fusiona automáticamente desde damAssetLucene-custom-1 y damAssetLucene-2) | No | Sí |
| /oak:index/cqPageLucene | Sí | Sí | No |
| /oak:index/cqPageLucene-2 | Sí | No | Sí |

### Limitaciones actuales {#current-limitations}

La administración de índices solo se admite para índices de tipo `lucene`, con `compatVersion` establezca en `2`. Internamente, se pueden configurar otros índices y utilizarse para consultas, por ejemplo índices de Elasticsearch. Consultas que se escriben en relación con `damAssetLucene` AEM index podría, en el caso de que esté as a Cloud Service, ejecutarse con una versión de Elasticsearch de este índice. Esta diferencia es invisible para el usuario final de la aplicación, aunque algunas herramientas, como la `explain` función informa de un índice diferente. Para ver las diferencias entre los índices de Lucene y Elasticsearch, consulte [la documentación del Elasticsearch en Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/query/elastic.html). Los clientes no pueden y no necesitan configurar índices de Elasticsearch directamente.

Solo se admiten analizadores integrados (es decir, aquellos analizadores que se envían con el producto). No se admiten analizadores personalizados.

Para obtener el mejor rendimiento operativo, los índices no deben ser excesivamente grandes. El tamaño total de todos los índices puede utilizarse como guía. Si este tamaño aumenta más del 100 % después de agregar índices personalizados y de ajustar los índices estándar en un entorno de desarrollo, se deben ajustar las definiciones de índices personalizados. AEM Los as a Cloud Service pueden evitar la implementación de índices que afectarían negativamente a la estabilidad y el rendimiento del sistema.

### Adición de un índice {#adding-an-index}

Para agregar un índice totalmente personalizado denominado `/oak:index/acme.product-custom-1`, para su uso en una nueva versión de la aplicación y posterior, el índice debe configurarse de la siguiente manera:

`acme.product-1-custom-1`

Esta configuración funciona anteponiendo un identificador personalizado al nombre del índice, seguido de un punto (**`.`**). El identificador debe tener entre 2 y 5 caracteres de longitud.

Como en el caso anterior, esta configuración garantiza que el índice solo lo utilice la nueva versión de la aplicación.

### Cambio de un índice {#changing-an-index}

Cuando se cambia un índice existente, se debe añadir uno nuevo con la definición de índice modificada. Por ejemplo, considere que el índice existente `/oak:index/acme.product-custom-1` cambia. El índice antiguo se almacena en `/oak:index/acme.product-custom-1` y el nuevo, en `/oak:index/acme.product-custom-2`.

La versión antigua de la aplicación utiliza la siguiente configuración:

`/oak:index/acme.product-custom-1`

La nueva versión de la aplicación utiliza la siguiente configuración (modificada):

`/oak:index/acme.product-custom-2`

>[!NOTE]
>
>Es posible que las definiciones de índice de AEM as a Cloud Service no coincidan por completo con las de una instancia de desarrollo local. AEM La instancia de desarrollo no tiene una configuración de Tika, mientras que las instancias de as a Cloud Service, sí, tienen una. Si personaliza un índice con una configuración de Tika, manténgala.

### Anulación de un cambio {#undoing-a-change}

A veces, es necesario deshacer una modificación en una definición de índice. Esto puede deberse a un error involuntario o a que la modificación ya no es necesaria. Tomemos, por ejemplo, la definición del índice `damAssetLucene-8-custom-3,` que se creó por error y ya se ha implementado. Por lo tanto, desea volver a la definición de índice anterior, `damAssetLucene-8-custom-2.` Para ello, debe introducir un nuevo índice denominado `damAssetLucene-8-custom-4` que incorpora la definición del índice anterior, `damAssetLucene-8-custom-2.`

### Eliminación de un índice {#removing-an-index}

Lo siguiente solo se aplica a los índices personalizados. Los índices de productos no se pueden eliminar porque los utiliza AEM.

Si se elimina un índice en una versión posterior de la aplicación, se puede definir un índice vacío (que no se utiliza nunca y que no contiene datos), con un nombre nuevo. Para este ejemplo, puede ponerle un nombre `/oak:index/acme.product-custom-3`. Este nombre reemplaza al índice `/oak:index/acme.product-custom-2`. Después `/oak:index/acme.product-custom-2` elimina el sistema, el índice vacío `/oak:index/acme.product-custom-3` a continuación, se puede eliminar. Un ejemplo de este índice vacío es el siguiente:

```xml
<acme.product-custom-3
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
</acme.product-custom-3>
```

Si ya no es necesario tener una personalización de un índice predeterminado, debe copiar la definición de índice predeterminada. Por ejemplo, si ya ha implementado `damAssetLucene-8-custom-3`, pero ya no necesita las personalizaciones y desea volver al índice `damAssetLucene-8` predeterminado, debe añadir un índice `damAssetLucene-8-custom-4` que contenga la definición de índice de `damAssetLucene-8`.

## Optimizaciones de índice y consulta {#index-query-optimizations}

Apache Jackrabbit Oak permite configuraciones de índice flexibles para gestionar de forma eficiente las consultas de búsqueda. Los índices son especialmente importantes para repositorios más grandes. Asegúrese de que todas las consultas estén respaldadas por un índice adecuado. Las consultas sin un índice adecuado pueden leer miles de nodos, que luego se registran como advertencia.

Consulte [este documento](query-and-indexing-best-practices.md) para obtener información sobre cómo se pueden optimizar las consultas y los índices.
