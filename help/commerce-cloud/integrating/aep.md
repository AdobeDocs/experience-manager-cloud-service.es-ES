---
title: AEM CIF Integración de componentes principales y Adobe Experience Platform de-
description: AEM Obtenga información sobre cómo enviar datos de evento de tienda desde una página de producto procesada por el al Experience Platform CIF mediante el conector de Experience Platform de la tienda de datos de la tienda.
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
source-git-commit: bae9a5178c025b3bafa8ac2da75a1203206c16e1
workflow-type: tm+mt
source-wordcount: '1866'
ht-degree: 1%

---


# AEM CIF Integración de componentes principales y Adobe Experience Platform de- {#aem-cif-aep-integration}

El [Commerce integration framework CIF ()](https://github.com/adobe/aem-core-cif-components) Los componentes principales proporcionan una integración perfecta con [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-overview.html?lang=en) para reenviar eventos de tienda y sus datos desde interacciones del lado del cliente, como __añadir al carro__.

El [AEM CIF Componentes principales de](https://github.com/adobe/aem-core-cif-components) El proyecto proporciona una biblioteca JavaScript llamada [Conector de Adobe Experience Platform para Adobe Commerce](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) para recopilar datos de evento de su tienda de Commerce. Esos datos de evento se envían al Experience Platform, donde se utilizan en otros productos de Adobe Experience Cloud, como Adobe Analytics y Adobe Target, para crear un perfil de 360 grados que cubra un recorrido del cliente. Al conectar los datos de Commerce a otros productos de Adobe Experience Cloud, puede realizar tareas como analizar el comportamiento del usuario en el sitio, realizar pruebas AB y crear campañas personalizadas.

Obtenga más información acerca de [Recopilación de datos de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/collection/home.html) conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente de fuentes del lado del cliente.

## Enviar `addToCart` datos de evento para el Experience Platform {#send-addtocart-to-aep}

Los siguientes pasos muestran cómo enviar el `addToCart` AEM datos de evento de páginas de producto procesadas por el usuario en el Experience Platform CIF mediante el conector de Experience Platform de la interfaz de usuario de. Con la extensión del explorador de Adobe Experience Platform Debugger, puede probar y revisar los datos enviados.

![Revisar los datos del evento addToCart en el Adobe Experience Platform Debugger](../assets/aep-integration/EventData-AEM-AEP.png)

## Requisitos previos {#prerequisites}

Utilice un entorno de desarrollo local para completar esta demostración. AEM Esto incluye una instancia de ejecución de la instancia de que está configurada y conectada a una instancia de Adobe Commerce. Revise los requisitos y pasos para [AEM configuración del desarrollo local con el SDK as a Cloud Service de](../develop.md).

También necesita acceder a [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-ui/ui-guide.html) y permisos para crear el esquema, el conjunto de datos y las secuencias de datos para la recopilación de datos. Para obtener más información, consulte [Administración de permisos](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html).

## AEM Configuración as a Cloud Service de comercio de {#aem-setup}

Para tener un __AEM Commerce as a Cloud Service__ entorno local con el código y la configuración necesarios, complete los siguientes pasos.

### Configuración local

Siga las [Configuración local](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/developing/develop.html?#local-setup) AEM Pasos para poder tener un entorno as a Cloud Service de Commerce en funcionamiento.

### Configuración del proyecto

Siga las [AEM Tipo de archivo del proyecto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/developing/develop.html?#project) AEM CIF Pasos para crear un nuevo proyecto de comercio de la ().

>[!TIP]
>
>AEM En el ejemplo siguiente, el nombre del proyecto de comercio de es: `My Demo Storefront`Sin embargo, puede elegir su propio nombre de proyecto.

![AEM Proyecto de comercio de](../assets/aep-integration/aem-project-with-commerce.png)


AEM AEM Cree e implemente el proyecto de Commerce creado en el SDK de la local ejecutando el siguiente comando desde el directorio raíz del proyecto.

```bash
$ mvn clean install -PautoInstallSinglePackage
```

El implementado localmente `My Demo StoreFront` el sitio de commerce con código y contenido predeterminados tiene el siguiente aspecto:

![AEM Sitio de comercio predeterminado](../assets/aep-integration/demo-aem-storefront.png)

### CIF Instalación de dependencias del conector Peregrine y AEP-

AEM Para recopilar y enviar los datos de evento desde las páginas de categoría y producto de este sitio de comercio de la, instale la clave `npm` paquetes en la `ui.frontend` AEM módulo del proyecto de comercio de la.

Vaya a `ui.frontend` e instale los paquetes necesarios ejecutando los siguientes comandos desde la línea de comandos.

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
>El `--force` se requiere a veces como [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/) es restrictivo con las dependencias del mismo nivel admitidas. Normalmente, esto no debería causar ningún problema.


### Configuración de Maven para utilizar `--force` discusión

Como parte del proceso de creación de Maven, la instalación limpia de npm (con `npm ci`) se activa. Esto también requiere lo siguiente `--force` argumento.

Vaya al archivo POM raíz del proyecto `pom.xml` y busque el `<id>npm ci</id>` bloque de ejecución. Actualice el bloque para que tenga el siguiente aspecto:

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

Cambiar del valor predeterminado `.babelrc` archivo de configuración relativa formato de archivo a `babel.config.js` formato. Se trata de un formato de configuración para todo el proyecto y permite aplicar los complementos y ajustes preestablecidos al `node_module` con mayor control.

1. Vaya a `ui.frontend` y elimine el existente `.babelrc` archivo.

1. Crear un `babel.config.js` que utiliza el `peregrine` ajuste preestablecido.

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

### Configurar Webpack para usar Babel

Para transformar los archivos JavaScript con el cargador Babel (`babel-loader`) y webpack, edite el `webpack.common.js` archivo.

Vaya a `ui.frontend` y actualice el módulo `webpack.common.js` para que pueda tener la siguiente regla dentro de `module` valor de propiedad:

```javascript
{
    test: /\.jsx?$/,
    exclude: /node_modules\/(?!@magento\/)/,
    loader: 'babel-loader'
}
```

### Configurar el cliente Apollo

El [Cliente Apollo](https://www.apollographql.com/docs/react/) se utiliza para administrar datos locales y remotos con GraphQL. También almacena los resultados de las consultas de GraphQL en una memoria caché local normalizada en memoria.

Para [`InMemoryCache`](https://www.apollographql.com/docs/react/caching/cache-configuration/) para trabajar de forma eficaz, necesita un `possibleTypes.js` archivo. Para generar este archivo, consulte [Generación automática de possibleTypes](https://www.apollographql.com/docs/react/data/fragments/#generating-possibletypes-automatically). Consulte también la [implementación de referencia del PWA Studio](https://github.com/magento/pwa-studio/blob/1977f38305ff6c0e2b23a9da7beb0b2f69758bed/packages/pwa-buildpack/lib/Utilities/graphQL.js#L106-L120) y un ejemplo de [`possibleTypes.js`](../assets/aep-integration/possibleTypes.js) archivo.


1. Vaya a `ui.frontend` y guarde el archivo como `./src/main/possibleTypes.js`

1. Actualice el `webpack.common.js` del archivo `DefinePlugin` para que pueda reemplazar las variables estáticas requeridas durante el tiempo de compilación.

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

### CIF Inicialización de los componentes principales de Peregrine y

CIF Para inicializar los componentes principales y de Peregrine basados en React, cree la configuración y los archivos JavaScript necesarios.

1. Vaya a `ui.frontend` y cree la siguiente carpeta: `src/main/webpack/components/commerce/App`

1. Crear un `config.js` archivo con el siguiente contenido:

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
   >Aunque es posible que ya esté familiarizado con el [`config.js`](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.frontend/src/main/components/App/config.js) archivo de __AEM CIF Guias de viaje en Venia - Proyecto Venia__ Sin embargo, debe realizar algunos cambios en este archivo. Primero, revise cualquier __PENDIENTE__ comentarios. A continuación, dentro de `eventsCollector` propiedad, busque la variable `eventsCollector > aep` y actualice el `orgId` y `datastreamId` a los valores correctos. [Más información](./aep.md#add-aep-values-to-aem).

1. Crear un `App.js` con el siguiente contenido. Este archivo es similar al típico archivo de punto de inicio de la aplicación React y contiene los vínculos React y Personalizado, así como el uso de React Context para facilitar la integración del Experience Platform.

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

   El `EventCollectorContext` exporta el contexto de React que:

   - carga la biblioteca commerce-events-sdk y commerce-events-collector,
   - los inicializa con una configuración determinada para Experience Platform o ACDS
   - se suscribe a todos los eventos de Peregrine y los reenvía al SDK de eventos

   Puede revisar los detalles de implementación de `EventCollectorContext` [aquí](https://github.com/adobe/aem-core-cif-components/blob/3d4e44d81fff2f398fd2376d24f7b7019f20b31b/extensions/experience-platform-connector/src/events-collector/EventCollectorContext.js).

### AEM Creación e implementación del proyecto de actualizado

AEM Para asegurarse de que los cambios de instalación, código y configuración del paquete anterior son correctos, vuelva a compilar e implemente el proyecto de Commerce actualizado mediante el siguiente comando Maven: `$ mvn clean install -PautoInstallSinglePackage`.

## configuración del Experience Platform {#aep-setup}

AEM Para recibir y almacenar los datos de evento procedentes de las páginas de comercio de la, como categoría y producto, complete los siguientes pasos:

>[!AVAILABILITY]
>
>Asegúrese de que forma parte de la __Perfiles de producto__ bajo __Adobe Experience Platform__ y __Recopilación de datos de Adobe Experience Platform__. Si es necesario, trabaje con el administrador del sistema para crear, actualizar o asignar __Perfiles de producto__ en el [Admin Console](https://adminconsole.adobe.com/).

### Crear esquema con el grupo de campos Comercio

Para definir la estructura de los datos de evento de comercio, debe crear un esquema del Modelo de datos de experiencia (XDM). Un esquema es un conjunto de reglas que representan y validan la estructura y el formato de los datos.

1. En el explorador, vaya a __Adobe Experience Platform__ Página de inicio del producto. Por ejemplo, <https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>.

1. Busque el __Esquemas__ en la sección de navegación izquierda, haga clic en el __Crear esquema__ en la sección superior derecha y seleccione. __ExperienceEvent de XDM__.

   ![Crear esquema AEP](../assets/aep-integration/AEP-Schema-EventSchema-1.png)

1. Asigne un nombre al esquema mediante la variable __Propiedades del esquema > Nombre para mostrar__ y añadir grupos de campos mediante el  __Composición > Grupos de campos > Añadir__ botón.

   ![Definición de esquema de AEP](../assets/aep-integration/AEP-Schema-Definition.png)

1. En el __Agregar grupos de campos__ diálogo, buscar `Commerce`, seleccione la __Detalles de comercio__ y haga clic en __Agregar grupos de campos__.

   ![Definición de esquema de AEP](../assets/aep-integration/AEP-Schema-Field-Group.png)


>[!TIP]
>
>Consulte la [Conceptos básicos de composición de esquemas](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html) para obtener más información.

### Crear conjunto de datos

Para almacenar los datos de evento, debe crear un Conjunto de datos que se ajuste a la definición del esquema. Un conjunto de datos es una construcción de almacenamiento y administración para una colección de datos (normalmente una tabla) que contiene un esquema (columnas) y campos (filas).

1. En el explorador, vaya a __Adobe Experience Platform__ Página de inicio del producto. Por ejemplo, <https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>.

1. Busque el __Conjuntos de datos__ en la sección de navegación izquierda y haga clic en el botón __Crear conjunto de datos__ de la sección superior derecha.

   ![Crear conjuntos de datos AEP](../assets/aep-integration/AEP-Datasets-Create.png)

1. En la nueva página, seleccione __Crear conjunto de datos a partir de esquema__ Tarjeta de.

   ![Opción de esquema Crear conjuntos de datos AEP](../assets/aep-integration/AEP-Datasets-Schema-Option.png)

   En la nueva página, __buscar y seleccionar__ Seleccione el esquema que ha creado en el paso anterior y haga clic en __Siguiente__ botón.

   ![Crear conjuntos de datos y seleccionar esquema AEP](../assets/aep-integration/AEP-Datasets-Select-Schema.png)

1. Asigne un nombre al conjunto de datos mediante __Configurar conjunto de datos > Nombre__ y haga clic en el __Finalizar__ botón.

   ![Nombre de creación de conjuntos de datos AEP](../assets/aep-integration/AEP-Datasets-Name.png)

>[!TIP]
>
>Consulte la [Información general sobre conjuntos de datos](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html) para obtener más información.


### Crear flujo de datos

Complete los siguientes pasos para poder crear una secuencia de datos en el Experience Platform.

1. En el explorador, vaya a __Adobe Experience Platform__ Página de inicio del producto. Por ejemplo, <https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>.

1. Busque el __Datastreams__ en la sección de navegación izquierda y haga clic en el botón __Nueva secuencia de datos__ de la sección superior derecha.

   ![Crear flujos de datos AEP](../assets/aep-integration/AEP-Datastream-Create.png)

1. Asigne un nombre a la secuencia de datos mediante __Nombre__ campo obligatorio. En el __Esquema de evento__ , seleccione el esquema creado y haga clic en __Guardar__.

   ![Definir flujos de datos AEP](../assets/aep-integration/AEP-Datastream-Define.png)

1. Abra la secuencia de datos creada y haga clic en __Añadir servicio__.

   ![Añadir servicio de flujos de datos AEP](../assets/aep-integration/AEP-Datastream-Add-Service.png)

1. En el __Servicio__ , seleccione el campo __Adobe Experience Platform__ opción. En __Conjunto de datos de evento__ , seleccione el nombre del conjunto de datos del paso anterior y haga clic en __Guardar__.

   ![Detalles del servicio Añadir flujos de datos AEP](../assets/aep-integration/AEP-Datastream-Add-Service-Define.png)

>[!TIP]
>
>Consulte la [Resumen de flujo de datos](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html) para obtener más información.

## AEM Añadir valor de flujo de datos a la configuración de comercio de {#add-aep-values-to-aem}

Después de completar la configuración del Experience Platform anterior, debe tener lo siguiente `datastreamId` en el carril izquierdo de la secuencia de datos, detalles y `orgId` en la esquina superior derecha de la __Imagen de perfil > Información de cuenta > Información de usuario__ modal.

![ID de flujos de datos AEP](../assets/aep-integration/AEP-Datastream-ID.png)

1. AEM En el proyecto de comercio de la `ui.frontend` módulo, actualice el `config.js` y, específicamente, el `eventsCollector > aep` propiedades del objeto.

1. AEM Cree e implemente el proyecto actualizado de Commerce


## Déclencheur `addToCart` y verificar la recopilación de datos {#event-trigger-verify}

AEM Los pasos anteriores completan la configuración de comercio y Experience Platform de la. Ahora puede almacenar en déclencheur una `addToCart` y verificar la recopilación de datos con la extensión Google Chrome _Inspector quitanieves_ y conjunto de datos __Métricas y gráficos__ en la interfaz de usuario del producto.

Para almacenar en déclencheur AEM el evento, puede utilizar el autor de la publicación o el servicio de publicación desde la configuración local de, o bien utilizar el autor de la publicación desde la configuración local de. AEM Para este ejemplo, inicie sesión en su cuenta para utilizar el autor de la.

1. En la página Sitios, seleccione __Mi tienda de demostraciónFront > us > es__ y haga clic en __Editar__ en la barra de acciones superior.

1. En la barra de acciones superior, haga clic en __Ver como aparece publicado__, luego haz clic en cualquier categoría preferida en la navegación de la tienda.

1. Haga clic en cualquier tarjeta de producto preferida de __Página de productos__, luego seleccione __color, tamaño__ para habilitar el __Añadir al carro__ botón.


1. Abra el __Inspector quitanieves__ en el panel de extensiones del explorador y seleccione. __SDK de Experience Platform Wed__ en el carril izquierdo.


1. Vuelva a la __Página de productos__ y haga clic en __Añadir al carro__ botón. Esto envía datos al Experience Platform. El __Adobe Experience Platform Debugger__ La extensión muestra los detalles del evento.

   ![Event-Data de complemento al carro de AEP Debugger](../assets/aep-integration/AEP-Debugger-AddToCart-EventData.png)



1. En la interfaz de usuario del producto de Experience Platform, vaya a __Conjuntos de datos > Mi tienda de demostraciónFront__, en __Actividad de conjunto de datos__ pestaña. If __Métricas y gráficos__ está activada, se muestran las estadísticas de datos de evento.

   ![Estadísticas de datos del conjunto de datos Experience Platform](../assets/aep-integration/AEP-Dataset-AddToCart-EventData.png)



## Detalles de implementación {#implementation-details}

El [CIF Conector del Experience Platform de](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) se basa en el [Conexión de datos para Adobe Commerce](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html), que forma parte del [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/) proyecto.

El proyecto PWA Studio permite crear tiendas de Progressive Web Application (PWA) con Adobe Commerce o Magento Open Source. El proyecto también contiene una biblioteca de componentes llamada [Peregrina](https://developer.adobe.com/commerce/pwa-studio/api/peregrine/) para agregar lógica a los componentes visuales. El [Biblioteca Peregrina](https://developer.adobe.com/commerce/pwa-studio/api/peregrine/) también proporciona los vínculos React personalizados que utilizan [CIF Conector del Experience Platform de](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) para integrarse perfectamente con Experience Platform.


## Eventos admitidos {#supported-events}

A partir de ahora, se admiten los siguientes eventos:

__Eventos de Experience XDM:__

1. AEM Añadir al carro ()
1. AEM Ver página ()
1. Ver producto (AEM)
1. AEM Solicitud de búsqueda enviada ()
1. AEM Respuesta de búsqueda recibida ()

Cuándo [Componentes de Peregrine](https://developer.adobe.com/commerce/pwa-studio/guides/packages/peregrine/) AEM se reutilizan en el proyecto de comercio de la:

__Eventos de Experience XDM:__

1. Eliminar del carro
1. Abrir carro
1. Ver carro
1. Compra instantánea
1. Iniciar cierre de compra
1. Finalizar pago y envío

__Eventos XDM de perfil:__

1. Iniciar sesión
1. Crear cuenta
1. Editar cuenta


## Recursos adicionales {#additional-resources}

Para obtener más información, consulte los siguientes recursos:

- [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/)
- [[!DNL Data Connection] descripción general](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/overview.html)
- [[!DNL Data Connection] Eventos](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/event-forwarding/events.html)
- [Información general de Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/home.html)
