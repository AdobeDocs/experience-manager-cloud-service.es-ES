---
title: Materiales de referencia de la API
description: AEM tiene API amplias y potentes que puede aprovechar para su proyecto de experiencia digital.
exl-id: d4ef3040-5a0a-4149-9e99-09eda9605038
source-git-commit: 08559417c8047c592f2db54321afe68836b75bd1
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 4%

---

# Materiales de referencia de la API {#api-reference-materials}

Adobe Experience Manager (AEM) proporciona muchas API para desarrollar aplicaciones y ampliar AEM. AEM se basa en una serie de tecnologías de código abierto, que también se pueden aprovechar.

## API principales de AEM {#core-aem-apis}

Las siguientes API son fundamentales para AEM.

| API | Descripción |
|---|---|
| [Adobe Experience Manager as a Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/index.html) | abstracciones de productos, como páginas, recursos, flujos de trabajo, etc. |
| [Interfaz de usuario de Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html#) | La pila Web abierta de Adobe, que proporciona varios componentes esenciales (tenga en cuenta que los materiales de Granite 6.5 se aplican a AEMaaCS) |
| [Interfaz de usuario de Coral](https://opensource.adobe.com/coral-spectrum/documentation/) | Estilo visual de Adobe para las IU en la nube, diseñado para proporcionar coherencia a la experiencia del usuario |

<!---
|Editor core JavaScript API reference|Provides all the base objects and concepts to support authoring of content resources|
--->

## Marcos adicionales {#additional-apis}

AEM se basa en varias API de código abierto adicionales.

| API | Descripción |
|---|---|
| [Apache Sling](https://sling.apache.org/apidocs/sling11/) | Marco web que utiliza un Repositorio de contenido Java (JCR) para almacenar y administrar contenido |
| [Apache Jackrabbit Oak](http://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | Implementación de un Repositorio de Contenido Java (JCR) jerárquico escalable y de alto rendimiento para su uso como base de sitios web modernos de nivel mundial |
| [Repositorio de contenido Java](https://www.adobe.io/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) | Especificación para la versión 2.0 de JCR |
| [Apache Felix](https://felix.apache.org) | Implementación del marco y la plataforma de servicios de la iniciativa Open Services Gateway (OSGi) |

## Directrices de preferencia de API {#guidelines}

AEM se basa en los cuatro conjuntos principales de API de Java siguientes en orden descendente de preferencia.

| Prioridad | API | Descripción |
|---|---|---|
| 1 | [Adobe Experience Manager as a Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/index.html) | abstracciones de productos, como páginas, recursos, flujos de trabajo, etc. |
| 2 | [Apache Sling](https://sling.apache.org/apidocs/sling11/) | REST y abstracciones basadas en recursos, como recursos, mapas de valores y solicitudes HTTP. |
| 3 | [Apache Jackrabbit Oak](http://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | Abstracciones de datos y contenido, como nodos, propiedades y sesiones. |
| 4 | [Apache Felix](https://felix.apache.org/) | abstracciones de contenedores de aplicaciones OSGi como servicios y componentes (OSGi). |

Si AEM proporciona una API, preferirla a Sling, JCR y OSGi. Si AEM no proporciona una API, entonces prefiera Sling antes que JCR y OSGi.

>[!TIP]
>
>Para obtener más información sobre estas directrices, consulte el documento [Comprender las prácticas recomendadas de la API de Java.](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)

## API y servicios de envío y administración de contenido de AEM {#delivery-apis}

AEM ofrece componentes personalizables y opciones de envío de contenido.

| Función | Descripción |
|---|---|
| [Los componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) | Componentes estandarizados de administración de contenido web (WCM) para AEM acelerar el tiempo de desarrollo y reducir el costo de mantenimiento de los sitios web |
| [Exportador JSON](/help/implementing/developing/components/json-exporter.md) | Enviar el contenido de cualquier página AEM en formato de modelo de datos JSON |
| [Activación de la exportación de JSON para un componente](/help/implementing/developing/components/enabling-json-exporter.md) | Generar exportación JSON de contenido de componente basado en un marco de modelos |
| [API de recursos](/help/assets/mac-api-assets.md) | Permite operaciones create-read-update-delete (CRUD) en recursos, incluidos binarios, metadatos, representaciones y comentarios. Consulte API HTTP de AEM Assets |
| [API HTTP de fragmentos de contenido](/help/assets/content-fragments/assets-api-content-fragments.md) | Acceda al contenido del fragmento de contenido directamente a través de la API HTTP mediante operaciones CRUD |
| [API de GraphQL de fragmento de contenido](/help/assets/content-fragments/graphql-api-content-fragments.md) | Habilitar la entrega eficiente de fragmentos de contenido a clientes JavaScript en implementaciones CMS sin encabezado |
| [Fragmentos de contenido API HTTP de recursos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html) | Formato exacto de las solicitudes de recursos HTTP admitidas |

## API específicas de SPA {#spa-apis}

AEM marco de trabajo del SDK del Editor de aplicaciones de una sola página (SPA) proporciona referencias específicas de la API de JavaScript.

| API | Descripción |
|---|---|
| [Asignación de componentes](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping) | Proporciona una forma para que la aplicación de una sola página asigne componentes front-end a tipos de recursos de Adobe Experience Manager (AEM componentes) |
| [Administrador de modelos de página](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager) | Un intérprete entre el Editor de Adobe Experience Manager y el Editor de aplicaciones de una sola página (SPA) de Adobe Experience Manager |
| [React Componentes editables](https://www.npmjs.com/package/@adobe/aem-react-editable-components) | Proporciona los componentes React y la capa de integración para empezar a usar el Editor de sitios de Adobe Experience Manager |
| [Componentes editables de angular](https://www.npmjs.com/package/@adobe/aem-angular-editable-components) | Proporciona los componentes de Angular y la capa de integración para ayudarle a empezar con el Editor de sitios de Adobe Experience Manager |

>[!TIP]
>
>Consulte la [SPA Introducción y Tutorial](/help/implementing/developing/hybrid/introduction.md) para obtener más información sobre las aplicaciones de una sola página.
