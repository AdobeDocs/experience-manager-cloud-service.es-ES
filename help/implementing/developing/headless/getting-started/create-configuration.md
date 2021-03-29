---
title: Guía de inicio rápido de Creación de una configuración sin encabezado
description: Cree una configuración como primer paso para comenzar con sin encabezado en AEM como Cloud Service.
translation-type: tm+mt
source-git-commit: e7ca6dc841ba777384be74021a27d523d530a956
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 2%

---


# Creación de una guía de inicio rápido de configuración sin encabezado {#creating-configuration}

Como primer paso para comenzar con sin encabezado en AEM como Cloud Service, debe crear una configuración.

## ¿Qué es una configuración? {#what-is-a-configuration}

El navegador de configuración proporciona una API de configuración genérica, estructura de contenido, mecanismo de resolución para las configuraciones en AEM.

En el contexto de la administración de contenido sin encabezado en AEM, piense en una configuración como lugar de trabajo dentro de AEM donde puede crear los modelos de contenido, que definen la estructura de su contenido futuro y los fragmentos de contenido. Puede tener varias configuraciones para separar estos modelos.

Si está familiarizado con las [plantillas de página en una implementación de AEM de pila completa,](/help/sites-cloud/authoring/features/templates.md) el uso de configuraciones para la administración de modelos de contenido es similar.

## Cómo crear una configuración {#how-to-create-a-configuration}

Un administrador solo tendría que crear una configuración una vez, o muy poco a poco cuando se necesita un nuevo espacio de trabajo para organizar los modelos de contenido. Para los fines de esta guía de introducción, solo necesitamos crear una configuración.

1. Inicie sesión en AEM como Cloud Service y, en el menú principal, seleccione **Tools -> General -> Configuration Browser**.
1. Proporcione un **Título** y un **Nombre** para la configuración.
   * El **Título** debe ser descriptivo.
   * El **Name** se convertirá en el nombre de nodo en el repositorio.
      * Se generará automáticamente en función del título y se ajustará según las [convenciones de nomenclatura de AEM.](/help/implementing/developing/introduction/naming-conventions.md)
      * Se puede ajustar si es necesario.
1. Compruebe las siguientes opciones:
   * **Modelos de fragmento de contenido**
   * **Consultas persistentes de GraphQL**

   ![Crear configuración](../assets/create-configuration.png)

1. Haga clic o pulse **Crear**

Si es necesario, puede crear varias configuraciones. Las configuraciones también se pueden anidar.

>[!NOTE]
>
>Las opciones de configuración además de **Content Fragment Models** y **GraphQL Persistent Queries** pueden ser necesarias en función de los requisitos de implementación.

## Pasos siguientes {#next-steps}

Con esta configuración, ahora puede pasar a la segunda parte de la guía de introducción y [crear modelos de fragmento de contenido.](create-content-model.md)

>[!TIP]
>
>Para obtener más información sobre el Explorador de configuración, [consulte la documentación del Explorador de configuración.](/help/implementing/developing/introduction/configurations.md)
