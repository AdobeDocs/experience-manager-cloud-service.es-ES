---
title: AEM Assets Ver extensibilidad de IU
description: Obtenga información acerca de la capacidad de extensibilidad de la IU de la vista AEM Assets. La IU de vista de AEM Assets permite agregar componentes de IU personalizados para satisfacer necesidades comerciales específicas.
feature: App Builder
role: User, Developer
exl-id: a11f7043-17cf-4331-b76c-d3db099c2411
source-git-commit: af7e6ab40212dfa3d91cda80a76b1b6b01dd65a3
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 3%

---

# AEM Assets Ver extensibilidad de IU{#AEM-Assets-View-UI-Extensibility}

| [Prácticas recomendadas de búsqueda](/help/assets/search-best-practices.md) | [Prácticas recomendadas de metadatos](/help/assets/metadata-best-practices.md) | [Centro de contenido](/help/assets/product-overview.md) | [Dynamic Media con funciones de OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentación de desarrollador de AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

La vista AEM Assets tiene la capacidad Extensibilidad de IU. Esta capacidad permite a los usuarios agregar componentes de interfaz de usuario personalizados a la interfaz de usuario de la vista Assets para satisfacer necesidades comerciales específicas que las funcionalidades integradas de la vista AEM Assets no satisfacen. Esta función de extensibilidad mejora la flexibilidad de la vista de AEM Assets, que permite a las organizaciones adaptar la interfaz a flujos de trabajo y requisitos específicos.
Puede añadir las extensiones a los niveles de recurso, carpeta y colección. La extensión añadida se muestra dentro de un panel dedicado en la página Detalles de recurso, colección o carpeta.

>[!IMPORTANT]
>
> * La extensibilidad de la IU de vista de AEM Assets está disponible con [Assets Ultimate](/help/assets/assets-ultimate-overview.md).
> * La extensibilidad de la IU de vista de Assets está disponible en su versión de Beta. Para obtener acceso anticipado a la extensibilidad de la interfaz de usuario de la vista de Assets, [cree y envíe un caso de asistencia al cliente de Adobe](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html).
> * Para proporcionar comentarios sobre la documentación, expanda las opciones de Comentarios detallados y haga clic en Informar de un problema.

## <a id="1"></a> Cómo acceder a la vista de Assets

Acceda a la vista de Assets de las siguientes maneras:
![access-assets-view-ui](/help/assets/assets/access-assets-view.jpg)

## ¿Dónde se muestran las extensiones de la interfaz de usuario en la interfaz de usuario de la vista Assets? {#ui-extensibility-panel-assets-view}

En la vista Assets, vaya a la página Detalles de un recurso, una carpeta o una colección. Esta página de detalles tiene un panel dedicado que muestra la extensión de la interfaz de usuario agregada.
![mi espacio de trabajo](/help/assets/assets/my-workspace-assets-view3.png)


## Requisitos previos para añadir el componente de extensibilidad

* [Acceso a la vista de Assets](#1).
* Acceso al [generador de aplicaciones de Adobe](https://developer.adobe.com/app-builder/docs/overview/), que está incluido en [Assets Ultimate](/help/assets/assets-ultimate-overview.md) de forma predeterminada.
* Con derecho a desarrollador de la función Administrador del sistema dentro de la organización. Consulte [this](https://developer.adobe.com/uix/docs/guides/get-access/) para obtener más información.
* La herramienta de línea de comandos de Adobe IO (AIO CLI) debe estar instalada en los equipos locales. Esta herramienta es esencial para crear e implementar proyectos de extensión. Consulte [this](https://developer.adobe.com/app-builder/docs/getting_started/#local-environment-set-up) para obtener más información.
* Buen conocimiento de las tecnologías JavaScript, Node.js y React.

## Adición del componente Extensibilidad de la IU en la IU de la vista Assets{#Adding-UI-Extensibility-Component-on-Assets-View}

1. Consulte [Introducción](https://developer.adobe.com/uix/docs/getting-started/) para obtener información esencial sobre las extensiones de la interfaz de usuario y el marco de App Builder de Adobe. Descubra cómo la extensibilidad de la interfaz de usuario permite la integración de la lógica y la interfaz de usuario personalizadas en los servicios de Adobe Experience Cloud y comprenda la arquitectura y el flujo de trabajo para implementar extensiones de interfaz de usuario.
1. Consulte [Guías](https://developer.adobe.com/uix/docs/guides/) para obtener información general sobre la extensibilidad de la interfaz de usuario, incluida la configuración del entorno local, la vista previa local, la publicación y la administración.
1. Consulte [Conceptos comunes al crear extensiones](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/commons/) para conocer los aspectos básicos necesarios para desarrollar una extensión de interfaz de usuario para la vista de AEM Assets.
1. Agregue paneles laterales personalizados a la interfaz de vista de Assets. La aplicación host (vista de Assets) administra estos paneles para gestionar las interacciones de la interfaz de usuario, como el alternado y la vinculación profunda. Las extensiones utilizan el punto de extensión `aem/assets/details/1` para integrar paneles personalizados que especifican propiedades, como el ID del panel, el título y la dirección URL de contenido. Los desarrolladores registran paneles personalizados con el método `getPanels()` y crean rutas para mostrar contenido personalizado. Para obtener una implementación detallada, que incluya referencias de API y ejemplos de código, consulte [Vista de detalles](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/details-view/).
1. Configure su entorno local y experimente el proceso de desarrollo de extensiones de IU en la vista de Assets creando su primera extensión de IU. Consulte [AEM Assets paso a paso Ver desarrollo de extensiones](https://developer.adobe.com/uix/docs/services/aem-assets-view/extension-development/) para obtener más información.
1. Configure la aplicación mediante la CLI de AIO para generar la estructura básica de extensión y el código requerido. Consulte [Generación de código para la vista de AEM Assets](https://developer.adobe.com/uix/docs/services/aem-assets-view/code-generation/) para obtener información detallada.
1. Pruebe las extensiones localmente para asegurarse de que funcionan según lo esperado antes de la implementación. Ejecute la extensión en un entorno completamente aislado o con aislamiento parcial y conecte la extensión a la vista AEM Assets de producción para realizar pruebas. Consulte [Solución de problemas - Extensibilidad de la vista de AEM Assets](https://developer.adobe.com/uix/docs/services/aem-assets-view/debug/) para obtener información detallada.
