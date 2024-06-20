---
title: Depuración de la caché de la CDN
description: Obtenga información sobre cómo quitar objetos en caché de la caché de la CDN de Adobe configurando el token de API de depuración que se puede utilizar en llamadas a la API.
feature: CDN Cache
exl-id: 4d091677-b817-4aeb-b131-7a5407ace3e0
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 3%

---

# Depuración de la caché de la CDN {#cdn-purge-cache}

>[!NOTE]
>Esta función aún no está disponible de forma general. Para unirse al programa de adopción anticipada, envíe un correo electrónico a `aemcs-cdn-config-adopter@adobe.com`.

La depuración elimina un objeto de la caché de la CDN de Adobe, lo que da como resultado que las solicitudes futuras sigan al origen como una falta de caché, en lugar de servirse desde la caché.
AEM La opción as a Cloud Service le permite configurar un token de API de purga, que luego se puede utilizar en llamadas a la API. Lea el [Artículo Configuración de credenciales y autenticación de CDN](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token) para aprender a configurar este token mediante las directivas de autenticación de canalización de configuración de Cloud Manager.

Existen tres variaciones de depuración admitidas:

* [Purga de URL única](#single-purge) : depure un solo recurso a la vez.
* [Purgar por clave suplente](#surrogate-key-purge) : depure varios recursos a la vez.
* [Depuración completa](#full-purge) - depurar todos los recursos.

Todas las variaciones de depuración comparten lo siguiente:

* El método HTTP debe configurarse como `PURGE`.
* AEM La dirección URL puede ser cualquier dominio asociado con el servicio al que está destinada la solicitud de purga de la dirección URL.
* El `X-AEM-Purge-Key` debe proporcionarse en un encabezado HTTP.

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

Como se muestra en el ejemplo anterior, puede **opcionalmente** especifique si la CDN debe realizar una **difícil** purge (predeterminado) o un **blando** depurar en los objetos almacenados en caché.

La depuración predeterminada impide que las nuevas solicitudes puedan acceder inmediatamente al contenido hasta que este se recupere del origen. La depuración suave marca el contenido como obsoleto, pero lo sirve a los clientes para que no tengan que esperar hasta que se recupere el contenido del origen.

## Depuración de clave suplente {#surrogate-key-purge}

Las claves de sustitución son identificadores únicos que se utilizan para depurar un conjunto de contenido. Se aplican al contenido añadiendo un `Surrogate-Key` encabezado a la respuesta. Se puede hacer referencia a una o varias claves sustitutas en una llamada de API de depuración.

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H "Surrogate-Key: my-surrogate-key"
-H "X-AEM-Purge: soft" #optional
```

El `Surrogate-Key`(s) están separados por espacios. De forma similar a la depuración de URL única, puede configurar una depuración grave o suave.

## Depuración completa {#full-purge}

Puede realizar una depuración completa de todos los recursos en caché de la siguiente manera:

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H "X-AEM-Purge: all"
```

Tenga en cuenta que la variable `X-AEM-Purge` el encabezado debe incluir el valor &quot;todo&quot;.

## Interacciones con la capa de Apache/Dispatcher {#apache-layer}

Como se describe en la [Artículo del flujo de distribución de contenido](/help/implementing/dispatcher/overview.md), la CDN recupera contenido de la capa de Apache/Dispatcher si la caché ha caducado. Esto implica que antes de purgar un recurso en la CDN, debe asegurarse de que una versión nueva del contenido también esté disponible en Dispatcher. Para obtener más información, consulte [Invalidación de caché de Dispatcher](/help/implementing/dispatcher/caching.md#disp).
