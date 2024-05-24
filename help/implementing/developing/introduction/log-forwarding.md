---
title: AEM Reenvío de registros para la as a Cloud Service
description: AEM Obtenga información acerca del reenvío de registros a Splunk y otros proveedores de registro en as a Cloud Service
hide: true
hidefromtoc: true
source-git-commit: d41390696383f8e430bb31bd8d56a5e8843f1257
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 3%

---


# Reenvío de registros {#log-forwarding}

>[!NOTE]
>
>Esta función aún no se ha lanzado y es posible que algunos destinos de registro no estén disponibles en el momento del lanzamiento. Mientras tanto, puede abrir un ticket de asistencia para reenviar registros a **Splunk**, tal como se describe en la [artículo de registro](/help/implementing/developing/introduction/logging.md).

AEM Los clientes que tengan una licencia para un proveedor de registro o alojen un producto de registro pueden tener registros de Apache, Apache/Dispatcher y CDN reenviados a los destinos de registro asociados. AEM as a Cloud Service admite los siguientes destinos de registro:

* Almacenamiento de Azure Blob
* DataDog
* Elasticsearch o OpenSearch
* HTTPS
* Splunk

El reenvío de registros se configura en forma de autoservicio declarando una configuración en Git e implementándola a través de la canalización de configuración de Cloud Manager para los tipos de entorno de desarrollo, fase y producción en programas de producción (que no sean de zona protegida).

Tenga en cuenta que el ancho de banda de red asociado con los registros enviados al destino de registro se consideran parte del uso de E/S de red de su organización.


## Organización de este artículo {#how-organized}

Este artículo está organizado de la siguiente manera:

* Configuración: común para todos los destinos de registro
* Registro de configuraciones de destino: cada destino tiene un formato ligeramente diferente
* AEM Redes avanzadas: envío de registros de Apache/Dispatcher y de los recursos de red a través de una salida dedicada o a través de una VPN


## Configuración {#setup}

1. Cree la siguiente estructura de carpetas y archivos en la carpeta de nivel superior del proyecto en Git:

   ```
   config/
        logForwarding.yaml
   ```

1. logForwarding.yaml debe contener metadatos y una configuración similar al siguiente formato (utilizamos Splunk como ejemplo).

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

   Se debe incluir el nodo predeterminado por motivos de compatibilidad futuros.

   El parámetro kind debe establecerse en LogForwarding . La versión debe establecerse en la versión de esquema, que es 1.

   Tokens en la configuración (como `${{SPLUNK_TOKEN}}`) representan secretos que no deberían almacenarse en Git. En su lugar, declárelos como Cloud Manager  [Variables de entorno](/help/implementing/cloud-manager/environment-variables.md) del tipo &quot;secreto&quot;. Asegúrese de seleccionar **Todo** como el valor desplegable del campo Servicio aplicado, de modo que los registros se pueden reenviar a los niveles de creación, publicación y vista previa.

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

Consideraciones:

* Autentique utilizando el token SAS, que debe tener un período de validez mínimo.
* El token SAS debe crearse en la página de la cuenta, no en la página contenedora.

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

## Redes avanzadas {#advanced-networking}

Si tiene requisitos de organización para bloquear el tráfico en el destino de registro, puede configurar el reenvío de registros para que se transmita [redes avanzadas](/help/security/configuring-advanced-networking.md). Consulte los patrones para los tres tipos de red avanzados siguientes, que utilizan un `port` junto con el parámetro `host` parámetro.

### Salida de puerto flexible {#flex-port}

Si el tráfico de registro va a un puerto distinto del 443 (por ejemplo, 8443 a continuación), configure la red avanzada de la siguiente manera:

```
{
    "portForwards": [
        {
            "name": "mylogging.service.logger.com",
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
      host: "proxy.tunnel"
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
            "name": "mylogging.service.com",
            "portDest": 443, # something other than 443
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
      host: "proxy.tunnel"
      token: "${{SomeToken}}"
      port: 30443
      index: "index_name"
```

### VPN {#vpn}

Si el tráfico de registro necesita pasar por una VPN, configure una red avanzada como la siguiente:

```
{
    "portForwards": [
        {
            "name": "mylogging.service.com",
            "portDest": 443, # something other than 443
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
      host: "mylogging.service.com"
      token: "${{SomeToken}}"
      port: 30443
      index: "index_name"
```
