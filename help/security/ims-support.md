---
title: Compatibilidad con IMS para Adobe Experience Manager as a Cloud Service
description: Compatibilidad del sistema de administración de imágenes con Adobe Experience Manager as a Cloud Service
exl-id: fb563dbd-a761-4d83-9da1-58f8e462b383
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1993'
ht-degree: 39%

---

# Compatibilidad con IMS para Adobe Experience Manager as a Cloud Service {#ims-support-for-aem-as-a-cloud-service}

## Introducción {#introduction}

* AEM as a Cloud Service incluye compatibilidad con Admin Console para instancias de AEM y autenticación basada en Adobe Identity Management System (IMS).
* Admin Console permite a los administradores gestionar de forma centralizada todos los usuarios de Experience Cloud.
* AEM Los usuarios y grupos pueden asignarse a perfiles de producto asociados a una instancia as a Cloud Service de la aplicación, lo que les permite iniciar sesión en esa instancia.

>[!TIP]
>
>Consulte [AEM Configuración del acceso a la para administradores](https://experienceleague.adobe.com/?recommended=ExperienceManager-A-1-2020.1.aem&amp;lang=es) AEM para obtener una introducción a cómo se autentican los usuarios con Adobe IMS para que se as a Cloud Service. AEM Además, aprenda cómo se utilizan los usuarios de IMS de Adobe, los grupos de usuarios y los perfiles de producto para controlar el acceso a los usuarios de, así como sus funciones y funcionalidades. Se requiere Adobe ID.

>[!NOTE]
>
>AEM no admite la asignación de grupos a perfiles. Los usuarios deben añadirse individualmente en su lugar.

## Puntos clave destacados {#key-highlights}

AEM El as a Cloud Service ofrece compatibilidad con la autenticación IMS solo para usuarios creadores, administradores y desarrolladores. No ofrece soporte para usuarios finales externos de sitios de clientes como visitantes del sitio.

* El Admin Console representa a los clientes como organizaciones de IMS, instancias de creación y publicación en un entorno como instancias de contexto de producto. Esta representación permite a los administradores de sistemas y productos administrar el acceso a las instancias.
* Los perfiles de producto del Admin Console determinan las instancias a las que puede acceder un usuario.
* Los clientes pueden utilizar sus propios proveedores de identidad (IDP) compatibles con SAML 2 para el inicio de sesión único.
* Solo se admiten los Enterprise ID o Federated ID para el inicio de sesión único del cliente, no los ID de Adobe personal.

## Arquitectura {#architecture}

La autenticación IMS funciona mediante el protocolo OAuth entre AEM y el extremo IMS de Adobe. Una vez que se añade un usuario a IMS y tiene una identidad de Adobe, puede iniciar sesión en el servicio de creación de AEM con las credenciales de IMS.

AEM El flujo de inicio de sesión del usuario se muestra a continuación; se redirige al usuario a IMS y, opcionalmente, al IDP de cliente para SSO y, a continuación, a la dirección de vuelta a la página de inicio de sesión de.

![Arquitectura IMS](/help/security/assets/ims1.png)

## Configuración {#how-to-set-up}

### Incorporación de organizaciones a Adobe Admin Console {#onboarding-orgs-to-adobe-admin-console}

La incorporación del cliente a Adobe Admin Console es un requisito previo para utilizar Adobe IMS para la autenticación de AEM.

Como primer paso, los clientes deben disponer de una organización en Adobe IMS. Los clientes de Adobe Enterprise están representados como organizaciones de IMS en la [Adobe Admin Console](https://helpx.adobe.com/es/enterprise/using/admin-console.html). Esta área es el portal que utilizan los clientes de Adobe para administrar las asignaciones de productos para sus usuarios y grupos.

AEM Los clientes de ya deben tener una organización aprovisionada y, como parte de la provisión de IMS, las instancias de cliente están disponibles en Admin Console para administrar los derechos de usuario y el acceso.

Una vez que un cliente existe como una organización de IMS, debe configurar su sistema como se resume en lo siguiente:

![Integración de IMS](/help/security/assets/ims2.png)

1. El administrador del sistema designado recibe una invitación para iniciar sesión en Cloud Manager. Después de iniciar sesión en Cloud Manager, los administradores del sistema pueden optar por ofrecer los programas y entornos de AEM o navegar a Admin Console para llevar a cabo tareas administrativas.
1. El administrador del sistema reclama un dominio para confirmar la propiedad del dominio en cuestión (por ejemplo, acme.com).
1. El administrador del sistema configura los directorios de usuario.
1. El administrador del sistema realiza la configuración de IDP en el Admin Console para configurar el inicio de sesión único.
1. El administrador de AEM gestiona los grupos locales, los permisos y los privilegios de la forma habitual.

Puede informarse sobre los conceptos básicos de Adobe Identity Management, incluida la configuración de IDP, [aquí](https://helpx.adobe.com/es/enterprise/using/set-up-identity.html).

Puede informarse sobre el uso de Enterprise Administration y Admin Console [aquí](https://helpx.adobe.com/es/enterprise/admin-guide.html).

### Incorporación de usuarios en Admin Console {#onboarding-users-in-admin-console}

Existen tres formas de incorporar usuarios. Cada método depende del tamaño del cliente y de sus preferencias. Puede crear usuarios manualmente en Admin Console, cargar un archivo .csv o sincronizar usuarios desde el Active Directory del cliente.

**Adición manual a través de la interfaz de usuario de Admin Console**

Los usuarios y grupos se pueden crear manualmente en la interfaz de usuario de Admin Console. Este método se puede utilizar si no tiene muchos usuarios que administrar. AEM Por ejemplo, menos de 50 usuarios de, o si ya está utilizando este método para administrar otros productos de Adobe como Analytics, Target o aplicaciones de Creative Cloud.

![Incorporación del usuario](/help/security/assets/ims3.png)

**Carga de archivos en la interfaz de usuario de Admin Console**

Para facilitar la gestión de la creación de usuarios, se puede cargar un archivo `.csv` para agregar usuarios de forma masiva.

![Carga de archivo](/help/security/assets/ims4.png)

**Herramienta de sincronización de usuarios**

La herramienta de sincronización de usuarios (o UST abreviada) permite a los clientes empresariales de Adobe crear y administrar usuarios de Adobe mediante Active Directory. Este UST también funciona para otros servicios de directorio OpenLDAP probados. Los usuarios de destino son administradores de identidad de TI (Enterprise Directory o administradores del sistema) que pueden instalar y configurar la herramienta. La herramienta de código abierto es personalizable para que los clientes la modifiquen y se adapten a sus propios requisitos particulares.

Cuando se ejecuta la sincronización de usuarios, se obtiene una lista de usuarios de Active Directory de la organización y se compara con la lista de usuarios del Admin Console. A continuación, llama a la API de administración de usuarios de Adobe para sincronizar el Admin Console con el directorio de la organización. El flujo de cambios es totalmente unidireccional. Las ediciones realizadas en Admin Console no se insertan en el directorio.

La herramienta permite al administrador del sistema asignar grupos de usuarios en el directorio del cliente con la configuración del producto y los grupos de usuarios en el Admin Console.

Para configurar la sincronización de usuarios, la organización debe crear un conjunto de credenciales de la misma manera que utilizaría el [API de administración de usuarios](https://developer.adobe.com/umapi/).

![Herramienta de sincronización de usuarios](/help/security/assets/ims5.png)

La herramienta de sincronización de usuarios se distribuye a través del repositorio de Adobe de GitHub [en esta ubicación](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.9.0rc2).

>[!NOTE]
>
>La versión de evaluación **2.4RC1** está disponible con compatibilidad para la creación de grupos dinámicos y se puede encontrar [aquí](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1).

Las principales características de esta versión son la capacidad de asignar dinámicamente nuevos grupos LDAP para la pertenencia de usuarios al Admin Console y la creación dinámica de grupos de usuarios.

Puede encontrar más información sobre las nuevas funciones de grupo [en esta ubicación](https://adobe-apiplatform.github.io/user-sync.py/en/user-manual/advanced_configuration.html#additional-group-options).

**Documentación de sincronización de usuarios**

Consulte [Documentación de UST](https://adobe-apiplatform.github.io/user-sync.py/es/) para obtener más información.

La herramienta de sincronización de usuarios debe registrarse como cliente de Adobe Developer UMAPI mediante el procedimiento [aquí](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html).

Puede encontrar la documentación de la consola Adobe Developer [aquí](https://developer.adobe.com/developer-console/).

La API de administración de usuarios que utiliza la herramienta de sincronización de usuarios se explica [aquí](https://adobe-apiplatform.github.io/user-sync.py/es/).

## Configuración de Adobe Experience as a Cloud Service {#aem-configuration}

>[!NOTE]
>
>AEM AEM La configuración de IMS requerida se configura automáticamente cuando se aprovisionan los entornos y las instancias de la. Sin embargo, el administrador puede modificarla según sus necesidades utilizando el método descrito [aquí](/help/implementing/deploying/overview.md).

AEM AEM La configuración de IMS requerida se configura automáticamente cuando se aprovisionan los entornos y las instancias de la. Los administradores de clientes pueden modificar parte de la configuración según sea preciso.

El método general consiste en configurar Adobe IMS como proveedor de OAuth. El **controlador de sincronización predeterminado Apache Jackrabbit Oak** puede modificarse como para la sincronización LDAP.

A continuación se muestran las configuraciones de OSGI clave que deben modificarse para cambiar propiedades como Pertenencia automática del usuario o Asignaciones de grupos.

<!-- Arun to provide list of osgi configs -->

## Usos {#how-to-use}

### Administración de productos y acceso de usuarios en Admin Console {#managing-products-and-user-access-in-admin-console}

Cuando el administrador de productos inicia sesión en el Admin Console AEM de, ve varias instancias del contexto de producto as a Cloud Service de la aplicación, como se muestra a continuación. Por ejemplo, seleccione cualquiera de los productos de la **Información general** página:

![Inicio de sesión en instancias](/help/security/assets/ims6.png)

Verá una lista de instancias existentes:

![Inicio de sesión en instancias 2](/help/security/assets/ims7.png)

En cada instancia de contexto de producto, hay instancias que abarcan los servicios de creación o publicación en los entornos Producción, Ensayo o Desarrollo. Cada instancia está asociada a perfiles de producto o funciones de Cloud Manager. Estos perfiles de producto se utilizan para asignar acceso a usuarios y grupos con los privilegios requeridos.

El **AEM Administradores de_xxx** AEM El perfil de se utiliza para otorgar privilegios de administrador en la instancia de asociada mientras que la variable **AEM Usuarios_xxx** Este perfil se utiliza para añadir usuarios habituales.

Todos los usuarios y grupos agregados bajo este perfil de producto pueden iniciar sesión en esa instancia, como se muestra en el ejemplo siguiente:

![Perfil del producto](/help/security/assets/ims8.png)

>[!WARNING]
>
>No cambie el **AEM Administradores de** nombre del perfil del producto. Cambiar el nombre del **AEM Administradores de** el perfil de producto elimina los derechos de administrador de todos los usuarios asignados a dicho perfil.

### Inicio de sesión en Adobe Experience Manager as a Cloud Service {#logging-in-to-aem}

**Inicio de sesión de administrador local**

AEM puede seguir admitiendo inicios de sesión locales para usuarios que sean administradores. La pantalla de inicio de sesión le permite iniciar sesión localmente:

![Inicio de sesión local](/help/security/assets/ims9.png)

<!-- the above image needs to be updated for skyline -->

**Inicio de sesión basado en IMS**

Para otros usuarios, el inicio de sesión basado en IMS se utiliza después de configurar IMS en la instancia. El usuario hace clic en el botón Iniciar sesión con el Adobe, como se muestra a continuación:

![Inicio de sesión en IMS](/help/security/assets/ims10.png)


>[!NOTE]
>
>Cualquier usuario creado en IMS puede crearse con un Adobe ID o un Federated ID. Si un usuario está configurado con Federated ID, se autentica con el proveedor de identidad de su compañía para iniciar sesión.

Se les redirige a la pantalla de inicio de sesión de IMS y deben introducir sus credenciales:

![Inicio de sesión de IMS 2](/help/security/assets/ims11.png)

![Inicio de sesión de IMS 3](/help/security/assets/ims12.png)

Si se configura un IDP federado durante la configuración inicial del Admin Console, se redirige al usuario al IDP del cliente para SSO:

![Inicio de sesión de IMS 4](/help/security/assets/ims13.png)

AEM Una vez finalizada la autenticación, se redirige al usuario de nuevo a la página de inicio de sesión de y se inicia la sesión con la sesión:

![Inicio de sesión de IMS 5](/help/security/assets/ims14.png)

### Administración de permisos y ACL en Adobe Experience Manager as a Cloud Service {#managing-permissions-in-aem}

AEM Las ACL y los permisos se siguen administrando en los. Los grupos de usuarios sincronizados desde IMS se pueden asignar a grupos locales donde se definen las ACL y los privilegios.

En el ejemplo siguiente, los grupos sincronizados se añaden a la variable local **Dam_Users** grupo como ejemplo.

El usuario forma parte de los siguientes grupos en IMS:

![ACL1](/help/security/assets/ims15.png)

Cuando el usuario inicia sesión, se sincronizan las suscripciones al grupo, como se muestra a continuación:

![ACL2](/help/security/assets/ims16.png)

En AEM, los grupos de usuarios sincronizados con IMS se pueden agregar como miembros a grupos locales existentes, como los **usuarios de DAM**.

![ACL3](/help/security/assets/ims17.png)

Como se muestra a continuación, el grupo **AEM-GRP_008** hereda los permisos y privilegios de **Usuarios de DAM**. Esta herencia es una forma eficaz de administrar permisos para grupos sincronizados y se utiliza comúnmente en el método de autenticación basado en LDAP.

![ACL3](/help/security/assets/ims18.png)


### Acceso a Cloud Manager {#accessing-cloud-manager}

AEM Para poder acceder a Cloud Manager o a entornos en los que está as a Cloud Service, debe estar asignado a Perfiles del producto de Cloud Manager.

Consulte Definiciones de funciones para obtener más información sobre las funciones de los usuarios que rigen la disponibilidad de funciones específicas en Cloud Manager.

>[!NOTE]
>Cloud Manager tiene funciones preconfiguradas con los permisos adecuados. Para obtener más información sobre cada una de las funciones con permisos específicos, tareas preconfiguradas o permisos asociados a cada función, consulte [Permisos basados en funciones](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/requirements/role-based-permissions.html?lang=en).

**Pasos para Añadir un usuario**

1. Añada un usuario a un perfil particular desde una pantalla de usuario existente o desde una pantalla de usuario nueva.

1. También puede agregar un usuario desde la pantalla **Información general**, como se muestra en la figura siguiente.

   ![ACL3](/help/security/assets/ims23.png)

   >[!NOTE]
   >Puede asignar más de un perfil a un usuario, como se muestra en la figura siguiente.

   ![ACL3](/help/security/assets/ims22.png)


1. Una vez agregado al perfil correspondiente, debe poder acceder a los inquilinos respectivos en Cloud Manager a través de [Adobe Experience Cloud](https://my.cloudmanager.adobe.com) utilizando la esquina superior derecha de la interfaz de usuario de.


### Acceder a una instancia en AEM as a Cloud Service {#accessing-instance-cloud-service}

>[!IMPORTANT]
>Se deben completar los pasos mencionados en la sección anterior antes de que se le conceda acceso a una instancia en AEM as a Cloud Service.

AEM Para tener acceso a una instancia de dentro de **Admin Console**, debería ver el Programa de Cloud Manager y los entornos dentro del programa en la lista de productos en la **Admin Console**.

Por ejemplo, en la captura de pantalla siguiente, puede ver dos entornos disponibles, a saber: *dev author* y una *publicar*.

![ACL3](/help/security/assets/ims19.png)

AEM Para obtener acceso a instancias de, el usuario debe agregarse a un grupo del producto de Cloud Service correspondiente.

AEM AEM AEM Cada instancia de autor tiene un perfil de administradores y usuarios de la publicación de la y cada instancia de publicación tiene un perfil de usuarios de la publicación de la. Puede agregar otros perfiles según sea necesario.

Para obtener acceso a nivel de administrador a la instancia de AEM, añada el usuario al Perfil de administradores de AEM para ese producto en particular.
