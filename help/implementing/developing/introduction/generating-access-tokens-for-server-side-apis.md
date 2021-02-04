---
title: Generación de Tokenes de acceso para las API del servidor
description: Obtenga información sobre cómo facilitar la comunicación entre un servidor de terceros y AEM como Cloud Service mediante la generación de un autentificador JWT seguro
translation-type: tm+mt
source-git-commit: e4c7fcc1576a401629461117be4dba404a3c37c8
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 0%

---


# Introducción {#introduction}

Algunas arquitecturas se basan en realizar llamadas a AEM como Cloud Service desde una aplicación alojada en un servidor fuera de AEM infraestructura. Por ejemplo, una aplicación móvil que llama a un servidor y luego realiza solicitudes de API para AEM como Cloud Service.

El flujo de servidor a servidor se describe a continuación, junto con un flujo simplificado para el desarrollo. El AEM como Cloud Service [Developer Console](development-guidelines.md#crxde-lite-and-developer-console) se utiliza para generar los tokens necesarios para el proceso de autenticación.

>[!NOTE]
>
>Además de esta documentación, también puede consultar el tutorial sobre [autenticación basada en token para AEM como Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication).

## Flujo de servidor a servidor {#the-server-to-server-flow}

Un usuario con una función de administrador de organización de IMS puede generar una AEM como una credencial de Cloud Service, que posteriormente puede recuperar un usuario con la AEM como administrador de Entorno de Cloud Service y debe instalarse en el servidor y debe tratarse cuidadosamente como clave secreta. Este archivo de formato JSON contiene todos los datos necesarios para la integración con un AEM como API de Cloud Service. Los datos se utilizan para crear un token de JWT firmado, que se intercambia con IMS para un token de acceso de IMS. Este token de acceso se puede usar como token de autenticación de portador para realizar solicitudes a AEM como Cloud Service.

El flujo de servidor a servidor incluye los siguientes pasos:

* Recuperar las credenciales del AEM como Cloud Service desde la Consola de programadores
* Instale el AEM como credenciales de Cloud Service en un servidor que no sea AEM que realice llamadas a AEM
* Genere un token de JWT e intercambie ese token por un token de acceso mediante las API de IMS de Adobe
* Llamar a la API de AEM con el token de acceso como testigo de autenticación de portador
* Configure los permisos adecuados para el usuario de la cuenta técnica en el entorno de AEM

### Buscar la AEM como credenciales de Cloud Service {#fetch-the-aem-as-a-cloud-service-credentials}

Los usuarios con acceso a la AEM como consola de desarrollador de Cloud Service verán la ficha integraciones en la Consola de desarrollador de un entorno determinado, así como dos botones. Un usuario con la AEM como administrador de Entorno de Cloud Service puede hacer clic en el botón **Obtener credenciales de servicio** para mostrar el archivo json de credenciales de servicio, que contendrá toda la información necesaria para el servidor que no sea AEM, incluidos el ID de cliente, el secreto de cliente, la clave privada, el certificado y la configuración para los niveles de creación y publicación del entorno, independientemente de la selección de pod.

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

>[!IMPORTANT]
>
>Un administrador de organización de IMS (normalmente el mismo usuario que aprovisionó el entorno mediante Cloud Manager) debe acceder primero a la consola de desarrollador y hacer clic en el botón **Obtener credenciales de servicio** para que un usuario con permisos de administrador pueda generar las credenciales y luego recuperarlas como entorno de Cloud Service. Si el administrador de organización de IMS no lo ha hecho, un mensaje les informará de que necesitan la función de administrador de organización de IMS.

### Instale las credenciales de servicio AEM en un servidor que no sea AEM {#install-the-aem-service-credentials-on-a-non-aem-server}

La aplicación no AEM que realiza llamadas a AEM debería poder acceder a la AEM como credenciales de Cloud Service, tratándola como un secreto.

### Generar un token de JWT y cambiarlo por un Token de acceso{#generate-a-jwt-token-and-exchange-it-for-an-access-token}

Utilice las credenciales para crear un token de JWT en una llamada al servicio IMS de Adobe para recuperar un token de acceso válido durante 24 horas.

Las credenciales de servicio de CS AEM pueden intercambiarse por un token de acceso mediante bibliotecas de cliente diseñadas para este fin. Las bibliotecas de cliente están disponibles en el repositorio público de GitHub](https://github.com/adobe/aemcs-api-client-lib) del [Adobe, que contiene información más detallada y más reciente.

```
/*jshint node:true */
"use strict";

const fs = require('fs');
const exchange = require("@adobe/aemcs-api-client-lib");

const jsonfile = "aemcs-service-credentials.json";

var config = JSON.parse(fs.readFileSync(jsonfile, 'utf8'));
exchange(config).then(accessToken => {
    // output the access token in json form including when it will expire.
    console.log(JSON.stringify(accessToken,null,2));
}).catch(e => {
    console.log("Failed to exchange for access token ",e);
});
```

El mismo intercambio se puede realizar en cualquier idioma capaz de generar un token de JWT firmado con el formato correcto y llamar a las API de intercambio de tokens de IMS.

El token de acceso definirá cuándo caduca, que suele ser de 12 horas. Hay código de muestra en el repositorio git para administrar un token de acceso y actualizarlo antes de que caduque.

### Llamar a la API de AEM {#calling-the-aem-api}

Realice las llamadas de API de servidor a servidor correspondientes a un AEM como entorno de Cloud Service, incluido el token de acceso en el encabezado. Por lo tanto, para el encabezado &quot;Autorización&quot;, utilice el valor `"Bearer <access_token>"`. Por ejemplo, con `curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### Establezca los permisos adecuados para el usuario de la cuenta técnica en AEM {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

Una vez creado el usuario de la cuenta técnica en AEM (esto ocurre después de la primera solicitud con el token de acceso correspondiente), el usuario de la cuenta técnica debe tener el permiso **en** AEM.

Tenga en cuenta que, de forma predeterminada, en el servicio AEM Author, el usuario de la cuenta técnica se agrega al grupo de usuarios Colaboradores, que proporciona AEM de acceso de lectura.

Este usuario técnico de la cuenta en AEM puede recibir permisos adicionales mediante los métodos habituales.

## Flujo de desarrollador {#developer-flow}

Es probable que los desarrolladores deseen realizar pruebas con una instancia de desarrollo de su aplicación no AEM (ya sea ejecutándose en su ordenador portátil o alojada) que realiza solicitudes a un AEM de desarrollo como entorno de desarrollo Cloud Service. Sin embargo, como los desarrolladores no tienen necesariamente permisos de función de administrador de IMS, no podemos asumir que pueden generar el portador de JWT descrito en el flujo regular de servidor a servidor. Por lo tanto, proporcionamos un mecanismo para que un desarrollador genere un token de acceso directamente que pueda utilizarse en solicitudes para AEM como entornos Cloud Service a los que tienen acceso.

Consulte la [documentación de las directrices para desarrolladores](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) para obtener información sobre los permisos necesarios para utilizar la AEM como una consola para desarrolladores de Cloud Service.

>[!NOTE]
>
>El token de acceso de desarrollo local es válido durante 24 horas, tras lo cual debe regenerarse con el mismo método.

Los desarrolladores pueden utilizar este token para realizar llamadas desde su aplicación de prueba no AEM a un AEM como entorno de Cloud Service. Normalmente, el desarrollador utilizará este token con la aplicación sin AEM en su propio portátil. Además, el AEM como nube suele ser un entorno sin producción.

El flujo del desarrollador incluye los siguientes pasos:

* Generar un token de acceso desde la Consola de programadores
* Llame a la aplicación AEM con el token de acceso.

Los desarrolladores también pueden realizar llamadas de API a un proyecto AEM que se ejecuta en su equipo local, en cuyo caso no se necesita un token de acceso.

### Generación del Token de acceso {#generating-the-access-token}

Haga clic en el botón **Obtener token de desarrollo local** en la Consola de programadores para generar un token de acceso.

### Llamar a AEM Aplicación con un Token de acceso {#call-the-aem-application-with-an-access-token}

Realice las llamadas de API de servidor a servidor correspondientes desde la aplicación que no es de AEM a una AEM como entorno de Cloud Service, incluido el token de acceso en el encabezado. Por lo tanto, para el encabezado &quot;Autorización&quot;, utilice el valor `"Bearer <access_token>"`.

## Revocación de credenciales de servicio {#service-credentials-revocation}

Envíe una solicitud a la asistencia al cliente si es necesario revocar el token del portador de JWT.