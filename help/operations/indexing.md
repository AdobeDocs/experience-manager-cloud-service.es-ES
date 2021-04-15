---
title: Buscar contenido e indexar
description: Buscar contenido e indexar
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
translation-type: tm+mt
source-git-commit: 28c3fb4c5c0da175ee84463d7c100bdb1b93bb30
workflow-type: tm+mt
source-wordcount: '1738'
ht-degree: 2%

---

# Buscar contenido e indexar {#indexing}

## Cambios en AEM como Cloud Service {#changes-in-aem-as-a-cloud-service}

Con AEM como Cloud Service, el Adobe está pasando de un modelo AEM centrado en instancias a una vista basada en servicios con contenedores de AEM n-x, impulsada por canalizaciones de CI/CD en Cloud Manager. En lugar de configurar y mantener los índices en instancias de AEM único, la configuración de Índice debe especificarse antes de una implementación. Los cambios de configuración en la producción claramente están rompiendo las políticas CI/CD. Lo mismo ocurre con los cambios de índice, ya que pueden afectar a la estabilidad y al rendimiento del sistema si no se especifica, se prueban y se reindexan antes de llevarlos a la producción.

A continuación se muestra una lista de los principales cambios en comparación con AEM 6.5 y versiones anteriores:

1. Los usuarios ya no tendrán acceso al Administrador de índices de una sola instancia de AEM para depurar, configurar o mantener la indexación. Solo se utiliza para implementaciones locales y locales.

1. Los usuarios no cambiarán los índices en una única instancia de AEM ni tendrán que preocuparse por las comprobaciones de coherencia o la reindexación.

1. En general, los cambios de índice se inician antes de ir a producción para no eludir las puertas de enlace de calidad en las canalizaciones CI/CD de Cloud Manager y no tener impacto en los KPI empresariales en producción.

1. Todas las métricas relacionadas, incluido el rendimiento de búsqueda en producción, estarán disponibles para los clientes durante la ejecución para proporcionar una vista holística de los temas de Búsqueda e Indexación.

1. Los clientes podrán configurar alertas según sus necesidades.

1. Las EEM supervisan el estado del sistema las 24 horas del día, los 7 días de la semana y adoptarán las medidas necesarias y lo antes posible.

1. La configuración del índice se cambia mediante implementaciones. Los cambios en la definición del índice se configuran como otros cambios en el contenido.

1. En un nivel superior en AEM como Cloud Service, con la introducción del modelo de implementación [Blue-Green](#index-management-using-blue-green-deployments), existirán dos conjuntos de índices: un conjunto para la versión antigua (azul) y otro conjunto para la nueva versión (verde).

1. Los clientes pueden ver si el trabajo de indexación se ha completado en la página de creación de Cloud Manager y recibirán una notificación cuando la nueva versión esté lista para recibir tráfico.

1. Limitaciones: actualmente, la administración de índices en AEM as a Cloud Service solo se admite para índices de tipo lucene.

## Usos {#how-to-use}

La definición de índices puede comprender los tres casos de uso siguientes:

1. Adición de una nueva definición de índice de cliente
1. Actualización de una definición de índice existente. Esto significa añadir una nueva versión de una definición de índice existente
1. Eliminación de un índice existente redundante u obsoleto.

Para los puntos 1 y 2 anteriores, debe crear una nueva definición de índice como parte del código personalizado en la programación de versiones correspondiente de Cloud Manager. Para obtener más información, consulte la [Implementación para AEM como Cloud Service documentación](/help/implementing/deploying/overview.md).

### Preparación de la nueva definición de índice {#preparing-the-new-index-definition}

Debe preparar un nuevo paquete de definición de índice que contenga la definición de índice real, siguiendo este patrón de nomenclatura:

`<indexName>[-<productVersion>]-custom-<customVersion>`

que luego debe ir en `ui.apps/src/main/content/jcr_root`. Las carpetas raíz secundarias no son compatibles desde ahora.

El paquete del ejemplo anterior se crea como `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`.

### Implementación de definiciones de índice {#deploying-index-definitions}

>[!NOTE]
>
>Hay un problema conocido con Jackrabbit Filevault Maven Package Plugin versión **1.1.0** que no le permite agregar `oak:index` a los módulos de `<packageType>application</packageType>`. Para solucionarlo, utilice la versión **1.0.4**.

Las definiciones de índice ahora están marcadas como personalizadas y con versiones:

* La propia definición del índice (por ejemplo `/oak:index/ntBaseLucene-custom-1`)

Por lo tanto, para implementar un índice, la definición del índice (`/oak:index/definitionname`) debe entregarse a través de `ui.apps` a través de Git y del proceso de implementación de Cloud Manager.

Una vez añadida la nueva definición de índice, la nueva aplicación debe implementarse mediante Cloud Manager. Tras la implementación se inician dos trabajos, responsables de agregar (y combinar si es necesario) las definiciones de índice a MongoDB y Azure Segment Store para la creación y publicación, respectivamente. Los repositorios subyacentes se están reindexando con las nuevas definiciones de índice, antes de que tenga lugar el conmutador Blue-Green.

>[!TIP]
>
>Para obtener más información sobre la estructura del paquete necesaria para AEM como Cloud Service, consulte el documento [AEM Estructura del proyecto.](/help/implementing/developing/introduction/aem-project-content-package-structure.md)

## Administración de índices mediante implementaciones Blue-Green {#index-management-using-blue-green-deployments}

### ¿Qué es la Administración de índices {#what-is-index-management}

La administración de índices consiste en agregar, quitar y cambiar índices. Cambiar la *definición* de un índice es rápido, pero la aplicación del cambio (a menudo denominada &quot;creación de un índice&quot; o, para los índices existentes, &quot;reindexación&quot;) requiere tiempo. No es instantánea: el repositorio debe analizarse para indizar los datos.

### Qué es la implementación Blue-Green {#what-is-blue-green-deployment}

La implementación Blue-Green puede reducir el tiempo de inactividad. También permite realizar upgrades sin downtime y proporciona reversiones rápidas. La versión antigua de la aplicación (azul) se ejecuta al mismo tiempo que la nueva versión de la aplicación (verde).

### Áreas de solo lectura y lectura-escritura {#read-only-and-read-write-areas}

Algunas áreas del repositorio (partes de solo lectura del repositorio) pueden ser diferentes en la versión antigua (azul) y en la nueva (verde) versión de la aplicación. Las áreas de solo lectura del repositorio suelen ser &quot;`/app`&quot; y &quot;`/libs`&quot;. En el siguiente ejemplo, se utiliza cursiva para marcar áreas de solo lectura, mientras que negrita se utiliza para áreas de lectura-escritura.

* **/**
* */apps (solo lectura)*
* **/content**
* */libs (solo lectura)*
* **/oak:index**
* **/oak:index/acme.**
* **/jcr:system**
* **/system**
* **/var**

Las áreas de lectura y escritura del repositorio se comparten entre todas las versiones de la aplicación, mientras que para cada versión de la aplicación hay un conjunto específico de `/apps` y `/libs`.

### Administración de índices sin implementación Blue-Green {#index-management-without-blue-green-deployment}

Durante el desarrollo o al utilizar instalaciones locales, los índices se pueden añadir, eliminar o cambiar durante la ejecución. Los índices se utilizan en cuanto están disponibles. Si se supone que un índice no debe utilizarse en la versión antigua de la aplicación todavía, el índice se crea normalmente durante un tiempo de inactividad programado. Lo mismo ocurre cuando se elimina un índice o se cambia un índice existente. Al eliminar un índice, deja de estar disponible en cuanto se elimina.

### Administración de índices con implementación Blue-Green {#index-management-with-blue-green-deployment}

Con las implementaciones en azul y verde, no hay tiempo de inactividad. Sin embargo, para la administración de índices, esto requiere que los índices solo los usen ciertas versiones de la aplicación. Por ejemplo, al añadir un índice en la versión 2 de la aplicación, no desea que lo utilice la versión 1 de la aplicación aún. Al contrario, cuando se elimina un índice: en la versión 1 sigue siendo necesario incluir un índice eliminado en la versión 2. Al cambiar una definición de índice, queremos que la versión antigua del índice solo se utilice para la versión 1, y la nueva versión del índice solo para la versión 2.

La tabla siguiente muestra cinco definiciones de índice: el índice `cqPageLucene` se utiliza en ambas versiones, mientras que el índice `damAssetLucene-custom-1` solo se utiliza en la versión 2.

>[!NOTE]
>
>`<indexName>-custom-<customerVersionNumber>` es necesario para que AEM como Cloud Service lo marque como reemplazo de un índice existente.

| Índice | Índice predeterminado | Uso en la versión 1 | Uso en la versión 2 |
|---|---|---|---|
| /oak:index/damAssetLucene | Sí | Sí | No |
| /oak:index/damAssetLucene-custom-1 | Sí (personalizado) | No | Sí |
| /oak:index/acme.product-custom-1 | No | Sí | No |
| /oak:index/acme.product-custom-2 | No | No | Sí |
| /oak:index/cqPageLucene | Sí | Sí | Sí |

El número de versión se incrementa cada vez que se cambia el índice. Para evitar que los nombres de índice personalizados entren en conflicto con los nombres de índice del propio producto, los índices personalizados, así como los cambios en los índices fuera de la caja deben terminar con `-custom-<number>`.

### Cambios en los índices predeterminados {#changes-to-out-of-the-box-indexes}

Una vez que el Adobe cambia un índice listo para usar como &quot;damAssetLucene&quot; o &quot;cqPageLucene&quot;, se crea un nuevo índice denominado `damAssetLucene-2` o `cqPageLucene-2` o, si el índice ya se ha personalizado, la definición del índice personalizado se combina con los cambios en el índice predeterminado, como se muestra a continuación. La combinación de cambios se produce automáticamente. Esto significa que no es necesario que haga nada si cambia un índice predeterminado. Sin embargo, es posible volver a personalizar el índice más adelante.

| Índice | Índice predeterminado | Uso en la versión 2 | Uso en la versión 3 |
|---|---|---|---|
| /oak:index/damAssetLucene-custom-1 | Sí (personalizado) | Sí | No |
| /oak:index/damAssetLucene-2-custom-1 | Sí (se fusiona automáticamente desde damAssetLucene-custom-1 y damAssetLucene-2) | No | Sí |
| /oak:index/cqPageLucene | Sí | Sí | No |
| /oak:index/cqPageLucene-2 | Sí | No | Sí |

### Limitaciones actuales {#current-limitations}

Actualmente, la administración de índices solo se admite para índices de tipo `lucene`.

### Adición de un índice {#adding-an-index}

Para añadir un índice denominado `/oak:index/acme.product-custom-1` para utilizarlo en una nueva versión de la aplicación y posterior, el índice debe configurarse de la siguiente manera:

`acme.product-1-custom-1`

Esto funciona anteponiendo un identificador personalizado al nombre del índice, seguido de un punto (**`.`**). El identificador debe tener entre 2 y 5 caracteres de longitud.

Como se ha indicado anteriormente, esto garantiza que el índice solo sea utilizado por la nueva versión de la aplicación.

### Cambio de un índice {#changing-an-index}

Cuando se cambia un índice existente, es necesario agregar un nuevo índice con la definición de índice modificada. Por ejemplo, considere que se ha cambiado el índice existente `/oak:index/acme.product-custom-1`. El índice antiguo se almacena en `/oak:index/acme.product-custom-1` y el nuevo índice en `/oak:index/acme.product-custom-2`.

La versión antigua de la aplicación utiliza la siguiente configuración:

`/oak:index/acme.product-custom-1`

La nueva versión de la aplicación utiliza la siguiente configuración (modificada):

`/oak:index/acme.product-custom-2`

>[!NOTE]
>
>Es posible que las definiciones de índice de AEM como Cloud Service no coincidan completamente con las definiciones de índice de una instancia de desarrollo local. La instancia de desarrollo no tiene una configuración de Tika, mientras que AEM como instancias de Cloud Service sí tiene una. Si personaliza un índice con una configuración de Tika, mantenga la configuración de Tika.

### Deshacer un cambio {#undoing-a-change}

A veces, es necesario revertir un cambio en una definición de índice. Las razones podrían ser que se hizo un cambio por error o que ya no es necesario. Por ejemplo, la definición de índice `damAssetLucene-8-custom-3` se creó por error y ya está implementada. Por ello, es posible que desee volver a la definición de índice anterior `damAssetLucene-8-custom-2`. Para ello, debe agregar un nuevo índice llamado `damAssetLucene-8-custom-4` que contenga la definición del índice anterior, `damAssetLucene-8-custom-2`.

### Eliminación de un índice {#removing-an-index}

Lo siguiente solo se aplica a los índices personalizados. Los índices de productos no se pueden eliminar porque los AEM los utilizan.

Si se va a eliminar un índice en una versión posterior de la aplicación, se puede definir un índice vacío (un índice vacío que no se utiliza nunca y que no contiene datos), con un nombre nuevo. Para este ejemplo, puede asignarle el nombre `/oak:index/acme.product-custom-3`. Esto reemplaza el índice `/oak:index/acme.product-custom-2`. Una vez que el sistema elimina `/oak:index/acme.product-custom-2`, también se puede eliminar el índice vacío `/oak:index/acme.product-custom-3`. Un ejemplo de este índice vacío es:

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

Si ya no es necesario tener una personalización de un índice predeterminado, debe copiar la definición de índice predeterminada. Por ejemplo, si ya ha implementado `damAssetLucene-8-custom-3`, pero ya no necesita las personalizaciones y desea volver al índice `damAssetLucene-8` predeterminado, debe agregar un índice `damAssetLucene-8-custom-4` que contenga la definición de índice de `damAssetLucene-8`.

### Disponibilidad del índice y tolerancia a errores {#index-availability-and-fault-tolerance}

Se recomienda crear índices duplicados para las funciones que son importantes (teniendo en cuenta la convención de nomenclatura para los índices mencionados anteriormente), por lo que en el caso de corrupción de índices o cualquier evento imprevisto de este tipo, hay un índice de reserva disponible para responder a las consultas.
