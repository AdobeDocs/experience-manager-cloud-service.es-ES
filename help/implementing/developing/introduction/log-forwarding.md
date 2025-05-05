---
title: Reenvío de registros para AEM as a Cloud Service
description: Obtenga información acerca del reenvío de registros a proveedores de registro en AEM as a Cloud Service
exl-id: 27cdf2e7-192d-4cb2-be7f-8991a72f606d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: d25c4aa5801d1ef2b746fc207d9c64ddf381bb8e
workflow-type: tm+mt
source-wordcount: '2276'
ht-degree: 1%

---

# Reenvío de registro {#log-forwarding}

>[!NOTE]
>
>El reenvío de registros ahora está configurado de forma de autoservicio, diferente del método heredado, que requería enviar un ticket de asistencia de Adobe. Consulte la sección [Migración](#legacy-migration) si Adobe configuró el reenvío de registros.

Los clientes con una licencia con un proveedor de registro o que alojen un producto de registro pueden hacer que los registros de AEM (incluido Apache/Dispatcher) y los registros de CDN se reenvíen al destino de registro asociado. AEM as a Cloud Service admite los siguientes destinos de registro:

* Amazon S3 (beta privada, consulte la nota más abajo)
* Almacenamiento de Azure Blob
* Datadog
* Elasticsearch o OpenSearch
* HTTPS
* Splunk
* Lógica de sumo (beta privada, consulte la nota más abajo)

El reenvío de registros se configura en modo de autoservicio declarando una configuración en Git y se puede implementar mediante canalizaciones de configuración de Cloud Manager en los tipos de entorno de desarrollo, ensayo y producción. El archivo de configuración se puede implementar en entornos de desarrollo rápido (RDE) mediante herramientas de línea de comandos.

Hay una opción para que los registros de AEM y Apache/Dispatcher se enruten a través de la infraestructura de red avanzada de AEM, como la IP de salida dedicada.

Tenga en cuenta que el ancho de banda de red asociado con los registros enviados al destino de registro se consideran parte del uso de E/S de red de su organización.

>[!NOTE]
>
>Amazon S3 y Sumo Logic están en Private Beta y solo admiten registros de AEM (incluido Apache/Dispatcher).  New Relic a través de HTTPS también está en versión beta privada. Envíe un correo electrónico a [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) para solicitar acceso.

## Organización de este artículo {#how-organized}

Este artículo está organizado de la siguiente manera:

* Configuración: común para todos los destinos de registro
* Transporte y redes avanzadas: se debe considerar la configuración de la red antes de crear la configuración de registro
* Registro de configuraciones de destino: cada destino tiene un formato ligeramente diferente
* Formatos de entrada de registro: información sobre los formatos de entrada de registro
* Migración del reenvío de registros heredado: cómo pasar del reenvío de registros configurado anteriormente por Adobe al enfoque de autoservicio

## Configuración {#setup}

1. Cree un archivo con el nombre `logForwarding.yaml`. Debe contener metadatos, tal como se describe en el [artículo de la canalización de configuración](/help/operations/config-pipeline.md#common-syntax) (**kind** debe establecerse en `LogForwarding` y la versión debe establecerse en &quot;1&quot;), con una configuración similar a la siguiente (usamos Splunk como ejemplo).

   ```yaml
   kind: "LogForwarding"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     splunk:
       default:
         enabled: true
         host: "splunk-host.example.com"
         token: "${{SPLUNK_TOKEN}}"
         index: "AEMaaCS"
   ```

1. Coloque el archivo en algún lugar bajo una carpeta de nivel superior llamada *config* o similar, como se describe en [Uso de canalizaciones de configuración](/help/operations/config-pipeline.md#folder-structure).

1. Para tipos de entorno distintos de RDE (que usa herramientas de línea de comandos), cree una canalización de configuración de implementación de destino en Cloud Manager, como se indica en [esta sección](/help/operations/config-pipeline.md#creating-and-managing); tenga en cuenta que las canalizaciones de pila completa y las canalizaciones de nivel web no implementan el archivo de configuración.

1. Implemente la configuración de.

Los tokens de la configuración (como `${{SPLUNK_TOKEN}}`) representan secretos que no deberían almacenarse en Git. En su lugar, declárelos como Cloud Manager [Variables de entorno secretas](/help/operations/config-pipeline.md#secret-env-vars). Asegúrese de seleccionar **Todos** como valor desplegable para el campo Servicio aplicado, de modo que los registros se puedan reenviar a los niveles de creación, publicación y vista previa.

Es posible establecer diferentes valores entre los registros de CDN y los registros de AEM (incluido Apache/Dispatcher), incluyendo un bloque **cdn** o **aem** adicional después del bloque **default**, donde las propiedades pueden anular las definidas en el bloque **default**; solo se requiere la propiedad enabled. Un posible caso de uso podría ser utilizar un índice de Splunk diferente para los registros de CDN, como se ilustra en el ejemplo siguiente.

```yaml
   kind: "LogForwarding"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     splunk:
       default:
         enabled: true
         host: "splunk-host.example.com"
         token: "${{SPLUNK_TOKEN}}"
         index: "AEMaaCS"
       cdn:
         enabled: true
         token: "${{SPLUNK_TOKEN_CDN}}"
         index: "AEMaaCS_CDN"   
```

Otro escenario es deshabilitar el reenvío de los registros de CDN o de AEM (incluido Apache/Dispatcher). Por ejemplo, para reenviar solo los registros de CDN, se puede configurar lo siguiente:

```yaml
   kind: "LogForwarding"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     splunk:
       default:
         enabled: true
         host: "splunk-host.example.com"
         token: "${{SPLUNK_TOKEN}}"
         index: "AEMaaCS"
       aem:
         enabled: false
```

## Transporte y redes avanzadas {#transport-advancednetworking}

Algunas organizaciones eligen restringir qué tráfico pueden recibir los destinos de registro, otras pueden requerir el uso de puertos que no sean HTTPS (443).  Si es así, será necesario configurar [Redes avanzadas](/help/security/configuring-advanced-networking.md) antes de implementar la configuración del reenvío de registros.

Utilice la tabla siguiente para ver cuáles son los requisitos para la configuración de Red avanzada y Registro en función de si está utilizando el puerto 443 o no, y de si necesita que los registros aparezcan o no desde una dirección IP fija.
&lt;html>
&lt;style>
table, th, td &lbrace;
  border: 1px solid black;
  border-collapse: collapse;
  text-align: center;
&rbrace;
&lt;/style>
<table>
  <tbody>
    <tr>
      <th>Puerto de destino</th>
      <th>¿Requisito para que los registros aparezcan desde una IP fija?</th>
      <th>Redes avanzadas necesarias</th>
      <th>Se necesita definición de puerto LogForwarding.yaml</th>
    </tr>
    <tr>
      <td rowspan="2">HTTPS (443)</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
    </tr>
    <tr>
      <td>Sí</td>
      <td>Sí, <a href="/help/security/configuring-advanced-networking.md#dedicated-egress-ip-address-dedicated-egress-ip-address">salida dedicada</a></td>
      <td>No</td>
    <tr>
    <tr>
      <td rowspan="2">Puerto no estándar (por ejemplo, 8088)</td>
      <td>No</td>
      <td>Sí, <a href="/help/security/configuring-advanced-networking.md#flexible-port-egress-flexible-port-egress">salida flexible</a></td>
      <td>Sí</td>
    </tr>
    <tr>
      <td>Sí</td>
      <td>Sí, <a href="/help/security/configuring-advanced-networking.md#dedicated-egress-ip-address-dedicated-egress-ip-address">salida dedicada</a></td>
      <td>Sí</td>
  </tbody>
</table>
&lt;/html>

>[!NOTE]
>El que los registros aparezcan desde una sola dirección IP viene determinado por la configuración de red avanzada que haya elegido.  Debe utilizarse una salida dedicada para facilitar esto.
>
> La configuración avanzada de redes es un [proceso de dos pasos](/help/security/configuring-advanced-networking.md#configuring-and-enabling-advanced-networking-configuring-enabling) que requiere habilitación a nivel de programa y entorno.

Para los registros de AEM (incluido Apache/Dispatcher), si ha configurado [Redes avanzadas](/help/security/configuring-advanced-networking.md), puede usar la propiedad `aem.advancedNetworking` para reenviarlas desde una dirección IP de salida dedicada o a través de una VPN.

El ejemplo siguiente muestra cómo configurar el registro en un puerto HTTPS estándar con funciones de red avanzadas.

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  splunk:
    default:
      enabled: true
      host: "splunk-host.example.com"
      port: 443
      token: "${{SPLUNK_TOKEN}}"
      index: "aemaacs"
    aem:
      advancedNetworking: true
```

Para los registros de CDN, puede incluir en la lista de permitidos las direcciones IP, tal como se describe en [Documentación de Fastly: Lista de IP públicas](https://www.fastly.com/documentation/reference/api/utils/public-ip-list/). Si esa lista de direcciones IP compartidas es demasiado grande, considere la posibilidad de enviar tráfico a un servidor https o a un almacén de blobs de Azure (que no sea de Adobe) donde se pueda escribir lógica para enviar los registros de una IP conocida a su destino final.

>[!NOTE]
>No es posible que los registros de CDN aparezcan desde la misma dirección IP desde la que aparecen los registros de AEM, esto se debe a que los registros se envían directamente desde Fastly y no desde AEM Cloud Service.

## Configuración de destino de registro {#logging-destinations}

A continuación se enumeran las configuraciones para los destinos de registro admitidos, junto con cualquier consideración específica.

### Amazon S3 {#amazons3}

>[!NOTE]
>
>Registros escritos en S3 periódicamente, cada 10 minutos para cada tipo de archivo de registro.  Esto puede provocar un retraso inicial para los registros que se escriben en S3 una vez que se activa la función.  Encontrará más información sobre por qué existe este comportamiento [aquí](https://docs.fluentbit.io/manual/pipeline/outputs/s3#differences-between-s3-and-other-fluent-bit-outputs).

```yaml
kind: "LogForwarding"
version: "1.0"
data:
  awsS3:
    default:
      enabled: true
      region: "your-bucket-region"
      bucket: "your_bucket_name"
      accessKey: "${{AWS_S3_ACCESS_KEY}}"
      secretAccessKey: "${{AWS_S3_SECRET_ACCESS_KEY}}"
```

Para utilizar el S3 Log Forwarder, deberá preconfigurar un usuario de AWS IAM con la política adecuada para acceder a su bloque S3.  Consulte [aquí](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html) para ver cómo crear las credenciales de usuario de IAM.

La directiva IAM debe permitir al usuario utilizar `s3:putObject`.  Por ejemplo:

```json
{
   "Version": "2012-10-17",
   "Statement": [{
       "Effect": "Allow",
       "Action": [
           "s3:PutObject"
       ],
       "Resource": "arn:aws:s3:::your_bucket_name/*"
   }]
}
```

Consulte [aquí](https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucket-policies.html) para obtener más información sobre la implementación de la directiva de compartimento de AWS.

### Almacenamiento de Azure Blob {#azureblob}

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  azureBlob:
    default:
      enabled: true       
      storageAccountName: "example_acc"
      container: "aem_logs"
      sasToken: "${{AZURE_BLOB_SAS_TOKEN}}
      
```

Se debe utilizar un token SAS para la autenticación. Debe crearse desde la página de firma de acceso compartido, en lugar de desde la página de token de acceso compartido, y debe configurarse con esta configuración:

* Servicios permitidos: se debe seleccionar un blob.
* Recursos permitidos: el objeto debe estar seleccionado.
* Permisos permitidos: Write, Add, Create deben estar seleccionados.
* Una fecha/hora de inicio y de caducidad válidas.

Esta es una captura de pantalla de un ejemplo de configuración de token SAS:

![Configuración del token SAS de Azure Blob](/help/implementing/developing/introduction/assets/azureblob-sas-token-config.png)

Si los registros han dejado de entregarse después de funcionar correctamente anteriormente, compruebe si el token SAS que configuró sigue siendo válido, ya que puede haber caducado.

#### Registros de CDN de almacenamiento de Azure Blob {#azureblob-cdn}

Cada uno de los servidores de registro distribuidos globalmente producirá un nuevo archivo cada pocos segundos, en la carpeta `aemcdn`. Una vez creado, el archivo ya no se anexará a. El formato del nombre de archivo es AAAA-MM-DDThh:mm:ss.ss-uniqueid.log. Por ejemplo, 2024-03-04T10:00:00.000-WnFWYN9BpOUs2aOVn4ee.log.

Por ejemplo, en algún momento:

```text
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
```

Y luego 30 segundos después:

```text
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
   2024-03-04T10:00:30.000-ghi.log
   2024-03-04T10:00:30.000-jkl.log
   2024-03-04T10:00:30.000-mno.log
```

Cada archivo contiene varias entradas de registro json, cada una en una línea independiente. Los formatos de entrada de registro se describen en [Registro para AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md), y cada entrada de registro también incluye las propiedades adicionales que se mencionan en la sección [Formatos de entrada de registro](#log-formats) a continuación.

#### Registros de Azure Blob Storage AEM {#azureblob-aem}

Los registros de AEM (incluido Apache/Dispatcher) aparecen debajo de una carpeta con la siguiente convención de nombres:

* aemaccess
* aemerror
* aemrequest
* aemdispatcher
* aemhttpdaccess
* aemhttpderror

En cada carpeta, se crea un solo archivo y se anexa a. Los clientes son responsables de procesar y administrar este archivo para que no crezca demasiado.

Consulte los formatos de entrada de registro en [Registro para AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md). Las entradas de registro también incluirán las propiedades adicionales mencionadas en la sección [Formatos de entrada de registro](#log-formats) a continuación.

### Datadog {#datadog}

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  datadog:
    default:
      enabled: true       
      host: "http-intake.logs.datadoghq.eu"
      token: "${{DATADOG_API_KEY}}"
      tags:
         tag1: value1
         tag2: value2
      
```

Consideraciones:

* Cree una clave de API sin ninguna integración con un proveedor de nube específico.
* La propiedad tags es opcional
* Para los registros de AEM, la etiqueta de origen Datadog está establecida en `aemaccess`, `aemerror`, `aemrequest`, `aemdispatcher`, `aemhttpdaccess` o `aemhttpderror`
* Para los registros de CDN, la etiqueta de origen Datadog está establecida en `aemcdn`
* La etiqueta de servicio Datadog está establecida en `adobeaemcloud`, pero puede sobrescribirla en la sección de etiquetas
* Si la canalización de ingesta utiliza etiquetas Datadog para determinar el índice adecuado para los registros de reenvío, compruebe que estas etiquetas estén correctamente configuradas en el archivo YAML de reenvío de registros. Las etiquetas que faltan pueden impedir la ingesta correcta del registro si la canalización depende de ellas.

### Elasticsearch y OpenSearch {#elastic}

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  elasticsearch:
    default:
      enabled: true
      host: "example.com"
      user: "${{ELASTICSEARCH_USER}}"
      password: "${{ELASTICSEARCH_PASSWORD}}"
      pipeline: "ingest pipeline name"
```

Consideraciones:

* el puerto predeterminado es 443. Opcionalmente, se puede sobrescribir con una propiedad denominada `port`
* Para las credenciales, asegúrese de utilizar credenciales de implementación en lugar de credenciales de cuenta. Estas son las credenciales que se generan en una pantalla que puede parecerse a esta imagen:

![Credenciales de implementación elásticas](/help/implementing/developing/introduction/assets/ec-creds.png)

* Para los registros de AEM, `index` se ha establecido en `aemaccess`, `aemerror`, `aemrequest`, `aemdispatcher`, `aemhttpdaccess` o `aemhttpderror`
* La propiedad de canalización opcional debe establecerse en el nombre de la canalización de ingesta de Elasticsearch u OpenSearch, que puede configurarse para enrutar la entrada de registro al índice adecuado. El tipo de procesador de la canalización debe establecerse en *script* y el idioma del script debe establecerse en *sin dolor*. Este es un ejemplo de fragmento de script para enrutar las entradas de registro a un índice como aemaccess_dev_26_06_2024:

```text
def envType = ctx.aem_env_type != null ? ctx.aem_env_type : 'unknown';
def sourceType = ctx._index;
def date = new SimpleDateFormat('dd_MM_yyyy').format(new Date());
ctx._index = sourceType + "_" + envType + "_" + date;
```

### HTTPS {#https}

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  https:
    default:
      enabled: true
      url: "https://example.com/aem_logs/aem"
      authHeaderName: "X-AEMaaCS-Log-Forwarding-Token"
      authHeaderValue: "${{HTTPS_LOG_FORWARDING_TOKEN}}"
```

Consideraciones:

* La cadena de dirección URL debe incluir **https://**; de lo contrario, la validación fallará.
* La dirección URL puede incluir un puerto. Por ejemplo, `https://example.com:8443/aem_logs/aem`. Si no se incluye ningún puerto en la cadena URL, se asume el puerto 443 (el puerto HTTPS predeterminado).

#### API de registro de New Relic {#newrelic-https}

Envíe un correo electrónico a [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) para solicitar acceso.

>[!NOTE]
>New Relic proporciona puntos finales específicos de la región en función de dónde se aprovisione su cuenta de New Relic.  Consulte [aquí](https://docs.newrelic.com/docs/logs/log-api/introduction-log-api/#endpoint) para obtener la documentación de New Relic.

#### Registros de CDN HTTPS {#https-cdn}

Las solicitudes web (POST) se enviarán de manera continua, con una carga útil json que es una matriz de entradas de registro, con el formato de entrada de registro descrito en [Registro para AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md#cdn-log). A continuación se mencionan propiedades adicionales en la sección [Formatos de entrada de registro](#log-formats).

También debe haber una propiedad denominada `sourcetype`, que se ha establecido en el valor `aemcdn`.

>[!NOTE]
>
> Antes de enviar la primera entrada de registro de CDN, el servidor HTTP debe completar correctamente un desafío único: una solicitud enviada a la ruta de acceso ``/.well-known/fastly/logging/challenge`` debe responder con un asterisco ``*`` en el cuerpo y el código de estado 200.

#### Registros de AEM HTTPS {#https-aem}

Para los registros de AEM (incluido apache/dispatcher), las solicitudes web (POST) se enviarán continuamente, con una carga útil json que es una matriz de entradas de registro, con los distintos formatos de entrada de registro como se describe en [Registro para AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md). A continuación se mencionan propiedades adicionales en la sección [Formatos de entrada de registro](#log-formats).

También debe existir una propiedad denominada `Source-Type`, que se establezca en uno de estos valores:

* aemaccess
* aemerror
* aemrequest
* aemdispatcher
* aemhttpdaccess
* aemhttpderror

### Splunk {#splunk}

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  splunk:
    default:
      enabled: true
      host: "splunk-host.example.com"
      token: "${{SPLUNK_TOKEN}}"
      index: "aemaacs"
```

Consideraciones:

* El puerto predeterminado es 443. Opcionalmente, se puede sobrescribir con una propiedad denominada `port`.
* El campo sourcetype tendrá uno de los siguientes valores, según el registro específico: *aemaccess*, *aemerror*,
  *aemrequest*, *aemdispatcher*, *aemhttpdaccess*, *aemhttpderror*, *aemcdn*
* Si las IP requeridas se han incluido en la lista de permitidos y los registros siguen sin entregarse, compruebe que no haya reglas de firewall que apliquen la validación de tokens de Splunk. Realiza rápidamente un paso de validación inicial al enviar intencionadamente un token de Splunk no válido. Si el cortafuegos está configurado para finalizar conexiones con tokens de Splunk no válidos, el proceso de validación fallará, lo que impide que Fastly envíe registros a la instancia de Splunk.

>[!NOTE]
>
> [Si se migra](#legacy-migration) del reenvío de registro heredado a este modelo de autoservicio, es posible que los valores del campo `sourcetype` enviados a su índice de Splunk hayan cambiado, por lo que debe ajustarlos en consecuencia.

### Lógica de sumo {#sumologic}

Al configurar Sumo Logic para la ingesta de datos, se le mostrará una &quot;Dirección HTTP Source&quot; que proporciona el host, el URI del receptor y la clave privada en una sola cadena.  Por ejemplo:

`https://collectors.de.sumologic.com/receiver/v1/http/ZaVnC...`

Deberá copiar la última sección de la dirección URL (sin la anterior `/`) y agregarla como [Variable de entorno secreto de CloudManager](/help/operations/config-pipeline.md#secret-env-vars), tal como se describe en la sección [Configuración](#setup) anterior, y luego hacer referencia a esa variable en la configuración.  A continuación se proporciona un ejemplo.

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  sumologic:
    default:
      enabled: true
      collectorURL: "https://collectors.de.sumologic.com/receiver/v1/http"
      privateKey: "${{SUMOLOGIC_PRIVATE_KEY}}"
      index: "aem-logs"
```

>[!NOTE]
> Necesitará una suscripción de Sumo Logic Enterprise para aprovechar la funcionalidad de campo &quot;índice&quot;.  Las suscripciones que no son de empresa tendrán sus registros enrutados a la partición `sumologic_default` como estándar.  Consulte la [Documentación de partición lógica de sumo](https://help.sumologic.com/docs/search/optimize-search-partitions/) para obtener más información.

## Formatos de entrada de registro {#log-formats}

Consulte [Registro para AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md) para ver el formato de cada tipo de registro respectivo (registros de CDN y registros de AEM, incluido Apache/Dispatcher).

Dado que los registros de varios programas y entornos se pueden reenviar al mismo destino de registro, además de la salida descrita en el artículo de registro, se incluirán las siguientes propiedades en cada entrada de registro:

* aem_env_id
* aem_env_type
* aem_program_id
* aem_tier

Por ejemplo, las propiedades podrían tener los siguientes valores:

```text
aem_env_id: 1242
aem_env_type: dev
aem_program_id: 12314
aem_tier: author
```

## Migración desde el reenvío de registros heredado {#legacy-migration}

Antes de que se lograra la configuración del reenvío de registros mediante un modelo de autoservicio, se solicitaba a los clientes que abrieran vales de soporte, donde Adobe iniciaría la integración.

Los clientes que Adobe haya configurado de esta manera pueden adaptarse al modelo de autoservicio según les convenga. Hay varias razones para realizar esta transición:

* Se ha aprovisionado un nuevo entorno (por ejemplo, un nuevo entorno de desarrollo o RDE).
* Cambios en las credenciales o el punto de conexión de Splunk existentes.
* Adobe ha configurado el reenvío de registros antes de que los registros de CDN estuvieran disponibles y desea recibir los registros de CDN.
* Una decisión consciente de adaptarse proactivamente al modelo de autoservicio para que su organización tenga el conocimiento incluso antes de que sea necesario un cambio con distinción de tiempo.

Cuando esté listo para migrar, simplemente configure el archivo YAML como se describe en las secciones anteriores. Utilice la canalización de configuración de Cloud Manager para implementar en cada uno de los entornos donde se debe aplicar la configuración.

Se recomienda, pero no es obligatorio, que se implemente una configuración en todos los entornos para que todos estén bajo control de autoservicio. Si no es así, es posible que olvide qué entornos ha configurado Adobe frente a los configurados de forma automática.

>[!NOTE]
>Los valores del campo `sourcetype` enviados a su índice de Splunk pueden haber cambiado, así que ajústelos en consecuencia.
>
>Cuando se implementa el reenvío de registros en un entorno previamente configurado por el soporte de Adobe, es posible que reciba registros duplicados durante un máximo de unas horas. Esto finalmente se resolverá automáticamente.
