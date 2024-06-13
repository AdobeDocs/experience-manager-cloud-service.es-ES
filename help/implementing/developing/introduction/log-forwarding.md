---
title: AEM Reenvío de registros para la as a Cloud Service
description: AEM Obtenga información acerca del reenvío de registros a Splunk y otros proveedores de registro en as a Cloud Service
exl-id: 27cdf2e7-192d-4cb2-be7f-8991a72f606d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: e007f2e3713d334787446305872020367169e6a2
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 1%

---

# Reenvío de registro {#log-forwarding}

>[!NOTE]
>
>Esta función aún no se ha lanzado y es posible que algunos destinos de registro no estén disponibles en el momento del lanzamiento. Mientras tanto, puede abrir un ticket de asistencia para reenviar registros a **Splunk**, tal como se describe en la [artículo de registro](/help/implementing/developing/introduction/logging.md).

AEM Los clientes que tengan una licencia para un proveedor de registro o alojen un producto de registro pueden tener registros de registro (incluidos los registros de Apache/Dispatcher) y registros de CDN reenviados a los destinos de registro asociados. AEM as a Cloud Service admite los siguientes destinos de registro:

* Almacenamiento de Azure Blob
* DataDog
* Elasticsearch o OpenSearch
* HTTPS
* Splunk

El reenvío de registros se configura en forma de autoservicio declarando una configuración en Git e implementándola a través de la canalización de configuración de Cloud Manager para los tipos de entorno de desarrollo, fase y producción en programas de producción (que no sean de zona protegida).

AEM AEM Hay una opción para que los registros de la y de Apache/Dispatcher se enruten a través de infraestructuras de red avanzadas, como la IP de salida dedicada.

Tenga en cuenta que el ancho de banda de red asociado con los registros enviados al destino de registro se consideran parte del uso de E/S de red de su organización.


## Organización de este artículo {#how-organized}

Este artículo está organizado de la siguiente manera:

* Configuración: común para todos los destinos de registro
* Registro de configuraciones de destino: cada destino tiene un formato ligeramente diferente
* Formatos de entrada de registro: información sobre los formatos de entrada de registro
* AEM Redes avanzadas: envío de registros de Apache/Dispatcher y de los recursos de red a través de una salida dedicada o a través de una VPN


## Configuración {#setup}

1. Cree la siguiente estructura de carpetas y archivos en la carpeta de nivel superior del proyecto en Git:

   ```
   config/
        logForwarding.yaml
   ```

1. `logForwarding.yaml` debe contener metadatos y una configuración similar al siguiente formato (utilizamos Splunk como ejemplo).

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

   El **bondadoso** el parámetro debe establecerse en `LogForwarding` la versión debe establecerse en la versión de esquema, que es 1.

   Tokens en la configuración (como `${{SPLUNK_TOKEN}}`) representan secretos que no deberían almacenarse en Git. En su lugar, declárelos como Cloud Manager  [Variables de entorno](/help/implementing/cloud-manager/environment-variables.md) de tipo **secreto**. Asegúrese de seleccionar **Todo** como el valor desplegable del campo Servicio aplicado, de modo que los registros se pueden reenviar a los niveles de creación, publicación y vista previa.

   AEM Es posible establecer diferentes valores entre los registros de CDN y los registros de (incluido Apache/Dispatcher), incluyendo un **cdn** y/o **aem** bloque después de **predeterminado** , donde las propiedades pueden anular las definidas en el **predeterminado** block; solo se requiere la propiedad enabled. Un posible caso de uso podría ser utilizar un índice de Splunk diferente para los registros de CDN, como se ilustra en el ejemplo siguiente.

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

1. Para tipos de entorno distintos de RDE (que actualmente no es compatible), cree una canalización de configuración de implementación de destino en Cloud Manager.

   * [Consulte Configuración de canalizaciones de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md).
   * [Consulte Configuración de canalizaciones que no son de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md).

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

![Configuración de token SAS de Azure Blob](/help/implementing/developing/introduction/assets/azureblob-sas-token-config.png)

#### Registros de CDN de almacenamiento de Azure Blob {#azureblob-cdn}

Cada uno de los servidores de registro distribuidos globalmente generará un nuevo archivo cada pocos segundos, en el `aemcdn` carpeta. Una vez creado, el archivo ya no se anexará a. El formato del nombre de archivo es AAAA-MM-DDThh:mm:ss.sss-uniqueid.log. Por ejemplo, 2024-03-04T10:00:00.000-WnFWYN9BpOUs2aOVn4ee.log.

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

Cada archivo contiene varias entradas de registro json, cada una en una línea independiente. Los formatos de entrada de registro se describen en la [artículo de registro](/help/implementing/developing/introduction/logging.md)y cada entrada de registro también incluye las propiedades adicionales mencionadas en la [Formatos de entrada de registro](#log-format) más abajo.

#### AEM Registros de Azure Blob Storage {#azureblob-aem}

AEM Los registros de datos (incluido Apache/Dispatcher) aparecen debajo de una carpeta con la siguiente convención de nombres:

* aemaccess
* aemerror
* aemdispatcher
* httpdaccess
* httpderror

En cada carpeta, se crea un solo archivo y se anexa a. Los clientes son responsables de procesar y administrar este archivo para que no crezca demasiado.

Consulte los formatos de entrada de registro en la [artículo de registro](/help/implementing/developing/introduction/logging.md). Las entradas de registro también incluirán las propiedades adicionales mencionadas en la variable [Formatos de entrada de registro](#log-formats) más abajo.


### Datadog {#datadog}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  dataDog:
    default:
      enabled: true       
      host: "http-intake.logs.datadoghq.eu"
      token: "${{DATADOG_API_KEY}}"
      
```

Consideraciones:

* Cree una clave de API sin ninguna integración con un proveedor de nube específico.


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
```

Consideraciones:

* Para las credenciales, asegúrese de utilizar credenciales de implementación en lugar de credenciales de cuenta. Estas son las credenciales que se generan en una pantalla que puede parecerse a esta imagen:

![Credenciales de implementación elásticas](/help/implementing/developing/introduction/assets/ec-creds.png)

### HTTPS {#https}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  https:
    default:
      url: "https://example.com/aem_logs/aem"
      authHeaderName: "X-AEMaaCS-Log-Forwarding-Token"
      authHeaderValue: "${{HTTPS_LOG_FORWARDING_TOKEN}}"
```

#### Registros de CDN HTTPS {#https-cdn}

Las solicitudes web (POST) se enviarán de forma continua, con una carga útil json que es una matriz de entradas de registro, con el formato de entrada de registro descrito en [artículo de registro](/help/implementing/developing/introduction/logging.md#cdn-log). Las propiedades adicionales se mencionan en la sección [Formatos de entrada de registro](#log-formats) más abajo.

También debe haber una propiedad denominada `sourcetype`, que se establece en el valor `aemcdn`.

>[!NOTE]
>
> Antes de enviar la primera entrada de registro de CDN, el servidor HTTP debe completar correctamente un desafío único: una solicitud enviada a la ruta ``wellknownpath`` debe responder con ``*``.


#### AEM Registros de HTTPS {#https-aem}

AEM Para los registros de datos (incluido apache/dispatcher), las solicitudes web (POST) se enviarán continuamente, con una carga útil json que es una matriz de entradas de registro, con los distintos formatos de entrada de registro como se describe en la [artículo de registro](/help/implementing/developing/introduction/logging.md). Las propiedades adicionales se mencionan en la sección [Formatos de entrada de registro](#log-format) más abajo.

También debe haber una propiedad denominada `sourcetype`, que se establece en uno de estos valores:

* aemaccess
* aemerror
* aemdispatcher
* httpdaccess
* httpderror

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
      index: "AEMaaCS"
```

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

Consulte la información general [artículo de registro](/help/implementing/developing/introduction/logging.md) AEM para el formato de cada tipo de registro respectivo (registros de CDN y registros de, incluidos Apache/Dispatcher).

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

>[!NOTE]
>
>Esta función aún no está lista para los usuarios que la adoptaron por primera vez.


Algunas organizaciones eligen restringir qué tráfico pueden recibir los destinos de registro.

Para el registro de CDN, puede incluir en la lista de permitidos las direcciones IP, tal como se describe en [este artículo](https://www.fastly.com/documentation/reference/api/utils/public-ip-list/). Si esa lista de direcciones IP compartidas es demasiado grande, considere la posibilidad de enviar tráfico a un almacén de blobs de Azure (que no sea de Adobe) donde se pueda escribir lógica para enviar los registros de una IP dedicada a su destino final.

AEM Para los registros de datos (incluido Apache/Dispatcher), puede configurar el reenvío de registros para que se realice a través de [redes avanzadas](/help/security/configuring-advanced-networking.md). Consulte los patrones para los tres tipos de red avanzados siguientes, que utilizan un `port` junto con el parámetro `host` parámetro.

### Salida de puerto flexible {#flex-port}

Si el tráfico de registro va a un puerto distinto del 443 (por ejemplo, 8443 a continuación), configure la red avanzada de la siguiente manera:

```
{
    "portForwards": [
        {
            "name": "splunk-host.example.com",
            "portDest": 8443, # something other than 443
            "portOrig": 30443
        }    
    ]
}
```

y configure el archivo yaml de la siguiente manera:

```
kind: "LogForwarding"
version: "1"
data:
  splunk:
    default:
      host: "${{AEM_PROXY_HOST}}"
      token: "${{SomeToken}}"
      port: 30443
      index: "index_name"
```

### IP de salida dedicada {#dedicated-egress}


Si el tráfico de registro tiene que salir de una IP de salida dedicada, configure una red avanzada como la siguiente:

```
{
    "portForwards": [
        {
            "name": "splunk-host.example.com",
            "portDest": 443, 
            "portOrig": 30443
        }    
    ]
}
```

y configure el archivo yaml de la siguiente manera:

```
      
kind: "LogForwarding"
version: "1"
   metadata:
     envTypes: ["dev"]
data:
  splunk:
     default:
       enabled: true
       index: "index_name" 
       token: "${{SPLUNK_TOKEN}}"  
     aem:
       enabled: true
       host: "${{AEM_PROXY_HOST}}"
       port: 30443       
     cdn:
       enabled: true
       host: "splunk-host.example.com"
       port: 443    
```

### VPN {#vpn}

Si el tráfico de registro necesita pasar por una VPN, configure una red avanzada como la siguiente:

```
{
    "portForwards": [
        {
            "name": "splunk-host.example.com",
            "portDest": 443,
            "portOrig": 30443
        }    
    ]
}

kind: "LogForwarding"
version: "1"
   metadata:
     envTypes: ["dev"]
data:
  splunk:
     default:
       enabled: true
       index: "index_name" 
       token: "${{SPLUNK_TOKEN}}"  
     aem:
       enabled: true
       host: "${{AEM_PROXY_HOST}}"
       port: 30443       
     cdn:
       enabled: true
       host: "splunk-host.example.com"
       port: 443     
```
