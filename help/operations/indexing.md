---
title: Búsqueda de contenido e indexación
description: Búsqueda de contenido e indexación
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
source-git-commit: 6fd5f8e7a9699f60457e232bb3cfa011f34880e9
workflow-type: tm+mt
source-wordcount: '2498'
ht-degree: 87%

---

# Búsqueda de contenido e indexación {#indexing}

## Cambios en AEM as a Cloud Service {#changes-in-aem-as-a-cloud-service}

Con AEM as a Cloud Service, Adobe se aleja de un modelo de AEM centrado en instancias y se acerca a una vista basada en servicios con contenedores de AEM n-x, impulsada por canalizaciones de CI/CD en Cloud Manager. En lugar de configurar y mantener los índices en instancias de AEM únicas, la configuración de Índice debe especificarse antes de una implementación. Los cambios de configuración en la producción están violando de forma clara las políticas CI/CD. Lo mismo ocurre con los cambios de índice, ya que pueden afectar a la estabilidad y al rendimiento del sistema si no se especifican, se prueban y se reindexan antes de llevarlos a la producción.

A continuación se muestra una lista de los principales cambios en comparación con la versión 6.5 y versiones anteriores de AEM:

1. Los usuarios ya no tendrán acceso al Administrador de índices de una sola instancia de AEM para depurar, configurar o mantener la indexación. Solo se utiliza para implementaciones y desarrollos locales.
1. Los usuarios no cambiarán los índices en una única instancia de AEM ni tendrán que preocuparse por las comprobaciones de coherencia o la reindexación.
1. En general, los cambios de índice se inician antes de ir a producción para no eludir las puertas de enlace de calidad en las canalizaciones CI/CD de Cloud Manager y no tener impacto en los KPI empresariales en producción.
1. Todas las métricas relacionadas, incluido el rendimiento de búsqueda en producción, estarán disponibles para los clientes en tiempo de ejecución para proporcionar una vista integral de los temas de Búsqueda e Indexación.
1. Los clientes podrán configurar alertas según sus necesidades.
1. Los SRE supervisan el estado del sistema las 24 horas del día y los siete días de la semana, y adoptarán las medidas necesarias lo antes posible.
1. La configuración del índice se cambia mediante implementaciones. Los cambios en la definición del índice se configuran como otros cambios en el contenido.
1. A un nivel alto sobre AEM as a Cloud Service, con la introducción del [Modelo de implementación azul-verde](#index-management-using-blue-green-deployments), existirán dos conjuntos de índices: un conjunto para la versión antigua (azul) y otro para la nueva (verde).
1. Los clientes pueden ver si el trabajo de indexación se ha completado en la página de creación de Cloud Manager y recibirán una notificación cuando la nueva versión esté lista para admitir tráfico.

Restricciones:

* En la actualidad, la administración de índices en AEM as a Cloud Service solo se admite para índices de tipo `lucene`.
* Solo se admiten analizadores estándar (es decir, aquellos que se envían con el producto). No se admiten analizadores personalizados.
* Internamente, se pueden configurar y utilizar otros índices para las consultas. Por ejemplo, las consultas que se escriben en relación con el índice `damAssetLucene`, en Skyline, podrían ejecutarse con una versión Elasticsearch de este. Esta diferencia no suele ser visible para la aplicación y el usuario, aunque algunas herramientas, como la funcionalidad `explain`, reportarán un índice diferente. Para ver las diferencias entre los índices de Lucene y los de Elastic, consulte [la documentación de Elastic en Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/query/elastic.html). Los clientes no necesitan ni pueden configurar los índices de Elasticsearch directamente.

## Usos {#how-to-use}

La definición de índices puede incluir los tres casos de uso siguientes:

1. Adición de una nueva definición de índice de cliente.
1. Actualización de una definición de índice existente. Esto significa añadir una nueva versión de una definición de índice existente.
1. Eliminación de un índice redundante u obsoleto.

Para los puntos 1 y 2 anteriores, debe crear una nueva definición de índice como parte del código personalizado en la programación de versiones correspondiente de Cloud Manager. Para obtener más información, consulte la [Implementación en la documentación de AEM as a Cloud Service](/help/implementing/deploying/overview.md).

## Nombres de índice {#index-names}

Una definición de índice puede ser la siguiente:

1. Un índice predeterminado. Un ejemplo es `/oak:index/cqPageLucene-2`.
1. Una personalización de un índice predeterminado. El cliente define estas personalizaciones. Un ejemplo es `/oak:index/cqPageLucene-2-custom-1`.
1. Un índice totalmente personalizado. Un ejemplo es `/oak:index/acme.product-1-custom-2`. Para evitar conflictos de nombres, es necesario que los índices totalmente personalizados tengan un prefijo, por ejemplo, `acme.`

Tenga en cuenta que tanto la personalización de un índice predeterminado como los índices totalmente personalizados deben contener `-custom-`. Solo los índices totalmente personalizados deben comenzar con un prefijo.

## Preparación de la nueva definición de índice {#preparing-the-new-index-definition}

>[!NOTE]
>
>Si personaliza un índice predeterminado, como `damAssetLucene-6`, copie la última definición de índice lista para usarse de un *entorno de Cloud Service* con el Administrador de paquetes CRX DE (`/crx/packmgr/`). A continuación, cambie el nombre de la configuración, por ejemplo, a `damAssetLucene-6-custom-1`. Añada sus personalizaciones en la parte superior. Esto garantiza que las configuraciones necesarias no se eliminen de forma involuntaria. Por ejemplo, el nodo `tika` bajo `/oak:index/damAssetLucene-6/tika` es necesario en el índice personalizado del servicio en la nube. No existe en el SDK de la nube.

Debe preparar un nuevo paquete de definición de índice que contenga la definición de índice real, con este patrón de nomenclatura:

`<indexName>[-<productVersion>]-custom-<customVersion>`

que luego debe ir bajo `ui.apps/src/main/content/jcr_root`. Todas las definiciones de índice personalizadas deben almacenarse en `/oak:index`.

El filtro del paquete debe configurarse de modo que los índices existentes (predeterminados) se mantengan. En el archivo `ui.apps/src/main/content/META-INF/vault/filter.xml`, cada índice personalizado debe enumerarse, por ejemplo, como `<filter root="/oak:index/damAssetLucene-6-custom-1"/>`. Si la versión del índice cambia posteriormente, es necesario ajustar el filtro.

<!-- Alexandru: temporarily drafting this statement due to CQDOC-17701

The package from the above sample is built as `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`. -->

>[!NOTE]
>
>Cualquier paquete de contenido que contenga definiciones de índice debe tener la siguiente propiedad establecida en el archivo de propiedades del paquete de contenido, ubicado en `/META-INF/vault/properties.xml`:
>
>`noIntermediateSaves=true`

## Implementación de definiciones de índice {#deploying-index-definitions}

Las definiciones de índice están marcadas como personalizadas y con versiones:

* La definición del índice en sí (por ejemplo `/oak:index/ntBaseLucene-custom-1`)

Para implementar un índice personalizado, la definición del índice (`/oak:index/definitionname`) debe entregarse mediante `ui.apps` mediante Git y el proceso de implementación de Cloud Manager. En el filtro FileVault, por ejemplo, `ui.apps/src/main/content/META-INF/vault/filter.xml`, enumere cada índice personalizado individualmente, por ejemplo `<filter root="/oak:index/damAssetLucene-7-custom-1"/>`. La definición de índice personalizada se almacenará en el archivo `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-7-custom-1/.content.xml`, como se indica a continuación:

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

Dependiendo de la versión del complemento de paquete Jackrabbit Filevault Maven que se use, se requiere algo más de configuración en el proyecto. Cuando se utiliza la versión del complemento de paquete Jackrabbit Filevault Maven **1.1.6** o posterior, el archivo `pom.xml` debe contener la siguiente sección en la configuración del complemento para `filevault-package-maven-plugin`, en `configuration/validatorsSettings` (justo antes de `jackrabbit-nodetypes`):

```xml
<jackrabbit-packagetype>
    <options>
        <immutableRootNodeNames>apps,libs,oak:index</immutableRootNodeNames>
    </options>
</jackrabbit-packagetype>
```

Además, en este caso, la versión `vault-validation` debe actualizarse a una versión más reciente:

```xml
<dependency>
    <groupId>org.apache.jackrabbit.vault</groupId>
    <artifactId>vault-validation</artifactId>
    <version>3.5.6</version>
</dependency>
```

A continuación, en `ui.apps.structure/pom.xml` y `ui.apps/pom.xml`, la configuración del `filevault-package-maven-plugin` necesita tener `allowIndexDefinitions` así como `noIntermediateSaves` activada. La opción `noIntermediateSaves` garantiza que las configuraciones de índice se añadan automáticamente.

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

En `ui.apps.structure/pom.xml`, la sección `filters` para este complemento debe contener una raíz de filtro como se indica a continuación:

```xml
<filter><root>/oak:index</root></filter>
```

Una vez añadida la nueva definición de índice, la nueva aplicación debe implementarse mediante Cloud Manager. Tras la implementación se inician dos trabajos, responsables de añadir (y combinar si es necesario) las definiciones de índice a MongoDB y Azure Segment Store para la creación y publicación, respectivamente. Los repositorios subyacentes se están reindexando con las nuevas definiciones de índice, antes de que tenga lugar el cambio azul-verde.

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
>Para obtener más información sobre la estructura de paquetes necesaria para AEM as a Cloud Service, consulte el documento [Estructura del proyecto de AEM.](/help/implementing/developing/introduction/aem-project-content-package-structure.md)

## Administración de índices mediante implementaciones azul-verde {#index-management-using-blue-green-deployments}

### Qué es la administración de índices {#what-is-index-management}

La administración de índices consiste en añadir, quitar y cambiar índices. Cambiar la *definición* de un índice es rápido, pero la aplicación del cambio (a menudo llamado “creación de un índice” o, para los índices existentes, “reindexación”) requiere tiempo. No es instantáneo: el repositorio debe analizarse para indexar los datos.

### Qué es la implementación azul-verde {#what-is-blue-green-deployment}

La implementación azul-verde puede reducir el tiempo de inactividad. También permite llevar a cabo actualizaciones sin tiempo de inactividad y proporciona reversiones rápidas. La versión antigua de la aplicación (azul) se ejecuta al mismo tiempo que la nueva (verde).

### Áreas de solo lectura y de lectura-escritura {#read-only-and-read-write-areas}

Algunas áreas del repositorio (partes de solo lectura) pueden ser diferentes en la versión antigua (azul) y en la nueva (verde) de la aplicación. Las áreas de solo lectura del repositorio suelen ser “`/app`” y “`/libs`”. En el siguiente ejemplo, se utiliza la cursiva para marcar las áreas de solo lectura, y la negrita para las de lectura-escritura.

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

### Administración de índices sin implementación azul-verde {#index-management-without-blue-green-deployment}

Durante el desarrollo o al utilizar instalaciones locales, los índices se pueden añadir, eliminar o cambiar en tiempo de ejecución. Los índices se utilizan en cuanto están disponibles. Si se supone que un índice no se va a utilizar todavía en la versión antigua de la aplicación, se suele construir durante un tiempo de inactividad programado. Lo mismo ocurre cuando se elimina un índice o se cambia uno existente. Al eliminar un índice, deja de estar disponible en ese mismo momento.

### Administración de índices con implementación azul-verde {#index-management-with-blue-green-deployment}

Con las implementaciones azul-verde, no hay tiempo de inactividad. En una actualización, durante algún tiempo, tanto la versión antigua (por ejemplo, la 1) de la aplicación, como la nueva (2), se ejecutan a la vez en el mismo repositorio. Si la versión 1 requiere que haya un determinado índice disponible, este no debe eliminarse en la 2: debe suprimirse más adelante (por ejemplo, en la 3), momento en el que se garantiza que la versión 1 de la aplicación ya no se está ejecutando. Además, las aplicaciones deben escribirse de tal manera que la versión 1 funcione bien, incluso si la 2 se está ejecutando y hay índices de ella disponibles.

Una vez completada la actualización a la nueva versión, el sistema puede retirar los índices antiguos. Es posible que los índices antiguos se mantengan durante algún tiempo para acelerar las reversiones (si fueran necesarias).

La tabla siguiente muestra cinco definiciones de índice: `cqPageLucene` se utiliza en ambas versiones, mientras que `damAssetLucene-custom-1` solo en la 2.

>[!NOTE]
>
>`<indexName>-custom-<customerVersionNumber>` es necesario para que AEM as a Cloud Service marque esto como reemplazo de un índice existente.

| Índice | Índice predeterminado | Uso en la versión 1 | Uso en la versión 2 |
|---|---|---|---|
| /oak:index/damAssetLucene | Sí | Sí | No |
| /oak:index/damAssetLucene-custom-1 | Sí (personalizado) | No | Sí |
| /oak:index/acme.product-custom-1 | No | Sí | No |
| /oak:index/acme.product-custom-2 | No | No | Sí |
| /oak:index/cqPageLucene | Sí | Sí | Sí |

El número de versión se incrementa cada vez que se cambia el índice. Para evitar que los nombres de índice personalizados entren en conflicto con los nombres de índice del propio producto, los índices personalizados, así como los cambios en los índices externos, deben terminar con `-custom-<number>`.

### Cambios en los índices predeterminados {#changes-to-out-of-the-box-indexes}

Una vez que Adobe cambia un índice predeterminado como “damAssetLucene” o “cqPageLucene”, se crea un nuevo índice denominado `damAssetLucene-2` o `cqPageLucene-2`. O, si el índice ya se ha personalizado, la definición del índice personalizado se combina con los cambios en el índice predeterminado, como se muestra a continuación. La fusión de los cambios se produce de forma automática. Esto significa que no es necesario que haga nada si un índice predeterminado cambia. Sin embargo, es posible volver a personalizar el índice más adelante.

| Índice | Índice predeterminado | Uso en la versión 2 | Uso en la versión 3 |
|---|---|---|---|
| /oak:index/damAssetLucene-custom-1 | Sí (personalizado) | Sí | No |
| /oak:index/damAssetLucene-2-custom-1 | Sí (se fusiona automáticamente desde damAssetLucene-custom-1 y damAssetLucene-2) | No | Sí |
| /oak:index/cqPageLucene | Sí | Sí | No |
| /oak:index/cqPageLucene-2 | Sí | No | Sí |

### Limitaciones actuales {#current-limitations}

Actualmente, la administración de índices solo es compatible con índices del tipo `lucene`, con `compatVersion` establezca en `2`. Internamente, se pueden configurar otros índices y utilizarse para consultas, por ejemplo índices de Elasticsearch. Consultas que se escriben en relación con `damAssetLucene` AEM index podría, en el caso de que esté as a Cloud Service, ejecutarse con una versión de Elasticsearch de este índice. Esta diferencia es invisible para el usuario final de la aplicación, aunque algunas herramientas, como la `explain` reportará un índice diferente. Para ver las diferencias entre los índices de Lucene y Elasticsearch, consulte [la documentación del Elasticsearch en Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/query/elastic.html). Los clientes no pueden y no necesitan configurar índices de Elasticsearch directamente.

Solo se admiten analizadores integrados (es decir, aquellos que se envían con el producto). No se admiten analizadores personalizados.

Para obtener el mejor rendimiento operativo, los índices no deben ser excesivamente grandes. El tamaño total de todos los índices puede utilizarse como guía: Si esto aumenta en más del 100 % después de agregar índices personalizados y de ajustar índices estándar en un entorno de desarrollo, se deben ajustar definiciones de índices personalizadas. AEM Los as a Cloud Service pueden evitar la implementación de índices que afectarían negativamente a la estabilidad y el rendimiento del sistema.

### Adición de un índice {#adding-an-index}

Para añadir un índice totalmente personalizado llamado `/oak:index/acme.product-custom-1` y utilizarlo en una nueva versión de la aplicación y más adelante, el índice debe configurarse de la siguiente manera:

`acme.product-1-custom-1`

Esto funciona anteponiendo un identificador personalizado al nombre del índice, seguido de un punto (**`.`**). El identificador debe tener entre dos y cinco caracteres de longitud.

Como en el caso anterior, esto garantiza que el índice solo lo utilice la nueva versión de la aplicación.

### Cambio de un índice {#changing-an-index}

Cuando se cambia un índice existente, es necesario añadir uno nuevo con la definición de índice modificada. Por ejemplo, considere que el índice existente `/oak:index/acme.product-custom-1` cambia. El índice antiguo se almacena en `/oak:index/acme.product-custom-1` y el nuevo, en `/oak:index/acme.product-custom-2`.

La versión antigua de la aplicación utiliza la siguiente configuración:

`/oak:index/acme.product-custom-1`

La nueva versión de la aplicación utiliza la siguiente configuración (modificada):

`/oak:index/acme.product-custom-2`

>[!NOTE]
>
>Es posible que las definiciones de índice de AEM as a Cloud Service no coincidan por completo con las de una instancia de desarrollo local. La instancia de desarrollo no tiene una configuración de Tika, mientras que las instancias de AEM as a Cloud Service, sí. Si personaliza un índice con una configuración de Tika, manténgala.

### Anulación de un cambio {#undoing-a-change}

A veces, es necesario revertir un cambio en una definición de índice. Las razones podrían ser que se hizo por error o que ya no es necesario. Por ejemplo, la definición de índice `damAssetLucene-8-custom-3` se creó por error y ya está implementado. Por ello, es posible que desee volver a la definición de índice anterior, `damAssetLucene-8-custom-2`. Para ello, debe añadir un nuevo índice denominado `damAssetLucene-8-custom-4`, que contiene la definición del índice anterior, `damAssetLucene-8-custom-2`.

### Eliminación de un índice {#removing-an-index}

Lo siguiente solo se aplica a los índices personalizados. Los índices de productos no se pueden eliminar porque los utiliza AEM.

Si se va a eliminar un índice en una versión posterior de la aplicación, se puede definir un índice vacío (que no se utiliza nunca y que no contiene datos), con un nombre nuevo. Para este ejemplo, puede llamarlo `/oak:index/acme.product-custom-3`. Esto reemplaza al índice `/oak:index/acme.product-custom-2`. Una vez que el sistema elimine `/oak:index/acme.product-custom-2`, el índice vacío `/oak:index/acme.product-custom-3` también se puede suprimir. Un ejemplo de este índice vacío es el siguiente:

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

Consulte lo siguiente [este documento](query-and-indexing-best-practices.md) para obtener información sobre cómo se pueden optimizar las consultas y los índices.
