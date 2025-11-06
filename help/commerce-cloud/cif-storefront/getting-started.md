---
title: Introducción a AEM Commerce as a Cloud Service
description: Aprenda a implementar un proyecto de comercio de Adobe Experience Manager (AEM) mediante Adobe Cloud Manager, una canalización de CI/CD y la tienda de referencia de Venia.
topics: Commerce
feature: Commerce Integration Framework, Cloud Manager
version: Experience Manager as a Cloud Service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
exl-id: 73ba707e-5e2d-459a-8cc8-846d1a5f2fd7
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 9%

---


# Introducción a AEM Commerce as a Cloud Service {#start}

Para empezar a usar Adobe Experience Manager (AEM) Commerce as a Cloud Service, su Experience Manager Cloud Service debe estar aprovisionado con el complemento de Commerce integration framework (CIF). El complemento de CIF es un módulo adicional sobre [AEM Sites as a Cloud Service.](/help/sites-cloud/sites-cloud-changes.md)

>[!TIP]
>
>**¿Has considerado Edge Delivery Services?**
>
>Edge Delivery Services es la solución preferida de Adobe para crear una tienda. Consulte el documento [Introducción y descripción general](/help/commerce-cloud/introduction.md) para obtener más información.

## Incorporación {#onboarding}

La incorporación de AEM Commerce as a Cloud Service es un proceso de dos pasos:

1. Obtenga AEM Commerce as a Cloud Service habilitado y el complemento CIF aprovisionado.
1. Conecte AEM Commerce as a Cloud Service con su solución de comercio

El primer paso de incorporación lo realiza Adobe. Para obtener más información sobre precios y aprovisionamiento, debe ponerse en contacto con su representante de ventas.

Una vez que se le haya proporcionado el complemento de CIF, se aplicará a cualquier programa de Cloud Manager existente. Si no tiene un programa de Cloud Manager, debe crear uno. Para obtener más información, consulte [Configurar el programa.](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/getting-started/program-setup.html?lang=es)

El segundo paso es el autoservicio para cada entorno de AEM as a Cloud Service. Hay algunas configuraciones adicionales que debe realizar después del aprovisionamiento inicial del complemento de CIF.

## Conexión de AEM con una solución de Commerce {#solution}

Para conectar el complemento CIF y los [componentes principales de AEM CIF](https://github.com/adobe/aem-core-cif-components) con una solución de comercio, debe proporcionar la dirección URL del extremo GraphQL mediante una variable de entorno de Cloud Manager. El nombre de la variable es `COMMERCE_ENDPOINT`. Se debe configurar una conexión segura mediante HTTPS.

Esta variable de entorno se utiliza en dos lugares:

* GraphQL llama desde AEM al back-end del comercio a través de algunos clientes comunes de GraphQL que se pueden compartir y que utilizan los componentes principales y de proyecto del cliente de AEM CIF.
* Configure una URL de proxy de GraphQL en cada entorno de AEM donde la variable esté disponible en `/api/graphql`. Esta URL la utilizan las herramientas de creación de comercio de AEM (complemento de CIF) y los componentes de cliente de CIF.

Se puede utilizar una dirección URL de extremo de GraphQL diferente para cada entorno de AEM as a Cloud Service. De este modo, los proyectos pueden conectar los entornos de ensayo de AEM con los sistemas de ensayo de comercio y el entorno de producción de AEM a un sistema de producción de comercio. Ese extremo de GraphQL debe estar disponible para el público, no se admiten conexiones privadas VPN o locales. Opcionalmente, se puede proporcionar un encabezado de autenticación para utilizar funciones de CIF adicionales que requieran autenticación.

De forma opcional, y solo para Adobe Commerce Enterprise/Cloud, el complemento de CIF admite el uso de datos de catálogo clasificados para autores de AEM. Estos datos requieren que configure un encabezado de autorización. Este encabezado solo está disponible y se utiliza en instancias de autor de AEM por motivos de seguridad. Las instancias de publicación de AEM no pueden mostrar datos clasificados.

Hay dos opciones para configurar el punto de conexión:

### Mediante la interfaz de usuario de Cloud Manager (predeterminada) {#cm-ui}

>[!VIDEO](https://video.tv.adobe.com/v/343270?captions=spa&quality=12&learn=on)

Esta configuración se puede realizar mediante un cuadro de diálogo en la página Detalles del entorno. Al ver esta página para un programa habilitado para Commerce, se muestra un botón si el punto de conexión no está configurado actualmente:

![Información del entorno de CM](/help/commerce-cloud/cif-storefront/assets/commerce-cmui.png)

Al hacer clic en este botón, se abre un cuadro de diálogo:

![Extremo de Commerce de CM](/help/commerce-cloud/cif-storefront/assets/commerce-cm-endpoint.png)

Una vez definido el punto de conexión y, opcionalmente, un encabezado de autorización para la compatibilidad con catálogos clasificados, el punto de conexión se muestra en la página de detalles. Haga clic en el icono Editar para abrir el mismo cuadro de diálogo en el que puede editar el punto de conexión, si es necesario.

![Información del entorno de CM](/help/commerce-cloud/cif-storefront/assets/commerce-cmui-done.png)

### Mediante CLI de Adobe I/O  {#adobe-cli}

Para conectar AEM con una solución de comercio mediante Adobe I/O CLI, siga estos pasos:

1. Obtenga la CLI de Adobe I/O con el complemento Cloud Manager.

   * Consulte la [documentación de Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=es) sobre cómo descargar, configurar y utilizar la [CLI de Adobe I/O](https://github.com/adobe/aio-cli) con el complemento [Cloud Manager CLI.](https://github.com/adobe/aio-cli-plugin-cloudmanager)

1. Autentique la CLI de Adobe I/O con el programa de AEM as a Cloud Service.

1. Establezca la variable `COMMERCE_ENDPOINT` en Cloud Manager.

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   * Consulte [los documentos sobre CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) para obtener más detalles.

   * La dirección URL del extremo de GraphQL de comercio debe señalar al servicio GraphQl de comercio y utilizar una conexión HTTPS segura. Por ejemplo: `https://<yourcommercesystem>/graphql`.

1. Habilite las funciones de catálogo en zona intermedia que requieran autenticación (opcional).

   >[!NOTE]
   >
   >Esta función solo está disponible con Adobe Commerce Enterprise o Cloud Edition. Consulte [Autenticación basada en tokens](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens) para obtener más información.

   * Establecer la variable secreta `COMMERCE_AUTH_HEADER` en Cloud Manager:

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization: Bearer <Access Token>"
   ```

>[!TIP]
>
>Puede realizar la lista de todas las variables de Cloud Manager usando el siguiente comando para comprobarlas: `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

Está listo para usar AEM Commerce as a Cloud Service y puede implementar su proyecto mediante Cloud Manager.

## Configuración de tiendas y catálogos {#catalog}

El complemento de CIF y los [componentes principales de CIF](https://github.com/adobe/aem-core-cif-components) se pueden usar en varias estructuras de sitio de AEM conectadas a diferentes tiendas de comercio (o vistas de tiendas, etc.). De forma predeterminada, el complemento de CIF se implementa con una configuración predeterminada que se conecta a la tienda y al catálogo predeterminados de Adobe Commerce.

Esta configuración se puede ajustar para el proyecto mediante la configuración de CIF Cloud Service siguiendo estos pasos:

1. En AEM, vaya a Herramientas > Cloud Services > Configuración de CIF.

1. Seleccione la configuración de comercio que desee cambiar.

1. Abra las propiedades de configuración mediante la barra de acciones.

![Configuración de CIF Cloud Services](/help/commerce-cloud/cif-storefront/assets/cif-cloud-service-config.png)

Se pueden configurar las siguientes propiedades:

* Cliente de GraphQL: seleccione el cliente de GraphQL configurado para la comunicación back-end comercial. Este cliente debería permanecer en modo predeterminado.
* Vista de tienda: el identificador de la vista de tienda. Si está vacía, se utiliza la vista de tienda predeterminada.
* Ruta del proxy de GraphQL: la ruta URL que utiliza el proxy de GraphQL en AEM para las solicitudes de proxy al extremo de GraphQL backend de comercio.

  >[!NOTE]
  >
  > En la mayoría de las configuraciones, no se debe cambiar el valor predeterminado `/api/graphql`. Solo la configuración avanzada que no utiliza el proxy de GraphQL proporcionado debe cambiar esta configuración.

* Habilitar la compatibilidad con UID del catálogo: habilite la compatibilidad con UID en lugar del ID en las llamadas de GraphQL del backend comercial.

  >[!NOTE]
  >
  > La compatibilidad con UID se ha introducido en Adobe Commerce 2.4.2. Habilite los UID únicamente si el backend de Commerce admite un esquema GraphQL de la versión 2.4.2 o posterior.

* Identificador de categoría raíz del catálogo: el identificador (UID o ID) de la raíz del catálogo de la tienda.

  >[!CAUTION]
  >
  > A partir de la versión 2.0.0 de los componentes principales de CIF, se quitó la compatibilidad con `id` y se reemplazó con `uid`. Si su proyecto utiliza los componentes principales de CIF versión 2.0.0, debe habilitar la compatibilidad con Catalog UID y utilizar un UID de categoría válido como &quot;Identificador de categoría raíz de catálogo&quot;.

La configuración que se muestra arriba es como referencia. Los proyectos deben proporcionar sus propias configuraciones.

Para configuraciones más complejas que utilicen varias estructuras de sitio de AEM combinadas con distintos catálogos comerciales, consulte el tutorial [Configuración de varias tiendas Commerce](/help/commerce-cloud/cif-storefront/configuring/multi-store-setup.md).

## Recursos adicionales {#additional-resources}

* [Tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype)
* [Tienda de referencia de Venia de AEM](https://github.com/adobe/aem-cif-guides-venia)
* [Configuración de varias tiendas de Commerce](/help/commerce-cloud/cif-storefront/configuring/multi-store-setup.md)
* [Varias configuraciones de sistemas de Commerce](/help/commerce-cloud/cif-storefront/configuring/multiple-commerce-systems-setup.md)
