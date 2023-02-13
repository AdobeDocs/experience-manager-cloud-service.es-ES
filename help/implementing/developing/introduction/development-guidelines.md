---
title: Directrices de desarrollo de AEM as a Cloud Service
description: Conozca las directrices para el desarrollo en AEM as a Cloud Service y sobre formas importantes en las que difiere de AEM en las instalaciones y AEM en AMS.
exl-id: 94cfdafb-5795-4e6a-8fd6-f36517b27364
source-git-commit: 01087aa2ec621d6bebd4d62edbc320df8122f71d
workflow-type: tm+mt
source-wordcount: '2591'
ht-degree: 2%

---

# Directrices de desarrollo de AEM as a Cloud Service {#aem-as-a-cloud-service-development-guidelines}

>[!CONTEXTUALHELP]
>id="development_guidelines"
>title="Directrices de desarrollo de AEM as a Cloud Service"
>abstract="Conozca las directrices para el desarrollo en AEM as a Cloud Service y sobre formas importantes en las que difiere de AEM en las instalaciones y AEM en AMS."
>additional-url="https://video.tv.adobe.com/v/330555/?captions=spa/" text="Demostración de la estructura del paquete"

En el presente documento se presentan directrices para la elaboración de AEM as a Cloud Service y de maneras importantes en que difiere de las AEM en los locales y AEM de AMS.

## El Código Debe Tener En Cuenta Los Clústeres {#cluster-aware}

El código que se ejecuta en AEM as a Cloud Service debe tener en cuenta que siempre se está ejecutando en un clúster. Esto significa que siempre hay más de una instancia en ejecución. El código debe ser flexible, especialmente porque una instancia puede detenerse en cualquier momento.

Durante la actualización de AEM as a Cloud Service, habrá instancias con código antiguo y nuevo ejecutándose en paralelo. Por lo tanto, el código antiguo no debe romper con el contenido creado por el código nuevo y el nuevo código debe poder lidiar con el contenido antiguo.

Si es necesario identificar el principal en el clúster, la API de Apache Sling Discovery se puede utilizar para detectarlo.

## Estado en memoria {#state-in-memory}

El estado no debe guardarse en la memoria, sino persistir en el repositorio. De lo contrario, este estado podría perderse si se detiene una instancia.

## Estado en el sistema de archivos {#state-on-the-filesystem}

El sistema de archivos de la instancia no debe usarse en AEM as a Cloud Service. El disco es efímero y se eliminará cuando se reciclen instancias. Es posible el uso limitado del sistema de archivos para el almacenamiento temporal relacionado con el procesamiento de solicitudes individuales, pero no debería abusarse de archivos enormes. Esto se debe a que puede tener un impacto negativo en la cuota de uso de recursos y tener limitaciones de disco.

Como ejemplo en el que no se admite el uso del sistema de archivos, el nivel Publicar debe garantizar que todos los datos que deban conservarse se envíen a un servicio externo para un almacenamiento a más largo plazo.

## Observación {#observation}

De forma similar, con todo lo que está sucediendo asincrónicamente como la actuación en eventos de observación, no se puede garantizar que se ejecute localmente y, por lo tanto, se debe utilizar con cuidado. Esto se aplica tanto a los eventos de JCR como a los eventos de recursos de Sling. En el momento en que se produce un cambio, la instancia se puede retirar y reemplazar por otra instancia. Otras instancias de la topología que estén activas en ese momento podrán reaccionar ante ese evento. En este caso, sin embargo, esto no será un evento local y podría incluso no haber un líder activo en caso de una elección de líder en curso cuando se publique el evento.

## Tareas en segundo plano y trabajos de larga duración {#background-tasks-and-long-running-jobs}

El código ejecutado como tareas en segundo plano debe suponer que la instancia en la que se está ejecutando se puede desactivar en cualquier momento. Por lo tanto, el código debe ser flexible y, lo más importante, reanudable. Esto significa que si el código se vuelve a ejecutar, no debería comenzar de nuevo desde el principio, sino más bien cerca de donde lo dejó. Aunque este no es un requisito nuevo para este tipo de código, en AEM as a Cloud Service es más probable que se produzca una eliminación de instancia.

Para minimizar los problemas, se deben evitar los trabajos de larga duración si es posible, y deben reanudarse como mínimo. Para ejecutar estos trabajos, utilice Sling Jobs, que tienen una garantía de al menos una vez y, por lo tanto, si se interrumpen, se vuelven a ejecutar lo antes posible. Pero probablemente no deberían comenzar de nuevo desde el principio. Para programar estos trabajos, es mejor utilizar la variable [Trabajos de Sling](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) como esto de nuevo garantiza la ejecución de al menos una vez.

El planificador de Sling Commons no debe utilizarse para la programación, ya que la ejecución no puede garantizarse. Es más probable que se programe.

Del mismo modo, con todo lo que está ocurriendo asincrónicamente, como actuar en eventos de observación (ya sean eventos JCR o eventos de recursos Sling), no se puede garantizar que se ejecute y, por lo tanto, se debe utilizar con cuidado. Esto ya se aplica a las implementaciones AEM en el presente.

## Conexiones HTTP salientes {#outgoing-http-connections}

Se recomienda encarecidamente que cualquier conexión HTTP saliente establezca tiempos de conexión y lectura razonables; los valores sugeridos son 1 segundo para el tiempo de espera de conexión y 5 segundos para el tiempo de espera de lectura. Los números exactos deben determinarse en función del rendimiento del sistema back-end que administra estas solicitudes.

Para el código que no aplica estos tiempos de espera, AEM instancias que se ejecutan en AEM as a Cloud Service impondrán un tiempo de espera global. Estos valores de tiempo de espera son 10 segundos para las llamadas de conexión y 60 segundos para las llamadas de lectura para las conexiones.

El Adobe recomienda el uso del [Biblioteca de Apache HttpComponents Client 4.x](https://hc.apache.org/httpcomponents-client-ga/) para realizar conexiones HTTP.

Las alternativas que se sabe que funcionan, pero que pueden requerir proporcionar la dependencia usted mismo son:

* [java.net.URL](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/net/URL.html) y/o [java.net.URLConnection](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/net/URLConnection.html) (Proporcionado por AEM)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/) (no recomendado, ya que está obsoleto y se ha sustituido por la versión 4.x)
* [Http correcto](https://square.github.io/okhttp/) (No proporcionado por AEM)

Junto a proporcionar tiempos de espera, también se debe implementar una gestión adecuada de dichos tiempos de espera, así como códigos de estado HTTP inesperados.

## Sin personalizaciones de la interfaz de usuario clásica {#no-classic-ui-customizations}

AEM as a Cloud Service solo admite la IU táctil para el código de cliente de terceros. La IU clásica no está disponible para la personalización.

## Evitar binarios nativos {#avoid-native-binaries}

El código no podrá descargar binarios durante la ejecución ni modificarlos. Por ejemplo, no se podrá desempaquetar `jar` o `tar` archivos.

## No hay binarios de transmisión por AEM as a Cloud Service {#no-streaming-binaries}

Se debe acceder a los binarios a través de la CDN, que servirá binarios fuera de los servicios AEM principales.

Por ejemplo, no utilice `asset.getOriginal().getStream()`, que déclencheur descargar un binario en el disco efímero del servicio de AEM.

## Sin agentes de replicación inversa {#no-reverse-replication-agents}

La replicación inversa de Publicar en Autor no es compatible con AEM as a Cloud Service. Si se necesita dicha estrategia, puede utilizar un almacén de persistencia externa que se comparta entre el conjunto de instancias de publicación y, potencialmente, el clúster de creación.

## Es posible que los agentes de replicación de reenvío necesiten ser transferidos {#forward-replication-agents}

El contenido se duplica de Autor a Publicación a través de un mecanismo pub-sub. No se admiten agentes de replicación personalizados.

## Monitorización y depuración {#monitoring-and-debugging}

### Registros {#logs}

Para el desarrollo local, las entradas de registro se escriben en archivos locales en la variable `/crx-quickstart/logs` carpeta.

En entornos de Cloud, los desarrolladores pueden descargar registros a través de Cloud Manager o utilizar una herramienta de línea de comandos para rastrear los registros. <!-- See the [Cloud Manager documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->

**Configuración del nivel de registro**

Para cambiar los niveles de registro para los entornos de Cloud, la configuración OSGI de registro de Sling debe modificarse, seguida de una reimplementación completa. Como esto no es instantáneo, tenga cuidado de habilitar registros detallados en entornos de producción que reciben mucho tráfico. En el futuro, es posible que haya mecanismos para cambiar más rápidamente el nivel de registro.

>[!NOTE]
>
>Para realizar los cambios de configuración que se enumeran a continuación, debe crearlos en un entorno de desarrollo local y, a continuación, colocarlos en una instancia as a Cloud Service AEM. Para obtener más información sobre cómo hacerlo, consulte [Implementación en AEM as a Cloud Service](/help/implementing/deploying/overview.md).

**Activación del nivel de registro de depuración**

El nivel de registro predeterminado es INFO, es decir, los mensajes DEBUG no se registran. Para activar el nivel de registro DEBUG, actualice la siguiente propiedad al modo de depuración.

`/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level`

Por ejemplo, establezca `/apps/<example>/config/org.apache.sling.commons.log.LogManager.factory.config~<example>.cfg.json` con el siguiente valor.

```json
{
   "org.apache.sling.commons.log.names": [
      "com.example"
   ],
   "org.apache.sling.commons.log.level": "DEBUG",
   "org.apache.sling.commons.log.file": "logs/error.log",
   "org.apache.sling.commons.log.additiv": "false"
}
```

No deje el registro en el nivel de registro de depuración más de lo necesario, ya que esto genera muchas entradas.

Se pueden configurar niveles de registro discretos para los diferentes entornos de AEM utilizando la segmentación de configuración OSGi basada en el modo de ejecución si es deseable iniciar sesión siempre en `DEBUG` durante el desarrollo. Por ejemplo:

| Entorno | Ubicación de configuración de OSGi por modo de ejecución | `org.apache.sling.commons.log.level` valor de propiedad | | - | - | - | | Desarrollo | /apps/example/config/org.apache.sling.commons.log.LogManager.factory.config~example.cfg.json | DEPURACIÓN | | Etapa | /apps/example/config.stage/org.apache.sling.commons.log.LogManager.factory.config~example.cfg.json | WARN | | Producción | /apps/example/config.prod/org.apache.sling.commons.log.LogManager.factory.config~example.cfg.json | ERROR |

Una línea en el archivo de depuración normalmente comienza con DEBUG y, a continuación, proporciona el nivel de registro, la acción del instalador y el mensaje de registro. Por ejemplo:

```text
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

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

Para el desarrollo local, los desarrolladores tienen acceso completo al CRXDE Lite (`/crx/de`) y la consola web AEM (`/system/console`).

Tenga en cuenta que en el desarrollo local (con el SDK), `/apps` y `/libs` se puede escribir en directamente, que es diferente de los entornos de Cloud donde esas carpetas de nivel superior son inmutables.

### AEM herramientas de desarrollo as a Cloud Service {#aem-as-a-cloud-service-development-tools}

Los clientes pueden acceder a CRXDE lite en el entorno de desarrollo del nivel de creación, pero no en la fase o en la producción. El repositorio inmutable (`/libs`, `/apps`) no se puede escribir en durante la ejecución, por lo que al intentar hacerlo se producirán errores.

En su lugar, el Explorador de repositorios se puede iniciar desde Developer Console, proporcionando una vista de solo lectura en el repositorio para todos los entornos en los niveles de autor, publicación y vista previa. Obtenga más información sobre el explorador del repositorio [here](/help/implementing/developing/tools/repository-browser.md).

Hay disponible un conjunto de herramientas para depurar AEM entornos de desarrollador as a Cloud Service en Developer Console para entornos de RDE, desarrollo, fase y producción. La dirección URL se puede determinar ajustando las direcciones url del servicio Autor o Publicación de la siguiente manera:

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

También resulta útil para la depuración, la consola de desarrollador tiene un vínculo a la herramienta Explicar consulta :

![Consola de desarrollo 4](/help/implementing/developing/introduction/assets/devconsole4.png)

En el caso de los programas de producción, el acceso a Developer Console se define mediante la función de desarrollador de Cloud Manager en el Admin Console, mientras que para los programas de simulación de pruebas, Developer Console está disponible para cualquier usuario con un perfil de producto que les permita acceder a AEM as a Cloud Service. Para todos los programas, &quot;Cloud Manager - Developer Role&quot; es necesario para los volcados de estado y el explorador de repositorios y los usuarios también deben definirse en el Perfil de productos de usuarios o administradores de AEM en los servicios de autor y publicación para poder ver los datos de ambos servicios. Para obtener más información sobre la configuración de permisos de usuario, consulte [Documentación de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html).

### Supervisión del rendimiento {#performance-monitoring}

El Adobe supervisa el rendimiento de la aplicación y toma medidas para solucionar el problema si se observa deterioro. En este momento, no se pueden respetar las métricas de la aplicación.

## Envío de correo electrónico {#sending-email}

Las secciones siguientes describen cómo solicitar, configurar y enviar correos electrónicos.

>[!NOTE]
>
>El servicio de correo se puede configurar con compatibilidad con OAuth2. Para obtener más información, consulte [Compatibilidad con OAuth2 para el servicio de correo](/help/security/oauth2-support-for-mail-service.md).

### Activación del correo electrónico saliente {#enabling-outbound-email}

De forma predeterminada, los puertos utilizados para enviar correos electrónicos están desactivados. Para activar un puerto, configure [red avanzada](/help/security/configuring-advanced-networking.md), asegúrese de configurar para cada entorno necesario el `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` reglas de reenvío de puertos del extremo, que asigna el puerto deseado (por ejemplo, 465 o 587) a un puerto proxy.

Se recomienda configurar redes avanzadas con un `kind` parámetro establecido en `flexiblePortEgress` ya que Adobe puede optimizar el rendimiento del tráfico de salida de puerto flexible. Si es necesaria una dirección IP de salida única, elija un `kind` parámetro de `dedicatedEgressIp`. Si ya ha configurado VPN por otros motivos, también puede utilizar la dirección IP única que proporciona esa variación de red avanzada.

Debe enviar un correo electrónico a través de un servidor de correo en lugar de enviarlo directamente a los clientes de correo electrónico. De lo contrario, los correos electrónicos podrían bloquearse.

### Envío de correos electrónicos {#sending-emails}

La variable [Servicio Day CQ Mail Service OSGI](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service) se debe utilizar y los correos electrónicos se deben enviar al servidor de correo indicado en la solicitud de asistencia, en lugar de enviarse directamente a los destinatarios.

### Configuración {#email-configuration}

Los correos electrónicos de AEM deben enviarse utilizando la variable [Servicio Day CQ Mail Service OSGi](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service).

Consulte la [Documentación de AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html) para obtener más información sobre la configuración de correo electrónico. Para AEM as a Cloud Service, tenga en cuenta los siguientes ajustes necesarios en la `com.day.cq.mailer.DefaultMailService OSGI` servicio:

* El nombre de host del servidor SMTP debe establecerse en $[env:AEM_PROXY_HOST;default=proxy.túnel]
* El puerto del servidor SMTP debe establecerse en el valor del puerto proxy original establecido en el parámetro portForwards utilizado en la llamada de API al configurar redes avanzadas. Por ejemplo, 30465 (en lugar de 465)

El puerto del servidor SMTP debe configurarse como el `portDest` valor establecido en el parámetro portForwards utilizado en la llamada de API al configurar redes avanzadas y `portOrig` debe ser un valor significativo que esté dentro del rango requerido de 30000 - 30999. Por ejemplo, si el puerto del servidor SMTP es 465, el puerto 30465 debe utilizarse como `portOrig` valor.

En este caso y suponiendo que SSL necesita estar habilitado, en la configuración de la variable **OSGI de Day CQ Mail Service** servicio:

* Establezca `smtp.port` a `30465`
* Establezca `smtp.ssl` a `true`

Alternativamente, si el puerto de destino es 587, una `portOrig` debe usarse el valor 30587. Y suponiendo que SSL debe deshabilitarse, la configuración del servicio OSGI Day CQ Mail Service:

* Establezca `smtp.port` a `30587`
* Establezca `smtp.ssl` a `false`

La variable `smtp.starttls` se establecerá automáticamente mediante AEM as a Cloud Service durante la ejecución a un valor apropiado. Así, si `smtp.ssl` se establece en true, `smtp.startls` se ignora. If `smtp.ssl` se establece en false, `smtp.starttls` se establece en true. Esto es independientemente de la variable `smtp.starttls` valores configurados en la configuración OSGI.


El servicio de correo puede configurarse opcionalmente con compatibilidad con OAuth2. Para obtener más información, consulte [Compatibilidad con OAuth2 para el servicio de correo](/help/security/oauth2-support-for-mail-service.md).

### Configuración de correo electrónico heredada {#legacy-email-configuration}

Antes de la versión 2021.9.0, el correo electrónico se configuraba mediante una solicitud de asistencia al cliente. Tenga en cuenta los siguientes ajustes necesarios para `com.day.cq.mailer.DefaultMailService OSGI` servicio:

AEM as a Cloud Service requiere que el correo se envíe a través del puerto 465. Si un servidor de correo no admite el puerto 465, se puede utilizar el puerto 587, siempre y cuando la opción TLS esté habilitada.

Si se ha solicitado el puerto 465:

* set `smtp.port` a `465`
* set `smtp.ssl` a `true`

y si se ha solicitado el puerto 587:

* set `smtp.port` a `587`
* set `smtp.ssl` a `false`

La variable `smtp.starttls` se establecerá automáticamente mediante AEM as a Cloud Service durante la ejecución a un valor apropiado. Así, si `smtp.ssl` se establece en true, `smtp.startls` se ignora. If `smtp.ssl` se establece en false, `smtp.starttls` se establece en true. Esto es independientemente de la variable `smtp.starttls` valores configurados en la configuración OSGI.

El host del servidor SMTP debe establecerse en el del servidor de correo.

## Evitar grandes propiedades de varios valores {#avoid-large-mvps}

El repositorio de contenido Oak que subyace AEM as a Cloud Service no está pensado para utilizarse con un número excesivo de propiedades de varios valores (MVP). Una regla general es mantener los MVP por debajo de 1000. Sin embargo, el rendimiento real depende de muchos factores.

Las advertencias se registran de forma predeterminada después de superar los 1000. Son similares a los siguientes.

```text
org.apache.jackrabbit.oak.jcr.session.NodeImpl Large multi valued property [/path/to/property] detected (1029 values). 
```

Los MVP grandes pueden provocar errores debido a que el documento MongoDB supera los 16 MB, lo que provoca errores similares a los siguientes.

```text
Caused by: com.mongodb.MongoWriteException: Resulting document after update is larger than 16777216
```

Consulte la [Documentación de Apache Oak](https://jackrabbit.apache.org/oak/docs/dos_and_donts.html#Large_Multi_Value_Property) para obtener más información.

## [!DNL Assets] directrices de desarrollo y casos de uso {#use-cases-assets}

Para obtener más información sobre los casos de uso de desarrollo, las recomendaciones y los materiales de referencia de los recursos as a Cloud Service, consulte [Referencias del desarrollador para Assets.](/help/assets/developer-reference-material-apis.md#assets-cloud-service-apis)
