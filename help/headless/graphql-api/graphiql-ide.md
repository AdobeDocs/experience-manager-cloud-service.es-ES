---
title: Uso del IDE de GraphiQL en AEM
description: Aprenda a utilizar el IDE de GraphiQL en Adobe Experience Manager.
feature: Content Fragments,GraphQL API
exl-id: be2ebd1b-e492-4d77-b6ef-ffdea9a9c775
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 100%

---

# Uso del IDE de GraphiQL {#graphiql-ide}

Una implementación del IDE estándar de [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) está disponible para usarse con GraphQL de AEM. Esto puede [instalarse con AEM](#installing-graphiql-ide).

>[!NOTE]
>
>GraphiQL está enlazado al punto de conexión global (y no funciona con otros puntos de conexión para configuraciones de sitios específicas).

La herramienta GraphiQL permite introducir, probar y depurar consultas directamente. GraphiQL también proporciona fácil acceso a la documentación, lo que facilita la comprensión de los métodos disponibles.

Por ejemplo:

* `http://localhost:4502/content/graphiql.html`

Esto proporciona funciones como resaltado de sintaxis, autocompletado o autosugerencia, junto con un historial y documentación en línea:

![Interfaz de GraphiQL](assets/cfm-graphiql-interface.png "Interfaz de GraphiQL")

## Instalación del IDE de GraphiQL de AEM {#installing-graphiql-ide}

El IDE de GraphiQL es una herramienta de desarrollo que solo se necesita en entornos de nivel inferior como una instancia de desarrollo o local. Por lo tanto, no se incluye en el proyecto de AEM, sino que se presenta como un paquete independiente que se puede instalar según sea necesario.

1. Vaya a **[Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-es/aemcloud.html)** > **AEM as a Cloud Service**.
1. Busque “GraphiQL” (asegúrese de incluir la **i** de **GraphiQL**.
1. Descargue el último **Paquete de contenido de GraphiQL v.x.x.x**
1. En el menú **Inicio de AEM** vaya a **Herramientas** > **Implementación** > **Paquetes**.
1. Haga clic en **Cargar paquete** y elija el paquete descargado en el paso anterior. Haga clic en **Instalar** para instalar el paquete.
