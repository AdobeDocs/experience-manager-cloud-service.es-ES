---
title: Generación de tokens de acceso para las API del lado del servidor
description: Obtenga información sobre cómo facilitar la comunicación entre un servidor de terceros y AEM as a Cloud Service mediante la generación de un token JWT seguro
exl-id: 20deaf8f-328e-4cbf-ac68-0a6dd4ebf0c9
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 22216d2c045b79b7da13f09ecbe1d56a91f604df
workflow-type: tm+mt
source-wordcount: '2112'
ht-degree: 0%

---

# Generación de tokens de acceso para las API del lado del servidor {#generating-access-tokens-for-server-side-apis}

Algunas arquitecturas dependen de la realización de llamadas a AEM as a Cloud Service desde una aplicación alojada en un servidor fuera de la infraestructura de AEM. Por ejemplo, una aplicación móvil que llama a un servidor y que luego realiza solicitudes de API a AEM as a Cloud Service.

A continuación se describe el flujo de servidor a servidor, junto con un flujo simplificado para el desarrollo. AEM as a Cloud Service [Developer Console](development-guidelines.md#crxde-lite-and-developer-console) se usa para generar los tokens necesarios para el proceso de autenticación.

<!-- Alexandru: hiding this until the tutorials reflect the new UI

>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=es#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## El flujo de servidor a servidor {#the-server-to-server-flow}

Los usuarios con una función de administrador de organización de IMS y que sean miembros de los usuarios de AEM o del perfil de producto de los administradores de AEM en AEM Author, pueden generar un conjunto de credenciales a partir de AEM as a Cloud Service. Cada credencial es una carga útil JSON que incluye un certificado (la clave pública), una clave privada y una cuenta técnica que consta de `clientId` y `clientSecret`. Estas credenciales las puede recuperar posteriormente un usuario con la función de administrador del entorno de AEM as a Cloud Service y deben instalarse en un servidor que no sea de AEM y tratarse cuidadosamente como una clave secreta. Este archivo de formato JSON contiene todos los datos necesarios para integrarse con una API de AEM as a Cloud Service. Los datos se utilizan para crear un token JWT firmado, que se intercambia con los servicios de Adobe Identity Management (IMS) por un token de acceso IMS. Este token de acceso se puede utilizar como token de autenticación del portador para realizar solicitudes a AEM as a Cloud Service. El certificado de las credenciales caduca después de un año de forma predeterminada, pero se puede actualizar cuando sea necesario; consulte [Actualizar credenciales](#refresh-credentials).

El flujo de servidor a servidor incluye los siguientes pasos:

* Recupere las credenciales en AEM as a Cloud Service desde Developer Console
* Instale las credenciales de AEM as a Cloud Service en un servidor que no sea de AEM y realice llamadas a AEM
* Genere un token JWT e intercámbielo por un token de acceso mediante las API de IMS de Adobe
* Llamar a la API de AEM con el token de acceso como token de autenticación del portador
* Establezca los permisos adecuados para el usuario de la cuenta técnica en el entorno de AEM

### Recuperar las credenciales de AEM as a Cloud Service {#fetch-the-aem-as-a-cloud-service-credentials}

Los usuarios con acceso a AEM as a Cloud Service developer console ven la pestaña integraciones de Developer Console para un entorno determinado. Un usuario con la función de administrador del entorno de AEM as a Cloud Service puede crear, ver o administrar credenciales.

Al hacer clic en **Crear nueva cuenta técnica**, se crea un conjunto de credenciales que incluye el ID de cliente, el secreto de cliente, la clave privada, el certificado y la configuración para los niveles de creación y publicación del entorno, independientemente de la selección del pod.

![Creando una nueva cuenta técnica](/help/implementing/developing/introduction/assets/s2s-createtechaccount.png)

Se abre una nueva pestaña del explorador que muestra las credenciales. Puede utilizar esta vista para descargar las credenciales pulsando el icono de descarga situado junto al título del estado:

![Descargar credenciales](/help/implementing/developing/introduction/assets/s2s-credentialdownload.png)

Una vez creadas las credenciales, aparecerán en la ficha **Cuentas técnicas** de la sección **Integraciones**:

![Ver credenciales](/help/implementing/developing/introduction/assets/s2s-viewcredentials.png)

Los usuarios pueden ver las credenciales más adelante mediante la acción Ver. Además, como se describe más adelante en el artículo, los usuarios pueden editar las credenciales de la misma cuenta técnica. Para realizar esta edición, crean una clave privada o un certificado, para casos en los que se debe renovar o revocar el certificado.

Los usuarios con la función de administrador del entorno de AEM as a Cloud Service pueden crear posteriormente credenciales para cuentas técnicas adicionales. Esta capacidad es útil cuando diferentes API tienen diferentes requisitos de acceso. Por ejemplo, lectura frente a lectura-escritura.

>[!NOTE]
>
>Los clientes pueden crear hasta diez cuentas técnicas, incluidas las que ya se hayan eliminado.

>[!IMPORTANT]
>
>Un administrador de organización de IMS (normalmente el mismo usuario que aprovisionó el entorno mediante Cloud Manager), que también es miembro del perfil de producto de los usuarios de AEM o de los administradores de AEM en AEM Author, debe acceder primero a Developer Console. A continuación, haga clic en **Crear nueva cuenta técnica** para que un usuario con permisos de administrador genere las credenciales y las recupere posteriormente en el entorno de AEM as a Cloud Service. Si el administrador de la organización de IMS aún no ha creado la cuenta técnica, un mensaje le informa de que necesita la función de administrador de la organización de IMS.

### Instalación de las credenciales del servicio de AEM en un servidor que no sea de AEM {#install-the-aem-service-credentials-on-a-non-aem-server}

La aplicación que realice llamadas a AEM debe poder acceder a las credenciales de AEM as a Cloud Service y tratarlas como un secreto.

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

>[!NOTE]
>Si hay varias credenciales, asegúrese de hacer referencia al archivo json adecuado para la llamada de API a AEM que se invoque más tarde.

### Llamar a la API de AEM {#calling-the-aem-api}

Realice las llamadas de API de servidor a servidor adecuadas a un entorno de AEM as a Cloud Service, incluido el token de acceso en el encabezado. Por lo tanto, para el encabezado &quot;Autorización&quot;, use el valor `"Bearer <access_token>"`. Por ejemplo, usar `curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### Establezca los permisos adecuados para el usuario de la cuenta técnica en AEM {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

En primer lugar, se debe crear un nuevo perfil de producto en Adobe Admin Console.

1. Vaya a Adobe Admin Console en [https://adminconsole.adobe.com/](https://adminconsole.adobe.com/).
1. Presione el vínculo **Administrar** en la columna **Productos y servicios** de la izquierda.
1. Seleccione **AEM as a Cloud Service**.
1. Presione el botón **Nuevo perfil**.

   ![Nuevo perfil](/help/implementing/developing/introduction/assets/s2s-newproductprofile.png)

1. Asigne un nombre al perfil y pulse **Guardar**.

   ![Guardar perfil](/help/implementing/developing/introduction/assets/s2s-saveprofile.png)

1. Seleccione el perfil que ha creado en la lista de perfiles.
1. Seleccione **Agregar usuario**.

   ![Agregar usuario](/help/implementing/developing/introduction/assets/s2s-addusers.png)

1. Agregue la cuenta técnica que creó (en este caso `84b2c3a2-d60a-40dc-84cb-e16b786c1673@techacct.adobe.com`) y haga clic en **Guardar**.

   ![Agregar cuenta técnica](/help/implementing/developing/introduction/assets/s2s-addtechaccount.png)

1. Espere 10 minutos para que los cambios surtan efecto y realice una llamada de API a AEM con un token de acceso generado a partir de la nueva credencial. Como comando cURL, se representaría de forma similar a este ejemplo:

   `curl -H "Authorization: Bearer <access_token>" https://author-pXXXXX-eXXXXX.adobeaemcloud.net/content/dam.json `


Después de realizar la llamada de API, el perfil de producto aparece como un grupo de usuarios en la instancia de autor de AEM as a Cloud Service, con la cuenta técnica adecuada como miembro de ese grupo.

Para comprobar esta información, haga lo siguiente:

1. Inicie sesión en la instancia de autor.
1. Vaya a **Herramientas** > **Seguridad** y luego haga clic en la tarjeta **Grupos**.
1. Busque el nombre del perfil que ha creado en la lista de grupos y haga clic en él:

   ![Perfil de grupo](/help/implementing/developing/introduction/assets/s2s-groupprofile.png)

1. En la siguiente ventana, cambie a la pestaña **Miembros** y compruebe si la cuenta técnica se encuentra en la lista correcta:

   ![Ficha Miembros](/help/implementing/developing/introduction/assets/s2s-techaccountmembers.png)


También puede comprobar que la cuenta técnica aparece en la lista del usuario realizando los siguientes pasos en la instancia de autor:

1. Vaya a **Herramientas** > **Seguridad** > **Usuarios**.
1. Compruebe que su cuenta técnica de es la lista de usuarios y selecciónela.
1. Haga clic en la ficha **Grupos** para comprobar que el usuario forma parte del grupo que corresponde al perfil del producto. Este usuario también es miembro de un puñado de otros grupos, incluidos los Colaboradores:

   ![Pertenencia a grupo](/help/implementing/developing/introduction/assets/s2s-groupmembership.png)

>[!NOTE]
>
>Antes de mediados de 2023, antes de que fuera posible crear varias credenciales, no se guiaba a los clientes para que crearan un perfil de producto en Adobe Admin Console. Como tal, la cuenta técnica no estaba asociada a ningún grupo que no fuera &quot;Colaboradores&quot; en la instancia de AEM as a Cloud Service. Para mantener la coherencia, se recomienda que cree un perfil de producto en Adobe Admin Console para esta cuenta técnica, tal como se ha descrito anteriormente, y que añada la cuenta técnica existente a ese grupo.

<u>**Establecer los permisos de grupo apropiados**</u>

Finalmente, configure el grupo con los permisos adecuados necesarios para que pueda invocar o bloquear las API correctamente.

1. Inicie sesión en la instancia de autor adecuada y vaya a **Configuración** > **Seguridad** > **Permisos**
1. Busque el nombre del grupo correspondiente al perfil de producto en el panel izquierdo (en este caso, API de solo lectura) y selecciónelo:

   ![Buscar grupo](/help/implementing/developing/introduction/assets/s2s-searchforgroup.png)

1. Haga clic en el botón Edit en la siguiente ventana:

   ![Editar permisos](/help/implementing/developing/introduction/assets/s2s-editpermissions.png) 

1. Modifique los permisos correctamente y haga clic en **Guardar**

   ![Confirmar edición de permisos](/help/implementing/developing/introduction/assets/s2s-confirmeditpermissions.png)

>[!INFO]
>
>Obtenga más información acerca de Adobe Identity Management System (IMS) y los usuarios y grupos de AEM. Consulte la [documentación](/help/security/ims-support.md).

## Flujo de desarrollador {#developer-flow}

Es probable que los desarrolladores deseen realizar pruebas con una instancia de desarrollo de su aplicación que no sea AEM (que se ejecute en su portátil o alojada) que realice solicitudes a un entorno de desarrollo de AEM as a Cloud Service de desarrollo. Sin embargo, dado que los desarrolladores no tienen necesariamente permisos de función de administrador de IMS, Adobe no puede suponer que pueden generar el portador JWT descrito en el flujo normal de servidor a servidor. Por lo tanto, Adobe proporciona un mecanismo para que un desarrollador genere un token de acceso directamente que pueda utilizarse en solicitudes a entornos de AEM as a Cloud Service a los que tiene acceso.

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

1. Vaya a **Token local** en **Integraciones**
1. Haga clic en **Obtener token de desarrollo local** en Developer Console para poder generar un token de acceso.

### Llamar a la aplicación de AEM con un token de acceso {#call-the-aem-application-with-an-access-token}

Realice las llamadas de API de servidor a servidor adecuadas desde la aplicación que no sea de AEM a un entorno de AEM as a Cloud Service, incluido el token de acceso en el encabezado. Por lo tanto, para el encabezado &quot;Autorización&quot;, use el valor `"Bearer <access_token>"`.

## Actualizar credenciales {#refresh-credentials}

De forma predeterminada, las credenciales de AEM as a Cloud Service caducan al cabo de un año. Para garantizar la continuidad del servicio, los desarrolladores tienen la opción de actualizar las credenciales y ampliar su disponibilidad durante un año adicional.

Para conseguir esta extensión de actualización, haga lo siguiente:

* Use el botón **Agregar certificado** en **Integraciones** - **Cuentas técnicas** en Developer Console, como se muestra a continuación

  ![Actualización de credenciales](/help/implementing/developing/introduction/assets/s2s-credentialrefresh.png)

* Después de pulsar el botón, se genera un conjunto de credenciales que incluye un nuevo certificado. Instale las nuevas credenciales en su servidor externo a AEM y asegúrese de que la conectividad se comporta según lo esperado, sin eliminar las credenciales antiguas.
* Asegúrese de que se utilizan las nuevas credenciales en lugar de las antiguas al generar el token de acceso.
* Si lo desea, puede revocar (y luego eliminar) el certificado anterior para que ya no se pueda utilizar en la autenticación con AEM as a Cloud Service.

## Revocación de credenciales {#credentials-revocation}

Si la clave privada está en peligro, debe crear credenciales con un nuevo certificado y una nueva clave privada. Una vez que la aplicación utiliza las nuevas credenciales para poder generar tokens de acceso, puede revocar y eliminar los certificados antiguos haciendo lo siguiente:

1. En primer lugar, añada la nueva clave. Esta clave genera credenciales con una nueva clave privada y un nuevo certificado. La nueva clave privada está marcada en la interfaz de usuario como **actual** y, por lo tanto, se usa para todas las credenciales nuevas de esta cuenta técnica a partir de ahora. Las credenciales asociadas con las claves privadas anteriores siguen siendo válidas hasta que se revoquen. Para lograr esta revocación, seleccione los tres puntos (**...**) de su cuenta técnica actual y, a continuación, seleccione **Agregar nueva clave privada**:

   ![Agregar nueva clave privada](/help/implementing/developing/introduction/assets/s2s-addnewprivatekey.png)

1. Seleccione **Add** en el símbolo del sistema que sigue:

   ![Confirmar adición de nueva clave privada](/help/implementing/developing/introduction/assets/s2s-addprivatekeyconfirm.png)

   Se abre una nueva pestaña de examinar con las nuevas credenciales y se actualiza la interfaz de usuario para mostrar ambas claves privadas con la nueva marcada como **actual**:

   ![Claves privadas en la interfaz de usuario](/help/implementing/developing/introduction/assets/s2s-twokeys.png)

1. Instale las nuevas credenciales en el servidor que no sea de AEM y asegúrese de que la conectividad funciona según lo esperado. Consulte [Flujo de servidor a servidor](#the-server-to-server-flow) para obtener más información.
1. Revocar el certificado antiguo seleccionando los tres puntos (**...**) a la derecha del certificado y seleccionando **Revocar**:

   ![Revocar certificado](/help/implementing/developing/introduction/assets/s2s-revokecert.png)

   A continuación, confirme la revocación en el siguiente mensaje presionando el botón **Revocar**:

   ![Revocar confirmación de certificado](/help/implementing/developing/introduction/assets/s2s-revokecertificateconfirmation.png)

1. Finalmente, elimine el certificado comprometido.
