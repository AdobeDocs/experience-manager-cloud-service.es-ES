---
title: 'Registro, inicio de sesión y perfil de usuario '
description: Obtenga información sobre Registro, Inicio de sesión, Datos de usuario y Sincronización de grupos para AEM as a Cloud Service
exl-id: a991e710-a974-419f-8709-ad86c333dbf8
source-git-commit: c49a70b4048acc4e925c69b7ebbedbf8779bbbc0
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 1%

---

# Registro, inicio de sesión y perfil de usuario {#registration-login-and-userprofile}

## Introducción {#introduction}

Las aplicaciones web a menudo proporcionan funciones de administración de cuentas para que los usuarios finales se registren en un sitio web, lo que persiste en su información de datos de usuario, lo que les permite iniciar sesión en el futuro y disfrutar de una experiencia coherente. Este artículo describe los siguientes conceptos para AEM as a Cloud Service:

* Registro
* Inicio de sesión
* Almacenamiento de datos de perfil de usuario
* Pertenencia a grupos
* Sincronización de datos

>[!IMPORTANT]
>
>Para que funcione la funcionalidad descrita en este artículo, debe habilitarse la función Sincronización de datos de usuario , que en este momento requiere una solicitud al servicio de atención al cliente indicando el programa y los entornos adecuados. Si no está habilitada, la información del usuario se mantendrá durante un breve periodo (de 1 a 24 horas) antes de desaparecer.

## Registro {#registration}

Cuando un usuario final se registra para una cuenta en una aplicación AEM, se crea una cuenta de usuario en el servicio AEM Publish, como se refleja en un recurso de usuario en `/home/users` en el repositorio JCR.

A continuación se describen dos métodos para la aplicación del registro.

### AEM administrado {#aem-managed-registration}

Se puede escribir un código de registro personalizado que contenga, como mínimo, el nombre de usuario y la contraseña del usuario final y que cree un registro de usuario en AEM que se pueda utilizar para autenticarse durante el inicio de sesión. Los siguientes pasos suelen utilizarse para construir este mecanismo de registro:

1. Mostrar un componente de AEM personalizado que recopila información de registro
1. Tras el envío, se utiliza un usuario de servicio aprovisionado correctamente para
   1. Compruebe que un usuario existente no existe ya, utilizando una de las API de UserManager `findAuthorizables()` métodos
   1. Cree un registro de usuario utilizando una de las API de UserManager `createUser()` métodos
   1. Conservar los datos de perfil capturados mediante el informe de `setProperty()` métodos
1. Flujos opcionales, como exigir al usuario que valide su correo electrónico.

### Externo {#external-managed-registration}

En algunos casos, el registro o la creación de usuarios se han producido anteriormente en infraestructura fuera de AEM. En ese escenario, el registro de usuario se crea en AEM durante el inicio de sesión.

## Inicio de sesión {#login}

Una vez que un usuario final está registrado en el servicio AEM Publish, estos usuarios pueden iniciar sesión para tener acceso autenticado (mediante mecanismos de autorización de AEM) y datos persistentes y específicos del usuario, como datos de perfil.

## Implementación {#implementation}

El inicio de sesión se puede implementar con los dos enfoques siguientes:

### AEM administrado {#aem-managed-implementation}

Los clientes pueden escribir sus propios componentes personalizados. Para obtener más información, considere la posibilidad de familiarizarse con:

* La variable [Marco de autenticación de Sling](https://sling.apache.org/documentation/the-sling-engine/authentication/authentication-framework.html)
* Y considere [pregunta sobre la sesión de expertos de la comunidad AEM](http://bit.ly/ATACEFeb15) acerca del inicio de sesión.

### Integración con un proveedor de identidad {#integration-with-an-idp}

Los clientes pueden integrarse con un IdP (proveedor de identidad), que autentica al usuario. Las tecnologías de integración incluyen SAML y OAuth/SSO, como se describe a continuación.

**BASADO EN SAML**

Los clientes pueden utilizar la autenticación basada en SAML a través de su SAML IdP preferido. Cuando se utiliza un IdP con AEM, el IdP es responsable de autenticar las credenciales del usuario final e intermediar la autenticación del usuario con AEM, crear el registro de usuario en AEM según sea necesario y administrar la pertenencia al grupo del usuario en AEM, como se describe en la afirmación de SAML.

>[!NOTE]
>
>Solo el IdP autentica la autenticación inicial de las credenciales del usuario y las solicitudes posteriores a AEM se realizan mediante una cookie de token de inicio de sesión AEM, siempre que la cookie esté disponible.

Consulte la documentación para obtener más información sobre [Gestor de autenticación SAML 2.0](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/authentication/saml-2-0.html).

**OAuth/SSO**

Consulte la [Documentación del inicio de sesión único (SSO)](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/single-sign-on.html) para obtener información sobre el uso de AEM servicio del gestor de autenticación SSO.

La variable `com.adobe.granite.auth.oauth.provider` La interfaz de se puede implementar con el proveedor de OAuth que elija.

### Sesiones adhesivas y tokens encapsulados {#sticky-sessions-and-encapsulated-tokens}

AEM as a Cloud Service tiene habilitadas las sesiones adhesivas basadas en cookies, lo que garantiza que un usuario final se enrute al mismo nodo de publicación en cada solicitud. Para aumentar el rendimiento, la función de token encapsulado está habilitada de forma predeterminada, por lo que no es necesario hacer referencia al registro de usuario en el repositorio en cada solicitud. Si se reemplaza el nodo de publicación al que un usuario final tiene afinidad, su registro de id de usuario estará disponible en el nuevo nodo de publicación, tal como se describe en la sección de sincronización de datos a continuación.

## Perfil de usuario {#user-profile}

Existen diversos enfoques para la persistencia de los datos, según la naturaleza de esos datos.

### Repositorio AEM {#aem-repository}

La información del perfil del usuario se puede escribir y leer de dos maneras:

* Uso del lado del servidor con la variable `com.adobe.granite.security.user` Interfaz UserPropertiesManager , que colocará los datos bajo el nodo del usuario en `/home/users`. Asegúrese de que las páginas que son únicas por usuario no se almacenen en caché.
* Lado del cliente mediante ContextHub, tal como lo describe [la documentación](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/personalization/contexthub.html?lang=en#personalization).

### Almacenes de datos de terceros {#third-party-data-stores}

Los datos del usuario final se pueden enviar a proveedores de terceros, como CRM, y recuperar mediante API al iniciar sesión el usuario para AEM y conservarlos (o actualizarlos) en el nodo de perfil del usuario de AEM, y los puede utilizar AEM según sea necesario.

El acceso en tiempo real a servicios de terceros para recuperar atributos de perfil es posible, pero es importante asegurarse de que esto no afecte sustancialmente al procesamiento de solicitudes en AEM.

## Permisos (grupos de usuarios cerrados) {#permissions-closed-user-groups}

Las políticas de acceso del nivel de publicación, también denominadas Grupos de usuarios cerrados (CUG), se definen en el AEM autor como [aquí](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/cug.html?lang=en#applying-your-closed-user-group-to-content-pages). Para restringir ciertas secciones o páginas de un sitio web de algunos usuarios, aplique los CUG según sea necesario utilizando el autor de AEM, como se describe aquí, y duplique en el nivel de publicación.

* Si los usuarios inician sesión al autenticarse con un proveedor de identidad (IdP) mediante SAML, el controlador de autenticación identificará las pertenencias de grupo del usuario (que deben coincidir con los CUG en el nivel de publicación) y persistirá la asociación entre el usuario y el grupo a través de un registro de repositorio
* Si el inicio de sesión se realiza sin integración con IdP, el código personalizado puede aplicar las mismas relaciones de estructura de repositorios.

Independientemente del inicio de sesión, el código personalizado también puede mantener y administrar las pertenencias de grupo de un usuario según los requisitos únicos de la organización.

## Sincronización de datos {#data-synchronization}

Los usuarios finales de sitios web esperan una experiencia coherente en cada solicitud de página web o incluso cuando inician sesión con un explorador diferente, aunque no sepan, se los lleva a diferentes nodos de servidor de la infraestructura del nivel de publicación. AEM as a Cloud Service lo consigue sincronizando rápidamente el `/home` jerarquía de carpetas (información de perfil de usuario, pertenencia a grupos, etc.) en todos los nodos del nivel de publicación.

A diferencia de otras soluciones AEM, la sincronización de la pertenencia de usuarios y grupos en AEM as a Cloud Service no utiliza un enfoque de mensajería punto a punto, sino que implementa un enfoque de suscripción de publicación que no requiere la configuración del cliente.

>[!NOTE]
>
>De forma predeterminada, la sincronización de perfiles de usuario y pertenencia a grupos no está habilitada y, por lo tanto, los datos no se sincronizarán con el nivel de publicación, ni siquiera se mantendrán de forma permanente. Para habilitar la función, envíe una solicitud al Servicio de atención al cliente indicando el programa y los entornos adecuados.

## Consideraciones de caché {#cache-considerations}

Las solicitudes HTTP autenticadas pueden ser difíciles de almacenar en caché tanto en la CDN como en Dispatcher, ya que pueden transferir el estado específico del usuario como parte de la respuesta de la solicitud. Almacenar en caché de forma involuntaria solicitudes autenticadas y enviarlas a otros navegadores solicitantes puede dar como resultado experiencias incorrectas, o incluso perder datos de usuarios o protegidos.

Los métodos para mantener una alta capacidad de caché de las solicitudes mientras se admiten respuestas específicas del usuario incluyen:

* AEM caché confidencial de permisos de Dispatcher
* Sling Dynamic Include
* AEM ContextHub
