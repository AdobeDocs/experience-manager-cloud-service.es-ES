---
title: 'Integrar el Selector de recursos con la aplicación  [!DNL Adobe] '
description: Integre el selector de recursos con varias aplicaciones de Adobe, que no sean de Adobe y de terceros.
role: Admin, User
exl-id: a0c030e2-2213-406b-ad92-4761f1e2ee9f
source-git-commit: 08fc43bc8edeea91bfeb01f053d435e136658e7f
workflow-type: tm+mt
source-wordcount: '813'
ht-degree: 15%

---

# Integración del Selector de recursos con la aplicación de Adobe {#integrate-asset-selector-with-adobe-app}

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

El Selector de recursos le permite integrarse utilizando varias aplicaciones de Adobe para permitir que funcionen juntas sin problemas.

## Requisitos previos{#prereqs-adobe-app}

Utilice los siguientes requisitos previos si integra el Selector de recursos con una aplicación de [!DNL Adobe]:

* [Métodos de comunicación](/help/assets/overview-asset-selector.md#prereqs)
* imsOrg
* imsToken
* apikey

## Integrar el Selector de recursos con una aplicación [!DNL Adobe] {#adobe-app-integration-vanilla}

En el siguiente ejemplo se muestra el uso del Selector de recursos al ejecutar una aplicación [!DNL Adobe] en Unified Shell o cuando ya se ha generado `imsToken` para la autenticación.

Incluya el paquete Selector de recursos en su código mediante la etiqueta `script`, tal como se muestra en las _líneas 6-15_ del ejemplo siguiente. Una vez cargado el script, la variable global `PureJSSelectors` está disponible para su uso. Defina el Selector de recursos [properties](/help/assets/asset-selector-properties.md) como se muestra en _líneas 16-23_. Las propiedades `imsOrg` y `imsToken` son necesarias para la autenticación en la aplicación Adobe. La propiedad de `handleSelection` se utiliza para gestionar los recursos seleccionados. Para procesar el Selector de recursos, llame a la función de `renderAssetSelector` como se menciona en _línea 17_. El Selector de recursos se muestra en el elemento contenedor de `<div>`, como se muestra en las _líneas 21 y 22_.

Si sigue estos pasos, puede usar el Selector de recursos con la aplicación [!DNL Adobe].

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
    <title>Asset Selector</title>
    <script src="https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js"></script>
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

### ImsAuthProps {#ims-auth-props}

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

### ImsAuthService {#ims-auth-service}

La clase `ImsAuthService` administra el flujo de autenticación para el Selector de recursos. Es responsable de obtener un `imsToken` del servicio de autenticación IMS de Adobe. `imsToken` se usa para autenticar al usuario y autorizar el acceso a [!DNL Adobe Experience Manager] como un repositorio de Assets de [!DNL Cloud Service]. ImsAuthService usa las propiedades `ImsAuthProps` para controlar el flujo de autenticación y registrar agentes de escucha para varios eventos de autenticación. Puede usar la práctica función [`registerAssetsSelectorsAuthService`](#purejsselectorsregisterassetsselectorsauthservice) para registrar la instancia de _ImsAuthService_ con el Selector de recursos. Las funciones siguientes están disponibles en la clase `ImsAuthService`. Sin embargo, si está utilizando la función _registerAssetsSelectorsAuthService_, no necesita llamar a estas funciones directamente.

| Nombre de función | Descripción |
|---|---|
| `isSignedInUser` | Determina si el usuario ha iniciado sesión en el servicio y devuelve un valor booleano en consecuencia. |
| `getImsToken` | Recupera la autenticación `imsToken` del usuario que ha iniciado sesión actualmente, que se puede utilizar para autenticar solicitudes en otros servicios como la generación de _representación de recursos. |
| `signIn` | Inicia el proceso de inicio de sesión del usuario. Esta función utiliza `ImsAuthProps` para mostrar la autenticación en una ventana emergente o en una recarga de página completa |
| `signOut` | Cierra la sesión del usuario del servicio, invalidando su token de autenticación y obligándole a iniciar sesión de nuevo para acceder a los recursos protegidos. Al invocar esta función, se volverá a cargar la página actual. |
| `refreshToken` | Actualiza el token de autenticación del usuario que ha iniciado sesión, lo que evita que caduque y garantiza un acceso ininterrumpido a los recursos protegidos. Devuelve un nuevo token de autenticación que puede utilizarse para solicitudes posteriores. |

### Validación con el token de IMS proporcionado {#validation-ims-token}

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

### Registro de llamadas de retorno al servicio IMS {#register-callback-ims-service}

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

>[!MORELIKETHIS]
>
>* [Integrar el Selector de recursos con varias aplicaciones](/help/assets/integrate-asset-selector.md)
>* [Propiedades del Selector de recursos](/help/assets/asset-selector-properties.md)
>* [Integre el Selector de recursos con Dynamic Media con funciones de OpenAPI](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
>* [Personalizaciones del Selector de recursos](/help/assets/asset-selector-customization.md)
