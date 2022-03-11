---
title: Información general sobre componentes
description: Los componentes son unidades modulares que implementan una funcionalidad específica para presentar el contenido en su sitio web
exl-id: 0fdc99e7-2103-448d-8217-d5d52c94acea
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 6%

---

# Información general sobre componentes {#components-overview}

Esta página proporciona información general sobre los componentes de Adobe Experience Manager (AEM), como los [se utiliza para la creación de páginas](/help/sites-cloud/authoring/fundamentals/components.md).

## ¿Qué son los componentes? {#what-are-components}

Los componentes de AEM son:

* Unidades modulares que implementan funcionalidades específicas para presentar el contenido en su sitio web.
* Reutilizable.
* Se desarrolla como unidades independientes dentro de una carpeta del repositorio.
* No tienen archivos de configuración ocultos.
* Puede contener otros componentes.
* Puede ejecutarse en cualquier lugar dentro de cualquier sistema AEM y también puede limitarse a ejecutarse bajo componentes específicos.
* Disponen de una interfaz de usuario estandarizada.
* Tenga un comportamiento de edición que se pueda configurar.
* Utilice cuadros de diálogo creados con subelementos basados en componentes de la interfaz de usuario de Granite.
* Se desarrollan utilizando [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=es).
* Se puede desarrollar para crear componentes personalizados que amplíen la funcionalidad predeterminada.

Como los componentes son modulares, puede:

* Desarrolle un nuevo componente en la instancia local.
* Implíquela en el entorno de prueba.
* Implíquela en su entorno de creación activo, donde permiten a los autores o administradores añadir y configurar contenido.
* Implemente en los entornos de publicación activos, donde se utilizan para representar contenido para los visitantes del sitio web.

Cada componente AEM:

* Es un tipo de recurso.
* Es una colección de scripts que realizan completamente una función específica.
* Puede funcionar de forma aislada, es decir, dentro de AEM o de un portal.

## AEM Core Components {#aem-core-components}

[Los componentes principales AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) son un conjunto de componentes estandarizados de Administración de contenido web (WCM, Web Content Management ) para AEM a fin de acelerar el tiempo de desarrollo y reducir el coste de mantenimiento de los sitios web.

Los componentes principales se proporcionan con AEM as a Cloud Service y la variable [Tutorial de WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) ilustra cómo implementar y utilizar componentes. Los componentes se proporcionan con todo el código fuente y se pueden utilizar tal cual o como puntos de partida para los componentes modificados o ampliados.

### Visualización de componentes disponibles {#viewing-available-components}

Para obtener una descripción general de todos los componentes disponibles en la instancia de AEM, utilice la variable [Consola Componentes](/help/sites-cloud/authoring/features/components-console.md).

Como alternativa, también puede utilizar CRXDE Lite para obtener una lista de todos los componentes disponibles en el repositorio.

1. En **[!UICONTROL CRXDE Lite]**, seleccione **[!UICONTROL Herramientas]** en la barra de herramientas y, a continuación, **[!UICONTROL Consulta]**, que abre el **[!UICONTROL Consulta]** pestaña .

1. En el **[!UICONTROL Consulta]** , seleccione `XPath` como **[!UICONTROL Tipo]**.

1. En el campo de entrada **[!UICONTROL Consulta]**, escriba la cadena siguiente:

   `//element(*, cq:Component)`

1. Haga clic en **[!UICONTROL Ejecutar]** y se muestran los componentes.
