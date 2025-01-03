---
title: Reenvío de registros para AEM as a Cloud Service
description: Obtenga información acerca del reenvío de registros a proveedores de registro en AEM as a Cloud Service
exl-id: 27cdf2e7-192d-4cb2-be7f-8991a72f606d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: f6de6b6636d171b6ab08fdf432249b52c2318c45
workflow-type: tm+mt
source-wordcount: '1781'
ht-degree: 0%

---

# Reenvío de registro {#log-forwarding}

>[!NOTE]
>
>El reenvío de registros ahora se configura de forma de autoservicio, diferente del método heredado, que requería el envío de un ticket de asistencia de Adobe. Consulte la sección [Migración](#legacy-migration) si su reenvío de registro se configuró por Adobe.

AEM Los clientes con una licencia con un proveedor de registro o que alojen un producto de registro pueden tener registros de registro (incluidos los registros de Apache/Dispatcher) y registros de CDN reenviados al destino de registro asociado. AEM as a Cloud Service admite los siguientes destinos de registro:

* Almacenamiento de Azure Blob
* Datadog
* Elasticsearch o OpenSearch
* HTTPS
* Splunk

El reenvío de registros se configura en modo de autoservicio declarando una configuración en Git e implementándola a través de la canalización de configuración de Cloud Manager en los tipos de entorno de RDE, desarrollo, fase y producción en programas de producción (que no sean de zona protegida).

AEM Hay una opción para que los registros de la y de Apache/Dispatcher AEM se enruten a través de infraestructuras de red avanzadas de la interfaz de usuario, como la IP de salida dedicada.

Tenga en cuenta que el ancho de banda de red asociado con los registros enviados al destino de registro se consideran parte del uso de E/S de red de su organización.


## Organización de este artículo {#how-organized}

Este artículo está organizado de la siguiente manera:

* Configuración: común para todos los destinos de registro
* Registro de configuraciones de destino: cada destino tiene un formato ligeramente diferente
* Formatos de entrada de registro: información sobre los formatos de entrada de registro
* AEM Redes avanzadas: envío de registros de Apache/Dispatcher y de los recursos de red a través de una salida dedicada o a través de una VPN
* Migración desde el reenvío de registros heredado: cómo pasar del reenvío de registros configurado anteriormente por Adobe al enfoque de autoservicio


## Configuración {#setup}

1. Cree un archivo con el nombre `logForwarding.yaml`. Debe contener metadatos, tal como se describe en el [artículo de la canalización de configuración](/help/operations/config-pipeline.md#common-syntax) (**kind** debe establecerse en `LogForwarding` y la versión debe establecerse en &quot;1&quot;), con una configuración similar a la siguiente (usamos Splunk como ejemplo).

   ```
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

AEM Es posible establecer diferentes valores entre los registros de CDN y los registros de (incluido Apache/Dispatcher), incluyendo un bloque **cdn** o **aem** adicional después del bloque **default**, donde las propiedades pueden anular las definidas en el bloque **default**; solo se requiere la propiedad enabled. Un posible caso de uso podría ser utilizar un índice de Splunk diferente para los registros de CDN, como se ilustra en el ejemplo siguiente.

```
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

AEM Otro escenario es deshabilitar el reenvío de los registros de CDN o los registros de (incluido Apache/Dispatcher). Por ejemplo, para reenviar solo los registros de CDN, se puede configurar lo siguiente:

```
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

## Configuración de destino de registro {#logging-destinations}

A continuación se enumeran las configuraciones para los destinos de registro admitidos, junto con cualquier consideración específica.

### Almacenamiento de Azure Blob {#azureblob}

```
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

```
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
```

Y luego 30 segundos después:

```
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
   2024-03-04T10:00:30.000-ghi.log
   2024-03-04T10:00:30.000-jkl.log
   2024-03-04T10:00:30.000-mno.log
```

Cada archivo contiene varias entradas de registro json, cada una en una línea independiente. Los formatos de entrada de registro se describen en [Registro para AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md), y cada entrada de registro también incluye las propiedades adicionales que se mencionan en la sección [Formatos de entrada de registro](#log-format) a continuación.

#### AEM Registros de Azure Blob Storage {#azureblob-aem}

AEM Los registros de datos (incluido Apache/Dispatcher) aparecen debajo de una carpeta con la siguiente convención de nombres:

* aemaccess
* aemerror
* aemrequest
* aemdispatcher
* aemhttpdaccess
* aemhttpderror

En cada carpeta, se crea un solo archivo y se anexa a. Los clientes son responsables de procesar y administrar este archivo para que no crezca demasiado.

Consulte los formatos de entrada de registro en [Registro para AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md). Las entradas de registro también incluirán las propiedades adicionales mencionadas en la sección [Formatos de entrada de registro](#log-formats) a continuación.


### Datadog {#datadog}

```
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
* AEM Para los registros de datos, la etiqueta de origen Datadog está establecida en `aemaccess`, `aemerror`, `aemrequest`, `aemdispatcher`, `aemhttpdaccess` o `aemhttpderror`
* Para los registros de CDN, la etiqueta de origen Datadog está establecida en `aemcdn`
* La etiqueta de servicio Datadog está establecida en `adobeaemcloud`, pero puede sobrescribirla en la sección de etiquetas
* Si la canalización de ingesta utiliza etiquetas Datadog para determinar el índice adecuado para los registros de reenvío, compruebe que estas etiquetas estén correctamente configuradas en el archivo YAML de reenvío de registros. Las etiquetas que faltan pueden impedir la ingesta correcta del registro si la canalización depende de ellas.



### Elasticsearch y OpenSearch {#elastic}

```
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

* AEM Para los registros de datos, `index` se ha establecido en `aemaccess`, `aemerror`, `aemrequest`, `aemdispatcher`, `aemhttpdaccess` o `aemhttpderror`
* La propiedad de canalización opcional debe establecerse en el nombre de la canalización de ingesta de Elasticsearch o OpenSearch, que puede configurarse para enrutar la entrada de registro al índice adecuado. El tipo de procesador de la canalización debe establecerse en *script* y el idioma del script debe establecerse en *sin dolor*. Este es un ejemplo de fragmento de script para enrutar las entradas de registro a un índice como aemaccess_dev_26_06_2024:

```
def envType = ctx.aem_env_type != null ? ctx.aem_env_type : 'unknown';
def sourceType = ctx._index;
def date = new SimpleDateFormat('dd_MM_yyyy').format(new Date());
ctx._index = sourceType + "_" + envType + "_" + date;
```

### HTTPS {#https}

```
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

#### Registros de CDN HTTPS {#https-cdn}

Las solicitudes web (POST) se enviarán de manera continua, con una carga útil json que es una matriz de entradas de registro, con el formato de entrada de registro descrito en [Registro para AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md#cdn-log). A continuación se mencionan propiedades adicionales en la sección [Formatos de entrada de registro](#log-formats).

También debe haber una propiedad denominada `sourcetype`, que se ha establecido en el valor `aemcdn`.

>[!NOTE]
>
> Antes de enviar la primera entrada de registro de CDN, el servidor HTTP debe completar correctamente un desafío único: una solicitud enviada a la ruta de acceso ``/.well-known/fastly/logging/challenge`` debe responder con un asterisco ``*`` en el cuerpo y el código de estado 200.

#### AEM Registros de HTTPS {#https-aem}

AEM Para los registros de datos (incluido apache/dispatcher), las solicitudes web (POST) se enviarán continuamente, con una carga útil json que es una matriz de entradas de registro, con los distintos formatos de entrada de registro como se describe en [Registro para AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md). A continuación se mencionan propiedades adicionales en la sección [Formatos de entrada de registro](#log-format).

También debe existir una propiedad denominada `Source-Type`, que se establezca en uno de estos valores:

* aemaccess
* aemerror
* aemrequest
* aemdispatcher
* aemhttpdaccess
* aemhttpderror

### Splunk {#splunk}

```
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


<!--
### Sumo Logic {#sumologic}

   ```
   kind: "LogForwarding"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     splunk:
       default:
         enabled: true
         host: "https://collectors.de.sumologic.com"
         uri: "/receiver/v1/http"
         privateKey: "${{SomeOtherToken}}"
   
   ```   
-->

## Formatos de entrada de registro {#log-formats}

Consulte [Registro para AEM as a Cloud Service AEM](/help/implementing/developing/introduction/logging.md) para ver el formato de cada tipo de registro respectivo (registros de CDN y registros de, incluidos Apache/Dispatcher).

Dado que los registros de varios programas y entornos se pueden reenviar al mismo destino de registro, además de la salida descrita en el artículo de registro, se incluirán las siguientes propiedades en cada entrada de registro:

* aem_env_id
* aem_env_type
* aem_program_id
* aem_tier

Por ejemplo, las propiedades podrían tener los siguientes valores:

```
aem_env_id: 1242
aem_env_type: dev
aem_program_id: 12314
aem_tier: author
```

## Redes avanzadas {#advanced-networking}

Algunas organizaciones eligen restringir qué tráfico pueden recibir los destinos de registro.

Para el registro de CDN, puede incluir en la lista de permitidos las direcciones IP, tal como se describe en [documentación de Fastly: Lista de IP públicas](https://www.fastly.com/documentation/reference/api/utils/public-ip-list/). Si esa lista de direcciones IP compartidas es demasiado grande, considere la posibilidad de enviar tráfico a un servidor https o a un almacén de blobs de Azure (que no sea de Adobe) donde se pueda escribir lógica para enviar los registros de una IP conocida a su destino final.

AEM Para los registros de datos (incluido Apache/Dispatcher), si ha configurado [red avanzada](/help/security/configuring-advanced-networking.md), puede usar la propiedad advancedNetworking para reenviarlos desde una dirección IP de salida dedicada o a través de una VPN.

```
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

## Migración desde el reenvío de registros heredado {#legacy-migration}

Antes de que se lograra la configuración del reenvío de registros mediante un modelo de autoservicio, se solicitaba a los clientes que abrieran vales de soporte, donde el Adobe iniciaría la integración.

Los clientes que hayan sido configurados de esa manera por Adobe son bienvenidos a adaptarse al modelo de autoservicio según su conveniencia. Hay varias razones para realizar esta transición:

* Se ha aprovisionado un nuevo entorno (por ejemplo, un nuevo entorno de desarrollo o RDE).
* Cambios en las credenciales o el punto de conexión de Splunk existentes.
* El Adobe ha configurado el reenvío de registros antes de que los registros de CDN estuvieran disponibles y desea recibir los registros de CDN.
* Una decisión consciente de adaptarse proactivamente al modelo de autoservicio para que su organización tenga el conocimiento incluso antes de que sea necesario un cambio con distinción de tiempo.

Cuando esté listo para migrar, simplemente configure el archivo YAML como se describe en las secciones anteriores. Utilice la canalización de configuración de Cloud Manager para implementar en cada uno de los entornos donde se debe aplicar la configuración.

Se recomienda, pero no es obligatorio, que se implemente una configuración en todos los entornos para que todos estén bajo control de autoservicio. Si no es así, es posible que olvide qué entornos se han configurado mediante Adobe en comparación con los configurados de forma automática.

>[!NOTE]
>
>Los valores del campo `sourcetype` enviados a su índice de Splunk pueden haber cambiado, así que ajústelos en consecuencia.

>[!NOTE]
>
>Cuando se implementa el reenvío de registros en un entorno previamente configurado por la compatibilidad con el Adobe, es posible que reciba registros duplicados durante un máximo de unas horas. Esto finalmente se resolverá automáticamente.

