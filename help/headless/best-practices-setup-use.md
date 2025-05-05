---
title: AEM Prácticas recomendadas para la configuración y el uso de GraphQL con fragmentos de contenido para la administración de contenido
description: AEM Conozca las Prácticas recomendadas para la configuración y el uso de GraphQL con fragmentos de contenido de la aplicación.
exl-id: 4d6a5aaa-c8be-4858-ad07-085dc4fb77e7
feature: Headless
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 24%

---

# AEM Prácticas recomendadas para la configuración y el uso de GraphQL con fragmentos de contenido para la administración de contenido{#best-practices-setup-use-aem-graphql-content-fragments}

AEM Estas directrices resumen las prácticas recomendadas para configurar y utilizar la configuración de fragmentos de contenido y GraphQL con el fin de utilizar la.

## Introducción {#getting-started}

Para ayudarle a ponerse al día:

* [¿Qué es sin encabezado?](/help/headless/what-is-headless.md)
* AEM Información general sobre los distintos entornos de la [Arquitectura](/help/headless/deployment/architecture.md) de la

## Configuración {#setup}

AEM Para configurar GraphQL de forma segura para su uso con fragmentos de contenido y sus aplicaciones, debe configurar varios componentes.

### Creación de extremos de GraphQL (incluida la seguridad) {#graphql-endpoint-creation}

El punto de conexión es la ruta utilizada para acceder a GraphQL para AEM. Estos extremos deben crearse y publicarse para que se pueda acceder a ellos de forma segura.

#### Detalles {#details-graphql-endpoint-creation}

[Administración de puntos de conexión de GraphQL en AEM](/help/headless/graphql-api/graphql-endpoint.md)

#### Entornos {#environments-graphql-endpoint-creation}

Los extremos deben configurarse en:

* Autor
* Vista previa
* Publicación

Para:

* Desarrollo
* Pruebas
* Producción

### AEM Almacenamiento en caché de Dispatcher {#dispatcher-caching}

>[!NOTE]
>Si el almacenamiento en caché en Dispatcher está habilitado, no es necesario configurar [CORS](#cors-setup), por lo que se puede ignorar.

El almacenamiento en caché de consultas persistentes no está habilitado de forma predeterminada en Dispatcher. La activación predeterminada no es posible, ya que los clientes que utilizan CORS (Intercambio de recursos de origen cruzado) con varios orígenes deben revisar, y posiblemente actualizar, su configuración de Dispatcher.

#### Detalles {#details-dispatcher-caching}

[Consultas persistentes de GraphQL: habilitar el almacenamiento en caché en Dispatcher](/help/headless/deployment/dispatcher-caching.md)

#### Entornos {#environments-dispatcher-caching}

Dispatcher suele estar configurado para lo siguiente:

* Publish: production

### Configuración de CORS {#cors-setup}

>[!NOTE]
>AEM Si el almacenamiento en caché en [Dispatcher](#dispatcher-caching) está habilitado, no es necesario configurar CORS y, por lo tanto, esta sección se puede ignorar.

Para acceder al punto de conexión de GraphQL AEM AEM, se debe configurar una política CORS y añadirla a un proyecto de que se implemente a través de Cloud Manager para que se pueda implementar a través de la interfaz de usuario. Para ello, añada un archivo de configuración OSGi CORS apropiado para los puntos de conexión deseados.

#### Detalles {#details-cors-setup}

[Configuración de Intercambio de Recursos de Origen Cruzado (CORS)](/help/headless/deployment/cross-origin-resource-sharing.md)

#### Entornos {#environments-cors-setup}

CORS suele estar configurado para:

* Publish: production

### Autenticación {#authentication}

Un caso de uso principal para la API de Adobe Experience Manager as a Cloud Service AEM () GraphQL para la entrega de fragmentos de contenido es aceptar consultas remotas desde aplicaciones o servicios de terceros. Estas consultas remotas pueden requerir acceso a una API autenticada para asegurar la entrega de contenido sin encabezado.

#### Detalles {#details-authentication}

[Autenticación para consultas de AEM de GraphQL remotas en fragmentos de contenido](/help/headless/security/authentication.md)

#### Entornos {#environments-authentication}

La autenticación suele configurarse para:

* Vista previa
* Publicación

Para:

* Desarrollo
* Pruebas
* Producción

### Permisos {#permissions}

Con una implementación sin encabezado, deben abordarse varias áreas de seguridad y permisos. Los permisos y los perfiles se pueden considerar en general, en función del entorno de AEM **Creación** o **Publicación**. Cada entorno contiene diferentes perfiles con distintas necesidades.

#### Detalles {#details-permissions}

[Consideraciones de permisos para contenido sin encabezado](/help/headless/security/permissions.md)

#### Entornos {#environments-permissions}

Los permisos suelen configurarse para:

* Autor
* Vista previa
* Publicación

Para:

* Desarrollo
* Pruebas
* Producción

### Uso de una red de distribución de contenido (CDN) {#cdn}

Las consultas GraphQL y sus respuestas JSON se pueden almacenar en caché si se dirigen como `GET` solicitudes al utilizar una CDN. Por el contrario, las solicitudes sin almacenar en caché pueden ser muy (recursos) costosas y lentas de procesar, con el potencial de tener más efectos perjudiciales en los recursos del origen.

#### Detalles {#details-cdn}

[CDN en AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md)

#### Entornos {#environments-cdn}

Una CDN suele configurarse para lo siguiente:

* Publish: production

### Configurar y crear fragmentos de contenido {#cconfigure-create-content-fragments}

AEM GraphQL se utiliza para recuperar información de los fragmentos de contenido. Deben configurarse y luego definirse una estructura y una ubicación para poder crear el contenido.

#### Detalles {#details-content-fragments}

* [Crear una configuración](/help/headless/setup/create-configuration.md)
* [Creación de un modelo de fragmento de contenido](/help/headless/setup/create-content-model.md)
* [Crear una carpeta de Assets](/help/headless/setup/create-assets-folder.md)
* [Cree y edite sus fragmentos de contenido](/help/headless/setup/create-content-fragment.md)

#### Entornos {#eenvironments-content-fragments}

Los fragmentos de contenido se definen, crean, prueban, publican y acceden a ellos en:

* Autor
* Vista previa
* Publicación

Para:

* Desarrollo
* Pruebas
* Producción

## AEM Uso de GraphQL {#use-aem-graphql}

### Optimización de las consultas de GraphQL {#optimize-graphql-queries}

Estas directrices se proporcionan para ayudar a evitar problemas de rendimiento con las consultas de GraphQL.

#### Detalles {#details-optimize-graphql-queries}

[Optimización de consultas de GraphQL](/help/headless/graphql-api/graphql-optimization.md)

>[!NOTE]
>
>Las directrices de optimización abarcan la configuración de la caché, que ya se trata en [Configuración](#setup).

### Acceso a GraphQL desde sus aplicaciones {#access-graphql-from-your-apps}

AEM El CMS sin encabezado proporciona a los desarrolladores la libertad de crear y ofrecer experiencias excepcionales utilizando los lenguajes, marcos y herramientas con los que ya están familiarizados.

#### Detalles {#details-your-apps}

* AEM [Instale y utilice el SDK de la para el desarrollo](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/aem-headless-sdk.html?lang=es)
* AEM [Recursos para desarrolladores sin encabezado](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=es)
* Ejemplos: [React](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/example-apps/react-app.html?lang=es), [Next.js](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/example-apps/next-js.html?lang=es), [Node.js](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/example-apps/server-to-server-app.html?lang=es), entre otros

#### Entornos {#environments-your-apps}

Las aplicaciones suelen desarrollarse, probarse y utilizarse en:

* Vista previa
* Publicación

Para:

* Desarrollo
* Pruebas
* Producción

### Recursos adicionales

AEM Para obtener más información acerca de los fragmentos de contenido y de GraphQL de, consulte lo siguiente:

* [API de GraphQL de AEM para su uso con fragmentos de contenido](/help/headless/graphql-api/content-fragments.md)
* [Uso del IDE de GraphiQL](/help/headless/graphql-api/graphiql-ide.md)
* AEM [Recursos para desarrolladores sin encabezado](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=es)
