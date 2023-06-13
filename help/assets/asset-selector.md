---
title: Selector de recursos para [!DNL Adobe Experience Manager] como un [!DNL Cloud Service]
description: Utilice el selector de recursos para buscar y recuperar metadatos y representaciones de recursos dentro de la aplicación.
contentOwner: Adobe
role: Admin,User
source-git-commit: af36101d8fecd7fab2300f93d40bba4c92f8eafe
workflow-type: ht
source-wordcount: '2378'
ht-degree: 100%

---


# Selector de recursos de Micro-Frontend {#Overview}

El Selector de recursos de Micro-Frontend proporciona una interfaz de usuario que se integra fácilmente con el repositorio de [!DNL Experience Manager Assets as a Cloud Service] para poder examinar o buscar recursos digitales disponibles en el repositorio y utilizarlos en la experiencia de creación de la aplicación.

La interfaz de usuario de Micro-Frontend está disponible en la experiencia de su aplicación mediante el paquete Selector de recursos. Las actualizaciones del paquete se importan automáticamente y el último Selector de recursos implementado se carga automáticamente en la aplicación.

![Información general](assets/overview.png)

El Selector de recursos ofrece muchas ventajas, como las siguientes:

* Facilidad de integración con cualquiera de las aplicaciones de Adobe o que no sean de Adobe mediante la biblioteca JavaScript de Vanilla.
* Son fáciles de mantener, ya que las actualizaciones del paquete del Selector de recursos se implementan automáticamente en el Selector de recursos disponible para su aplicación. No se requieren actualizaciones dentro de la aplicación para cargar las modificaciones más recientes.
* Facilidad de personalización, ya que hay propiedades disponibles que controlan la visualización del Selector de recursos en la aplicación.

* Filtros personalizados, de búsqueda de texto completo y listos para usar para navegar rápidamente a los recursos y utilizarlos en la experiencia de creación.

* Capacidad para cambiar repositorios dentro de una organización IMS para la selección de recursos.

* Capacidad para ordenar recursos por nombre, dimensiones y tamaño y verlos en la vista Lista, Cuadrícula, Galería o Cascada.

El ámbito de este artículo es demostrar cómo utilizar el Selector de recursos con una aplicación de [!DNL Adobe] bajo Unified Shell o cuando ya tiene un imsToken generado para la autenticación. Estos flujos de trabajo se denominan flujo no SUSI en este artículo.

Realice las siguientes tareas para integrar y utilizar el Selector de recursos con su repositorio de [!DNL Experience Manager Assets as a Cloud Service]:

* [Integración del Selector de recursos mediante Vanilla JS](#integration-with-vanilla-js)
* [Definir propiedades de visualización del Selector de recursos](#asset-selector-properties)
* [Uso del Selector de recursos](#using-asset-selector)

## Integración del Selector de recursos mediante Vanilla JS {#integration-with-vanilla-js}

Puede integrar cualquier [!DNL Adobe] o aplicación sin Adobe con [!DNL Experience Manager Assets] como un repositorio de [!DNL Cloud Service] y seleccione recursos desde la aplicación.

La integración se realiza importando el paquete Selector de recursos y conectándose a los Assets as a Cloud Service mediante la biblioteca JavaScript de Vanilla. Debe editar un `index.html` o cualquier archivo apropiado dentro de su aplicación para:
* Definición de los detalles de autenticación
* Acceso al repositorio Assets as a Cloud Service
* Configurar las propiedades de visualización del Selector de recursos

<!--
Asset Selector supports authentication to the [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository using Identity Management System (IMS) properties such as `imsScope` or `imsClientID`. Authentication using these IMS properties is referred to as SUSI (Sign Up Sign In) flow in this article.

You can perform authentication without defining some of the IMS properties, such as `imsScope` or `imsClientID`, if:

*   You are integrating an [!DNL Adobe] application on [Unified Shell](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=en).
*   You already have an IMS token generated for authentication.

Accessing [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository without defining `imsScope` or `imsClientID` IMS properties is referred to as a non-SUSI flow in this article.
-->

Puede realizar la autenticación sin definir algunas de las propiedades de IMS, si:

* Está integrando una aplicación de [!DNL Adobe] en [Unified Shell](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=es).
* Ya ha generado un token de IMS para la autenticación.

## Requisitos previos {#prerequisites}

<!--
If your application requires user based authentication, out-of-the-box Asset Selector also supports a flow for authentication to the [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository using Identity Management System (IMS.)

You can use properties such as `imsScope` or `imsClientID` to retrieve `imsToken` automatically. You can use SUSI (Sign Up Sign In) flow and IMS properties. Also, you can obtain your own imsToken and pass it to Asset Selector by integrating within [!DNL Adobe] application on Unified Shell or if you already have an imsToken obtained via other methods (for example, using technical account). Accessing [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository without defining IMS properties (For example, `imsScope` and `imsClientID`) is referred to as a non-SUSI flow.
-->

Defina los requisitos previos en el archivo de `index.html` o un archivo similar dentro de la implementación de la aplicación para definir los detalles de la autenticación para acceder al repositorio de [!DNL Experience Manager Assets] as a [!DNL Cloud Service]. Los requisitos previos incluyen:
* imsOrg
* imsToken
* apikey

<!--
The prerequisites vary if you are authenticating using a SUSI flow or a non-SUSI flow.

**Non-SUSI flow**

*   imsOrg
*   imsToken
*   apikey

For more information on these properties, refer to [Asset Selector Properties](#asset-selector-properties).

**SUSI flow**

*   imsClientId
*   imsScope
*   redirectUrl
*   imsOrg
*   apikey

For more information on these properties, refer to [Example for the SUSI flow](#susi-vanilla) and [Asset Selector Properties](#asset-selector-properties).
-->

## Instalación {#installation}

Los selectores de recursos están disponibles a través de la CDN de ESM (por ejemplo, [esm.sh](https://esm.sh/)/[skypack](https://www.skypack.dev/)) y versión [UMD](https://github.com/umdjs/umd).

En navegadores que utilizan la **Versión de UMD** (recomendado):

```
<script src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js"></script>

<script>
  const { renderAssetSelector } = PureJSSelectors;
</script>
```

En navegadores con compatibilidad con `import maps` con **Versión de CDN de ESM**:

```
<script type="module">
  import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/@assets/selectors/index.js'
</script>
```

En la federación de módulos Deno/Webpack mediante **Versión de CDN de ESM**:

```
import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/@assets/selectors/index.js'
```

### Tipo de recurso seleccionado {#selected-asset-type}

El tipo de recurso seleccionado es una matriz de objetos que contiene la información del recurso al utilizar las funciones `handleSelection`, `handleAssetSelection`, y `onDrop`.

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
        'http://ns.adobe.com/adobecloud/rel/rendition': Array<{
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

| Propiedad | Tipo | Explicación |
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
| *_links.http://ns.adobe.com/adobecloud/rel/rendition* | `Array<Object>` | Matriz de objetos que contiene información sobre las representaciones del recurso. |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].href* | cadena | URI de la representación. |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].type* | cadena | Tipo MIME de la representación. |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].&#39;repo:size&#39;* | número | El tamaño de la representación en bytes. |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].width* | número | La anchura de la representación. |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].height* | número | Altura de la representación. |

Para obtener una lista completa de las propiedades y un ejemplo detallado, visite [Ejemplo de código del selector de recursos](https://github.com/adobe/aem-assets-selectors-mfe-examples).

<!--
### ImsAuthProps {#ims-auth-props}

The `ImsAuthProps` properties define the authentication information and flow that the Asset Selector uses to obtain an `imsToken`. By setting these properties, you can control how the authentication flow should behave and register listeners for various authentication events.

| Property Name | Description|
|---|---|
| `imsClientId`| A string value representing the IMS client ID used for authentication purposes. This value is provided by Adobe and is specific to your Adobe AEM CS organization.|
| `imsScope`| Describes the scopes used in authentication. The scopes determine the level of access that the application has to your organization resources. Multiple scopes can be separated by commas.|
| `redirectUrl` | Represents the URL where the user is redirected after authentication. This value is typically set to the current URL of the application. If a `redirectUrl` is not supplied, `ImsAuthService` will use the redirectUrl used to register the `imsClientId`|
| `modalMode`| A boolean indicating whether the authentication flow should be displayed in a modal (pop-up) or not. If set to `true`, the authentication flow is displayed in a pop-up. If set to `false`, the authentication flow is displayed in a full page reload. _Note:_ for better UX, you can dynamically control this value if the user has browser pop-up disabled. |
| `onImsServiceInitialized`| A callback function that is called when the Adobe IMS authentication service is initialized. This function takes one parameter, `service`, which is an object representing the Adobe IMS service. See [`ImsAuthService`](#imsauthservice-ims-auth-service) for more details.|
| `onAccessTokenReceived`| A callback function that is called when an `imsToken` is received from the Adobe IMS authentication service. This function takes one parameter, `imsToken`, which is a string representing the access token. |
| `onAccessTokenExpired`| A callback function that is called when an access token has expired. This function is typically used to trigger a new authentication flow to obtain a new access token. |
| `onErrorReceived`| A callback function that is called when an error occurs during authentication. This function takes two parameters: the error type and error message. The error type is a string representing the type of error and the error message is a string representing the error message. |

### ImsAuthService {#ims-auth-service}

`ImsAuthService` class handles the authentication flow for the Asset Selector. It is responsible for obtaining an `imsToken` from the Adobe IMS authentication service. The `imsToken` is used to authenticate the user and authorize access to the Adobe Experience Manager (AEM) CS Assets repository. ImsAuthService uses the `ImsAuthProps` properties to control the authentication flow and register listeners for various authentication events. You can use the convenient [`registerAssetsSelectorsAuthService`](#purejsselectorsregisterassetsselectorsauthservice) function to register the _ImsAuthService_ instance with the Asset Selector. The following functions are available on the `ImsAuthService` class. However, if you're using the _registerAssetsSelectorsAuthService_ function, you do not need to call these functions directly.

| Function Name | Description |
|---|---|
| `isSignedInUser` | Determines whether the user is currently signed in to the service and returns a boolean value accordingly.|
| `getImsToken`    | Retrieves the authentication `imsToken` for the currently signed-in user, which can be used to authenticate requests to other services such as generating asset _rendition.|
| `signIn`| Initiates the sign-in process for the user. This function uses the `ImsAuthProps` to show authentication in either a pop-up or a full page reload |
| `signOut`| Signs the user out of the service, invalidating their authentication token and requiring them to sign in again to access protected resources. Invoking this function will reload the current page.|
| `refreshToken`| Refreshes the authentication token for the currently signed-in user, preventing it from expiring and ensuring uninterrupted access to protected resources. Returns a new authentication token that can be used for subsequent requests. |
-->

### Ejemplo de flujo no SUSI {#non-susi-vanilla}

En este ejemplo se muestra cómo utilizar el Selector de recursos con un flujo que no sea SUSI al ejecutar una aplicación de [!DNL Adobe] en Unified Shell o cuando ya tiene `imsToken` generado para la autenticación.

Incluya el paquete Selector de recursos en su código mediante la etiqueta `script`, como se muestra en las _líneas 6 a 15_ del ejemplo siguiente. Una vez cargado el script, la variable global `PureJSSelectors` está disponible para su uso. Definición de las [propiedades](#asset-selector-properties) del Selector de recursos como se muestra en las _líneas 16 a 23_. Las propiedades de `imsOrg` y `imsToken` son necesarias para la autenticación en un flujo que no es SUSI. La propiedad de `handleSelection` se utiliza para gestionar los recursos seleccionados. Para procesar el Selector de recursos, llame a la función de `renderAssetSelector` como se menciona en _línea 17_. El Selector de recursos se muestra en el elemento contenedor de `<div>`, como se muestra en las _líneas 21 y 22_.

Al seguir estos pasos, puede utilizar el Selector de recursos con un flujo que no sea SUSI en su aplicación de [!DNL Adobe].

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
    <title>Asset Selector</title>
    <script src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js"></script>
    <script>
        // get the container element in which we want to render the AssetSelector component
        const container = document.getElementById('asset-selector-container');
        // imsOrg and imsToken are required for authentication in non-SUSI flow
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

Para ver un ejemplo detallado, visite [Ejemplo de código del selector de recursos](https://github.com/adobe/aem-assets-selectors-mfe-examples).

<!--
### Example for the SUSI flow {#susi-vanilla}

Use this example `index.html` file for authentication if you are integrating your application using SUSI flow.

Access the Asset Selector package using the `Script` Tag, as shown in *line 9* to *line 11* of the example `index.html` file.

*Line 14* to *line 38* of the example describes the IMS flow properties, such as `imsClientId`, `imsScope`, and `redirectURL`. The function requires that you define at least one of the `imsClientId` and `imsScope` properties. If you do not define a value for `redirectURL`, the registered redirect URL for the client ID is used.

As you do not have an `imsToken` generated, use the `registerAssetsSelectorsAuthService` and `renderAssetSelectorWithAuthFlow` functions, as shown in line 40 to line 50 of the example `index.html` file. Use the `registerAssetsSelectorsAuthService` function before `renderAssetSelectorWithAuthFlow` to register the `imsToken` with the Asset Selector. [!DNL Adobe] recommends to call `registerAssetsSelectorsAuthService` when you instantiate the component.

Define the authentication and other Assets as a Cloud Service access-related properties in the `const props` section, as shown in *line 54* to *line 60* of the example `index.html` file.

The `PureJSSelectors` global variable, mentioned in *line 65*, is used to render the Asset Selector in the web browser.

Asset Selector is rendered on the `<div>` container element, as mentioned in *line 74* to *line 81*. The example uses a dialog to display the Asset Selector.

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
-->

## Usar propiedades del Selector de recursos {#asset-selector-properties}

Puede utilizar las propiedades del Selector de recursos para personalizar la forma en que se procesa el Selector de recursos. En la tabla siguiente se enumeran las propiedades que puede utilizar para personalizar y utilizar el Selector de recursos.

| Propiedad | Tipo | Requerido | Predeterminado | Descripción |
|---|---|---|---|---|
| *carril* | booleano | No | false | Si está marcado `true`, el Selector de recursos se representará en una vista del carril izquierdo. Si está marcado `false`, el Selector de recursos se representará en la vista modal. |
| *imsOrg* | cadena | Sí |  | ID del sistema Identity Management de Adobe (IMS) asignado durante el aprovisionamiento [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] para su organización. La clave `imsOrg` es necesaria para autenticar si la organización a la que accede se encuentra en Adobe IMS o no. |
| *imsToken* | cadena | No |  | Token de portador de IMS utilizado para la autenticación. `imsToken` es necesario si utiliza el flujo que no es SUSI. |
| *apiKey* | cadena | No |  | Clave de API utilizada para acceder al servicio AEM Discovery. `apiKey` es necesario si utiliza el flujo que no es SUSI. |
| *rootPath* | cadena | No | /content/dam/ | Ruta de la carpeta desde la que el Selector de recursos muestra los recursos. `rootPath` también se puede utilizar en forma de encapsulación. Por ejemplo, dada la siguiente ruta, `/content/dam/marketing/subfolder/`, el Selector de recursos no le permite atravesar ninguna carpeta principal, sino que solo muestra las carpetas secundarias. |
| *ruta* | cadena | No |  | Ruta que se utiliza para navegar a un directorio específico de recursos cuando se procesa el Selector de recursos. |
| *filterSchema* | matriz | No |  | Modelo que se utiliza para configurar las propiedades del filtro. Esto resulta útil cuando desea limitar ciertas opciones de filtro en el Selector de recursos. |
| *filterFormProps* | Objeto | No |  | Especifique las propiedades del filtro que debe utilizar para restringir la búsqueda. Por ejemplo, JPG de tipo MIME, PNG, GIF. |
| *selectedAssets* | Matriz `<Object>` | No |  | Especificar los recursos seleccionados cuando se procese el selector de recursos. Se requiere una matriz de objetos que contenga una propiedad id de los recursos. Por ejemplo, `[{id: 'urn:234}, {id: 'urn:555'}]` Un recurso debe estar disponible en el directorio actual. Si necesita utilizar un directorio diferente, proporcione un valor para la propiedad de `path` también. |
| *acvConfig* | Objeto | No |  | Propiedad de vista de colección de recursos que contiene un objeto con una configuración personalizada para anular los valores predeterminados. |
| *i18nSymbols* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | No |  | Si las traducciones de OOTB no son suficientes para las necesidades de la aplicación, puede exponer una interfaz a través de la cual puede pasar sus propios valores localizados personalizados a través del prop `i18nSymbols`. Al pasar un valor a través de esta interfaz, se anulan las traducciones predeterminadas proporcionadas y, en su lugar, se utilizan las suyas.  Para realizar la anulación, debe pasar un objeto [Descriptor del mensaje](https://formatjs.io/docs/react-intl/api/#message-descriptor) válido a la clave de `i18nSymbols` que desee anular. |
| *intl* | Objeto | No |  | El Selector de recursos proporciona traducciones OOTB predeterminadas. Puede seleccionar el idioma de traducción proporcionando una cadena de configuración regional válida a través del prop `intl.locale`. Por ejemplo: `intl={{ locale: "es-es" }}` </br></br> Las cadenas de configuración regional admitidas siguen los [Códigos ISO 639](https://www.iso.org/iso-639-language-codes.html) para la representación de los estándares de nombres de idiomas. </br></br> Lista de configuraciones regionales admitidas: Inglés - &#39;en-us&#39; (predeterminado) Español - &#39;es-es&#39; Alemán - &#39;de-de&#39; Francés - &#39;fr-fr&#39; Italiano - &#39;it-it&#39; Japonés - &#39;ja-jp&#39; Coreano - &#39;ko-kr&#39; Portugués - &#39;pt-br&#39; Chino (tradicional) - &#39;zh-cn&#39; Chino (Taiwán) - &#39;zh-tw&#39; |
| *repositoryId* | cadena | No | &#39;&#39; | Repositorio desde el que el Selector de recursos carga el contenido. |
| *additionalAemSolutions* | `Array<string>` | No | [ ] | Le permite agregar una lista de repositorios de AEM adicionales. Si no se proporciona información en esta propiedad, solo se tienen en cuenta los repositorios de la biblioteca de medios o de AEM Assets. |
| *hideTreeNav* | booleano | No |  | Especifica si se muestra u oculta la barra lateral de navegación del árbol de recursos. Solo se utiliza en la vista modal y, por lo tanto, no hay ningún efecto de esta propiedad en la vista de carril. |
| *onDrop* | Función | No |  | La propiedad permite la funcionalidad de colocación de un recurso. |
| *dropOptions* | `{allowList?: Object}` | No |  | Configura las opciones de colocación mediante &#39;allowList&#39;. |
| *colorScheme* | cadena | No |  | Configurar tema (`light` o `dark`) para el Selector de recursos. |
| *handleSelection* | Función | No |  | Se invoca con la matriz de elementos de recurso cuando se seleccionan los recursos y se hace clic en el botón `Select` en el modal. Esta función solo se invoca en la vista modal. Para la vista de carril, utilice las funciones `handleAssetSelection` o `onDrop`. Ejemplo: <pre>handleSelection=(assets: Asset[])=> {...}</pre> Consulte [Tipo de recurso seleccionado](#selected-asset-type) para obtener más información. |
| *handleAssetSelection* | Función | No |  | Se invoca con una matriz de elementos cuando los recursos se seleccionan o no. Esto resulta útil cuando desea escuchar los recursos a medida que el usuario los selecciona. Ejemplo: <pre>handleSelection=(assets: Asset[])=> {...}</pre> Consulte [Tipo de recurso seleccionado](#selected-asset-type) para obtener más información. |
| *onClose* | Función | No |  | Se invoca cuando se pulsa el botón `Close` en la vista modal. Esto solo se llama en la vista `modal` y se ignora en la vista `rail`. |
| *onFilterSubmit* | Función | No |  | Se invoca con elementos de filtro cuando el usuario cambia criterios de filtro diferentes. |
| *selectionType* | cadena | No | sencillo | Configuración para selección de `single` o `multiple` de recursos a la vez. |

## Ejemplos de uso de las propiedades del Selector de recursos {#usage-examples}

Puede definir las [propiedades](#asset-selector-properties) del Selector de recursos en el archivo `index.html` para personalizar la visualización del Selector de recursos en la aplicación.

### Ejemplo 1: Selector de recursos en la vista de carril

![rail-view-example](assets/rail-view-example-vanilla.png)

Si el valor de AssetSelector `rail` se establece en `false` o no se menciona en las propiedades, el Selector de recursos se muestra en la vista Modal de forma predeterminada.

<!--
### Example 2: Use selectedAssets property in addition to the path property

Use the `path` property to define the folder name that displays automatically when the Asset Selector is rendered. In addition, use the `selectedAssets` property to define the IDs for the assets that you need to select within the folder. Moreover, when you want to display assets that are pre-defined within the folder, you can use selectedAssets property.

   ![selected-assets-example](assets/selected-assets-example-vanilla.png)
-->

### Ejemplo 2: ventana emergente de metadatos

Utilice varias propiedades para definir los metadatos de un recurso que desee ver mediante un icono de información. La ventana emergente de información proporciona la colección de información sobre el recurso o la carpeta, incluido el título, las dimensiones, la fecha de modificación, la ubicación y la descripción de un recurso. En el ejemplo siguiente, se utilizan varias propiedades para mostrar los metadatos de un recurso, por ejemplo: la propiedad `repo:path` especifica la ubicación de un recurso. <!--`repo` represents the repository from where the asset is showing, whereas, `path` represents the route from where the asset or folder is rendered.-->

![metadata-popover-example](assets/metadata-popover.png)


### Ejemplo 3: Propiedad de filtro personalizado en la vista de carril

Además de la búsqueda con facetas, el Selector de recursos le permite personalizar varios atributos para restringir la búsqueda desde la aplicación [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]. Debe agregar el siguiente código para agregar filtros de búsqueda personalizados en la aplicación. En el ejemplo siguiente, la búsqueda `Type Filter` que filtra el tipo de recurso entre imágenes, documentos o vídeos o el tipo de filtro que ha agregado para la búsqueda.

![custom-filter-example-vanilla](assets/custom-filter-example-vanilla.png)

<!--

## Customization after integrating Asset Selector 

### Custom metadata

Assets display panel shows the out of the box metadata that can be displayed in the info of the asset. In addition to this, [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application allows configuration of the asset selector by adding custom metadata that is shown in info panel of the asset.
-->

<!-- Property details to be added here. Referred the ticket https://jira.corp.adobe.com/browse/ASSETS-19023-->

<!--
## Asset Selector Object Schema {#object-schema}

Schema describes the object properties associated with an asset selected using Asset Selector. It uses the combination of data types and their values to validate the object describing the selected Asset using an Asset Selector.

**Schema Syntax**
````
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
        'http://ns.adobe.com/adobecloud/rel/rendition': Array<{
            href: string;
            type: string;
            'repo:size': number;
            width: number;
            height: number;
            [others: string]: any;
        }>;
    };
}
````

**Query Parameters**

| Parameter | Type | Description |
|---|---|---|
| repo:id | string | ID of an Asset |
| repo:name | string | The name of an Asset |
| repo:path | string | The path of an Asset |
| repo:size | number | Size of an Asset (in bytes) |
| repo:createdBy | string | ID of a user who created an Asset |
| repo: createdDate | string | The timestamp when an asset was created |
| repo:modifiedBy | string | ID of a user who modified the asset recently |
| repo:modifyDate | string | The timestamp when the asset was last modified |
| dc:format | string | MIME type of an Asset |
| tiff:imageWidth | number | The width of an image type of Asset |
| tiff:imageLength | number | The height of an image type of Asset |
| repo:state | string | The `Approved`, `Rejected`, or `Expired`state of an Asset |
| computedMetadata | string | It is an object that represents a bucket for all the Asset's metadata of all kinds (repository, application or embedded metadata) |
| _links | string | It represents the collection of links used in the Asset Selector. The links are represented in the form of an array. The parameters of an array include: `href`, `type`, `repo:size`, `width`, `height`, etc.  |

For the detailed example of Object Schema, click 
-->

## Gestión de la selección de recursos mediante el esquema de objetos {#handling-selection}

La propiedad `handleSelection` se utiliza para gestionar una o varias selecciones de recursos en el Selector de recursos. El ejemplo siguiente indica la sintaxis de uso de `handleSelection`.

![handle-selection](assets/handling-selection.png)

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

El Selector de recursos también le permite cambiar de repositorio para realizar la selección de recursos. Puede seleccionar el repositorio que desee en la lista desplegable disponible en el panel izquierdo. Las opciones del repositorio disponibles en la lista desplegable se basan en la propiedad `repositoryId` definida en el archivo `index.html`. Se basa en los entornos de la organización de IMS seleccionada a la que accede el usuario que ha iniciado sesión. Los consumidores pueden aprobar un `repositoryID` preferido y, en ese caso, el Selector de recursos deja de procesar el conmutador de repositorios y solo procesa los recursos del repositorio dado.
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

Además de la búsqueda de texto completo, el Selector de recursos le permite buscar recursos dentro de los archivos mediante búsquedas personalizadas. Puede utilizar filtros de búsqueda personalizados en los modos Vista modal y Vista de carril.

![custom-search](assets/custom-search.png)

También puede crear un filtro de búsqueda predeterminado para guardar los campos que busca con frecuencia y utilizarlos más adelante. Para crear una búsqueda personalizada de sus recursos, puede utilizar la propiedad `filterSchema`.

### Barra de búsqueda {#search-bar}

El Selector de recursos le permite realizar una búsqueda de texto completo de los recursos del repositorio seleccionado. Por ejemplo, si escribe la palabra clave `wave` en la barra de búsqueda, se muestran todos los recursos con la palabra clave `wave` mencionada en cualquiera de las propiedades de metadatos.

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
*   **Configure** You can configure the files/folders that you want to show at the upfront. The assets that are chosen to view can be of any supported formats, for example, JPEG. It allows you to control the display of various text or symbols as per your choice.
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
*   **Open in media library** Allows you to open the asset in media library.
*   **Upload** Allows you to upload an asset directly.
*   **Download** Downloads the asset in [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
-->
<!--

### Status of an asset

Asset Selector allows you to know the status of your uploaded assets. The status can be `Approved`, `Rejected`, or `Expired` of the asset. 
-->
<!--

### Localization

The integration of Asset Selector with [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] allows localized content appear in your application.
-->