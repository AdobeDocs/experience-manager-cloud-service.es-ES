---
title: Materiales de referencia de la API
description: AEM tiene API amplias y potentes que puede utilizar para su proyecto de experiencia digital.
exl-id: d4ef3040-5a0a-4149-9e99-09eda9605038
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 5%

---

# Materiales de referencia de la API {#api-reference-materials}

Adobe Experience Manager (AEM) proporciona muchas API para desarrollar aplicaciones y ampliar AEM. AEM se basa en varias tecnologías de código abierto, que también se pueden utilizar.

## API principales de AEM {#core-aem-apis}

Las siguientes API son fundamentales para AEM.

| API | Descripción |
|---|---|
| [Adobe Experience Manager as a Cloud Service](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) | Abstracciones de productos, como páginas, recursos, flujos de trabajo, etc. |
| [IU de Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html#) | Pila web abierta de Adobe que proporciona varios componentes esenciales (los materiales Granite 6.5 se aplican a AEMaaCS) |
| [IU de Coral](https://opensource.adobe.com/coral-spectrum/documentation/) | Estilo visual de Adobe para IU en la nube, diseñado para proporcionar coherencia en la experiencia del usuario |

<!---
|Editor core JavaScript API reference|Provides all the base objects and concepts to support authoring of content resources|
--->

>[!NOTE]
>
>Para obtener la información más reciente sobre las API de Experience Manager, visite también [API de Adobe Experience Manager as a Cloud Service](https://developer.adobe.com/experience-cloud/experience-manager-apis/).

## Marcos de trabajo adicionales {#additional-apis}

AEM se basa en varias API de código abierto adicionales.

| API | Descripción |
|---|---|
| [Apache Sling](https://sling.apache.org/apidocs/sling11/) | Marco web que utiliza un repositorio de contenido Java (JCR) para almacenar y administrar contenido |
| [Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | Implementación de un repositorio de contenido Java (JCR) jerárquico, escalable y de alto rendimiento que se utilizará como base de los sitios web modernos de primera clase |
| [Repositorio de contenido Java](https://www.adobe.io/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) | Especificación de la versión 2.0 de JCR |
| [Apache Felix](https://felix.apache.org) | Implementación del marco y la plataforma de servicios de la iniciativa Open Services Gateway (OSGi) |

## Directrices de preferencias de API {#guidelines}

AEM se basa en los cuatro conjuntos de API de Java principales siguientes en orden descendente de preferencia.

| Prioridad | API | Descripción |
|---|---|---|
| 1 | [Adobe Experience Manager as a Cloud Service](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) | Abstracciones de productos, como páginas, recursos, flujos de trabajo, etc. |
| 2 | [Apache Sling](https://sling.apache.org/apidocs/sling11/) | REST y abstracciones basadas en recursos como recursos, mapas de valores y solicitudes HTTP. |
| 3 | [Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | Resumen de datos y contenido, como nodos, propiedades y sesiones. |
| 4 | [Apache Felix](https://felix.apache.org/) | Abstracciones del contenedor de aplicaciones OSGi, como servicios y componentes (OSGi). |

Si AEM proporciona una API, prefiera esta en lugar de Sling, JCR y OSGi. Si AEM no proporciona una API, prefiera Sling sobre JCR y OSGi.

>[!TIP]
>
>Para obtener más información sobre estas directrices, consulte el documento [Comprender las prácticas recomendadas de la API de Java](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html).

## API y servicios de envío y administración de contenido de AEM {#delivery-apis}

AEM ofrece componentes personalizables y opciones de entrega de contenido.

| Función | Descripción |
|---|---|
| [Los componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) | Componentes estandarizados de administración de contenido web (WCM) para AEM a fin de acelerar el tiempo de desarrollo y reducir el coste de mantenimiento de los sitios web |
| [Exportador JSON](/help/implementing/developing/components/json-exporter.md) | Enviar el contenido de cualquier página de AEM en formato de modelo de datos JSON |
| [Habilitación de la exportación de JSON para un componente](/help/implementing/developing/components/enabling-json-exporter.md) | Generar una exportación JSON del contenido del componente en función de un marco de modelado |
| [API abiertas de modelos de fragmentos de contenido y fragmentos de contenido](/help/headless/content-fragment-openapis.md) | API abiertas de modelos de fragmentos de contenido y fragmentos de contenido |
| [Envío de fragmentos de contenido de AEM con OpenAPI](/help/headless/aem-content-fragment-delivery-with-openapi.md) | Una API de REST HTTP en AEM Edge Delivery Services, diseñada para entregar contenido estructurado desde fragmentos de contenido en formato JSON. |
| [API de GraphQL de fragmento de contenido](/help/headless/graphql-api/content-fragments.md) | Habilite la entrega eficiente de fragmentos de contenido a clientes de JavaScript en implementaciones de CMS sin encabezado |
|  |  |
| [API de Assets](/help/assets/mac-api-assets.md) | Permite operaciones de creación, lectura, actualización y eliminación (CRUD) en recursos, incluidos binarios, metadatos, representaciones y comentarios. Consulte API HTTP de AEM Assets |
| [Fragmentos de contenido: API HTTP](/help/assets/content-fragments/assets-api-content-fragments.md) | Acceso al contenido de fragmentos de contenido directamente a través de la API HTTP mediante operaciones CRUD |
| [Fragmentos de contenido API HTTP de Assets](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html?lang=es) | Formato exacto de las solicitudes de recursos HTTP admitidas |

>[!NOTE]
>
>Consulte [API de AEM para la administración y entrega de contenido estructurado](/help/headless/apis-headless-and-content-fragments.md) para obtener una descripción general de las diversas API disponibles y una comparación de algunos de los conceptos involucrados.

## API específicas de SPA {#spa-apis}

El marco de trabajo del Editor de aplicaciones de una sola página (SPA) de AEM SDK proporciona referencias específicas de la API de JavaScript.

| API | Descripción |
|---|---|
| [Asignación de componentes](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping) | Proporciona una forma para que la aplicación de una sola página asigne componentes front-end a tipos de recursos de Adobe Experience Manager (componentes de AEM) |
| [Administrador de modelos de página](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager) | Un intérprete entre Adobe Experience Manager Editor y el Editor de aplicaciones de una sola página (SPA) de Adobe Experience Manager |
| [Componentes editables de React](https://www.npmjs.com/package/@adobe/aem-react-editable-components) | Proporciona los componentes de React y la capa de integración para ayudarle a empezar con el Editor del sitio de Adobe Experience Manager |
| [Componentes editables de Angular](https://www.npmjs.com/package/@adobe/aem-angular-editable-components) | Proporciona los componentes de Angular y la capa de integración para ayudarle a empezar con el Editor del sitio de Adobe Experience Manager |

>[!TIP]
>
>Consulte la [Introducción y tutorial de SPA](/help/implementing/developing/hybrid/introduction.md) para obtener más información sobre las aplicaciones de una sola página.
