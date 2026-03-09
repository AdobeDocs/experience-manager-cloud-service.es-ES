---
title: Integración del Selector de fragmentos de contenido con aplicaciones que no sean de Adobe o de terceros
description: Integre el selector de fragmentos de contenido con varias aplicaciones de Adobe, que no sean de Adobe y de terceros.
role: Admin, User, Developer
source-git-commit: 3af1a89489af96bf9c9908aea7fb20883956517b
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 5%

---

# Integración con una aplicación que no es de Adobe {#integration-with-non-adobe-application}

El Selector de fragmentos de contenido le permite integrarse con varias aplicaciones diferentes de Adobe o de terceros para permitirles trabajar juntos sin problemas.

## Requisitos previos {#prerequisites}

Utilice los siguientes requisitos previos si integra el Selector de fragmentos de contenido con una aplicación que no sea de Adobe:

* [Requisitos previos](/help/headless/content-fragment-selector/overview.md#prerequisites)
* imsClientId
* imsScope
* redirectUrl
* imsOrg
* apikey

Cuando lo integra con una aplicación que no es de Adobe, el Selector de fragmentos de contenido admite la autenticación en el repositorio de as a Cloud Service de Adobe Experience Manager (AEM) mediante propiedades de Identity Management System (IMS) como `imsScope` o `imsClientID`.

## Configuración del selector de fragmentos de contenido para una aplicación que no sea de Adobe {#configure-content-fragment-selector-for-a-non-adobe-application}

Para configurar el Selector de fragmentos de contenido para una aplicación que no sea de Adobe, primero debe registrar un ticket de asistencia para el aprovisionamiento antes de continuar con los pasos de integración.

### Registro de un ticket de asistencia {#logging-a-support-ticket}

Pasos para registrar un ticket de asistencia a través de Admin Console:

1. Agregue **Selector de fragmentos de contenido con fragmentos de AEM** en el título del ticket.

1. En la descripción, proporcione los siguientes detalles:

   * URL de Experience Manager as a Cloud Service (ID de programa e ID de entorno).
   * Nombres de dominio en los que está alojada la aplicación web que no es de Adobe.

## Pasos de integración {#integration-steps}

Utilice el siguiente archivo de ejemplo `index.html` para la autenticación al integrar el Selector de fragmentos de contenido con una aplicación que no sea de Adobe:

* Acceda al paquete Selector de fragmentos de contenido usando la etiqueta `Script`.

* Defina las propiedades de flujo de IMS, como `imsClientId`, `imsScope` y `redirectURL`.

   * La función requiere que defina al menos una de las propiedades `imsClientId` y `imsScope`.
   * Si no define un valor para `redirectURL`, se utilizará la dirección URL de redireccionamiento registrada para el ID de cliente.

* Como el ejemplo no tiene un `imsToken` generado, use las funciones `registerFragmentsSelectorsAuthService` y `renderFragmentSelectorWithAuthFlow`.

   * Use la función `registerFragmentsSelectorsAuthService` antes de `renderFragmentSelectorWithAuthFlow` para registrar `imsToken` con el selector de fragmentos de contenido.
   * Adobe recomienda llamar a `registerFragmentsSelectorsAuthService` al crear una instancia del componente.

* Defina la autenticación y otras propiedades relacionadas con el acceso a as a Cloud Service de Fragmentos en la sección `const props`.
* La variable global `PureJSContentFragmentSelectors` se usa para procesar el selector de fragmentos de contenido en el explorador web.
* El selector de fragmentos de contenido se representa en el elemento contenedor `<div>`. El ejemplo utiliza un cuadro de diálogo para mostrar el Selector de fragmentos de contenido.

**Ejemplo`ìndex.html`**

```html {line-numbers="true"}
<!doctype html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <link rel="icon" type="image/svg+xml" href="/vite.svg" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>testing-cf-mfe-integration-with-3rd-party-app</title>
        <script
            id="content-fragments-selector"
            src="https://experience.adobe.com/solutions/CQ-sites-content-fragment-selector/static-assets/resources/content-fragment-selector.js"
        ></script>
        <script>
            const imsProps = {
                imsClientId: '<IMS_CLIENT_ID>',
                imsScope:
                    'additional_info.projectedProductContext, AdobeID, openid, read_organizations',
                redirectUrl: window.location.href,
                onImsServiceInitialized: (service) => {
                    // invoked when the ims service is initialized and is ready
                    console.log('onImsServiceInitialized', service);
                },
                onAccessTokenReceived: (token) => {
                    console.log('onAccessTokenReceived', token);
                },
                onAccessTokenExpired: () => {
                    console.log('onAccessTokenError');
                    // re-trigger sign-in flow
                },
                onErrorReceived: (type, msg) => {
                    console.log('onErrorReceived', type, msg);
                },
            };

            function load() {
                const registeredTokenService =
                    PureJSContentFragmentSelectors.registerContentFragmentSelectorAuthService(
                        imsProps
                    );
                imsInstance = registeredTokenService;
            }

            // initialize the IMS flow before attempting to render the content fragment selector
            load();

            // function that will render the content fragment selector
            function renderContentFragmentSelectorWithAuthFlow() {
                const contentFragmentSelectorDialog = document.getElementById(
                    'content-fragment-selector-dialog'
                );

                const contentFragmentSelectorProps = {
                    inventoryViewToggleEnabled: true,
                    isOpen: true,
                    noWrap: false,
                    orgId: 'YOUR_ORG_ID@AdobeOrg',
                    // repoId: "author-p12345-e67890.adobeaemcloud.com", // if wanted to restrict to a specific repo
                    runningInUnifiedShell: false,
                    onDismiss: () => contentFragmentSelectorDialog.close(),
                    onSubmit: ({ contentFragments }) => {
                        const selectedContentFragment = contentFragments[0];
                        alert(selectedContentFragment.path);
                    },
                };
                // container element on which you want to render the ContentFragmentSelector component
                const container = document.getElementById('content-fragment-selector');

                /// Use the PureJSContentFragmentSelectors in globals to render the ContentFragmentSelector component
                PureJSContentFragmentSelectors.renderContentFragmentSelectorWithAuthFlow(
                    container,
                    contentFragmentSelectorProps,
                    () => contentFragmentSelectorDialog.showModal()
                );
            }
        </script>
    </head>
    <body>
        <div>
            <button onclick="renderContentFragmentSelectorWithAuthFlow()">
                Content Fragment Selector - Select Content Fragments with Ims Flow
            </button>
        </div>
        <dialog id="content-fragment-selector-dialog">
            <div
                id="content-fragment-selector"
                style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px"
            ></div>
        </dialog>
    </body>
</html>
```

## No se puede acceder al repositorio de envío {#unable-to-access-delivery-repository}

Si ha integrado el Selector de fragmentos de contenido mediante el flujo de trabajo de Registro de inicio de sesión, pero sigue sin poder acceder al repositorio de envío, asegúrese de que se hayan limpiado las cookies del explorador.

De lo contrario, es posible que vea el error `invalid_credentials All session cookies are empty` en la consola.
