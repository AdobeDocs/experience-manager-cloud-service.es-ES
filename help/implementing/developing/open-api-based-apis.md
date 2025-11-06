---
title: API basadas en OpenAPI
description: Obtenga información acerca de la compatibilidad de AEM as a Cloud Service con las API basadas en OpenAPI
feature: Developing
role: Admin, Developer
exl-id: 4aeafba9-8f9e-4ecb-9e37-8d048b0474cc
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 1%

---

# API basadas en OpenAPI {#openapi-based-apis}

Las nuevas API de AEM as a Cloud Service siguen la especificación de OpenAPI y, por lo tanto, ofrecen un conjunto de API coherente y bien documentado.

>[!NOTE]
>
> Un [tutorial completo](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) es un recurso recomendado para aprender a configurar e invocar las API de AEM basadas en OpenAPI.

En el caso de los extremos que requieren autenticación, el método de autenticación difiere según el extremo, pero puede utilizar OAuth Servidor a servidor, OAuth Web App o OAuth Single Page App (SPA). Las credenciales se configuran mediante proyectos en [Adobe Developer Console](https://developer.adobe.com/developer-console/).

Los casos de uso comunes de la API implican integraciones con sistemas como CRM o PIM, donde las API de AEM se invocan para recuperar o mantener datos. Como parte de la implementación de la integración, las aplicaciones pueden suscribirse a [eventos emitidos por AEM](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-eventing/overview), que pueden almacenar en déclencheur la lógica empresarial en Adobe App Builder u otra infraestructura.

Este documento sirve como información general, pero hay documentación más detallada disponible en las siguientes páginas:

* Los vínculos de la sección API basada en OpenAPI de [documentación de referencia](https://developer.adobe.com/experience-cloud/experience-manager-apis/). La documentación de referencia de cada API también incluye un área de reproducción de API, lo que facilita la prueba de un extremo mediante un token de portador generado con Adobe Developer Console.

* [Guías](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/) de información, incluidos [conceptos y sintaxis de API](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/how-to/).

* Un tutorial de nivel superior que describe [enfoques de autenticación](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/overview#authentication-support) y otros conceptos.

* Un tutorial con vídeo centrado en [cómo configurar las API basadas en OpenAPI](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup).

* [Un tutorial completo](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) sobre la configuración y la invocación de OpenAPI con la estrategia de autenticación de servidor a servidor. También se pueden encontrar tutoriales similares para los enfoques de autenticación de Aplicación web y Aplicación de una sola página.

## Configuración del acceso a API {#configuring-api-access}

Algunas API de AEM basadas en OpenAPI necesitan autenticación, lo que requiere que se generen credenciales con [Adobe Developer Console](https://developer.adobe.com/developer-console/). La configuración implica los siguientes pasos:

1. Modernización del entorno de AEM as a Cloud Service. Para obtener más información, consulte el tutorial [Modernización del entorno de AEM as a Cloud Service](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup?#modernization-of-aem-as-a-cloud-service-environment).
1. Habilite el acceso a las API de AEM mediante Perfiles de producto. Los perfiles de producto están asociados a los servicios que representan a los grupos de usuarios de AEM con listas de control de acceso (ACL) predefinidas. Aunque algunos servicios están asociados de manera predeterminada con perfiles de producto específicos, otros necesitan estar asociados explícitamente; por ejemplo, el servicio Usuarios de la API de AEM Assets no está asociado con ningún [Perfil de producto](/help/onboarding/aem-cs-team-product-profiles.md#aem-product-profiles), por lo que debe habilitarlo para que utilice la API de AEM Assets. Para obtener más información, consulte el paso del tutorial [Habilitar el acceso a las API de AEM](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup#enable-aem-apis-access).
1. Para añadir la autenticación de servidor a servidor, la integración de configuración del usuario debe ser el administrador del sistema de la organización en Adobe Admin Console o agregarse como desarrollador al perfil de producto donde está asociado el servicio. Para obtener más información, consulte el paso del tutorial [Habilitar el acceso a las API de AEM](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup#enable-aem-apis-access).
1. Crear un proyecto de Adobe Developer Console (ADC).
1. Configure el proyecto ADC. Esto genera credenciales que se utilizarán más adelante para intercambiar un token de portador al invocar la API.
1. Configure la instancia de AEM para habilitar la comunicación del proyecto ADC. Esto implica registrar el ID de cliente con el entorno mediante la configuración e implementación de un archivo YAML, tal como se describe en la sección [Registro de un ID de cliente](#registering-a-client-id) a continuación.

Para obtener instrucciones detalladas paso a paso, consulte el [tutorial Configurar API basadas en OpenAPI](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup).

### Registro de un ID de cliente {#registering-a-client-id}

Los ID de cliente vinculan las API de un proyecto de Adobe Developer Console a entornos de AEM específicos. Esto se logra de la siguiente manera:

1. Cree un archivo con el nombre `api.yaml` o similar con una configuración como el fragmento siguiente, incluidos los niveles deseados (autor, publicación y vista previa). Los valores de `Client_id` deben provenir de sus proyectos de API de Adobe Developer Console.

   Las propiedades `kind`, `version` y `metadata` se describen en el artículo [Canalización de configuración](/help/operations/config-pipeline.md#common-syntax). El valor de la propiedad `kind` debe establecerse en *API* y la propiedad `version` debe establecerse en *1*.

   ```
   kind: "API"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     allowedClientIDs:
       author:
         - "<client_id>"
       publish:
         - "<client_id>"
       preview:
         - "<client_id>"
   ```

1. Coloque el archivo en algún lugar bajo una carpeta de nivel superior llamada `config` o similar, como se describe en [Canalización de configuración](/help/operations/config-pipeline.md#folder-structure).
1. Para tipos de entorno distintos de RDE (que usa herramientas de línea de comandos), cree una canalización de configuración de implementación de destino en Cloud Manager, tal como se hace referencia en [esta sección](/help/operations/config-pipeline.md#creating-and-managing) en el artículo Canalización de configuración. Tenga en cuenta que las canalizaciones de pila completa y de nivel web no implementan el archivo de configuración.
1. Implemente la configuración de.
