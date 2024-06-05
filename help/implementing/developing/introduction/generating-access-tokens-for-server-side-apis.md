---
title: Generación de tokens de acceso para las API del lado del servidor
description: AEM Obtenga información sobre cómo facilitar la comunicación entre un servidor de terceros y el as a Cloud Service de la mediante la generación de un token JWT seguro
exl-id: 20deaf8f-328e-4cbf-ac68-0a6dd4ebf0c9
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '2089'
ht-degree: 0%

---

# Generación de tokens de acceso para las API del lado del servidor {#generating-access-tokens-for-server-side-apis}

AEM Algunas arquitecturas se basan en realizar llamadas a las infraestructuras as a Cloud Service AEM desde una aplicación hospedada en un servidor fuera de la infraestructura de la red de trabajo de la infraestructura de. AEM Por ejemplo, una aplicación móvil que llama a un servidor y que luego hace que las solicitudes de API se vean as a Cloud Service, se.

A continuación se describe el flujo de servidor a servidor, junto con un flujo simplificado para el desarrollo. AEM El as a Cloud Service [Developer Console](development-guidelines.md#crxde-lite-and-developer-console) se utiliza para generar los tokens necesarios para el proceso de autenticación.

<!-- Alexandru: hiding this until the tutorials reflect the new UI

>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## El flujo de servidor a servidor {#the-server-to-server-flow}

AEM AEM AEM AEM Los usuarios con un rol de administrador de organización de IMS y que sean miembros del Perfil de producto de usuarios de la organización de IMS o administradores de la organización de la en Autor, pueden generar un conjunto de credenciales a partir de las credenciales as a Cloud Service de los usuarios de la organización de. Cada credencial es una carga útil JSON que incluye un certificado (la clave pública), una clave privada y una cuenta técnica que consta de una `clientId` y `clientSecret`. AEM Estas credenciales las puede recuperar posteriormente un usuario con la función de administrador de entorno as a Cloud Service AEM de la, y deben instalarse en un servidor que no sea de la red de servidores de y tratarse cuidadosamente como una clave secreta. AEM Este archivo de formato JSON contiene todos los datos necesarios para integrarse con una API as a Cloud Service de. Los datos se utilizan para crear un token JWT firmado, que se intercambia con los servicios de Identity Management de Adobe (IMS) por un token de acceso IMS. AEM A continuación, este token de acceso se puede utilizar como token de autenticación del portador para realizar solicitudes a los as a Cloud Service de la. El certificado de las credenciales caduca después de un año de forma predeterminada, pero se puede actualizar cuando sea necesario, tal como se describe a continuación [aquí](#refresh-credentials).

El flujo de servidor a servidor incluye los siguientes pasos:

* AEM Recupere las credenciales en las as a Cloud Service desde Developer Console
* AEM Instale las credenciales para la as a Cloud Service AEM AEM en un servidor que no sea de la red y que realice llamadas a la red desde un servidor que no sea de la red de
* Genere un token JWT e intercámbielo por un token de acceso mediante las API de IMS de Adobe
* AEM Llamar a la API de con el token de acceso como token de autenticación del portador
* AEM Establezca los permisos adecuados para el usuario de la cuenta técnica en el entorno de la

### AEM Recuperar las credenciales as a Cloud Service de la {#fetch-the-aem-as-a-cloud-service-credentials}

AEM Los usuarios con acceso a la consola de desarrollador as a Cloud Service de la ven la pestaña integraciones en Developer Console para un entorno determinado. AEM Un usuario con la función de administrador de entorno as a Cloud Service de puede crear, ver o administrar credenciales.

Clic **Crear nueva cuenta técnica** A continuación, se crea un conjunto de credenciales que incluye el id de cliente, el secreto de cliente, la clave privada, el certificado y la configuración para los niveles de autor y publicación del entorno, independientemente de la selección del pod.

![Creación de una nueva cuenta técnica](/help/implementing/developing/introduction/assets/s2s-createtechaccount.png)

Se abre una nueva pestaña del explorador que muestra las credenciales. Puede utilizar esta vista para descargar las credenciales pulsando el icono de descarga situado junto al título del estado:

![Descargar credenciales](/help/implementing/developing/introduction/assets/s2s-credentialdownload.png)

Una vez creadas las credenciales, aparecerán en el **Cuentas técnicas** en la pestaña **Integraciones** sección:

![Ver credenciales](/help/implementing/developing/introduction/assets/s2s-viewcredentials.png)

Los usuarios pueden ver las credenciales más adelante mediante la acción Ver. Además, como se describe más adelante en el artículo, los usuarios pueden editar las credenciales de la misma cuenta técnica. Para realizar esta edición, crean una clave privada o un certificado, para casos en los que se debe renovar o revocar el certificado.

AEM Los usuarios con la función Administrador de entornos as a Cloud Service de la aplicación de la pueden crear posteriormente credenciales para cuentas técnicas adicionales. Esta capacidad es útil cuando diferentes API tienen diferentes requisitos de acceso. Por ejemplo, lectura frente a lectura-escritura.

>[!NOTE]
>
>Los clientes pueden crear hasta diez cuentas técnicas, incluidas las que ya se hayan eliminado.

>[!IMPORTANT]
>
>AEM AEM AEM Un administrador de organización de IMS (normalmente el mismo usuario que aprovisionó el entorno mediante Cloud Manager), que también es miembro del Perfil de producto de usuarios o administradores de en el Autor de, debe acceder primero a Developer Console. A continuación, haga clic en **Crear nueva cuenta técnica** AEM para que las credenciales se generen y posteriormente se recuperen mediante un usuario con permisos de administrador en el entorno as a Cloud Service de la. Si el administrador de la organización de IMS aún no ha creado la cuenta técnica, un mensaje le informa de que necesita la función de administrador de la organización de IMS.

### AEM AEM Instalación de las credenciales del servicio de en un servidor que no sea de tipo {#install-the-aem-service-credentials-on-a-non-aem-server}

AEM AEM La aplicación que realice llamadas a la debe poder acceder a las credenciales de los as a Cloud Service de la aplicación, tratándolas como un secreto.

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

>[!NOTE]
>AEM Si hay varias credenciales, asegúrese de hacer referencia al archivo json adecuado para la llamada de API a que se invoque más tarde

### AEM Llamar a la API de {#calling-the-aem-api}

AEM Realice las llamadas de API de servidor a servidor adecuadas a un entorno as a Cloud Service de la, incluido el token de acceso del encabezado. Por lo tanto, para el encabezado Autorización, utilice el valor `"Bearer <access_token>"`. Por ejemplo, con `curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### AEM Establezca los permisos adecuados para el usuario de la cuenta técnica en el cuadro de {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

En primer lugar, se debe crear un nuevo perfil de producto en Adobe Admin Console.

1. Vaya a Adobe Admin Console en [https://adminconsole.adobe.com/](https://adminconsole.adobe.com/).
1. Pulse el botón **Administrar** vínculo debajo de **Productos y servicios** columna de la izquierda.
1. Seleccionar **AEM as a Cloud Service**.
1. Pulse el botón **Nuevo perfil** botón.

   ![Nuevo perfil](/help/implementing/developing/introduction/assets/s2s-newproductprofile.png)

1. Asigne un nombre al perfil y pulse **Guardar**.

   ![Guardar perfil](/help/implementing/developing/introduction/assets/s2s-saveprofile.png)

1. Seleccione el perfil que ha creado en la lista de perfiles.
1. Seleccionar **Añadir usuario**.

   ![Añadir usuario](/help/implementing/developing/introduction/assets/s2s-addusers.png)

1. Añada la cuenta técnica que ha creado (en este caso, ) `84b2c3a2-d60a-40dc-84cb-e16b786c1673@techacct.adobe.com`) y haga clic en **Guardar**.

   ![Agregar cuenta técnica](/help/implementing/developing/introduction/assets/s2s-addtechaccount.png)

1. AEM Espere 10 minutos para que los cambios surtan efecto y realice una llamada de API a la función con un token de acceso generado a partir de la nueva credencial. Como comando cURL, se representaría de forma similar a este ejemplo:

   `curl -H "Authorization: Bearer <access_token>" https://author-pXXXXX-eXXXXX.adobeaemcloud.net/content/dam.json `


AEM Después de realizar la llamada de API, el perfil de producto aparece como un grupo de usuarios en la instancia de autor as a Cloud Service de la aplicación, con la cuenta técnica adecuada como miembro de ese grupo.

Para comprobar esta información, haga lo siguiente:

1. Inicie sesión en la instancia de autor.
1. Ir a **Herramientas** > **Seguridad**, luego haga clic en **Grupos** Tarjeta de.
1. Busque el nombre del perfil que ha creado en la lista de grupos y haga clic en él:

   ![Perfil de grupo](/help/implementing/developing/introduction/assets/s2s-groupprofile.png)

1. En la siguiente ventana, cambie a la **Miembros** y compruebe si la cuenta técnica de se muestra correctamente en la lista:

   ![Pestaña Miembros](/help/implementing/developing/introduction/assets/s2s-techaccountmembers.png)


También puede comprobar que la cuenta técnica aparece en la lista del usuario realizando los siguientes pasos en la instancia de autor:

1. Vaya a **Herramientas** > **Seguridad** > **Usuarios**.
1. Compruebe que su cuenta técnica de es la lista de usuarios y selecciónela.
1. Haga clic en **Grupos** para que pueda verificar que el usuario forma parte del grupo que corresponde al perfil de producto. Este usuario también es miembro de un puñado de otros grupos, incluidos los Colaboradores:

   ![Pertenencia a grupo](/help/implementing/developing/introduction/assets/s2s-groupmembership.png)

>[!NOTE]
>
>Antes de mediados de 2023, antes de que fuera posible crear varias credenciales, no se guiaba a los clientes para que crearan un perfil de producto en Adobe Admin Console. AEM Como tal, la cuenta técnica no estaba asociada a ningún grupo que no fuera &quot;Colaboradores&quot; en la instancia as a Cloud Service de la. Para mantener la coherencia, se recomienda que cree un perfil de producto en Adobe Admin Console para esta cuenta técnica, tal como se ha descrito anteriormente, y que añada la cuenta técnica existente a ese grupo.

<u>**Establecer los permisos de grupo adecuados**</u>

Finalmente, configure el grupo con los permisos adecuados necesarios para que pueda invocar o bloquear las API correctamente.

1. Inicie sesión en la instancia de autor adecuada y navegue hasta **Configuración** > **Seguridad** > **Permisos**
1. Busque el nombre del grupo correspondiente al perfil de producto en el panel izquierdo (en este caso, API de solo lectura) y selecciónelo:

   ![Buscar por grupo](/help/implementing/developing/introduction/assets/s2s-searchforgroup.png)

1. Haga clic en el botón Edit en la siguiente ventana:

   ![Edición de permisos](/help/implementing/developing/introduction/assets/s2s-editpermissions.png) 

1. Modifique los permisos correctamente y haga clic en **Guardar**

   ![Confirmar edición de permisos](/help/implementing/developing/introduction/assets/s2s-confirmeditpermissions.png)

>[!INFO]
>
>Obtenga más información acerca del sistema Identity Management AEM de Adobe (IMS) y los usuarios y grupos de. Consulte la [documentación](/help/security/ims-support.md).

## Flujo de desarrollador {#developer-flow}

AEM AEM Es probable que los desarrolladores deseen realizar pruebas con una instancia de desarrollo de su aplicación que no sea de desarrollo (ya sea que se ejecute en su portátil o alojada) que realice solicitudes a un entorno de desarrollo as a Cloud Service de desarrollo de. Sin embargo, como los desarrolladores no tienen necesariamente permisos de función de administrador de IMS, Adobe no puede suponer que pueden generar el portador JWT descrito en el flujo normal de servidor a servidor. Por lo tanto, el Adobe AEM proporciona un mecanismo para que un desarrollador genere un token de acceso directamente que se pueda utilizar en solicitudes a entornos en los que tenga acceso en el as a Cloud Service de los entornos a los que tenga acceso.

Consulte la [Documentación de directrices para desarrolladores](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) AEM para obtener información acerca de los permisos necesarios para utilizar la consola de desarrollador de as a Cloud Service.

>[!NOTE]
>
>El token de acceso de desarrollo local es válido durante un máximo de 24 horas tras las cuales debe regenerarse mediante el mismo método.

AEM AEM Los desarrolladores pueden utilizar este token para realizar llamadas desde su aplicación de prueba no-a un entorno as a Cloud Service de la. AEM Normalmente, el desarrollador utiliza este token con la aplicación que no es de la aplicación en su propio portátil, es decir, con la aplicación que no es de la misma aplicación. AEM Además, el entorno de as a Cloud no suele ser de producción.

El flujo para desarrolladores incluye los siguientes pasos:

* Generar un token de acceso desde Developer Console
* AEM Llame a la aplicación de con el token de acceso.

AEM Los desarrolladores también pueden realizar llamadas de API a un proyecto de que se ejecute en su equipo local, en cuyo caso no se necesita un token de acceso.

### Generación del token de acceso {#generating-the-access-token}

1. Vaya a la **Token local** bajo **Integraciones**
1. Clic **Obtener token de desarrollo local** en Developer Console para poder generar un token de acceso.

### AEM Llamar a la aplicación de con un token de acceso {#call-the-aem-application-with-an-access-token}

AEM AEM Realice las llamadas de API de servidor a servidor adecuadas desde la aplicación no-a un entorno as a Cloud Service de la aplicación, incluido el token de acceso en el encabezado. Por lo tanto, para el encabezado Autorización, utilice el valor `"Bearer <access_token>"`.

## Actualizar credenciales {#refresh-credentials}

AEM De forma predeterminada, las credenciales de los as a Cloud Service caducan al cabo de un año. Para garantizar la continuidad del servicio, los desarrolladores tienen la opción de actualizar las credenciales y ampliar su disponibilidad durante un año adicional.

Para conseguir esta extensión de actualización, haga lo siguiente:

* Utilice el **Añadir certificado** botón debajo de **Integraciones** - **Cuentas técnicas** en Developer Console, como se muestra a continuación

  ![Actualización de credenciales](/help/implementing/developing/introduction/assets/s2s-credentialrefresh.png)

* Después de pulsar el botón, se genera un conjunto de credenciales que incluye un nuevo certificado. AEM Instale las nuevas credenciales en su servidor fuera de la red y asegúrese de que la conectividad es la esperada, sin eliminar las credenciales antiguas.
* Asegúrese de que se utilizan las nuevas credenciales en lugar de las antiguas al generar el token de acceso.
* AEM Opcionalmente, puede revocar (y luego eliminar) el certificado anterior para que ya no se pueda utilizar para autenticarse con el as a Cloud Service de la.

## Revocación de credenciales {#credentials-revocation}

Si la clave privada está en peligro, debe crear credenciales con un nuevo certificado y una nueva clave privada. Una vez que la aplicación utiliza las nuevas credenciales para poder generar tokens de acceso, puede revocar y eliminar los certificados antiguos haciendo lo siguiente:

1. En primer lugar, añada la nueva clave. Esta clave genera credenciales con una nueva clave privada y un nuevo certificado. La nueva clave privada se marca en la interfaz de usuario como **corriente** y, por lo tanto, se utiliza para todas las nuevas credenciales de esta cuenta técnica a partir de ahora. Las credenciales asociadas con las claves privadas anteriores siguen siendo válidas hasta que se revoquen. Para conseguir esta revocación, seleccione los tres puntos (**...**) en su cuenta técnica actual y seleccione **Añadir nueva clave privada**:

   ![Añadir nueva clave privada](/help/implementing/developing/introduction/assets/s2s-addnewprivatekey.png)

1. Seleccionar **Añadir** en el siguiente mensaje:

   ![Confirmar la adición de una nueva clave privada](/help/implementing/developing/introduction/assets/s2s-addprivatekeyconfirm.png)

   Se abre una nueva pestaña de exploración con las nuevas credenciales y la interfaz de usuario se actualiza para mostrar ambas claves privadas con la nueva marcada como **corriente**:

   ![Claves privadas en la interfaz de usuario](/help/implementing/developing/introduction/assets/s2s-twokeys.png)

1. AEM Instale las nuevas credenciales en el servidor que no sea de la red y asegúrese de que la conectividad funciona según lo esperado. Consulte [Sección Flujo de servidor a servidor](#the-server-to-server-flow) para obtener más información.
1. Revocar el certificado antiguo seleccionando los tres puntos (**...**) a la derecha del certificado y seleccione **Revocar**:

   ![Revocar certificado](/help/implementing/developing/introduction/assets/s2s-revokecert.png)

   A continuación, confirme la revocación en el siguiente mensaje pulsando la tecla **Revocar** botón:

   ![Revocar confirmación de certificado](/help/implementing/developing/introduction/assets/s2s-revokecertificateconfirmation.png)

1. Finalmente, elimine el certificado comprometido.
