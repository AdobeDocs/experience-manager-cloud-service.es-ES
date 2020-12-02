---
title: Componentes Información general
description: Los componentes son unidades modulares que cuentan con una funcionalidad específica para presentar el contenido en el sitio web
translation-type: tm+mt
source-git-commit: 83c27daae4e8ae2ae6a8f115c9da9527971c6ecb
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 7%

---


# Información general de componentes {#components-overview}

Esta página proporciona información general sobre los componentes de Adobe Experience Manager (AEM), como los [utilizados para la creación de páginas](/help/sites-cloud/authoring/fundamentals/components.md).

## ¿Qué son los componentes? {#what-are-components}

Los componentes de AEM son:

* Unidades modulares que proporcionan una funcionalidad específica para presentar el contenido en el sitio web.
* Reutilizable.
* Desarrollado como unidades independientes dentro de una carpeta del repositorio.
* No tiene archivos de configuración ocultos.
* Puede contener otros componentes.
* Puede ejecutarse en cualquier lugar dentro de cualquier sistema AEM y también puede limitarse a ejecutarse bajo componentes específicos.
* Tener una interfaz de usuario estandarizada.
* Tener un comportamiento de edición que se pueda configurar.
* Utilice cuadros de diálogo creados con subelementos basados en componentes de la interfaz de usuario de Granite.
* Se desarrollan utilizando [HTL](https://docs.adobe.com/content/help/es-ES/experience-manager-htl/using/overview.html).
* Se puede desarrollar para crear componentes personalizados que extiendan la funcionalidad predeterminada.

Debido a que los componentes son modulares, puede:

* Desarrolle un nuevo componente en la instancia local.
* Implementarlo en el entorno de prueba.
* Implementarla en el entorno de creación en directo, donde permite a los autores y/o administradores agregar y configurar contenido.
* Implíquelo en los entornos de publicación activa, donde se utilizan para procesar contenido para visitantes en el sitio web.

Cada componente AEM:

* Es un tipo de recurso.
* Es una colección de secuencias de comandos que realizan completamente una función específica.
* Puede funcionar de forma aislada, es decir, en AEM o en un portal.

## AEM Core Components {#aem-core-components}

[Los componentes principales AEM ](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/introduction.html) son un conjunto de componentes de Gestor de contenido web (WCM) estandarizados para AEM a fin de acelerar el tiempo de desarrollo y reducir el coste de mantenimiento de los sitios web.

Los componentes principales se proporcionan con AEM como Cloud Service y el [tutorial de WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) ilustra cómo implementar y utilizar los componentes. Los componentes se proporcionan con todo el código fuente y pueden utilizarse tal cual o como puntos de partida para componentes modificados o ampliados.

### Visualización de componentes disponibles {#viewing-available-components}

Para obtener una visión general de todos los componentes disponibles en la instancia de AEM, utilice la [Consola de componentes](/help/sites-cloud/authoring/features/components-console.md).

También puede utilizar CRXDE Lite para obtener una lista de todos los componentes disponibles en el repositorio.

1. En **[!UICONTROL CRXDE Lite]**, seleccione **[!UICONTROL Herramientas]** en la barra de herramientas, luego **[!UICONTROL Consulta]**, que abre la ficha **[!UICONTROL Consulta]**.

1. En la ficha **[!UICONTROL Consulta]**, seleccione `XPath` como **[!UICONTROL Tipo]**.

1. En el campo de entrada **[!UICONTROL Consulta]**, escriba la cadena siguiente:

   `//element(*, cq:Component)`

1. Haga clic en **[!UICONTROL Ejecutar]** y se enumerarán los componentes.

