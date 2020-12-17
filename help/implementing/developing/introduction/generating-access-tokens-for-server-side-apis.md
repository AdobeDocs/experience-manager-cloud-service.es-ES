---
title: Generación de Tokenes de acceso para las API del servidor
description: Obtenga información sobre cómo facilitar la comunicación entre un servidor de terceros y AEM como Cloud Service mediante la generación de un autentificador JWT seguro
translation-type: tm+mt
source-git-commit: 9a4cb6d981fdf5eea4d1b9c7ae9e3c99947d9745
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 0%

---


# Introducción {#introduction}

>[!IMPORTANT]
>
>Esta función aún no está disponible. Consulte las [Notas de la versión](/help/release-notes/release-notes-cloud/release-notes-current.md) para obtener una lista actualizada de las funciones.

Algunas arquitecturas se basan en realizar llamadas a AEM como Cloud Service desde una aplicación alojada en un servidor fuera de AEM infraestructura. Por ejemplo, una aplicación móvil que llama a un servidor y luego realiza solicitudes de API para AEM como Cloud Service.

El flujo de servidor a servidor se describe a continuación, junto con un flujo simplificado para el desarrollo. El AEM como Cloud Service [Developer Console](development-guidelines.md#crxde-lite-and-developer-console) se utiliza para generar los tokens necesarios para el proceso de autenticación.

## Flujo de servidor a servidor {#the-server-to-server-flow}

Un usuario con la función de administrador puede generar un token portador JWT, que debe instalarse en el servidor y tratarse cuidadosamente como clave secreta. El distintivo portador JWT debe intercambiarse con IMS por un token de acceso, que debe incluirse en la solicitud de AEM como Cloud Service.

El flujo de servidor a servidor incluye los siguientes pasos:

* Genere el token portador de JWT desde la consola del desarrollador
* Instale el token en un servidor que no sea AEM y realice llamadas a AEM
* Intercambiar el token del portador de JWT por un token de acceso mediante las API de IMS de Adobe
* Llamar a la API de AEM

### Generación del token del portador de JWT {#generating-the-jwt-bearer-token}

Los usuarios que tengan la función de administrador de una organización verán la ficha integraciones en la consola de desarrollo de un entorno determinado, así como dos botones. Al hacer clic en el botón **Obtener credenciales de servicio** se generarán la clave privada, el certificado y la configuración.

![Generación JWT](assets/JWTtoken3.png)

El resultado será similar al siguiente:

```
{
  "ok": true,
  "integration": {
    "imsEndpoint": "ims-na1.adobelogin.com",
    "metascopes": "ent_aem_cloud_sdk,ent_cloudmgr_sdk",
    "technicalAccount": {
      "clientId": "cm-p123-e1234",
      "clientSecret": "4AREDACTED17"
    },
    "email": "abcd@techacct.adobe.com",
    "id": "ABCDAE10A495E8C@techacct.adobe.com",
    "org": "1234@AdobeOrg",
    "privateKey": "-----BEGIN RSA PRIVATE KEY-----\r\REDACTED\r\n==\r\n-----END RSA PRIVATE KEY-----\r\n",
    "publicKey": "-----BEGIN CERTIFICATE-----\r\nREDACTED\r\n-----END CERTIFICATE-----\r\n"
  },
  "statusCode": 200
}
```

### Instalar el token en un servidor no AEM {#install-the-token-on-a-non-aem-server}

La aplicación no AEM que realiza llamadas a AEM debe instalar el distintivo portador JWT, tratándolo como un secreto.

### Intercambiar el token de JWT por un Token de acceso {#exchange-the-jwt-token-for-an-access-token}

Incluya el token de JWT en una llamada al servicio IMS del Adobe para recuperar un token de acceso, válido durante 24 horas.

### Llamar a la API de AEM {#calling-the-aem-api}

Realice las llamadas de API de servidor a servidor correspondientes a un AEM como entorno de Cloud Service, incluido el token de acceso en el encabezado. Por lo tanto, para el encabezado &quot;Autorización&quot;, utilice el valor `"Bearer <access_token>"`.

<!-- ### Code Samples {#code-samples}

https://git.corp.adobe.com/boston/skyline-api-client-lib (internal note: URL will change to public git repo before we publish) contains client libraries written in node.js that will exchange the JSON outputted by the developer console for an access token. -->

## Flujo de desarrollador {#developer-flow}

Es probable que los desarrolladores deseen realizar pruebas con una instancia de desarrollo de su aplicación no AEM (ya sea ejecutándose en su ordenador portátil o alojada) que realiza solicitudes a un AEM de desarrollo como entorno de desarrollo Cloud Service. Sin embargo, dado que los desarrolladores no necesariamente tienen acceso de rol de administrador al AEM como entorno de desarrollo de Cloud Service, no podemos asumir que pueden generar el portador de JWT descrito en el flujo regular de servidor a servidor. Por lo tanto, proporcionamos un mecanismo para que un desarrollador genere un token de acceso directamente que pueda utilizarse en solicitudes para AEM como entornos Cloud Service a los que tienen acceso. Consulte la [documentación de las directrices para desarrolladores](/help/implementing/developing/introduction/development-guidelines.md) para obtener información sobre los permisos necesarios para utilizar la AEM como una consola para desarrolladores de Cloud Service.

>[!NOTE]
>
>El token es válido durante 24 horas, tras lo cual debe regenerarse con el mismo método.

Los desarrolladores pueden utilizar este token para realizar llamadas desde su aplicación de prueba no AEM a un AEM como entorno de Cloud Service. Normalmente, el desarrollador utilizará este token con la aplicación sin AEM en su propio portátil. Además, el AEM como nube suele ser un entorno sin producción.

El flujo del desarrollador incluye los siguientes pasos:

* Generar un token de acceso desde la Consola de programadores
* Llame a la aplicación AEM con el token de acceso.

Los desarrolladores también pueden realizar llamadas de API a un proyecto AEM que se ejecuta en su equipo local, en cuyo caso no se necesita un token de acceso.

### Generación del Token de acceso {#generating-the-access-token}

Haga clic en el botón **Obtener token de desarrollo local** en la Consola de programadores para generar un token de acceso.

### Llamar a AEM Aplicación con un Token de acceso {#call-the-aem-application-with-an-access-token}

Realice las llamadas de API de servidor a servidor correspondientes desde la aplicación que no es de AEM a una AEM como entorno de Cloud Service, incluido el token de acceso en el encabezado. Por lo tanto, para el encabezado &quot;Autorización&quot;, utilice el valor `"Bearer <access_token>"`.

## Revocación de token del portador JWT {#jwt-bearer-token-revocation}

Envíe una solicitud a la asistencia al cliente si es necesario revocar el token del portador de JWT.