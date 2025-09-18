---
title: Fragmentos de contenido y OpenAPI de fragmentos de contenido y modelos
description: Obtenga información acerca de los fragmentos de contenido y los modelos de fragmentos de contenido OpenAPI.
exl-id: 077eed73-a066-4273-b2f5-da4bf5cd900c
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 1fb1201fa976e4c0e3c87f22bd9327a55828efef
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 4%

---

# Administración de fragmentos de contenido y modelos de fragmentos de contenido OpenAPI {#content-fragments-and-content-fragment-models-management-openapis}

La implementación modernizada de OpenAPI de la API de administración de fragmentos de contenido permite a los desarrolladores realizar mediante programación operaciones de Crear, Leer, Actualizar y Eliminar en AEM Author para administrar modelos de fragmentos de contenido y fragmentos de contenido almacenados en AEM. Estas API admiten una serie de casos de uso.

Para obtener documentación completa, consulte [API de administración de fragmentos de contenido](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/).

>[!NOTE]
>
>El uso existente de [Assets HTTP API](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/admin/mac-api-assets) para fragmentos de contenido debe migrarse a la nueva OpenAPI de administración de fragmentos de contenido.

>[!NOTE]
>
>Se requiere autorización para acceder a OpenAPI cuando no ha iniciado sesión en AEM; por ejemplo, cuando se utiliza OpenAPI desde otro producto como parte de una integración.
>
>Consulte [API basadas en OpenAPI](/help/implementing/developing/open-api-based-apis.md) para obtener más información sobre cómo autorizar su acceso a OpenAPI.

>[!CAUTION]
>
>De forma predeterminada, la API de Apertura de administración de fragmentos de contenido está desactivada en la publicación. En lugar de esto, para casos de uso orientados a la entrega, recomendamos usar la [API abierta de entrega de fragmentos de contenido](/help/headless/aem-content-fragment-delivery-with-openapi.md).

>[!NOTE]
>
>Consulte [API de AEM para la administración y entrega de contenido estructurado](/help/headless/apis-headless-and-content-fragments.md) para obtener una descripción general de las diversas API disponibles y una comparación de algunos de los conceptos involucrados.