---
title: Integración Adobe Experience Platform y componentes principales AEM-CIF
description: Aprenda a enviar datos de evento de escaparate desde un página de producto procesado por AEM al Experience Platform utilizando el conector CIF - Experience Platform.
sub-product: Commerce
version: Cloud Service
activity: setup
feature: Commerce Integration Framework
topic: Commerce
role: Architect, Developer
level: Beginner
kt: 10834
thumbnail: 346811.jpeg
exl-id: 30bb9b2c-5f00-488e-ad5c-9af7cd2c4735
source-git-commit: 05e4adb0d7ada0f7cea98858229484bf8cca0d16
workflow-type: tm+mt
source-wordcount: '1866'
ht-degree: 1%

---


# Integración Adobe Experience Platform y componentes principales AEM-CIF {#aem-cif-aep-integration}

Los [componentes principales del Marco de integración de comercio (CIF)](https://github.com/adobe/aem-core-cif-components) proporcionan a los integración optimizada Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-overview.html?lang=en) para [reenviar eventos de escaparate y sus datos a partir de interacciones lado del cliente, como __agregar a carro de compras__.

El [proyecto de componentes](https://github.com/adobe/aem-core-cif-components) principales de CIF de AEM proporciona un JavaScript biblioteca denominado [conector Adobe Experience Platform para que Adobe Systems Commerce recoja datos de evento de su escaparate de Commerce](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) . Ese datos de evento se envía a la Experience Platform donde se usa en otros productos Adobe Experience Cloud, como Adobe Analytics y Adobe Target para versión un perfil de 360 grados que cubre un recorrido del cliente. Al conectar datos de comercio con otros productos del Adobe Experience Cloud, puede realizar tareas gustar analizar usuario comportamiento en su sitio, realizar pruebas AB y crear campañas personalizadas.

Obtenga más información sobre Experience Platform [conjunto de tecnologías de recopilación](https://experienceleague.adobe.com/docs/experience-platform/collection/home.html) de datos que le permiten recopilar datos experiencia del cliente de fuentes lado del cliente.

## Enviar `addToCart` datos de evento a Experience Platform {#send-addtocart-to-aep}

Los pasos siguientes muestran cómo enviar el datos de evento desde páginas de productos procesadas por AEM al Experience Platform mediante el `addToCart` conector CIF Experience Platform. Mediante la extensión de explorador de Adobe Experience Platform Debugger, puede prueba y revisar los datos enviados.

![Revisar las datos de evento de addToCart en Adobe Experience Platform Debugger](../assets/aep-integration/EventData-AEM-AEP.png)

## Requisitos previos {#prerequisites}

Utilice un entorno de desarrollo local para completar esta demostración. Esto incluye una instancia en ejecución de AEM configurada y conectada a una instancia de Adobe Systems Commerce. Revise los requisitos y pasos para [configurar el desarrollo local con AEM como Cloud Service SDK](../develop.md).

También necesita acceso a [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-ui/ui-guide.html) y permisos para crear el esquema, la conjunto de datos y los flujos de datos para recopilación de datos. Para obtener más información, consulte [Administración de permisos](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html).

## AEM configuración de Commerce como Cloud Service {#aem-setup}

Para tener un __entorno AEM de comercio como Cloud Service__ local con el código y la configuración necesarios, complete los siguientes pasos.

### Configuración local

Siga los pasos de Configuración [](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/developing/develop.html?#local-setup) local para que pueda tener una AEM de comercio como Cloud Service entorno.

### Configuración del proyecto

Siga los pasos del arquetipo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/developing/develop.html?#project) del [proyecto AEM para poder crear un nuevo proyecto marca AEM Commerce (CIF).

>[!TIP]
>
>En el ejemplo siguiente, el nombre del proyecto AEM Commerce: `My Demo Storefront`, aunque puede elegir su propio nombre de proyecto.

![AEM Commerce Project](../assets/aep-integration/aem-project-with-commerce.png)


Compile y implementar el proyecto de AEM Commerce creado al SDK de AEM local ejecutando el siguiente comando desde el directorio raíz del proyecto.

```bash
$ mvn clean install -PautoInstallSinglePackage
```

El sitio de comercio implementado `My Demo StoreFront` localmente con código y contenido predeterminados gustar los siguientes aspectos:

![Sitio de AEM comercio predeterminado](../assets/aep-integration/demo-aem-storefront.png)

### Instalación de dependencias de conector Peregrine y CIF-AEP

Para recopilar y enviar los datos de evento de las páginas de categoría y productos de este sitio de AEM Commerce, instale los paquetes de claves `npm` en el `ui.frontend` módulo del proyecto de AEM Commerce.

Navegue hasta el `ui.frontend` módulo e instale los paquetes necesarios ejecutando los siguientes comandos desde la línea de comandos.

```bash
npm i --save lodash.get@^4.4.2 lodash.set@^4.3.2
npm i --save apollo-cache-persist@^0.1.1
npm i --save redux-thunk@~2.3.0
npm i --save @adobe/apollo-link-mutation-queue@~1.1.0
npm i --save @magento/peregrine@~12.5.0
npm i --save @adobe/aem-core-cif-react-components --force
npm i --save-dev @magento/babel-preset-peregrine@~1.2.1
npm i --save @adobe/aem-core-cif-experience-platform-connector --force
```

>[!IMPORTANT]
>
>A veces se requiere el `--force` argumento, ya [que PWA Studio](https://developer.adobe.com/commerce/pwa-studio/) es restrictivo con las dependencias del mismo nivel admitidas. Por lo general, esto no debería causar ningún problema.


### Configurar Maven para usar `--force` argumentos

Como parte del proceso de versión de Maven, se activa la instalación limpia de npm (mediante `npm ci`). Esto también requiere el `--force` argumento.

Desplácese hasta el archivo `pom.xml` POM raíz del proyecto y localice el bloque de `<id>npm ci</id>` ejecución. Actualice el bloque para que tenga el gustar siguiente aspecto:

```xml
<execution>
    <id>npm ci</id>
    <goals>
    <goal>npm</goal>
    </goals>
    <configuration>
    <arguments>ci --force</arguments>
    </configuration>
</execution>
```

### Cambiar el formato de configuración de Babel

Cambie del archivo de configuración predeterminado `.babelrc` relativo al formato a `babel.config.js` formato. Este es un formato de configuración para todo el `node_module` proyecto y permite que los complementos y ajustes preestablecidos se apliquen al con mayor control.

1. Desplácese a la `ui.frontend` módulo y elimine el archivo existente `.babelrc` .

1. Crear un `babel.config.js` archivo que utilice el `peregrine` ajuste preestablecido.

   ```javascript
   const peregrine = require('@magento/babel-preset-peregrine');
   
   module.exports = (api, opts = {}) => {
       const config = {
           ...peregrine(api, opts),
           sourceType: 'unambiguous'
       } 
   
       config.plugins = config.plugins.filter(plugin => plugin !== 'react-refresh/babel');
   
       return config;
   }
   ```

### Configurar webpack para usar Babel

To transpile the JavaScript files using Babel loader (`babel-loader`) and webpack, edit the `webpack.common.js` archivo.

Vaya a `ui.frontend` module and update the `webpack.common.js` file so you can have the following rule inside the `module` property value:

```javascript
{
    test: /\.jsx?$/,
    exclude: /node_modules\/(?!@magento\/)/,
    loader: 'babel-loader'
}
```

### Configure Apollo Client

El [cliente](https://www.apollographql.com/docs/react/) Apollo se utiliza para administrar datos locales y remotos con GraphQL. También almacena los resultados de las consultas GraphQL en una caché local, normalizada y en memoria.

Para [`InMemoryCache`](https://www.apollographql.com/docs/react/caching/cache-configuration/) que funcione eficazmente, necesita un `possibleTypes.js` archivo. Para generar este archivo, consulte [Generación automática](https://www.apollographql.com/docs/react/data/fragments/#generating-possibletypes-automatically) de possibleTypes. Además, consulte la [implementación de referencia de PWA Studio](https://github.com/magento/pwa-studio/blob/1977f38305ff6c0e2b23a9da7beb0b2f69758bed/packages/pwa-buildpack/lib/Utilities/graphQL.js#L106-L120) y un ejemplo de un [`possibleTypes.js`](../assets/aep-integration/possibleTypes.js) archivo.


1. Vaya a `ui.frontend` module and save the file as `./src/main/possibleTypes.js`

1. Actualice el `webpack.common.js` del archivo `DefinePlugin` section so you can replace the required static variables during build time.

   ```javascript
   const { DefinePlugin } = require('webpack');
   const { POSSIBLE_TYPES } = require('./src/main/possibleTypes');
   
   ...
   
   plugins: [
       ...
       new DefinePlugin({
           'process.env.USE_STORE_CODE_IN_URL': false,
           POSSIBLE_TYPES
       })
   ]
   ```

### Initialize Peregrine and CIF core components

To initialize the React-based Peregrine and CIF core components, create the required configuration and JavaScript files.

1. Desplácese a la módulo y cree la `ui.frontend` carpeta siguiente: `src/main/webpack/components/commerce/App`

1. Crear un `config.js` archivo con las siguientes contenido:

   ```javascript
   // get and parse the CIF store configuration from the <head>
   const storeConfigEl = document.querySelector('meta[name="store-config"]');
   const storeConfig = storeConfigEl ? JSON.parse(storeConfigEl.content) : {};
   
   // the following global variables are needed for some of the peregrine features
   window.STORE_VIEW_CODE = storeConfig.storeView || 'default';
   window.AVAILABLE_STORE_VIEWS = [
       {
           code: window.STORE_VIEW_CODE,
           base_currency_code: 'USD',
           default_display_currency_code: 'USD',
           id: 1,
           locale: 'en',
           secure_base_media_url: '',
           store_name: 'My Demo StoreFront'
       }
   ];
   window.STORE_NAME = window.STORE_VIEW_CODE;
   window.DEFAULT_COUNTRY_CODE = 'en';
   
   export default {
       storeView: window.STORE_VIEW_CODE,
       graphqlEndpoint: storeConfig.graphqlEndpoint,
       // Can be GET or POST. When selecting GET, this applies to cache-able GraphQL query requests only.
       // Mutations will always be executed as POST requests.
       graphqlMethod: storeConfig.graphqlMethod,
       headers: storeConfig.headers,
   
       mountingPoints: {
           // TODO: define the application specific mount points as they may be used by <Portal> and <PortalPlacer>
       },
       pagePaths: {
           // TODO: define the application specific paths/urls as they may be used by the components
           baseUrl: storeConfig.storeRootUrl
       },
       eventsCollector: {
           eventForwarding: {
               acds: true,
               aep: false,
           }
       }
   };
   ```

   >[!IMPORTANT]
   >
   >Aunque es posible que ya esté familiarizado con el [`config.js`](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.frontend/src/main/components/App/config.js) archivo de __AEM Guides - CIF Venia Project__, hay algunos cambios que debe realizar en este archivo. Primero, revise cualquier __comentarios de TAREAS__ . A continuación, dentro del `eventsCollector` Propiedad, busque el `eventsCollector > aep` objeto y actualice las `orgId` propiedades and `datastreamId` a los valores correctos. [Más información](./aep.md#add-aep-values-to-aem).

1. Crear un `App.js` archivo con las siguientes contenido. Este archivo se asemeja a un archivo de punto de inicio típico de React aplicación y contiene React y ganchos personalizados y el uso de React Context para facilitar la integración Experience Platform.

   ```javascript
   import config from './config';
   
   import React, { useEffect } from 'react';
   import ReactDOM from 'react-dom';
   import { IntlProvider } from 'react-intl';
   import { BrowserRouter as Router } from 'react-router-dom';
   import { combineReducers, createStore } from 'redux';
   import { Provider as ReduxProvider } from 'react-redux';
   import { createHttpLink, ApolloProvider } from '@apollo/client';
   import { ConfigContextProvider, useCustomUrlEvent, useReferrerEvent, usePageEvent, useDataLayerEvents, useAddToCartEvent } from '@adobe/aem-core-cif-react-components';
   import { EventCollectorContextProvider, useEventCollectorContext } from '@adobe/aem-core-cif-experience-platform-connector';
   import { useAdapter } from '@magento/peregrine/lib/talons/Adapter/useAdapter';
   import { customFetchToShrinkQuery } from '@magento/peregrine/lib/Apollo/links';
   import { BrowserPersistence } from '@magento/peregrine/lib/util';
   import { default as PeregrineContextProvider } from '@magento/peregrine/lib/PeregrineContextProvider';
   import { enhancer, reducers } from '@magento/peregrine/lib/store';
   
   const storage = new BrowserPersistence();
   const store = createStore(combineReducers(reducers), enhancer);
   
   storage.setItem('store_view_code', config.storeView);
   
   const App = () => {
       const [{ sdk: mse }] = useEventCollectorContext();
   
       // trigger page-level events
       useCustomUrlEvent({ mse });
       useReferrerEvent({ mse });
       usePageEvent({ mse });
       // listen for add-to-cart events and enable forwarding to the magento storefront events sdk
       useAddToCartEvent(({ mse }));
       // enable CIF specific event forwarding to the Adobe Client Data Layer
       useDataLayerEvents();
   
       useEffect(() => {
           // implement a proper marketing opt-in, for demo purpose you hard-set the consent cookie
           if (document.cookie.indexOf('mg_dnt') < 0) {
               document.cookie += '; mg_dnt=track';
           }
       }, []);
   
       // TODO: use the App to create Portals and PortalPlaceholders to mount the CIF / Peregrine components to the server side rendered markup
       return <></>;
   };
   
   const AppContext = ({ children }) => {
       const { storeView, graphqlEndpoint, graphqlMethod = 'POST', headers = {}, eventsCollector } = config;
       const { apolloProps } = useAdapter({
           apiUrl: new URL(graphqlEndpoint, window.location.origin).toString(),
           configureLinks: (links, apiBase) =>
               // reconfigure the HTTP link to use the configured graphqlEndpoint, graphqlMethod and storeView header
   
               links.set('HTTP', createHttpLink({
                   fetch: customFetchToShrinkQuery,
                   useGETForQueries: graphqlMethod !== 'POST',
                   uri: apiBase,
                   headers: { ...headers, 'Store': storeView }
               }))
       });
   
       return (
           <ApolloProvider {...apolloProps}>
               <IntlProvider locale='en' messages={{}}>
                   <ConfigContextProvider config={config}>
                       <ReduxProvider store={store}>
                           <PeregrineContextProvider>
                               <EventCollectorContextProvider {...eventsCollector}>
                                   {children}
                               </EventCollectorContextProvider>
                           </PeregrineContextProvider>
                       </ReduxProvider>
                   </ConfigContextProvider>
               </IntlProvider>
           </ApolloProvider>
       );
   };
   
   window.onload = async () => {
       const root = document.createElement('div');
       document.body.appendChild(root);
   
       ReactDOM.render(
           <Router>
               <AppContext>
                   <App />
               </AppContext>
           </Router>,
           root
       );
   };
   ```

   El `EventCollectorContext` exporta el contexto de reacción que:

   - Carga el SDK commerce-events-y el biblioteca commerce-events-collector,
   - los inicializa con una configuración determinada para Experience Platform y/o ACDS
   - se suscribe a todos los eventos de Peregrine y los reenvía al SDK de eventos

   Puede revisar los detalles implementación de la `EventCollectorContext` [aquí](https://github.com/adobe/aem-core-cif-components/blob/3d4e44d81fff2f398fd2376d24f7b7019f20b31b/extensions/experience-platform-connector/src/events-collector/EventCollectorContext.js).

### Genere y implementar el proyecto de AEM actualizado

Para asegurarse de que los cambios de instalación, código y configuración del paquete anterior son correctos, reconstruya y implementar el proyecto actualizado de AEM Commerce utilizando el siguiente comando de Maven: `$ mvn clean install -PautoInstallSinglePackage`.

## Configuración Experience Platform {#aep-setup}

Para recibir y tienda los datos de evento provenientes de las páginas de AEM Commerce, como categoría y producto, complete los siguientes pasos:

>[!AVAILABILITY]
>
>Asegúrese de formar parte de los perfiles de producto correctos ____ en __Adobe Experience Platform__ y __Adobe Experience Platform recopilación__ de datos. Si es necesario, trabaje con el administrador del sistema para crear, actualizar o asignar __perfiles__ de producto en la [Admin Console](https://adminconsole.adobe.com/).

### Crear grupo de campo Esquema con comercio

Para definir la estructura de los datos de evento comerciales, debe crear un Modelo de datos de experiencia (XDM) esquema. Una esquema es un conjunto de reglas que representan y validan la estructura y el formato de datos.

1. En la explorador, navegue hasta la página principal del __producto Adobe Experience Platform__ Página. Por ejemplo, <https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>.

1. Busque el __menú Esquemas__ en la sección navegación izquierda, haga clic en la botón Esquema __de Crear en la__ sección superior derecha y seleccione __XDM ExperienceEvent__.

   ![Esquema Crear AEP](../assets/aep-integration/AEP-Schema-EventSchema-1.png)

1. Asigne un nombre a su esquema mediante el campo Nombre para mostrar __del__ esquema Propiedades > y agregue grupos de campos mediante los grupos de > de __composición > añadir__ de campos botón.

   ![Definición del esquema de AEP](../assets/aep-integration/AEP-Schema-Definition.png)

1. En el cuadro de diálogo añadir __grupos de campos, búsqueda para `Commerce`, seleccione la casilla de verificación Detalles de__ comercio y haga clic en __añadir grupos de____campos__.

   ![Definición del esquema de AEP](../assets/aep-integration/AEP-Schema-Field-Group.png)


>[!TIP]
>
>Consulte Fundamentos [de esquema composición](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html) para obtener más información.

### Crear conjunto de datos

Para tienda el datos de evento, debe crear un conjunto de datos que se ajuste a la definición de esquema. Un conjunto de datos es una construcción de almacenamiento y administración para un colección de datos, normalmente una tabla, que contiene un esquema (columnas) y campos (filas).

1. En la explorador, navegue hasta la página principal del __producto Adobe Experience Platform__ Página. Por ejemplo, <https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>.

1. Busque el menú Conjuntos ____ de datos en la sección navegación izquierda y haga clic en la botón Crear conjunto de datos __de la__ sección superior derecha.

   ![Conjuntos de datos de AEP Crear](../assets/aep-integration/AEP-Datasets-Create.png)

1. En la nueva Página, seleccione __Crear conjunto de datos en esquema__ tarjeta.

   ![Opción de esquema de conjuntos de datos de AEP Crear](../assets/aep-integration/AEP-Datasets-Schema-Option.png)

   En el nuevo Página, __búsqueda__ seleccione la esquema que creó en el paso anterior y haga clic en la __botón Siguiente__ .

   ![Conjuntos de datos de AEP Crear Seleccionar esquema](../assets/aep-integration/AEP-Datasets-Select-Schema.png)

1. Asigne un nombre al conjunto de datos mediante el __campo Configurar nombre__ conjunto de datos > datos y haga clic en la __botón finalización__ .

   ![Nombre de conjuntos de datos de AEP Crear](../assets/aep-integration/AEP-Datasets-Name.png)

>[!TIP]
>
>Consulte la descripción general](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html) de los conjuntos de [datos para obtener más información.


### Crear Datastream

Todas las aplicaciones los pasos siguientes para poder crear un flujo de datos en el Experience Platform.

1. En la explorador, navegue hasta la página principal del __producto Adobe Experience Platform__ Página. Por ejemplo, <https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>.

1. Busque el __menú Flujos de datos en la sección navegación izquierda y haga clic en la botón Nuevo Flujo__ de datos de __la__ sección superior derecha.

   ![Flujos de datos de AEP Crear](../assets/aep-integration/AEP-Datastream-Create.png)

1. Asigne un nombre al flujo de datos mediante el __campo Nombre__ requerido. En el campo Esquema __de eventos, seleccione el__ esquema creado y haga clic en __Guardar__.

   ![AEP Definir flujos de datos](../assets/aep-integration/AEP-Datastream-Define.png)

1. Abra el flujo de datos creado y haga clic en __añadir servicio__.

   ![AEP Datastreams Add Service](../assets/aep-integration/AEP-Datastream-Add-Service.png)

1. En el __Servicio__ , seleccione el campo __Adobe Experience Platform__ opción. En __Event Dataset__ field, select the dataset name from the previous step and click __Guardar__.

   ![AEP Datastreams Add Service Details](../assets/aep-integration/AEP-Datastream-Add-Service-Define.png)

>[!TIP]
>
>Consulte la descripción general](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html) del [flujo de datos para obtener más información.

## añadir valor del flujo de datos a la configuración de AEM Commerce {#add-aep-values-to-aem}

After completing the above Experience Platform setup, you should have `datastreamId` in the left rail of the Datastream details and `orgId` in the top-right corner of the __Profile Picture > Account info > User Information__ modal.

![AEP Datastreams ID](../assets/aep-integration/AEP-Datastream-ID.png)

1. In the AEM Commerce project&#39;s `ui.frontend` module, update the `config.js` file and specifically the `eventsCollector > aep` object properties.

1. Build and deploy the updated AEM Commerce project


## Déclencheur `addToCart` event and verify data collection {#event-trigger-verify}

The above steps complete the AEM Commerce and Experience Platform setup. Ahora puede activar una `addToCart` evento y verificar recopilación de datos con la extensión _Google Cromo Snowplow Inspector_ y conjunto de datos __Las métricas y los__ gráficos se alternan en el IU del producto.

Para activar el evento, puede usar AEM autor o el servicio publicar de su configuración local. Para este ejemplo, utilice AEM autor por registro en su cuenta.

1. Desde Sites Página, seleccione My __Demo StoreFront > nosotros > en__ Página y haga clic __en Editar__ en la barra de acciones superior.

1. En la barra de acciones superior, haz clic en Ver como Publicado __y, a continuación, haz clic en__ cualquier categoría preferido del navegación del escaparate.

1. Haga clic en cualquier tarjeta de producto preferido en el Página __Producto y, a continuación, seleccione__ el color y el tamaño __para permitir que el__ añadir al carro __de__ botón.


1. Abra la __extensión Snowplow Inspector__ desde el panel de extensión del explorador y seleccione __Experience Platform SDK__ Wed en el carril izquierdo.


1. Vuelva al Página __del producto y haga clic en__ añadir al __botón del carro de compras__. This sends data to the Experience Platform. El __Adobe Experience Platform Debugger__ extension shows the event details.

   ![AEP Debugger Add-To-Cart Event-Data](../assets/aep-integration/AEP-Debugger-AddToCart-EventData.png)



1. Dentro de Experience Platform IU producto, vaya a __Conjuntos de datos > Mi StoreFront__ de demostración, en el conjunto de __datos actividad__ pestaña. Si __las métricas y los gráficos están activados__ , se muestran las estadísticas de evento datos.

   ![Estadísticas de datos del conjunto de datos de Experience Platform](../assets/aep-integration/AEP-Dataset-AddToCart-EventData.png)



## Implementation Details {#implementation-details}

El [CIF Experience Platform Connector](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) is built on top of the [Data Connection for Adobe Commerce](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html), which is part of the [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/) proyecto.

The PWA Studio project lets you create Progressive Web Application (PWA) storefronts powered by Adobe Commerce or Magento Open Source. The project also contains a component library called [Peregrin](https://developer.adobe.com/commerce/pwa-studio/api/peregrine/) for adding logic to visual components. El [Peregrin library](https://developer.adobe.com/commerce/pwa-studio/api/peregrine/) also provides the custom React hooks that are used by [CIF Experience Platform Connector](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) to integrate with Experience Platform seamlessly.


## Eventos admitidos {#supported-events}

A partir de ahora, se admiten los siguientes eventos:

__Experimente eventos XDM:__

1. añadir al carro (AEM)
1. Ver Página (AEM)
1. Ver producto (AEM)
1. Search Solicitud enviada (AEM)
1. Search Respuesta recibida (AEM)

Cuando [los componentes](https://developer.adobe.com/commerce/pwa-studio/guides/packages/peregrine/) de Peregrine se reutilizan en el proyecto AEM Commerce:

__Experimente eventos XDM:__

1. Quitar del carro
1. Abrir carro de compras
1. Carro Ver
1. compra instantánea
1. Inicio Cierre de compra
1. Todas las aplicaciones cierre de compra

__Eventos XDM de perfil:__

1. Iniciar sesión
1. Crear cuenta
1. Editar cuenta


## Recursos adicionales {#additional-resources}

Para obtener más información, consulte los recursos siguientes:

- [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/)
- [[!DNL Data Connection] Visión general](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/overview.html)
- [[!DNL Data Connection] Eventos](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/event-forwarding/events.html)
- [Información general Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/home.html)
