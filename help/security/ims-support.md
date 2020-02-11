---
title: Compatibilidad con IMS para Adobe Experience Manager como servicio de nube
description: 'Compatibilidad con IMS para Adobe Experience Manager como servicio de nube '
translation-type: tm+mt
source-git-commit: bef17376f0b7de79511f9ad6ceb00e9f084f45d2

---


# Compatibilidad con IMS para Adobe Experience Manager como servicio de nube {#ims-support-for-aem-as-a-cloud-service}

## Introducción {#introduction}

* AEM como servicio de nube incluye compatibilidad con Admin Console para instancias de AEM y autenticación basada en Adobe Identity Management System (IMS para abreviar).
* La Consola de administración permite a los administradores administrar de forma centralizada todos los usuarios de Experience Cloud.
* Los usuarios y grupos pueden asignarse a perfiles de producto asociados a AEM como instancias de Cloud Service, lo que les permite iniciar sesión en esa instancia.

## Puntos destacados de la clave {#key-highlights}

AEM como servicio de nube ofrece compatibilidad con la autenticación IMS solo para usuarios autores, administradores y desarrolladores. No ofrece soporte para usuarios finales externos de sitios de clientes como visitantes del sitio.

* La Consola de administración representará a los clientes como organizaciones de IMS, instancias de autor y publicación en un entorno como instancias de contexto de producto. Esto permitirá a los administradores de sistemas y productos administrar el acceso a las instancias.
* Los perfiles de producto de Admin Console determinarán las instancias a las que puede acceder un usuario.
* Los clientes podrán utilizar sus propios proveedores de identidad (IDP) compatibles con SAML 2 para el inicio de sesión único.
* Solo se admitirán los Enterprise ID o Federated ID para el inicio de sesión único del cliente, no los Adobe ID personales.

## Arquitectura {#architecture}

La autenticación IMS funciona mediante el protocolo OAuth entre AEM y el extremo IMS de Adobe. Una vez que un usuario se ha agregado a IMS y tiene una identidad de Adobe, puede iniciar sesión en el servicio de creación de AEM con las credenciales de IMS.

El flujo de inicio de sesión del usuario se muestra a continuación; el usuario será redirigido a IMS y, opcionalmente, al cliente IDP para SSO y, a continuación, redirigido a AEM.

![Arquitectura IMS](/help/security/assets/ims1.png)

## Cómo configurar {#how-to-set-up}

### Incorporación de organizaciones a Adobe Admin Console {#onboarding-orgs-to-adobe-admin-console}

La incorporación del cliente a Adobe Admin Console es un requisito previo para utilizar Adobe IMS para la autenticación AEM.

Como primer paso, los clientes deben disponer de una organización aprovisionada en Adobe IMS. Los clientes de Adobe Enterprise están representados como organizaciones de IMS en [Adobe Admin Console](https://helpx.adobe.com/enterprise/using/admin-console.html) . Éste es el portal que utilizan los clientes de Adobe para administrar las asignaciones de productos para sus usuarios y grupos.

Los clientes de AEM ya deben disponer de una organización aprovisionada y, como parte del aprovisionamiento de IMS, las instancias de cliente estarán disponibles en Admin Console para administrar los derechos de usuario y el acceso.

Una vez que un cliente existe como una organización de IMS, tendrá que configurar su sistema como se resume a continuación:

![Integración de IMS](/help/security/assets/ims2.png)

1. El administrador del sistema designado recibe una invitación para iniciar sesión en Cloud Manager. Después de iniciar sesión en el administrador de nube, los administradores del sistema pueden optar por aprovisionar los programas y entornos de AEM o navegar a Admin Console para tareas administrativas.
1. El Administrador del sistema reclama un dominio para confirmar la propiedad del dominio respectivo (por ejemplo, acme.com)
1. El administrador del sistema configura los directorios de usuario
1. El Administrador del sistema realiza la configuración de IDP en la Consola de administración para configurar el Registro único.
1. El administrador de AEM administra los grupos locales, los permisos y los privilegios de la forma habitual.

Los conceptos básicos de Adobe Identity Management, incluida la configuración de IDP, se tratan [aquí](https://helpx.adobe.com/enterprise/using/set-up-identity.html).

El uso de Enterprise Administration y Admin Console se trata [aquí](https://helpx.adobe.com/enterprise/managing/user-guide.html).

### Incorporación de usuarios en Admin Console {#onboarding-users-in-admin-console}

Existen tres formas de integrar a los usuarios en función del tamaño del cliente y de sus preferencias: crear usuarios manualmente en Admin Console, cargar un archivo .csv o sincronizar usuarios desde Enterprise Directory del cliente.

**Adición manual a través de la interfaz de usuario de la Consola de administración**

Los usuarios y grupos se pueden crear manualmente en la interfaz de usuario de la Consola de administración. Este método se puede utilizar si no tiene un gran número de usuarios que administrar. Por ejemplo, menos de 50 usuarios de AEM o si ya está utilizando este método para administrar otros productos de Adobe como Analytics, Target o aplicaciones de Creative Cloud.

![Incorporación del usuario](/help/security/assets/ims3.png)

**Carga de archivos en la interfaz de usuario de la Consola de administración**

Para facilitar la gestión de la creación de usuarios, se puede cargar un `.csv` archivo para agregar usuarios de forma masiva.

![Carga de archivo](/help/security/assets/ims4.png)

**Herramienta de sincronización de usuarios**

La Herramienta de sincronización de usuarios (UST en resumen) permite a los clientes de la empresa crear y administrar usuarios de Adobe mediante Active Directory. Esto también funciona para otros servicios de directorio OpenLDAP probados. Los usuarios de destino son administradores de identidad de TI (Enterprise Directory o Administradores del sistema) que podrán instalar y configurar la herramienta. La herramienta de código abierto es personalizable para que los clientes la modifiquen y se adapten a sus propios requisitos particulares.

Cuando se ejecuta la sincronización de usuarios, se obtiene una lista de usuarios de Active Directory de la organización y se compara con la lista de usuarios de Admin Console.  A continuación, llama a la API de administración de usuarios de Adobe para sincronizar la Consola de administración con el directorio de la organización. El flujo de cambios es totalmente unidireccional. Las ediciones realizadas en la Consola de administración no se insertan en el directorio.

La herramienta permite al administrador del sistema asignar grupos de usuarios en el directorio del cliente con la configuración del producto y los grupos de usuarios en Admin Console.

Para configurar la sincronización de usuarios, la organización debe crear un conjunto de credenciales de la misma manera que usaría la API [de administración de](https://www.adobe.io/apis/experienceplatform/umapi-new.html)usuarios.

![Herramienta de sincronización de usuarios](/help/security/assets/ims5.png)

La herramienta de sincronización de usuarios se distribuye a través del repositorio de Adobe Github [en esta ubicación](https://github.com/adobe-apiplatform/user-sync.py/releases/latest).

>[!NOTE]
>
> La versión de evaluación **2.4RC1** está disponible con compatibilidad para la creación de grupos dinámicos y se puede encontrar [aquí](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1).

Las principales características de esta versión son la capacidad de asignar dinámicamente nuevos grupos LDAP para la pertenencia de usuarios a Admin Console, así como la creación dinámica de grupos de usuarios.

Puede encontrar más información sobre las nuevas funciones de grupo [en esta ubicación](https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration.md#additional-group-options).

**Documentación de sincronización de usuarios**

Consulte la documentación [del](https://adobe-apiplatform.github.io/user-sync.py/en/) Departamento del Tesoro para obtener más detalles.

La herramienta de sincronización de usuarios debe registrarse como cliente de Adobe I/O UMAPI mediante el procedimiento [aquí](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html).

La documentación de la consola de Adobe I/O se puede encontrar [aquí](https://www.adobe.io/apis/cloudplatform/console.html).

La API de administración de usuarios que utiliza la herramienta de sincronización de usuarios se trata [aquí](https://www.adobe.io/apis/cloudplatform/umapi-new.html).

## Configuración de Adobe Experience como servicio de nube {#aem-configuration}

> [!NOTE]
>
>La configuración de AEM IMS requerida se configurará automáticamente cuando se aprovisionen los entornos y las instancias de AEM. Sin embargo, el administrador puede modificarla según sus necesidades utilizando el método descrito [aquí](/help/implementing/deploying/overview.md).

La configuración de AEM IMS requerida se configurará automáticamente cuando se aprovisionen los entornos y las instancias de AEM.  Los administradores de clientes pueden modificar parte de la configuración según sus necesidades

El método general consiste en configurar Adobe IMS como proveedor de OAuth. El controlador **Apache Jackrabbit Oak Default Sync Handler** puede modificarse como para la sincronización LDAP.

A continuación se muestran las configuraciones de OSGI clave que deben modificarse para cambiar propiedades como Pertenencia automática del usuario o Asignaciones de grupos.

<!-- Arun to provide list of osgi configs -->

## Usos {#how-to-use}

### Administración de productos y acceso de usuarios en Admin Console {#managing-products-and-user-access-in-admin-console}

Cuando el administrador de productos inicie sesión en Admin Console, verá varias instancias del contexto de producto de los servicios gestionados de AEM, como se muestra a continuación:

![Inicio de sesión en instancias](/help/security/assets/ims6.png)

En este ejemplo, la organización **AEM-MS-Onboard** tiene 32 instancias que abarcan diferentes topologías y entornos como Stage o Prod.

![Inicio de sesión de instancias2](/help/security/assets/ims7.png)

En cada instancia de contexto de producto, habrá perfiles de producto asociados. Estos perfiles de producto se utilizan para asignar acceso a usuarios y grupos con el privilegio requerido.

El perfil **Administrator_xxx** se utilizará para otorgar privilegios de administrador en la instancia de AEM asociada, mientras que el perfil **User_xxx** se utilizará para agregar usuarios habituales.

Los usuarios y grupos agregados bajo este perfil de producto podrán iniciar sesión en esa instancia en particular, como se muestra en el ejemplo siguiente:

![Perfil del producto](/help/security/assets/ims8.png)

### Inicio de sesión en Adobe Experience Manager como servicio de nube (#logging-in-to-aem)

**Inicio de sesión de administrador local**

AEM puede seguir admitiendo inicios de sesión locales para usuarios administradores. La pantalla de inicio de sesión tiene una opción para iniciar sesión localmente:

![Inicio de sesión local](/help/security/assets/ims9.png)

<!-- the above image needs to be updated for skyline -->

**Inicio de sesión basado en IMS**

Para otros usuarios, el inicio de sesión basado en IMS se puede utilizar una vez que IMS esté configurado en la instancia. El usuario primero hará clic en el botón Iniciar sesión con Adobe, como se muestra a continuación:

![Inicio de sesión de IMS](/help/security/assets/ims10.png)

Luego se les redirigirá a la pantalla de inicio de sesión de IMS y deberán introducir sus credenciales:

![Inicio de sesión de IMS2](/help/security/assets/ims11.png)

![Inicio de sesión de IMS3](/help/security/assets/ims12.png)

Si se configura un IDP federado durante la configuración inicial de la Consola de administración, se redirigirá al usuario al IDP del cliente para SSO:

![Inicio de sesión de IMS4](/help/security/assets/ims13.png)

Una vez finalizada la autenticación, se redirigirá al usuario a AEM e iniciará sesión:

![Inicio de sesión de IMS5](/help/security/assets/ims14.png)

### Administración de permisos y ACL en Adobe Experience Manager como servicio de nube {#managing-permissions-in-aem}

Las ACL y los permisos seguirán administrándose en AEM. Los grupos de usuarios sincronizados desde IMS se pueden asignar a grupos locales donde se definen ACL y privilegios.

En el ejemplo siguiente, se agregan grupos sincronizados al grupo local **Dam_Users** como ejemplo.

El usuario forma parte de los siguientes grupos en IMS:

![ACL1](/help/security/assets/ims15.png)

Cuando el usuario inicia sesión, se sincronizan las suscripciones al grupo, como se muestra a continuación:

![ACL2](/help/security/assets/ims16.png)

En AEM, los grupos de usuarios sincronizados con IMS se pueden agregar como miembros a grupos locales existentes, como los usuarios **de** DAM.

![ACL3](/help/security/assets/ims17.png)

Como se muestra a continuación, el grupo **AEM-GRP_008** hereda los permisos y privilegios de los usuarios **de** DAM, es una forma eficaz de administrar los permisos para los grupos sincronizados y se utiliza comúnmente también en el método de autenticación basado en LDAP.

![ACL3](/help/security/assets/ims18.png)