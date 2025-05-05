---
title: 'Consultas persistentes de GraphQL: habilitar el almacenamiento en caché en Dispatcher'
description: Dispatcher es una capa de almacenamiento en caché y seguridad situada frente a los entornos de publicación de Adobe Experience Manager. AEM Puede habilitar el almacenamiento en caché para consultas persistentes en la interfaz de usuario sin encabezado de.
feature: Headless, Dispatcher, GraphQL API
exl-id: 30a97e56-6699-41c4-a4eb-fc6236667f8f
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 12%

---

# Consultas persistentes de GraphQL: habilitar el almacenamiento en caché en Dispatcher {#graphql-persisted-queries-enabling-caching-dispatcher}

>[!CAUTION]
>
>Si el almacenamiento en caché en Dispatcher está habilitado, el [filtro CORS](/help/headless/deployment/cross-origin-resource-sharing.md) no es necesario, y por lo tanto esa sección se puede ignorar.

El almacenamiento en caché de consultas persistentes no está habilitado de forma predeterminada en Dispatcher. La activación predeterminada no es posible, ya que los clientes que utilizan CORS (Intercambio de recursos de origen cruzado) con varios orígenes deben revisar, y posiblemente actualizar, su configuración de Dispatcher.

>[!NOTE]
>
>Dispatcher no almacena en caché el encabezado `Vary`.
>
>El almacenamiento en caché de otros encabezados relacionados con CORS se puede habilitar en Dispatcher, pero puede ser insuficiente cuando hay varios orígenes de CORS.

>[!NOTE]
>
>Para obtener documentación detallada acerca de Dispatcher, consulte la [Guía de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=es).

## Habilitar el almacenamiento en caché de consultas persistentes {#enable-caching-persisted-queries}

Para habilitar el almacenamiento en caché de consultas persistentes, defina la variable de Dispatcher `CACHE_GRAPHQL_PERSISTED_QUERIES`:

1. Agregue la variable al archivo de Dispatcher `global.vars`:

   ```xml
   Define CACHE_GRAPHQL_PERSISTED_QUERIES
   ```

>[!NOTE]
>
>Para lograr el cálculo del encabezado `ETag` individual en las consultas persistentes en caché (para *cada respuesta* que es única), se debe usar la configuración `FileETag Digest` en la configuración del host virtual de la instancia de Dispatcher (si aún no existe):
>
>```xml
><Directory />    
>   ...    
>   FileETag Digest
></Directory> 
>```

>[!NOTE]
>
>Para cumplir con los requisitos de [Dispatcher para los documentos que se pueden almacenar en caché](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/troubleshooting/dispatcher-faq.html?lang=es#how-does-the-dispatcher-return-documents%3F), Dispatcher agrega el sufijo `.json` a todas las direcciones URL de consultas persistentes, de modo que el resultado se pueda almacenar en caché.
>
>Este sufijo se agrega mediante una regla de reescritura, una vez habilitado el almacenamiento en caché de consultas persistentes.

## Configuración de CORS en Dispatcher {#cors-configuration-in-dispatcher}

Es posible que los clientes que utilizan solicitudes CORS tengan que revisar y actualizar su configuración CORS en Dispatcher.

* AEM No se debe pasar el encabezado `Origin` a la publicación de la a través de Dispatcher:
   * Compruebe el archivo `clientheaders.any`.
* En su lugar, las solicitudes CORS deben evaluarse para detectar orígenes permitidos en el nivel de Dispatcher. Este enfoque también garantiza que los encabezados relacionados con CORS se establezcan correctamente, en un solo lugar, en todos los casos.
   * Esta configuración se debe agregar al archivo `vhost`. A continuación se muestra un ejemplo de configuración; para simplificar, solo se ha proporcionado la parte relacionada con CORS. Puede adaptarlo para sus casos de uso específicos.

  ```xml
  <VirtualHost *:80>
     ServerName "publish"
  
     # ...
  
     <IfModule mod_headers.c>
         Header add X-Vhost "publish"
  
          ################## Start of the CORS specific configuration ##################
  
          SetEnvIfExpr "req_novary('Origin') == ''"  CORSType=none CORSProcessing=false
          SetEnvIfExpr "req_novary('Origin') != ''"  CORSType=cors CORSProcessing=true CORSTrusted=false
  
          SetEnvIfExpr "req_novary('Access-Control-Request-Method') == '' && %{REQUEST_METHOD} == 'OPTIONS' && req_novary('Origin') != ''  " CORSType=invalidpreflight CORSProcessing=false
          SetEnvIfExpr "req_novary('Access-Control-Request-Method') != '' && %{REQUEST_METHOD} == 'OPTIONS' && req_novary('Origin') != ''  " CORSType=preflight CORSProcessing=true CORSTrusted=false
          SetEnvIfExpr "req_novary('Origin') -strcmatch 'https://%{HTTP_HOST}*'"  CORSType=samedomain CORSProcessing=false
  
          # For requests that require CORS processing, check if the Origin can be trusted
          SetEnvIfExpr "%{HTTP_HOST} =~ /(.*)/ " ParsedHost=$1
  
          ################## Adapt the regex to match CORS origin for your environment
          SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*.your-domain.tld(:\d+)?$)#" CORSTrusted=true
  
          # Extract the Origin header 
          SetEnvIfNoCase ^Origin$ ^https://(.*)$ CORSTrustedOrigin=https://$1
  
          # Flush If already set
          Header unset Access-Control-Allow-Origin
          Header unset Access-Control-Allow-Credentials
  
          # Trusted
          Header always set Access-Control-Allow-Credentials "true" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Origin "%{CORSTrustedOrigin}e" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Methods "GET" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Max-Age 1800 "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Headers "Origin, Accept, X-Requested-With, Content-Type, Access-Control-Request-Method, Access-Control-Request-Headers" "expr=reqenv('CORSTrusted') == 'true'"
  
          # Non-CORS or Not Trusted
          Header unset Access-Control-Allow-Credentials "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Allow-Origin "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Allow-Methods "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Max-Age "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
  
          # Always vary on origin, even if its not there.
          Header merge Vary Origin
  
          # CORS - send 204 for CORS requests which are not trusted
          RewriteCond expr "reqenv('CORSProcessing') == 'true' && reqenv('CORSTrusted') == 'false'"
          RewriteRule "^(.*)" - [R=204,L]
  
          ################## End of the CORS specific configuration ##################
  
     </IfModule>
  
     <Directory />
  
         # ...
  
     </Directory>
  
     # ...
  
  </VirtualHost>
  ```
