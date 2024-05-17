---
title: Selector de recursos para [!DNL Adobe Experience Manager] como un [!DNL Cloud Service]
description: Utilice el selector de recursos para buscar y recuperar metadatos y representaciones de recursos dentro de la aplicación.
contentOwner: KK
role: Admin,User
exl-id: 5f962162-ad6f-4888-8b39-bf5632f4f298
source-git-commit: 2ce64892cd5bf414d328a9112c47092b762d3668
workflow-type: tm+mt
source-wordcount: '3908'
ht-degree: 45%

---

# Selector de recursos de Micro-Frontend {#Overview}

El Selector de recursos de Micro-Frontend proporciona una interfaz de usuario que se integra fácilmente con el repositorio de [!DNL Experience Manager Assets] para poder examinar o buscar recursos digitales disponibles en el repositorio y utilizarlos en la experiencia de creación de la aplicación.

La interfaz de usuario de Micro-Frontend está disponible en la experiencia de su aplicación mediante el paquete Selector de recursos. Las actualizaciones del paquete se importan automáticamente y el último Selector de recursos implementado se carga automáticamente en la aplicación.

![Información general](assets/overview.png)

El Selector de recursos ofrece muchas ventajas, como las siguientes:

* Facilidad de integración con cualquiera de las [Adobe](#asset-selector-ims) o [no Adobe](#asset-selector-non-ims) aplicaciones que utilizan la biblioteca JavaScript de Vanilla.
* Son fáciles de mantener, ya que las actualizaciones del paquete del Selector de recursos se implementan automáticamente en el Selector de recursos disponible para su aplicación. No se requieren actualizaciones dentro de la aplicación para cargar las modificaciones más recientes.
* Facilidad de personalización, ya que hay propiedades disponibles que controlan la visualización del Selector de recursos en la aplicación.
* Filtros personalizados, de búsqueda de texto completo y listos para usar para navegar rápidamente a los recursos y utilizarlos en la experiencia de creación.
* Capacidad para cambiar repositorios dentro de una organización IMS para la selección de recursos.
* Capacidad para ordenar recursos por nombre, dimensiones y tamaño y verlos en la vista Lista, Cuadrícula, Galería o Cascada.

<!--Perform the following tasks to integrate and use Asset Selector with your [!DNL Experience Manager Assets] repository:

1. [Install Asset Selector](#installation)
2. [Integrate Asset Selector using Vanilla JS](#integration-using-vanilla-js)
3. [Use Asset Selector](#using-asset-selector)
-->

<!--
## Setting up Asset Selector {#asset-selector-setup}

![Asset Selector set up](assets/asset-selector-prereqs.png)
-->

## Requisitos previos{#prereqs}

Debe asegurarse de que dispone de los siguientes métodos de comunicación:

* La aplicación se está ejecutando en HTTPS.
* La dirección URL de la aplicación está en la lista de permitidos de direcciones URL de redireccionamiento del cliente IMS.
* El flujo de inicio de sesión de IMS se configura y se representa mediante una ventana emergente en el explorador web. Por lo tanto, las ventanas emergentes deben habilitarse o permitirse en el explorador de destino.

Utilice los requisitos previos anteriores si necesita el flujo de trabajo de autenticación IMS del Selector de recursos. Alternativamente, si ya está autenticado con el flujo de trabajo de IMS, puede añadir la información de IMS en su lugar.

>[!IMPORTANT]
>
> Este repositorio está diseñado para servir como documentación suplementaria que describa las API disponibles y ejemplos de uso para la integración del Selector de recursos. Antes de intentar instalar o utilizar el Selector de recursos, asegúrese de que su organización tenga acceso al Selector de recursos como parte del perfil as a Cloud Service de Experience Manager Assets. Si no se ha aprovisionado, no puede integrar ni utilizar estos componentes. Para solicitar el aprovisionamiento, el administrador del programa debe generar un ticket de asistencia marcado como P2 desde Admin Console e incluir la siguiente información:
>
>* Nombres de dominio en los que está alojada la aplicación integradora.
>* Después del aprovisionamiento, su organización recibirá `imsClientId`, `imsScope`, y a `redirectUrl` correspondientes a los entornos solicitados que son esenciales para la configuración del Selector de recursos. Sin estas propiedades válidas, no se pueden ejecutar los pasos de instalación.

## Instalación {#installation}

El Selector de recursos está disponible a través de la CDN de ESM (por ejemplo, [esm.sh](https://esm.sh/)/[skypack](https://www.skypack.dev/)) y [UMD](https://github.com/umdjs/umd) versión.

En navegadores que utilizan la **Versión de UMD** (recomendado):

```
<script src="https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js"></script>

<script>
  const { renderAssetSelector } = PureJSSelectors;
</script>
```

En navegadores con compatibilidad con `import maps` con **Versión de CDN de ESM**:

```
<script type="module">
  import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/@assets/selectors/index.js'
</script>
```

En la federación de módulos Deno/Webpack mediante **Versión de CDN de ESM**:

```
import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/@assets/selectors/index.js'
```

## Integración del Selector de recursos mediante Vanilla JS {#integration-using-vanilla-js}

Puede integrar cualquier [!DNL Adobe] o aplicación sin Adobe con [!DNL Experience Manager Assets] repositorio y seleccione recursos desde la aplicación. Consulte [Integración del Selector de recursos con diversas aplicaciones](#asset-selector-integration-with-apps).

La integración se realiza importando el paquete Selector de recursos y conectándose a los Assets as a Cloud Service mediante la biblioteca JavaScript de Vanilla. Editar un `index.html` o cualquier archivo apropiado dentro de su aplicación para:

* Definición de los detalles de autenticación
* Acceso al repositorio Assets as a Cloud Service
* Configurar las propiedades de visualización del Selector de recursos

Puede realizar la autenticación sin definir algunas de las propiedades de IMS, si:

* Está integrando una aplicación de [!DNL Adobe] en [Unified Shell](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=es).
* Ya ha generado un token de IMS para la autenticación.

## Integración del Selector de recursos con varias aplicaciones {#asset-selector-integration-with-apps}

Puede integrar el Selector de recursos con varias aplicaciones, como:

* [Integrar el Selector de recursos con una [!DNL Adobe] aplicación](#adobe-app-integration-vanilla)
* [Integración del Selector de recursos con una aplicación que no sea de Adobe](#adobe-non-app-integration)

>[!BEGINTABS]

<!--Integration with an Adobe application content starts here-->

>[!TAB Integración con una aplicación de Adobe]

### Requisitos previos{#prereqs-adobe-app}

Utilice los siguientes requisitos previos si integra el Selector de recursos con una [!DNL Adobe] aplicación:

* [Métodos de comunicación](#prereqs)
* imsOrg
* imsToken
* apikey

### Integrar el Selector de recursos con una [!DNL Adobe] aplicación {#adobe-app-integration-vanilla}

En el siguiente ejemplo se muestra el uso del Selector de recursos al ejecutar un [!DNL Adobe] aplicación en Unified Shell o cuando ya tiene `imsToken` generado para la autenticación.

Incluya el paquete Selector de recursos en su código mediante el `script` , como se muestra en _líneas 6-15_ del ejemplo siguiente. Una vez cargado el script, la variable global `PureJSSelectors` está disponible para su uso. Definición del selector de recursos [propiedades](#asset-selector-properties) como se muestra en _líneas 16-23_. El `imsOrg` y `imsToken` ambas propiedades son necesarias para la autenticación en la aplicación de Adobe. La propiedad de `handleSelection` se utiliza para gestionar los recursos seleccionados. Para procesar el Selector de recursos, llame a la función de `renderAssetSelector` como se menciona en _línea 17_. El Selector de recursos se muestra en el elemento contenedor de `<div>`, como se muestra en las _líneas 21 y 22_.

Al seguir estos pasos, puede utilizar el Selector de recursos con su [!DNL Adobe] aplicación.

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
    <title>Asset Selector</title>
    <script src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js"></script>
    <script>
        // get the container element in which we want to render the AssetSelector component
        const container = document.getElementById('asset-selector-container');
        // imsOrg and imsToken are required for authentication in Adobe application
        const assetSelectorProps = {
            imsOrg: 'example-ims@AdobeOrg',
            imsToken: "example-imsToken",
            apiKey: "example-apiKey-associated-with-imsOrg",
            handleSelection: (assets: SelectedAssetType[]) => {},
        };
        // Call the `renderAssetSelector` available in PureJSSelectors globals to render AssetSelector
        PureJSSelectors.renderAssetSelector(container, assetSelectorProps);
    </script>
</head>

<body>
    <div id="asset-selector-container" style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px;">
    </div>
</body>

</html>
```

<!--For detailed example, visit [Asset Selector Code Example](https://github.com/adobe/aem-assets-selectors-mfe-examples).-->

+++**ImsAuthProps**
El `ImsAuthProps` Las propiedades de definen la información de autenticación y el flujo que utiliza el Selector de recursos para obtener una `imsToken`. Al establecer estas propiedades, puede controlar cómo debe comportarse el flujo de autenticación y registrar los agentes de escucha para varios eventos de autenticación.

| Nombre de la propiedad | Descripción |
|---|---|
| `imsClientId` | Valor de cadena que representa el ID de cliente de IMS utilizado con fines de autenticación. Este valor lo proporciona el Adobe y es específico de su organización de Adobe AEM CS. |
| `imsScope` | Describe los ámbitos utilizados en la autenticación. Los ámbitos determinan el nivel de acceso que la aplicación tiene a los recursos de su organización. Los ámbitos múltiples se pueden separar con comas. |
| `redirectUrl` | Representa la dirección URL a la que se redirige al usuario después de la autenticación. Este valor se suele establecer en la dirección URL actual de la aplicación. Si un `redirectUrl` no se proporciona, `ImsAuthService` utiliza la redirectUrl utilizada para registrar el `imsClientId` |
| `modalMode` | Un booleano que indica si el flujo de autenticación debe mostrarse en un modal (emergente) o no. Si se establece en `true`, el flujo de autenticación se muestra en una ventana emergente. Si se establece en `false`, el flujo de autenticación se muestra en una recarga de página completa. _Nota:_ para una mejor experiencia de usuario, puede controlar dinámicamente este valor si el usuario tiene deshabilitadas las ventanas emergentes del explorador. |
| `onImsServiceInitialized` | Una función de llamada de retorno que se llama cuando se inicializa el servicio de autenticación IMS de Adobe. Esta función toma un parámetro, `service`, que es un objeto que representa el servicio IMS de Adobe. Consulte [`ImsAuthService`](#imsauthservice-ims-auth-service) para obtener más información. |
| `onAccessTokenReceived` | Una función de llamada de retorno a la que se llama cuando una función `imsToken` se recibe desde el servicio de autenticación IMS de Adobe. Esta función toma un parámetro, `imsToken`, que es una cadena que representa el token de acceso. |
| `onAccessTokenExpired` | Función de llamada de retorno a la que se llama cuando ha caducado un token de acceso. Esta función se utiliza generalmente para almacenar en déclencheur un nuevo flujo de autenticación para obtener un nuevo token de acceso. |
| `onErrorReceived` | Función de llamada de retorno a la que se llama cuando se produce un error durante la autenticación. Esta función toma dos parámetros: el tipo de error y el mensaje de error. El tipo de error es una cadena que representa el tipo de error y el mensaje de error es una cadena que representa el mensaje de error. |

+++

+++**ImsAuthService**
`ImsAuthService` administra el flujo de autenticación para el Selector de recursos. Es responsable de obtener una `imsToken` del servicio de autenticación IMS de Adobe. El `imsToken` se utiliza para autenticar al usuario y autorizar el acceso a [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] Repositorio de recursos. ImsAuthService utiliza `ImsAuthProps` propiedades para controlar el flujo de autenticación y registrar agentes de escucha para varios eventos de autenticación. Puede usar el conveniente [`registerAssetsSelectorsAuthService`](#purejsselectorsregisterassetsselectorsauthservice) función para registrar el _ImsAuthService_ con el Selector de recursos. Las siguientes funciones están disponibles en la `ImsAuthService` clase. Sin embargo, si utiliza el _registerAssetsSelectorsAuthService_ función, no es necesario llamar a estas funciones directamente.

| Nombre de función | Descripción |
|---|---|
| `isSignedInUser` | Determina si el usuario ha iniciado sesión en el servicio y devuelve un valor booleano en consecuencia. |
| `getImsToken` | Recupera la autenticación `imsToken` para el usuario que ha iniciado sesión, que se puede utilizar para autenticar solicitudes a otros servicios, como la generación de la _representación del recurso. |
| `signIn` | Inicia el proceso de inicio de sesión del usuario. Esta función utiliza el `ImsAuthProps` para mostrar la autenticación en una ventana emergente o en una recarga de página completa |
| `signOut` | Cierra la sesión del usuario del servicio, invalidando su token de autenticación y obligándole a iniciar sesión de nuevo para acceder a los recursos protegidos. Al invocar esta función, se volverá a cargar la página actual. |
| `refreshToken` | Actualiza el token de autenticación del usuario que ha iniciado sesión, lo que evita que caduque y garantiza un acceso ininterrumpido a los recursos protegidos. Devuelve un nuevo token de autenticación que puede utilizarse para solicitudes posteriores. |

+++

+++**Validación con el token de IMS proporcionado**

```
<script>
    const apiToken="<valid IMS token>";
    function handleSelection(selection) {
    console.log("Selected asset: ", selection);
    };
    function renderAssetSelectorInline() {
    console.log("initializing Asset Selector");
    const props = {
    "repositoryId": "delivery-p64502-e544757.adobeaemcloud.com",
    "apiKey": "ngdm_test_client",
    "imsOrg": "<IMS org>",
    "imsToken": apiToken,
    handleSelection,
    hideTreeNav: true
    }
    const container = document.getElementById('asset-selector-container');
    PureJSSelectors.renderAssetSelector(container, props);
    }
    $(document).ready(function() {
    renderAssetSelectorInline();
    });
</script>
```

+++

+++**Registro de llamadas de retorno al servicio IMS**

```
// object `imsProps` to be defined as below 
let imsProps = {
    imsClientId: <IMS Client Id>,
        imsScope: "openid",
        redirectUrl: window.location.href,
        modalMode: true,
        adobeImsOptions: {
            modalSettings: {
            allowOrigin: window.location.origin,
},
        useLocalStorage: true,
},
onImsServiceInitialized: (service) => {
            console.log("onImsServiceInitialized", service);
},
onAccessTokenReceived: (token) => {
            console.log("onAccessTokenReceived", token);
},
onAccessTokenExpired: () => {
            console.log("onAccessTokenError");
// re-trigger sign-in flow
},
onErrorReceived: (type, msg) => {
            console.log("onErrorReceived", type, msg);
},
}
```

+++

<!--Integration with non-Adobe application content starts here-->

>[!TAB Integración con una aplicación que no es de Adobe]

<!--### Integrate Asset Selector with a [!DNL non-Adobe] application {#adobe-non-app-integration}-->

### Requisitos previos {#prereqs-non-adobe-app}

Utilice los siguientes requisitos previos si integra el Selector de recursos con una aplicación que no sea de Adobe:

* [Métodos de comunicación](#prereqs)
* imsClientId
* imsScope
* redirectUrl
* imsOrg
* apikey

El Selector de recursos admite la autenticación en [!DNL Experience Manager Assets] repositorio que utiliza propiedades del sistema Identity Management (IMS) como `imsScope` o `imsClientID` cuando se integra con una aplicación que no es de Adobe.

+++**Configuración del Selector de recursos para una aplicación que no sea de Adobe**
Para configurar el Selector de recursos para una aplicación que no sea de Adobe, primero debe registrar un ticket de asistencia para el aprovisionamiento seguido de los pasos de integración.

**Registro de un ticket de asistencia**
Pasos para registrar un ticket de asistencia a través del Admin Console:

1. Añadir **Selector de recursos con AEM Assets** en el título del billete.

1. En la descripción, proporcione los siguientes detalles:

   * [!DNL Experience Manager Assets] as a [!DNL Cloud Service] URL (ID de programa e ID de entorno).
   * Nombres de dominio en los que está alojada la aplicación web que no es de Adobe.
+++

+++**Pasos de integración**
Utilice este ejemplo `index.html` para la autenticación al integrar el Selector de recursos con una aplicación que no sea de Adobe.

Acceda al paquete Selector de recursos mediante el `Script` Etiqueta, como se muestra en *línea 9* hasta *línea 11* del ejemplo `index.html` archivo.

*Línea 14* hasta *línea 38* En el ejemplo se describen las propiedades de flujo de IMS, como `imsClientId`, `imsScope`, y `redirectURL`. La función requiere que defina al menos una de las `imsClientId` y `imsScope` propiedades. Si no define un valor para `redirectURL`, se utiliza la URL de redireccionamiento registrada para el ID del cliente.

Como no tiene un `imsToken` generado, utilice el `registerAssetsSelectorsAuthService` y `renderAssetSelectorWithAuthFlow` funciones, como se muestra en las líneas 40 a 50 del ejemplo `index.html` archivo. Utilice el `registerAssetsSelectorsAuthService` función antes de `renderAssetSelectorWithAuthFlow` para registrar el `imsToken` con el Selector de recursos. [!DNL Adobe] recomienda llamar a `registerAssetsSelectorsAuthService` al crear una instancia del componente.

Defina la autenticación y otras propiedades relacionadas con el acceso as a Cloud Service de Assets en la `const props` , como se muestra en *línea 54* hasta *línea 60* del ejemplo `index.html` archivo.

El `PureJSSelectors` variable global, mencionada en *línea 65*, se utiliza para representar el Selector de recursos en el explorador web.

El selector de recursos se procesa en la `<div>` elemento contenedor, tal como se menciona en *línea 74* hasta *línea 81*. En el ejemplo se utiliza un cuadro de diálogo para mostrar el Selector de recursos.

```html {line-numbers="true"}
<!DOCTYPE html>
<html>

<head>
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta charset="utf-8">
    <title>Asset Selectors</title>
    <link rel="stylesheet" href="index.css">
    <script id="asset-selector"
        src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/asset-selectors.js"></script>
    <script>

        const imsProps = {
            imsClientId: "<obtained from IMS team>",
            imsScope: "openid, <other scopes>",
            redirectUrl: window.location.href,
            modalMode: true, // false to open in a full page reload flow
            onImsServiceInitialized: (service) => {
                // invoked when the ims service is initialized and is ready
                console.log("onImsServiceInitialized", service);
            },
            onAccessTokenReceived: (token) => {
                console.log("onAccessTokenReceived", token);
            },
            onAccessTokenExpired: () => {
                console.log("onAccessTokenError");
                // re-trigger sign-in flow
            },
            onErrorReceived: (type, msg) => {
                console.log("onErrorReceived", type, msg);
            },
        }

        function load() {
            const registeredTokenService = PureJSSelectors.registerAssetsSelectorsAuthService(imsProps);
            imsInstance = registeredTokenService;
        };

        // initialize the IMS flow before attempting to render the asset selector
        load();
        

        //function that will render the asset selector
            const otherProps = {
            // any other props supported by asset selector
            }
            const assetSelectorProps = {
                "imsOrg": "imsorg",
                ...otherProps
            }
             // container element on which you want to render the AssetSelector/DestinationSelector component
            const container = document.getElementById('asset-selector');

            /// Use the PureJSSelectors in globals to render the AssetSelector/DestinationSelector component
            PureJSSelectors.renderAssetSelectorWithAuthFlow(container, assetSelectorProps, () => {
                const assetSelectorDialog = document.getElementById('asset-selector-dialog');
                assetSelectorDialog.showModal();
            });
        }
    </script>

</head>
<body class="asset-selectors">
    <div>
        <button onclick="renderAssetSelectorWithAuthFlowFlow()">Asset Selector - Select Assets with Ims Flow</button>
    </div>
        <dialog id="asset-selector-dialog">
            <div id="asset-selector" style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px;">
            </div>
        </dialog>
    </div>
</body>

</html>
```

+++

+++**No se puede acceder al repositorio de envío**

>[!TIP]
>
>Si ha integrado el Selector de recursos mediante el flujo de trabajo de registro de inicio de sesión, pero sigue sin poder acceder al repositorio de envío, asegúrese de que las cookies del explorador se limpien. De lo contrario, terminará obteniendo `invalid_credentials All session cookies are empty` error en la consola.

>[!ENDTABS]

## Propiedades del Selector de recursos {#asset-selector-properties}

Puede utilizar las propiedades del Selector de recursos para personalizar la forma en que se procesa el Selector de recursos. En la tabla siguiente se enumeran las propiedades que puede utilizar para personalizar y utilizar el Selector de recursos.

| Propiedad | Tipo | Requerido | Predeterminado | Descripción |
|---|---|---|---|---|
| *carril* | booleano | No | false | Si está marcado `true`, el Selector de recursos se representa en una vista del carril izquierdo. Si está marcado `false`, el Selector de recursos se procesará en la vista modal. |
| *imsOrg* | cadena | Sí | | ID del sistema Identity Management de Adobe (IMS) asignado durante el aprovisionamiento [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] para su organización. El `imsOrg` La clave es necesaria para autenticar si la organización a la que accede se encuentra en Adobe IMS o no. |
| *imsToken* | cadena | No | | Token de portador de IMS utilizado para la autenticación. `imsToken` es necesario si utiliza un [!DNL Adobe] aplicación para la integración. |
| *apiKey* | cadena | No | | Clave de API utilizada para acceder al servicio AEM Discovery. `apiKey` es necesario si utiliza un [!DNL Adobe] integración de aplicaciones. |
| *rootPath* | cadena | No | /content/dam/ | Ruta de la carpeta desde la que el Selector de recursos muestra los recursos. `rootPath` también se puede utilizar en forma de encapsulación. Por ejemplo, dada la siguiente ruta, `/content/dam/marketing/subfolder/`Sin embargo, el Selector de recursos no le permite atravesar ninguna carpeta principal, sino que solo muestra las carpetas secundarias. |
| *ruta* | cadena | No | | Ruta que se utiliza para navegar a un directorio específico de recursos cuando se procesa el Selector de recursos. |
| *filterSchema* | matriz | No | | Modelo que se utiliza para configurar las propiedades del filtro. Esto resulta útil cuando desea limitar ciertas opciones de filtro en el Selector de recursos. |
| *filterFormProps* | Objeto | No | | Especifique las propiedades del filtro que debe utilizar para restringir la búsqueda. Por ejemplo, JPG de tipo MIME, PNG, GIF. |
| *selectedAssets* | Matriz `<Object>` | No |                 | Especificar los recursos seleccionados cuando se procese el selector de recursos. Se requiere una matriz de objetos que contenga una propiedad id de los recursos. Por ejemplo, `[{id: 'urn:234}, {id: 'urn:555'}]` Un recurso debe estar disponible en el directorio actual. Si necesita utilizar un directorio diferente, proporcione un valor para la propiedad de `path` también. |
| *acvConfig* | Objeto | No | | Propiedad de vista de colección de recursos que contiene un objeto con una configuración personalizada para anular los valores predeterminados. Además, esta propiedad se utiliza con `rail` para habilitar la vista de carril del visor de recursos. |
| *i18nSymbols* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | No |                 | Si las traducciones OOTB no son suficientes para las necesidades de la aplicación, puede exponer una interfaz a través de la cual puede pasar sus propios valores localizados personalizados a través de la variable `i18nSymbols` prop. Al pasar un valor a través de esta interfaz, se anulan las traducciones predeterminadas proporcionadas y, en su lugar, se utilizan las suyas. Para realizar la anulación, debe pasar un objeto [Descriptor del mensaje](https://formatjs.io/docs/react-intl/api/#message-descriptor) válido a la clave de `i18nSymbols` que desee anular. |
| *intl* | Objeto | No | | El Selector de recursos proporciona traducciones OOTB predeterminadas. Puede seleccionar el idioma de traducción proporcionando una cadena de configuración regional válida a través del prop `intl.locale`. Por ejemplo: `intl={{ locale: "es-es" }}` </br></br> Las cadenas de configuración regional admitidas siguen los [Códigos ISO 639](https://www.iso.org/iso-639-language-codes.html) para la representación de los estándares de nombres de idiomas. </br></br> Lista de configuraciones regionales admitidas: Inglés - &#39;en-us&#39; (predeterminado) Español - &#39;es-es&#39; Alemán - &#39;de-de&#39; Francés - &#39;fr-fr&#39; Italiano - &#39;it-it&#39; Japonés - &#39;ja-jp&#39; Coreano - &#39;ko-kr&#39; Portugués - &#39;pt-br&#39; Chino (tradicional) - &#39;zh-cn&#39; Chino (Taiwán) - &#39;zh-tw&#39; |
| *repositoryId* | cadena | No | &#39;&#39; | Repositorio desde el que el Selector de recursos carga el contenido. |
| *additionalAemSolutions* | `Array<string>` | No | [ ] | AEM Permite añadir una lista de repositorios de recursos de la adicionales. Si no se proporciona información en esta propiedad, solo se tienen en cuenta los repositorios de la biblioteca de medios o de AEM Assets. |
| *hideTreeNav* | booleano | No |  | Especifica si se muestra u oculta la barra lateral de navegación del árbol de recursos. Solo se utiliza en la vista modal y, por lo tanto, no hay ningún efecto de esta propiedad en la vista de carril. |
| *onDrop* | Función | No | | La propiedad permite la funcionalidad de colocación de un recurso. |
| *dropOptions* | `{allowList?: Object}` | No | | Configura las opciones de colocación mediante &#39;allowList&#39;. |
| *colorScheme* | cadena | No | | Configurar tema (`light` o `dark`) para el Selector de recursos. |
| *handleSelection* | Función | No | | Se invoca con la matriz de elementos de recurso cuando se seleccionan los recursos y se hace clic en el botón `Select` en el modal. Esta función solo se invoca en la vista modal. Para la vista de carril, utilice las funciones `handleAssetSelection` o `onDrop`. Ejemplo: <pre>handleSelection=(assets: Asset[])=> {...}</pre> Consulte [Tipo de recurso seleccionado](#selected-asset-type) para obtener más información. |
| *handleAssetSelection* | Función | No | | Se invoca con una matriz de elementos cuando los recursos se seleccionan o no. Esto resulta útil cuando desea escuchar los recursos a medida que el usuario los selecciona. Ejemplo: <pre>handleSelection=(assets: Asset[])=> {...}</pre> Consulte [Tipo de recurso seleccionado](#selected-asset-type) para obtener más información. |
| *onClose* | Función | No | | Se invoca cuando se pulsa el botón `Close` en la vista modal. Esto solo se llama en la vista `modal` y se ignora en la vista `rail`. |
| *onFilterSubmit* | Función | No | | Se invoca con elementos de filtro cuando el usuario cambia criterios de filtro diferentes. |
| *selectionType* | cadena | No | sencillo | Configuración para selección de `single` o `multiple` de recursos a la vez. |
| *dragOptions.lista de permitidos* | booleano | No | | La propiedad se utiliza para permitir o denegar el arrastre de recursos que no se pueden seleccionar. |
| *aemTierType* | cadena | No | | Permite seleccionar si desea mostrar los recursos del nivel de entrega, del nivel de creación o de ambos. <br><br> Sintaxis: `aemTierType:[0: "author" 1: "delivery"` <br><br> Por ejemplo, si tanto `["author","delivery"]` se utilizan, el conmutador de repositorios muestra las opciones para la creación y la entrega. |
| *handleNavigateToAsset* | Función | No | | Es una función de llamada de retorno para gestionar la selección de un recurso. |
| *noWrap* | booleano | No | | El *noWrap* La propiedad ayuda a procesar el Selector de recursos en el panel de raíl lateral. Si no se menciona esta propiedad, procesa el *Vista de diálogo* de forma predeterminada. |
| *dialogSize* | adquisición en pequeña, mediana, grande, pantalla completa o pantalla completa | Cadena | Opcional | Puede controlar el diseño especificando su tamaño con las opciones dadas. |
| *colorScheme* | claro u oscuro | No | | Esta propiedad se utiliza para establecer la temática de una aplicación Selector de recursos. Puede elegir entre tema claro u oscuro. |
| *filterRepoList* | Función | No |  | Puede utilizar `filterRepoList` función de llamada de retorno que llama al repositorio del Experience Manager y devuelve una lista filtrada de repositorios. |

## Ejemplos de uso de las propiedades del Selector de recursos {#usage-examples}

Puede definir las [propiedades](#asset-selector-properties) del Selector de recursos en el archivo `index.html` para personalizar la visualización del Selector de recursos en la aplicación.

### Ejemplo 1: Selector de recursos en la vista de carril

![rail-view-example](assets/rail-view-example-vanilla.png)

Si el valor de AssetSelector `rail` se establece en `false` o no se menciona en las propiedades, el Selector de recursos se muestra en la vista modal de forma predeterminada. El `acvConfig` permite realizar algunas configuraciones en profundidad, como Arrastrar y soltar. Visita [habilitar o deshabilitar arrastrar y soltar](#enable-disable-drag-and-drop) para comprender el uso de `acvConfig` propiedad.

<!--
### Example 2: Use selectedAssets property in addition to the path property

Use the `path` property to define the folder name that displays automatically when the Asset Selector is rendered. In addition, use the `selectedAssets` property to define the IDs for the assets that you need to select within the folder. Moreover, when you want to display assets that are pre-defined within the folder, you can use selectedAssets property.

   ![selected-assets-example](assets/selected-assets-example-vanilla.png)
-->

### Ejemplo 2: ventana emergente de metadatos

Utilice varias propiedades para definir los metadatos de un recurso que desee ver mediante un icono de información. La ventana emergente de información proporciona la colección de información sobre el recurso o la carpeta, incluido el título, las dimensiones, la fecha de modificación, la ubicación y la descripción de un recurso. En el ejemplo siguiente, se utilizan varias propiedades para mostrar los metadatos de un recurso, por ejemplo: la propiedad `repo:path` especifica la ubicación de un recurso. <!--`repo` represents the repository from where the asset is showing, whereas, `path` represents the route from where the asset or folder is rendered.-->

![metadata-popover-example](assets/metadata-popover.png)

### Ejemplo 3: Propiedad de filtro personalizado en la vista de carril

Además de la búsqueda con facetas, el Selector de recursos permite personalizar varios atributos para restringir la búsqueda desde [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] aplicación. Agregue el siguiente código para agregar filtros de búsqueda personalizados en la aplicación. En el ejemplo siguiente, la búsqueda `Type Filter` que filtra el tipo de recurso entre imágenes, documentos o vídeos o el tipo de filtro que ha agregado para la búsqueda.

![custom-filter-example-vanilla](assets/custom-filter-example-vanilla.png)

<!--

## Customization after integrating Asset Selector 

### Custom metadata

Assets display panel shows the out of the box metadata that can be displayed in the info of the asset. In addition to this, [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application allows configuration of the asset selector by adding custom metadata that is shown in info panel of the asset.
-->

## Fragmentos de código de configuración funcional{#code-snippets}

Defina los requisitos previos en la `index.html` o un archivo similar dentro de la implementación de la aplicación para definir los detalles de autenticación para acceder al [!DNL Experience Manager Assets] repositorio. Una vez finalizado, puede agregar fragmentos de código según sus necesidades.

### Personalizar panel de filtro {#customize-filter-panel}

Puede añadir el siguiente fragmento de código en `assetSelectorProps` para personalizar el panel de filtros:

```
filterSchema: [
    {
    header: 'File Type',
    groupKey: 'TopGroup',
    fields: [
    {
    element: 'checkbox',
    name: 'type',
    options: [
    {
    label: 'Images',
    value: '<comma separated mimetypes, without space, that denote all images, for e.g., image/>',
    },
    {
    label: 'Videos',
    value: '<comma separated mimetypes, without space, that denote all videos for e.g., video/,model/vnd.mts,application/mxf>'
    }
    ]
    }
    ]
    },
    {
    fields: [
    {
    element: 'checkbox',
    name: 'type',
    options: [
    { label: 'JPG', value: 'image/jpeg' },
    { label: 'PNG', value: 'image/png' },
    { label: 'TIFF', value: 'image/tiff' },
    { label: 'GIF', value: 'image/gif' },
    { label: 'MP4', value: 'video/mp4' }
    ],
    columns: 3,
    },
    ],
    header: 'Mime Types',
    groupKey: 'MimeTypeGroup',
    }},
    {
    fields: [
    {
    element: 'checkbox',
    name: 'property=metadata.application.xcm:keywords.value',
    options: [
    { label: 'Fruits', value: 'fruits' },
    { label: 'Vegetables', value: 'vegetables'}
    ],
    columns: 3,
    },
    ],
    header: 'Food Category',
    groupKey: 'FoodCategoryGroup',
    }
],
```

### Personalizar información en la vista modal {#customize-info-in-modal-view}

Puede personalizar la vista de detalles de un recurso al hacer clic en ![icono de información](assets/info-icon.svg) icono. Ejecute el siguiente código:

```
// Create an object infoPopoverMap and set the property `infoPopoverMap` with it in assetSelectorProps
const infoPopoverMap = (map) => {
// for example, to skip `path` from the info popover view
let defaultPopoverData = PureJSSelectors.getDefaultInfoPopoverData(map);
return defaultPopoverData.filter((i) => i.label !== 'Path'
};
assetSelectorProps.infoPopoverMap = infoPopoverMap;
```

### Habilitar o deshabilitar el modo de arrastrar y soltar {#enable-disable-drag-and-drop}

Agregue las siguientes propiedades a `assetSelectorProp` para habilitar el modo de arrastrar y soltar. Para deshabilitar la función de arrastrar y soltar, reemplace el `true` parámetro con `false`.

```
rail: true,
acvConfig: {
dragOptions: {
allowList: {
'*': true,
},
},
selectionType: 'multiple'
}

// the drop handler to be implemented
function drop(e) {
e.preventDefault();
// following helps you get the selected assets – an array of objects.
const data = JSON.parse(e.dataTransfer.getData('collectionviewdata'));
}
```

### Selección de recursos {#selection-of-assets}

El tipo de recurso seleccionado es una matriz de objetos que contiene la información del recurso al utilizar las funciones `handleSelection`, `handleAssetSelection`, y `onDrop`.

Ejecute los siguientes pasos para configurar la selección de uno o varios recursos:

```
acvConfig: {
selectionType: 'multiple' // 'single' for single selection
}
// the `handleSelection` callback, always gets you the array of selected assets
```

**Sintaxis de esquema**

```
interface SelectedAsset {
    'repo:id': string;
    'repo:name': string;
    'repo:path': string;
    'repo:size': number;
    'repo:createdBy': string;
    'repo:createDate': string;
    'repo:modifiedBy': string; 
    'repo:modifyDate': string; 
    'dc:format': string; 
    'tiff:imageWidth': number;
    'tiff:imageLength': number;
    'repo:state': string;
    computedMetadata: Record<string, any>;
    _links: {
        'https://ns.adobe.com/adobecloud/rel/rendition': Array<{
            href: string;
            type: string;
            'repo:size': number;
            width: number;
            height: number;
            [others: string]: any;
        }>;
    };
}
```

En la tabla siguiente se describen algunas de las propiedades importantes del objeto Recurso seleccionado.

| Propiedad | Tipo | Descripción |
|---|---|---|
| *repo:repositoryId* | cadena | Identificador único del repositorio en el que se almacena el recurso. |
| *repo:id* | cadena | Identificador único del recurso. |
| *repo:assetClass* | cadena | La clasificación del recurso (por ejemplo, imagen o vídeo, documento). |
| *repo:name* | cadena | Nombre del recurso, incluida la extensión de archivo. |
| *repo:size* | número | El tamaño del recurso en bytes. |
| *repo:path* | cadena | La ubicación del recurso dentro del repositorio. |
| *repo:ancestors* | `Array<string>` | Matriz de elementos antecesores del recurso en el repositorio. |
| *repo:state* | cadena | Estado actual del recurso en el repositorio (por ejemplo, activo, eliminado, etc.). |
| *repo:createdBy* | cadena | El usuario o sistema que creó el recurso. |
| *repo:createDate* | cadena | La fecha y la hora en que se creó el recurso. |
| *repo:modifiedBy* | cadena | Usuario o sistema que modificó el recurso por última vez. |
| *repo:modifyDate* | cadena | La fecha y la hora en que se modificó el recurso por última vez. |
| *dc:format* | cadena | El formato del recurso, como el tipo de archivo (por ejemplo, JPEG, PNG, etc.). |
| *tiff:imageWidth* | número | La anchura de un recurso. |
| *tiff:imageLength* | número | Altura de un recurso. |
| *computedMetadata* | `Record<string, any>` | Un objeto que representa un cubo para todos los metadatos del recurso de todo tipo (repositorio, aplicación o metadatos incrustados). |
| *_links* | `Record<string, any>` | Vínculos de hipermedia para el recurso asociado. Incluye vínculos para recursos como metadatos y representaciones. |
| *_vínculos.<https://ns.adobe.com/adobecloud/rel/rendition>* | `Array<Object>` | Matriz de objetos que contiene información sobre las representaciones del recurso. |
| *_vínculos.<https://ns.adobe.com/adobecloud/rel/rendition[].href>* | cadena | URI de la representación. |
| *_vínculos.<https://ns.adobe.com/adobecloud/rel/rendition[].type>* | cadena | Tipo MIME de la representación. |
| *_vínculos.<https://ns.adobe.com/adobecloud/rel/rendition[].'repo:size>&#39;* | número | El tamaño de la representación en bytes. |
| *_vínculos.<https://ns.adobe.com/adobecloud/rel/rendition[].width>* | número | La anchura de la representación. |
| *_vínculos.<https://ns.adobe.com/adobecloud/rel/rendition[].height>* | número | Altura de la representación. |

Para obtener una lista completa de las propiedades y un ejemplo detallado, visite [Ejemplo de código del selector de recursos](https://github.com/adobe/aem-assets-selectors-mfe-examples).

## Gestión de la selección de recursos mediante el esquema de objetos {#handling-selection}

La propiedad `handleSelection` se utiliza para gestionar una o varias selecciones de recursos en el Selector de recursos. El ejemplo siguiente indica la sintaxis de uso de `handleSelection`.

![handle-selection](assets/handling-selection.png)

## Desactivación de la selección de recursos {#disable-selection}

Deshabilitar selección se utiliza para ocultar o deshabilitar la selección de recursos o carpetas. Oculta la casilla de verificación de selección de la tarjeta o el recurso, lo que impide que se seleccione. Para utilizar esta función, puede declarar la posición de un recurso o carpeta que desee deshabilitar en una matriz. Por ejemplo, si desea deshabilitar la selección de una carpeta que aparece en la primera posición, puede agregar el siguiente código:
`disableSelection: [0]:folder`

Puede proporcionar a la matriz una lista de tipos MIME (como imagen, carpeta, archivo u otros tipos MIME, por ejemplo, imagen/jpeg) que desee desactivar. Los tipos MIME que declare se asignan a `data-card-type` y `data-card-mimetype` atributos de un recurso.

Además, los recursos con la selección deshabilitada se pueden arrastrar. Para desactivar la función de arrastrar y soltar de un tipo de recurso concreto, puede utilizar `dragOptions.allowList` propiedad.

La sintaxis de la selección de deshabilitar es la siguiente:

```
(args)=> {
    return(
        <ASDialogWrapper
            {...args}
            disableSelection={args.disableSelection}
            handleAssetSelection={action('handleAssetSelection')}
            handleSelection={action('handleSelection')}
            selectionType={args.selectionType}
        />
    );
}
```

>[!NOTE]
>
> En el caso de un recurso, la casilla de verificación de selección está oculta, mientras que en el caso de una carpeta, la carpeta no se puede seleccionar, pero sigue apareciendo la navegación por la carpeta mencionada.

## Uso del Selector de recursos {#using-asset-selector}

Una vez configurado el Selector de recursos y autenticado para usar el Selector de recursos con su aplicación [!DNL Adobe Experience Manager] as a [!DNL Cloud Service], puede seleccionar recursos o realizar otras operaciones para buscar los recursos dentro del repositorio.

![using-asset-selector](assets/using-asset-selector.png)

* **A**: [Ocultar/Mostrar panel](#hide-show-panel)
* **B**: [Conmutador de repositorios](#repository-switcher)
* **C**: [Recursos](#repository)
* **D**: [Filtros](#filters)
* **E**: [Barra de búsqueda](#search-bar)
* **F**: [Ordenación](#sorting)
* **G**: [Ordenación en orden ascendente o descendente](#sorting)
* **H**: [Ver](#types-of-view)

### Ocultar/Mostrar panel {#hide-show-panel}

Para ocultar carpetas en el panel de navegación izquierdo, haga clic en el icono **[!UICONTROL Ocultar carpetas]**. Para deshacer los cambios, haga clic en el icono **[!UICONTROL Ocultar carpetas]** de nuevo.

### Conmutador de repositorios {#repository-switcher}

El Selector de recursos también le permite cambiar de repositorio para la selección de recursos. Puede seleccionar el repositorio que desee en la lista desplegable disponible en el panel izquierdo. Las opciones del repositorio disponibles en la lista desplegable se basan en la propiedad `repositoryId` definida en el archivo `index.html`. Se basa en el entorno de la organización de IMS seleccionada al que accede el usuario que ha iniciado sesión. Los consumidores pueden aprobar un `repositoryID` preferido y, en ese caso, el Selector de recursos deja de procesar el conmutador de repositorios y solo procesa los recursos del repositorio dado.
<!--
It is based on the `imsOrg` that is provided in the application. If you want to see the list of repositories, then `repositoryId` is required to view those specific repositories in your application.
-->

### Repositorio de recursos

Es una colección de carpetas de recursos que puede utilizar para realizar operaciones.

### Filtros listos para usar {#filters}

El Selector de recursos también proporciona opciones de filtro listas para usar para restringir los resultados de búsqueda. Los filtros disponibles son los siguientes:

* `File type`: incluye carpeta, archivo, imágenes, documentos o vídeo
* `MIME type`: incluye JPG, GIF, PPTX, PNG, MP4, DOCX, TIFF, PDF, XLSX
* `Image Size`: incluye la anchura mínima/máxima, la altura mínima/máxima de la imagen

  ![rail-view-example](assets/filters-asset-selector.png)

### Búsqueda personalizada

Además de la búsqueda de texto completo, el Selector de recursos permite buscar recursos dentro de los archivos mediante búsquedas personalizadas. Puede utilizar filtros de búsqueda personalizados en los modos Vista modal y Vista de carril.

![custom-search](assets/custom-search1.png)

También puede crear un filtro de búsqueda predeterminado para guardar los campos que busca con frecuencia y utilizarlos más adelante. Para crear una búsqueda personalizada de sus recursos, puede utilizar la propiedad `filterSchema`.

### Barra de búsqueda {#search-bar}

El Selector de recursos permite realizar una búsqueda de texto completo de los recursos del repositorio seleccionado. Por ejemplo, si escribe la palabra clave `wave` en la barra de búsqueda, se muestran todos los recursos con la palabra clave `wave` mencionada en cualquiera de las propiedades de metadatos.

### Ordenación {#sorting}

Puede ordenar los recursos en el Selector de recursos por nombre, dimensiones o tamaño de un recurso. También puede ordenar los recursos en orden ascendente o descendente.

### Tipos de vista {#types-of-view}

El Selector de recursos le permite ver el recurso en cuatro vistas diferentes:

* **![vista de lista](assets/do-not-localize/list-view.png) [!UICONTROL Vista de lista]**: la vista de lista muestra los archivos y carpetas desplazables en una sola columna.
* **![vista de cuadrícula](assets/do-not-localize/grid-view.png) [!UICONTROL Vista de cuadrícula]**: la vista de cuadrícula muestra archivos y carpetas desplazables en una cuadrícula de filas y columnas.
* **![vista de galería](assets/do-not-localize/gallery-view.png) [!UICONTROL Vista de galería]**: la vista de galería muestra los archivos o carpetas en una lista horizontal bloqueada en el centro.
* **![vista de cascada](assets/do-not-localize/waterfall-view.png) [!UICONTROL Vista de cascada]**: la vista de cascada muestra los archivos o carpetas en forma de puente.

<!--
### Modes to view Asset Selector

Asset Selector supports two types of out of the box views:

**  Modal view or Inline view:** The modal view or inline view is the default view of Asset Selector that represents Assets folders in the front area. The modal view allows users to view assets in a full screen to ease the selection of multiple assets for import. Use `<AssetSelector rail={false}>` to enable modal view.

    ![modal-view](assets/modal-view.png)

**  Rail view:** The rail view represents Assets folders in a left panel. The drag and drop of assets can be performed in this view. Use `<AssetSelector rail={true}>` to enable rail view.

    ![rail-view](assets/rail-view.png)
-->
<!--

### Application Integration

Asset Selector is flexible and can be integrated within your existing [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application. It is accessible and localized to add, search, and select assets in your application. With Asset Selector you can:
*   **Configure** You can configure the files/folders that you want to show at the upfront. The assets that are chosen to view can be of any supported formats, for example, JPEG. It lets you control the display of various text or symbols as per your choice.
*   **Perfect fit** Asset selector easily fits in your existing [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application and choose the way you want to view. The mode of view can be inline, rail, or modal view.
*   **Accessible** With Asset Selector, you can reach the desired asset in an easy manner.
*   **Localize** Assets can be availed for the various locales available as per Adobe's localization standards.
-->
<!--

### Support for multiple instances

The micro front-end design supports the display of multiple instances of Asset Selector on a single screen.

![multiple-instance](assets/multiple-instance.png)
-->

<!--

### Controlled selection with multi-select

You can make default multi-selection of assets by specifying the assets to the component using `selectedAssets` property. You should specify an array of asset IDs. For example, `[{id: 'urn:234}, {id: 'urn:555'}].`
-->
<!--

### Action buttons

When you customize your application with Asset Selector based on ReactJS, you are provided with the following action buttons to perform various actions:
*   **Open in media library** Lets you open the asset in media library.
*   **Upload** Lets you upload an asset directly.
*   **Download** Downloads the asset in [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
-->
<!--

### Status of an asset

Asset Selector lets you know the status of your uploaded assets. The status can be `Approved`, `Rejected`, or `Expired` of the asset. 
-->
<!--

### Localization

The integration of Asset Selector with [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] allows localized content appear in your application.
-->



<!--Best Practice-->
<!--
+++**Control default selection of the filter**
You can make the selection of filter default by implementing the following code snippet:

```
"defaultValue": [
    "image/*",
    "application/*"
],

{
    "label": "Documents",
    "value": "application/*"
}
```

+++
-->
