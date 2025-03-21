---
title: Habilitar la extensibilidad de la IU en  [!DNL AEM Assets View]
description: Obtenga información acerca de la capacidad de extensibilidad de la interfaz de usuario de  [!DNL AEM Assets View]. [!DNL AEM Assets View] UI permite agregar componentes de interfaz de usuario personalizados para satisfacer necesidades empresariales específicas.
feature: App Builder
role: User, Developer
exl-id: a11f7043-17cf-4331-b76c-d3db099c2411
source-git-commit: e32cd7b7822a983840377f7e69ac3ed0ceb86e16
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 3%

---

# Habilitar la extensibilidad de la IU en [!DNL AEM Assets View] {#AEM-Assets-View-UI-Extensibility}

| [Prácticas recomendadas de búsqueda](/help/assets/search-best-practices.md) | [Prácticas recomendadas de metadatos](/help/assets/metadata-best-practices.md) | [Centro de contenido](/help/assets/product-overview.md) | [Dynamic Media con funciones de OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentación de desarrollador de AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

[!DNL AEM Assets View] admite la extensibilidad de la interfaz de usuario, lo que le permite agregar componentes de la interfaz de usuario personalizados a la interfaz de usuario de [!DNL Assets View] para flujos de trabajo específicos y requisitos empresariales que no cumplen las capacidades predeterminadas de [!DNL AEM Assets View]. Esta capacidad de extensibilidad de la interfaz de usuario de [!DNL AEM Assets View] mejora su flexibilidad, lo que permite a las organizaciones adaptar la interfaz para flujos de trabajo y requisitos específicos.

Habilite la extensibilidad de la interfaz de usuario en [!DNL AEM Assets View] para agregar componentes personalizados a la interfaz de usuario de [!DNL Assets View] a fin de satisfacer requisitos empresariales específicos que no cumplen las capacidades predeterminadas de [!DNL AEM Assets View].\
Puede agregar sus extensiones a los niveles **Asset**, **Folder** y **Collection**. La extensión agregada se muestra en un panel dedicado en la página **Recurso**, **Colección** o **Carpeta** **[!UICONTROL Detalles]**.

>[!IMPORTANT]
>
> * La extensibilidad de la interfaz de usuario [!DNL AEM Assets View] está disponible con [[!DNL Assets Ultimate]](/help/assets/assets-ultimate-overview.md).
> * Para obtener acceso a la extensibilidad de la interfaz de usuario de [!DNL Assets view], [cree y envíe un  [!DNL Adobe] caso de asistencia al cliente](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html).
> * Para proporcionar comentarios sobre la documentación, expanda **[!UICONTROL Opciones de comentarios detallados]** y haga clic en **[!UICONTROL Informar de un problema]**.

## <a id="1"></a> acceder a la vista de Assets{#add-UI-Extensibility-in-AEM-Assets-View}

Siga los pasos mencionados en la siguiente imagen para acceder a [!DNL Assets View]:
![iu de vista de recursos de acceso](/help/assets/assets/access-assets-view.jpg)

## Ver extensiones de IU en [!DNL Assets View] {#ui-extensibility-panel-assets-view}

En [!DNL Assets View], vaya a la página **[!UICONTROL Detalles]** de un recurso, una carpeta o una colección. La página **[!UICONTROL Detalles]** muestra la extensión de la interfaz de usuario agregada en un panel dedicado.
![mi espacio de trabajo](/help/assets/assets/my-workspace-assets-view3.png)

## Requisitos previos para añadir el componente de extensibilidad{#assets-view-ui-extensibility}

Complete los siguientes requisitos para empezar a agregar el componente de extensibilidad en su [!DNL Assets View UI]:

* [Acceso a [!DNL Assets View]](#1).
* Acceso a [[!DNL Adobe app builder]](https://developer.adobe.com/app-builder/docs/overview/).
* Derecho al desarrollador de la función de administrador del sistema dentro de la organización. Consulte [esta documentación](https://developer.adobe.com/uix/docs/guides/get-access/) para obtener más información.
* [!DNL Adobe IO command line tool (AIO CLI)] está instalado en sus equipos locales. Esta herramienta es esencial para crear e implementar proyectos de extensión. Consulte [esta documentación](https://developer.adobe.com/app-builder/docs/getting_started/#local-environment-set-up) para obtener más información.
* Buen conocimiento de las tecnologías [!DNL JavaScript], [!DNL Node.js] y [!DNL React].

## Agregar el componente de extensibilidad de IU a [!DNL Assets View] {#ui-extensibility-in-assets-view}

1. Consulte [Introducción](https://developer.adobe.com/uix/docs/getting-started/) para obtener información esencial sobre las extensiones de IU y el marco de [!DNL Adobe App Builder]. Descubra cómo la extensibilidad de la interfaz de usuario permite la integración de la lógica personalizada y la interfaz de usuario en [!DNL Adobe Experience Cloud services] y comprenda la arquitectura y el flujo de trabajo para implementar las extensiones de interfaz de usuario.
1. Consulte [Guías](https://developer.adobe.com/uix/docs/guides/) para obtener información general sobre la extensibilidad de la interfaz de usuario, incluida la configuración del entorno local, la vista previa local, la publicación y la administración.
1. Consulte [Conceptos comunes al crear extensiones](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/commons/) para comprender los aspectos básicos necesarios para desarrollar una extensión de interfaz de usuario para [!DNL AEM Assets View].
1. Agregar paneles laterales personalizados a la interfaz [!DNL Assets View]. La aplicación host ([!DNL Assets View]) administra estos paneles para administrar las interacciones de la interfaz de usuario, como el alternado y la vinculación profunda. Las extensiones utilizan el punto de extensión `aem/assets/details/1` para integrar paneles personalizados que especifican propiedades, como el ID del panel, el título y la dirección URL de contenido. Los desarrolladores registran paneles personalizados con el método `getPanels()` y crean rutas para mostrar contenido personalizado. Para obtener una implementación detallada, que incluya referencias de API y ejemplos de código, consulte [Vista de detalles](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/details-view/).
1. Configure su entorno local y cree su primera extensión de interfaz de usuario para disfrutar de primera mano del proceso de desarrollo de extensiones de interfaz de usuario en [!DNL Assets View]. Consulte [AEM Assets paso a paso Ver desarrollo de extensiones](https://developer.adobe.com/uix/docs/services/aem-assets-view/extension-development/) para obtener más información.
1. Configure la aplicación utilizando la CLI de AIO para generar la estructura básica de extensión y el código requerido. Consulte [generación de código para [!DNL AEM Assets View]](https://developer.adobe.com/uix/docs/services/aem-assets-view/code-generation/) para obtener información detallada.
1. Pruebe las extensiones localmente para asegurarse de que funcionan según lo esperado antes de la implementación. Ejecute la extensión en un entorno totalmente aislado o con aislamiento parcial y conecte la extensión a la instancia de producción [!DNL AEM Assets View] para realizar pruebas. Consulte [Solución de problemas - [!DNL AEM Assets View] extensibilidad](https://developer.adobe.com/uix/docs/services/aem-assets-view/debug/) para obtener información detallada.
