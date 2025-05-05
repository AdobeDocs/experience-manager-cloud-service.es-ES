---
title: Propiedades del selector de fragmentos de contenido de Micro-FrontEnd para Adobe Experience Manager as a Cloud Service
description: Propiedades para configurar el Selector de fragmentos de contenido de Micro-FrontEnd para buscar, buscar y recuperar fragmentos de contenido de la aplicación.
role: Admin, User
exl-id: c81b5256-09fb-41ce-9581-f6d1ad316ca4
source-git-commit: a3d8961b6006903c42d983c82debb63ce8abe9ad
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 3%

---

# Selector de fragmentos de contenido: propiedades relacionadas {#content-fragment-selector-related-properties}

El Selector de fragmentos de contenido de Micro-FrontEnd le permite examinar o buscar fragmentos de contenido en el repositorio y utilizarlos en la aplicación.

Puede utilizar las siguientes propiedades para personalizar cómo se procesa el Selector de fragmentos de contenido y cómo se puede utilizar:

## Propiedades del selector de fragmentos de contenido {#content-fragment-selector-properties}

| Propiedad | Tipo | Requerido | Predeterminado | Descripción |
|--- |--- |--- |--- |--- |
| `imsToken` | cadena | No | | Token de IMS utilizado para la autenticación. |
| `repoId` | cadena | No | | ID del repositorio utilizado para la autenticación. |
| `orgId` | cadena | Sí | | ID de organización utilizado para la autenticación. |
| `locale` | cadena | No | | Datos de configuración regional. |
| `env` | Entorno | No | | Entorno de implementación del Selector de fragmentos de contenido. |
| `filters` | FragmentFilter | No | | Filtros que se aplicarán a la lista de fragmentos de contenido. De forma predeterminada, se mostrarán los fragmentos de `/content/dam`. Valor predeterminado: `{ folder: "/content/dam" }` |
| `isOpen` | booleano | Sí | `false` | Marcar como déclencheur para abrir o cerrar el selector. |
| `onDismiss` | () => void | Sí | | Función a la que se llamará cuando se seleccione **Dismiss**. |
| `onSubmit` | ({ contentFragments: `{id: string, path: string}[]`, domainNames: `string[]` }) => void | Sí | | Función a la que se llamará cuando se use **Select** después de seleccionar uno o más fragmentos de contenido. <br><br>La función recibirá:<br><ul><li> Seleccionar los fragmentos de contenido seleccionados con `id` y `path` campos</li><li>y nombres de dominio relacionados con el id de programa y el id de entorno del repositorio, que tienen el estado `ready` y la publicación `tier`</li></ul><br>Si no hay nombres de dominio, se utilizará la instancia de publicación como dominio de reserva. |
| `theme` | &quot;claro&quot; u &quot;oscuro&quot; | No | | Tema del selector de fragmentos de contenido. El tema predeterminado se establece en el tema del entorno UnifiedShell. |
| `selectionType` | &quot;single&quot; o &quot;multiple&quot; | No | `single` | Tipo de selección que se puede utilizar para restringir la selección de FragmentSelector. |
| `dialogSize` | &quot;fullscreen&quot; o &quot;fullscreenTakeover&quot; | No | `fullscreen` | Propiedad opcional para controlar el tamaño del diálogo. |
| `waitForImsToken` | booleano | No | `false` | Indica si el selector de fragmentos de contenido se representa en el contexto del flujo SUSI y debe esperar a que `imsToken` esté listo. |
| `imsAuthInfo` | ImsAuthInfo | No | | Objeto que contiene la información de autenticación IMS del usuario que ha iniciado sesión. |
| `runningInUnifiedShell` | booleano | No | | Indica si el Selector de fragmentos de contenido se está ejecutando en UnifiedShell o de forma independiente. |
| `readonlyFilters` | ResourceReadonlyFiltersField | No | | Filtros de solo lectura que se pueden aplicar a la lista de contenido y que no se pueden eliminar. |

## Propiedades De ImsAuthProps {#imsauthprops-properties}

Las propiedades de `ImsAuthProps` definen la información de autenticación y el flujo que utiliza el Selector de fragmentos de contenido para obtener un `imsToken`. Al establecer estas propiedades, puede controlar cómo debe comportarse el flujo de autenticación y registrar los agentes de escucha para varios eventos de autenticación.

| Nombre de la propiedad | Descripción |
|--- |--- |
| `imsClientId` | Valor de cadena que representa el ID de cliente de IMS utilizado con fines de autenticación. Este valor lo proporciona Adobe y es específico de su organización de Adobe AEM CS. |
| `imsScope` | Describe los ámbitos utilizados en la autenticación. Los ámbitos determinan el nivel de acceso que la aplicación tiene a los recursos de su organización. Los ámbitos múltiples se pueden separar con comas. |
| `redirectUrl` | Representa la dirección URL a la que se redirige al usuario después de la autenticación. Este valor se suele establecer en la dirección URL actual de la aplicación. Si no se proporciona `redirectUrl`, `ImsAuthService` usará la redirectUrl utilizada para registrar `imsClientId` |
| `modalMode` | Un booleano que indica si el flujo de autenticación debe mostrarse en un modal (emergente) o no. Si se establece en `true`, el flujo de autenticación se mostrará en una ventana emergente. Si se establece en `false`, el flujo de autenticación se mostrará en una recarga de página completa.<br>**Nota:** para una mejor experiencia de usuario, puede controlar dinámicamente este valor si el usuario tiene deshabilitada la ventana emergente del explorador. |
| `onImsServiceInitialized` | Una función de llamada de retorno que se llama cuando se inicializa el servicio de autenticación IMS de Adobe. Esta función toma un parámetro, `service`, que es un objeto que representa el servicio IMS de Adobe. Consulte [`ImsAuthService`](#imsauthservice-ims-auth-service) para obtener más detalles. |
| `onAccessTokenReceived` | Una función de llamada de retorno que se llama cuando se recibe un `imsToken` del servicio de autenticación IMS de Adobe. Esta función toma un parámetro, `imsToken`, que es una cadena que representa el token de acceso. |
| `onAccessTokenExpired` | Función de llamada de retorno a la que se llama cuando ha caducado un token de acceso. Esta función se utiliza generalmente para almacenar en déclencheur un nuevo flujo de autenticación para obtener un nuevo token de acceso. |
| `onErrorReceived` | Función de llamada de retorno a la que se llama cuando se produce un error durante la autenticación. Esta función toma dos parámetros: el tipo de error y el mensaje de error. El tipo de error es una cadena que representa el tipo de error y el mensaje de error es una cadena que representa el mensaje de error. |

## Propiedades De ImsAuthService {#imsauthservice-properties}

La clase `ImsAuthService` administra el flujo de autenticación para el Selector de fragmentos de contenido. Es responsable de obtener un `imsToken` del servicio de autenticación IMS de Adobe. `imsToken` se usa para autenticar al usuario y autorizar el acceso al repositorio de Adobe Experience Manager (AEM) CS. ImsAuthService usa las propiedades `ImsAuthProps` para controlar el flujo de autenticación y registrar agentes de escucha para varios eventos de autenticación. Puede utilizar la práctica función `registerContentFragmentSelectorAuthService` para registrar la instancia `ImsAuthService` con el Selector de fragmentos de contenido. Las funciones siguientes están disponibles en la clase `ImsAuthService`. Sin embargo, si está utilizando la función `registerContentFragmentSelectorAuthService`, no necesita llamar a estas funciones directamente.

| Nombre de función | Descripción |
|--- |--- |
| `isSignedInUser` | Determina si el usuario ha iniciado sesión en el servicio y devuelve un valor booleano en consecuencia. |
| `getImsToken` | Recupera la autenticación `imsToken` del usuario que ha iniciado sesión actualmente, que se puede usar para autenticar solicitudes en otros servicios como la generación de la representación del recurso _2&rbrace;._ |
| `signIn` | Inicia el proceso de inicio de sesión del usuario. Esta función utiliza `ImsAuthProps` para mostrar la autenticación en una ventana emergente o en una recarga de página completa. |
| `signOut` | Cierra la sesión del usuario del servicio, invalidando su token de autenticación y obligándole a iniciar sesión de nuevo para acceder a los recursos protegidos. Al invocar esta función, se volverá a cargar la página actual. |
| `refreshToken` | Actualiza el token de autenticación del usuario que ha iniciado sesión, lo que evita que caduque y garantiza un acceso ininterrumpido a los recursos protegidos. Devuelve un nuevo token de autenticación que puede utilizarse para solicitudes posteriores. |
