---
title: Generación de tokens de acceso para las API del lado del servidor (heredadas)
description: Obtenga información sobre cómo facilitar la comunicación entre un servidor de terceros y AEM as a Cloud Service mediante la generación de un token JWT seguro
hidefromtoc: true
exl-id: 6561870c-cbfe-40ef-9efc-ea75c88c4ed7
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 22216d2c045b79b7da13f09ecbe1d56a91f604df
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 0%

---

# Generación de tokens de acceso para las API del lado del servidor (heredadas) {#generating-access-tokens-for-server-side-apis-legacy}

Algunas arquitecturas dependen de la realización de llamadas a AEM as a Cloud Service desde una aplicación alojada en un servidor fuera de la infraestructura de AEM. Por ejemplo, una aplicación móvil que llama a un servidor y que luego realiza solicitudes de API a AEM as a Cloud Service.

A continuación se describe el flujo de servidor a servidor, junto con un flujo simplificado para el desarrollo. AEM as a Cloud Service [Developer Console](development-guidelines.md#crxde-lite-and-developer-console) se usa para generar los tokens necesarios para el proceso de autenticación.

<!-- ERROR: Not Found (HTTP error 404)
>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## El flujo de servidor a servidor {#the-server-to-server-flow}

Un usuario con una función de administrador de organización de IMS y que también sea miembro del perfil de producto de los usuarios de AEM o de los administradores de AEM en AEM Author, puede generar una credencial de AEM as a Cloud Service. Esa credencial la puede recuperar posteriormente un usuario con la función de administrador del entorno de AEM as a Cloud Service y debe instalarse en el servidor y tratarse cuidadosamente como una clave secreta. Este archivo de formato JSON contiene todos los datos necesarios para integrarse con una API de AEM as a Cloud Service. Los datos se utilizan para crear un token JWT firmado, que se intercambia con IMS por un token de acceso IMS. Este token de acceso se puede utilizar como token de autenticación del portador para realizar solicitudes a AEM as a Cloud Service. Las credenciales caducan después de un año de forma predeterminada, pero se pueden actualizar cuando sea necesario. Vea [Actualizar credenciales](#refresh-credentials).

El flujo de servidor a servidor incluye los siguientes pasos:

* Recupere las credenciales de AEM as a Cloud Service desde Developer Console
* Instale las credenciales de AEM as a Cloud Service en un servidor que no sea de AEM y realice llamadas a AEM
* Genere un token JWT e intercámbielo por un token de acceso mediante las API de IMS de Adobe
* Llamar a la API de AEM con el token de acceso como token de autenticación del portador
* Establezca los permisos adecuados para el usuario de la cuenta técnica en el entorno de AEM

### Recuperar las credenciales de AEM as a Cloud Service {#fetch-the-aem-as-a-cloud-service-credentials}

Los usuarios con acceso a AEM as a Cloud Service developer console ven la pestaña integraciones de Developer Console para un entorno determinado y dos botones. Un usuario con el rol de administrador de entorno de AEM as a Cloud Service puede hacer clic en el botón **Generar credenciales de servicio** para generar y mostrar el json de credenciales de servicio. El json contiene toda la información necesaria para el servidor que no es de AEM, incluido el ID de cliente, el secreto de cliente, la clave privada, el certificado y la configuración para los niveles de creación y publicación del entorno, independientemente de la selección del pod.

![Generación de JWT](assets/JWTtoken3.png)

El resultado es similar al siguiente:

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

Una vez generadas, las credenciales se pueden recuperar más adelante presionando el botón **Obtener credenciales del servicio** en la misma ubicación.

>[!IMPORTANT]
>
>Un administrador de organización de IMS, que suele ser el usuario que aprovisionó el entorno mediante Cloud Manager, y que también debe ser miembro del Perfil de producto de los usuarios de AEM o de los administradores de AEM en AEM Author, accede a Developer Console. A continuación, debe hacer clic en el botón **Generar credenciales de servicio** para que un usuario con permisos de administrador genere y recupere las credenciales del entorno de AEM as a Cloud Service. Si el administrador de la organización de IMS no ha realizado esta tarea, un mensaje le informa de que necesita la función Administrador de organización de IMS.

### Instalación de las credenciales del servicio de AEM en un servidor que no sea de AEM {#install-the-aem-service-credentials-on-a-non-aem-server}

La aplicación que no sea de AEM que realice llamadas a AEM debe poder acceder a las credenciales de AEM as a Cloud Service y tratarla como un secreto.

### Generar un token JWT e intercambiarlo por un token de acceso {#generate-a-jwt-token-and-exchange-it-for-an-access-token}

Utilice las credenciales para crear un token JWT en una llamada al servicio IMS de Adobe para recuperar un token de acceso, que es válido durante 24 horas.

Las credenciales del servicio AEM CS se pueden intercambiar por un token de acceso utilizando ejemplos de código diseñados para este fin. Hay código de muestra disponible en el [repositorio público de GitHub de Adobe](https://github.com/adobe/aemcs-api-client-lib), que contiene ejemplos de código que puede copiar y adaptar para sus propios proyectos. Tenga en cuenta que este repositorio contiene código de ejemplo para referencia y no se mantiene como dependencia de biblioteca lista para la producción.

```
/*jshint node:true */
"use strict";

const fs = require('fs');
// Sample code adapted from Adobe's GitHub repository
const exchange = require("./your-local-aemcs-client"); // Copy and adapt the code from the GitHub repository

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

El token de acceso define cuándo caduca, que suelen ser 24 horas. Hay un código de ejemplo en el repositorio de Git para administrar un token de acceso y actualizarlo antes de que caduque.

### Llamar a la API de AEM {#calling-the-aem-api}

Realice las llamadas de API de servidor a servidor adecuadas a un entorno de AEM as a Cloud Service, incluido el token de acceso en el encabezado. Por lo tanto, para el encabezado &quot;Autorización&quot;, use el valor `"Bearer <access_token>"`. Por ejemplo, usar `curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### Establezca los permisos adecuados para el usuario de la cuenta técnica en AEM {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

Una vez que el usuario de la cuenta técnica se haya creado en AEM (ocurre después de la primera solicitud con el token de acceso correspondiente), el usuario de la cuenta técnica debe tener los permisos adecuados para **en** AEM.

De forma predeterminada, en el servicio de AEM Author, el usuario de la cuenta técnica se agrega al grupo de usuarios Colaboradores que proporciona acceso de lectura a AEM.

Este usuario de cuenta técnica de AEM puede recibir permisos adicionales mediante los métodos habituales.

## Flujo de desarrollador {#developer-flow}

Los desarrolladores deben probar con una instancia de desarrollo de su aplicación que no sea AEM (que se ejecute en su portátil o alojada) que realice solicitudes a un entorno de desarrollo de AEM as a Cloud Service de desarrollo. Sin embargo, dado que los desarrolladores no tienen necesariamente permisos de función de administrador de IMS, Adobe no puede suponer que pueden generar el portador JWT descrito en el flujo normal de servidor a servidor. Por lo tanto, Adobe proporciona un mecanismo para que un desarrollador genere un token de acceso directamente que se pueda utilizar en solicitudes a un entorno de AEM as a Cloud Service al que tengan acceso.

Consulte la [documentación de las Directrices para desarrolladores](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) para obtener información sobre los permisos necesarios para utilizar AEM as a Cloud Service developer console.

>[!NOTE]
>
>El token de acceso de desarrollo local es válido durante un máximo de 24 horas tras las cuales debe regenerarse mediante el mismo método.

Los desarrolladores pueden utilizar este token para hacer llamadas desde aplicaciones de prueba que no sean de AEM a un entorno de AEM as a Cloud Service. Normalmente, el desarrollador utiliza este token con la aplicación que no es de AEM en su propio portátil. Además, AEM as a Cloud suele ser un entorno que no es de producción.

El flujo para desarrolladores incluye los siguientes pasos:

* Generación de un token de acceso desde Developer Console
* Llame a la aplicación AEM con el token de acceso.

Los desarrolladores también pueden realizar llamadas de API a un proyecto de AEM que se ejecute en su equipo local, en cuyo caso no se necesita un token de acceso.

### Generación del token de acceso {#generating-the-access-token}

Para generar un token de acceso, en Developer Console, haga clic en **Obtener token de desarrollo local**.

### Llamar a y después a la aplicación de AEM con un token de acceso {#call-the-aem-application-with-an-access-token}

Realice las llamadas de API de servidor a servidor adecuadas desde la aplicación que no sea de AEM a un entorno de AEM as a Cloud Service, incluido el token de acceso en el encabezado. Por lo tanto, para el encabezado &quot;Autorización&quot;, use el valor `"Bearer <access_token>"`.

## Actualizar credenciales {#refresh-credentials}

De forma predeterminada, las credenciales de AEM as a Cloud Service caducan al cabo de un año. Para garantizar la continuidad del servicio, los desarrolladores tienen la opción de actualizar las credenciales y ampliar su disponibilidad durante un año adicional. Use **Actualizar credenciales de servicio** de la ficha **Integraciones** de Developer Console, como se muestra a continuación.

![Actualización de credenciales](assets/credential-refresh.png)

Después de pulsar el botón, se genera un nuevo conjunto de credenciales. Puede actualizar el almacenamiento secreto con las nuevas credenciales y validar que funcionan como deberían.

>[!NOTE]
>
> Después de hacer clic en el botón **Actualizar credenciales del servicio**, las credenciales antiguas permanecen registradas hasta que caducan, pero solo el conjunto más reciente está disponible para verse desde Developer Console en cualquier momento.

## Revocación de credenciales de servicio {#service-credentials-revocation}

Si se deben revocar las credenciales, debe enviar una solicitud al servicio de atención al cliente siguiendo estos pasos:

1. Deshabilite el usuario de la cuenta técnica de Adobe Admin Console en la interfaz de usuario de:
   * En Cloud Manager, presione el botón **...** situado junto a su entorno. Esta acción abre la página de perfiles de producto
   * Ahora, haga clic en el perfil **Usuarios de AEM** para mostrar una lista de los usuarios
   * Haga clic en la ficha **Credenciales de API**, busque el usuario de cuenta técnica correspondiente y elimínelo
2. Póngase en contacto con Atención al cliente y solicite que se eliminen las credenciales de servicio de ese entorno específico
3. Finalmente, puede volver a generar las credenciales, tal como se describe en esta documentación. Asegúrese también de que el nuevo usuario de cuenta técnica que se crea tiene los permisos adecuados.
