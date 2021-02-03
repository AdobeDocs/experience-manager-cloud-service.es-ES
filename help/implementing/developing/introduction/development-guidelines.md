---
title: Directrices de desarrollo de AEM as a Cloud Service
description: Directrices de desarrollo de AEM as a Cloud Service
translation-type: tm+mt
source-git-commit: a01a55f85639613e5febd2588c9c55590f888124
workflow-type: tm+mt
source-wordcount: '2284'
ht-degree: 1%

---


# Directrices de desarrollo de AEM as a Cloud Service {#aem-as-a-cloud-service-development-guidelines}

El código que se ejecuta en AEM como Cloud Service debe ser consciente del hecho de que siempre se ejecuta en un clúster. Esto significa que siempre hay más de una instancia en ejecución. El código debe ser flexible, especialmente porque una instancia puede detenerse en cualquier momento.

Durante la actualización de AEM como Cloud Service, habrá instancias con código antiguo y nuevo ejecutándose en paralelo. Por lo tanto, el código antiguo no debe romperse con el contenido creado por el nuevo código y el nuevo código debe ser capaz de tratar el contenido antiguo.
<!--

>[!NOTE]
> All of the best practices mentioned here hold true for on-premise deployments of AEM, if not stated otherwise. An instance can always stop due to various reasons. However, with Skyline it is more likely to happen therefore an instance stopping is the rule not an exception.

-->

Si existe la necesidad de identificar el principal en el clúster, la API de Apache Sling Discovery puede utilizarse para detectarlo.

## Estado en memoria {#state-in-memory}

El estado no debe guardarse en la memoria sino en el repositorio. De lo contrario, este estado podría perderse si se detiene una instancia.

## Estado en el sistema de archivos {#state-on-the-filesystem}

El sistema de archivos de la instancia no debe utilizarse en AEM como Cloud Service. El disco es efímero y se eliminará cuando se reciclen las instancias. Es posible el uso limitado del sistema de archivos para almacenamientos temporales relacionados con el procesamiento de solicitudes individuales, pero no se debe abusar de archivos enormes. Esto se debe a que puede tener un impacto negativo en la cuota de uso de recursos y tener limitaciones de disco.

Como ejemplo en el caso de que no se admita el uso del sistema de archivos, el nivel Publicar debe garantizar que todos los datos que deban conservarse se envíen a un servicio externo para un almacenamiento a largo plazo.

## Observación {#observation}

De manera similar, con todo lo que sucede asincrónicamente como actuar en eventos de observación, no se puede garantizar que se ejecute localmente y, por lo tanto, debe usarse con cuidado. Esto es válido tanto para eventos JCR como para eventos de recursos Sling. En el momento en que se produce un cambio, la instancia se puede retirar y reemplazar por otra instancia. Otras instancias de la topología que estén activas en ese momento podrán reaccionar a ese evento. En este caso, sin embargo, esto no será un evento local y podría incluso no haber un líder activo en caso de una elección de líder en curso cuando se publique el evento.

## Tareas en segundo plano y trabajos de larga duración {#background-tasks-and-long-running-jobs}

El código ejecutado como tareas en segundo plano debe suponer que la instancia en la que se está ejecutando se puede desactivar en cualquier momento. Por lo tanto, el código debe ser resiliente y la mayoría de las importaciones deben poder reanudarse. Esto significa que si el código se vuelve a ejecutar, no debería volver a inicio desde el principio, sino más bien cerca de donde lo dejó. Aunque este no es un nuevo requisito para este tipo de código, en AEM como Cloud Service es más probable que se produzca una eliminación de instancia.

Para minimizar el problema, se deben evitar los trabajos de larga duración si es posible, y se deben reanudar al menos. Para ejecutar estos trabajos, utilice Sling Jobs, que cuenta con una garantía de al menos una vez y por lo tanto si se interrumpen, será reejecutado lo antes posible. Pero probablemente no deberían volver a inicio desde el principio. Para programar estos trabajos, es mejor utilizar el Planificador [Trabajos de Sling](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) ya que esta vez se ejecuta al menos una vez.

El Planificador de Sling Commons no debe ser usado para programar, ya que no se puede garantizar la ejecución. Es más probable que se programe.

De manera similar, con todo lo que está sucediendo asincrónicamente, como actuar en eventos de observación (ya sean eventos JCR o eventos de recursos Sling), no se puede garantizar que se ejecute y, por lo tanto, se debe usar con cuidado. Esto ya se aplica a AEM implementaciones en el presente.

## Conexiones HTTP salientes {#outgoing-http-connections}

Se recomienda encarecidamente que cualquier conexión HTTP saliente establezca tiempos de conexión y de espera de lectura razonables. Para el código que no aplica estos tiempos de espera, AEM instancias que se ejecutan en AEM como Cloud Service exigirán tiempos de espera globales. Estos valores de tiempo de espera son de 10 segundos para llamadas de conexión y de 60 segundos para llamadas de lectura para conexiones utilizadas por las siguientes bibliotecas de Java populares:

Adobe recomienda el uso de la biblioteca [Apache HttpComponents Client 4.x](https://hc.apache.org/httpcomponents-client-ga/) proporcionada para realizar conexiones HTTP.

Las alternativas que se sabe que funcionan, pero que pueden requerir que usted mismo proporcione la dependencia son:

* [java.net.](https://docs.oracle.com/javase/7/docs/api/java/net/URL.html) URLand/o  [java.net.URLConnection](https://docs.oracle.com/javase/7/docs/api/java/net/URLConnection.html) (proporcionado por AEM)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/)  (no recomendado porque está obsoleto y reemplazado por la versión 4.x)
* [Aceptar HTTP](https://square.github.io/okhttp/)  (no proporcionado por AEM)

## No hay personalizaciones clásicas de la interfaz de usuario {#no-classic-ui-customizations}

AEM como Cloud Service solo admite la IU táctil para el código de cliente de terceros. La IU clásica no está disponible para la personalización.

## Evitar binarios nativos {#avoid-native-binaries}

El código no podrá descargar archivos binarios en tiempo de ejecución ni modificarlos. Por ejemplo, no podrá desempaquetar `jar` ni `tar` archivos.

## Ningún binario de flujo a través de AEM como Cloud Service {#no-streaming-binaries}

Se debe acceder a los binarios a través de la CDN, que servirá binarios fuera de los servicios principales de AEM.

Por ejemplo, no utilice `asset.getOriginal().getStream()`, que déclencheur descargar un binario en el disco efímero del servicio de AEM.

## No hay agentes de replicación inversa {#no-reverse-replication-agents}

La replicación inversa de Publicar en autor no se admite en AEM como Cloud Service. Si se necesita una estrategia de este tipo, puede utilizar un almacén de persistencia externo que se comparte entre el conjunto de instancias de Publish y, potencialmente, el clúster de Autor.

## Es posible que los agentes de replicación de avanzada necesiten portarse {#forward-replication-agents}

El contenido se replica de Autor a Publicación mediante un mecanismo de subprocesamiento de pub. No se admiten los agentes de replicación personalizados.

## Monitoreo y depuración {#monitoring-and-debugging}

### Registros {#logs}

Para el desarrollo local, las entradas de registro se escriben en archivos locales de la carpeta `/crx-quickstart/logs`.

En los entornos de Cloud, los desarrolladores pueden descargar registros a través de Cloud Manager o utilizar una herramienta de línea de comandos para reducir los registros. <!-- See the [Cloud Manager documentation](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->

**Configuración del nivel de registro**

Para cambiar los niveles de registro de los entornos de nube, se debe modificar la configuración de OSGI de registro de Sling, seguida de una reimplementación completa. Dado que esto no es instantáneo, tenga cuidado de habilitar los registros detallados en entornos de producción que reciben mucho tráfico. En el futuro, es posible que haya mecanismos para cambiar más rápidamente el nivel de registro.

>[!NOTE]
>
>Para realizar los cambios de configuración que se indican a continuación, debe crearlos en un entorno de desarrollo local y luego insertarlos en un AEM como una instancia de Cloud Service. Para obtener más información sobre cómo hacerlo, consulte [Implementación para AEM como Cloud Service](/help/implementing/deploying/overview.md).

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

### Volcados de subprocesos {#thread-dumps}

Los volcados de subprocesos en entornos de la nube se recopilan de forma continua, pero no se pueden descargar de forma automática en este momento. Mientras tanto, póngase en contacto con el servicio de soporte AEM si se necesitan volcados de subprocesos para depurar un problema, especificando la hora exacta.

## CRX/DE Lite y la consola de desarrollador {#crxde-lite-and-developer-console}

### Desarrollo local {#local-development}

Para el desarrollo local, los desarrolladores tienen acceso completo al CRXDE Lite (`/crx/de`) y a la consola web de AEM (`/system/console`).

Tenga en cuenta que en el desarrollo local (con el inicio rápido listo para la nube), `/apps` y `/libs` se pueden escribir directamente en, lo cual es diferente de los entornos de nube donde las carpetas de nivel superior son inmutables.

### AEM como herramientas de desarrollo de Cloud Service {#aem-as-a-cloud-service-development-tools}

Los clientes pueden acceder a la lista CRXDE en el entorno de desarrollo de la capa de creación, pero no en fase ni en producción. El repositorio inmutable (`/libs`, `/apps`) no se puede escribir en tiempo de ejecución, por lo que intentar hacerlo provocará errores.

Hay un conjunto de herramientas para depurar AEM como entornos de desarrollador Cloud Service disponibles en la consola de desarrollador para entornos de desarrollo, etapa y producción. La dirección URL se puede determinar ajustando las direcciones URL del servicio Autor o Publicación de la siguiente manera:

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

Para los programas regulares, el acceso a la consola de desarrollador se define mediante el &quot;Administrador de la nube - Función de desarrollador&quot; en el Admin Console, mientras que para los programas de simulación de pruebas, la consola de desarrollador está disponible para cualquier usuario con un perfil de producto que les permita acceder a AEM como Cloud Service. Para todos los programas, &quot;Cloud Manager - Función de desarrollador&quot; es necesario para los volcados de estado y los usuarios también deben definirse en el Perfil de producto de los usuarios de AEM o administradores de AEM en los servicios de creación y publicación para poder vista los datos de volcado de estado de ambos servicios. Para obtener más información sobre la configuración de permisos de usuario, consulte [Documentación del Administrador de nube](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html).


### Servicio de ensayo y producción de AEM {#aem-staging-and-production-service}

Los clientes no tendrán acceso a las herramientas para desarrolladores para entornos de ensayo y producción.

### Monitoreo del performance {#performance-monitoring}

El Adobe supervisa el rendimiento de la aplicación y toma medidas para corregir el deterioro. En este momento, las métricas de la aplicación no se pueden respetar.

## Dirección IP de salida dedicada {#dedicated-egress-ip-address}

Si se solicita, AEM como Cloud Service proporcionará una dirección IP estática y dedicada para el tráfico saliente HTTP (puerto 80) y HTTPS (puerto 443) programado en el código Java.

### Beneficios {#benefits}

Esta dirección IP dedicada puede mejorar la seguridad al integrarse con proveedores de SaaS (como un proveedor de CRM) u otras integraciones fuera de AEM como Cloud Service que oferta una lista de permitidos de direcciones IP. Al agregar la dirección IP dedicada a la lista de permitidos, se asegura de que sólo el tráfico del Cloud Service de AEM del cliente pueda fluir al servicio externo. Esto se suma al tráfico de cualquier otra IP permitida.

Sin la característica de dirección IP dedicada habilitada, el tráfico que sale de AEM como Cloud Service fluye a través de un conjunto de direcciones IP compartidas con otros clientes.

### Configuración {#configuration}

Para habilitar una dirección IP dedicada, envíe una solicitud a la asistencia al cliente, que le proporcionará la información de la dirección IP. La solicitud debe especificar cada entorno y se deben realizar solicitudes adicionales si los nuevos entornos necesitan la función después de la solicitud inicial. No se admiten entornos de programa de Simulador para pruebas.

### Uso de funciones {#feature-usage}

La función es compatible con el código Java o las bibliotecas que resultan en tráfico saliente, siempre que utilicen las propiedades estándar del sistema Java para las configuraciones de proxy. En la práctica, esto debería incluir las bibliotecas más comunes.

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

La misma IP dedicada se aplica a todos los programas de un cliente en su organización de Adobe y a todos los entornos de cada uno de sus programas. Se aplica a los servicios de creación y publicación.

Solo se admiten los puertos HTTP y HTTPS. Esto incluye HTTP/1.1, así como HTTP/2 cuando se cifra.

### Consideraciones de depuración {#debugging-considerations}

Para validar que el tráfico sea realmente saliente en la dirección IP dedicada esperada, compruebe los registros en el servicio de destino, si están disponibles. De lo contrario, puede resultar útil llamar a un servicio de depuración como [https://ifconfig.me/ip](https://ifconfig.me/ip), que devolverá la dirección IP que llama.

## Enviando correo electrónico {#sending-email}

AEM como Cloud Service requiere que el correo saliente esté cifrado. Las secciones siguientes describen cómo solicitar, configurar y enviar correo electrónico.

### Solicitando acceso {#requesting-access}

De forma predeterminada, el correo electrónico saliente está desactivado. Para activarlo, envíe un ticket de asistencia técnica con:

1. El nombre de dominio completo para el servidor de correo (por ejemplo, `smtp.sendgrid.net`)
1. El puerto que se va a utilizar. Debe ser el puerto 465 si es compatible con el servidor de correo, de lo contrario puerto 587. Tenga en cuenta que el puerto 587 solo se puede usar si el servidor de correo requiere y aplica TLS en ese puerto
1. El ID de programa y el ID de entorno de los entornos de los que les gustaría enviar por correo
1. Si se necesita acceso SMTP en el autor, la publicación o ambos.

### Envío de correos electrónicos {#sending-emails}

El [servicio OSGI del servicio de correo de CQ diario](https://docs.adobe.com/content/help/en/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service) debe usarse y los correos electrónicos deben enviarse al servidor de correo indicado en la solicitud de soporte en lugar de directamente a los destinatarios.

AEM CS requiere que el correo se envíe a través del puerto 465. Si un servidor de correo no admite el puerto 465, se puede utilizar el puerto 587, siempre que la opción TLS esté habilitada.

>[!NOTE]
>
>Tenga en cuenta que Adobe no admite el bloqueo SMTP a través de una dirección IP exclusiva dedicada.

### Configuración {#email-configuration}

Los correos electrónicos de AEM deben enviarse mediante el servicio OSGi [Day CQ Mail Service](https://docs.adobe.com/content/help/en/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service).

Consulte la [documentación de AEM 6.5](https://docs.adobe.com/content/help/en/experience-manager-65/administering/operations/notification.html) para obtener más información sobre la configuración de la configuración de correo electrónico. Para AEM como Cloud Service, se deben realizar los siguientes ajustes en el servicio `com.day.cq.mailer.DefaultMailService OSGI`:

Si se ha solicitado el puerto 465:

* set `smtp.port` to `465`
* set `smtp.ssl` to `true`

Si se ha solicitado el puerto 587 (solo se permite si el servidor de correo no admite el puerto 465):

* set `smtp.port` to `587`
* set `smtp.ssl` to `false`

La propiedad `smtp.starttls` se establecerá automáticamente por AEM como Cloud Service en tiempo de ejecución con un valor adecuado. Por lo tanto, si `smtp.tls` se establece en true, `smtp.startls` se omite. Si `smtp.ssl` se establece en false, `smtp.starttls` se establece en true. Esto es independientemente de los valores `smtp.starttls` establecidos en la configuración OSGI.