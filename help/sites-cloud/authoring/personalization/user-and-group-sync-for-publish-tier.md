---
title: 'Registro, inicio de sesión y Perfil del usuario '
description: Obtenga información sobre el registro, el inicio de sesión y el Perfil del usuario en el nivel de publicación
translation-type: tm+mt
source-git-commit: 2c00c3723c3c84365044b5cd2fe6779de0360736
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 0%

---


# Registro, inicio de sesión y Perfil del usuario {#registration-login-and-userprofile}

## Introducción {#introduction}

Las aplicaciones web suelen proporcionar funciones de administración de cuentas para que los usuarios finales se registren en un sitio web, lo que persiste en la información de perfil del usuario, lo que les permite iniciar sesión en el futuro y disfrutar de una experiencia coherente. Este artículo describe:

* Registro
* Inicio de sesión
* Almacenamiento de datos de perfil de usuario
* Membresía del grupo
* Sincronización de datos

>[!IMPORTANT]
>
>Para que la funcionalidad descrita en este artículo funcione, debe habilitarse la función de sincronización de datos de usuario, que en este momento requiere una solicitud al servicio de atención al cliente indicando el programa y los entornos adecuados. Si no está habilitada, la información del usuario se mantendrá durante un breve período (de 1 a 24 horas) antes de desaparecer.

## Registro {#registration}

Cuando un usuario final se registra para una cuenta en una aplicación AEM, se crea una cuenta de usuario en el servicio AEM Publish, como se refleja en un recurso de usuario en `/home/users` en el repositorio JCR.

Existen dos métodos para aplicar el registro, que se describen a continuación.

### AEM administrado {#aem-managed-registration}

Se puede escribir un código de registro personalizado que tome, como mínimo, el nombre de usuario y la contraseña del usuario final y cree un registro de usuario en AEM que pueda utilizarse para autenticarse durante el inicio de sesión. Los siguientes pasos suelen utilizarse para construir este mecanismo de registro:

1. Mostrar un componente de AEM personalizado que recopila información de registro
1. Tras el envío, se utiliza un usuario de servicios aprovisionado correctamente para
   1. Verifique que un usuario existente no exista ya, utilizando uno de los métodos `findAuthorizables()` de la API de UserManager
   1. Cree un registro de usuario mediante uno de los métodos `createUser()` de la API de UserManager
   1. Persista cualquier dato de perfil capturado mediante los métodos `setProperty()` de la interfaz Autorizable
1. Flujos opcionales, como exigir al usuario que valide su correo electrónico.

### Externo {#external-managed-registration}

En algunos casos, el registro o la creación de usuarios se ha producido anteriormente en infraestructuras fuera de AEM. En ese escenario, el registro de usuario se crea en AEM durante el inicio de sesión.

## Inicio de sesión {#login}

Una vez que un usuario final está registrado en el servicio AEM Publish, estos usuarios pueden iniciar sesión para tener acceso autenticado (mediante mecanismos de autorización AEM) y datos persistentes específicos del usuario, como datos de perfil.

## Implementación {#implementation}

El inicio de sesión se puede implementar con los dos enfoques siguientes:

### AEM administrado {#aem-managed-implementation}

Los clientes pueden escribir sus propios componentes personalizados. Para obtener más información, considere familiarizarse con:

* El [Módulo de autenticación de Sling](https://sling.apache.org/documentation/the-sling-engine/authentication/authentication-framework.html)
* Y considere [preguntar a la sesión de los expertos de la comunidad AEM](http://bit.ly/ATACEFeb15) acerca del inicio de sesión.

### Integración con un proveedor de identidad {#integration-with-an-idp}

Los clientes pueden integrarse con un IdP (proveedor de identidad) que autentica al usuario. Las tecnologías de integración incluyen SAML y OAuth/SSO, como se describe a continuación.

**BASADO EN SAML**

Los clientes pueden utilizar la autenticación basada en SAML mediante su ID de SAML preferido. Cuando se utiliza un IdP con AEM, el IdP es responsable de autenticar las credenciales del usuario final y de intermediar la autenticación del usuario con AEM, crear el registro de usuario en AEM según sea necesario y administrar la pertenencia al grupo del usuario en AEM, como se describe en la afirmación de SAML.

>[!NOTE]
>
>El IdP sólo autentica la autenticación inicial de las credenciales del usuario y las solicitudes posteriores a AEM se realizan mediante una cookie de autentificador de inicio de sesión AEM, siempre y cuando la cookie esté disponible.

Consulte la documentación para obtener más información sobre el controlador de autenticación [SAML 2.0](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/saml-2-0-authenticationhandler.html?lang=en#saml-authentication-handler).

**OAuth/SSO**

Consulte la documentación de [Inicio de sesión único (SSO)](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/single-sign-on.html) para obtener información sobre cómo utilizar AEM servicio de controlador de autenticación SSO.

La interfaz `com.adobe.granite.auth.oauth.provider` se puede implementar con el proveedor de OAuth de su elección.

### Sesiones adhesivas y tokens encapsulados {#sticky-sessions-and-encapsulated-tokens}

AEM como Cloud Service tiene habilitadas las sesiones adhesivas basadas en cookies, lo que garantiza que un usuario final se dirija al mismo nodo de publicación en cada solicitud. Para aumentar el rendimiento, la función de token encapsulado está habilitada de forma predeterminada, por lo que no es necesario hacer referencia al registro de usuario en el repositorio en cada solicitud. Si se reemplaza el nodo de publicación al que un usuario final tiene una afinidad, su registro de ID de usuario estará disponible en el nuevo nodo de publicación, tal como se describe en la sección de sincronización de datos a continuación.

## Perfil de usuario {#user-profile}

Existen diversos criterios para la persistencia de los datos, según la naturaleza de esos datos.

### Repositorio de AEM {#aem-repository}

La información de perfil del usuario se puede escribir y leer de dos maneras:

* Uso del lado del servidor con la interfaz `com.adobe.granite.security.user` UserPropertiesManager, que coloca los datos bajo el nodo del usuario en `/home/users`. Asegúrese de que las páginas únicas por usuario no se almacenen en la caché.
* Desde el cliente mediante ContextHub, como se describe en [la documentación](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/personalization/contexthub.html?lang=en#personalization).

### Almacenes de datos de terceros {#third-party-data-stores}

Los datos del usuario final pueden enviarse a proveedores de terceros, como CRM, y recuperarse mediante API tras el inicio de sesión del usuario para AEM, persistir (o actualizarse) en el nodo de perfil del usuario AEM y ser utilizados por AEM según sea necesario.

El acceso en tiempo real a servicios de terceros para recuperar atributos de perfil es posible, pero es importante asegurarse de que esto no afecte significativamente al procesamiento de solicitudes en AEM.

## Permisos (grupos de usuarios cerrados) {#permissions-closed-user-groups}

Las directivas de acceso de capa de publicación, también denominadas Grupos de usuarios cerrados (CUG), se definen en el autor del AEM como [descritas aquí](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/cug.html?lang=en#applying-your-closed-user-group-to-content-pages). Para restringir ciertas secciones o páginas de un sitio web de algunos usuarios, aplique los CUG según sea necesario utilizando el autor de AEM, como se describe aquí, y remuéstrelos en el nivel de publicación.

* Si los usuarios inician sesión autenticándose con un proveedor de identidad (IdP) mediante SAML, el controlador de autenticación identificará las pertenencias de grupo del usuario (que deben coincidir con los CUG en el nivel de publicación) y mantendrá la asociación entre el usuario y el grupo a través de un registro de repositorio
* Si el inicio de sesión se realiza sin la integración con IdP, el código personalizado puede aplicar las mismas relaciones de estructura de repositorio.

Independientemente del inicio de sesión, el código personalizado también puede persistir y administrar las pertenencias de grupo de un usuario, según lo requieran los requisitos exclusivos de una organización.

## Sincronización de datos {#data-synchronization}

Los usuarios finales del sitio web esperan una experiencia uniforme en cada solicitud de página web o incluso cuando inician sesión con un navegador diferente, aunque no sepan, se los lleva a diferentes nodos del servidor de la infraestructura del nivel de publicación. AEM como Cloud Service lo logra sincronizando rápidamente la jerarquía de carpetas `/home` (información de perfil de usuario, pertenencia a grupos, etc.) en todos los nodos del nivel de publicación.

A diferencia de otras soluciones AEM, la sincronización de la pertenencia de usuarios y grupos en AEM como Cloud Service no utiliza un enfoque de mensajería punto a punto, sino que implementa un enfoque de suscripción a publicación que no requiere la configuración del cliente.

>[!NOTE]
>
>De forma predeterminada, la sincronización del perfil del usuario y de la pertenencia a grupos no está habilitada y, por tanto, los datos no se sincronizarán ni persistirán permanentemente en el nivel de publicación. Para habilitar la función, envíe una solicitud al servicio de asistencia al cliente indicando el programa y los entornos adecuados.

## Consideraciones de caché {#cache-considerations}

Las solicitudes HTTP autenticadas pueden resultar difíciles de almacenar en caché tanto en CDN como en Dispatcher, ya que pueden transferir un estado específico del usuario como parte de la respuesta de la solicitud. Almacenar en caché de forma involuntaria solicitudes autenticadas y enviarlas a otros exploradores solicitantes puede resultar en experiencias incorrectas o incluso en la pérdida de datos de usuarios o protegidos.

Los métodos para mantener una alta capacidad de caché de las solicitudes y, al mismo tiempo, admitir respuestas específicas del usuario incluyen:

* AEM caché sensible de permisos de despachante
* Sling Dynamic Include
* AEM ContextHub