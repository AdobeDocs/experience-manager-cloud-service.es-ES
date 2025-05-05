---
title: Directrices de desarrollo de AEM as a Cloud Service
description: Conozca las directrices para el desarrollo en AEM as a Cloud Service y sobre las formas importantes en las que difiere de AEM On-Premise y AEM en AMS.
exl-id: 94cfdafb-5795-4e6a-8fd6-f36517b27364
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '2770'
ht-degree: 4%

---

# Directrices de desarrollo de AEM as a Cloud Service {#aem-as-a-cloud-service-development-guidelines}

>[!CONTEXTUALHELP]
>id="development_guidelines"
>title="Directrices de desarrollo de AEM as a Cloud Service"
>abstract="Conozca las directrices para el desarrollo en AEM as a Cloud Service y sobre las formas importantes en las que difiere de AEM On-Premise y AEM en AMS."
>additional-url="https://video.tv.adobe.com/v/345901?captions=spa" text="Demostración de la estructura del paquete"

Este documento presenta directrices para el desarrollo en AEM as a Cloud Service AEM AEM y acerca de formas importantes en las que difiere de la forma en que se realiza en las instalaciones y en la forma en que se realiza en AMS de forma.

## El código debe tener en cuenta el clúster {#cluster-aware}

El código que se ejecuta en AEM as a Cloud Service debe tener en cuenta que siempre se ejecuta en un clúster. Esto significa que siempre hay más de una instancia en ejecución. El código debe ser flexible, especialmente porque una instancia puede detenerse en cualquier momento.

Durante la actualización de AEM as a Cloud Service, hay instancias con el código antiguo y el nuevo ejecutándose en paralelo. Por lo tanto, el código antiguo no debe romperse con el contenido creado por el nuevo código y el nuevo debe poder hacer frente al contenido antiguo.

Si es necesario identificar el principal en el clúster, se puede utilizar la API de detección de Apache Sling para detectarlo.

## Estado en memoria {#state-in-memory}

El estado no debe conservarse en la memoria, sino que debe persistir en el repositorio. De lo contrario, este estado podría perderse si se detiene una instancia.

## Estado en el sistema de archivos {#state-on-the-filesystem}

No utilice el sistema de archivos de la instancia en AEM as a Cloud Service. El disco es efímero y se elimina cuando las instancias se reciclan. Es posible el uso limitado del sistema de archivos para el almacenamiento temporal relacionado con el procesamiento de solicitudes únicas, pero no se debe abusar de él para archivos enormes. Esto se debe a que puede tener un impacto negativo en la cuota de uso de recursos y encontrarse con limitaciones de disco.

Por ejemplo, cuando no se admite el uso del sistema de archivos, el nivel de Publish debe garantizar que los datos que deban persistir se envíen a un servicio externo para un almacenamiento a largo plazo.

## Observación {#observation}

De forma similar, con todo lo que sucede asincrónicamente, como actuar sobre eventos de observación, no se puede garantizar que se ejecute localmente y, por lo tanto, debe utilizarse con cuidado. Esto es así tanto para eventos JCR como para eventos de recursos de Sling. En el momento en que se produce un cambio, la instancia puede eliminarse y reemplazarse por una instancia diferente. Otras instancias de la topología que están activas en ese momento pueden reaccionar a ese evento. En este caso, sin embargo, esto no será un evento local y podría incluso no haber un líder activo en caso de una elección de líder en curso cuando se emita el evento.

## Tareas de fondo y trabajos de larga duración {#background-tasks-and-long-running-jobs}

El código ejecutado como tarea en segundo plano debe suponer que la instancia en la que se está ejecutando puede caerse en cualquier momento. Por lo tanto, el código debe ser flexible y, lo que es más importante, reanudable. Esto significa que si el código se vuelve a ejecutar no debe comenzar desde el principio de nuevo, sino más bien cerca de desde donde lo dejó. Aunque este no es un requisito nuevo para este tipo de código, en AEM as a Cloud Service es más probable que se produzca una eliminación de instancias.

Para minimizar los problemas, si es posible deben evitarse los trabajos de larga duración y, como mínimo, deben poder reanudarse. Para ejecutar estos trabajos, utilice Trabajos de Sling, que tienen una garantía de al menos una vez y, por lo tanto, si se interrumpen, se vuelven a ejecutar lo antes posible. Pero probablemente no deberían empezar desde el principio de nuevo. Para programar estos trabajos, es mejor usar el programador [Sling Jobs](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing), ya que esto nuevamente garantiza la ejecución de al menos una vez.

No utilice el Planificador de Sling Commons para la programación, ya que la ejecución no se puede garantizar. Es más probable que esté programado.

Del mismo modo, con todo lo que se produce de forma asíncrona, como actuar sobre eventos de observación (ya sean eventos JCR o eventos de recursos Sling), no se puede garantizar su ejecución y, por lo tanto, debe utilizarse con cuidado. AEM Esto ya es así para implementaciones de en el presente.

## Conexiones HTTP salientes {#outgoing-http-connections}

Se recomienda encarecidamente que todas las conexiones HTTP salientes establezcan tiempos de espera de conexión y lectura razonables; los valores sugeridos son 1 segundo para el tiempo de espera de conexión y 5 segundos para el tiempo de espera de lectura. Los números exactos deben determinarse en función del rendimiento del sistema backend que gestiona estas solicitudes.

AEM Para el código que no aplica estos tiempos de espera, las instancias de que se ejecutan en AEM as a Cloud Service aplican un tiempo de espera global. Estos valores de tiempo de espera son de 10 segundos para llamadas de conexión y de 60 segundos para llamadas de lectura para conexiones.

El Adobe recomienda el uso de la biblioteca [Apache HttpComponents Client 4.x](https://hc.apache.org/httpcomponents-client-ga/) proporcionada para realizar conexiones HTTP.

Las alternativas que funcionan, pero que pueden requerir que usted proporcione la dependencia son las siguientes:

* AEM [java.net.URL](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/net/URL.html) y/o [java.net.URLConnection](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/net/URLConnection.html) (proporcionados por el usuario)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/) (no se recomienda porque está obsoleto y se ha reemplazado por la versión 4.x)
* AEM [Aceptar Http](https://square.github.io/okhttp/) (No proporcionado por el usuario

Además de proporcionar tiempos de espera, se debe implementar un manejo adecuado de estos tiempos de espera y códigos de estado HTTP inesperados.

## Administrar límites de tasa de solicitud {#rate-limit-handling}

AEM AEM Cuando la tasa de solicitudes entrantes que se van a supera los niveles correctos, responde a las nuevas solicitudes con el código de error HTTP 429. AEM Las aplicaciones que realizan llamadas programáticas a los programas pueden considerar la posibilidad de programar de forma defensiva, reintentando después de unos segundos con una estrategia de retroceso exponencial. AEM Antes de mediados de agosto de 2023, respondió a la misma condición con el código de error HTTP 503.

## Sin personalizaciones de IU clásica {#no-classic-ui-customizations}

AEM as a Cloud Service solo admite la interfaz de usuario táctil para el código de cliente de terceros. La IU clásica no está disponible para la personalización.

## No hay binarios nativos ni bibliotecas nativas {#avoid-native-binaries}

Los binarios y bibliotecas nativos no deben implementarse ni instalarse en entornos en la nube.

Además, el código no debe intentar descargar binarios nativos o extensiones java nativas (por ejemplo, JNI) durante la ejecución.

## Sin binarios de streaming a través de AEM as a Cloud Service {#no-streaming-binaries}

AEM Se debe acceder a los binarios a través de la red de distribución de contenido (CDN), que servirá binarios fuera de los servicios principales de.

Por ejemplo, no use `asset.getOriginal().getStream()`, que almacena en déclencheur AEM la descarga de un binario en el disco efímero del servicio de la unidad de disco de la aplicación de la aplicación de seguridad de la aplicación.

## No hay agentes de replicación inversa {#no-reverse-replication-agents}

La replicación inversa de Publish a Autor no se admite en AEM as a Cloud Service. Si se necesita una estrategia de este tipo, puede utilizar un almacén de persistencia externo que se comparta entre la granja de instancias de Publish y el clúster de creación.

## Es posible que sea necesario trasladar los agentes de replicación avanzada {#forward-replication-agents}

El contenido se duplica de Autor a Publish a través de un mecanismo pub-sub. No se admiten agentes de replicación personalizados.

## No hay sobrecarga de entornos de desarrollo {#overloading-dev-envs}

Los entornos de producción tienen un tamaño mayor para garantizar un funcionamiento estable, mientras que los entornos de ensayo tienen un tamaño similar al de los entornos de producción para garantizar pruebas realistas en condiciones de producción.

Los entornos de desarrollo y de desarrollo rápido deben limitarse al desarrollo, el análisis de errores y las pruebas funcionales, y no están diseñados para procesar cargas de trabajo elevadas ni grandes cantidades de contenido.

Por ejemplo, cambiar una definición de índice en un repositorio de contenido grande en un entorno de desarrollo puede resultar en una reindexación que resulta en un procesamiento excesivo. Las pruebas que requieren contenido sustancial deben ejecutarse en entornos de ensayo.

## Monitorización y depuración {#monitoring-and-debugging}

### Registros {#logs}

Para el desarrollo local, las entradas de registros se escriben en archivos locales en la carpeta `/crx-quickstart/logs`.

En entornos de Cloud, los desarrolladores pueden descargar registros a través de Cloud Manager o utilizar una herramienta de línea de comandos para rastrearlos. <!-- See the [Cloud Manager documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=es) for more details. Custom logs are not supported and so all logs should be output to the error log. -->

**Estableciendo el nivel de registro**

Para cambiar los niveles de registro para los entornos en la nube, se debe modificar la configuración del OSGI de registro de Sling, seguida de una reimplementación completa. Como esto no es instantáneo, tenga cuidado de habilitar registros detallados en entornos de producción que reciben mucho tráfico. En el futuro, es posible que haya mecanismos para cambiar más rápidamente el nivel de registro.

>[!NOTE]
>
>Para realizar los cambios de configuración que se enumeran a continuación, debe crearlos en un entorno de desarrollo local y luego insertarlos en una instancia de AEM as a Cloud Service. Para obtener más información sobre cómo hacerlo, consulte [Implementación en AEM as a Cloud Service](/help/implementing/deploying/overview.md).

**Activando el nivel de registro de depuración**

El nivel de registro predeterminado es INFO, es decir, los mensajes de DEPURACIÓN no se registran. Para activar el nivel de registro DEBUG, actualice la siguiente propiedad al modo de depuración.

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

No deje el registro en el nivel de registro DEBUG más tiempo del necesario, ya que esto genera muchas entradas.

AEM Se pueden establecer niveles de registro discretos para los diferentes entornos de mediante la segmentación de configuración OSGi basada en el modo de ejecución si es deseable iniciar sesión siempre en `DEBUG` durante el desarrollo. Por ejemplo:

| Entorno | Ubicación de configuración de OSGi por modo de ejecución | Valor de propiedad `org.apache.sling.commons.log.level` |
| - | - | - |
| Desarrollo | /apps/example/config/org.apache.sling.commons.log.LogManager.factory.config~example.cfg.json | DEPURAR |
| Escenario | /apps/example/config.stage/org.apache.sling.commons.log.LogManager.factory.config~example.cfg.json | AVISAR |
| Producción | /apps/example/config.prod/org.apache.sling.commons.log.LogManager.factory.config~example.cfg.json | ERROR |

Una línea del archivo de depuración suele comenzar con DEBUG y, a continuación, proporciona el nivel de registro, la acción del instalador y el mensaje de registro. Por ejemplo:

```text
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

Los niveles de registro son los siguientes:

| 0 | Error grave | La acción ha fallado y el instalador no puede continuar. |
|---|---|---|
| 1 | Error | La acción ha fallado. La instalación continúa, pero una parte de CRX no se instaló correctamente y no funcionará. |
| 2 | Advertencia | La acción se realizó correctamente pero se encontraron problemas. Es posible que CRX funcione o no correctamente. |
| 3 | Información | La acción se ha realizado correctamente. |

### Volcados de procesos {#thread-dumps}

Los volcados de hilos en entornos de Cloud se recopilan de forma continua, pero no se pueden descargar de forma automática en este momento. AEM Mientras tanto, póngase en contacto con el servicio de asistencia técnica de la si son necesarios volcados de hilos para depurar un problema, especificando la ventana de tiempo exacta.

## CRX/DE Lite y AEM as a Cloud Service Developer Console {#crxde-lite-and-developer-console}

### Desarrollo local {#local-development}

Para el desarrollo local, los desarrolladores tienen acceso completo al CRXDE Lite AEM (`/crx/de`) y a la consola web de la (`/system/console`).

En el desarrollo local (mediante SDK), `/apps` y `/libs` se pueden escribir directamente en, lo que es diferente de los entornos de la nube, donde esas carpetas de nivel superior son inmutables.

### Herramientas de desarrollo de AEM as a Cloud Service {#aem-as-a-cloud-service-development-tools}

>[!NOTE]
>El Developer Console de AEM as a Cloud Service no debe confundirse con el [*Adobe Developer Console*](https://developer.adobe.com/developer-console/) con nombre similar.
>

>[!NOTE]
>Algunos clientes tendrán la opción de probar una experiencia renovada para AEM Cloud Service Developer Console. Consulte [este artículo](/help/implementing/developing/introduction/aem-developer-console.md) para obtener más información.

Los clientes pueden acceder a la lista CRXDE en el entorno de desarrollo del nivel de creación, pero no en la fase o en la producción. El repositorio inmutable (`/libs`, `/apps`) no se puede escribir en el tiempo de ejecución, por lo que al intentar hacerlo se producirán errores.

En su lugar, el Explorador de repositorios se puede iniciar desde AEM as a Cloud Service Developer Console, lo que proporciona una vista de solo lectura del repositorio para todos los entornos en los niveles de creación, publicación y vista previa. Para obtener más información, consulte [Explorador de repositorios](/help/implementing/developing/tools/repository-browser.md).

Un conjunto de herramientas para depurar entornos de desarrollador de AEM as a Cloud Service está disponible en AEM as a Cloud Service Developer Console para entornos de RDE, desarrollo, fase y producción. La dirección URL se puede determinar ajustando las direcciones URL del autor o del servicio Publish de la siguiente manera:

`https://dev-console-<namespace>.<cluster>.dev.adobeaemcloud.com`

Como método abreviado, se puede utilizar el siguiente comando CLI de Cloud Manager para iniciar AEM as a Cloud Service Developer Console en función de un parámetro de entorno que se describe a continuación:

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

Consulte [Información de la versión](/help/release-notes/home.md) para obtener más información.

Los desarrolladores pueden generar información de estado y resolver varios recursos.

Como se muestra a continuación, la información de estados disponibles incluye el estado de los paquetes, los componentes, las configuraciones de OSGI, los índices de Oak, los servicios OSGI y los trabajos de Sling.

![Consola de desarrollador 1](/help/implementing/developing/introduction/assets/devconsole1.png)

Como se muestra a continuación, los desarrolladores pueden resolver las dependencias y los servlets de los paquetes:

![Consola de desarrollador 2](/help/implementing/developing/introduction/assets/devconsole2.png)

![Consola de desarrollador 3](/help/implementing/developing/introduction/assets/devconsole3.png)

También resulta útil para la depuración, ya que AEM as a Cloud Service Developer Console tiene un vínculo a la herramienta Explicar consulta:

![Consola de desarrollador 4](/help/implementing/developing/introduction/assets/devconsole4.png)

Para los programas de producción, el acceso a AEM as a Cloud Service Developer Console se define mediante la &quot;Cloud Manager - Developer Role&quot; en Adobe Admin Console, mientras que para los programas de zona protegida, AEM as a Cloud Service Developer Console está disponible para cualquier usuario con un perfil de producto que le permita acceder a AEM as a Cloud Service. Para todos los programas, se necesita &quot;Cloud Manager AEM AEM: función de desarrollador&quot; para los volcados de estado y el explorador de repositorios y los usuarios también deben definirse en el perfil de producto de los usuarios o administradores de la en los servicios de autor y publicación para ver los datos de ambos servicios. Para obtener más información sobre cómo configurar permisos de usuario, consulte [Documentación de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html?lang=es).

### Monitorización del rendimiento {#performance-monitoring}

El Adobe supervisa el rendimiento de la aplicación y toma medidas para controlar si se observa deterioro. En este momento, no se pueden observar las métricas de la aplicación.

## Envío de correo electrónico {#sending-email}

Las secciones siguientes describen cómo solicitar, configurar y enviar correos electrónicos.

>[!NOTE]
>
>El servicio de correo se puede configurar con compatibilidad con OAuth2. Para obtener más información, consulte [Compatibilidad con OAuth2 para el servicio de correo](/help/security/oauth2-support-for-mail-service.md).

### Habilitar correo electrónico saliente {#enabling-outbound-email}

De forma predeterminada, los puertos utilizados para enviar correo electrónico están desactivados. Para activar un puerto, configure [red avanzada](/help/security/configuring-advanced-networking.md), asegurándose de establecer para cada entorno necesario las reglas de reenvío de puertos del extremo `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking`, que asigna el puerto deseado (por ejemplo, 465 o 587) a un puerto proxy.

Se recomienda configurar la red avanzada con un parámetro `kind` establecido en `flexiblePortEgress`, ya que el Adobe puede optimizar el rendimiento del tráfico de salida de puerto flexible. Si se necesita una dirección IP de salida única, elija un parámetro `kind` de `dedicatedEgressIp`. Si ya ha configurado una VPN por otros motivos, también puede utilizar la dirección IP única proporcionada por esa variación avanzada de red.

Debe enviar correo electrónico a través de un servidor de correo en lugar de directamente a los clientes de correo electrónico. De lo contrario, es posible que los correos electrónicos se bloqueen.

### Envío de correos electrónicos {#sending-emails}

Se debe usar el servicio OSGI del servicio de correo CQ de [Day](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html?lang=es#configuring-the-mail-service) y los mensajes de correo electrónico se deben enviar al servidor de correo indicado en la solicitud de soporte en lugar de directamente a los destinatarios.

### Configuración {#email-configuration}

AEM Los mensajes de correo electrónico en la dirección de correo electrónico de la dirección de correo electrónico se deben enviar mediante el servicio OSGi de CQ Mail [Day](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html?lang=es#configuring-the-mail-service).

AEM Consulte la [documentación de 6.5 de](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html?lang=es) para obtener más información sobre cómo configurar el correo electrónico. Para AEM as a Cloud Service, tenga en cuenta los siguientes ajustes necesarios en el servicio `com.day.cq.mailer.DefaultMailService OSGI`:

* AEM El nombre de host del servidor SMTP debe establecerse en $[env:_PROXY_HOST;default=proxy.túnel]
* El puerto del servidor SMTP debe establecerse en el valor del puerto proxy original establecido en el parámetro portForwards utilizado en la llamada de API al configurar la red avanzada. Por ejemplo, 30465 (en lugar de 465)

El puerto del servidor SMTP debe establecerse como el valor `portDest` establecido en el parámetro portForwards utilizado en la llamada API al configurar la red avanzada y el valor `portOrig` debe ser un valor significativo que se encuentre dentro del intervalo requerido de 30000 - 30999. Por ejemplo, si el puerto del servidor SMTP es 465, el puerto 30465 debe usarse como el valor `portOrig`.

En este caso, y suponiendo que SSL necesita estar habilitado, en la configuración del servicio **Day CQ Mail Service OSGI**:

* Establecer `smtp.port` en `30465`
* Establecer `smtp.ssl` en `true`

Alternativamente, si el puerto de destino es 587, se debe utilizar un valor `portOrig` de 30587. Y suponiendo que SSL debe estar deshabilitado, la configuración del servicio OSGI Day CQ Mail Service:

* Establecer `smtp.port` en `30587`
* Establecer `smtp.ssl` en `false`

AEM as a Cloud Service establecerá automáticamente la propiedad `smtp.starttls` en tiempo de ejecución en un valor apropiado. Por lo tanto, si `smtp.ssl` se establece en true, `smtp.startls` se omite. Si `smtp.ssl` se establece en falso, `smtp.starttls` se establece en verdadero. Esto es independientemente de los valores de `smtp.starttls` establecidos en la configuración de OSGI.


El servicio de correo puede configurarse opcionalmente con compatibilidad con OAuth2. Para obtener más información, consulte [Compatibilidad con OAuth2 para el servicio de correo](/help/security/oauth2-support-for-mail-service.md).

### Configuración de correo electrónico heredada {#legacy-email-configuration}

Antes de la versión 2021.9.0, el correo electrónico se configuraba mediante una solicitud de asistencia al cliente. Tenga en cuenta los siguientes ajustes necesarios en el servicio `com.day.cq.mailer.DefaultMailService OSGI`:

AEM as a Cloud Service requiere que el correo se envíe a través del puerto 465. Si un servidor de correo no es compatible con el puerto 465, se puede utilizar el puerto 587, siempre y cuando la opción TLS esté habilitada.

Si se ha solicitado el puerto 465:

* se estableció `smtp.port` en `465`
* se estableció `smtp.ssl` en `true`

y si se ha solicitado el puerto 587:

* se estableció `smtp.port` en `587`
* se estableció `smtp.ssl` en `false`

AEM as a Cloud Service establecerá automáticamente la propiedad `smtp.starttls` en tiempo de ejecución en un valor apropiado. Por lo tanto, si `smtp.ssl` se establece en true, `smtp.startls` se omite. Si `smtp.ssl` se establece en falso, `smtp.starttls` se establece en verdadero. Esto es independientemente de los valores de `smtp.starttls` establecidos en la configuración de OSGI.

El host del servidor SMTP debe configurarse como el del servidor de correo.

## Evite las propiedades grandes de varios valores {#avoid-large-mvps}

El repositorio de contenido de Oak subyacente a AEM as a Cloud Service no está diseñado para utilizarse con un número excesivo de propiedades de varios valores (MVP). Una regla general es mantener los MVP por debajo de 1000. Sin embargo, el rendimiento real depende de muchos factores.

Las advertencias se registran de forma predeterminada después de superar los 1000. Son similares a los siguientes.

```text
org.apache.jackrabbit.oak.jcr.session.NodeImpl Large multi valued property [/path/to/property] detected (1029 values). 
```

Los MVP grandes pueden provocar errores debido a que el documento MongoDB supera los 16 MB, lo que resulta en errores similares a los siguientes.

```text
Caused by: com.mongodb.MongoWriteException: Resulting document after update is larger than 16777216
```

Consulte la [documentación de Apache Oak](https://jackrabbit.apache.org/oak/docs/dos_and_donts.html#Large_Multi_Value_Property) para obtener más información.

## Directrices de desarrollo y casos de uso de [!DNL Assets] {#use-cases-assets}

Para obtener más información acerca de los casos de uso de desarrollo, recomendaciones y materiales de referencia para Assets as a Cloud Service, consulte [Referencias de desarrollador para Assets](/help/assets/developer-reference-material-apis.md#assets-cloud-service-apis).
