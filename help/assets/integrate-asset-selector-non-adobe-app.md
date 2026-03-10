---
title: Integrar el Selector de recursos con aplicaciones que no sean de Adobe o de terceros
description: Integre el selector de recursos con varias aplicaciones de Adobe, que no sean de Adobe y de terceros.
role: Admin, User
badgeSaas: label="AEM Assets" type="Positive" tooltip="(Se aplica a los AEM Assets)."
exl-id: 55848de0-aff2-42a0-b959-c771235d9425
source-git-commit: a641933d1049cd07ee8935672c8ef357a5bbf18c
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 9%

---

# Integración con una aplicación que no es de Adobe {#integrate-asset-selector-non-adobe-app}

El Selector de recursos le permite integrarse utilizando varias aplicaciones diferentes de Adobe o de terceros para permitir que funcionen juntas sin problemas.

## Requisitos previos {#prereqs-non-adobe-app}

Utilice los siguientes requisitos previos si integra el Selector de recursos con una aplicación que no sea de Adobe:

* [Métodos de comunicación](/help/assets/overview-asset-selector.md#prereqs)
* imsClientId
* imsScope
* redirectUrl
* imsOrg
* apikey

El Selector de recursos admite la autenticación en el repositorio [!DNL Experience Manager Assets] mediante propiedades de Identity Management System (IMS) como `imsScope` o `imsClientID` cuando se integra con una aplicación que no es de Adobe.

## Configuración del Selector de recursos para una aplicación que no sea de Adobe {#configure-non-adobe-app}

Para configurar el Selector de recursos para una aplicación que no sea de Adobe, primero debe registrar un ticket de asistencia para el aprovisionamiento seguido de los pasos de integración.

### Registro de un ticket de asistencia {#log-a-support-ticket}

Pasos para registrar un ticket de asistencia a través de Admin Console:

1. Agregue **Selector de recursos con AEM Assets** en el título del ticket.

1. En la descripción, proporcione los siguientes detalles:

   * [!DNL Experience Manager Assets] como URL de [!DNL Cloud Service] (ID de programa e ID de entorno).
   * Nombres de dominio en los que está alojada la aplicación web que no es de Adobe.

## Pasos de integración {#non-adobe-app-integration-steps}

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
        src="https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js"></script>
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
        function renderAssetSelectorWithAuthFlowFlow() {
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

## No se puede acceder al repositorio de envío {#unable-to-access-delivery-repository}

>[!TIP]
>
>Si ha integrado el Selector de recursos mediante el flujo de trabajo de registro de inicio de sesión, pero sigue sin poder acceder al repositorio de envío, asegúrese de que las cookies del explorador se limpien. De lo contrario, obtendrá el error `invalid_credentials All session cookies are empty` en la consola.

>[!MORELIKETHIS]
>
>* [Integrar el Selector de recursos con varias aplicaciones](/help/assets/integrate-asset-selector.md)
>* [Propiedades del Selector de recursos](/help/assets/asset-selector-properties.md)
>* [Integre el Selector de recursos con Dynamic Media con funciones de OpenAPI](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
>* [Personalizaciones del Selector de recursos](/help/assets/asset-selector-customization.md)
