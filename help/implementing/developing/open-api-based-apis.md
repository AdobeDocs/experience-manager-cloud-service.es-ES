---
title: API basadas en OpenAPI
description: Obtenga información acerca de la compatibilidad de AEM as a Cloud Service con las API basadas en OpenAPI
feature: Developing
role: Admin, Architect, Developer
exl-id: 4aeafba9-8f9e-4ecb-9e37-8d048b0474cc
source-git-commit: e735f7d2a39e3165907969d2e27565639499a636
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 1%

---

# API basadas en OpenAPI {#openapi-based-apis}

>[!NOTE]
>
>Las API abiertas están disponibles como parte de un programa de acceso anticipado. Si está interesado en acceder a ellos, le recomendamos que envíe un correo electrónico a [aem-apis@adobe.com](mailto:aem-apis@adobe.com) con una descripción de su caso de uso.

Las nuevas API de AEM as a Cloud Service siguen la especificación de OpenAPI y, por lo tanto, producen API coherentes, bien documentadas y fáciles de usar. Encontrará información detallada en las siguientes páginas:

* Un [tutorial completo](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) sobre cómo configurar e invocar las API de AEM basadas en OpenAPI mediante la autenticación de servidor a servidor.
* [Guías](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/) de información, incluidos [conceptos y sintaxis de API](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/how-to/).
* Extremo de API [documentación de referencia](https://developer.adobe.com/experience-cloud/experience-manager-apis/), donde algunas de las API están basadas en OpenAPI, como [esta API de Sites](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/). La documentación de referencia también incluye un área de reproducción de API, que facilita la prueba de un extremo mediante un token de portador generado con Adobe Developer Console.

Un caso de uso común de la API implica integraciones con sistemas como CRM o PIM, donde las API de AEM se invocan para recuperar o mantener datos. Como parte de la implementación de la integración, las aplicaciones pueden suscribirse a [eventos emitidos por AEM](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-eventing/overview), que pueden almacenar en déclencheur la lógica empresarial en Adobe App Builder u otra infraestructura.

Los tipos de autenticación de API admitidos difieren según el extremo, pero pueden ser de servidor a servidor OAuth, OAuth Web App y OAuth Single Page App (SPA).

>[!NOTE]
>
> El [tutorial completo](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) es un recurso recomendado para aprender a configurar e invocar las API de AEM basadas en OpenAPI.


## Configuración del acceso a API {#configuring-api-access}

Muchas API de AEM basadas en OpenAPI requieren autenticación, lo que requiere que se generen credenciales con [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/). La configuración implica los siguientes pasos:

1. Asegúrese de que los [perfiles de producto del programa AEM se hayan actualizado](/help/onboarding/aem-cs-team-product-profiles.md#aem-product-profiles) y de que tenga habilitado un servicio apropiado para acceder a la API que desee.
1. Cree un nuevo proyecto en Adobe Developer Console y añada las API deseadas al proyecto, seleccionando también el tipo de autenticación adecuado.
1. Genere la credencial, que más adelante se utilizará para intercambiar por un token de portador al invocar la API.
1. Registre el ID de cliente con el entorno configurando un archivo YAML, que se implementa mediante la canalización de configuración (o la línea de comandos para RDE).

Consulte el tutorial [Configurar API basadas en OpenAPI](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/setup) para obtener instrucciones paso a paso.

## Registro de un ID de cliente {#registering-a-client-id}

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
