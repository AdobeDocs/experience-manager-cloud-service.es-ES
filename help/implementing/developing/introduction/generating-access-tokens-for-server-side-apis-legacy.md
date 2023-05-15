---
title: Generación de tokens de acceso para API del lado del servidor (heredadas)
description: Aprenda a facilitar la comunicación entre un servidor de terceros y AEM as a Cloud Service mediante la generación de un token JWT seguro
hidefromtoc: true
exl-id: 6561870c-cbfe-40ef-9efc-ea75c88c4ed7
source-git-commit: 98eff568686c72c626d2bf77d82e8c3f224eda42
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 0%

---

# Generación de tokens de acceso para API del lado del servidor (heredadas) {#generating-access-tokens-for-server-side-apis-legacy}

Algunas arquitecturas dependen de realizar llamadas a AEM as a Cloud Service desde una aplicación alojada en un servidor fuera de AEM infraestructura. Por ejemplo, una aplicación móvil que llama a un servidor y que luego realiza solicitudes de API para AEM as a Cloud Service.

El flujo de servidor a servidor se describe a continuación, junto con un flujo simplificado para el desarrollo. El AEM as a Cloud Service [Developer Console](development-guidelines.md#crxde-lite-and-developer-console) se utiliza para generar los tokens necesarios para el proceso de autenticación.

<!-- ERROR: Not Found (HTTP error 404)
>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## Flujo de servidor a servidor {#the-server-to-server-flow}

Un usuario con una función de administrador de organización de IMS y que también sea miembro del perfil de producto de AEM usuarios AEM o administradores en AEM Author, puede generar una credencial as a Cloud Service AEM. Ese credencial puede ser recuperado posteriormente por un usuario con la función de administrador de entorno as a Cloud Service de AEM y debe instalarse en el servidor y debe tratarse cuidadosamente como clave secreta. Este archivo de formato JSON contiene todos los datos necesarios para la integración con una API as a Cloud Service AEM. Los datos se utilizan para crear un token de JWT firmado, que se intercambia con IMS por un token de acceso de IMS. Este token de acceso se puede utilizar como token de autenticación del portador para realizar solicitudes AEM as a Cloud Service. Las credenciales caducan después de un año de forma predeterminada, pero se pueden actualizar cuando sea necesario, tal como se describe [here](#refresh-credentials).

El flujo de servidor a servidor implica los siguientes pasos:

* Recupere las credenciales de AEM as a Cloud Service desde Developer Console
* Instale las credenciales para AEM as a Cloud Service en un servidor no AEM que realice llamadas a AEM
* Genere un token JWT e intercambie ese token por un token de acceso mediante las API IMS de Adobe
* Llamar a la API de AEM con el token de acceso como token de autenticación de portador
* Establezca los permisos adecuados para el usuario de cuenta técnica en el entorno de AEM

### Recuperación de las credenciales as a Cloud Service AEM {#fetch-the-aem-as-a-cloud-service-credentials}

Los usuarios con acceso a la consola de desarrollador as a Cloud Service AEM ven la pestaña integraciones en Developer Console de un entorno determinado y dos botones. Un usuario con la función de administrador de entorno as a Cloud Service de AEM puede hacer clic en el botón **Generar credenciales de servicio** para generar y mostrar las credenciales del servicio json. El json contiene toda la información necesaria para el servidor que no es de AEM, incluido el ID del cliente, el secreto del cliente, la clave privada, el certificado y la configuración para los niveles de creación y publicación del entorno, independientemente de la selección del pod.

![Generación JWT](assets/JWTtoken3.png)

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

Una vez generadas, las credenciales se pueden recuperar más adelante pulsando la tecla **Obtener credenciales de servicio** en la misma ubicación.

>[!IMPORTANT]
>
>Un administrador de organización de IMS (normalmente el usuario que aprovisionó el entorno mediante Cloud Manager) que también debe ser miembro del perfil de producto de los usuarios AEM o AEM administradores en AEM Author, accede a Developer Console. A continuación, deben hacer clic en el botón **Generar credenciales de servicio** para que las credenciales las genere y luego las recupere un usuario con permisos de administrador en el entorno as a Cloud Service AEM. Si el administrador de organización de IMS no ha realizado esta tarea, un mensaje les informa de que necesitan la función de administrador de organización de IMS.

### Instalación de las credenciales del servicio de AEM en un servidor que no sea AEM {#install-the-aem-service-credentials-on-a-non-aem-server}

La aplicación no AEM que realiza llamadas a AEM debe poder acceder a las credenciales de AEM as a Cloud Service, tratándolas como un secreto.

### Generar un token de JWT e intercambiarlo por un token de acceso {#generate-a-jwt-token-and-exchange-it-for-an-access-token}

Utilice las credenciales para crear un token JWT en una llamada al servicio IMS de Adobe para recuperar un token de acceso, válido durante 24 horas.

Las credenciales del servicio AEM CS se pueden intercambiar por un token de acceso mediante bibliotecas de cliente diseñadas para este fin. Las bibliotecas de cliente están disponibles en [Repositorio público de GitHub de Adobe](https://github.com/adobe/aemcs-api-client-lib), que contiene directrices más detalladas e información más reciente.

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

Realice las llamadas de API de servidor a servidor adecuadas a un entorno as a Cloud Service AEM, incluido el token de acceso en el encabezado. Por lo tanto, para el encabezado &quot;Autorización&quot;, utilice el valor `"Bearer <access_token>"`. Por ejemplo, al usar `curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### Establezca los permisos adecuados para el usuario de cuenta técnica en AEM {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

Una vez que el usuario de la cuenta técnica se ha creado en AEM (se produce después de la primera solicitud con el token de acceso correspondiente), se debe autorizar correctamente al usuario de la cuenta técnica **en** AEM.

De forma predeterminada, en el servicio Autor de AEM, el usuario de la cuenta técnica se agrega al grupo de usuarios Colaboradores , que proporciona acceso de lectura AEM.

Este usuario de cuenta técnica de AEM puede ser aprovisionado con permisos adicionales mediante los métodos habituales.

## Flujo de desarrollador {#developer-flow}

Los desarrolladores deben probar utilizando una instancia de desarrollo de su aplicación que no sea de AEM (ya sea que se ejecute en su portátil o que esté alojada) que realice solicitudes a un entorno de desarrollo AEM desarrollo as a Cloud Service. Sin embargo, como los desarrolladores no tienen necesariamente permisos de rol de administrador de IMS, Adobe no puede suponer que puedan generar el portador de JWT descrito en el flujo regular de servidor a servidor. Por lo tanto, Adobe proporciona un mecanismo para que un desarrollador genere un token de acceso directamente que se pueda utilizar en solicitudes a un entorno as a Cloud Service AEM al que tenga acceso.

Consulte la [Documentación de las directrices para desarrolladores](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) para obtener información sobre los permisos necesarios para utilizar la consola de desarrollador as a Cloud Service de AEM.

>[!NOTE]
El token de acceso de desarrollo local es válido durante un máximo de 24 horas tras las cuales debe regenerarse con el mismo método.

Los desarrolladores pueden utilizar este token para realizar llamadas desde su aplicación de prueba AEM a un entorno as a Cloud Service AEM. Normalmente, el desarrollador utiliza este token con la aplicación que no es de AEM en su propio portátil. Además, el AEM as a Cloud suele ser un entorno que no sea de producción.

El flujo del desarrollador incluye los siguientes pasos:

* Generar un token de acceso desde Developer Console
* Llame a la aplicación AEM con el token de acceso.

Los desarrolladores también pueden realizar llamadas API a un proyecto AEM que se ejecuta en su equipo local, en cuyo caso no se necesita un token de acceso.

### Generación del token de acceso {#generating-the-access-token}

Para generar un token de acceso, en Developer Console, haga clic en **Obtener token de desarrollo local**.

### Llame a y luego AEM la aplicación con un token de acceso {#call-the-aem-application-with-an-access-token}

Realice las llamadas de API de servidor a servidor adecuadas desde la aplicación que no es de AEM a un entorno as a Cloud Service AEM, incluido el token de acceso en el encabezado. Por lo tanto, para el encabezado &quot;Autorización&quot;, utilice el valor `"Bearer <access_token>"`.

## Actualizar credenciales {#refresh-credentials}

De forma predeterminada, las credenciales de AEM as a Cloud Service caducan después de un año. Para garantizar la continuidad del servicio, los desarrolladores tienen la opción de actualizar las credenciales, ampliando su disponibilidad durante un año adicional. Uso **Actualizar credenciales del servicio** de la variable **Integraciones** en Developer Console, como se muestra a continuación.

![Actualización de la credencial](assets/credential-refresh.png)

Después de pulsar el botón , se generará un nuevo conjunto de credenciales. Puede actualizar el almacenamiento secreto con las nuevas credenciales y validar que funcionan como deberían.

>[!NOTE]
Después de hacer clic en el botón **Actualizar credenciales del servicio** , las credenciales antiguas permanecen registradas hasta que caducan, pero solo el conjunto más reciente está disponible para su visualización desde Developer Console en cualquier momento.

## Revocación de credenciales de servicio {#service-credentials-revocation}

Si las credenciales deben revocarse, debe enviar una solicitud al servicio de atención al cliente siguiendo estos pasos:

1. Deshabilite el usuario de cuenta técnica de Adobe Admin Console en la interfaz de usuario:
   * En Cloud Manager, presione la tecla **...** situado junto al entorno. Esta acción abre la página de perfiles de producto
   * A continuación, haga clic en el **AEM usuarios** para mostrar una lista de los usuarios
   * Haga clic en el **Credenciales de API** , busque el usuario de cuenta técnica apropiado y elimínelo
2. Póngase en contacto con el servicio de asistencia al cliente y solicite que se eliminen las credenciales de servicio de ese entorno específico
3. Por último, puede volver a generar las credenciales, tal como se describe en esta documentación. Asegúrese también de que el nuevo usuario de cuenta técnica que se ha creado tenga los permisos adecuados.
