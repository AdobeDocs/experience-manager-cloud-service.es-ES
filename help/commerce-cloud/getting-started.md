---
title: Introducción a AEM Commerce as a Cloud Service
description: Obtenga información sobre cómo implementar un proyecto de AEM habilitado para el comercio en un AEM en ejecución como entorno de servicio de nube. Utilice las funciones de Adobe Cloud Manager y una canalización CI/CD para crear la tienda de referencia de Venia en un entorno en ejecución.
topics: Commerce
feature: Commerce Integration Framework, Cloud Manager
version: cloud-service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
translation-type: tm+mt
source-git-commit: b3abefb2953080443e220a248dd4484d23c09a0e
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 93%

---


# Introducción a AEM Commerce as a Cloud Service {#start}

Para comenzar con AEM Commerce as a Cloud Service, Experience Manager Cloud Service debe estar aprovisionado con el complemento Commerce Integration Framework (CIF). El complemento CIF es un módulo adicional sobre [AEM Sites as a Cloud Service](https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-service/sites/home.html).

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

## Incorporación {#onboarding}

La incorporación de AEM Commerce as a Cloud Service es un proceso de dos pasos:

1. Obtenga AEM Commerce as a Cloud Service habilitado y el complemento CIF aprovisionado.
2. Conecte AEM Commerce as a Cloud Service en su entorno Magento.

El primer paso lo realiza Adobe. Deberá proporcionar información como la organización IMS, la dirección URL del extremo GraphQL del entorno del Magento, etc. como parte del proceso de aprovisionamiento. Para obtener más información sobre precios y aprovisionamiento, debe ponerse en contacto con su representante de ventas.

Una vez que haya sido aprovisionado con el complemento CIF, se aplicará a cualquier programa existente de Cloud Manager. En caso de que no tenga un programa de Cloud Manager, deberá crear uno nuevo. Para obtener más información, consulte [Configuración del programa](https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-manager/using/getting-started/setting-up-program.html).

El segundo paso es el autoservicio para cada entorno de AEM as a Cloud Service. Hay algunas configuraciones adicionales que deberá realizar después del aprovisionamiento inicial del complemento CIF.

## Conexión de AEM Commerce con Magento {#magento}

Para conectar el complemento CIF y los [componentes principales del CIF de AEM](https://github.com/adobe/aem-core-cif-components) con el entorno de Magento, debe proporcionar la URL de extremo de Magento GraphQL mediante una variable de entorno de Cloud Manager. El nombre de la variable es `COMMERCE_ENDPOINT`. Se debe configurar una conexión segura mediante un HTTPS.
Se puede usar una dirección URL de extremo de Magento GraphQL diferente para cada entorno de AEM as a Cloud Service. De este modo, los proyectos pueden conectar los entornos de ensayo de AEM con los sistemas de ensayo de Magento y el entorno de producción de AEM a un sistema de producción de Magento. El extremo de Magento GraphQL debe estar disponible para el público, no se admiten conexiones privadas VPN o locales.

Para realzar la conexión de AEM Commerce con Magento, siga estos pasos:

1. Obtenga la CLI de Adobe I/O con el complemento Cloud Manager

   Consulte la [documentación de Adobe Cloud Manager](https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) sobre cómo descargar, configurar y utilizar la [CLI de Adobe I/O](https://github.com/adobe/aio-cli) con el [complemento CLI de Cloud Manager](https://github.com/adobe/aio-cli-plugin-cloudmanager).

2. Autentique la CLI como programa de AEM as a Cloud Service

3. Configure la `COMMERCE_ENDPOINT` variable en Cloud Manager

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   Consulte [los documentos sobre CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) para obtener más detalles.

   La dirección URL de extremo de Magento GraphQL debe señalar al servicio Magento GraphQL y utilizar una conexión HTTPS segura. Por ejemplo: `https://demo.magentosite.cloud/graphql`.

>[!TIP]
>
>Puede realizar la lista de todas las variables de Cloud Manager usando el siguiente comando para comprobarlas: `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

>[!NOTE]
>
>Como alternativa, también puede utilizar la [API de Cloud Manager](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html) para configurar las variables de Cloud Manager.

Con esto, está listo para usar AEM Commerce as a Cloud Service y puede implementar su proyecto a través de Cloud Manager.

## Integraciones de comercio de terceros {#integrations}

Para integraciones de comercio de terceros, se necesita una [capa de asignación de API](architecture/third-party.md) para conectar AEM Commerce as a Cloud Service y los componentes principales del CIF con su sistema comercial. Esta capa de asignación de API suele implementarse en Adobe I/O Runtime. Póngase en contacto con su representante de ventas para obtener integraciones disponibles y acceso a Adobe I/O Runtime.
