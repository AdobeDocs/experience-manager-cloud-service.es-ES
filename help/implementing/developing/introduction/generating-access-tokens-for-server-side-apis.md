---
title: Generación de tokens de acceso para las API del servidor
description: Aprenda a facilitar la comunicación entre un servidor de terceros y AEM as a Cloud Service mediante la generación de un token JWT seguro
exl-id: 20deaf8f-328e-4cbf-ac68-0a6dd4ebf0c9
source-git-commit: 41458eb1fba12e8ef45a32d3bb6fc5dd732f78ec
workflow-type: tm+mt
source-wordcount: '2199'
ht-degree: 1%

---

# Generación de tokens de acceso para las API del servidor {#generating-access-tokens-for-server-side-apis}

>[!AVAILABILITY]
>
>El Adobe está en proceso de implementar gradualmente las nuevas funciones de revocación de credenciales y múltiples credenciales que se describen en este artículo. Si, al comprobar la pestaña integraciones en la consola de desarrollador de AEM de su organización, observa que la pantalla tiene un aspecto diferente al de las capturas de pantalla siguientes, significa que los nuevos cambios aún no se han implementado en su organización. En este caso, consulte la [documentación heredada](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis-legacy.md).

Algunas arquitecturas dependen de realizar llamadas a AEM as a Cloud Service desde una aplicación alojada en un servidor fuera de AEM infraestructura. Por ejemplo, una aplicación móvil que llama a un servidor y que luego realiza solicitudes de API para AEM as a Cloud Service.

El flujo de servidor a servidor se describe a continuación, junto con un flujo simplificado para el desarrollo. El AEM as a Cloud Service [Developer Console](development-guidelines.md#crxde-lite-and-developer-console) se utiliza para generar los tokens necesarios para el proceso de autenticación.

<!-- Alexandru: hiding this until the tutorials reflect the new UI

>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## Flujo de servidor a servidor {#the-server-to-server-flow}

Un usuario con una función de administrador de organización de IMS y que también sea miembro del perfil de producto AEM Usuarios o Administradores de AEM en AEM Author, puede generar un conjunto de credenciales as a Cloud Service AEM, cada una de las cuales es una carga útil JSON que incluye un certificado (la clave pública), una clave privada y una cuenta técnica que consta de una `clientId` y `clientSecret`. Estas credenciales pueden ser recuperadas posteriormente por un usuario con la función de administrador de entorno as a Cloud Service de AEM y deben instalarse en un servidor no AEM y tratarse cuidadosamente como clave secreta. Este archivo de formato JSON contiene todos los datos necesarios para la integración con una API as a Cloud Service AEM. Los datos se utilizan para crear un token de JWT firmado, que se intercambia con el Adobe Identity Management Services (IMS) por un token de acceso de IMS. Este token de acceso se puede utilizar como token de autenticación del portador para realizar solicitudes AEM as a Cloud Service. El certificado de las credenciales caduca después de un año de forma predeterminada, pero se puede actualizar cuando sea necesario, tal como se describe [here](#refresh-credentials).

El flujo de servidor a servidor implica los siguientes pasos:

* Recupere las credenciales as a Cloud Service AEM de Developer Console
* Instale las credenciales as a Cloud Service de AEM en un servidor que no sea AEM realizando llamadas a AEM
* Genere un token JWT e intercambie ese token por un token de acceso mediante las API IMS de Adobe
* Llamar a la API de AEM con el token de acceso como token de autenticación de portador
* Establezca los permisos adecuados para el usuario de cuenta técnica en el entorno de AEM

### Recuperación de las credenciales as a Cloud Service AEM {#fetch-the-aem-as-a-cloud-service-credentials}

Los usuarios con acceso a la consola de desarrollador as a Cloud Service de AEM verán la pestaña integraciones en Developer Console para un entorno determinado. Un usuario con la función de administrador de entorno as a Cloud Service de AEM puede crear, ver o administrar credenciales.

Al hacer clic en **Crear nueva cuenta técnica** , se creará un nuevo conjunto de credenciales que incluye id de cliente, secreto de cliente, clave privada, certificado y configuración para los niveles de creación y publicación del entorno, independientemente de la selección del pod.

![Creación de una nueva cuenta técnica](/help/implementing/developing/introduction/assets/s2s-createtechaccount.png)

Se abrirá una nueva pestaña del explorador que mostrará las credenciales. Puede utilizar esta vista para descargar las credenciales pulsando el icono de descarga situado junto al título del estado:

![Descargar credenciales](/help/implementing/developing/introduction/assets/s2s-credentialdownload.png)

Una vez creadas las credenciales, aparecerán en la sección **Cuentas técnicas** en la ficha **Integraciones** sección:

![Ver credenciales](/help/implementing/developing/introduction/assets/s2s-viewcredentials.png)

Posteriormente, los usuarios pueden ver las credenciales mediante la acción Ver . Además, como se describe más adelante en el artículo, los usuarios pueden modificar las credenciales de la misma cuenta técnica creando una nueva clave privada o certificado, en los casos en que sea necesario renovar o revocar el certificado.

Los usuarios con la AEM función de administrador as a Cloud Service de entorno pueden crear más adelante nuevas credenciales para cuentas técnicas adicionales. Esto resulta útil cuando diferentes API tienen diferentes requisitos de acceso. Por ejemplo, lectura frente a lectura-escritura.

>[!NOTE]
>
>Los clientes pueden crear hasta 10 cuentas técnicas, incluidas las que ya se han eliminado.

>[!IMPORTANT]
>
>Un administrador de organización de IMS (normalmente el mismo usuario que aprovisionó el entorno a través de Cloud Manager), que también debe ser miembro del perfil de producto de los usuarios AEM o AEM administradores en AEM Author, primero debe acceder a Developer Console y hacer clic en el botón **Crear nueva cuenta técnica** para que un usuario con permisos de administrador en el entorno as a Cloud Service AEM genere y recupere posteriormente las credenciales. Si el administrador de organización de IMS no lo ha hecho, un mensaje les informará de que necesitan la función de administrador de organización de IMS.

### Instalación de las credenciales del servicio de AEM en un servidor que no sea AEM {#install-the-aem-service-credentials-on-a-non-aem-server}

La aplicación que realiza llamadas a AEM debe poder acceder a las credenciales as a Cloud Service de AEM, tratándolas como un secreto.

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

>[!NOTE]
>Si hay varias credenciales, asegúrese de hacer referencia al archivo json apropiado para la llamada de API a AEM que se invocará más adelante.

### Llamar a la API de AEM {#calling-the-aem-api}

Realice las llamadas de API de servidor a servidor adecuadas a un entorno as a Cloud Service AEM, incluido el token de acceso en el encabezado. Por lo tanto, para el encabezado &quot;Autorización&quot;, utilice el valor `"Bearer <access_token>"`. Por ejemplo, al usar `curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### Establezca los permisos adecuados para el usuario de cuenta técnica en AEM {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

En primer lugar, se debe crear un nuevo perfil de producto en Adobe Admin Console. Para conseguirlo, siga estos pasos:

1. Vaya a Adobe Admin Console en [https://adminconsole.adobe.com/](https://adminconsole.adobe.com/)
1. Pulse el botón **Administrar** enlace en el **Productos y servicios** a la izquierda.
1. Select **AEM as a Cloud Service**
1. Pulse el botón **Nuevo perfil** botón

   ![Nuevo perfil](/help/implementing/developing/introduction/assets/s2s-newproductprofile.png)

1. Asigne un nombre al perfil y pulse **Guardar**

   ![Guardar perfil](/help/implementing/developing/introduction/assets/s2s-saveprofile.png)

1. Seleccione el perfil que acaba de crear en la lista de perfiles
1. Pulse el botón **Agregar usuario** botón

   ![Agregar usuario](/help/implementing/developing/introduction/assets/s2s-addusers.png)

1. Añada la cuenta técnica que acaba de crear (en este caso `84b2c3a2-d60a-40dc-84cb-e16b786c1673@techacct.adobe.com`) y pulse **Guardar**

   ![Agregar cuenta técnica](/help/implementing/developing/introduction/assets/s2s-addtechaccount.png)

1. Espere 10 minutos para que los cambios surtan efecto y realice una llamada API a AEM con un token de acceso generado a partir de la nueva credencial. Como comando cURL, se representaría de forma similar a este ejemplo:

   `curl -H "Authorization: Bearer <access_token>" https://author-pXXXXX-eXXXXX.adobeaemcloud.net/content/dam.json `


Después de realizar la llamada de API, el perfil de producto aparecerá como grupo de usuarios en la instancia de autor as a Cloud Service de AEM, con la cuenta técnica adecuada como miembro de ese grupo.

Para comprobar esto, debe:

1. Inicie sesión en la instancia de autor.
1. Vaya a **Herramientas** - **Seguridad** y haga clic en el botón **Grupos** tarjeta
1. Busque el nombre del perfil que creó en la lista de grupos y haga clic en él:

   ![Perfil de grupo](/help/implementing/developing/introduction/assets/s2s-groupprofile.png)

1. En la siguiente ventana, cambie a la **Miembros** y compruebe si la cuenta técnica está correctamente enumerada allí:

   ![Ficha Miembros](/help/implementing/developing/introduction/assets/s2s-techaccountmembers.png)


También puede verificar que la cuenta técnica aparece en la lista de usuarios realizando los pasos siguientes en la instancia de autor:

1. Vaya a **Herramientas** - **Seguridad** - **Usuarios**
1. Compruebe que su cuenta técnica sea la lista de usuarios y haga clic en ella
1. Haga clic en el **Grupos** para comprobar que el usuario forma parte del grupo que corresponde a su perfil de producto. Este usuario también es miembro de un puñado de otros grupos, incluidos los colaboradores:

   ![Miembros del grupo](/help/implementing/developing/introduction/assets/s2s-groupmembership.png)

>[!NOTE]
>
>Antes de mediados de 2023, antes de poder crear varias credenciales, no se les guiaba para crear un perfil de producto en Admin Console de Adobe y, por lo tanto, la cuenta técnica no estaba asociada a ningún grupo que no fuera &quot;Colaboradores&quot; en la instancia as a Cloud Service de AEM. En aras de la coherencia, se recomienda que, para esta cuenta técnica, cree un nuevo perfil de producto en Adobe Admin Console como se ha descrito anteriormente y agregue la cuenta técnica existente a ese grupo.

<u>**Establecer los permisos del grupo apropiado**</u>

Finalmente, configure el grupo con los permisos adecuados a para invocar o bloquear sus API de forma adecuada. Para ello:

1. Inicie sesión en la instancia de autor adecuada y vaya a **Configuración** - **Seguridad** - **Permisos**
1. Busque el nombre del grupo correspondiente al perfil del producto en el panel izquierdo (en este caso API de solo lectura) y haga clic en él:

   ![Buscar grupo](/help/implementing/developing/introduction/assets/s2s-searchforgroup.png)

1. Haga clic en el botón Editar en la siguiente ventana:

   ![Edición de permisos](/help/implementing/developing/introduction/assets/s2s-editpermissions.png) 

1. Modifique los permisos correctamente y haga clic en **Guardar**

   ![Confirmar edición de permisos](/help/implementing/developing/introduction/assets/s2s-confirmeditpermissions.png)

>[!INFO]
>
>Obtenga más información sobre el sistema Identity Management de Adobe (IMS) y AEM usuarios y grupos consultando al [documentación](/help/security/ims-support.md).

## Flujo de desarrollador {#developer-flow}

Es probable que los desarrolladores deseen probar utilizando una instancia de desarrollo de su aplicación no AEM (ya sea ejecutándose en su portátil o alojada) que realice solicitudes a un entorno de desarrollo AEM desarrollo as a Cloud Service. Sin embargo, dado que los desarrolladores no tienen necesariamente permisos de rol de administrador de IMS, no podemos suponer que puedan generar el portador de JWT descrito en el flujo regular de servidor a servidor. Por lo tanto, proporcionamos un mecanismo para que un desarrollador genere un token de acceso directamente que pueda utilizarse en solicitudes para AEM entornos as a Cloud Service a los que tenga acceso.

Consulte la [Documentación de las directrices para desarrolladores](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) para obtener información sobre los permisos necesarios para utilizar la consola de desarrollador as a Cloud Service de AEM.

>[!NOTE]
>
>El token de acceso de desarrollo local es válido durante un máximo de 24 horas tras las cuales debe regenerarse con el mismo método.

Los desarrolladores pueden utilizar este token para realizar llamadas desde su aplicación de prueba AEM a un entorno as a Cloud Service AEM. Normalmente, el desarrollador utilizará este token con la aplicación que no es de AEM en su propio portátil. Además, el AEM as a Cloud suele ser un entorno que no sea de producción.

El flujo del desarrollador incluye los siguientes pasos:

* Generar un token de acceso desde Developer Console
* Llame a la aplicación AEM con el token de acceso.

Los desarrolladores también pueden realizar llamadas API a un proyecto AEM que se ejecuta en su equipo local, en cuyo caso no se necesita un token de acceso.

### Generación del token de acceso {#generating-the-access-token}

1. Vaya a la **Token local** under **Integraciones**
1. Haga clic en el **Obtener token de desarrollo local** para generar un token de acceso.

### Llame a la aplicación AEM con un token de acceso {#call-the-aem-application-with-an-access-token}

Realice las llamadas de API de servidor a servidor adecuadas desde la aplicación que no es de AEM a un entorno as a Cloud Service AEM, incluido el token de acceso en el encabezado. Por lo tanto, para el encabezado &quot;Autorización&quot;, utilice el valor `"Bearer <access_token>"`.

## Actualizar credenciales {#refresh-credentials}

De forma predeterminada, las credenciales as a Cloud Service AEM caducan después de un año. Para garantizar la continuidad del servicio, los desarrolladores tienen la opción de actualizar las credenciales, ampliando su disponibilidad durante un año adicional.

Para lograrlo, puede:

* Utilice la variable **Agregar certificado** botón debajo de **Integraciones** - **Cuentas técnicas** en Developer Console, como se muestra a continuación

   ![Actualización de la credencial](/help/implementing/developing/introduction/assets/s2s-credentialrefresh.png)

* Después de pulsar el botón , se generará un conjunto de credenciales que incluye un nuevo certificado. Instale las nuevas credenciales en su servidor fuera de AEM y asegúrese de que la conectividad se ajusta a lo esperado, sin eliminar las credenciales antiguas 
* Asegúrese de que se utilicen las nuevas credenciales en lugar de las antiguas al generar el token de acceso
* Si lo desea, revoque (y luego elimine) el certificado anterior para que ya no se pueda usar para autenticarse con AEM as a Cloud Service.

## Revocación de credenciales {#credentials-revocation}

Si la clave privada está en peligro, debe crear credenciales con un nuevo certificado y una nueva clave privada. Una vez que la aplicación utilice las nuevas credenciales para generar tokens de acceso, puede revocar y eliminar los certificados antiguos.

Para ello, siga estos pasos:

1. En primer lugar, añada la nueva clave. Esto generará credenciales con una nueva clave privada y un nuevo certificado. La nueva clave privada se marcará en la interfaz de usuario como **current** y por lo tanto se utilizará para todas las nuevas credenciales de esta cuenta técnica a partir de ahora. Tenga en cuenta que las credenciales asociadas con las claves privadas antiguas seguirán siendo válidas hasta que se revoquen. Para conseguirlo, presione los tres puntos (**...**) en su cuenta técnica actual y pulse **Añadir nueva clave privada**:

   ![Añadir nueva clave privada](/help/implementing/developing/introduction/assets/s2s-addnewprivatekey.png)

1. Press **Agregar** en el mensaje que se indica a continuación:

   ![Confirmar la adición de la nueva clave privada](/help/implementing/developing/introduction/assets/s2s-addprivatekeyconfirm.png)

   Se abrirá una nueva pestaña de navegación con las nuevas credenciales y la interfaz de usuario se actualizará para mostrar ambas claves privadas, con la nueva marcada como **current**:

   ![Claves privadas en la interfaz de usuario](/help/implementing/developing/introduction/assets/s2s-twokeys.png)

1. Instale las nuevas credenciales en el servidor no AEM y asegúrese de que la conectividad funciona según lo esperado. Consulte la [Sección Flujo de servidor a servidor](#the-server-to-server-flow) para obtener más información sobre cómo hacerlo
1. Revocar el certificado antiguo. Para ello, seleccione los tres puntos (**...**) a la derecha del certificado y presionando **Revocar**:

   ![Revocar certificado](/help/implementing/developing/introduction/assets/s2s-revokecert.png)

   A continuación, confirme la revocación en el siguiente mensaje pulsando la tecla **Revocar** botón:

   ![Revocar confirmación de certificado](/help/implementing/developing/introduction/assets/s2s-revokecertificateconfirmation.png)

1. Finalmente, elimine el certificado comprometido.
