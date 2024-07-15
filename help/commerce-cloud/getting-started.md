---
title: Introducción a AEM Commerce as a Cloud Service
description: Aprenda a implementar un proyecto de comercio de Adobe Experience Manager AEM () mediante Adobe Cloud Manager, una canalización de CI/CD y la tienda de referencia de Venia.
topics: Commerce
feature: Commerce Integration Framework, Cloud Manager
version: Cloud Service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
exl-id: 73ba707e-5e2d-459a-8cc8-846d1a5f2fd7
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '1066'
ht-degree: 10%

---

# Introducción a AEM Commerce as a Cloud Service {#start}

Para empezar a usar Adobe Experience Manager AEM () Commerce as a Cloud Service, el Experience Manager Cloud Service debe estar aprovisionado con el complemento Commerce integration framework CIF (). CIF El complemento es un módulo adicional sobre [AEM Sites as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/home.html).

## Incorporación {#onboarding}

La incorporación de AEM Commerce as a Cloud Service es un proceso de dos pasos:

1. Obtenga AEM Commerce as a Cloud Service habilitado y el complemento CIF aprovisionado.
2. AEM Conectar Commerce as a Cloud Service con su solución de comercio

El primer paso de incorporación se realiza por Adobe. Para obtener más información sobre precios y aprovisionamiento, debe ponerse en contacto con su representante de ventas.

CIF Una vez que se le haya aprovisionado con el complemento de, se aplicará a cualquier programa de Cloud Manager existente. Si no tiene un programa de Cloud Manager, debe crear uno. Para obtener más información, consulta [Configurar tu programa](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/getting-started/program-setup.html).

El segundo paso es el autoservicio para cada entorno de AEM as a Cloud Service. CIF Hay algunas configuraciones adicionales que debe realizar después del aprovisionamiento inicial del complemento de.

## AEM Conectarse a un cliente con una solución de Commerce {#solution}

CIF AEM CIF Para conectar el complemento de y los [componentes principales de la](https://github.com/adobe/aem-core-cif-components) con una solución de comercio, debe proporcionar la dirección URL del extremo de GraphQL mediante una variable de entorno de Cloud Manager. El nombre de la variable es `COMMERCE_ENDPOINT`. Se debe configurar una conexión segura mediante HTTPS.

Esta variable de entorno se utiliza en dos lugares:

- Llamadas de GraphQL AEM AEM CIF desde el servidor de comercio a través de un cliente de GraphQl que se puede compartir de forma habitual y que utilizan los componentes principales de los clientes y los componentes de proyecto del cliente de la.
- Configure una URL de proxy de GraphQL AEM en cada entorno en el que la variable esté disponible en `/api/graphql`. AEM CIF CIF Esta URL la utilizan las herramientas de creación de comercio de la (complemento de) y los componentes del lado del cliente de la.

Se puede utilizar una dirección URL de extremo de GraphQL diferente para cada entorno de AEM as a Cloud Service. AEM AEM De este modo, los proyectos pueden conectar entornos de ensayo de la con sistemas de ensayo de comercio y entornos de producción de la segmentación con un sistema de producción de comercio. Ese extremo de GraphQL debe estar disponible para el público, no se admiten conexiones privadas VPN o locales. CIF Opcionalmente, se puede proporcionar un encabezado de autenticación para utilizar funciones de autenticación adicionales que requieran autenticación.

De forma opcional, y solo para Adobe Commerce CIF AEM Enterprise/Cloud, el complemento de admite el uso de datos de catálogo clasificados para autores de informes en la fase de creación de informes Estos datos requieren que configure un encabezado de autorización. AEM Este encabezado solo está disponible y se utiliza en instancias de Autor de por motivos de seguridad. AEM Las instancias de Publish no pueden mostrar datos clasificados.

Hay dos opciones para configurar el punto de conexión:

### Mediante la interfaz de usuario de Cloud Manager (predeterminada) {#cm-ui}

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

Esta configuración se puede realizar mediante un cuadro de diálogo en la página Detalles del entorno. Al ver esta página para un programa habilitado para Commerce, se muestra un botón si el punto de conexión no está configurado actualmente:

![Información del entorno de CM](/help/commerce-cloud/assets/commerce-cmui.png)

Al hacer clic en este botón, se abre un cuadro de diálogo:

![Extremo de Commerce de CM](/help/commerce-cloud/assets/commerce-cm-endpoint.png)

Una vez definido el punto de conexión y, opcionalmente, un encabezado de autorización para la compatibilidad con catálogos clasificados, el punto de conexión se muestra en la página de detalles. Haga clic en el icono Editar para abrir el mismo cuadro de diálogo en el que puede editar el punto de conexión, si es necesario.

![Información del entorno de CM](/help/commerce-cloud/assets/commerce-cmui-done.png)

### Mediante CLI de Adobe I/O  {#adobe-cli}

AEM Para conectarse con una solución de comercio mediante CLI de Adobe I/O, siga estos pasos:

1. Obtenga la CLI de Adobe I/O con el complemento Cloud Manager

   Consulte la [documentación de Cloud Manager de Adobe](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=es) sobre cómo descargar, configurar y utilizar la [CLI de Adobe I/O](https://github.com/adobe/aio-cli) con el complemento [Cloud Manager CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager).

2. Autentique la CLI de Adobe I/O con el programa AEM as a Cloud Service

3. Configure la `COMMERCE_ENDPOINT` variable en Cloud Manager

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   Consulte [los documentos sobre CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) para obtener más detalles.

   La dirección URL del extremo de GraphQL de comercio debe señalar al servicio GraphQl de comercio y utilizar una conexión HTTPS segura. Por ejemplo: `https://<yourcommercesystem>/graphql`.

4. Habilitar las funciones de catálogo preconfigurado que requieren autenticación (opcional)

   >[!NOTE]
   >
   >Esta función solo está disponible con Adobe Commerce Enterprise o Cloud Edition. Consulte [Autenticación basada en tokens](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens) para obtener más información.

   Establecer la variable secreta `COMMERCE_AUTH_HEADER` en Cloud Manager:

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization: Bearer <Access Token>"
   ```

>[!TIP]
>
>Puede realizar la lista de todas las variables de Cloud Manager usando el siguiente comando para comprobarlas: `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

AEM Está listo para usar el as a Cloud Service de Commerce de la y puede implementar su proyecto a través de Cloud Manager.

## Configuración de tiendas y catálogos {#catalog}

CIF CIF AEM El complemento de datos y los [componentes principales de la lista de distribución de datos](https://github.com/adobe/aem-core-cif-components) se pueden usar en varias estructuras de sitio conectadas a diferentes tiendas comerciales (o vistas de tiendas, etc.), y se pueden usar en varias estructuras de sitio de la lista de distribución de datos. CIF De forma predeterminada, el complemento de se implementa con una configuración predeterminada que se conecta a la tienda y al catálogo predeterminados de Adobe Commerce.

CIF Esta configuración se puede ajustar para el proyecto mediante la configuración del Cloud Service de la aplicación de la manera siguiente:

1. AEM En la página de inicio, vaya a Herramientas > Cloud Service CIF > Configuración de la.

2. Seleccione la configuración de comercio que desee cambiar.

3. Abra las propiedades de configuración mediante la barra de acciones.

CIF ![Configuración de Cloud Service de](/help/commerce-cloud/assets/cif-cloud-service-config.png)

Se pueden configurar las siguientes propiedades:

- Cliente de GraphQL: seleccione el cliente de GraphQL configurado para la comunicación back-end comercial. Este cliente debería permanecer en modo predeterminado.
- Vista de tienda: el identificador de la vista de tienda. Si está vacía, se utiliza la vista de tienda predeterminada.
- Ruta del proxy de GraphQL: la ruta URL del proxy de GraphQL AEM que se utiliza para las solicitudes de proxy al extremo de GraphQL backend de comercio.
  >[!NOTE]
  >
  > En la mayoría de las configuraciones, no se debe cambiar el valor predeterminado `/api/graphql`. Solo la configuración avanzada que no utiliza el proxy de GraphQL proporcionado debe cambiar esta configuración.
- Habilitar compatibilidad con UID de catálogo: habilite la compatibilidad con UID en lugar de con ID en las llamadas comerciales de GraphQL back-end.
  >[!NOTE]
  >
  > La compatibilidad con UID se ha introducido en Adobe Commerce 2.4.2. Habilite los UID únicamente si el backend de Commerce admite un esquema GraphQL de la versión 2.4.2 o posterior.
- Identificador de categoría raíz del catálogo: el identificador (UID o ID) de la raíz del catálogo de la tienda
  >[!CAUTION]
  >
  > CIF A partir de la versión 2.0.0 de los componentes principales de la, se quitó la compatibilidad con `id` y se reemplazó con `uid`. CIF Si el proyecto utiliza componentes principales de la versión 2.0.0 de la, debe habilitar la compatibilidad con UID de catálogo y utilizar un UID de categoría válido como &quot;Identificador de categoría raíz de catálogo&quot;.

La configuración que se muestra arriba es como referencia. Los proyectos deben proporcionar sus propias configuraciones.

AEM Para configuraciones más complejas, usando múltiples estructuras de sitio combinadas con diferentes catálogos de comercio, vea el tutorial [Configuración de varias tiendas Commerce](configuring/multi-store-setup.md).

## Recursos adicionales {#additional-resources}

- [Tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype)
- [Tienda de referencia de Venia de AEM](https://github.com/adobe/aem-cif-guides-venia)
- [Configuración de varias tiendas de Commerce](configuring/multi-store-setup.md)
- [Varias configuraciones de sistemas de Commerce](configuring/multiple-commerce-systems-setup.md)

