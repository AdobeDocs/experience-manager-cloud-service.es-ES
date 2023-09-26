---
title: Información general sobre componentes
description: Los componentes son unidades modulares que implementan una funcionalidad específica para presentar el contenido en su sitio web
exl-id: 0fdc99e7-2103-448d-8217-d5d52c94acea
source-git-commit: 78ead5f15c2613d9c3bed3025b43423a66805c59
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 67%

---

# Información general sobre componentes {#components-overview}

Esta página proporciona información general sobre los componentes de Adobe Experience Manager (AEM), como los [usados para la creación de páginas](/help/sites-cloud/authoring/fundamentals/components.md).

## ¿Qué son los componentes? {#what-are-components}

* Unidades modulares que implementan funcionalidades específicas para presentar el contenido en su sitio web.
* Reutilizable.
* Se desarrolla como unidades independientes dentro de una carpeta del repositorio.
* No tienen archivos de configuración ocultos.
* Pueden contener otros componentes.
* AEM Pueden ejecutarse en cualquier lugar dentro de cualquier sistema de y también pueden limitarse a ejecutarse en componentes específicos.
* Disponen de una interfaz de usuario estandarizada.
* Tienen un comportamiento de edición que se puede configurar.
* Utilice cuadros de diálogo creados con subelementos basados en componentes de la interfaz de usuario de Granite.
* Se desarrollan utilizando [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=es).
* Se pueden desarrollar para crear componentes personalizados que amplíen la funcionalidad predeterminada.

Como los componentes son modulares, puede hacer lo siguiente:

* Desarrollar un nuevo componente en la instancia local.
* Implementarla en su entorno de prueba.
* Implementarla en su entorno de creación activo, donde permiten a los autores o administradores añadir y configurar contenido.
* Impleméntelo en los entornos de publicación activos, donde se utiliza para representar contenido para los visitantes del sitio web.

Cada componente AEM:

* Es un tipo de recurso.
* Es una colección de scripts que realizan completamente una función específica.
* Puede funcionar de forma aislada, es decir, dentro de AEM o de un portal.

## Los componentes principales de AEM {#aem-core-components}

[AEM Los componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) AEM son un conjunto de componentes estandarizados de gestión de contenido web (WCM) para la administración de contenido web con el fin de acelerar el tiempo de desarrollo y reducir el coste de mantenimiento de los sitios web.

Los componentes principales se proporcionan con AEM as a Cloud Service, y el [Tutorial de WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) ilustra cómo implementar y utilizar los componentes. Los componentes se proporcionan con todo el código fuente y se pueden utilizar tal cual o como puntos de partida para los componentes modificados o ampliados.

### Visualización de componentes disponibles {#viewing-available-components}

AEM Para obtener una descripción general de todos los componentes disponibles en la instancia de la, utilice el [Consola Componentes](/help/sites-cloud/authoring/features/components-console.md).

Como alternativa, también puede utilizar CRXDE Lite para obtener una lista de todos los componentes disponibles en el repositorio.

1. En **[!UICONTROL CRXDE Lite]**, seleccione **[!UICONTROL Herramientas]** en la barra de herramientas y, a continuación, **[!UICONTROL Consulta]**, que abre la pestaña **[!UICONTROL Consulta]**.

1. En la pestaña **[!UICONTROL Consulta]**, seleccione `XPath` como **[!UICONTROL Tipo]**.

1. En el **[!UICONTROL Consulta]** campo de entrada, introduzca la siguiente cadena:

   `//element(*, cq:Component)`

1. Cuando hace clic en **[!UICONTROL Ejecutar]**, se muestran los componentes.
