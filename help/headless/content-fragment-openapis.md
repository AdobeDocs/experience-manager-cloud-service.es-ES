---
title: Fragmentos de contenido y modelos de fragmentos de contenido OpenAPI
description: Obtenga información acerca de los fragmentos de contenido y los modelos de fragmentos de contenido OpenAPI.
exl-id: 077eed73-a066-4273-b2f5-da4bf5cd900c
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 1a55c35814d6651173f7bdeaa677a7dbdec13f73
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Administración de fragmentos de contenido y modelos de fragmentos de contenido OpenAPI {#content-fragments-and-content-fragment-models-management-openapis}

AEM AEM La implementación modernizada de OpenAPI de la API de administración de fragmentos de contenido permite a los desarrolladores realizar mediante programación operaciones de Crear, Leer, Actualizar y Eliminar en el Autor de la publicación para administrar modelos de fragmentos de contenido y fragmentos de contenido almacenados en la biblioteca de segmentos de contenido de la aplicación de la API de. Estas API admiten una serie de casos de uso.

El uso existente de [Assets HTTP API](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/admin/mac-api-assets) para fragmentos de contenido debe migrarse a la nueva OpenAPI de administración de fragmentos de contenido. Para obtener documentación completa, consulte [API de administración de fragmentos de contenido](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/).

>[!NOTE]
>
>AEM Se requiere autorización para acceder a OpenAPI cuando no ha iniciado sesión en el sitio web; por ejemplo, cuando se utiliza OpenAPI desde otro producto como parte de una integración de, o cuando no ha iniciado sesión en el sitio web.
>
>Consulte [API basadas en OpenAPI](/help/implementing/developing/open-api-based-apis.md) para obtener más información sobre cómo autorizar su acceso a OpenAPI.

>[!NOTE]
>
>AEM Consulte [API de para la administración y entrega de contenido estructurado](/help/headless/apis-headless-and-content-fragments.md) para obtener una descripción general de las diversas API disponibles y una comparación de algunos de los conceptos involucrados.