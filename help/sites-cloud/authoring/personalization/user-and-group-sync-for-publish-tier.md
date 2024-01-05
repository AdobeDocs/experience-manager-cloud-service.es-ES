---
title: Registro, inicio de sesión y perfil de usuario
description: Obtenga información sobre el registro, el inicio de sesión, los datos de usuario y la sincronización de grupos para AEM as a Cloud Service
exl-id: a991e710-a974-419f-8709-ad86c333dbf8
source-git-commit: ecf4c06fd290d250c14386b3135250633b26c910
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 90%

---

# Registro, inicio de sesión y perfil de usuario {#registration-login-and-userprofile}

## Introducción {#introduction}

Las aplicaciones web a menudo proporcionan funciones de administración de cuentas para que los usuarios finales se registren en un sitio web, lo que mantiene su información de datos de usuario, permitiéndoles iniciar sesión en el futuro y disfrutar de una experiencia coherente. Este artículo describe los siguientes conceptos de AEM as a Cloud Service:

* Registro
* Inicio de sesión
* Almacenamiento de datos de perfil del usuario
* Miembros del grupo
* Sincronización de datos

>[!IMPORTANT]
>
>Para que la funcionalidad descrita en este artículo funcione, debe habilitarse la función Sincronización de datos del usuario, que en este momento requiere una solicitud al servicio de atención al cliente indicando el programa y los entornos adecuados. Si no está habilitada, la información del usuario se mantiene durante un breve período (de 1 a 24 horas) antes de desaparecer.

## Registro {#registration}

Cuando un usuario final se registra en una aplicación de AEM, se crea una cuenta de usuario en el servicio AEM Publish, como se refleja en un recurso de usuario en `/home/users` en el repositorio JCR.

A continuación se describen dos métodos para la aplicación del registro.

### Gestionado por AEM {#aem-managed-registration}

AEM Se puede escribir un código de registro personalizado que contenga, como mínimo, el nombre de usuario y la contraseña del usuario y que cree un registro de usuario en el que se pueda utilizar para autenticarse durante el inicio de sesión. Los siguientes pasos suelen utilizarse para construir este mecanismo de registro:

1. Mostrar un componente de AEM personalizado que recopila información de registro
1. Tras el envío, se utiliza un usuario de servicio aprovisionado correctamente para lo siguiente:
   1. Verificar que un usuario existente ya no existe utilizando uno de los métodos `findAuthorizables()` de la API de UserManager
   1. Crear un registro de usuario utilizando uno de los métodos `createUser()` de la API de UserManager
   1. Conservar los datos de perfil capturados mediante los métodos `setProperty()` de la Interfaz autorizable 
1. Flujos opcionales, como exigir al usuario que valide su correo electrónico.

### Externo {#external-managed-registration}

En algunos casos, el registro o la creación de usuarios se han producido anteriormente en infraestructura fuera de AEM. En ese caso, el registro de usuario se crea en AEM durante el inicio de sesión.

## Inicio de sesión {#login}

Una vez que un usuario final está registrado en el servicio AEM Publish, estos usuarios pueden iniciar sesión para tener acceso autenticado (mediante mecanismos de autorización de AEM) y datos persistentes y específicos del usuario, como los datos de perfil.

## Implementación {#implementation}

El inicio de sesión se puede implementar con los dos enfoques siguientes:

### Gestionado por AEM {#aem-managed-implementation}

Los clientes pueden escribir sus propios componentes personalizados. Para obtener más información, considere la posibilidad de familiarizarse con lo siguiente:

* El [marco de trabajo de autenticación de Sling](https://sling.apache.org/documentation/the-sling-engine/authentication/authentication-framework.html)
* Y considere [preguntar en la sesión de expertos de la comunidad AEM](https://bit.ly/ATACEFeb15) acerca del inicio de sesión.

### Integración con un proveedor de identidad {#integration-with-an-idp}

Los clientes pueden integrarse con un IdP (proveedor de identidad), que autentica al usuario. Las tecnologías de integración incluyen SAML y OAuth/SSO, como se describe a continuación.

**BASADO EN SAML**

Los clientes pueden utilizar la autenticación basada en SAML a través de su SAML IdP preferido. AEM AEM AEM AEM Cuando se utiliza un IdP con el, el IdP es responsable de autenticar las credenciales del usuario e intermediar la autenticación del usuario con el, crear el registro de usuario en el que es necesario y administrar la pertenencia del usuario al grupo en el que es miembro, tal como se describe en la afirmación de SAML. El IdP es el responsable de la autenticación del usuario con el que es miembro, según se describe en la declaración de.

>[!NOTE]
>
>El IdP solo autentica la autenticación inicial de las credenciales del usuario y las solicitudes posteriores a AEM se realizan mediante una cookie de token de inicio de sesión de AEM, siempre que la cookie esté disponible.

Consulte la documentación para obtener más información sobre [Controlador de autenticación SAML 2.0](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/authentication/saml-2-0.html).

**OAuth/SSO**

Consulte la [documentación de inicio de sesión único (SSO)](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/single-sign-on.html?lang=es) para obtener información sobre cómo usar el servicio del controlador de autenticación SSO de AEM.

La interfaz `com.adobe.granite.auth.oauth.provider` se puede implementar con el proveedor de OAuth que elija.

### Sesiones de persistencia y tokens encapsulados {#sticky-sessions-and-encapsulated-tokens}

AEM as a Cloud Service tiene habilitadas las sesiones de persistencia basadas en cookies, lo que garantiza que un usuario final se enrute al mismo nodo de publicación en cada solicitud. Para aumentar el rendimiento, la función de token encapsulado está habilitada de forma predeterminada, por lo que no es necesario hacer referencia al registro de usuario en el repositorio en cada solicitud. Si se reemplaza el nodo de publicación al que un usuario final tiene afinidad, su registro de ID de usuario está disponible en el nuevo nodo de publicación, tal como se describe en la sección de sincronización de datos a continuación.

## Perfil de usuario {#user-profile}

Existen diversos enfoques para la persistencia de los datos, según la naturaleza de esos datos.

### Repositorio de AEM {#aem-repository}

La información de perfil del usuario se puede escribir y leer de dos maneras:

* Usando el lado del servidor con la Interfaz `com.adobe.granite.security.user` interfaz UserPropertiesManager, que colocará los datos bajo el nodo del usuario en `/home/users`. Asegúrese de que las páginas que son únicas por usuario no se almacenen en caché.
* Usando el lado del cliente mediante ContextHub, tal como lo describe [la documentación](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/personalization/contexthub.html#personalization).

### Almacenes de datos de terceros {#third-party-data-stores}

Los datos del usuario final se pueden enviar a proveedores de terceros como CRM, recuperar mediante API al iniciar sesión en AEM y conservarlos (o actualizarlos) en el nodo de perfil del usuario de AEM. AEM los puede utilizar según sea necesario.

El acceso en tiempo real a servicios de terceros para recuperar atributos de perfil es posible, pero es importante asegurarse de que esto no afecte sustancialmente al procesamiento de solicitudes en AEM.

## Permisos (grupos de usuarios cerrados) {#permissions-closed-user-groups}

Las políticas de acceso del nivel de publicación, también denominadas Grupos de usuarios cerrados (CUG), se definen en el autor de AEM como [se describe aquí](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/cug.html#applying-your-closed-user-group-to-content-pages). Para restringir ciertas secciones o páginas de un sitio web a algunos usuarios, aplique los CUG según sea necesario utilizando el autor de AEM, como se describe aquí, y duplíquelos en el nivel de publicación.

* Si los usuarios inician sesión al autenticarse con un proveedor de identidad (IdP) mediante SAML, el controlador de autenticación identificará las pertenencias de grupo del usuario (que deben coincidir con los CUG en el nivel de publicación) y persistirá la asociación entre el usuario y el grupo a través de un registro de repositorio.
* Si el inicio de sesión se realiza sin integración de IdP, el código personalizado puede aplicar las mismas relaciones de estructura de repositorios.

Independientemente del inicio de sesión, el código personalizado también puede persistir y administrar las pertenencias de grupo de un usuario según los requisitos únicos de la organización.

## Sincronización de datos {#data-synchronization}

Los usuarios finales de sitios web esperan una experiencia coherente en cada solicitud de página web o incluso cuando inician sesión con un explorador diferente, aunque no sean conscientes de que se los lleva a diferentes nodos de servidor de la infraestructura del nivel de publicación. AEM El as a Cloud Service lo consigue sincronizando rápidamente el `/home` jerarquía de carpetas (información de perfil de usuario, pertenencia a grupos, etc.) en todos los nodos del nivel de publicación.

A diferencia de otras soluciones de AEM, la sincronización de usuarios y la pertenencia a grupos en AEM as a Cloud Service no utiliza un enfoque de mensajería de extremo a extremo, sino que implementa un enfoque de publicación-suscripción que no requiere la configuración del cliente.

>[!NOTE]
>
>De forma predeterminada, la sincronización de perfiles de usuario y la pertenencia a grupos no está habilitada y, por lo tanto, los datos no se sincronizarán y ni siquiera persistirán de forma permanente en el nivel de publicación. Para habilitar la función, envíe una solicitud al Servicio de atención al cliente indicando el programa y los entornos adecuados.

## Consideraciones de caché {#cache-considerations}

Las solicitudes HTTP autenticadas pueden ser difíciles de almacenar en caché tanto en la red de distribución de contenido (CDN) como en Dispatcher, ya que pueden transferir el estado específico del usuario como parte de la respuesta de la solicitud. Almacenar en caché solicitudes autenticadas de forma involuntaria y enviarlas a otros navegadores solicitantes puede dar como resultado experiencias incorrectas, o incluso perder datos de usuarios o protegidos.

Los métodos para mantener una alta capacidad de caché de las solicitudes mientras se admiten respuestas específicas del usuario incluyen las siguientes:

* Permisos de almacenamiento en caché confidencial de AEM Dispatcher
* Sling Dynamic Include
* AEM ContextHub
