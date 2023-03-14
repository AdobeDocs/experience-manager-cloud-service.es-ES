---
title: Generación de tokens de acceso para las API del servidor (heredadas)
description: AEM Obtenga información sobre cómo facilitar la comunicación entre un servidor de terceros y el as a Cloud Service de la mediante la generación de un token JWT seguro
hidefromtoc: true
source-git-commit: 75eb7919c437fe21ceeba934f264c653597aace5
workflow-type: tm+mt
source-wordcount: '1438'
ht-degree: 0%

---

# Generación de tokens de acceso para las API del servidor (heredadas) {#generating-access-tokens-for-server-side-apis-legacy}

AEM Algunas arquitecturas se basan en realizar llamadas a las infraestructuras as a Cloud Service AEM desde una aplicación hospedada en un servidor fuera de la infraestructura de la red de trabajo de la infraestructura de. AEM Por ejemplo, una aplicación móvil que llama a un servidor y que luego hace que las solicitudes de API se vean as a Cloud Service, se.

A continuación se describe el flujo de servidor a servidor, junto con un flujo simplificado para el desarrollo. AEM El as a Cloud Service [Developer Console](development-guidelines.md#crxde-lite-and-developer-console) se utiliza para generar los tokens necesarios para el proceso de autenticación.

>[!NOTE]
>
>Además de esta documentación, también puede consultar los tutoriales sobre [AEM Autenticación basada en tokens para el uso de as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication) y [Obtención de un token de inicio de sesión para integraciones](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html).

## El flujo de servidor a servidor {#the-server-to-server-flow}

AEM AEM AEM Un usuario con un rol de administrador de organización de IMS y que también sea miembro del Perfil de producto de usuarios de la organización de IMS o administradores de la organización de la organización de AEM en AEM Author, puede generar una credencial as a Cloud Service de la organización de. AEM Posteriormente, un usuario con la función de administrador de entorno as a Cloud Service puede recuperar esa credencial, que debe instalarse en el servidor y tratarse cuidadosamente como una clave secreta. AEM Este archivo de formato JSON contiene todos los datos necesarios para integrarse con una API as a Cloud Service de. Los datos se utilizan para crear un token JWT firmado, que se intercambia con IMS por un token de acceso IMS. AEM A continuación, este token de acceso se puede utilizar como token de autenticación del portador para realizar solicitudes a los as a Cloud Service de la. Las credenciales caducan después de un año de forma predeterminada, pero se pueden actualizar cuando sea necesario, tal como se describe a continuación [aquí](#refresh-credentials).

El flujo de servidor a servidor incluye los siguientes pasos:

* AEM Recupere las credenciales as a Cloud Service de la desde Developer Console
* AEM Instalar las credenciales as a Cloud Service AEM AEM de la en un servidor no de la red que realice llamadas a la red de la red de
* Genere un token JWT e intercámbielo por un token de acceso mediante las API de IMS de Adobe
* AEM Llamar a la API de con el token de acceso como token de autenticación del portador
* AEM Establezca los permisos adecuados para el usuario de la cuenta técnica en el entorno de la

### AEM Recuperar las credenciales as a Cloud Service de la {#fetch-the-aem-as-a-cloud-service-credentials}

AEM Los usuarios con acceso a la consola de desarrollador as a Cloud Service de la verán la pestaña integraciones en Developer Console para un entorno determinado, así como dos botones. AEM Un usuario con la función de administrador del entorno as a Cloud Service de la puede hacer clic en **Generar credenciales de servicio** AEM para generar y mostrar el json de credenciales de servicio, que contendrá toda la información necesaria para el servidor que no es de servicio, incluidos el id de cliente, el secreto de cliente, la clave privada, el certificado y la configuración para los niveles de creación y publicación del entorno, independientemente de la selección del pod.

![Generación de JWT](assets/JWTtoken3.png)

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

Una vez generadas, las credenciales se pueden recuperar en una fecha posterior pulsando la tecla **Obtener credenciales del servicio** en la misma ubicación.

>[!IMPORTANT]
>
>AEM AEM Un administrador de organización de IMS (normalmente el mismo usuario que aprovisionó el entorno a través de Cloud Manager), que también debe ser miembro del Perfil de producto de los usuarios de la aplicación o administradores de la aplicación en AEM Author, debe acceder primero a Developer Console y hacer clic en el botón **Generar credenciales de servicio** AEM para que un usuario con permisos de administrador pueda generar y recuperar las credenciales en el entorno as a Cloud Service. Si el administrador de la organización de IMS no lo ha hecho, un mensaje le informará de que necesita la función Administrador de organización de IMS.

### AEM AEM Instalación de las credenciales del servicio de la en un servidor que no sea de {#install-the-aem-service-credentials-on-a-non-aem-server}

AEM AEM AEM La aplicación que no realiza llamadas a la aplicación que no está en la lista de direcciones, debe poder acceder a las credenciales as a Cloud Service de la lista de direcciones de correo electrónico de la lista de direcciones de correo electrónico de la lista de direcciones de correo electrónico tratándolas como un secreto.

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

AEM Una vez que se crea el usuario de la cuenta técnica en la cuenta de usuario de (lo que sucede después de la primera solicitud con el token de acceso correspondiente), se le deben otorgar los permisos adecuados **in** AEM.

AEM Tenga en cuenta que, de forma predeterminada, en el servicio de AEM de creación, el usuario de la cuenta técnica se agrega al grupo de usuarios Colaboradores, que proporciona acceso de lectura a los usuarios de la cuenta de.

AEM Este usuario de la cuenta técnica en la que se está usando puede aprovisionarse de permisos adicionales mediante los métodos habituales.

## Flujo de desarrollador {#developer-flow}

AEM AEM Es probable que los desarrolladores deseen realizar pruebas con una instancia de desarrollo de su aplicación que no sea de desarrollo (ya sea que se ejecute en su portátil o alojada) que realice solicitudes a un entorno de desarrollo as a Cloud Service de desarrollo de un entorno de desarrollo de. Sin embargo, dado que los desarrolladores no tienen necesariamente permisos de función de administrador de IMS, no podemos suponer que pueden generar el portador JWT descrito en el flujo normal de servidor a servidor. AEM Por lo tanto, proporcionamos un mecanismo para que un desarrollador genere un token de acceso directamente que pueda utilizarse en solicitudes a entornos as a Cloud Service a los que tenga acceso.

Consulte la [Documentación de directrices para desarrolladores](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) AEM para obtener información acerca de los permisos necesarios para utilizar la consola de desarrollador de as a Cloud Service.

>[!NOTE]
>
>El token de acceso de desarrollo local es válido durante un máximo de 24 horas tras las cuales debe regenerarse mediante el mismo método.

AEM AEM Los desarrolladores pueden utilizar este token para realizar llamadas desde su aplicación de prueba no-a un entorno as a Cloud Service de la. AEM Normalmente, el desarrollador utilizará este token con la aplicación que no sea de tipo de aplicación en su propio portátil. AEM Además, el entorno de as a Cloud no suele ser de producción.

El flujo para desarrolladores incluye los siguientes pasos:

* Generar un token de acceso desde Developer Console
* AEM Llame a la aplicación de con el token de acceso.

AEM Los desarrolladores también pueden realizar llamadas de API a un proyecto de que se ejecute en su equipo local, en cuyo caso no se necesita un token de acceso.

### Generación del token de acceso {#generating-the-access-token}

Haga clic en **Obtener token de desarrollo local** en Developer Console para generar un token de acceso.

### AEM Llamar a y luego a la aplicación con un token de acceso {#call-the-aem-application-with-an-access-token}

AEM AEM Realice las llamadas de API de servidor a servidor adecuadas desde la aplicación no-a un entorno as a Cloud Service de la aplicación, incluido el token de acceso en el encabezado. Por lo tanto, para el encabezado Autorización, utilice el valor `"Bearer <access_token>"`.

## Actualizar credenciales {#refresh-credentials}

AEM De forma predeterminada, las credenciales as a Cloud Service de la caducan al cabo de un año. Para garantizar la continuidad del servicio, los desarrolladores tienen la opción de actualizar las credenciales y ampliar su disponibilidad durante un año adicional.

Para conseguirlo, puede utilizar el **Actualizar credenciales del servicio** del menú contextual **Integraciones** en Developer Console, como se muestra a continuación.

![Actualización de credenciales](assets/credential-refresh.png)

Después de pulsar el botón, se generará un nuevo conjunto de credenciales. Puede actualizar el almacenamiento secreto con las nuevas credenciales y validar que funcionan como deberían.

>[!NOTE]
>
> Después de hacer clic en **Actualizar credenciales del servicio** , las credenciales antiguas permanecen registradas hasta que caducan, pero solo el conjunto más reciente está disponible para verse desde Developer Console en un momento dado.

## Revocación de credenciales de servicio {#service-credentials-revocation}

Si es necesario revocar las credenciales, debe enviar una solicitud al servicio de atención al cliente siguiendo estos pasos:

1. Deshabilite el usuario de la cuenta técnica de Adobe Admin Console en la interfaz de usuario de:
   * En Cloud Manager, pulse el botón **...** junto a su entorno. Se abrirá la página de perfiles de producto
   * Ahora, haga clic en **AEM Usuarios de** , para mostrar una lista de los usuarios
   * Haga clic en **Credenciales de API** , busque el usuario de la cuenta técnica correspondiente y elimínelo
2. Póngase en contacto con Atención al cliente y solicite que se eliminen las credenciales de servicio de ese entorno específico
3. Finalmente, puede volver a generar las credenciales, tal como se describe en esta documentación. Asegúrese también de que el nuevo usuario de cuenta técnica que se crea tiene los permisos adecuados.
