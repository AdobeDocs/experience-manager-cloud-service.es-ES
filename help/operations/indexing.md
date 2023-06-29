---
title: Búsqueda de contenido e indexación
description: Búsqueda de contenido e indexación
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '2427'
ht-degree: 38%

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

## Usos {#how-to-use}

La definición de índices puede comprender estos tres casos de uso:

1. Agregar una definición de índice de cliente.
1. Actualización de una definición de índice existente. Esta actualización significa que se añade una nueva versión de una definición de índice existente.
1. Eliminación de un índice redundante u obsoleto.

Para los puntos 1 y 2 anteriores, debe crear una definición de índice como parte del código personalizado en la programación de versiones correspondiente de Cloud Manager. Para obtener más información, consulte [AEM Implementación en documentación as a Cloud Service de la](/help/implementing/deploying/overview.md).

## Nombres de índice {#index-names}

Una definición de índice puede ser la siguiente:

1. Un índice predeterminado. Un ejemplo es `/oak:index/cqPageLucene-2`.
1. Una personalización de un índice predeterminado. El cliente define estas personalizaciones. Un ejemplo es `/oak:index/cqPageLucene-2-custom-1`.
1. Un índice totalmente personalizado. Un ejemplo es `/oak:index/acme.product-1-custom-2`. Para evitar conflictos de nombres, el Adobe requiere que los índices totalmente personalizados tengan un prefijo, por ejemplo, `acme.`

Tenga en cuenta que tanto la personalización de un índice predeterminado como los índices totalmente personalizados deben contener `-custom-`. Solo los índices totalmente personalizados deben comenzar con un prefijo.

## Preparación de la nueva definición de índice {#preparing-the-new-index-definition}

>[!NOTE]
>
>Si personaliza un índice predeterminado, por ejemplo, `damAssetLucene-6`, copie la última definición de índice lista para usar de un *entorno Cloud Service* usar el Administrador de paquetes CRX DE (`/crx/packmgr/`). A continuación, cambie el nombre de la configuración, por ejemplo, a `damAssetLucene-6-custom-1`. Añada sus personalizaciones en la parte superior. Este proceso garantiza que las configuraciones necesarias no se eliminen de forma involuntaria. Por ejemplo, el nodo `tika` bajo `/oak:index/damAssetLucene-6/tika` es necesario en el índice personalizado del servicio en la nube. No existe en el SDK de la nube.

Prepare un paquete de definición de índice que contenga la definición de índice real, siguiendo este patrón de nomenclatura:

`<indexName>[-<productVersion>]-custom-<customVersion>`

Que entonces debe ir bajo `ui.apps/src/main/content/jcr_root`. Todas las definiciones de índice personalizadas deben almacenarse en `/oak:index`.

El filtro del paquete debe configurarse de modo que los índices existentes (predeterminados) se mantengan. En el archivo `ui.apps/src/main/content/META-INF/vault/filter.xml`, cada índice personalizado debe enumerarse, por ejemplo, como `<filter root="/oak:index/damAssetLucene-6-custom-1"/>`. Si la versión del índice cambia posteriormente, se debe ajustar el filtro.

<!-- Alexandru: temporarily drafting this statement due to CQDOC-17701

The package from the above sample is built as `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`. -->

>[!NOTE]
>
>Cualquier paquete de contenido que contenga definiciones de índice debe tener la siguiente propiedad establecida en el archivo de propiedades del paquete de contenido, en `/META-INF/vault/properties.xml`:
>
>`noIntermediateSaves=true`

## Implementación de definiciones de índice {#deploying-index-definitions}

Las definiciones de índice están marcadas como personalizadas y con versiones:

* La definición del índice en sí (por ejemplo `/oak:index/ntBaseLucene-custom-1`)

Para implementar un índice personalizado, la definición del índice (`/oak:index/definitionname`) debe entregarse mediante `ui.apps` mediante Git y el proceso de implementación de Cloud Manager. En el filtro FileVault, por ejemplo, `ui.apps/src/main/content/META-INF/vault/filter.xml`, enumere cada índice personalizado individualmente, por ejemplo `<filter root="/oak:index/damAssetLucene-7-custom-1"/>`. La definición de índice personalizada se almacena en el archivo `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-7-custom-1/.content.xml`, como se indica a continuación:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:oak="https://jackrabbit.apache.org/oak/ns/1.0" xmlns:dam="http://www.day.com/dam/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0" xmlns:rep="internal"
        jcr:primaryType="oak:QueryIndexDefinition"
        async="[async,nrt]"
        compatVersion="{Long}2"
        ...
        </indexRules>
        <tika jcr:primaryType="nt:unstructured">
            <config.xml jcr:primaryType="nt:file"/>
        </tika>
</jcr:root>
```

El ejemplo anterior contiene una configuración para Apache Tika. El archivo de configuración de Tika se almacenaría en `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-7-custom-1/tika/config.xml`.

### Configuración del proyecto

Dependiendo de la versión del complemento de paquete Jackrabbit Filevault Maven que se use, se requiere algo más de configuración en el proyecto. Al utilizar la versión del complemento de paquete Jackrabbit Filevault Maven **1.1.6** o más reciente, a continuación, el archivo `pom.xml` debe contener la siguiente sección en la configuración del complemento para `filevault-package-maven-plugin`, en `configuration/validatorsSettings` (justo antes de `jackrabbit-nodetypes`):

```xml
<jackrabbit-packagetype>
    <options>
        <immutableRootNodeNames>apps,libs,oak:index</immutableRootNodeNames>
    </options>
</jackrabbit-packagetype>
```

Además, en este caso, la variable `vault-validation` La versión debe actualizarse a una versión más reciente:

```xml
<dependency>
    <groupId>org.apache.jackrabbit.vault</groupId>
    <artifactId>vault-validation</artifactId>
    <version>3.5.6</version>
</dependency>
```

A continuación, en `ui.apps.structure/pom.xml` y `ui.apps/pom.xml`, la configuración del `filevault-package-maven-plugin` debe tener `allowIndexDefinitions` y `noIntermediateSaves` activado. La opción `noIntermediateSaves` garantiza que las configuraciones de índice se añadan automáticamente.

```xml
<groupId>org.apache.jackrabbit</groupId>
    <artifactId>filevault-package-maven-plugin</artifactId>
    <configuration>
        <allowIndexDefinitions>true</allowIndexDefinitions>
        <properties>
            <cloudManagerTarget>none</cloudManagerTarget>
            <noIntermediateSaves>true</noIntermediateSaves>
        </properties>
    ...
```

Entrada `ui.apps.structure/pom.xml`, el `filters` para este complemento debe contener una raíz de filtro como se indica a continuación:

```xml
<filter><root>/oak:index</root></filter>
```

Una vez añadida la nueva definición de índice, la nueva aplicación se implementa mediante Cloud Manager. En la implementación, se inician dos trabajos responsables de agregar (y combinar si es necesario) las definiciones de índice a MongoDB y Azure Segment Store para la creación y publicación, respectivamente. Los repositorios subyacentes se reindexan con las nuevas definiciones de índice, antes de que tenga lugar el cambio.

### NOTA

En caso de que observe el siguiente error en la validación de filevault <br>
`[ERROR] ValidationViolation: "jackrabbit-nodetypes: Mandatory child node missing: jcr:content [nt:base] inside node with types [nt:file]"` <br>
A continuación, se puede seguir cualquiera de los siguientes pasos para solucionar el problema: <br>

1. Actualice filevault a la versión 1.0.4 y añada lo siguiente al pom de nivel superior:

```xml
<allowIndexDefinitions>true</allowIndexDefinitions>
```

A continuación se muestra un ejemplo de dónde colocar la configuración anterior en el pom.

```xml
<plugin>
    <groupId>org.apache.jackrabbit</groupId>
    <artifactId>filevault-package-maven-plugin</artifactId>
    <configuration>
        <properties>
        ...
        </properties>
        ...
        <allowIndexDefinitions>true</allowIndexDefinitions>
        <repositoryStructurePackages>
        ...
        </repositoryStructurePackages>
        <dependencies>
        ...
        </dependencies>
    </configuration>
</plugin>
```

1. Deshabilite la validación del tipo de nodo. Establezca la siguiente propiedad en la sección jackrabbit-nodetypes de la configuración del complemento filevault:

```xml
<isDisabled>true</isDisabled>
```

A continuación se muestra un ejemplo de dónde colocar la configuración anterior en el pom.

```xml
<plugin>
    <groupId>org.apache.jackrabbit</groupId>
    <artifactId>filevault-package-maven-plugin</artifactId>
    ...
    <configuration>
    ...
        <validatorsSettings>
        ...
            <jackrabbit-nodetypes>
                <isDisabled>true</isDisabled>
            </jackrabbit-nodetypes>
        </validatorsSettings>
    </configuration>
</plugin>
```

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

A veces, se debe revertir un cambio en una definición de índice. Las razones podrían ser que se hizo por error o que ya no es necesario. Por ejemplo, la definición de índice `damAssetLucene-8-custom-3` se creó por error y ya está implementado. Por ello, es posible que desee volver a la definición de índice anterior, `damAssetLucene-8-custom-2`. Para ello, añada un índice llamado `damAssetLucene-8-custom-4` que contiene la definición del índice anterior, `damAssetLucene-8-custom-2`.

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
