---
title: Depuración de la caché de la CDN
description: Obtenga información sobre cómo quitar objetos en caché de la caché de la CDN de Adobe configurando el token de API de depuración que se puede utilizar en llamadas a la API.
feature: CDN Cache
exl-id: 4d091677-b817-4aeb-b131-7a5407ace3e0
role: Admin
source-git-commit: 3b55f3094b7154b7723ef7ae2230d7ae01eb4abc
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 1%

---

# Depuración de la caché de la CDN {#cdn-purge-cache}

La depuración elimina un objeto de la caché de la CDN de Adobe, lo que da como resultado que las solicitudes futuras sigan al origen como una falta de caché, en lugar de servirse desde la caché.
AEM as a Cloud Service le permite configurar un token de API de depuración, que luego se puede utilizar en las llamadas de API de depuración. Lea el artículo [Configuración de credenciales y autenticación de CDN](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token) para saber cómo configurar este token mediante las directivas de autenticación de canalización de configuración de Cloud Manager.

Existen tres variaciones de depuración admitidas:

* [Purga de dirección URL única](#single-purge): purgue un solo recurso a la vez.
* [Purgar mediante clave suplente](#surrogate-key-purge): purgue varios recursos a la vez.
* [Purga completa](#full-purge) - purgar todos los recursos.

Todas las variaciones de depuración comparten lo siguiente:

* El método HTTP debe establecerse en `PURGE`.
* AEM La dirección URL puede ser cualquier dominio asociado con el servicio al que está destinada la solicitud de purga de la dirección URL.
* `X-AEM-Purge-Key` debe proporcionarse en un encabezado HTTP.

>[!CAUTION]
>La depuración de la caché de la CDN, especialmente con el indicador estricto, aumentará el tráfico en el origen y podría provocar una interrupción cuando no se ejecute correctamente.

## Purga de URL única {#single-purge}

Puede depurar un único recurso a la vez de la siguiente manera:

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com/resource-path" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H 'X-AEM-Purge: soft'
```

Como se muestra en el ejemplo anterior, puede **opcionalmente** especificar si la red de distribución de contenido (CDN) debe realizar una depuración de **hard** (predeterminada) o de **soft** en los objetos en caché.

La depuración predeterminada impide que las nuevas solicitudes puedan acceder inmediatamente al contenido hasta que este se recupere del origen. La depuración suave marca el contenido como obsoleto, pero lo sirve a los clientes para que no tengan que esperar hasta que se recupere el contenido del origen.

## Depuración de clave suplente {#surrogate-key-purge}

Las claves de sustitución son identificadores únicos que se utilizan para depurar un conjunto de contenido. Se aplican al contenido agregando un encabezado `Surrogate-Key` a la respuesta. Se puede hacer referencia a una o varias claves sustitutas en una llamada de API de depuración.

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H "Surrogate-Key: my-surrogate-key"
-H "X-AEM-Purge: soft" #optional
```

Los `Surrogate-Key` están separados por espacios. De forma similar a la depuración de URL única, puede configurar una depuración grave o suave.

## Depuración completa {#full-purge}

Puede realizar una depuración completa de todos los recursos en caché de la siguiente manera:

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H "X-AEM-Purge: all"
```

Tenga en cuenta que el encabezado `X-AEM-Purge` debe incluir el valor &quot;todo&quot;.

## Interacciones con la capa de Apache/Dispatcher {#apache-layer}

Como se describe en el [artículo Flujo de distribución de contenido](/help/implementing/dispatcher/overview.md), la CDN recupera contenido de la capa Apache/Dispatcher si la caché ha caducado. Esto implica que antes de purgar un recurso en la CDN, debe asegurarse de que también hay una versión nueva del contenido disponible en Dispatcher. Para obtener más información, consulte [Invalidación de caché de Dispatcher](/help/implementing/dispatcher/caching.md#disp).
