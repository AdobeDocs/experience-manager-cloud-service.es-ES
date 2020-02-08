---
title: Guía de ajuste del rendimiento de los recursos
description: Áreas de enfoque clave en la configuración de AEM, cambios en hardware, software y componentes de red para eliminar cuellos de botella y optimizar el rendimiento de Recursos AEM.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Guía de ajuste del rendimiento de los recursos{#assets-performance-tuning-guide}

La configuración de Recursos Adobe Experience Manager (AEM) contiene varios componentes de hardware, software y red. Según el escenario de implementación, es posible que necesite cambios específicos en la configuración de hardware, software y componentes de red para eliminar los cuellos de botella de rendimiento.

Además, la identificación y el cumplimiento de determinadas directrices de optimización de hardware y software ayuda a crear una base sólida que permite que la implementación de AEM Assets satisfaga las expectativas de rendimiento, escalabilidad y fiabilidad.

El bajo rendimiento de Recursos AEM puede afectar a la experiencia del usuario en cuanto al rendimiento interactivo, el procesamiento de recursos, la velocidad de descarga y otras áreas.

De hecho, la optimización del rendimiento es una tarea fundamental que se realiza antes de establecer métricas de objetivo para cualquier proyecto.

A continuación se indican algunas áreas de enfoque clave en las que se detectan y corrigen los problemas de rendimiento antes de que afecten a los usuarios.

## Plataforma {#platform}

Aunque AEM es compatible con varias plataformas, Adobe ha encontrado la mayor compatibilidad con herramientas nativas en Linux y Windows, lo que contribuye a un rendimiento óptimo y a una implementación más sencilla. Lo ideal es implementar un sistema operativo de 64 bits para cumplir los requisitos de memoria alta de una implementación de AEM Assets. Al igual que con cualquier implementación de AEM, debe implementar TarMK siempre que sea posible. Aunque TarMK no puede escalar más allá de una sola instancia de autor, se ha descubierto que funciona mejor que MongoMK. Puede añadir instancias de descarga de TarMK para aumentar el poder de procesamiento del flujo de trabajo de la implementación de AEM Assets.

### Carpeta temporal {#temp-folder}

Para mejorar los tiempos de carga de recursos, utilice almacenamiento de alto rendimiento para el directorio temporal de Java. En Linux y Windows, se puede utilizar una unidad RAM o SSD. En entornos basados en la nube, se podría utilizar un tipo de almacenamiento de alta velocidad equivalente. Por ejemplo, en Amazon EC2, se puede utilizar una unidad [&quot;efímero&quot;](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) para la carpeta temp.

Si el servidor tiene una memoria amplia, configure una unidad de RAM. En Linux, ejecute estos comandos para crear una unidad de RAM de 8 GB:

```
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

En el sistema operativo Windows, tendría que utilizar un controlador de terceros para crear una unidad de RAM o simplemente usar almacenamiento de alto rendimiento como SSD.

Una vez que el volumen temporal de alto rendimiento esté listo, establezca el parámetro JVM -Djava.io.tmpdir. Por ejemplo, puede agregar el parámetro JVM siguiente a la variable CQ_JVM_OPTS en la secuencia de comandos bin/start de AEM:

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Configuración de Java {#java-configuration}

### Versión de Java {#java-version}

Dado que Oracle dejó de publicar actualizaciones para Java 7 a partir de abril de 2015, Adobe recomienda implementar Recursos AEM en Java 8. En algunos casos, ha demostrado un mejor rendimiento.

### Parámetros de JVM {#jvm-parameters}

Debe establecer los siguientes parámetros de JVM:

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=verdadero

## Almacenamiento de datos y configuración de memoria {#data-store-and-memory-configuration}

### Configuración del almacén de datos de archivos {#file-data-store-configuration}

Se recomienda separar el almacén de datos del almacén de segmentos para todos los usuarios de Recursos AEM. Además, la configuración de los parámetros `maxCachedBinarySize` y `cacheSizeInMB` puede ayudar a maximizar el rendimiento. Establezca `maxCachedBinarySize` el tamaño de archivo más pequeño que se puede guardar en la caché. Especifique el tamaño de la caché en memoria que se va a usar para el almacén de datos dentro de `cacheSizeInMB`. Adobe recomienda configurar este valor entre el 2 y el 10 por ciento del tamaño total del montón. Sin embargo, las pruebas de carga y rendimiento pueden ayudar a determinar la configuración ideal.

### Configurar el tamaño máximo de la caché de imágenes en búfer {#configure-the-maximum-size-of-the-buffered-image-cache}

Al cargar grandes cantidades de recursos en Adobe Experience Manager, para permitir picos inesperados en el consumo de memoria y evitar que JVM falle con OutOfMemoryErrors, reduzca el tamaño máximo configurado de la caché de imágenes en búfer. Considere un ejemplo en el que tiene un sistema con una pila máxima (- `Xmx`param) de 5 GB, un Oak BlobCache establecido en 1 GB y una caché de documentos establecida en 2 GB. En este caso, la memoria caché almacenada en el búfer requeriría un máximo de 1,25 GB y memoria, lo que dejaría sólo 0,75 GB de memoria para picos inesperados.

Configure el tamaño de caché en búfer en la consola web OSGi. En `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`, establezca la propiedad `cq.dam.image.cache.max.memory` en bytes. Por ejemplo, 1073741824 es 1 GB (1024 x 1024 x 1024 = 1 GB).

Desde AEM 6.1 SP1, si está utilizando un `sling:osgiConfig` nodo para configurar esta propiedad, asegúrese de establecer el tipo de datos en Long. Para obtener más información, consulte [CQBufferedImageCache consume mucha información durante las cargas](https://helpx.adobe.com/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html)de recursos.

### Almacenes de datos compartidos {#shared-data-stores}

La implementación de un almacén de datos de archivos compartidos o S3 puede ayudar a ahorrar espacio en disco y aumentar el rendimiento de la red en implementaciones a gran escala.

### S3 data store {#s-data-store}

La siguiente configuración del almacén de datos S3 ( `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`) ayudó a Adobe a extraer 12,8 TB de objetos binarios grandes (BLOB) de un almacén de datos de archivos existente en un almacén de datos S3 en un sitio del cliente:

```
accessKey=<snip>
 secretKey=<snip>
 s3Bucket=<snip>
 s3Region=us-standard
 s3EndPoint=<a href="https://s3.amazonaws.com/">s3.amazonaws.com</a>
 connectionTimeout=120000
 socketTimeout=120000
 maxConnections=80
 writeThreads=60
 concurrentUploadsThreads=30
 asyncUploadLimit=30
 maxErrorRetry=1000
 path=/opt/author/crx-quickstart/repository/datastore
 s3RenameKeys=false
 s3Encryption=SSE_S3
 proactiveCaching=true
 uploadRetries=1000
 migrateFailuresCount=400
```

## Optimización de la red {#network-optimization}

Adobe recomienda habilitar HTTPS porque muchas empresas tienen servidores de seguridad que detectan el tráfico HTTP, lo que afecta negativamente a las cargas y corrompe los archivos. Para cargas de archivos de gran tamaño, asegúrese de que los usuarios tienen conexiones cableadas a la red porque una red WiFi se satura rápidamente. Para evaluar el rendimiento de la red mediante el análisis de la topología de la red, consulte Consideraciones [de la red de](/help/assets/assets-network-considerations.md)recursos.

Principalmente, la estrategia de optimización de red depende de la cantidad de ancho de banda disponible y de la carga de la instancia de AEM. Las opciones de configuración comunes, incluyendo servidores de seguridad o proxies, pueden ayudar a mejorar el rendimiento de la red. Estos son algunos de los puntos clave a tener en cuenta:

* Según el tipo de instancia (pequeña, moderada y grande), asegúrese de que dispone de ancho de banda de red suficiente para su instancia de AEM. La asignación adecuada del ancho de banda es especialmente importante si AEM está alojado en AWS.
* Si la instancia de AEM está alojada en AWS, puede beneficiarse de una política de escala versátil. Actualice la instancia si los usuarios esperan una carga alta. Disminuya el tamaño para una carga moderada o baja.
* HTTPS: La mayoría de los usuarios tiene servidores de seguridad que detectan el tráfico HTTP, lo que puede afectar negativamente a la carga de archivos o incluso dañar archivos durante la operación de carga.
* Cargas de archivos grandes: Asegúrese de que los usuarios tienen conexiones cableadas a la red (las conexiones Wi-Fi se saturan rápidamente).

## Flujos de trabajo {#workflows}

### Flujos de trabajo transitorios {#transient-workflows}

Siempre que sea posible, establezca el flujo de trabajo de recursos de actualización de DAM en Temporal. La configuración reduce considerablemente los gastos generales necesarios para procesar los flujos de trabajo porque, en este caso, los flujos de trabajo no tienen que pasar por los procesos normales de seguimiento y archivo.

>[!NOTE]
>
>De forma predeterminada, el flujo de trabajo de recursos de actualización de DAM se establece en Temporal en AEM 6.3. En este caso, puede omitir el siguiente procedimiento.

1. Vaya a */miscadmin* en la instancia de AEM que va a configurar (por ejemplo, [https://localhost:4502/miscadmin)](https://localhost:4502/miscadmin)).
1. En el árbol de navegación, expanda **Herramientas** > **Flujo de trabajo** > **Modelos** > **presa**.
1. Haga doble clic en **DAM Update Asset**.
1. En el panel de herramientas flotante, cambie a la ficha **Página** y, a continuación, haga clic en Propiedades **de página...**
1. Seleccione Flujo de trabajo **transitorio** y, a continuación, haga clic en **Aceptar**.

   >[!NOTE]
   >
   >Algunas funciones no admiten flujos de trabajo transitorios. Si la implementación de AEM Assets requiere estas funciones, no configure flujos de trabajo transitorios.

   En los casos en los que no se puedan utilizar flujos de trabajo transitorios, ejecute la depuración de flujo de trabajo con regularidad para eliminar flujos de trabajo de recursos de actualización DAM archivados para garantizar que el rendimiento del sistema no se deteriore.

   Normalmente, los flujos de trabajo de depuración se ejecutan semanalmente. Sin embargo, en situaciones de uso intensivo de recursos, como durante la ingestión de recursos a gran escala, puede ejecutarlo con más frecuencia.

   Para configurar la depuración del flujo de trabajo, agregue una nueva configuración de depuración del flujo de trabajo de Adobe Granite a través de la consola OSGi. A continuación, configure y programe el flujo de trabajo como parte de la ventana de mantenimiento semanal.

   Si la purga dura demasiado tiempo, se agota el tiempo de espera. Por lo tanto, debe asegurarse de que los trabajos de depuración se completan para evitar situaciones en las que los flujos de trabajo de depuración no se completan debido al gran número de flujos de trabajo.

   Por ejemplo, después de ejecutar numerosos flujos de trabajo no transitorios (que crean nodos de instancia de flujo de trabajo), puede ejecutar [ACS AEM Commons Workflow Remover](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) de forma ad-hoc. Elimina inmediatamente las instancias de flujo de trabajo redundantes y completadas en lugar de esperar a que se ejecute el programador de purga de flujo de trabajo de Adobe Granite.

### Número máximo de trabajos en paralelo {#maximum-parallel-jobs}

De forma predeterminada, AEM ejecuta un número máximo de trabajos paralelos igual al número de procesadores del servidor. El problema con esta configuración es que durante períodos de carga pesada, todos los procesadores están ocupados por flujos de trabajo de recursos de actualización de DAM, lo que ralentiza la capacidad de respuesta de la interfaz de usuario e impide que AEM ejecute otros procesos que salvaguardan el rendimiento y la estabilidad del servidor. Como práctica recomendada, ajuste este valor a la mitad de los procesadores disponibles en el servidor realizando los siguientes pasos:

1. En AEM Author, vaya a [https://localhost:4502/system/console/slingevent](https://localhost:4702/system/console/slingevent).
1. Haga clic en Editar en cada cola de flujo de trabajo que sea relevante para la implementación, por ejemplo, Granite Transient Workflow Queue.
1. Cambie el valor de Número máximo de trabajos paralelos y haga clic en Guardar.

Establecer una cola para la mitad de los procesadores disponibles es una solución viable para empezar. Sin embargo, es posible que tenga que aumentar o disminuir este número para lograr el máximo rendimiento y ajustarlo por entorno. Hay colas independientes para flujos de trabajo transitorios y no transitorios, así como para otros procesos, como los flujos de trabajo externos. Si varias colas configuradas en el 50% de los procesadores están activas simultáneamente, el sistema puede sobrecargarse rápidamente. Las colas que se utilizan con frecuencia varían considerablemente según las implementaciones de los usuarios. Por lo tanto, es posible que tenga que configurarlas cuidadosamente para lograr la máxima eficacia sin sacrificar la estabilidad del servidor.

### Configuración del recurso de actualización DAM {#dam-update-asset-configuration}

El flujo de trabajo de recursos de actualización de DAM contiene un conjunto completo de pasos configurados para tareas como la generación de PTIFF de Scene7 y la integración de InDesign Server. Sin embargo, es posible que la mayoría de los usuarios no requieran varios de estos pasos. Adobe recomienda crear una copia personalizada del modelo de flujo de trabajo de recursos de actualización de DAM y eliminar los pasos innecesarios. En este caso, actualice los lanzadores de DAM Update Asset para que apunten al nuevo modelo.

>[!NOTE]
>
>La ejecución intensiva del flujo de trabajo de recursos de actualización de DAM puede aumentar considerablemente el tamaño del almacén de datos de archivos. Los resultados de un experimento realizado por Adobe han demostrado que el tamaño del almacén de datos puede aumentar en aproximadamente 400 GB si se realizan unos 5500 flujos de trabajo en un plazo de 8 horas.
>
>Se trata de un aumento temporal y el almacén de datos se restaura a su tamaño original después de ejecutar la tarea de recolección de elementos no utilizados del almacén de datos.
>
>Normalmente, la tarea de recolección de elementos no utilizados del almacén de datos se ejecuta semanalmente junto con otras tareas de mantenimiento programadas.
>
>Si tiene un espacio de disco limitado y ejecuta los flujos de trabajo de recursos de actualización de DAM de forma intensiva, considere programar la tarea de recolección de elementos no utilizados con más frecuencia.

#### Generación de representaciones en tiempo de ejecución {#runtime-rendition-generation}

Los clientes utilizan imágenes de diversos tamaños y formatos en su sitio web o para su distribución a socios comerciales. Dado que cada representación se añade a la huella del recurso en el repositorio, Adobe recomienda utilizar esta función con prudencia. Para reducir la cantidad de recursos necesarios para procesar y almacenar imágenes, puede generar estas imágenes en tiempo de ejecución en lugar de como representaciones durante la ingestión.

Muchos clientes de Sitios implementan un servlet de imagen que cambia el tamaño y recorta las imágenes en el momento en que se solicitan, lo que impone una carga adicional en la instancia de publicación. Sin embargo, mientras estas imágenes se puedan almacenar en caché, el desafío se puede mitigar.

Un método alternativo es utilizar la tecnología de Scene7 para eliminar por completo la manipulación de imágenes. Además, puede implementar Brand Portal que no solo asume las responsabilidades de generación de representaciones de la infraestructura de AEM, sino también de todo el nivel de publicación.

### XMP writeback {#xmp-writeback}

La reescritura XMP actualiza el recurso original cada vez que se modifican los metadatos en AEM, lo que resulta en lo siguiente:

* Se modifica el recurso mismo
* Se crea una versión del recurso
* El recurso de actualización DAM se ejecuta con el recurso

Los resultados de la lista consumen recursos considerables. Por lo tanto, Adobe recomienda [desactivar la reescritura](https://helpx.adobe.com/experience-manager/kb/disable-xmp-writeback.html)XMP si no es necesaria.

La importación de una gran cantidad de metadatos puede dar como resultado una actividad de reescritura XMP intensiva en recursos si se marca el indicador de flujos de trabajo de ejecución. Planifique una importación de este tipo durante el uso del servidor liso para que el rendimiento de otros usuarios no se vea afectado.

## Replicación {#replication}

Al replicar recursos en un gran número de instancias de publicación, por ejemplo en una implementación de sitios, Adobe recomienda utilizar la replicación en cadena. En este caso, la instancia de autor se replica en una única instancia de publicación que, a su vez, se replica en las demás instancias de publicación, lo que libera la instancia de autor.

### Configurar replicación de cadenas {#configure-chain-replication}

1. Elija la instancia de publicación que desea utilizar para encadenar las replicaciones a
1. En esa instancia de publicación, agregue agentes de replicación que apunten a otras instancias de publicación
1. En cada uno de esos agentes de replicación, habilite &quot;Al recibir&quot; en la ficha &quot;Desencadenadores&quot;

>[!NOTE]
>
>Adobe no recomienda la activación automática de recursos. Sin embargo, si es necesario, Adobe recomienda que esto sea el último paso de un flujo de trabajo, normalmente DAM Update Asset.

## Índices de búsqueda {#search-indexes}

Asegúrese de implementar los Service Packs más recientes y las revisiones relacionadas con el rendimiento, ya que suelen incluir actualizaciones en los índices del sistema. Consulte Consejos [de optimización del rendimiento| 6.x](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html) para algunas optimizaciones de índice que se pueden aplicar, según la versión de AEM.

<!--
Create custom indexes for queries that you run often. For details, see [methodology for analyzing slow queries](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html) and [crafting custom indexes](/help/sites-deploying/queries-and-indexing.md). For additional insights around query and index best practices, see [Best Practices for Queries and Indexing](/help/sites-deploying/best-practices-for-queries-and-indexing.md).
-->

### Configuraciones de índice de Lucene {#lucene-index-configurations}

Se pueden realizar algunas optimizaciones en las configuraciones de índice Oak que pueden ayudar a mejorar el rendimiento de Recursos AEM:

Actualice las configuraciones de índice para mejorar el tiempo de reindexación:

1. Abra CRXDe /crx/de/index.jsp e inicie sesión como usuario administrativo
1. Vaya a /oak:index/lucene
1. Agregue una propiedad String[] denominada &quot;excludedPaths&quot; con los valores &quot;/var&quot;, &quot;/etc/workflow/instance&quot; y &quot;/etc/Replication&quot;
1. Vaya a /oak:index/damAssetLucene
1. Agregue una propiedad String[] denominada &quot;includePaths&quot; con un valor &quot;/content/dam&quot;
1. Guardar

(Solo AEM6.1 y 6.2) Actualice el índice ntBaseLucene para mejorar el rendimiento de eliminación y movimiento de recursos:

1. Vaya a */roak:index/ntBaseLucene/indexRules/nt:base/properties*
1. Agregue dos nodos nt:no estructurados &quot;slingResource&quot; y &quot;damResolvedPath&quot; en */oak:index/ntBaseLucene/indexRules/nt:base/properties*
1. Defina las propiedades siguientes en los nodos (donde las propiedades order y propertyIndex son del tipo *Boolean*:
slingResourcename=&quot;sling:resource&quot;ordered=falsepropertyIndex= truetype=&quot;String&quot;damResolvedPathname=&quot;dam:resolvePath&quot;ordered=falsepropertyIndex=truetype=&quot;String&quot;

1. En el nodo /oak:index/ntBaseLucene, establezca la propiedad *reindex=true*
1. Haga clic en &quot;Guardar todo&quot;
1. Supervise el error.log para ver cuándo se completa la indexación:
Reindexación completada para índices: [/roak:index/ntBaseLucene]
1. También puede ver que la indexación se completa actualizando el nodo /oak:index/ntBaseLucene en CRXDe, ya que la propiedad reindex volvería a false
1. Una vez completada la indexación, vuelva a CRXDe y establezca la propiedad &quot;type&quot; en disabled en estos dos índices

   * */oak:index/slingResource*
   * */oak:index/damResolvedPath*

1. Haga clic en &quot;Guardar todo&quot;

<!--
Disable Lucene Text Extraction:

If your users don't need to be able to search the contents of assets, for example, searching the text contained in PDF documents, then you can improve index performance by disabling this feature.

1. Go to the AEM package manager /crx/packmgr/index.jsp
1. Upload and install the package below

[Get File](assets/disable_indexingbinarytextextraction-10.zip)
-->

### Total de asistentes {#guess-total}

Cuando cree consultas que generen grandes conjuntos de resultados, utilice el `guessTotal` parámetro para evitar una gran utilización de la memoria al ejecutarlos.

## Problemas conocidos {#known-issues}

### Archivos grandes {#large-files}

Existen dos problemas conocidos principales relacionados con archivos de gran tamaño en AEM. Cuando los archivos alcanzan tamaños superiores a 2 GB, la sincronización en espera en frío puede encontrarse en una situación de memoria insuficiente. En algunos casos, evita que se ejecute la sincronización en espera. En otros casos, provoca el bloqueo de la instancia principal. Este escenario se aplica a cualquier archivo de AEM que supere los 2 GB, incluidos los paquetes de contenido.

Del mismo modo, cuando los archivos alcanzan los 2 GB de tamaño mientras se utiliza un almacén de datos S3 compartido, puede que tarde algún tiempo en que el archivo permanezca completamente desde la caché hasta el sistema de archivos. Como resultado, al utilizar la replicación sin binarios, es posible que los datos binarios no se hayan mantenido antes de que se complete la replicación. Esta situación puede dar lugar a problemas, especialmente si la disponibilidad de datos es importante.

## Pruebas de rendimiento {#performance-testing}

Para cada implementación de AEM, establezca un régimen de prueba de rendimiento que pueda identificar y resolver cuellos de botella rápidamente. A continuación se indican algunas áreas clave en las que centrar la atención.

### Pruebas de red {#network-testing}

Para todas las preocupaciones de rendimiento de red del cliente, realice las siguientes tareas:

* Probar el rendimiento de la red desde la red del cliente
* Compruebe el rendimiento de la red desde la red de Adobe. Para los clientes de AMS, trabaje con su CSE para realizar pruebas desde la red de Adobe.
* Probar el rendimiento de la red desde otro punto de acceso
* Mediante el uso de una herramienta de referencia de red
* Prueba con el despachante

### Pruebas de instancia de AEM {#aem-instance-testing}

Para minimizar la latencia y lograr un alto rendimiento mediante la utilización eficiente de la CPU y el uso compartido de la carga, supervise el rendimiento de su instancia de AEM de forma regular. En particular:

* Ejecutar pruebas de carga con la instancia de AEM
* Supervisión del rendimiento de carga y la respuesta de la interfaz de usuario

## Lista de comprobación del rendimiento de AEM Assets e impacto de las tareas de gestión de recursos {#checklist}

* Habilitar HTTPS para evitar cualquier husmeador de tráfico HTTP corporativo
* Usar una conexión por cable para cargar recursos pesados
* Implementar en Java 8.
* Establecer parámetros JVM óptimos
* Configuración de un almacén de datos del sistema de archivos o un almacén de datos S3
* Habilitar flujos de trabajo transitorios
* Ajustar las colas de flujo de trabajo de Granite para limitar los trabajos simultáneos
* Configurar ImageMagick para limitar el consumo de recursos
* Eliminar pasos innecesarios del flujo de trabajo de recursos de actualización de DAM
* Configurar el flujo de trabajo y la depuración de versiones
* Optimice los índices con los paquetes de servicios y revisiones más recientes. Consulte con la asistencia de Adobe si hay optimizaciones de índice adicionales disponibles.
* Utilice el valor de adivinarTotal para optimizar el rendimiento de la consulta.
* Si configura AEM para que detecte tipos de archivo a partir del contenido de los archivos (habilitando el servicio **[!UICONTROL Day CQ DAM Mime Type en la consola]** web de **** AEM), cargue muchos archivos de forma masiva durante las horas no pico, ya que consume muchos recursos.

