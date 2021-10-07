---
title: Directrices de desarrollo de AEM as a Cloud Service
description: Directrices de desarrollo de AEM as a Cloud Service
exl-id: 94cfdafb-5795-4e6a-8fd6-f36517b27364
source-git-commit: d37193833d784f3f470780b8f28e53b473fd4e10
workflow-type: tm+mt
source-wordcount: '2073'
ht-degree: 2%

---

# Directrices de desarrollo de AEM as a Cloud Service {#aem-as-a-cloud-service-development-guidelines}

El código que se ejecuta en AEM as a Cloud Service debe tener en cuenta que siempre se está ejecutando en un clúster. Esto significa que siempre hay más de una instancia en ejecución. El código debe ser flexible, especialmente porque una instancia puede detenerse en cualquier momento.

Durante la actualización de AEM as a Cloud Service, habrá instancias con código antiguo y nuevo ejecutándose en paralelo. Por lo tanto, el código antiguo no debe romper con el contenido creado por el código nuevo y el nuevo código debe poder lidiar con el contenido antiguo.
<!--

>[!NOTE]
> All of the best practices mentioned here hold true for on-premise deployments of AEM, if not stated otherwise. An instance can always stop due to various reasons. However, with Skyline it is more likely to happen therefore an instance stopping is the rule not an exception.

-->

Si es necesario identificar el principal en el clúster, la API de Apache Sling Discovery se puede utilizar para detectarlo.

## Estado en memoria {#state-in-memory}

El estado no debe guardarse en la memoria, sino persistir en el repositorio. De lo contrario, este estado podría perderse si se detiene una instancia.

## Estado en el sistema de archivos {#state-on-the-filesystem}

El sistema de archivos de la instancia no debe usarse en AEM as a Cloud Service. El disco es efímero y se eliminará cuando se reciclen instancias. Es posible el uso limitado del sistema de archivos para el almacenamiento temporal relacionado con el procesamiento de solicitudes individuales, pero no debería abusarse de archivos enormes. Esto se debe a que puede tener un impacto negativo en la cuota de uso de recursos y tener limitaciones de disco.

Como ejemplo en el que no se admite el uso del sistema de archivos, el nivel Publicar debe garantizar que todos los datos que deban conservarse se envíen a un servicio externo para un almacenamiento a más largo plazo.

## Observación {#observation}

De forma similar, con todo lo que está sucediendo asincrónicamente como la actuación en eventos de observación, no se puede garantizar que se ejecute localmente y, por lo tanto, se debe utilizar con cuidado. Esto se aplica tanto a los eventos de JCR como a los eventos de recursos de Sling. En el momento en que se produce un cambio, la instancia se puede retirar y reemplazar por otra instancia. Otras instancias de la topología que estén activas en ese momento podrán reaccionar ante ese evento. En este caso, sin embargo, esto no será un evento local y podría incluso no haber un líder activo en caso de una elección de líder en curso cuando se publique el evento.

## Tareas en segundo plano y trabajos de larga duración {#background-tasks-and-long-running-jobs}

El código ejecutado como tareas en segundo plano debe suponer que la instancia en la que se está ejecutando se puede desactivar en cualquier momento. Por lo tanto, el código debe ser flexible y la mayoría de las importaciones reanudarlas. Esto significa que si el código se vuelve a ejecutar, no debería comenzar de nuevo desde el principio, sino más bien cerca de donde lo dejó. Aunque este no es un requisito nuevo para este tipo de código, en AEM as a Cloud Service es más probable que se produzca una eliminación de instancia.

Para minimizar los problemas, se deben evitar los trabajos de larga duración si es posible, y deben reanudarse como mínimo. Para ejecutar estos trabajos, utilice Sling Jobs, que tienen una garantía de al menos una vez y, por lo tanto, si se interrumpen, se vuelven a ejecutar lo antes posible. Pero probablemente no deberían comenzar de nuevo desde el principio. Para programar estos trabajos, es mejor utilizar el programador [Sling Jobs](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) ya que esta vez es la ejecución de al menos una vez.

El planificador de Sling Commons no debe utilizarse para la programación, ya que la ejecución no puede garantizarse. Es más probable que se programe.

Del mismo modo, con todo lo que está ocurriendo asincrónicamente, como actuar en eventos de observación (ya sean eventos JCR o eventos de recursos Sling), no se puede garantizar que se ejecute y, por lo tanto, se debe utilizar con cuidado. Esto ya se aplica a las implementaciones AEM en el presente.

## Conexiones HTTP salientes {#outgoing-http-connections}

Se recomienda encarecidamente que cualquier conexión HTTP saliente establezca tiempos de conexión y lectura razonables. Para el código que no aplica estos tiempos de espera, AEM instancias que se ejecutan en AEM as a Cloud Service impondrán un tiempo de espera global. Estos valores de tiempo de espera son 10 segundos para las llamadas de conexión y 60 segundos para las llamadas de lectura para las conexiones utilizadas por las siguientes bibliotecas Java populares:

Adobe recomienda el uso de la biblioteca [Apache HttpComponents Client 4.x](https://hc.apache.org/httpcomponents-client-ga/) proporcionada para realizar conexiones HTTP.

Las alternativas que se sabe que funcionan, pero que pueden requerir proporcionar la dependencia usted mismo son:

* [java.net.](https://docs.oracle.com/javase/7/docs/api/java/net/URL.html) URLand/or  [java.net.URLConnection](https://docs.oracle.com/javase/7/docs/api/java/net/URLConnection.html)  (proporcionado por AEM)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/)  (no recomendado porque está obsoleto y reemplazado por la versión 4.x)
* [OK Http](https://square.github.io/okhttp/)  (No proporcionado por AEM)

## Sin personalizaciones de la interfaz de usuario clásica {#no-classic-ui-customizations}

AEM as a Cloud Service solo admite la IU táctil para el código de cliente de terceros. La IU clásica no está disponible para la personalización.

## Evitar binarios nativos {#avoid-native-binaries}

El código no podrá descargar binarios durante la ejecución ni modificarlos. Por ejemplo, no podrá desempaquetar archivos `jar` o `tar`.

## No hay binarios de transmisión por AEM as a Cloud Service {#no-streaming-binaries}

Se debe acceder a los binarios a través de la CDN, que servirá binarios fuera de los servicios AEM principales.

Por ejemplo, no utilice `asset.getOriginal().getStream()`, que déclencheur descargar un binario en el disco efímero del servicio de AEM.

## Sin agentes de replicación inversa {#no-reverse-replication-agents}

La replicación inversa de Publicar en Autor no es compatible con AEM as a Cloud Service. Si se necesita dicha estrategia, puede utilizar un almacén de persistencia externa que se comparta entre el conjunto de instancias de publicación y, potencialmente, el clúster de creación.

## Es posible que los agentes de replicación de reenvío necesiten ser transferidos {#forward-replication-agents}

El contenido se duplica de Autor a Publicación a través de un mecanismo pub-sub. No se admiten agentes de replicación personalizados.

## Monitorización y depuración {#monitoring-and-debugging}

### Registros {#logs}

Para el desarrollo local, las entradas de registro se escriben en archivos locales de la carpeta `/crx-quickstart/logs` .

En entornos de Cloud, los desarrolladores pueden descargar registros a través de Cloud Manager o utilizar una herramienta de línea de comandos para rastrear los registros. <!-- See the [Cloud Manager documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->

**Configuración del nivel de registro**

Para cambiar los niveles de registro para los entornos de Cloud, la configuración OSGI de registro de Sling debe modificarse, seguida de una reimplementación completa. Como esto no es instantáneo, tenga cuidado de habilitar registros detallados en entornos de producción que reciben mucho tráfico. En el futuro, es posible que haya mecanismos para cambiar más rápidamente el nivel de registro.

>[!NOTE]
>
>Para realizar los cambios de configuración que se enumeran a continuación, debe crearlos en un entorno de desarrollo local y, a continuación, colocarlos en una instancia as a Cloud Service AEM. Para obtener más información sobre cómo hacerlo, consulte [Implementación para AEM](/help/implementing/deploying/overview.md) as a Cloud Service.

**Activación del nivel de registro de depuración**

El nivel de registro predeterminado es INFO, es decir, los mensajes DEBUG no se registran.
Para activar el nivel de registro de DEBUG, establezca la variable

``` /libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level ```

para depurar. No deje el registro en el nivel de registro DEBUG más tiempo del necesario, ya que genera muchos registros.
Una línea en el archivo de depuración normalmente comienza con DEBUG y, a continuación, proporciona el nivel de registro, la acción del instalador y el mensaje de registro. Por ejemplo:

``` DEBUG 3 WebApp Panel: WebApp successfully deployed ```

Los niveles de registro son los siguientes:

| 0 | Error grave | La acción ha fallado y el instalador no puede continuar. |
|---|---|---|
| 1 | Error | La acción ha fallado. La instalación continúa, pero una parte de CRX no se instaló correctamente y no funcionará. |
| 2 | Advertencia | La acción se ha realizado correctamente, pero se han encontrado problemas. CRX puede o no funcionar correctamente. |
| 3 | Información | La acción se ha realizado correctamente. |

### Volcados de subprocesos {#thread-dumps}

Los volcados de subprocesos en entornos de Cloud se recopilan de forma continua, pero no se pueden descargar de forma automática en este momento. Mientras tanto, póngase en contacto con el servicio de asistencia AEM si se necesitan volcados de subprocesos para depurar un problema, especificando el tiempo exacto.

## CRX/DE Lite y Developer Console {#crxde-lite-and-developer-console}

### Desarrollo local {#local-development}

Para el desarrollo local, los desarrolladores tienen acceso completo al CRXDE Lite (`/crx/de`) y a la Consola Web AEM (`/system/console`).

Tenga en cuenta que en el desarrollo local (con el SDK), `/apps` y `/libs` se pueden escribir directamente en , lo que es diferente de los entornos de Cloud en los que esas carpetas de nivel superior son inmutables.

### AEM herramientas de desarrollo as a Cloud Service {#aem-as-a-cloud-service-development-tools}

Los clientes pueden acceder a CRXDE lite en el entorno de desarrollo del nivel de creación, pero no en la fase o en la producción. El repositorio inmutable (`/libs`, `/apps`) no se puede escribir en durante la ejecución, por lo que al intentar hacerlo se producirán errores.

En Developer Console hay disponible un conjunto de herramientas para depurar AEM entornos de desarrollador as a Cloud Service para entornos de desarrollo, fase y producción. La dirección URL se puede determinar ajustando las direcciones url del servicio Autor o Publicación de la siguiente manera:

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

Como método abreviado, se puede utilizar el siguiente comando CLI de Cloud Manager para iniciar la consola del desarrollador en función de un parámetro de entorno descrito a continuación:

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

Consulte [esta página](/help/release-notes/home.md) para obtener más información.

Los desarrolladores pueden generar información de estado y resolver varios recursos.

Como se muestra a continuación, la información de los estados disponibles incluye el estado de los paquetes, componentes, configuraciones OSGI, índices de roak, servicios OSGI y trabajos Sling.

![Consola de desarrollo 1](/help/implementing/developing/introduction/assets/devconsole1.png)

Como se ilustra a continuación, los desarrolladores pueden resolver dependencias y servlets de paquetes:

![Consola de desarrollo 2](/help/implementing/developing/introduction/assets/devconsole2.png)

![Consola de desarrollo 3](/help/implementing/developing/introduction/assets/devconsole3.png)

También resulta útil para la depuración, ya que la consola de desarrollador tiene un vínculo a la herramienta Explicar consulta :

![Consola de desarrollo 4](/help/implementing/developing/introduction/assets/devconsole4.png)

En el caso de los programas de producción, el acceso a Developer Console se define mediante la función de desarrollador de Cloud Manager en el Admin Console, mientras que para los programas de simulación de pruebas, Developer Console está disponible para cualquier usuario con un perfil de producto que les permita acceder a AEM as a Cloud Service. Para todos los programas, &quot;Cloud Manager - Developer Role&quot; es necesario para los volcados de estado y los usuarios también deben definirse en el perfil de producto de los usuarios de AEM o de los administradores de AEM en los servicios de autor y publicación para ver los datos de volcado de estado de ambos servicios. Para obtener más información sobre la configuración de permisos de usuario, consulte [Documentación de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html).

### Servicio de ensayo y producción de AEM {#aem-staging-and-production-service}

Los clientes no tendrán acceso a las herramientas para desarrolladores para entornos de ensayo y producción.

### Supervisión del rendimiento {#performance-monitoring}

El Adobe supervisa el rendimiento de la aplicación y toma medidas para solucionar el problema si se observa deterioro. En este momento, no se pueden respetar las métricas de la aplicación.

## Envío de correo electrónico {#sending-email}

AEM as a Cloud Service requiere que el correo saliente esté cifrado. Las secciones siguientes describen cómo solicitar, configurar y enviar correos electrónicos.

>[!NOTE]
>
>El servicio de correo se puede configurar con compatibilidad con OAuth2. Para obtener más información, consulte [Compatibilidad con OAuth2 para el servicio de correo](/help/security/oauth2-support-for-mail-service.md).

### Activación del correo electrónico saliente {#enabling-outbound-email}

De forma predeterminada, los puertos utilizados para enviar están desactivados. Para activarlo, configure [red avanzada](/help/security/configuring-advanced-networking.md), asegurándose de establecer para cada entorno necesario las reglas de reenvío de puertos del extremo `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` para que el tráfico pueda pasar por el puerto 465 (si es compatible con el servidor de correo) o el puerto 587 (si el servidor de correo lo requiere y también aplica TLS en ese puerto).

Se recomienda configurar redes avanzadas con un parámetro `kind` establecido en `flexiblePortEgress`, ya que el Adobe puede optimizar el rendimiento del tráfico de salida de puerto flexible. Si es necesaria una dirección IP de salida única, elija un parámetro `kind` de `dedicatedEgressIp`. Si ya ha configurado VPN por otros motivos, también puede utilizar la dirección IP única que proporciona esa variación de red avanzada.

Debe enviar un correo electrónico a través de un servidor de correo en lugar de enviarlo directamente a los clientes de correo electrónico. De lo contrario, los correos electrónicos podrían bloquearse.

### Envío de correos electrónicos {#sending-emails}

El [servicio OSGI del servicio de correo de CQ Day](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service) debe usarse y los correos electrónicos deben enviarse al servidor de correo indicado en la solicitud de asistencia, en lugar de enviarse directamente a los destinatarios.

AEM as a Cloud Service requiere que el correo se envíe a través del puerto 465. Si un servidor de correo no admite el puerto 465, se puede utilizar el puerto 587, siempre y cuando la opción TLS esté habilitada.

>[!NOTE]
>
>Tenga en cuenta que el Adobe no admite la representación SMTP a través de una dirección IP dedicada única.

### Configuración {#email-configuration}

Los correos electrónicos de AEM deben enviarse utilizando el [Day CQ Mail Service OSGi service](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service).

Consulte la [AEM documentación de 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html) para obtener más información sobre la configuración del correo electrónico. Para AEM as a Cloud Service, se deben realizar los siguientes ajustes en el servicio `com.day.cq.mailer.DefaultMailService OSGI`:

Si se ha solicitado el puerto 465:

* establezca `smtp.port` en `465`
* establezca `smtp.ssl` en `true`

Si se ha solicitado el puerto 587 (solo se permite si el servidor de correo no admite el puerto 465):

* establezca `smtp.port` en `587`
* establezca `smtp.ssl` en `false`

La propiedad `smtp.starttls` se establecerá automáticamente mediante AEM as a Cloud Service durante la ejecución a un valor apropiado. Por lo tanto, si `smtp.tls` se establece en true, `smtp.startls` se omite. Si `smtp.ssl` se establece en false, `smtp.starttls` se establece en true. Esto es independientemente de los valores `smtp.starttls` establecidos en la configuración OSGI.

El servicio de correo puede configurarse opcionalmente con compatibilidad con OAuth2. Para obtener más información, consulte [Compatibilidad con OAuth2 para el servicio de correo](/help/security/oauth2-support-for-mail-service.md).

## [!DNL Assets] directrices de desarrollo y casos de uso {#use-cases-assets}

Para obtener información sobre los casos de uso de desarrollo, las recomendaciones y los materiales de referencia de los recursos as a Cloud Service, consulte [Referencias del desarrollador para Assets](/help/assets/developer-reference-material-apis.md#assets-cloud-service-apis).
