---
title: Selector de recursos para [!DNL Adobe Experience Manager] como un [!DNL Cloud Service]
description: Utilice el selector de recursos para buscar y recuperar metadatos y representaciones de recursos dentro de la aplicación.
contentOwner: KK
feature: Selectors
role: Admin,User
exl-id: 5f962162-ad6f-4888-8b39-bf5632f4f298
source-git-commit: f171bbeaf01e2d9be3a8f3b5172919a5e8ca7d97
workflow-type: tm+mt
source-wordcount: '5418'
ht-degree: 39%

---

# Selector de recursos de Micro-Frontend {#Overview}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime y Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integración de AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>New</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Extensibilidad de la IU</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar Dynamic Media Prime y Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Prácticas recomendadas de búsqueda</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Prácticas recomendadas de metadatos</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Centro de contenido</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funciones de OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentación de desarrollador de AEM Assets</b></a>
        </td>
    </tr>
</table>

El Selector de recursos de Micro-Frontend proporciona una interfaz de usuario que se integra fácilmente con el repositorio de [!DNL Experience Manager Assets] para poder examinar o buscar recursos digitales disponibles en el repositorio y utilizarlos en la experiencia de creación de la aplicación.

La interfaz de usuario de Micro-Frontend está disponible en la experiencia de su aplicación mediante el paquete Selector de recursos. Las actualizaciones del paquete se importan automáticamente y el último Selector de recursos implementado se carga automáticamente en la aplicación.

![Información general](assets/overview.png)

El Selector de recursos ofrece muchas ventajas, como las siguientes:

* Facilidad de integración con cualquiera de las aplicaciones [Adobe](#asset-selector-ims) o [que no son de Adobe](#asset-selector-non-ims) que usan la biblioteca JavaScript de Vanilla.
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
* La URL de la aplicación está en la lista de URL de redirección permitidas del cliente de IMS.
* El flujo de inicio de sesión de IMS se configura y se representa mediante una ventana emergente en el explorador web. Por lo tanto, las ventanas emergentes deben habilitarse o permitirse en el explorador de destino.

Utilice los requisitos previos anteriores si necesita el flujo de trabajo de autenticación IMS del Selector de recursos. Alternativamente, si ya está autenticado con el flujo de trabajo de IMS, puede añadir la información de IMS en su lugar.

>[!IMPORTANT]
>
> Este repositorio está diseñado para servir como documentación suplementaria que describa las API disponibles y ejemplos de uso para la integración del Selector de recursos. Antes de intentar instalar o utilizar el Selector de recursos, asegúrese de que su organización tenga acceso al Selector de recursos como parte del perfil de Experience Manager Assets as a Cloud Service. Si no se le ha proporcionado acceso, no puede integrar ni utilizar estos componentes. Para solicitar el aprovisionamiento, el administrador del programa debe generar un ticket de asistencia marcado como P2 desde Admin Console e incluir la siguiente información:
>
>* Nombres de dominio en los que está alojada la aplicación integradora.
>* Después del aprovisionamiento, se proporcionará a su organización `imsClientId`, `imsScope` y `redirectUrl` correspondientes a los entornos solicitados que son esenciales para la configuración del Selector de recursos. Sin estas propiedades válidas, no se pueden ejecutar los pasos de instalación.

## Instalación {#installation}

El Selector de recursos está disponibles a través de la CDN de ESM (por ejemplo, [esm.sh](https://esm.sh/)/[skypack](https://www.skypack.dev/)) y la versión de [UMD](https://github.com/umdjs/umd).

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

Puede integrar cualquier aplicación [!DNL Adobe] o que no sea de Adobe con el repositorio [!DNL Experience Manager Assets] y seleccionar recursos desde la aplicación. Consulte [Integración del selector de recursos con varias aplicaciones](#asset-selector-integration-with-apps).

La integración se realiza importando el paquete Selector de recursos y conectándose a los Assets as a Cloud Service mediante la biblioteca JavaScript de Vanilla. Edite un `index.html` o cualquier archivo apropiado dentro de su aplicación para:

* Definición de los detalles de autenticación
* Acceso al repositorio Assets as a Cloud Service
* Configurar las propiedades de visualización del Selector de recursos

Puede realizar la autenticación sin definir algunas de las propiedades de IMS, si:

* Está integrando una aplicación de [!DNL Adobe] en [Unified Shell](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=es).
* Ya ha generado un token de IMS para la autenticación.

## Integración del Selector de recursos con varias aplicaciones {#asset-selector-integration-with-apps}

Puede integrar el Selector de recursos con varias aplicaciones, como:

* [Integrar el Selector de recursos con una aplicación  [!DNL Adobe] ](#adobe-app-integration-vanilla)
* [Integre el Selector de recursos con una aplicación que no sea de Adobe](#adobe-non-app-integration)
* [Integración de Dynamic Media con funciones de OpenAPI](#adobe-app-integration-polaris)

>[!BEGINTABS]

<!--Integration with an Adobe application content starts here-->

>[!TAB Integración con una aplicación de Adobe]

### Requisitos previos{#prereqs-adobe-app}

Utilice los siguientes requisitos previos si integra el Selector de recursos con una aplicación de [!DNL Adobe]:

* [Métodos de comunicación](#prereqs)
* imsOrg
* imsToken
* apikey

### Integrar el Selector de recursos con una aplicación [!DNL Adobe] {#adobe-app-integration-vanilla}

En el siguiente ejemplo se muestra el uso del Selector de recursos al ejecutar una aplicación [!DNL Adobe] en Unified Shell o cuando ya se ha generado `imsToken` para la autenticación.

Incluya el paquete Selector de recursos en su código mediante la etiqueta `script`, tal como se muestra en las _líneas 6-15_ del ejemplo siguiente. Una vez cargado el script, la variable global `PureJSSelectors` está disponible para su uso. Defina el Selector de recursos [properties](#asset-selector-properties) como se muestra en _líneas 16-23_. Las propiedades `imsOrg` y `imsToken` son necesarias para la autenticación en la aplicación Adobe. La propiedad de `handleSelection` se utiliza para gestionar los recursos seleccionados. Para procesar el Selector de recursos, llame a la función de `renderAssetSelector` como se menciona en _línea 17_. El Selector de recursos se muestra en el elemento contenedor de `<div>`, como se muestra en las _líneas 21 y 22_.

Si sigue estos pasos, puede usar el Selector de recursos con la aplicación [!DNL Adobe].

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
Las propiedades de `ImsAuthProps` definen la información de autenticación y el flujo que usa el Selector de recursos para obtener un `imsToken`. Al establecer estas propiedades, puede controlar cómo debe comportarse el flujo de autenticación y registrar los agentes de escucha para varios eventos de autenticación.

| Nombre de la propiedad | Descripción |
|---|---|
| `imsClientId` | Valor de cadena que representa el ID de cliente de IMS utilizado con fines de autenticación. Este valor lo proporciona Adobe y es específico de su organización de Adobe AEM CS. |
| `imsScope` | Describe los ámbitos utilizados en la autenticación. Los ámbitos determinan el nivel de acceso que la aplicación tiene a los recursos de su organización. Los ámbitos múltiples se pueden separar con comas. |
| `redirectUrl` | Representa la dirección URL a la que se redirige al usuario después de la autenticación. Este valor se suele establecer en la dirección URL actual de la aplicación. Si no se proporciona `redirectUrl`, `ImsAuthService` usa la redirectUrl utilizada para registrar `imsClientId` |
| `modalMode` | Un booleano que indica si el flujo de autenticación debe mostrarse en un modal (emergente) o no. Si se establece en `true`, el flujo de autenticación se mostrará en una ventana emergente. Si se establece en `false`, el flujo de autenticación se mostrará en una recarga de página completa. _Nota:_ para una mejor experiencia de usuario, puede controlar dinámicamente este valor si el usuario tiene deshabilitada la ventana emergente del explorador. |
| `onImsServiceInitialized` | Una función de llamada de retorno que se llama cuando se inicializa el servicio de autenticación IMS de Adobe. Esta función toma un parámetro, `service`, que es un objeto que representa el servicio IMS de Adobe. Consulte [`ImsAuthService`](#imsauthservice-ims-auth-service) para obtener más detalles. |
| `onAccessTokenReceived` | Una función de llamada de retorno que se llama cuando se recibe un `imsToken` del servicio de autenticación IMS de Adobe. Esta función toma un parámetro, `imsToken`, que es una cadena que representa el token de acceso. |
| `onAccessTokenExpired` | Función de llamada de retorno a la que se llama cuando ha caducado un token de acceso. Esta función se utiliza generalmente para almacenar en déclencheur un nuevo flujo de autenticación para obtener un nuevo token de acceso. |
| `onErrorReceived` | Función de llamada de retorno a la que se llama cuando se produce un error durante la autenticación. Esta función toma dos parámetros: el tipo de error y el mensaje de error. El tipo de error es una cadena que representa el tipo de error y el mensaje de error es una cadena que representa el mensaje de error. |

+++

+++**ImsAuthService**
La clase `ImsAuthService` administra el flujo de autenticación para el Selector de recursos. Es responsable de obtener un `imsToken` del servicio de autenticación IMS de Adobe. `imsToken` se usa para autenticar al usuario y autorizar el acceso a [!DNL Adobe Experience Manager] como un repositorio de Assets de [!DNL Cloud Service]. ImsAuthService usa las propiedades `ImsAuthProps` para controlar el flujo de autenticación y registrar agentes de escucha para varios eventos de autenticación. Puede usar la práctica función [`registerAssetsSelectorsAuthService`](#purejsselectorsregisterassetsselectorsauthservice) para registrar la instancia de _ImsAuthService_ con el Selector de recursos. Las funciones siguientes están disponibles en la clase `ImsAuthService`. Sin embargo, si está utilizando la función _registerAssetsSelectorsAuthService_, no necesita llamar a estas funciones directamente.

| Nombre de función | Descripción |
|---|---|
| `isSignedInUser` | Determina si el usuario ha iniciado sesión en el servicio y devuelve un valor booleano en consecuencia. |
| `getImsToken` | Recupera la autenticación `imsToken` del usuario que ha iniciado sesión actualmente, que se puede utilizar para autenticar solicitudes en otros servicios como la generación de _representación de recursos. |
| `signIn` | Inicia el proceso de inicio de sesión del usuario. Esta función utiliza `ImsAuthProps` para mostrar la autenticación en una ventana emergente o en una recarga de página completa |
| `signOut` | Cierra la sesión del usuario del servicio, invalidando su token de autenticación y obligándole a iniciar sesión de nuevo para acceder a los recursos protegidos. Al invocar esta función, se volverá a cargar la página actual. |
| `refreshToken` | Actualiza el token de autenticación del usuario que ha iniciado sesión, lo que evita que caduque y garantiza un acceso ininterrumpido a los recursos protegidos. Devuelve un nuevo token de autenticación que puede utilizarse para solicitudes posteriores. |

+++

+++**Validación con token de IMS proporcionado**

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

+++**Registrar devoluciones de llamadas al servicio IMS**

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

El Selector de recursos admite la autenticación en el repositorio [!DNL Experience Manager Assets] mediante propiedades de Identity Management System (IMS) como `imsScope` o `imsClientID` cuando se integra con una aplicación que no es de Adobe.

+++**Configurar el Selector de recursos para una aplicación que no es de Adobe**
Para configurar el Selector de recursos para una aplicación que no sea de Adobe, primero debe registrar un ticket de asistencia para el aprovisionamiento seguido de los pasos de integración.

**Registrando un ticket de asistencia**
Pasos para registrar un ticket de asistencia a través de Admin Console:

1. Agregue **Selector de recursos con AEM Assets** en el título del ticket.

1. En la descripción, proporcione los siguientes detalles:

   * [!DNL Experience Manager Assets] como URL de [!DNL Cloud Service] (ID de programa e ID de entorno).
   * Nombres de dominio en los que está alojada la aplicación web que no es de Adobe.
+++

+++**Pasos de integración**
Utilice este archivo de ejemplo `index.html` para la autenticación al integrar el Selector de recursos con una aplicación que no sea de Adobe.

Obtenga acceso al paquete del Selector de recursos mediante la etiqueta `Script`, tal como se muestra en la *línea 9* a la *línea 11* del archivo de ejemplo `index.html`.

*La línea 14* a *línea 38* del ejemplo describe las propiedades de flujo de IMS, como `imsClientId`, `imsScope` y `redirectURL`. La función requiere que defina al menos una de las propiedades `imsClientId` y `imsScope`. Si no define un valor para `redirectURL`, se utilizará la dirección URL de redireccionamiento registrada para el ID de cliente.

Dado que no se ha generado ningún `imsToken`, use las funciones `registerAssetsSelectorsAuthService` y `renderAssetSelectorWithAuthFlow`, como se muestra en la línea 40 a la línea 50 del archivo de ejemplo `index.html`. Use la función `registerAssetsSelectorsAuthService` antes de `renderAssetSelectorWithAuthFlow` para registrar `imsToken` con el Selector de recursos. [!DNL Adobe] recomienda llamar a `registerAssetsSelectorsAuthService` al crear una instancia del componente.

Defina la autenticación y otras propiedades relacionadas con el acceso a Assets as a Cloud Service en la sección `const props`, como se muestra en la *línea 54* a la *línea 60* del archivo de ejemplo `index.html`.

La variable global `PureJSSelectors`, mencionada en la *línea 65*, se usa para procesar el Selector de recursos en el explorador web.

El selector de recursos se procesa en el elemento contenedor `<div>`, como se menciona en la *línea 74* a la *línea 81*. En el ejemplo se utiliza un cuadro de diálogo para mostrar el Selector de recursos.

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
>Si ha integrado el Selector de recursos mediante el flujo de trabajo de registro de inicio de sesión, pero sigue sin poder acceder al repositorio de envío, asegúrese de que las cookies del explorador se limpien. De lo contrario, obtendrá el error `invalid_credentials All session cookies are empty` en la consola.

+++

<!--Integration with Polaris application content starts here-->

>[!TAB Integración de Dynamic Media con funciones OpenAPI]

### Requisitos previos {#prereqs-polaris}

Utilice los siguientes requisitos previos si integra el Selector de recursos con Dynamic Media con las capacidades de OpenAPI:

* [Métodos de comunicación](#prereqs)
* Para acceder a Dynamic Media con las funciones de OpenAPI, debe tener licencias para:
   * Repositorio de Assets (por ejemplo, Experience Manager Assets as a Cloud Service).
   * AEM Dynamic Media.
* Solo hay [recursos aprobados](#approved-assets.md) disponibles para usar, lo que garantiza la coherencia de la marca.

### Integración de Dynamic Media con funciones de OpenAPI{#adobe-app-integration-polaris}

La integración del Selector de recursos con el proceso OpenAPI de Dynamic Media implica varios pasos, entre los que se incluye la creación de una URL de Dynamic Media personalizada o una URL de Dynamic Media lista para elegir, etc.

+++**Integrar el Selector de recursos para Dynamic Media con las capacidades de OpenAPI**

Las propiedades `rootPath` y `path` no deben formar parte de Dynamic Media con capacidades de OpenAPI. En su lugar, puede configurar la propiedad `aemTierType`. A continuación se muestra la sintaxis de la configuración:

```
aemTierType:[1: "delivery"]
```

Esta configuración le permite ver todos los recursos aprobados sin carpetas o como una estructura plana. Para obtener más información, vaya a la propiedad `aemTierType` en [Propiedades del selector de recursos](#asset-selector-properties)

+++

+++**Crear una URL de envío dinámico a partir de recursos aprobados**
Una vez configurado el Selector de recursos, se utiliza un esquema de objetos para crear una URL de envío dinámico a partir de los recursos seleccionados.
Por ejemplo, un esquema de un objeto de una matriz de objetos que se recibe al seleccionar un recurso:

```
{
"dc:format": "image/jpeg",
"repo:assetId": "urn:aaid:aem:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
"repo:name": "image-7.jpg",
"repo:repositoryId": "delivery-pxxxx-exxxxxx.adobe.com",
...
}
```

La función `handleSelection` que actúa como objeto JSON lleva todos los recursos seleccionados. Por ejemplo, `JsonObj`. La URL de envío dinámico se crea combinando los siguientes operadores:

| Objeto | JSON |
|---|---|
| Host | `assetJsonObj["repo:repositoryId"]` |
| Raíz API | `/adobe/assets` |
| asset-id | `assetJsonObj["repo:assetId"]` |
| seo-name | `assetJsonObj["repo:name"].split(".").slice(0,-1).join(".")` |
| formato | `.jpg` |

**Especificación de API de entrega de recursos aprobada**

Formato de URL:
`https://<delivery-api-host>/adobe/assets/<asset-id>/as/<seo-name>.<format>?<image-modification-query-parameters>`

Donde,

* El host es `https://delivery-pxxxxx-exxxxxx.adobe.com`
* La raíz de API es `"/adobe/assets"`
* `<asset-id>` es el identificador del recurso
* `as` es la parte constante de la especificación de API abierta que indica a qué se puede hacer referencia el recurso
* `<seo-name>` es el nombre de un recurso
* `<format>` es el formato de salida
* `<image modification query parameters>` es compatible con la especificación de API de entrega de recursos aprobados

**API de entrega de representación original de recursos aprobados**

La dirección URL de envío dinámico tiene la siguiente sintaxis:
`https://<delivery-api-host>/adobe/assets/<asset-id>/original/as/<seo-name>`, donde,

* El host es `https://delivery-pxxxxx-exxxxxx.adobe.com`
* La raíz de la API para la entrega de la representación original es `"/adobe/assets"`
* `<asset-id>` es el identificador de recurso
* `/original/as` es la parte constante de la especificación de API abierta que indica a qué se puede hacer referencia en la representación original
* `<seo-name>` es el nombre del recurso que puede tener o no una extensión

+++

+++**Listo para elegir la URL de envío dinámico**
Todos los recursos seleccionados están a cargo de la función `handleSelection` que actúa como objeto JSON. Por ejemplo, `JsonObj`. La URL de envío dinámico se crea combinando los siguientes operadores:

| Objeto | JSON |
|---|---|
| Host | `assetJsonObj["repo:repositoryId"]` |
| Raíz API | `/adobe/assets/deliver` |
| asset-id | `assetJsonObj["repo:assetId"]` |
| seo-name | `assetJsonObj["repo:name"]` |

A continuación se muestran las dos formas de atravesar el objeto JSON:

![URL de envío dinámico](assets/dynamic-delivery-url.png)

* **Miniatura:** Las miniaturas pueden ser imágenes y recursos como PDF, vídeo, imágenes, etc. Sin embargo, puede utilizar los atributos de altura y anchura de la miniatura de un recurso como representación de envío dinámico.
Se puede utilizar el siguiente conjunto de representaciones para los recursos de tipo PDF:
Una vez que se selecciona un pdf en la barra de tareas, el contexto de selección ofrece la siguiente información. A continuación se muestra la forma de atravesar el objeto JSON:

  <!--![Thumbnail dynamic delivery url](image-1.png)-->

  Puede hacer referencia a `selection[0].....selection[4]` para la matriz de vínculos de representación desde la captura de pantalla anterior. Por ejemplo, las propiedades clave de una de las representaciones de miniaturas incluyen:

  ```
  { 
      "height": 319, 
      "width": 319, 
      "href": "https://delivery-pxxxxx-exxxxx.adobeaemcloud.com/adobe/assets/urn:aaid:aem:8560f3a1-d9cf-429d-a8b8-d81084a42d41/as/algorithm design.jpg?width=319&height=319", 
      "type": "image/webp" 
  } 
  ```

En la captura de pantalla anterior, la dirección URL de envío de la representación original de PDF debe incorporarse en la experiencia de destino si se requiere PDF y no su miniatura. Por ejemplo, `https://delivery-pxxxxx-exxxxx-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:8560f3a1-d9cf-429d-a8b8-d81084a42d41/original/as/algorithm design.pdf`

* **Vídeo:** Puede usar la URL del reproductor de vídeo para los recursos de tipo de vídeo que usan un iFrame incrustado. Puede utilizar las siguientes representaciones de matrices en la experiencia de Target:
  <!--![Video dynamic delivery url](image.png)-->

  ```
  { 
      "height": 319, 
      "width": 319, 
      "href": "https://delivery-pxxxxx-exxxxx.adobeaemcloud.com/adobe/assets/urn:aaid:aem:2fdef732-a452-45a8-b58b-09df1a5173cd/as/asDragDrop.2.jpg?width=319&height=319", 
      "type": "image/webp" 
  } 
  ```

  Puede hacer referencia a `selection[0].....selection[4]` para la matriz de vínculos de representación desde la captura de pantalla anterior. Por ejemplo, las propiedades clave de una de las representaciones de miniaturas incluyen:

  El fragmento de código de la captura de pantalla anterior es un ejemplo de un recurso de vídeo. Incluye la matriz de vínculos de representaciones. El `selection[5]` del extracto es el ejemplo de una miniatura de imagen que puede utilizarse como marcador de posición de una miniatura de vídeo en la experiencia de destino. `selection[5]` en la matriz de representaciones es para el reproductor de vídeo. Esto sirve un HTML y se puede establecer como `src` del iframe. Admite flujo de velocidad de bits adaptable, que es una entrega del vídeo optimizada para la web.

  En el ejemplo anterior, la dirección URL del reproductor de vídeo es `https://delivery-pxxxxx-exxxxx.adobeaemcloud.com/adobe/assets/urn:aaid:aem:2fdef732-a452-45a8-b58b-09df1a5173cd/play`

+++**Interfaz de usuario del Selector de recursos para Dynamic Media con capacidades OpenAPI**

Después de la integración con el Selector de recursos de Micro-FrontEnd de Adobe, puede ver la estructura de recursos solamente de todos los recursos aprobados disponibles en el repositorio de recursos de Experience Manager.

![Dynamic Media con la IU de capacidades de OpenAPI](assets/polaris-ui.png)

* **A**: [Ocultar/Mostrar panel](#hide-show-panel)
* **B**: [Assets](#repository)
* **C**: [Ordenando](#sorting)
* **D**: [Filtros](#filters)
* **E**: [Barra de búsqueda](#search-bar)
* **F**: [Orden ascendente o descendente](#sorting)
* **G**: Cancelar Selección
* **H**: seleccione uno o varios recursos

+++

+++**Configurar filtros personalizados**
El Selector de recursos para Dynamic Media con funciones de OpenAPI le permite configurar propiedades personalizadas y los filtros basados en ellas. La propiedad `filterSchema` se usa para configurar dichas propiedades. La personalización puede exponerse como `metadata.<metadata bucket>.<property name>.`, en función de la cual se pueden configurar los filtros, donde,

* `metadata` es la información de un recurso
* `embedded` es el parámetro estático utilizado para la configuración, y
* `<propertyname>` es el nombre de filtro que está configurando

Para la configuración, las propiedades definidas en el nivel `jcr:content/metadata/` se exponen como `metadata.<metadata bucket>.<property name>.` para los filtros que desea configurar.

Por ejemplo, en el Selector de recursos para Dynamic Media con capacidades OpenAPI, una propiedad de `asset jcr:content/metadata/client_name:market` se convierte en `metadata.embedded.client_name:market` para la configuración de filtros.

Para obtener el nombre, se debe realizar una actividad única. Realice una llamada a la API de búsqueda del recurso y obtenga el nombre de la propiedad (el contenedor, en esencia).

+++

>[!ENDTABS]

## Propiedades del Selector de recursos {#asset-selector-properties}

Puede utilizar las propiedades del Selector de recursos para personalizar la forma en que se procesa el Selector de recursos. En la tabla siguiente se enumeran las propiedades que puede utilizar para personalizar y utilizar el Selector de recursos.

| Propiedad | Tipo | Requerido | Predeterminado | Descripción |
|---|---|---|---|---|
| *carril* | Booleano | No | Falso | Si se marca `true`, el Selector de recursos se representa en una vista del carril izquierdo. Si está marcado como `false`, el Selector de recursos se representa en la vista modal. |
| *imsOrg* | Cadena | Sí | | ID del sistema Identity Management de Adobe (IMS) asignado durante el aprovisionamiento [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] para su organización. La clave `imsOrg` es necesaria para autenticar si la organización a la que accede se encuentra en Adobe IMS o no. |
| *imsToken* | Cadena | No | | Token de portador de IMS utilizado para la autenticación. `imsToken` es necesario si utiliza una aplicación [!DNL Adobe] para la integración. |
| *apiKey* | Cadena | No | | Clave de API utilizada para acceder al servicio AEM Discovery. `apiKey` es necesario si utiliza una integración de aplicación [!DNL Adobe]. |
| *filterSchema* | Matriz | No | | Modelo que se utiliza para configurar las propiedades del filtro. Esto resulta útil cuando desea limitar ciertas opciones de filtro en el Selector de recursos. |
| *filterFormProps* | Objeto | No | | Especifique las propiedades del filtro que debe utilizar para restringir la búsqueda. ¡Por! Por ejemplo, tipo MIME JPG, PNG, GIF. |
| *selectedAssets* | Matriz `<Object>` | No |                 | Especificar los recursos seleccionados cuando se procese el selector de recursos. Se requiere una matriz de objetos que contenga una propiedad id de los recursos. Por ejemplo, `[{id: 'urn:234}, {id: 'urn:555'}]` Un recurso debe estar disponible en el directorio actual. Si necesita utilizar un directorio diferente, proporcione un valor para la propiedad de `path` también. |
| *acvConfig* | Objeto | No | | Propiedad de vista de colección de recursos que contiene un objeto con una configuración personalizada para anular los valores predeterminados. Además, esta propiedad se usa con la propiedad `rail` para habilitar la vista de carril del visor de recursos. |
| *i18nSymbols* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | No |                 | Si las traducciones OOTB no son suficientes para las necesidades de la aplicación, puede exponer una interfaz a través de la cual puede pasar sus propios valores localizados personalizados mediante la propiedad `i18nSymbols`. Al pasar un valor a través de esta interfaz, se anulan las traducciones predeterminadas proporcionadas y, en su lugar, se utilizan las suyas. Para realizar la anulación, debe pasar un objeto [Descriptor del mensaje](https://formatjs.io/docs/react-intl/api/#message-descriptor) válido a la clave de `i18nSymbols` que desee anular. |
| *intl* | Objeto | No | | El Selector de recursos proporciona traducciones OOTB predeterminadas. Puede seleccionar el idioma de traducción proporcionando una cadena de configuración regional válida a través del prop `intl.locale`. Por ejemplo: `intl={{ locale: "es-es" }}` </br></br> Las cadenas de configuración regional admitidas siguen los [Códigos ISO 639](https://www.iso.org/iso-639-language-codes.html) para la representación de los estándares de nombres de idiomas. </br></br> Lista de configuraciones regionales admitidas: Inglés - &#39;en-us&#39; (predeterminado) Español - &#39;es-es&#39; Alemán - &#39;de-de&#39; Francés - &#39;fr-fr&#39; Italiano - &#39;it-it&#39; Japonés - &#39;ja-jp&#39; Coreano - &#39;ko-kr&#39; Portugués - &#39;pt-br&#39; Chino (tradicional) - &#39;zh-cn&#39; Chino (Taiwán) - &#39;zh-tw&#39; |
| *repositoryId* | Cadena | No | &#39;&#39; | Repositorio desde el que el Selector de recursos carga el contenido. |
| *additionalAemSolutions* | `Array<string>` | No | [ ] | Permite añadir una lista de repositorios de AEM adicionales. Si no se proporciona información en esta propiedad, solo se tienen en cuenta los repositorios de la biblioteca de medios o de AEM Assets. |
| *hideTreeNav* | Booleano | No |  | Especifica si se muestra u oculta la barra lateral de navegación del árbol de recursos. Solo se utiliza en la vista modal y, por lo tanto, no hay ningún efecto de esta propiedad en la vista de carril. |
| *onDrop* | Función | No | | La propiedad permite la funcionalidad de colocación de un recurso. |
| *dropOptions* | `{allowList?: Object}` | No | | Configura las opciones de colocación mediante &#39;allowList&#39;. |
| *colorScheme* | Cadena | No | | Configurar tema (`light` o `dark`) para el Selector de recursos. |
| *handleSelection* | Función | No | | Se invoca con la matriz de elementos de recurso cuando se seleccionan los recursos y se hace clic en el botón `Select` en el modal. Esta función solo se invoca en la vista modal. Para la vista de carril, utilice las funciones `handleAssetSelection` o `onDrop`. Ejemplo: <pre>handleSelection=(recursos: Asset[])=> {...}</pre> Consulte [Tipo de recurso seleccionado](#selected-asset-type) para obtener más información. |
| *handleAssetSelection* | Función | No | | Se invoca con una matriz de elementos cuando los recursos se seleccionan o no. Esto resulta útil cuando desea escuchar los recursos a medida que el usuario los selecciona. Ejemplo: <pre>handleSelection=(recursos: Asset[])=> {...}</pre> Consulte [Tipo de recurso seleccionado](#selected-asset-type) para obtener más información. |
| *onClose* | Función | No | | Se invoca cuando se pulsa el botón `Close` en la vista modal. Esto solo se llama en la vista `modal` y se ignora en la vista `rail`. |
| *onFilterSubmit* | Función | No | | Se invoca con elementos de filtro cuando el usuario cambia criterios de filtro diferentes. |
| *selectionType* | Cadena | No | Soltero/a | Configuración para selección de `single` o `multiple` de recursos a la vez. |
| *dragOptions.lista de permitidos* | booleano | No | | La propiedad se utiliza para permitir o denegar el arrastre de recursos que no se pueden seleccionar. |
| *aemTierType* | Cadena | No |  | Permite seleccionar si desea mostrar los recursos del nivel de entrega, del nivel de creación o de ambos. Sintaxis <br><br>: `aemTierType:[0]: "author" 1: "delivery"` <br><br> Por ejemplo, si se usan `["author","delivery"]`, el conmutador de repositorios mostrará opciones de autor y envío. |
| *handleNavigateToAsset* | Función | No | | Es una función de llamada de retorno para gestionar la selección de un recurso. |
| *noWrap* | Booleano | No | | La propiedad *noWrap* ayuda a procesar el Selector de recursos en el panel de raíl lateral. Si no se menciona esta propiedad, se representa la *vista del cuadro de diálogo* de forma predeterminada. |
| *dialogSize* | adquisición en pequeña, mediana, grande, pantalla completa o pantalla completa | Cadena | Opcional | Puede controlar el diseño especificando su tamaño con las opciones dadas. |
| *colorScheme* | Claro u oscuro | No | | Esta propiedad se utiliza para establecer la temática de una aplicación Selector de recursos. Puede elegir entre tema claro u oscuro. |
| *filterRepoList* | Función | No |  | Puede utilizar la función de devolución de llamada `filterRepoList` que llama al repositorio de Experience Manager y devuelve una lista filtrada de repositorios. |
| *expiryOptions* | Función | | | Puede usar entre las dos propiedades siguientes: **getExpiryStatus**, que proporciona el estado de un recurso caducado. La función devuelve `EXPIRED`, `EXPIRING_SOON` o `NOT_EXPIRED` según la fecha de caducidad del recurso que proporcione. Consulte [personalizar recursos caducados](#customize-expired-assets). Además, puede usar **allowSelectionAndDrag**, en el que el valor de la función puede ser `true` o `false`. Cuando el valor se establece en `false`, el recurso caducado no se puede seleccionar ni arrastrar al lienzo. |
| *showToast* | | No | | Permite que el Selector de recursos muestre un mensaje de mensaje personalizado para el recurso caducado. |

<!--
| *rootPath* | String | No | /content/dam/ | Folder path from which Asset Selector displays your assets. `rootPath` can also be used in the form of encapsulation. For example, given the following path, `/content/dam/marketing/subfolder/`, Asset Selector does not allow you to traverse through any parent folder, but only displays the children folders. |
| *path* | String | No | | Path that is used to navigate to a specific directory of assets when the Asset Selector is rendered. |
| *expirationDate* | Function | No | | This function is used to set the usability period of an asset. |
| *disableDefaultBehaviour* | Boolean | No | False | It is a function that is used to enable or disable the selection of an expired asset. You can customize the default behavior of an asset that is set to expire. See [customize expired assets](#customize-expired-assets). |
-->

## Ejemplos de uso de las propiedades del Selector de recursos {#usage-examples}

Puede definir las [propiedades](#asset-selector-properties) del Selector de recursos en el archivo `index.html` para personalizar la visualización del Selector de recursos en la aplicación.

### Ejemplo 1: Selector de recursos en la vista de carril

![rail-view-example](assets/rail-view-example-vanilla.png)

Si el valor de AssetSelector `rail` está establecido en `false` o no se menciona en las propiedades, el Selector de recursos se muestra en la vista modal de forma predeterminada. La propiedad `acvConfig` permite algunas configuraciones en profundidad, como Arrastrar y soltar. Visite [habilitar o deshabilitar arrastrar y soltar](#enable-disable-drag-and-drop) para comprender el uso de la propiedad `acvConfig`.

<!--
### Example 2: Use selectedAssets property in addition to the path property

Use the `path` property to define the folder name that displays automatically when the Asset Selector is rendered. In addition, use the `selectedAssets` property to define the IDs for the assets that you need to select within the folder. Moreover, when you want to display assets that are pre-defined within the folder, you can use selectedAssets property.

   ![selected-assets-example](assets/selected-assets-example-vanilla.png)
-->

### Ejemplo 2: ventana emergente de metadatos

Utilice varias propiedades para definir los metadatos de un recurso que desee ver mediante un icono de información. La ventana emergente de información proporciona la colección de información sobre el recurso o la carpeta, incluido el título, las dimensiones, la fecha de modificación, la ubicación y la descripción de un recurso. En el ejemplo siguiente, se utilizan varias propiedades para mostrar los metadatos de un recurso, por ejemplo: la propiedad `repo:path` especifica la ubicación de un recurso. <!--`repo` represents the repository from where the asset is showing, whereas, `path` represents the route from where the asset or folder is rendered.-->

![metadata-popover-example](assets/metadata-popover.png)

### Ejemplo 3: Propiedad de filtro personalizado en la vista de carril

Además de la búsqueda con facetas, el Selector de Assets le permite personalizar varios atributos para restringir la búsqueda de [!DNL Adobe Experience Manager] como una aplicación [!DNL Cloud Service]. Agregue el siguiente código para agregar filtros de búsqueda personalizados en la aplicación. En el ejemplo siguiente, la búsqueda `Type Filter` que filtra el tipo de recurso entre imágenes, documentos o vídeos o el tipo de filtro que ha agregado para la búsqueda.

![custom-filter-example-vanilla](assets/custom-filter-example-vanilla.png)

<!--

## Customization after integrating Asset Selector 

### Custom metadata

Assets display panel shows the out of the box metadata that can be displayed in the info of the asset. In addition to this, [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application allows configuration of the asset selector by adding custom metadata that is shown in info panel of the asset.
-->

## Fragmentos de código de configuración funcional{#code-snippets}

Defina los requisitos previos en el archivo `index.html` o un archivo similar dentro de la implementación de la aplicación para definir los detalles de autenticación para acceder al repositorio [!DNL Experience Manager Assets]. Una vez finalizado, puede agregar fragmentos de código según sus necesidades.

### Personalizar panel de filtro {#customize-filter-panel}

Puede agregar el siguiente fragmento de código en el objeto `assetSelectorProps` para personalizar el panel de filtro:

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

Puede personalizar la vista de detalles de un recurso al hacer clic en el icono ![información](assets/info-icon.svg). Ejecute el siguiente código:

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

Agregue las siguientes propiedades a `assetSelectorProp` para habilitar el modo de arrastrar y soltar. Para deshabilitar la función de arrastrar y soltar, reemplace el parámetro `true` por `false`.

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

### Selección de Assets {#selection-of-assets}

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
| *_vínculos.<https://ns.adobe.com/adobecloud/rel/rendition[].repo:size>&#39;* | número | El tamaño de la representación en bytes. |
| *_vínculos.<https://ns.adobe.com/adobecloud/rel/rendition[].width>* | número | La anchura de la representación. |
| *_vínculos.<https://ns.adobe.com/adobecloud/rel/rendition[].height>* | número | Altura de la representación. |

<!--For a complete list of properties and detailed example, visit [Asset Selector Code Example](https://github.com/adobe/aem-assets-selectors-mfe-examples).-->

### Personalizar recursos caducados {#customize-expired-assets}

El Selector de recursos permite controlar el uso de un recurso caducado. Puede personalizar el recurso caducado con un distintivo de **Vencimiento pronto** que le ayudará a conocer de antemano los recursos que caducarán dentro de los 30 días posteriores a la fecha actual. Además, esto se puede personalizar según el requisito. También puede permitir la selección de un recurso caducado en el lienzo o viceversa. La personalización de un recurso caducado se puede realizar mediante algunos fragmentos de código de varias formas:

<!--{
    getExpiryStatus: function, // to control Expired/Expiring soon badges of the asset
    allowSelectionAndDrag: boolean, // set true to allow the selection of expired assets on canvas, set false, otherwise.
}-->

```
expiryOptions: {
    getExpiryStatus: getExpiryStatus;
}
```

#### Selección de un recurso caducado {#selection-of-expired-asset}

Puede personalizar el uso de un recurso caducado para que se pueda seleccionar o no. Puede personalizar si desea permitir o no la operación de arrastrar y soltar un recurso caducado en el lienzo del Selector de recursos. Para ello, utilice los siguientes parámetros para que un recurso no se pueda seleccionar en el lienzo:

```
expiryOptions:{
    allowSelectionAndDrop: false;
}
```
<!--
Additionally, To do this, navigate to **[!UICONTROL Disable default expiry behavior]** under the [!UICONTROL Controls] tab and set the boolean value to `true` or `false` as per the requirement. If `true` is selected, you can see the select box over the expired asset, otherwise it remains unselected. You can hover to the info icon of an asset to know the details of an expired asset. 

![Disable default expiry behavior](assets/disable-default-expiry-behavior.png)-->

#### Configuración de la duración de un recurso caducado {#set-duration-of-expired-asset}

El siguiente fragmento de código le ayuda a establecer el distintivo **caducará pronto** para los recursos que caduquen en los próximos cinco días: <!--The `expirationDate` property is used to set the expiration duration of an asset. Refer to the code snippet below:-->

```
/**
  const getExpiryStatus = async (asset) => {
  if (!asset.expirationDate) {
    return null;
  }
  const currentDate = new Date();
  const millisecondsInDay = 1000 * 60 * 60 * 24;
  const fiveDaysFromNow = new Date(value: currentDate.getTime() + 5 * millisecondsInDay);
  const expirationDate = new Date(asset.expirationDate);
  if (expirationDate.getTime() < currentDate.getTime()) {
    return 'EXPIRED';
  } else if (expirationDate.getTime() < fiveDaysFromNow.getTime()) {
    return 'EXPIRING_SOON';
  } else {
    return 'NOT_EXPIRED';
  }
};
```

<!--In the above code snippet, the `getExpiryStatus` function is used to show the **Expiring soon** badge that have expiration date stored in `customExpirationDate`. Additionally, it sets the expiration date of an asset to five days from the current date. The `millisecondsInDay` helps you set expiry of an asset by specifying the time range in milliseconds. You can replace milliseconds with hours directly or customize function as per the requirement. Whereas, the `getTime()` function returns the number of milliseconds for the mentioned date. See [properties](#asset-selector-properties) to know about `expirationDate` property.-->

Consulte el siguiente ejemplo para comprender cómo funciona la propiedad para recuperar la fecha y la hora actuales:

```
const currentData = new Date();
currentData.getTime(),
```

devuelve `1718779013959`, que es según el formato de fecha 2024-06-19T06:36:53.959Z.

#### Personalizar el mensaje de mensaje de un recurso caducado {#customize-toast-message}

La propiedad `showToast` se usa para personalizar el mensaje de mensaje que desea mostrar en un recurso caducado.

Sintaxis:

```
{
    type: 'ERROR', 'NEUTRAL', 'INFO', 'SUCCESS',
    message: '<message to be shown>',
    timeout: optional,
}
```

El tiempo de espera predeterminado es de 500 milisegundos. Por su parte, puede modificarla según los requisitos. Además, al pasar el valor `timeout: 0`, se mantiene abierto el mensaje hasta que se hace clic en el botón cruzado.

A continuación se muestra un ejemplo para mostrar un mensaje de mensaje cuando es necesario impedir la selección de una carpeta y mostrar un mensaje correspondiente:

```
const showToast = {
    type: 'ERROR',
    message: 'Folder cannot be selected',
    timeout: 5000,
}
```

Utilice el siguiente fragmento de código para mostrar el mensaje de mensaje para el uso de un recurso caducado:

![mensaje de mensaje](assets/toast-message.png)

### Filtro de invocación contextual{#contextual-invocation-filter}

El Selector de recursos le permite agregar un filtro de selector de etiquetas. Admite un grupo de etiquetas que combina todas las etiquetas relevantes con un grupo de etiquetado concreto. Además, le permite seleccionar etiquetas adicionales correspondientes al recurso que está buscando. Además, también puede establecer los grupos de etiquetas predeterminados en el filtro de invocación contextual que utiliza principalmente para que le sean accesibles en sus desplazamientos.

>
>
> * Se debe añadir un fragmento de código de invocación contextual para habilitar el filtro de etiquetado en la búsqueda.
> * Es obligatorio usar la propiedad name correspondiente al tipo de grupo de etiquetas `(property=xcm:keywords.id=)`.

Sintaxis:

```
const filterSchema=useMemo(() => {
    return: [
        {
            element: 'taggroup',
            name: 'property=xcm:keywords.id='
        },
    ];
}, []);
```

Para agregar grupos de etiquetas en el panel Filtros, es obligatorio agregar al menos un grupo de etiquetas como predeterminado. Además, utilice el siguiente fragmento de código para añadir las etiquetas predeterminadas preseleccionadas del grupo de etiquetas.

```
export const WithAssetTags = (props) = {
const [selectedTags, setSelectedTags] = useState (
new Set(['orientation', 'color', 'facebook', 'experience-fragments:', 'dam', 'monochrome'])
const handleSelectTags = (selected) => {
setSelectedTags (new Set (selected)) ;
};
const filterSchema = useMemo ((); => {
    return {
        schema: [
            ｛
                fields: [
                    {
                    element: 'checkbox', 
                    name: 'property=xcm:keywords=', 
                    defaultValue: Array. from(selectedTags), 
                    options: assetTags, 
                    orientation: 'vertical',
                    },
                ],
    header: 'Asset Tags', 
    groupkey: 'AssetTagsGroup',
        ],
    },
｝；
}, [selectedTags]);
```

![filtro de grupo de etiquetas](assets/tag-group.gif)

## Gestión de la selección de recursos mediante el esquema de objetos {#handling-selection}

La propiedad `handleSelection` se utiliza para gestionar una o varias selecciones de recursos en el Selector de recursos. El ejemplo siguiente indica la sintaxis de uso de `handleSelection`.

![handle-selection](assets/handling-selection.png)

## Desactivación de la selección de Assets {#disable-selection}

Deshabilitar selección se utiliza para ocultar o deshabilitar la selección de recursos o carpetas. Oculta la casilla de verificación de selección de la tarjeta o el recurso, lo que impide que se seleccione. Para utilizar esta función, puede declarar la posición de un recurso o carpeta que desee deshabilitar en una matriz. Por ejemplo, si desea deshabilitar la selección de una carpeta que aparece en la primera posición, puede agregar el siguiente código:
`disableSelection: [0]:folder`

Puede proporcionar a la matriz una lista de tipos MIME (como imagen, carpeta, archivo u otros tipos MIME, por ejemplo, imagen/jpeg) que desee desactivar. Los tipos MIME que declare se asignan a los atributos `data-card-type` y `data-card-mimetype` de un recurso.

Además, se pueden arrastrar Assets con la selección deshabilitada. Para deshabilitar la función de arrastrar y soltar de un tipo de recurso concreto, puede utilizar la propiedad `dragOptions.allowList`.

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

El Selector de recursos también le permite cambiar de repositorio para realizar la selección de recursos. Puede seleccionar el repositorio que desee en la lista desplegable disponible en el panel izquierdo. Las opciones del repositorio disponibles en la lista desplegable se basan en la propiedad `repositoryId` definida en el archivo `index.html`. Se basa en los entornos de la organización de IMS seleccionada a la que accede el usuario que ha iniciado sesión. Los consumidores pueden aprobar un `repositoryID` preferido y, en ese caso, el Selector de recursos deja de procesar el conmutador de repositorios y solo procesa los recursos del repositorio dado.

### Repositorio de recursos

Es una colección de carpetas de recursos que puede utilizar para realizar operaciones.

### Filtros listos para usar {#filters}

El Selector de recursos también proporciona opciones de filtro listas para usar para restringir los resultados de búsqueda. Los filtros disponibles son los siguientes:

* **[!UICONTROL Estado]:** es el estado actual del recurso, que puede ser `all`, `approved`, `rejected` o `no status`.
* **[!UICONTROL Tipo de archivo]:** incluye `folder`, `file`, `images`, `documents` o `video`.
* **[!UICONTROL Estado de caducidad]:** señala la duración de la caducidad de los recursos. Puede marcar la casilla de verificación `[!UICONTROL Expired]` para filtrar los recursos que han caducado o establecer el elemento `[!UICONTROL Expiration Duration]` de un recurso para mostrar los recursos en función de la duración de su caducidad. Cuando un recurso ya ha caducado o está a punto de caducar, aparece un distintivo que muestra lo mismo. Además, puede decidir si desea permitir el uso (o arrastrar y soltar) de un recurso caducado. Más información sobre [personalizar recursos caducados](#customize-expired-assets). De manera predeterminada, se muestra el distintivo **Vence pronto** para los recursos que caduquen en los próximos 30 días. Sin embargo, puede configurar la caducidad mediante la propiedad `expirationDate`.

  >[!TIP]
  >
  > Si desea ver o filtrar recursos en función de su fecha de caducidad futura, mencione el intervalo de fechas futuras en el campo `[!UICONTROL Expiration Duration]`. Muestra los recursos que tienen el distintivo **caducará pronto**.

* **[!UICONTROL Tipo MIME]:** incluye `JPG`, `GIF`, `PPTX`, `PNG`, `MP4`, `DOCX`, `TIFF`, `PDF`, `XLSX`.
* **[!UICONTROL Tamaño de la imagen]:** incluye la anchura mínima/máxima y la altura mínima/máxima de la imagen.

  ![rail-view-example](assets/filters-asset-selector.png)

### Búsqueda personalizada

Además de la búsqueda de texto completo, el Selector de recursos le permite buscar recursos dentro de los archivos mediante búsquedas personalizadas. Puede utilizar filtros de búsqueda personalizados en los modos Vista modal y Vista de carril.

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
