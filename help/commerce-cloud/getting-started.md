---
title: Introducción a AEM Commerce as a Cloud Service
description: Obtenga información sobre cómo implementar un proyecto de AEM habilitado para comercio en un entorno de AEM en ejecución as a Cloud Service. Utilice las funciones de Adobe Cloud Manager y una canalización CI/CD para crear la tienda de referencia de Venia en un entorno en ejecución.
topics: Commerce
feature: Commerce Integration Framework, Cloud Manager
version: Cloud Service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
exl-id: 73ba707e-5e2d-459a-8cc8-846d1a5f2fd7
source-git-commit: f5e465d90477f1b49e4ff1c5ca9dd47cc5d539bb
workflow-type: tm+mt
source-wordcount: '1095'
ht-degree: 29%

---

# Introducción a AEM Commerce as a Cloud Service {#start}

Para comenzar con AEM Commerce as a Cloud Service, Experience Manager Cloud Service debe estar aprovisionado con el complemento Commerce Integration Framework (CIF). El complemento CIF es un módulo adicional sobre [AEM Sites as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/home.html).

## Incorporación {#onboarding}

La incorporación de AEM Commerce as a Cloud Service es un proceso de dos pasos:

1. Obtenga AEM Commerce as a Cloud Service habilitado y el complemento CIF aprovisionado.
2. Conecte AEM Commerce as a Cloud Service con su solución de comercio

El primer paso de incorporación se realiza por Adobe. Para obtener más información sobre precios y aprovisionamiento, debe ponerse en contacto con su representante de ventas.

Una vez que haya sido aprovisionado con el complemento CIF, se aplicará a cualquier programa existente de Cloud Manager. En caso de que no tenga un programa de Cloud Manager, deberá crear uno nuevo. Para obtener más información, consulte [Configuración del programa](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html).

El segundo paso es el autoservicio para cada entorno de AEM as a Cloud Service. Hay algunas configuraciones adicionales que deberá realizar después del aprovisionamiento inicial del complemento CIF.

## Conexión de AEM con una solución de comercio {#solution}

Para conectar el complemento CIF y el [Componentes principales del CIF de AEM](https://github.com/adobe/aem-core-cif-components) con una solución de comercio, debe proporcionar la URL de extremo de GraphQL mediante una variable de entorno de Cloud Manager. El nombre de la variable es `COMMERCE_ENDPOINT`. Se debe configurar una conexión segura mediante un HTTPS.

Esta variable de entorno se utiliza en dos lugares:

- GraphQL realiza llamadas desde AEM hasta el back-end de comercio, a través de algunos clientes comunes que se pueden compartir con GraphQl, y que utilizan los componentes principales del CIF de AEM y los componentes del proyecto del cliente.
- Configure una URL proxy de GraphQL en cada entorno de AEM en el que la variable esté disponible en `/api/graphql`. Esto lo utilizan las herramientas de creación de comercio de AEM (complemento CIF) y los componentes del cliente CIF.

Se puede usar una dirección URL de extremo de GraphQL diferente para cada entorno de AEM as a Cloud Service. De este modo, los proyectos pueden conectar AEM entornos de ensayo con sistemas de ensayo comerciales y AEM entorno de producción a un sistema de producción comercial. El extremo de GraphQL debe estar disponible para el público, no se admiten conexiones privadas VPN o locales. Opcionalmente, se puede proporcionar un encabezado de autenticación para utilizar funciones de CIF adicionales que requieran autenticación.

De forma opcional y solo para Adobe Commerce Enterprise/Cloud, el complemento CIF admite el uso de datos de catálogo clasificados para AEM autores. Esto requiere configurar un encabezado de autorización. Este encabezado solo está disponible y se utiliza en AEM instancias de autor por motivos de seguridad. AEM instancias de publicación no pueden mostrar datos clasificados.

Hay dos opciones para configurar el extremo:

### A través de la interfaz de usuario de Cloud Manager (predeterminada) {#cm-ui}

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

Esto se puede hacer mediante un cuadro de diálogo en la página Detalles del entorno . Al ver esta página para un programa habilitado para comercio, se mostrará un botón si el extremo no está configurado actualmente:

![Información sobre el entorno de CM](/help/commerce-cloud/assets/commerce-cmui.png)

Al hacer clic en este botón, se abre un cuadro de diálogo:

![Punto final de comercio de CM](/help/commerce-cloud/assets/commerce-cm-endpoint.png)

Después de establecer el punto final y, opcionalmente, un encabezado de autorización para la compatibilidad con el catálogo por etapas, el punto final se mostrará en la página de detalles. Al hacer clic en el icono Editar se abrirá el mismo cuadro de diálogo en el que el punto final se puede modificar si es necesario.

![Información sobre el entorno de CM](/help/commerce-cloud/assets/commerce-cmui-done.png)

### Mediante CLI de Adobe I/O  {#adobe-cli}

Para conectar AEM con una solución de comercio a través de la CLI de Adobe I/O, siga estos pasos:

1. Obtenga la CLI de Adobe I/O con el complemento Cloud Manager

   Marque la [Documentación de Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=es) sobre cómo descargar, configurar y usar el [CLI de Adobe I/O](https://github.com/adobe/aio-cli) con la variable [Complemento CLI de Cloud Manager](https://github.com/adobe/aio-cli-plugin-cloudmanager).

2. Autentique la CLI de Adobe I/O con el programa as a Cloud Service AEM

3. Configure la `COMMERCE_ENDPOINT` variable en Cloud Manager

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   Consulte [los documentos sobre CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) para obtener más detalles.

   La dirección URL de extremo de Commerce GraphQL debe apuntar al servicio de GraphQl del comercio y utilizar una conexión HTTPS segura. Por ejemplo: `https://<yourcommercesystem>/graphql`.

4. Habilitar las funciones del catálogo por etapas que requieren autenticación (opcional)

   >[!NOTE]
   >
   >Esta función solo está disponible con Adobe Commerce Enterprise o Cloud Edition. Consulte [Autenticación basada en tokens](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens) para obtener más información.

   Configure las variables `COMMERCE_AUTH_HEADER` variable secreta en Cloud Manager:

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization: Bearer <Access Token>"
   ```

>[!TIP]
>
>Puede realizar la lista de todas las variables de Cloud Manager usando el siguiente comando para comprobarlas: `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

Con esto, está listo para usar AEM Commerce as a Cloud Service y puede implementar su proyecto a través de Cloud Manager.

## Configuración de tiendas y catálogos {#catalog}

El complemento CIF y el [Componentes principales de CIF](https://github.com/adobe/aem-core-cif-components) se puede utilizar en varias estructuras de sitios AEM conectadas a diferentes tiendas de comercio (o vistas de tiendas, etc.). De forma predeterminada, el complemento CIF se implementa con una configuración predeterminada que se conecta al catálogo y la tienda predeterminados de Adobe Commerce.

Esta configuración se puede ajustar para el proyecto mediante la configuración del Cloud Service del CIF siguiendo estos pasos:

1. En AEM vaya a Herramientas -> Cloud Services -> Configuración del CIF

2. Seleccione la configuración de comercio que desee cambiar

3. Abra las propiedades de configuración mediante la barra de acciones

![Configuración de Cloud Services del CIF](/help/commerce-cloud/assets/cif-cloud-service-config.png)

Se pueden configurar las siguientes propiedades:

- Cliente de GraphQL: seleccione el cliente de GraphQL configurado para la comunicación de back-end de comercio. Esto suele permanecer de forma predeterminada.
- Vista de almacén: el identificador de vista de tienda. Si está vacía, se utilizará la vista de tienda predeterminada.
- Ruta de proxy de GraphQL: la ruta de URL del proxy GraphQL AEM usar para solicitudes de proxy al extremo de comercio back-end GraphQL.
   >[!NOTE]
   >
   > En la mayoría de las configuraciones, el valor predeterminado `/api/graphql` no debe cambiarse. Solo la configuración avanzada que no utilice el proxy de GraphQL proporcionado debe cambiar esta configuración.
- Habilitar compatibilidad con UID de catálogo : habilite la compatibilidad con UID en lugar de con ID en las llamadas de GraphQL de comercio back-end.
   >[!NOTE]
   >
   > La compatibilidad con UID se ha introducido en Adobe Commerce 2.4.2. Solo debe habilitarse si el back-end de comercio admite un esquema de GraphQL de la versión 2.4.2 o posterior.
- Identificador de categoría raíz del catálogo: el identificador (UID o ID) de la raíz del catálogo del almacén
   >[!CAUTION]
   >
   > A partir de la versión 2.0.0 de los componentes principales de CIF, la compatibilidad con `id` se ha eliminado y se ha reemplazado por `uid`. Si su proyecto utiliza los componentes principales del CIF versión 2.0.0, debe activar la compatibilidad con el UID del catálogo y utilizar un UID de categoría válido como &quot;Identificador de categoría raíz del catálogo&quot;.

La configuración que se muestra arriba es para referencia. Los proyectos deben proporcionar sus propias configuraciones.

Para obtener configuraciones más complejas que utilizan varias estructuras de sitios de AEM combinadas con distintos catálogos de comercio, consulte la [Configuración de varias tiendas de comercio](configuring/multi-store-setup.md) tutorial.

## Recursos adicionales {#additional-resources}

- [Tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype)
- [Tienda de referencia de Venia de AEM](https://github.com/adobe/aem-cif-guides-venia)
- [Configuración de varias tiendas de comercio](configuring/multi-store-setup.md)
