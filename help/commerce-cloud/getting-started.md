---
title: Introducción a AEM Commerce as a Cloud Service
description: AEM AEM Obtenga información sobre cómo implementar un proyecto de habilitado para el comercio en un entorno de as a Cloud Service en ejecución. Utilice las funciones de Adobe Cloud Manager y una canalización de CI/CD para crear la tienda de referencia de Venia en un entorno en ejecución.
topics: Commerce
feature: Commerce Integration Framework, Cloud Manager
version: Cloud Service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
exl-id: 73ba707e-5e2d-459a-8cc8-846d1a5f2fd7
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 28%

---

# Introducción a AEM Commerce as a Cloud Service {#start}

Para comenzar con AEM Commerce as a Cloud Service, Experience Manager Cloud Service debe estar aprovisionado con el complemento Commerce Integration Framework (CIF). El complemento CIF es un módulo adicional sobre [AEM Sites as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/home.html).

## Incorporación {#onboarding}

La incorporación de AEM Commerce as a Cloud Service es un proceso de dos pasos:

1. Obtenga AEM Commerce as a Cloud Service habilitado y el complemento CIF aprovisionado.
2. AEM Conectar el comercio de la as a Cloud Service con su solución de comercio

El primer paso de incorporación se realiza por Adobe. Para obtener más información sobre precios y aprovisionamiento, debe ponerse en contacto con su representante de ventas.

Una vez que se le haya aprovisionado con el complemento CIF, se aplica a cualquier programa existente de Cloud Manager. En caso de que no tenga un programa de Cloud Manager, deberá crear uno nuevo. Para obtener más información, consulte [Configuración del programa](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html).

El segundo paso es el autoservicio para cada entorno de AEM as a Cloud Service. Hay algunas configuraciones adicionales que deberá realizar después del aprovisionamiento inicial del complemento CIF.

## AEM Conectarse a los clientes con una solución de comercio {#solution}

Para conectar el complemento CIF y la [AEM Componentes principales de CIF](https://github.com/adobe/aem-core-cif-components) con una solución de comercio, debe proporcionar la URL del extremo de GraphQL a través de una variable de entorno de Cloud Manager. El nombre de la variable es `COMMERCE_ENDPOINT`. Se debe configurar una conexión segura mediante un HTTPS.

Esta variable de entorno se utiliza en dos lugares:

- Llamadas de GraphQL AEM AEM desde el servidor de comercio a través de un cliente de GraphQl que se puede compartir de forma habitual y que utilizan los componentes principales del CIF y los componentes de proyecto del cliente de la.
- Configure una URL de proxy de GraphQL AEM en cada entorno en el que la variable se establezca y esté disponible en `/api/graphql`. AEM Esto lo utilizan las herramientas de creación de comercio de (complemento CIF) y los componentes del lado del cliente del CIF.

Se puede usar una dirección URL de extremo de GraphQL diferente para cada entorno de AEM as a Cloud Service. AEM AEM De este modo, los proyectos pueden conectar entornos de ensayo de la con sistemas de ensayo de comercio y entornos de producción de la segmentación con un sistema de producción de comercio. El extremo de GraphQL debe estar disponible para el público, no se admiten conexiones privadas VPN o locales. Opcionalmente, se puede proporcionar un encabezado de autenticación para utilizar funciones de CIF adicionales que requieran autenticación.

De forma opcional, y solo para Adobe Commerce AEM Enterprise/Cloud, el complemento CIF admite el uso de datos de catálogo clasificados para autores de informes en la fase de creación de la. Esto requiere configurar un encabezado de autorización. AEM Por motivos de seguridad, este encabezado solo está disponible y se utiliza en instancias de autor de. AEM Las instancias de publicación no pueden mostrar datos clasificados.

Hay dos opciones para configurar el punto de conexión:

### A través de la interfaz de usuario de Cloud Manager (predeterminada) {#cm-ui}

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

Esto se puede hacer mediante un cuadro de diálogo en la página Detalles del entorno. Al ver esta página para un programa habilitado para Commerce, se muestra un botón si el punto de conexión no está configurado actualmente:

![Información del entorno de CM](/help/commerce-cloud/assets/commerce-cmui.png)

Al hacer clic en este botón, se abre un cuadro de diálogo:

![Punto final de CM Commerce](/help/commerce-cloud/assets/commerce-cm-endpoint.png)

Una vez definido el punto de conexión y, opcionalmente, un encabezado de autorización para la compatibilidad con catálogos clasificados, el punto de conexión se muestra en la página de detalles. Al hacer clic en el icono Editar se abrirá el mismo cuadro de diálogo en el que el punto de conexión se puede modificar si es necesario.

![Información del entorno de CM](/help/commerce-cloud/assets/commerce-cmui-done.png)

### Mediante CLI de Adobe I/O  {#adobe-cli}

AEM Para conectarse con una solución de comercio a través de la CLI de Adobe I/O, siga estos pasos:

1. Obtenga la CLI de Adobe I/O con el complemento Cloud Manager

   Compruebe la [Documentación de Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=es) sobre cómo descargar, configurar y utilizar [CLI DE ADOBE I/O](https://github.com/adobe/aio-cli) con el [Complemento CLI de Cloud Manager](https://github.com/adobe/aio-cli-plugin-cloudmanager).

2. Autentique la CLI de Adobe I/O AEM con el programa as a Cloud Service de la

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

   Configure las variables `COMMERCE_AUTH_HEADER` variable secreta en Cloud Manager:

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization: Bearer <Access Token>"
   ```

>[!TIP]
>
>Puede realizar la lista de todas las variables de Cloud Manager usando el siguiente comando para comprobarlas: `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

Con esto, está listo para usar AEM Commerce as a Cloud Service y puede implementar su proyecto a través de Cloud Manager.

## Configuración de tiendas y catálogos {#catalog}

El complemento CIF y la [Componentes principales del CIF](https://github.com/adobe/aem-core-cif-components) AEM se puede utilizar en varias estructuras de sitio de conectadas a diferentes tiendas comerciales (o vistas de tiendas, etc.). De forma predeterminada, el complemento CIF se implementa con una configuración predeterminada que se conecta a la tienda y el catálogo predeterminados de Adobe Commerce.

Esta configuración se puede ajustar para el proyecto a través de la configuración del Cloud Service del CIF siguiendo estos pasos:

1. AEM En el paso de la sesión, vaya a Herramientas -> Cloud Services -> Configuración del CIF

2. Seleccione la configuración de comercio que desee cambiar

3. Abra las propiedades de configuración a través de la barra de acciones

![Configuración de Cloud Services del CIF](/help/commerce-cloud/assets/cif-cloud-service-config.png)

Se pueden configurar las siguientes propiedades:

- Cliente de GraphQL: seleccione el cliente de GraphQL configurado para la comunicación back-end comercial. Esto debería permanecer en modo predeterminado.
- Vista de tienda: el identificador de la vista de tienda. Si está vacía, se utiliza la vista de tienda predeterminada.
- Ruta del proxy de GraphQL: la ruta URL del proxy de GraphQL AEM que se utiliza para las solicitudes de proxy al extremo de GraphQL backend de comercio.
  >[!NOTE]
  >
  > En la mayoría de las configuraciones, el valor predeterminado `/api/graphql` no se debe cambiar. Solo la configuración avanzada que no utiliza el proxy de GraphQL proporcionado debe cambiar esta configuración.
- Habilitar compatibilidad con UID de catálogo: habilite la compatibilidad con UID en lugar de con ID en las llamadas comerciales de GraphQL back-end.
  >[!NOTE]
  >
  > La compatibilidad con UID se ha introducido en Adobe Commerce 2.4.2. Habilite esta opción solo si el backend de Commerce admite un esquema GraphQL de la versión 2.4.2 o posterior.
- Identificador de categoría raíz del catálogo: el identificador (UID o ID) de la raíz del catálogo de la tienda
  >[!CAUTION]
  >
  > A partir de la versión 2.0.0 de los componentes principales del CIF, la compatibilidad con `id` se ha eliminado y reemplazado por `uid`. Si su proyecto utiliza la versión 2.0.0 de los componentes principales del CIF, debe habilitar la compatibilidad con el UID de catálogo y utilizar un UID de categoría válido como &quot;Identificador de categoría raíz del catálogo&quot;.

La configuración que se muestra arriba es como referencia. Los proyectos deben proporcionar sus propias configuraciones.

AEM Para obtener configuraciones más complejas que utilicen varias estructuras de sitio de la combinadas con diferentes catálogos de comercio, consulte la [Configuración de varias tiendas de Commerce](configuring/multi-store-setup.md) tutorial.

## Recursos adicionales {#additional-resources}

- [Tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype)
- [Tienda de referencia de Venia de AEM](https://github.com/adobe/aem-cif-guides-venia)
- [Configuración de varias tiendas de Commerce](configuring/multi-store-setup.md)
- [Configuración de varios sistemas de comercio](configuring/multiple-commerce-systems-setup.md)

