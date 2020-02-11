---
title: AEM como directrices de desarrollo de servicios en la nube
description: 'Para completar '
translation-type: tm+mt
source-git-commit: 13c0a670330532f574c2b38823b8a924c609e8e4

---


# AEM como directrices de desarrollo de servicios en la nube {#aem-as-a-cloud-service-development-guidelines}

## Tareas en segundo plano y trabajos de larga duración {#background-tasks-and-long-running-jobs}

El código ejecutado como tareas en segundo plano debe suponer que la instancia en la que se está ejecutando se puede desactivar en cualquier momento. Por lo tanto, el código debe ser resiliente y la mayoría de las importaciones deben poder reanudarse. Esto significa que si el código se vuelve a ejecutar, no debería empezar de nuevo desde el principio, sino más bien cerca de donde lo dejó. Aunque este no es un requisito nuevo para este tipo de código, en AEM como servicio de nube es más probable que se produzca una eliminación de instancia.

Para minimizar el problema, se deben evitar los trabajos de larga duración si es posible, y se deben reanudar al menos. Para ejecutar estos trabajos, utilice Sling Jobs, que cuenta con una garantía de al menos una vez y por lo tanto si se interrumpen, será reejecutado lo antes posible. Pero probablemente no deberían empezar de nuevo desde el principio. Para programar estos trabajos, es mejor utilizar el programador de trabajos [](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) de Sling, ya que de nuevo se trata de la ejecución de al menos una vez.

El programador de Sling Commons no debe utilizarse para programar, ya que no se puede garantizar la ejecución. Es más probable que se programe.

De manera similar, con todo lo que está sucediendo asincrónicamente, como actuar en eventos de observación (ya sean eventos JCR o eventos de recursos Sling), no se puede garantizar que se ejecute y por lo tanto debe usarse con cuidado. Esto ya se aplica a las implementaciones de AEM en este momento.

## Conexiones HTTP salientes {#outgoing-http-connections}

Se recomienda encarecidamente que cualquier conexión HTTP saliente establezca tiempos de conexión y de espera de lectura razonables. Para el código que no aplica estos tiempos de espera, las instancias de AEM que se ejecutan en AEM como un servicio de nube exigirán tiempos de espera globales. Estos valores de tiempo de espera son de 10 segundos para llamadas de conexión y de 60 segundos para llamadas de lectura para conexiones utilizadas por las siguientes bibliotecas de Java populares:

Adobe recomienda el uso de la biblioteca [](https://hc.apache.org/httpcomponents-client-ga/) Apache HttpComponents Client 4.x proporcionada para realizar conexiones HTTP.

Las alternativas que se sabe que funcionan, pero que pueden requerir que usted mismo proporcione la dependencia son:

* [java.net.URL](https://docs.oracle.com/javase/7/docs/api/java/net/URL.html) y/o [java.net.URLConnection](https://docs.oracle.com/javase/7/docs/api/java/net/URLConnection.html) (AEM)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/) (no recomendado porque está obsoleto y reemplazado por la versión 4.x)
* [OK Http](OK Http (No proporcionado por AEM)) (No proporcionado por AEM)

## Monitoreo y depuración {#monitoring-and-debugging}

### Registros {#logs}

* Para el desarrollo local, las entradas de registro se escriben en archivos locales
   * `./crx-quickstart/logs`
* En los entornos de Cloud, los desarrolladores pueden descargar registros a través de Cloud Manager o utilizar una herramienta de línea de comandos para reducir los registros. <!-- See the [Cloud Manager documentation](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->
* Para cambiar los niveles de registro de los entornos de nube, se debe modificar la configuración OSGI de registro de Sling, seguida de una reimplementación completa. Dado que esto no es instantáneo, tenga cuidado de habilitar los registros detallados en entornos de producción que reciben mucho tráfico. En el futuro, es posible que haya mecanismos para cambiar más rápidamente el nivel de registro.

### Duques de rosca {#thread-dumps}

Los volcados de subprocesos en entornos de nube se recopilan de forma continua, pero no se pueden descargar de forma automática en este momento. Mientras tanto, póngase en contacto con el servicio de asistencia de AEM si se necesitan volcados de subprocesos para depurar un problema, especificando la ventana horaria exacta.

### CRX/DE Lite y la consola del sistema {#crxde-lite-and-system-console}

## Desarrollo local {#local-development}

Para el desarrollo local, los desarrolladores tienen acceso completo a CRXDE Lite (`/crx/de`) y a la consola web de AEM (`/system/console`).

Tenga en cuenta que en el desarrollo local (con el inicio rápido listo para la nube) `/apps` , y `/libs` se puede escribir directamente en él, lo cual es diferente de los entornos de nube donde esas carpetas de nivel superior son inmutables.

## AEM como herramienta de desarrollo de servicios en la nube {#aem-as-a-cloud-service-development-tools}

Los clientes pueden acceder a CRXDE lite en el entorno de desarrollo, pero no en fase ni en producción. No se puede escribir en el repositorio inmutable (`/libs`, `/apps`) durante la ejecución, por lo que al intentar hacerlo se generarán errores.

En la consola para desarrolladores hay disponible un conjunto de herramientas para depurar AEM como entornos de desarrollador de servicios de nube para entornos de desarrollo, fase y producción. La dirección URL se puede determinar ajustando las direcciones URL del servicio de creación o publicación de la siguiente manera:

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

También resulta útil para la depuración, ya que la consola del desarrollador tiene un vínculo a la herramienta Explicar consulta:

![Consola de desarrollo 4](/help/implementing/developing/introduction/assets/devconsole4.png)

**Servicio de ensayo y producción de AEM**

Los clientes no tendrán acceso a las herramientas para desarrolladores para entornos de ensayo y producción.

### Diagnósticos {#diagnostics}

La consola del sistema está disponible para entornos de desarrollo. Sin embargo, no se dispone de depósitos de diagnóstico para ensayo y producción.