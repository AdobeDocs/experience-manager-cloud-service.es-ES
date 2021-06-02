---
title: Directrices de desarrollo de AEM as a Cloud Service
description: Directrices de desarrollo de AEM as a Cloud Service
exl-id: 94cfdafb-5795-4e6a-8fd6-f36517b27364
source-git-commit: 07a03d603e2a5e0a7d55a64862f991fedebbf93d
workflow-type: tm+mt
source-wordcount: '2301'
ht-degree: 1%

---

# Directrices de desarrollo de AEM as a Cloud Service {#aem-as-a-cloud-service-development-guidelines}

El código que se ejecuta en AEM como Cloud Service debe tener en cuenta que siempre se está ejecutando en un clúster. Esto significa que siempre hay más de una instancia en ejecución. El código debe ser flexible, especialmente porque una instancia puede detenerse en cualquier momento.

Durante la actualización de AEM como Cloud Service, habrá instancias con código antiguo y nuevo ejecutándose en paralelo. Por lo tanto, el código antiguo no debe romper con el contenido creado por el código nuevo y el nuevo código debe poder lidiar con el contenido antiguo.
<!--

>[!NOTE]
> All of the best practices mentioned here hold true for on-premise deployments of AEM, if not stated otherwise. An instance can always stop due to various reasons. However, with Skyline it is more likely to happen therefore an instance stopping is the rule not an exception.

-->

Si es necesario identificar el principal en el clúster, la API de Apache Sling Discovery se puede utilizar para detectarlo.

## Estado en memoria {#state-in-memory}

El estado no debe guardarse en la memoria, sino persistir en el repositorio. De lo contrario, este estado podría perderse si se detiene una instancia.

## Estado en el sistema de archivos {#state-on-the-filesystem}

El sistema de archivos de la instancia no debe utilizarse en AEM como Cloud Service. El disco es efímero y se eliminará cuando se reciclen instancias. Es posible el uso limitado del sistema de archivos para el almacenamiento temporal relacionado con el procesamiento de solicitudes individuales, pero no debería abusarse de archivos enormes. Esto se debe a que puede tener un impacto negativo en la cuota de uso de recursos y tener limitaciones de disco.

Como ejemplo en el que no se admite el uso del sistema de archivos, el nivel Publicar debe garantizar que todos los datos que deban conservarse se envíen a un servicio externo para un almacenamiento a más largo plazo.

## Observación {#observation}

De forma similar, con todo lo que está sucediendo asincrónicamente como la actuación en eventos de observación, no se puede garantizar que se ejecute localmente y, por lo tanto, se debe utilizar con cuidado. Esto se aplica tanto a los eventos de JCR como a los eventos de recursos de Sling. En el momento en que se produce un cambio, la instancia se puede retirar y reemplazar por otra instancia. Otras instancias de la topología que estén activas en ese momento podrán reaccionar ante ese evento. En este caso, sin embargo, esto no será un evento local y podría incluso no haber un líder activo en caso de una elección de líder en curso cuando se publique el evento.

## Tareas en segundo plano y trabajos de larga duración {#background-tasks-and-long-running-jobs}

El código ejecutado como tareas en segundo plano debe suponer que la instancia en la que se está ejecutando se puede desactivar en cualquier momento. Por lo tanto, el código debe ser flexible y la mayoría de las importaciones reanudarlas. Esto significa que si el código se vuelve a ejecutar, no debería comenzar de nuevo desde el principio, sino más bien cerca de donde lo dejó. Aunque este no es un requisito nuevo para este tipo de código, en AEM como Cloud Service es más probable que se produzca una eliminación de instancia.

Para minimizar los problemas, se deben evitar los trabajos de larga duración si es posible, y deben reanudarse como mínimo. Para ejecutar estos trabajos, utilice Sling Jobs, que tienen una garantía de al menos una vez y, por lo tanto, si se interrumpen, se vuelven a ejecutar lo antes posible. Pero probablemente no deberían comenzar de nuevo desde el principio. Para programar estos trabajos, es mejor utilizar el programador [Sling Jobs](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) ya que esta vez es la ejecución de al menos una vez.

El planificador de Sling Commons no debe utilizarse para la programación, ya que la ejecución no puede garantizarse. Es más probable que se programe.

Del mismo modo, con todo lo que está ocurriendo asincrónicamente, como actuar en eventos de observación (ya sean eventos JCR o eventos de recursos Sling), no se puede garantizar que se ejecute y, por lo tanto, se debe utilizar con cuidado. Esto ya se aplica a las implementaciones AEM en el presente.

## Conexiones HTTP salientes {#outgoing-http-connections}

Se recomienda encarecidamente que cualquier conexión HTTP saliente establezca tiempos de conexión y lectura razonables. Para el código que no aplica estos tiempos de espera, AEM instancias que se ejecutan en AEM como Cloud Service impondrán un tiempo de espera global. Estos valores de tiempo de espera son 10 segundos para las llamadas de conexión y 60 segundos para las llamadas de lectura para las conexiones utilizadas por las siguientes bibliotecas Java populares:

Adobe recomienda el uso de la biblioteca [Apache HttpComponents Client 4.x](https://hc.apache.org/httpcomponents-client-ga/) proporcionada para realizar conexiones HTTP.

Las alternativas que se sabe que funcionan, pero que pueden requerir proporcionar la dependencia usted mismo son:

* [java.net.](https://docs.oracle.com/javase/7/docs/api/java/net/URL.html) URLand/or  [java.net.URLConnection](https://docs.oracle.com/javase/7/docs/api/java/net/URLConnection.html)  (proporcionado por AEM)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/)  (no recomendado porque está obsoleto y reemplazado por la versión 4.x)
* [OK Http](https://square.github.io/okhttp/)  (No proporcionado por AEM)

## Ninguna personalización de IU clásica {#no-classic-ui-customizations}

AEM como Cloud Service solo admite la IU táctil para el código de cliente de terceros. La IU clásica no está disponible para la personalización.

## Evitar binarios nativos {#avoid-native-binaries}

El código no podrá descargar binarios durante la ejecución ni modificarlos. Por ejemplo, no podrá desempaquetar archivos `jar` o `tar`.

## No hay binarios de transmisión a través de AEM como Cloud Service {#no-streaming-binaries}

Se debe acceder a los binarios a través de la CDN, que servirá binarios fuera de los servicios AEM principales.

Por ejemplo, no utilice `asset.getOriginal().getStream()`, que déclencheur descargar un binario en el disco efímero del servicio de AEM.

## No hay agentes de replicación inversa {#no-reverse-replication-agents}

La replicación inversa de Publicar en Autor no se admite en AEM como Cloud Service. Si se necesita dicha estrategia, puede utilizar un almacén de persistencia externa que se comparta entre el conjunto de instancias de publicación y, potencialmente, el clúster de creación.

## Es posible que los agentes de replicación de reenvío necesiten portarse {#forward-replication-agents}

El contenido se duplica de Autor a Publicación a través de un mecanismo pub-sub. No se admiten agentes de replicación personalizados.

## Monitorización y depuración {#monitoring-and-debugging}

### Registros {#logs}

Para el desarrollo local, las entradas de registro se escriben en archivos locales de la carpeta `/crx-quickstart/logs` .

En entornos de Cloud, los desarrolladores pueden descargar registros a través de Cloud Manager o utilizar una herramienta de línea de comandos para rastrear los registros. <!-- See the [Cloud Manager documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->

**Configuración del nivel de registro**

Para cambiar los niveles de registro para los entornos de Cloud, la configuración OSGI de registro de Sling debe modificarse, seguida de una reimplementación completa. Como esto no es instantáneo, tenga cuidado de habilitar registros detallados en entornos de producción que reciben mucho tráfico. En el futuro, es posible que haya mecanismos para cambiar más rápidamente el nivel de registro.

>[!NOTE]
>
>Para realizar los cambios de configuración que se enumeran a continuación, debe crearlos en un entorno de desarrollo local y, a continuación, insertarlos en una AEM como instancia de Cloud Service. Para obtener más información sobre cómo hacerlo, consulte [Implementación para AEM como Cloud Service](/help/implementing/deploying/overview.md).

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

### Herramientas de desarrollo de AEM as a Cloud Service {#aem-as-a-cloud-service-development-tools}

Los clientes pueden acceder a CRXDE lite en el entorno de desarrollo del nivel de creación, pero no en la fase o en la producción. El repositorio inmutable (`/libs`, `/apps`) no se puede escribir en durante la ejecución, por lo que al intentar hacerlo se producirán errores.

En Developer Console hay disponible un conjunto de herramientas para depurar AEM como entornos de desarrollador Cloud Service para entornos de desarrollo, fase y producción. La dirección URL se puede determinar ajustando las direcciones url del servicio Autor o Publicación de la siguiente manera:

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

En el caso de los programas de producción, el acceso a Developer Console se define mediante la función de desarrollador de Cloud Manager en el Admin Console, mientras que para los programas de simulación de pruebas, Developer Console está disponible para cualquier usuario con un perfil de producto que les permita acceder a AEM como Cloud Service. Para todos los programas, &quot;Cloud Manager - Developer Role&quot; es necesario para los volcados de estado y los usuarios también deben definirse en el perfil de producto de los usuarios de AEM o de los administradores de AEM en los servicios de autor y publicación para ver los datos de volcado de estado de ambos servicios. Para obtener más información sobre la configuración de permisos de usuario, consulte [Documentación de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html).

### Servicio de Ensayo y Producción de AEM {#aem-staging-and-production-service}

Los clientes no tendrán acceso a las herramientas para desarrolladores para entornos de ensayo y producción.

### Monitorización del rendimiento {#performance-monitoring}

El Adobe supervisa el rendimiento de la aplicación y toma medidas para solucionar el problema si se observa deterioro. En este momento, no se pueden respetar las métricas de la aplicación.

## Dirección IP de salida dedicada {#dedicated-egress-ip-address}

Si se solicita, AEM como Cloud Service proporcionará una dirección IP estática y dedicada para el tráfico saliente HTTP (puerto 80) y HTTPS (puerto 443) programado en el código Java.

### Ventajas {#benefits}

Esta dirección IP dedicada puede mejorar la seguridad al integrarse con proveedores de SaaS (como un proveedor CRM) u otras integraciones fuera de AEM como Cloud Service que ofrecen una lista de permitidos de direcciones IP. Al agregar la dirección IP dedicada a la lista de permitidos, se garantiza que solo el tráfico del Cloud Service de AEM del cliente pueda fluir al servicio externo. Esto se suma al tráfico de cualquier otra IP permitida.

Sin la función de dirección IP dedicada habilitada, el tráfico que sale de AEM como Cloud Service fluye a través de un conjunto de IP compartidas con otros clientes.

### Configuración {#configuration}

Para habilitar una dirección IP dedicada, envíe una solicitud al Servicio de atención al cliente, que proporcionará la información de la dirección IP. La solicitud debe especificar cada entorno y se deben realizar solicitudes adicionales si nuevos entornos necesitan la función después de la solicitud inicial. No se admiten entornos de programa de espacio aislado.

### Uso de características {#feature-usage}

La función es compatible con el código Java o las bibliotecas que resultan en tráfico saliente, siempre que utilicen propiedades estándar del sistema Java para las configuraciones de proxy. En la práctica, esto debería incluir las bibliotecas más comunes.

A continuación se muestra un ejemplo de código:

```
public JSONObject getJsonObject(String relativePath, String queryString) throws IOException, JSONException {
  String relativeUri = queryString.isEmpty() ? relativePath : (relativePath + '?' + queryString);
  URL finalUrl = endpointUri.resolve(relativeUri).toURL();
  URLConnection connection = finalUrl.openConnection();
  connection.addRequestProperty("Accept", "application/json");
  connection.addRequestProperty("X-API-KEY", apiKey);

  try (InputStream responseStream = connection.getInputStream(); Reader responseReader = new BufferedReader(new InputStreamReader(responseStream, Charsets.UTF_8))) {
    return new JSONObject(new JSONTokener(responseReader));
  }
}
```

La misma IP dedicada se aplica a todos los programas de un cliente en su organización de Adobe y a todos los entornos de cada uno de sus programas. Se aplica tanto a los servicios de autor como de publicación.

Solo se admiten puertos HTTP y HTTPS. Esto incluye HTTP/1.1, así como HTTP/2 cuando está cifrado.

### Consideraciones de depuración {#debugging-considerations}

Para validar que el tráfico es realmente saliente en la dirección IP dedicada esperada, compruebe los registros en el servicio de destino, si está disponible. De lo contrario, puede resultar útil llamar a un servicio de depuración como [https://ifconfig.me/ip](https://ifconfig.me/ip), que devolverá la dirección IP que realiza la llamada.

## Envío de correo electrónico {#sending-email}

AEM como Cloud Service requiere que el correo saliente se encripte. Las secciones siguientes describen cómo solicitar, configurar y enviar correos electrónicos.

### Solicitud de acceso {#requesting-access}

De forma predeterminada, el correo electrónico saliente está desactivado. Para activarlo, envíe un ticket de asistencia con:

1. El nombre de dominio completo del servidor de correo (por ejemplo, `smtp.sendgrid.net`)
1. El puerto que se va a utilizar. Debe ser puerto 465 si es compatible con el servidor de correo; de lo contrario, puerto 587. Tenga en cuenta que el puerto 587 solo se puede usar si el servidor de correo requiere y aplica TLS en ese puerto
1. ID de programa e ID de entorno para los entornos desde los que desee enviar el correo
1. Indica si se necesita acceso SMTP en el autor, la publicación o ambos.

### Envío de correos electrónicos {#sending-emails}

El [servicio OSGI del servicio de correo de CQ Day](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service) debe usarse y los correos electrónicos deben enviarse al servidor de correo indicado en la solicitud de asistencia, en lugar de enviarse directamente a los destinatarios.

AEM CS requiere que el correo se envíe a través del puerto 465. Si un servidor de correo no admite el puerto 465, se puede utilizar el puerto 587, siempre y cuando la opción TLS esté habilitada.

>[!NOTE]
>
>Tenga en cuenta que el Adobe no admite la representación SMTP a través de una dirección IP dedicada única.

### Configuración {#email-configuration}

Los correos electrónicos de AEM deben enviarse utilizando el [Day CQ Mail Service OSGi service](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service).

Consulte la [AEM documentación de 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html) para obtener más información sobre la configuración del correo electrónico. Para AEM como Cloud Service, se deben realizar los siguientes ajustes en el servicio `com.day.cq.mailer.DefaultMailService OSGI`:

Si se ha solicitado el puerto 465:

* establezca `smtp.port` en `465`
* establezca `smtp.ssl` en `true`

Si se ha solicitado el puerto 587 (solo se permite si el servidor de correo no admite el puerto 465):

* establezca `smtp.port` en `587`
* establezca `smtp.ssl` en `false`

La propiedad `smtp.starttls` se establecerá automáticamente AEM como Cloud Service en tiempo de ejecución con un valor apropiado. Por lo tanto, si `smtp.tls` se establece en true, `smtp.startls` se omite. Si `smtp.ssl` se establece en false, `smtp.starttls` se establece en true. Esto es independientemente de los valores `smtp.starttls` establecidos en la configuración OSGI.

## Recommendations y directrices para [!DNL Assets] {#use-cases-assets}

Para obtener información sobre los casos de uso de desarrollo, las recomendaciones y los materiales de referencia para Assets como Cloud Service, consulte [Referencias del desarrollador para Assets](/help/assets/developer-reference-material-apis.md#assets-cloud-service-apis).
