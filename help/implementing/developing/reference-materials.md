---
title: Materiales de referencia de la API
description: AEM Tiene API amplias y potentes que puede utilizar para su proyecto de experiencia digital.
exl-id: d4ef3040-5a0a-4149-9e99-09eda9605038
feature: Developing
role: Admin, Architect, Developer
source-git-commit: b3405279393be51b805c1129c171bb2249fd5726
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Materiales de referencia de la API {#api-reference-materials}

Adobe Experience Manager AEM AEM () proporciona muchas API para desarrollar aplicaciones y ampliar el alcance de los recursos AEM La tecnología de código abierto se basa en varias tecnologías de código abierto, que también se pueden utilizar.

## AEM API de núcleo {#core-aem-apis}

AEM Las siguientes API son fundamentales para la.

| API | Descripción |
|---|---|
| [Adobe Experience Manager as a Cloud Service](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) | Abstracciones de productos, como páginas, recursos, flujos de trabajo, etc. |
| [Granite UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html#) | Pila web abierta de Adobe que proporciona varios componentes esenciales (los materiales de Granite 6.5 se aplican a AEMaaCS) |
| [IU de Coral](https://opensource.adobe.com/coral-spectrum/documentation/) | Estilo visual del Adobe para las IU de la nube, diseñado para proporcionar coherencia en la experiencia del usuario |

<!---
|Editor core JavaScript API reference|Provides all the base objects and concepts to support authoring of content resources|
--->

>[!NOTE]
>
>Para obtener la información más reciente sobre las API de Experience Manager, visite también [API de Adobe Experience Manager as a Cloud Service](https://developer.adobe.com/experience-cloud/experience-manager-apis/).

## Marcos de trabajo adicionales {#additional-apis}

AEM Se basa en varias API de código abierto adicionales.

| API | Descripción |
|---|---|
| [Apache Sling](https://sling.apache.org/apidocs/sling11/) | Marco web que utiliza un repositorio de contenido Java (JCR) para almacenar y administrar contenido |
| [Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | Implementación de un repositorio de contenido Java (JCR) jerárquico, escalable y de alto rendimiento que se utilizará como base de los sitios web modernos de primera clase |
| [Repositorio de contenido Java](https://www.adobe.io/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) | Especificación de la versión 2.0 de JCR |
| [Apache Felix](https://felix.apache.org) | Implementación del marco y la plataforma de servicios de la iniciativa Open Services Gateway (OSGi) |

## Directrices de preferencias de API {#guidelines}

AEM Se basa en los cuatro conjuntos de API de Java principales siguientes en orden descendente de preferencia.

| Prioridad | API | Descripción |
|---|---|---|
| 1 | [Adobe Experience Manager as a Cloud Service](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) | Abstracciones de productos, como páginas, recursos, flujos de trabajo, etc. |
| 2 | [Apache Sling](https://sling.apache.org/apidocs/sling11/) | REST y abstracciones basadas en recursos como recursos, mapas de valores y solicitudes HTTP. |
| 3 | [Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | Resumen de datos y contenido, como nodos, propiedades y sesiones. |
| 4 | [Apache Felix](https://felix.apache.org/) | Abstracciones del contenedor de aplicaciones OSGi, como servicios y componentes (OSGi). |

AEM Si proporciona una API, la prefiere en lugar de Sling, JCR y OSGi. AEM Si no proporciona una API, prefiera Sling en lugar de JCR y OSGi.

>[!TIP]
>
>Para obtener más información sobre estas directrices, consulte el documento [Comprender las prácticas recomendadas de la API de Java.](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)

## AEM API y servicios de envío y administración de contenido {#delivery-apis}

AEM ofrece componentes personalizables y opciones de envío de contenido.

| Funcionalidad | Descripción |
|---|---|
| [Los componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) | AEM Componentes estandarizados de gestión de contenido web (WCM) para acelerar el tiempo de desarrollo y reducir el coste de mantenimiento de los sitios web. Se han diseñado para que los componentes de gestión de contenido web (WCM) sean más eficaces. |
| [Exportador JSON](/help/implementing/developing/components/json-exporter.md) | AEM Entregar el contenido de cualquier página de en formato de modelo de datos JSON. |
| [Activación de la exportación de JSON para un componente](/help/implementing/developing/components/enabling-json-exporter.md) | Generar una exportación JSON del contenido del componente en función de un marco de modelado |
| [API de Assets](/help/assets/mac-api-assets.md) | Permite operaciones de creación, lectura, actualización y eliminación (CRUD) en recursos, incluidos binarios, metadatos, representaciones y comentarios. Consulte API HTTP de AEM Assets |
| [API HTTP de fragmentos de contenido](/help/assets/content-fragments/assets-api-content-fragments.md) | Acceso al contenido de fragmentos de contenido directamente a través de la API HTTP mediante operaciones CRUD |
| [API de GraphQL de fragmentos de contenido](/help/headless/graphql-api/content-fragments.md) | Habilite la entrega eficiente de fragmentos de contenido a clientes JavaScript en implementaciones de CMS sin encabezado |
| [API HTTP de recursos de fragmentos de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html) | Formato exacto de las solicitudes de recursos HTTP admitidas |
| [API abiertas de modelos de fragmentos de contenido y fragmentos de contenido](/help/headless/content-fragment-openapis.md) | API abiertas de modelos de fragmentos de contenido y fragmentos de contenido |

## SPA API específicas de la {#spa-apis}

AEM SPA El marco de trabajo del SDK del Editor de aplicaciones de una sola página () proporciona referencias específicas a la API de JavaScript.

| API | Descripción |
|---|---|
| [Asignación de componentes](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping) | Proporciona una forma para que la aplicación de una sola página asigne componentes front-end a tipos de recursos de Adobe Experience Manager AEM (componentes de la página de inicio |
| [Administrador de modelos de página](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager) | Un intérprete entre el Editor de Adobe Experience Manager y el Editor de aplicaciones de una sola página de Adobe Experience Manager SPA (Editor de aplicaciones de una sola página |
| [Reaccionar componentes editables](https://www.npmjs.com/package/@adobe/aem-react-editable-components) | Proporciona los componentes de React y la capa de integración para ayudarle a empezar con el Editor del sitio de Adobe Experience Manager |
| [Angular Componentes editables](https://www.npmjs.com/package/@adobe/aem-angular-editable-components) | Proporciona los componentes de Angular y la capa de integración para ayudarle a empezar con el Editor del sitio de Adobe Experience Manager |

>[!TIP]
>
>Consulte la [SPA Introducción y tutorial de](/help/implementing/developing/hybrid/introduction.md) para obtener más información sobre las aplicaciones de una sola página.
