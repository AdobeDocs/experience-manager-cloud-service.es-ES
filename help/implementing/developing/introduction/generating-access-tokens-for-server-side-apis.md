---
title: Generación de tokens de acceso para las API del servidor
description: Aprenda a facilitar la comunicación entre un servidor de terceros y AEM como Cloud Service mediante la generación de un token JWT seguro
exl-id: 20deaf8f-328e-4cbf-ac68-0a6dd4ebf0c9
source-git-commit: 89b43e14f35e18393ffab538483121c10f6b5a01
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 0%

---

# Introducción {#introduction}

Algunas arquitecturas dependen de realizar llamadas a AEM como Cloud Service desde una aplicación alojada en un servidor fuera de AEM infraestructura. Por ejemplo, una aplicación móvil que llama a un servidor y luego realiza solicitudes de API para AEM como Cloud Service.

El flujo de servidor a servidor se describe a continuación, junto con un flujo simplificado para el desarrollo. El AEM como Cloud Service [Developer Console](development-guidelines.md#crxde-lite-and-developer-console) se utiliza para generar los tokens necesarios para el proceso de autenticación.

>[!NOTE]
>
>Además de esta documentación, también puede consultar el tutorial sobre [Autenticación basada en token para AEM como Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication).

## Flujo de servidor a servidor {#the-server-to-server-flow}

Un usuario con una función de administrador de organización de IMS y que también sea miembro del perfil de producto de AEM Usuarios o AEM Administradores en AEM Author, puede generar una AEM como credencial de Cloud Service. Ese credencial puede ser recuperado posteriormente por un usuario con la función de administrador de entorno de AEM como Cloud Service y debe instalarse en el servidor y debe tratarse cuidadosamente como clave secreta. Este archivo de formato JSON contiene todos los datos necesarios para la integración con una API de Cloud Service de AEM. Los datos se utilizan para crear un token de JWT firmado, que se intercambia con IMS por un token de acceso de IMS. Este token de acceso se puede utilizar como token de autenticación del portador para realizar solicitudes para AEM como Cloud Service.

El flujo de servidor a servidor implica los siguientes pasos:

* Recuperación de las credenciales de AEM como Cloud Service desde Developer Console
* Instale el AEM como credenciales de Cloud Service en un servidor que no sea AEM que realice llamadas a AEM
* Genere un token JWT e intercambie ese token por un token de acceso mediante las API IMS de Adobe
* Llamar a la API de AEM con el token de acceso como token de autenticación de portador
* Establezca los permisos adecuados para el usuario de cuenta técnica en el entorno de AEM

### Recuperación de las credenciales de AEM como Cloud Service {#fetch-the-aem-as-a-cloud-service-credentials}

Los usuarios con acceso a la consola de desarrollador de AEM as a Cloud Service podrán ver la pestaña integraciones en Developer Console de un entorno determinado, así como dos botones. Un usuario con la función AEM como administrador de entorno de Cloud Service puede hacer clic en el botón **Get Service Credentials** para mostrar las credenciales de servicio json, que contendrán toda la información necesaria para el servidor que no sea AEM, incluido el ID de cliente, el secreto del cliente, la clave privada, el certificado y la configuración para los niveles de creación y publicación del entorno, independientemente de la selección del pod.

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
>Un administrador de organización de IMS (normalmente el mismo usuario que aprovisionó el entorno a través de Cloud Manager), que también debe ser miembro del perfil de producto de AEM usuarios de AEM o administradores en AEM Author, primero debe acceder a Developer Console y hacer clic en el botón **Obtener credenciales de servicio** para que un usuario con permisos de administrador pueda generar las credenciales y luego recuperarlas en el AEM como entorno de Cloud Service. Si el administrador de organización de IMS no lo ha hecho, un mensaje les informará de que necesitan la función de administrador de organización de IMS.

### Instalación de las credenciales del servicio de AEM en un servidor que no sea AEM {#install-the-aem-service-credentials-on-a-non-aem-server}

La aplicación no AEM que realiza llamadas a AEM debe poder acceder a la AEM como credenciales de Cloud Service, tratándola como un secreto.

### Generar un token de JWT e intercambiarlo por un token de acceso{#generate-a-jwt-token-and-exchange-it-for-an-access-token}

Utilice las credenciales para crear un token JWT en una llamada al servicio IMS de Adobe para recuperar un token de acceso, válido durante 24 horas.

Las credenciales del servicio AEM CS se pueden intercambiar por un token de acceso mediante bibliotecas de cliente diseñadas para este fin. Las bibliotecas de cliente están disponibles en el [repositorio público de GitHub](https://github.com/adobe/aemcs-api-client-lib) del Adobe, que contiene información más detallada y actualizada.

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

El mismo intercambio se puede realizar en cualquier idioma capaz de generar un token JWT firmado con el formato correcto y llamar a las API de intercambio de tokens de IMS.

El token de acceso define cuándo caduca, que suele ser de 24 horas. Hay código de muestra en el repositorio de Git para administrar un token de acceso y actualizarlo antes de que caduque.

### Llamar a la API de AEM {#calling-the-aem-api}

Realice las llamadas de API de servidor a servidor adecuadas a un AEM como entorno de Cloud Service, incluido el token de acceso en el encabezado. Por lo tanto, para el encabezado &quot;Autorización&quot;, utilice el valor `"Bearer <access_token>"`. Por ejemplo, utilizando `curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### Establezca los permisos adecuados para el usuario de cuenta técnica en AEM {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

Una vez que el usuario de la cuenta técnica se crea en AEM (esto ocurre después de la primera solicitud con el token de acceso correspondiente), el usuario de la cuenta técnica debe tener el permiso **en la AEM** adecuado.

Tenga en cuenta que, de forma predeterminada, en el servicio Autor de AEM, el usuario de la cuenta técnica se agrega al grupo de usuarios Colaboradores , que proporciona acceso de lectura AEM.

Este usuario de cuenta técnica de AEM puede obtener permisos adicionales mediante los métodos habituales.

## Flujo de desarrollador {#developer-flow}

Es probable que los desarrolladores deseen probar utilizando una instancia de desarrollo de su aplicación que no sea de AEM (ya sea que se ejecute en su portátil o que esté alojada) que realice solicitudes a un AEM de desarrollo como entorno de desarrollo de Cloud Service. Sin embargo, dado que los desarrolladores no tienen necesariamente permisos de rol de administrador de IMS, no podemos suponer que puedan generar el portador de JWT descrito en el flujo regular de servidor a servidor. Por lo tanto, proporcionamos un mecanismo para que un desarrollador genere un token de acceso directamente que se pueda utilizar en solicitudes para AEM como entornos de Cloud Service a los que tenga acceso.

Consulte la [Documentación de las directrices para desarrolladores](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) para obtener información sobre los permisos necesarios para utilizar el AEM como consola para desarrolladores de Cloud Service.

>[!NOTE]
>
>El token de acceso de desarrollo local es válido durante un máximo de 24 horas tras las cuales debe regenerarse con el mismo método.

Los desarrolladores pueden utilizar este token para realizar llamadas desde su aplicación de prueba AEM a un AEM como entorno de Cloud Service. Normalmente, el desarrollador utilizará este token con la aplicación que no es de AEM en su propio portátil. Además, el AEM as a Cloud suele ser un entorno que no sea de producción.

El flujo del desarrollador incluye los siguientes pasos:

* Generar un token de acceso desde Developer Console
* Llame a la aplicación AEM con el token de acceso.

Los desarrolladores también pueden realizar llamadas API a un proyecto AEM que se ejecuta en su equipo local, en cuyo caso no se necesita un token de acceso.

### Generación del token de acceso {#generating-the-access-token}

Haga clic en el botón **Get Local Development Token** de Developer Console para generar un token de acceso.

### Llame a y luego AEM la aplicación con un token de acceso {#call-the-aem-application-with-an-access-token}

Realice las llamadas de API de servidor a servidor apropiadas desde la aplicación que no es de AEM a un AEM como entorno de Cloud Service, incluido el token de acceso en el encabezado. Por lo tanto, para el encabezado &quot;Autorización&quot;, utilice el valor `"Bearer <access_token>"`.

## Revocación de credenciales de servicio {#service-credentials-revocation}

Si es necesario revocar las credenciales, debe enviar una solicitud al servicio de atención al cliente siguiendo estos pasos:

1. Deshabilite el usuario de cuenta técnica de Adobe Admin Console en la interfaz de usuario:
   * En Cloud Manager, presione **...** situado junto al entorno. Esto abrirá la página de perfiles de producto
   * Ahora, haga clic en el perfil **AEM Users** para mostrar una lista de los usuarios
   * Haga clic en la pestaña **API Credentials** y, a continuación, busque el usuario de cuenta técnica adecuado y elimínelo
2. Póngase en contacto con el servicio de asistencia al cliente y solicite que se eliminen las credenciales de servicio de ese entorno específico
3. Por último, puede volver a generar las credenciales, tal como se describe en esta documentación. Asegúrese también de que el nuevo usuario de cuenta técnica que se ha creado tenga los permisos adecuados.
