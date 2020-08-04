---
title: Introducción a AEM comercio como Cloud Service
description: Introducción a AEM comercio como Cloud Service
translation-type: tm+mt
source-git-commit: 1fcdfa60c134491c781906e4a757a3a10399bde1
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 3%

---


# Introducción a AEM comercio como Cloud Service {#start}

Para comenzar con AEM comercio como Cloud Service, su Experience Manager Cloud Service debe estar aprovisionado con el complemento Commerce Integration Framework (CIF). El complemento CIF es un módulo adicional sobre [AEM Sites como Cloud Service](https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-service/sites/home.html).

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

## Integración {#onboarding}

La integración de AEM comercio como Cloud Service es un proceso de dos pasos:

1. Obtenga AEM comercio como Cloud Service habilitado y el complemento CIF aprovisionado
2. Conectar AEM comercio como Cloud Service con su entorno Magento

El primer paso se realiza por Adobe. Deberá proporcionar información como la organización IMS, la dirección URL del extremo GraphQL del entorno del Magento, etc. como parte del proceso de aprovisionamiento. Para obtener más información sobre precios y aprovisionamiento, debe ponerse en contacto con su representante de ventas.

Una vez que haya sido aprovisionado con el complemento CIF, se aplicará a cualquier programa existente del Administrador de nube. En caso de que no tenga un Programa de Cloud Manager, deberá crear uno nuevo. Para obtener más información, consulte [Configuración del Programa](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/getting-started/setting-up-program.html).

El segundo paso es el autoservicio para cada AEM como entorno Cloud Service. Hay algunas configuraciones adicionales que deberá realizar después del aprovisionamiento inicial del complemento CIF.

## Conexión de AEM comercio con Magento {#magento}

Para conectar el complemento CIF y los [AEM componentes](https://github.com/adobe/aem-core-cif-components) principales de CIF con el entorno de Magento, debe proporcionar la URL del extremo de Magento GraphQL mediante una variable de entorno de Cloud Manager. El nombre de la variable es `COMMERCE_ENDPOINT`. Se debe configurar una conexión segura mediante HTTPS.
Se puede usar una dirección URL de extremo de GraphQL de Magento diferente para cada AEM como entorno de Cloud Service. De este modo, los proyectos pueden conectar AEM entornos de ensayo con sistemas de ensayo Magento y AEM entorno de producción a un sistema de producción Magento. El extremo de Magento GraphQL debe estar disponible para el público, no se admiten conexiones privadas VPN o locales.

Para conectar AEM comercio con Magento, siga estos pasos:

1. Obtenga la CLI de E/S de Adobe con el complemento Cloud Manager

   Consulte la documentación [de](https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) Adobe Cloud Manager sobre cómo descargar, configurar y utilizar la CLI [de E/S de](https://github.com/adobe/aio-cli) Adobe con el complemento [CLI de](https://github.com/adobe/aio-cli-plugin-cloudmanager)Cloud Manager.

2. Autentique la CLI con la AEM como programa Cloud Service

3. Configure la `COMMERCE_ENDPOINT` variable en Cloud Manager

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   Consulte los documentos [de CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) para obtener más detalles.

   La URL del extremo de Magento GraphQL debe apuntar al servicio GraphQl de Magento y utilizar una conexión HTTPS segura. Por ejemplo: `https://demo.magentosite.cloud/graphql`.

>[!TIP]
>
>Puede realizar la lista de todas las variables de Cloud Manager mediante el siguiente comando para comprobar el doble: `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

>[!Note]
>
>También puede utilizar la API [de](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html) Cloud Manager para configurar las variables de Cloud Manager.

Con esto, está listo para usar AEM Commerce como Cloud Service y puede implementar su proyecto a través de Cloud Manager.

## Integraciones de comercio de terceros {#integrations}

Para integraciones comerciales de terceros, se necesita una capa [de asignación de](architecture/third-party.md) API para conectar AEM Commerce como Cloud Service y componentes principales de CIF con su sistema comercial. Esta capa de asignación de API suele implementarse en Adobe I/O Runtime. Póngase en contacto con su representante de ventas para obtener integraciones disponibles y acceso a Adobe I/O Runtime.
