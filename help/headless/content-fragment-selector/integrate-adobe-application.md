---
title: Integración del Selector de fragmentos de contenido con una aplicación de Adobe
description: Integre el selector Fragmento de contenido con varias aplicaciones de Adobe.
role: Admin, User, Developer
source-git-commit: a16d9e9fa6483a89283c595372abcc437d1d962e
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 1%

---

# Integración del Selector de fragmentos de contenido con la aplicación Adobe {#integrate-content-fragment-selector-with-adobe-application}

El Selector de fragmentos de contenido le permite integrarse con varias aplicaciones de Adobe para permitirles trabajar juntos sin problemas.

## Requisitos previos {#prerequisites}

Utilice los siguientes requisitos previos si integra el Selector de fragmentos de contenido con una aplicación de Adobe:

* [Requisitos previos](/help/headless/content-fragment-selector/overview.md#prerequisites)
* imsOrg
* imsToken
* apikey

## Integración del Selector de fragmentos de contenido con una aplicación de Adobe {#integrate-content-fragment-selector-with-an-adobe-application}

En el siguiente ejemplo se muestra el uso del Selector de fragmentos de contenido al ejecutar una aplicación de Adobe en Unified Shell o cuando ya se ha generado un `imsToken` para la autenticación.

Incluya el paquete Selector de fragmentos de contenido en su código mediante la etiqueta `script`, como se muestra en el ejemplo siguiente.

* Una vez cargado el script, la variable global `PureJSContentFragmentSelectors` está disponible para su uso.
* Defina el Selector de fragmentos de contenido [properties](/help/headless/content-fragment-selector/properties.md):

   * las propiedades `imsOrg` y `imsToken` son necesarias para la autenticación en la aplicación Adobe
   * la propiedad `handleSelection` se usa para controlar los fragmentos seleccionados.

* Para procesar el selector de fragmentos de contenido, llame a la función `renderFragmentSelector`.
* El selector de fragmentos de contenido se muestra en el elemento contenedor `<div>`.

Al seguir estos pasos, puede utilizar el Selector de fragmentos de contenido con la aplicación de Adobe.

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
    <title>Fragment Selector</title>
    <script src="https://experience.adobe.com/solutions/CQ-fragmentss-selectors/static-fragments/resources/fragments-selectors.js"></script>
    <script>
        // get the container element in which we want to render the FragmentSelector component
        const container = document.getElementById('fragment-selector-container');
        // imsOrg and imsToken are required for authentication in Adobe application
        const fragmentSelectorProps = {
            imsOrg: 'example-ims@AdobeOrg',
            imsToken: "example-imsToken",
            apiKey: "example-apiKey-associated-with-imsOrg",
            handleSelection: (fragmentss: SelectedFragmentType[]) => {},
        };
        // Call the `renderFragmentSelector` available in PureJSContentFragmentSelectors globals to render FragmenttSelector
        PureJSContentFragmentSelectors.renderFragmentSelector(container, fragmentSelectorProps);
    </script>
</head>

<body>
    <div id="fragment-selector-container" style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px;">
    </div>
</body>

</html>
```

### ImsAuthProps {#imsauthprops}

Las propiedades de `ImsAuthProps` definen la información de autenticación y el flujo que utiliza el Selector de fragmentos de contenido para obtener un `imsToken`. Al establecer estas propiedades, puede controlar cómo se comporta el flujo de autenticación y registrar agentes de escucha para varios eventos de autenticación.

Para obtener detalles de la propiedad, consulte [Propiedades de ImsAuthProps](/help/headless/content-fragment-selector/properties.md#imsauthprops-properties)

### ImsAuthService {#imsauthservice}

La clase `ImsAuthService` administra el flujo de autenticación para el Selector de fragmentos. Es responsable de obtener un `imsToken` del servicio de autenticación IMS de Adobe. `imsToken` se usa para autenticar al usuario y autorizar el acceso al repositorio de AEM as a Cloud Service. `ImsAuthService` utiliza las propiedades `ImsAuthProps` para controlar el flujo de autenticación y registrar agentes de escucha para varios eventos de autenticación. Puede usar la función `registerFragmentsSelectorsAuthService` para registrar la instancia `ImsAuthService` con el Selector de fragmentos. Las funciones siguientes están disponibles en la clase `ImsAuthService`. Sin embargo, si está utilizando la función `registerFragmentsSelectorsAuthService`, no necesita llamar a estas funciones directamente.

Para obtener detalles de la propiedad, consulte [Propiedades de ImsAuthService](/help/headless/content-fragment-selector/properties.md#imsauthservice-properties)

### Validación con el token de IMS proporcionado {#validation-with-provided-ims-token}

```javascript
<script>
    const apiToken="<valid IMS token>";
    function handleSelection(selection) {
    console.log("Selected fragment: ", selection);
    };
    function renderFragmentSelectorInline() {
    console.log("initializing Fragment Selector");
    const props = {
    "repositoryId": "delivery-p64502-e544757.adobeaemcloud.com",
    "apiKey": "ngdm_test_client",
    "imsOrg": "<IMS org>",
    "imsToken": apiToken,
    handleSelection,
    hideTreeNav: true
    }
    const container = document.getElementById('fragment-selector-container');
    PureJSContentFragmentSelectors.renderFragmentSelector(container, props);
    }
    $(document).ready(function() {
    renderFragmentSelectorInline();
    });
</script>
```

### Registro de llamadas de retorno al servicio IMS {#register-callbacks-to-ims-service}

```java
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
