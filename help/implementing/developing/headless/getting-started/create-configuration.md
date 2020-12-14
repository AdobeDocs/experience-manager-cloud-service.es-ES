---
title: Creación de una guía de Inicio rápido sin encabezado de configuración
description: Como primer paso para empezar con AEM sin cabeza como Cloud Service, debe crear una configuración.
translation-type: tm+mt
source-git-commit: 259d54a225f8dee5929f62b784e28f3fc2bb794a
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 2%

---


# Creación de una guía de Inicio rápido sin encabezado de configuración {#creating-configuration}

Como primer paso para empezar con AEM sin cabeza como Cloud Service, debe crear una configuración.

## ¿Qué es una configuración? {#what-is-a-configuration}

El navegador de configuración proporciona una API de configuración genérica, estructura de contenido y mecanismo de resolución para las configuraciones en AEM.

En el contexto de un gestor de contenido sin cabeza en AEM, piense en una configuración como un lugar de trabajo dentro AEM donde puede crear los modelos de contenido, que definen la estructura del contenido futuro y los fragmentos de contenido. Puede tener varias configuraciones para separar estos modelos.

Si está familiarizado con [plantillas de página en una implementación de AEM de pila completa,](/help/sites-cloud/authoring/features/templates.md) el uso de configuraciones para la administración de modelos de contenido es similar.

## Cómo crear una configuración {#how-to-create-a-configuration}

Un administrador solo tendría que crear una configuración una vez, o muy raramente cuando se necesita un nuevo espacio de trabajo para organizar los modelos de contenido. A efectos de esta guía de introducción, solo necesitamos crear una configuración.

1. Inicie sesión en AEM como Cloud Service y, en el menú principal, seleccione **Herramientas -> General -> Navegador de configuración**.
1. Proporcione un **Título** y un **Nombre** para la configuración.
   * El **Título** debe ser descriptivo.
   * El **Nombre** se convertirá en el nombre del nodo en el repositorio.
      * Se generará automáticamente en función del título y se ajustará en función de [convenciones de nombres de AEM.](/help/implementing/developing/introduction/naming-conventions.md)
      * Puede ajustarse si es necesario.
1. Marque las siguientes opciones:
   * **Modelos de fragmento de contenido**
   * **Consultas persistentes de GraphQL**

   ![Crear configuración](../assets/create-configuration.png)

1. Haga clic o pulse **Crear**

Si es necesario, puede crear varias configuraciones. Las configuraciones también se pueden anidar.

>[!NOTE]
>
>Las opciones de configuración, además de **Modelos de fragmento de contenido** y **Consultas persistentes de GraphQL**, pueden ser necesarias según los requisitos de implementación.

## Próximos pasos {#next-steps}

Con esta configuración, ahora puede pasar a la segunda parte de la guía de introducción y [crear modelos de fragmentos de contenido.](create-content-model.md)

>[!TIP]
>
>Para obtener más información sobre el Explorador de configuración, [consulte la documentación del Explorador de configuración.](/help/implementing/developing/introduction/configurations.md)
