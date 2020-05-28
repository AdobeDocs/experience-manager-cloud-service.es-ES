---
title: Directrices de desarrollo de AEM as a Cloud Service
description: Para completar
translation-type: tm+mt
source-git-commit: 8e8863d390132ff8df943548b04e9d7c636c4248
workflow-type: tm+mt
source-wordcount: '1588'
ht-degree: 1%

---


# Directrices de desarrollo de AEM as a Cloud Service {#aem-as-a-cloud-service-development-guidelines}

El código que se ejecuta en AEM como servicio de nube debe tener en cuenta que siempre se ejecuta en un clúster. Esto significa que siempre hay más de una instancia en ejecución. El código debe ser flexible, especialmente porque una instancia puede detenerse en cualquier momento.

Durante la actualización de AEM como servicio de nube, habrá instancias con código antiguo y nuevo ejecutándose en paralelo. Por lo tanto, el código antiguo no debe romperse con el contenido creado por el nuevo código y el nuevo código debe ser capaz de tratar el contenido antiguo.
<!--

>[!NOTE]
> All of the best practices mentioned here hold true for on-premise deployments of AEM, if not stated otherwise. An instance can always stop due to various reasons. However, with Skyline it is more likely to happen therefore an instance stopping is the rule not an exception.

-->

Si es necesario identificar al maestro en el clúster, la API de Apache Sling Discovery puede utilizarse para detectarla.

## Estado en memoria {#state-in-memory}

El estado no debe guardarse en la memoria sino en el repositorio. De lo contrario, este estado podría perderse si se detiene una instancia.

## Estado en el sistema de archivos {#state-on-the-filesystem}

El sistema de archivos de la instancia no debe usarse en AEM como un servicio de nube. El disco es efímero y se eliminará cuando se reciclen las instancias. Es posible el uso limitado del sistema de archivos para almacenamientos temporales relacionados con el procesamiento de solicitudes individuales, pero no se debe abusar de archivos enormes. Esto se debe a que puede tener un impacto negativo en la cuota de uso de recursos y tener limitaciones de disco.

Como ejemplo en el caso de que no se admita el uso del sistema de archivos, el nivel Publicar debe garantizar que todos los datos que deban conservarse se envíen a un servicio externo para un almacenamiento a largo plazo.

## Observación {#observation}

De manera similar, con todo lo que sucede asincrónicamente como actuar en eventos de observación, no se puede garantizar que se ejecute localmente y, por lo tanto, debe usarse con cuidado. Esto es válido tanto para eventos JCR como para eventos de recursos Sling. En el momento en que se produce un cambio, la instancia se puede retirar y reemplazar por otra instancia. Otras instancias de la topología que estén activas en ese momento podrán reaccionar a ese evento. En este caso, sin embargo, esto no será un evento local y podría incluso no haber un líder activo en caso de una elección de líder en curso cuando se publique el evento.

## Tareas en segundo plano y trabajos de larga duración {#background-tasks-and-long-running-jobs}

El código ejecutado como tareas en segundo plano debe suponer que la instancia en la que se está ejecutando se puede desactivar en cualquier momento. Por lo tanto, el código debe ser resiliente y la mayoría de las importaciones deben poder reanudarse. Esto significa que si el código se vuelve a ejecutar, no debería volver a inicio desde el principio, sino más bien cerca de donde lo dejó. Aunque este no es un requisito nuevo para este tipo de código, en AEM como servicio de nube es más probable que se produzca una eliminación de instancia.

Para minimizar el problema, se deben evitar los trabajos de larga duración si es posible, y se deben reanudar al menos. Para ejecutar estos trabajos, utilice Sling Jobs, que cuenta con una garantía de al menos una vez y por lo tanto si se interrumpen, será reejecutado lo antes posible. Pero probablemente no deberían volver a inicio desde el principio. Para programar estos trabajos, es mejor utilizar el Planificador Trabajos [de](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) Sling como una ejecución al menos una vez.

El Planificador de Sling Commons no debe ser usado para programar, ya que no se puede garantizar la ejecución. Es más probable que se programe.

De manera similar, con todo lo que está sucediendo asincrónicamente, como actuar en eventos de observación (ya sean eventos JCR o eventos de recursos Sling), no se puede garantizar que se ejecute y, por lo tanto, se debe usar con cuidado. Esto ya se aplica a las implementaciones de AEM en este momento.

## Conexiones HTTP salientes {#outgoing-http-connections}

Se recomienda encarecidamente que cualquier conexión HTTP saliente establezca tiempos de conexión y de espera de lectura razonables. Para el código que no aplica estos tiempos de espera, las instancias de AEM que se ejecutan en AEM como un servicio de nube exigirán tiempos de espera globales. Estos valores de tiempo de espera son de 10 segundos para llamadas de conexión y de 60 segundos para llamadas de lectura para conexiones utilizadas por las siguientes bibliotecas de Java populares:

Adobe recomienda el uso de la biblioteca [](https://hc.apache.org/httpcomponents-client-ga/) Apache HttpComponents Client 4.x proporcionada para realizar conexiones HTTP.

Las alternativas que se sabe que funcionan, pero que pueden requerir que usted mismo proporcione la dependencia son:

* [java.net.URL](https://docs.oracle.com/javase/7/docs/api/java/net/URL.html) y/o [java.net.URLConnection](https://docs.oracle.com/javase/7/docs/api/java/net/URLConnection.html) (AEM)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/) (no recomendado porque está obsoleto y reemplazado por la versión 4.x)
* [Http](https://square.github.io/okhttp/) correcto (no proporcionado por AEM)

## No hay personalizaciones de IU clásicas {#no-classic-ui-customizations}

AEM como servicio de nube solo admite la IU táctil para el código de cliente de terceros. La IU clásica no está disponible para la personalización.

## Evitar binarios nativos {#avoid-native-binaries}

El código no podrá descargar archivos binarios en tiempo de ejecución ni modificarlos. Por ejemplo, no podrá desempaquetar `jar` ni `tar` archivos.

## Sin archivos binarios de flujo continuo a través de AEM como un servicio de nube {#no-streaming-binaries}

Se debe acceder a los binarios a través de la CDN, que servirá binarios fuera de los servicios principales de AEM.

Por ejemplo, no utilice `asset.getOriginal().getStream()`, lo que desencadena la descarga de un binario en el disco efímero del servicio AEM.

## No hay agentes de replicación inversa {#no-reverse-replication-agents}

La replicación inversa de Publicar en autor no se admite en AEM como un servicio de nube. Si se necesita una estrategia de este tipo, puede utilizar un almacén de persistencia externo que se comparte entre el conjunto de instancias de Publish y, potencialmente, el clúster de Autor.

## Es posible que los agentes de replicación de avanzada necesiten ser trasladados {#forward-replication-agents}

El contenido se replica de Autor a Publicación mediante un mecanismo de subprocesamiento de pub. No se admiten los agentes de replicación personalizados.

## Monitoreo y depuración {#monitoring-and-debugging}

### Registros {#logs}

Para el desarrollo local, las entradas de registro se escriben en los archivos locales de la `/crx-quickstart/logs` carpeta.

En los entornos de Cloud, los desarrolladores pueden descargar registros a través de Cloud Manager o utilizar una herramienta de línea de comandos para reducir los registros. <!-- See the [Cloud Manager documentation](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->

**Configuración del nivel de registro**

Para cambiar los niveles de registro de los entornos de nube, se debe modificar la configuración de OSGI de registro de Sling, seguida de una reimplementación completa. Dado que esto no es instantáneo, tenga cuidado de habilitar los registros detallados en entornos de producción que reciben mucho tráfico. En el futuro, es posible que haya mecanismos para cambiar más rápidamente el nivel de registro.

>[!NOTE]
>
>Para realizar los cambios de configuración que se indican a continuación, debe crearlos en un entorno de desarrollo local y, a continuación, colocarlos en una instancia de AEM como servicio de nube. Para obtener más información sobre cómo hacerlo, consulte [Implementación en AEM como un servicio](/help/implementing/deploying/overview.md)de nube.

**Activación del nivel de registro DEBUG**

El nivel de registro predeterminado es INFO, es decir, los mensajes DEBUG no se registran.
Para activar el nivel de registro DEBUG, establezca la variable

``` /libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level ```

para depurar. No deje el registro en el nivel de registro DEBUG más tiempo del necesario, ya que genera muchos registros.
Una línea en el archivo de depuración normalmente inicio con DEBUG y, a continuación, proporciona el nivel de registro, la acción del instalador y el mensaje de registro. Por ejemplo:

``` DEBUG 3 WebApp Panel: WebApp successfully deployed ```

Los niveles de registro son los siguientes:

| 0 | Error fatal | Error en la acción y el instalador no puede continuar. |
|---|---|---|
| 1 | Error | Error en la acción. La instalación continúa, pero una parte de CRX no se instaló correctamente y no funcionará. |
| 2 | Advertencia | La acción se ha realizado correctamente, pero se han encontrado problemas. CRX puede funcionar correctamente o no. |
| 3 | Información | La acción se ha realizado correctamente. |

### Duques de rosca {#thread-dumps}

Los volcados de subprocesos en entornos de la nube se recopilan de forma continua, pero no se pueden descargar de forma automática en este momento. Mientras tanto, póngase en contacto con el servicio de asistencia de AEM si se necesitan volcados de subprocesos para depurar un problema, especificando la ventana horaria exacta.

## CRX/DE Lite y la consola del sistema {#crxde-lite-and-system-console}

### Desarrollo local {#local-development}

Para el desarrollo local, los desarrolladores tienen acceso completo a CRXDE Lite (`/crx/de`) y a la consola web de AEM (`/system/console`).

Tenga en cuenta que en el desarrollo local (con el inicio rápido listo para la nube) `/apps` , y `/libs` se puede escribir directamente en él, lo cual es diferente de los entornos de nube donde las carpetas de nivel superior son inmutables.

### AEM as a Cloud Service Development tools {#aem-as-a-cloud-service-development-tools}

Los clientes pueden acceder a la lista CRXDE en el entorno de desarrollo, pero no en fase o producción. No se puede escribir en el repositorio inmutable (`/libs`, `/apps`) durante la ejecución, por lo que al intentar hacerlo se generarán errores.

Hay disponible un conjunto de herramientas para depurar AEM como entornos de desarrollador de Cloud Service en Developer Console para entornos de desarrollo, fase y producción. La dirección URL se puede determinar ajustando las direcciones URL del servicio Autor o Publicación de la siguiente manera:

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

Como método abreviado, se puede utilizar el siguiente comando de CLI de Cloud Manager para iniciar la consola de desarrollador en función de un parámetro de entorno que se describe a continuación:

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

Consulte [esta página](/help/release-notes/home.md) para obtener más información.

Los desarrolladores pueden generar información de estado y resolver varios recursos.

Como se ilustra a continuación, la información de estado disponible incluye el estado de los paquetes, componentes, configuraciones OSGI, índices de roble, servicios OSGI y trabajos Sling.

![Consola de desarrollo 1](/help/implementing/developing/introduction/assets/devconsole1.png)

Como se ilustra a continuación, los desarrolladores pueden resolver dependencias de paquetes y servlets:

![Consola de desarrollo 2](/help/implementing/developing/introduction/assets/devconsole2.png)

![Consola de desarrollo 3](/help/implementing/developing/introduction/assets/devconsole3.png)

También resulta útil para la depuración, ya que la consola para desarrolladores tiene un vínculo a la herramienta de Consulta Explicar:

![Consola de desarrollo 4](/help/implementing/developing/introduction/assets/devconsole4.png)

Para los programas regulares, el acceso a la consola de desarrollador se define mediante el &quot;Cloud Manager - Función de desarrollador&quot; en la Consola de administración, mientras que para los programas de simulación de pruebas, la consola de desarrollador está disponible para cualquier usuario con un perfil de producto que les permita acceder a AEM como servicio de nube. Para obtener más información sobre la configuración de permisos de usuario, consulte la documentación [de](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html)Cloud Manager.



### Servicio de ensayo y producción de AEM {#aem-staging-and-production-service}

Los clientes no tendrán acceso a las herramientas para desarrolladores para entornos de ensayo y producción.

### Monitoreo del rendimiento {#performance-monitoring}

Adobe supervisa el rendimiento de las aplicaciones y toma medidas para solucionar el problema si se observa un deterioro. En este momento, las métricas de la aplicación no se pueden respetar.
