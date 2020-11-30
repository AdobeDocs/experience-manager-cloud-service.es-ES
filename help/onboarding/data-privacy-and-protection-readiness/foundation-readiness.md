---
title: 'Regulaciones de protección de datos y privacidad de datos: Adobe Experience Manager como Cloud Service de preparación para bases'
description: 'Obtenga información sobre la compatibilidad de Adobe Experience Manager como Cloud Service Foundation con las diversas normas de protección de datos y privacidad de datos; incluyendo el Reglamento General de Protección de Datos de la UE (RGPD), la Ley de Privacidad del Consumidor de California y cómo cumplir con la implementación de un nuevo AEM como proyecto Cloud Service. '
translation-type: tm+mt
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 5%

---


# Adobe Experience Manager como Cloud Service está preparado para la protección de datos y las normas de privacidad de datos {#aem-foundation-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>El contenido del presente documento no constituye asesoramiento jurídico y no sustituye al asesoramiento jurídico.
>
>Consulte con el departamento legal de su compañía para obtener asesoramiento sobre las normas de protección de datos y privacidad de datos.

>[!NOTE]
>
>Para obtener más información sobre la respuesta del Adobe a los problemas de privacidad y lo que esto significa para usted como cliente de Adobe, consulte el Centro de privacidad del [Adobe](https://www.adobe.com/privacy.html).

## Soporte de protección y privacidad de datos de AEM Foundation {#aem-foundation-data-privacy-and-protection-support}

En el nivel de base de AEM, los datos personales almacenados se conservan en el Perfil del usuario. Por lo tanto, la información de este artículo trata principalmente de cómo acceder y eliminar perfiles de usuario, para abordar las solicitudes de acceso y eliminación respectivamente.

## Acceso a un Perfil de usuario {#accessing-a-user-profile}

### Pasos manuales {#manual-steps}

1. Abra la consola Administración de usuarios, navegando hasta **[!UICONTROL Herramientas - Seguridad - Usuarios]** o navegando directamente a `https://<serveraddress>:<serverport>/security/users.html`

<!--
   ![useradmin2](assets/useradmin2.png)
-->

1. A continuación, busque el usuario en cuestión escribiendo el nombre en la barra de búsqueda situada en la parte superior de la página:

   ![buscar cuenta](assets/dpp-foundation-01.png)

1. Finalmente, abra el perfil del usuario haciendo clic en él y, a continuación, marque la casilla de verificación en la ficha **[!UICONTROL Detalles]** .

   ![perfil del usuario](assets/dpp-foundation-02.png)

### HTTP API {#http-api}

Como ya se ha mencionado, Adobe proporciona API para acceder a los datos de usuario, con el fin de facilitar la automatización. Existen varios tipos de API que puede utilizar:

**API UserProperties**

```shell
curl -u user:password http://localhost:4502/libs/granite/security/search/profile.userproperties.json\?authId\=cavery
```

**Sling API**

**Descubriendo la página principal del usuario:**

```xml
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

**Recuperando datos de usuario:**

Utilizando la ruta de nodo de la propiedad home de la carga útil JSON devuelta por el comando anterior:

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile.-1.json'
```

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profiles.-1.json'
```

## Desactivación de un usuario y eliminación de los Perfiles asociados {#disabling-a-user-and-deleting-the-associated-profiles}

### Deshabilitar usuario {#disable-user}

1. Abra la consola Administración de usuarios y busque el usuario en cuestión, tal como se describe más arriba.
2. Pase el ratón sobre el usuario y haga clic en el icono de selección. El perfil se pondrá gris para indicar que está seleccionado.

3. Pulse el botón **Deshabilitar** en el menú superior para deshabilitar el usuario:

   ![deshabilitar cuenta](assets/dpp-foundation-03.png)

4. Finalmente, confirme la acción.

   A continuación, la interfaz de usuario indicará que la cuenta de usuario se ha desactivado al atenuar y agregar un candado a la tarjeta de perfil:

   ![cuenta deshabilitada](assets/dpp-foundation-04.png)

### Eliminar información de Perfil de usuario {#delete-user-profile-information}

>[!NOTE]
>
>Para AEM como Cloud Service no hay ningún procedimiento manual disponible en la interfaz de usuario para la eliminación de un perfil de usuario, ya que no se puede acceder a CRXDE.

### HTTP API {#http-api-1}

Los siguientes procedimientos utilizan la herramienta de línea de comandos `curl` para ilustrar cómo deshabilitar al usuario con la  **[!UICONTROL captura]** `userId` y eliminación de sus perfiles disponibles en la ubicación predeterminada.

**Descubriendo la página principal del usuario:**

```shell
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

**Desactivación del usuario:**

Utilizando la ruta de nodo de la propiedad home de la carga útil JSON devuelta por el comando anterior:

```shell
curl -X POST -u user:password -FdisableUser="describe the reasons for disabling this user (Data Privacy in this case)" 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN.rw.userprops.html'
```

**Eliminación de perfiles de usuario**

Utilizando la ruta de acceso del nodo de la propiedad home de la carga útil JSON devuelta por el comando de detección de cuentas y las ubicaciones de nodos de perfil conocidas fuera de la caja:

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```
