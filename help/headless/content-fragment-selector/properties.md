---
title: Propiedades del selector de fragmentos de contenido de Micro-FrontEnd para Adobe Experience Manager as a Cloud Service
description: Propiedades para configurar el Selector de fragmentos de contenido de Micro-FrontEnd para buscar, buscar y recuperar fragmentos de contenido de la aplicación.
role: Admin, User
exl-id: c81b5256-09fb-41ce-9581-f6d1ad316ca4
source-git-commit: 58995ae9c29d5a76b3f94de43f2bafecdaf7cf68
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 4%

---

# Selector de fragmentos de contenido: propiedades relacionadas {#content-fragment-selector-related-properties}

El Selector de fragmentos de contenido de Micro-FrontEnd le permite examinar o buscar fragmentos de contenido en el repositorio y utilizarlos en la aplicación.

Puede utilizar las siguientes propiedades para personalizar cómo se procesa el Selector de fragmentos de contenido y cómo se puede utilizar:

## Propiedades del selector de fragmentos de contenido {#content-fragment-selector-properties}

| Propiedad | Tipo | Requerido | Predeterminado | Descripción |
|--- |--- |--- |--- |--- |
| `ref` | FragmentSelectorRef | | | Referencia a la instancia `ContentFragmentSelector`, que permite el acceso a la funcionalidad proporcionada como `reload`. |
| `imsToken` | cadena | No | | Token de IMS utilizado para la autenticación. Si no se proporciona, se iniciará el flujo de inicio de sesión de IMS. |
| `repoId` | cadena | No | | ID del repositorio utilizado para el selector de fragmentos. Cuando se proporciona, el selector se conecta automáticamente al repositorio especificado y la lista desplegable de repositorios está oculta. Si no se proporciona, el usuario puede seleccionar un repositorio de la lista de repositorios disponibles a los que tiene acceso. |
| `defaultRepoId` | cadena | No | | ID del repositorio que se seleccionará de forma predeterminada cuando se muestre el selector de repositorios. Solo se usa cuando no se proporciona `repoId`. Si se establece `repoId`, el selector del repositorio estará oculto y se omitirá este valor. |
| `orgId` | cadena | No | | ID de organización utilizado para la autenticación. Si no se proporciona, el usuario puede seleccionar un repositorio de diferentes organizaciones a las que tiene acceso. Si el usuario no tiene acceso a ningún repositorio u organización, el contenido no se carga. |
| `locale` | cadena | No | &quot;en-US&quot; | Configuración regional. |
| `env` | cadena | No | | Entorno de implementación. Consulte el tipo `Env` para ver los nombres de entorno permitidos. |
| `filters` | FragmentFilter | No | `{ folder: "/content/dam" }` | Filtros que se aplicarán a la lista de fragmentos de contenido. De forma predeterminada, se mostrarán los fragmentos de `/content/dam`. |
| `isOpen` | booleano | No | `false` | Indicador que controla si el selector está abierto o cerrado. |
| `noWrap` | booleano | No | `false` | Determina si el Selector de fragmentos se procesa sin un cuadro de diálogo de ajuste. Cuando se establece en `true`, el selector de fragmentos está incrustado directamente en el contenedor principal. Útil para integrar el selector en diseños o flujos de trabajo personalizados. |
| `onSelectionChange` | ({ contentFragments: `ContentFragmentSelection`, domainName?: `string`, tenantInfo?: `string`, repoId?: `string`, deliveryRepos?: `DeliveryRepository[]` }) => void | No | | Función de llamada de retorno activada cada vez que cambia la selección de fragmentos de contenido. Proporciona los fragmentos, el nombre de dominio, la información de inquilino, el ID de repositorio y los repositorios de envío seleccionados actualmente. |
| `onDismiss` | () => void | No | | Función de llamada de retorno activada cuando se realiza la acción de descartar (por ejemplo, cerrar el selector). |
| `onSubmit` | ({ contentFragments: `ContentFragmentSelection`, domainName?: `string`, tenantInfo?: `string`, repoId?: `string`, deliveryRepos?: `DeliveryRepository[]` }) => void | No | | Función de llamada de retorno activada cuando el usuario confirma su selección. Recibe los fragmentos de contenido, el nombre de dominio, la información del inquilino, el ID de repositorio y los repositorios de envío seleccionados. |
| `theme` | &quot;claro&quot; u &quot;oscuro&quot; | No | | Tema para el selector de fragmentos. De forma predeterminada, se establece en el tema de entorno unifiedShell. |
| `selectionType` | &quot;single&quot; o &quot;multiple&quot; | No | `single` | El tipo de selección se puede utilizar para restringir la selección del Selector de fragmentos. |
| `dialogSize` | &quot;fullscreen&quot; o &quot;fullscreenTakeover&quot; | No | `fullscreen` | Prop opcional para controlar el tamaño del cuadro de diálogo. |
| `runningInUnifiedShell` | booleano | No | | Indica si DestinationSelector se está ejecutando en UnifiedShell o de forma independiente. |
| `readonlyFilters` | ResourceReadonlyFiltersField[] | No | | Filtros de solo lectura aplicados a la lista de fragmentos de contenido. El usuario no puede eliminar estos filtros. |
| `selectedFragments` | ContentFragmentIdentifier[] | No | `[]` | Selección inicial de fragmentos de contenido que se preseleccionarán cuando se abra el selector. |
| `hipaaEnabled` | booleano | No | `false` | Indica si el cumplimiento de HIPAA está habilitado. |
| `inventoryView` | InventoryViewType | No | `table` | Tipo de vista predeterminada de inventario que se utilizará en el selector. |
| `inventoryViewToggleEnabled` | booleano | No | `false` | Indica si la opción de vista de inventario está habilitada, lo que permite al usuario cambiar entre las vistas de tabla y de cuadrícula. |

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
