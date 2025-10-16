---
title: 'Crear una configuración: configuración sin encabezado'
description: Cree una configuración como primer paso para empezar a utilizar sin encabezado en AEM as a Cloud Service.
exl-id: 48801599-f279-4e55-8033-9c418d2af5bb
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 38a4bf89e099432163163e90e08aa0f47407724f
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 68%

---

# Crear una configuración: configuración sin encabezado {#create-configuration}

Como primer paso para empezar a utilizar sin encabezado en AEM as a Cloud Service, debe crear una configuración.

## ¿Qué es una configuración? {#what-is-a-configuration}

El explorador de configuración proporciona una API de configuración genérica, una estructura de contenido y un mecanismo de resolución para las configuraciones en AEM.

En el contexto de la administración de contenido sin encabezado en AEM, piense en una configuración como lugar de trabajo dentro de AEM donde puede crear los modelos de contenido, que definen la estructura de su contenido futuro y los fragmentos de contenido. Puede tener varias configuraciones para separar estos modelos.

Si está familiarizado con las [plantillas de página en una implementación de AEM de pila completa](/help/sites-cloud/authoring/page-editor/templates.md), el uso de configuraciones para la administración de modelos de contenido es similar.

## Cómo crear una configuración {#how-to-create-a-configuration}

Un administrador solo tendría que crear una configuración una vez, o poco a poco cuando se necesite un nuevo espacio de trabajo para organizar los modelos de contenido. Para los fines de esta guía de introducción, solo necesitamos crear una configuración.

Para obtener detalles paso a paso, consulte [Habilitar la funcionalidad de fragmento de contenido en el explorador de configuración](/help/sites-cloud/administering/content-fragments/setup.md#enable-content-fragment-functionality-configuration-browser).

>[!NOTE]
>
>Pueden ser necesarias las opciones de configuración además de los **Modelos de fragmentos de contenido** y **Consultas persistentes de GraphQL** en función de los requisitos de implementación.

## Próximos pasos {#next-steps}

Con esta configuración, ahora puede pasar a la segunda parte de la guía de introducción y [crear modelos de fragmentos de contenido](create-content-model.md).

>[!TIP]
>
>Para obtener información detallada acerca del Explorador de configuración, consulte la [documentación del Explorador de configuración](/help/implementing/developing/introduction/configurations.md).
