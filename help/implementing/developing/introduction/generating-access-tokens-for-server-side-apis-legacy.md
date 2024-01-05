---
title: Generación de tokens de acceso para las API del lado del servidor (heredadas)
description: AEM Obtenga información sobre cómo facilitar la comunicación entre un servidor de terceros y el as a Cloud Service de la mediante la generación de un token JWT seguro
hidefromtoc: true
exl-id: 6561870c-cbfe-40ef-9efc-ea75c88c4ed7
source-git-commit: ecf4c06fd290d250c14386b3135250633b26c910
workflow-type: tm+mt
source-wordcount: '1359'
ht-degree: 0%

---

# Generación de tokens de acceso para las API del lado del servidor (heredadas) {#generating-access-tokens-for-server-side-apis-legacy}

AEM Algunas arquitecturas se basan en realizar llamadas a las infraestructuras as a Cloud Service AEM desde una aplicación hospedada en un servidor fuera de la infraestructura de la red de trabajo de la infraestructura de. AEM Por ejemplo, una aplicación móvil que llama a un servidor y que luego hace que las solicitudes de API se vean as a Cloud Service, se.

A continuación se describe el flujo de servidor a servidor, junto con un flujo simplificado para el desarrollo. AEM El as a Cloud Service [Developer Console](development-guidelines.md#crxde-lite-and-developer-console) se utiliza para generar los tokens necesarios para el proceso de autenticación.

<!-- ERROR: Not Found (HTTP error 404)
>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## El flujo de servidor a servidor {#the-server-to-server-flow}

AEM AEM AEM AEM Un usuario con una función de administrador de organización de IMS y que también sea miembro del Perfil de producto de usuarios de la organización de IMS o administradores de la en Autor de la organización de IMS, puede generar una credencial as a Cloud Service de la organización de IMS (en inglés) que se llame a la función de usuario de la organización de IMS. AEM Esa credencial la puede recuperar posteriormente un usuario con la función de administrador de entorno as a Cloud Service de la y debe instalarse en el servidor y tratarse cuidadosamente como una clave secreta. AEM Este archivo de formato JSON contiene todos los datos necesarios para integrarse con una API as a Cloud Service de. Los datos se utilizan para crear un token JWT firmado, que se intercambia con IMS por un token de acceso IMS. AEM A continuación, este token de acceso se puede utilizar como token de autenticación del portador para realizar solicitudes a los as a Cloud Service de la. Las credenciales caducan después de un año de forma predeterminada, pero se pueden actualizar cuando sea necesario, tal como se describe a continuación [aquí](#refresh-credentials).

El flujo de servidor a servidor incluye los siguientes pasos:

* AEM Recupere las credenciales para las credenciales de los as a Cloud Service desde Developer Console
* AEM Instale las credenciales para la as a Cloud Service AEM AEM en un servidor que no sea de la red y que realice llamadas a la red desde un servidor que no sea de la red de
* Genere un token JWT e intercámbielo por un token de acceso mediante las API de IMS de Adobe
* AEM Llamar a la API de con el token de acceso como token de autenticación del portador
* AEM Establezca los permisos adecuados para el usuario de la cuenta técnica en el entorno de la

### AEM Recuperar las credenciales as a Cloud Service de la {#fetch-the-aem-as-a-cloud-service-credentials}

AEM Los usuarios con acceso a la consola de desarrollador as a Cloud Service de la ven la pestaña integraciones de Developer Console para un entorno determinado y dos botones. AEM Un usuario con la función de administrador del entorno as a Cloud Service de la puede hacer clic en **Generar credenciales de servicio** para generar y mostrar el json de credenciales de servicio. AEM El json contiene toda la información necesaria para el no servidor de publicación, incluido el ID de cliente, el secreto de cliente, la clave privada, el certificado y la configuración para los niveles de creación y publicación del entorno, independientemente de la selección del pod.

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

Después de generarse, las credenciales se pueden recuperar más adelante presionando la tecla **Obtener credenciales del servicio** en la misma ubicación.

>[!IMPORTANT]
>
>AEM AEM AEM Un administrador de organización de IMS, que suele ser el usuario que aprovisionó el entorno mediante Cloud Manager, y que también debe ser miembro del Perfil de producto de los usuarios o administradores de la en Autor de la aplicación, accede a la consola de desarrollador. A continuación, deben hacer clic en **Generar credenciales de servicio** AEM para que las credenciales se generen y posteriormente las recupere un usuario con permisos de administrador en el entorno as a Cloud Service de la. Si el administrador de la organización de IMS no ha realizado esta tarea, un mensaje le informa de que necesita la función Administrador de organización de IMS.

### AEM AEM Instalación de las credenciales del servicio de en un servidor que no sea de tipo {#install-the-aem-service-credentials-on-a-non-aem-server}

AEM AEM AEM La aplicación que no realiza llamadas a la aplicación que no está en la lista de direcciones, debe ser capaz de acceder a las credenciales de la aplicación que no está en la lista de direcciones de correo electrónico de la aplicación que realiza llamadas a la lista de direcciones de correo electrónico y debe poder acceder a las credenciales de la aplicación as a Cloud Service, tratándola como un secreto.

### Generar un token JWT e intercambiarlo por un token de acceso {#generate-a-jwt-token-and-exchange-it-for-an-access-token}

Utilice las credenciales de para crear un token JWT en una llamada al servicio IMS de Adobe para recuperar un token de acceso, que es válido durante 24 horas.

AEM Las credenciales del servicio CS se pueden intercambiar por un token de acceso mediante bibliotecas de cliente diseñadas para este fin. Las bibliotecas de cliente están disponibles en [Repositorio público de GitHub de Adobe](https://github.com/adobe/aemcs-api-client-lib), que contiene directrices más detalladas e información más reciente.

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

El token de acceso define cuándo caduca, que suelen ser 24 horas. Hay un código de ejemplo en el repositorio de Git para administrar un token de acceso y actualizarlo antes de que caduque.

### AEM Llamar a la API de {#calling-the-aem-api}

AEM Realice las llamadas de API de servidor a servidor adecuadas a un entorno as a Cloud Service de la, incluido el token de acceso del encabezado. Por lo tanto, para el encabezado Autorización, utilice el valor `"Bearer <access_token>"`. Por ejemplo, con `curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### AEM Establezca los permisos adecuados para el usuario de la cuenta técnica en el cuadro de {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

AEM Una vez que se crea el usuario de la cuenta técnica en la cuenta de usuario técnica de (se produce después de la primera solicitud con el token de acceso correspondiente), el usuario de la cuenta técnica debe recibir los permisos adecuados **in** AEM.

AEM AEM De forma predeterminada, en el servicio de autor de la, el usuario de la cuenta técnica se agrega al grupo de usuarios Colaboradores, que proporciona acceso de lectura a los recursos de la cuenta de usuario de forma.

AEM Este usuario de la cuenta técnica en la que se está usando puede aprovisionarse de permisos adicionales mediante los métodos habituales.

## Flujo de desarrollador {#developer-flow}

AEM AEM Los desarrolladores deben probar el uso de una instancia de desarrollo de su aplicación que no sea de desarrollo (ya sea que se ejecute en su portátil o alojada) que realice solicitudes a un entorno de desarrollo as a Cloud Service de desarrollo de. Sin embargo, como los desarrolladores no tienen necesariamente permisos de función de administrador de IMS, Adobe no puede suponer que pueden generar el portador JWT descrito en el flujo normal de servidor a servidor. Por lo tanto, el Adobe AEM de proporciona a un desarrollador un mecanismo para generar un token de acceso directamente que se puede utilizar en solicitudes a un entorno as a Cloud Service al que tenga acceso.

Consulte la [Documentación de directrices para desarrolladores](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) AEM para obtener información acerca de los permisos necesarios para utilizar la consola de desarrollador de as a Cloud Service.

>[!NOTE]
>
El token de acceso de desarrollo local es válido durante un máximo de 24 horas tras las cuales debe regenerarse mediante el mismo método.

AEM AEM Los desarrolladores pueden utilizar este token para realizar llamadas desde su aplicación de prueba no-a un entorno as a Cloud Service de la. AEM Normalmente, el desarrollador utiliza este token con la aplicación que no es de la aplicación en su propio portátil, es decir, con la aplicación que no es de la misma aplicación. AEM Además, el entorno de as a Cloud no suele ser de producción.

El flujo para desarrolladores incluye los siguientes pasos:

* Generar un token de acceso desde Developer Console
* AEM Llame a la aplicación de con el token de acceso.

AEM Los desarrolladores también pueden realizar llamadas de API a un proyecto de que se ejecute en su equipo local, en cuyo caso no se necesita un token de acceso.

### Generación del token de acceso {#generating-the-access-token}

Para generar un token de acceso, en Developer Console, haga clic en **Obtener token de desarrollo local**.

### AEM Llamar a y luego a la aplicación con un token de acceso {#call-the-aem-application-with-an-access-token}

AEM AEM Realice las llamadas de API de servidor a servidor adecuadas desde la aplicación no-a un entorno as a Cloud Service de la aplicación, incluido el token de acceso en el encabezado. Por lo tanto, para el encabezado Autorización, utilice el valor `"Bearer <access_token>"`.

## Actualizar credenciales {#refresh-credentials}

AEM De forma predeterminada, las credenciales en las fechas as a Cloud Service caducan después de un año. Para garantizar la continuidad del servicio, los desarrolladores tienen la opción de actualizar las credenciales y ampliar su disponibilidad durante un año adicional. Uso **Actualizar credenciales del servicio** desde el **Integraciones** en Developer Console, como se muestra a continuación.

![Actualización de credenciales](assets/credential-refresh.png)

Después de pulsar el botón, se genera un nuevo conjunto de credenciales. Puede actualizar el almacenamiento secreto con las nuevas credenciales y validar que funcionan como deberían.

>[!NOTE]
>
Después de hacer clic en **Actualizar credenciales del servicio** , las credenciales antiguas permanecen registradas hasta que caducan, pero solo el conjunto más reciente está disponible para verse desde Developer Console en un momento dado.

## Revocación de credenciales de servicio {#service-credentials-revocation}

Si se deben revocar las credenciales, debe enviar una solicitud al servicio de atención al cliente siguiendo estos pasos:

1. Deshabilite el usuario de la cuenta técnica de Adobe Admin Console en la interfaz de usuario de:
   * En Cloud Manager, pulse el botón **...** junto a su entorno. Esta acción abre la página de perfiles de producto
   * A continuación, haga clic en **AEM Usuarios de** , para mostrar una lista de los usuarios
   * Haga clic en **Credenciales de API** , busque el usuario de la cuenta técnica correspondiente y elimínelo
2. Póngase en contacto con Atención al cliente y solicite que se eliminen las credenciales de servicio de ese entorno específico
3. Finalmente, puede volver a generar las credenciales, tal como se describe en esta documentación. Asegúrese también de que el nuevo usuario de cuenta técnica que se crea tiene los permisos adecuados.
