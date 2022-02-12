---
title: Uso del IDE de GraphiQL en AEM
description: Aprenda a utilizar GraphiQL IDE en Adobe Experience Manager.
feature: Content Fragments,GraphQL API
source-git-commit: c4490690edb1ec0e2a6b8cca724fe9c290650bc8
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 3%

---


# Uso del IDE de GraphiQL {#graphiql-ide}

Implementación de la norma [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) IDE está disponible para usar con AEM GraphQL. Esto puede ser [instalado con AEM](#installing-graphiql-ide).

>[!NOTE]
>
>GraphiQL está enlazado al extremo global (y no funciona con otros extremos para configuraciones de sitios específicas).

La herramienta GraphiQL permite introducir, probar y depurar consultas directamente. GraphiQL también proporciona fácil acceso a la documentación, lo que facilita la comprensión de los métodos disponibles.

Por ejemplo:

* `http://localhost:4502/content/graphiql.html`

Esto proporciona funciones como resaltado de sintaxis, autocompletado, autosugerencia, junto con un historial y documentación en línea:

![Interfaz de GraphiQL](assets/cfm-graphiql-interface.png "Interfaz de GraphiQL")

## Instalación del AEM GraphiQL IDE {#installing-graphiql-ide}

El IDE de GraphiQL es una herramienta de desarrollo que solo se necesita en entornos de nivel inferior como un desarrollo o una instancia local. Por lo tanto, no se incluye en el proyecto AEM, sino que se presenta como un paquete independiente que se puede instalar según sea necesario.

1. Vaya a la **[Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-ES/aemcloud.html)** > **AEM as a Cloud Service**.
1. Busque &quot;GraphiQL&quot; (asegúrese de incluir la variable **i** en **GraphiQL**.
1. Descargue la última **Paquete de contenido de GraphiQL v.x.x.x**
1. En el **Inicio de AEM** vaya a **Herramientas** > **Implementación** > **Paquetes**.
1. Haga clic en **Cargar paquete** y elija el paquete descargado en el paso anterior. Haga clic en **Instalar** para instalar el paquete.

