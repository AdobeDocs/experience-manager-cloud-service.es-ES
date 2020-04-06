---
title: Búsqueda de contenido e indexación
description: 'Búsqueda de contenido e indexación '
translation-type: tm+mt
source-git-commit: 99dce041a6d7554785fd43eb82c671643e903f23

---


# Búsqueda de contenido e indexación {#indexing}

## Cambios en AEM como servicio de nube {#changes-in-aem-as-a-cloud-service}

Con AEM como servicio de nube, Adobe está pasando de un modelo centrado en la instancia de AEM a una vista basada en servicios con Contenedores AEM n-x, impulsados por canalizaciones de CD/CI en el Administrador de nube. En lugar de configurar y mantener índices en instancias de AEM únicas, la configuración de índice debe especificarse antes de la implementación. Los cambios de configuración en la producción están claramente rompiendo las políticas de CI/CD. Lo mismo se aplica a los cambios de índice, ya que pueden afectar a la estabilidad y el rendimiento del sistema si no se especifica, se prueban y se vuelven a indexar antes de llevarlos a la producción.

A continuación se muestra una lista de los principales cambios en comparación con AEM 6.5 y versiones anteriores:

1. Los usuarios ya no tendrán acceso al Administrador de índices de una sola instancia de AEM para depurar, configurar o mantener la indexación. Solo se utiliza para el desarrollo local y las implementaciones in situ.

1. Los usuarios no cambiarán los índices en una sola instancia de AEM ni tendrán que preocuparse por las comprobaciones de coherencia o el reindexado.

1. En general, los cambios en los índices se inician antes de ir a la producción para no eludir las puertas de enlace de calidad en las canalizaciones de CD/CI de Cloud Manager y no tener impacto en los KPI empresariales en la producción.

1. Todas las métricas relacionadas, incluido el rendimiento de búsqueda en producción, estarán disponibles para los clientes en tiempo de ejecución a fin de proporcionar la vista holística sobre los temas de búsqueda e indexación.

1. Los clientes podrán configurar alertas según sus necesidades.

1. Los ERS supervisan la salud del sistema las 24 horas del día, los 7 días de la semana y tomarán las medidas necesarias y lo antes posible.

1. La configuración del índice se cambia mediante implementaciones. Los cambios en la definición del índice se configuran como otros cambios en el contenido.

1. En un nivel elevado de AEM como servicio de nube, con la introducción del modelo [de implementación](#index-management-using-blue-green-deployments) azul-verde, existirán dos conjuntos de índices: un conjunto para la versión antigua (azul) y otro para la nueva versión (verde).

La versión del índice que se utiliza se configura mediante indicadores en las definiciones de índice a través del `useIfExist` indicador. Un índice solo puede utilizarse en una versión de la aplicación (por ejemplo, solo azul o solo verde) o en ambas versiones. Encontrará documentación detallada en Administración de [índices con implementaciones](#index-management-using-blue-green-deployments)Blue-Green.

1. Los clientes pueden ver si el trabajo de indexación se ha completado en la página de compilación de Cloud Manager y recibirán una notificación cuando la nueva versión esté lista para recibir tráfico.

1. Limitaciones: actualmente, la administración de índices en AEM como servicio de nube solo es compatible con índices de tipo lucene.

<!-- ## Sizing Considerations {#sizing-considerations}

AEM as a Cloud Service comes with a default capacity model to provide sufficient performance for average web applications. This "average" measure relates to the repository size and even more relevant to the indexing size. If we have reasons to believe that we need extended capacity for a specific customer project, an evaluation with SREs and Engineering will take place to determine the required capacity settings. 

AS NOTE: the above is internal for now.

-->

## Usos {#how-to-use}

La definición de índices puede incluir los tres casos de uso:

1. Añadir una nueva definición de índice de cliente
1. Actualizando una definición de índice existente. Esto significa en realidad añadir una nueva versión de una definición de índice existente
1. Eliminación de un índice existente que sea redundante u obsoleto.

Tanto para los puntos 1 como 2 anteriores, debe crear una nueva definición de índice como parte de su base de código personalizado en la programación de versiones correspondiente de Cloud Manager. Para obtener más información, consulte la documentación [](/help/implementing/deploying/overview.md)Implementación en AEM como un servicio de nube.

### Preparación de la nueva definición de índice {#preparing-the-new-index-definition}

Debe preparar un nuevo paquete de definición de índice que contenga la definición de índice real, siguiendo este patrón de nomenclatura:

`<indexName>[-<productVersion>]-custom-<customVersion>`

que luego debe pasar `ui.content/src/main/content/jcr_root`. Las carpetas raíz secundarias no son compatibles hasta ahora.

<!-- need to review and link info on naming convention from https://wiki.corp.adobe.com/display/WEM/Merging+Customer+and+OOTB+Index+Changes?focusedCommentId=1784917629#comment-1784917629 -->

El paquete de la muestra anterior se crea como `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`.

### Implementación de definiciones de índice {#deploying-index-definitions}

Las definiciones de índice ahora se marcan como personalizadas y con versiones:

* La definición de índice misma (por ejemplo `/oak:index/ntBaseLucene-custom-1`) que es contenido MUTABLE

Por lo tanto, para implementar un índice, la definición del índice (`/oak:index/definitionname`) debe entregarse a través del paquete **** mutable, generalmente `ui.content` a través de Git y del proceso de implementación de Cloud Manager.

Una vez que se agrega la nueva definición de índice, la nueva aplicación debe implementarse mediante Cloud Manager. Tras la implementación se inician dos trabajos, responsables de agregar (y combinar si es necesario) las definiciones de índice a MongoDB y Azure Segment Store para la creación y publicación, respectivamente. Los repositorios subyacentes se están reindexando con las nuevas definiciones de índice, antes de que tenga lugar el cambio Blue-Green.

## Administración de índices mediante implementaciones Blue-Green {#index-management-using-blue-green-deployments}

### ¿Qué es la administración de índices? {#what-is-index-management}

La administración de índices consiste en agregar, eliminar y cambiar índices. Cambiar la *definición* de un índice es rápido, pero la aplicación del cambio (a menudo llamado &quot;generar un índice&quot; o, para índices existentes, &quot;volver a indexar&quot;) requiere tiempo. No es instantánea: el repositorio debe analizarse para que los datos se indiquen.

### ¿Qué es la implementación azul-verde? {#what-is-blue-green-deployment}

La implementación Blue-Green puede reducir el tiempo de inactividad. También permite actualizaciones sin downtime y proporciona reversiones rápidas. La versión antigua de la aplicación (azul) se ejecuta al mismo tiempo que la nueva versión de la aplicación (verde).

### Áreas de solo lectura y escritura de lectura {#read-only-and-read-write-areas}

Determinadas áreas del repositorio (partes de sólo lectura del repositorio) pueden ser diferentes en la versión antigua (azul) y en la nueva (verde) de la aplicación. Las áreas de sólo lectura del repositorio suelen ser &quot;`/app`&quot; y &quot;`/libs`&quot;. En el siguiente ejemplo, se utiliza cursiva para marcar áreas de solo lectura, mientras que negrita para áreas de lectura y escritura.

* **/**
* */apps (solo lectura)*
* **/content**
* */libs (solo lectura)*
* **/oak:index**
* **/oak:index/acme**
* **/jcr:system**
* **/system**
* **/var**

Las áreas de lectura y escritura del repositorio se comparten entre todas las versiones de la aplicación, mientras que para cada versión de la aplicación hay un conjunto específico de `/apps` y `/libs`.

### Administración de índices sin implementación Blue-Green {#index-management-without-blue-green-deployment}

Durante el desarrollo, o cuando se utilizan instalaciones in situ, los índices se pueden agregar, eliminar o cambiar en tiempo de ejecución. Los índices se utilizan en cuanto están disponibles. Si un índice no debe utilizarse aún en la versión anterior de la aplicación, el índice se crea normalmente durante un tiempo de inactividad programado. Lo mismo ocurre cuando se elimina un índice o se cambia un índice existente. Al eliminar un índice, deja de estar disponible en cuanto se elimina.

### Administración De Índices Con Implementación Azul-Verde {#index-management-with-blue-green-deployment}

Con implementaciones en azul y verde, no hay tiempo de inactividad. Sin embargo, para la administración de índices, esto requiere que los índices solo sean utilizados por ciertas versiones de la aplicación. Por ejemplo, al agregar un índice en la versión 2 de la aplicación, no querrá que lo utilice la versión 1 de la aplicación. Lo contrario sucede cuando se elimina un índice: en la versión 1 sigue siendo necesario eliminar un índice en la versión 2. Al cambiar una definición de índice, queremos que la versión antigua del índice se utilice solamente para la versión 1, y que la nueva versión del índice se utilice solamente para la versión 2.

La siguiente tabla muestra 5 definiciones de índice: index `cqPageLucene` se utiliza en ambas versiones, mientras que index `damAssetLucene-custom-1` se utiliza únicamente en la versión 2.


> [!NOTE]
> `<indexName>-custom-<customerVersionNumber>` es necesario para que AEM como servicio de nube marque esto como un reemplazo de un índice existente.

| Índice | Índice listo para usar | Uso en la versión 1 | Uso en la versión 2 |
|---|---|---|---|
| /oak:index/damAssetLucene | Sí | Sí | No |
| /oak:index/damAssetLucene-custom-1 | Sí (personalizado) | No | Sí |
| /oak:index/acmeProduct-custom-1 | No | Sí | No |
| /oak:index/acmeProduct-custom-2 | No | No | Sí |
| /oak:index/cqPageLucene | Sí | Sí | Sí |

El número de versión se incrementa cada vez que se cambia el índice. Para evitar que los nombres de índice personalizados entren en conflicto con los nombres de índice del propio producto, es necesario que los índices personalizados, así como los cambios realizados en los índices predeterminados, terminen por `-custom-<number>`.

### Cambios en los índices predeterminados {#changes-to-out-of-the-box-indexes}

Una vez que Adobe cambia un índice listo para usar como &quot;damAssetLucene&quot; o &quot;cqPageLucene&quot;, se crea un nuevo índice denominado `damAssetLucene-2` o `cqPageLucene-2` se crea o, si el índice ya se ha personalizado, la definición del índice personalizado se combina con los cambios en el índice listo para usar, como se muestra a continuación. La combinación de cambios se produce automáticamente. Esto significa que no es necesario hacer nada si cambia un índice predeterminado. Sin embargo, es posible volver a personalizar el índice más tarde.

| Índice | Índice listo para usar | Uso en la versión 2 | Uso en la versión 3 |
|---|---|---|---|
| /oak:index/damAssetLucene-custom-1 | Sí (personalizado) | Sí | No |
| /oak:index/damAssetLucene-2-custom-1 | Sí (se combina automáticamente desde damAssetLucene-custom-1 y damAssetLucene-2) | No | Sí |
| /oak:index/cqPageLucene | Sí | Sí | No |
| /oak:index/cqPageLucene-2 | Sí | No | Sí |

### Restricciones      {#limitations}

Actualmente, la administración de índices solo se admite para índices de tipo `lucene`.

### Eliminación de un índice {#removing-an-index}

Si se va a eliminar un índice en una versión posterior de la aplicación, puede definir un índice vacío (un índice sin datos para indexar), con un nombre nuevo. Por ejemplo, puede asignarle un nombre `/oak:index/acmeProduct-custom-3`. Esto reemplaza al índice `/oak:index/acmeProduct-custom-2`. Una vez que `/oak:index/acmeProduct-custom-2` el sistema lo elimina, también se `/oak:index/acmeProduct-custom-3` puede eliminar el índice vacío.

### Añadir un índice {#adding-an-index}

Para agregar un índice denominado &quot;/oak:index/acmeProduct-custom-1&quot; para utilizarlo en una nueva versión de la aplicación y posterior, el índice debe configurarse de la siguiente manera:

`/oak:index/acmeProduct-custom-1`

Como se ha indicado anteriormente, esto garantiza que la nueva versión de la aplicación solo utilice el índice.

### Cambio de un índice {#changing-an-index}

Cuando se cambia un índice existente, se debe agregar un nuevo índice con la definición de índice modificada. Por ejemplo, piense en que se ha cambiado el índice existente &quot;/oak:index/acmeProduct-custom-1&quot;. El índice antiguo se almacena en `/oak:index/acmeProduct-custom-1`y el nuevo índice se almacena en `/oak:index/acmeProduct-custom-2`.

La versión anterior de la aplicación utiliza la siguiente configuración:

`/oak:index/acmeProduct-custom-1`

La nueva versión de la aplicación utiliza la siguiente configuración (modificada):

`/oak:index/acmeProduct-custom-2`