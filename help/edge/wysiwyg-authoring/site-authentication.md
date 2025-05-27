---
title: Configuración de la autenticación de sitios para la creación de contenido
description: Descubra cómo AEM Live admite la autenticación basada en tókenes y cómo configurar AEM para utilizar la autenticación con la creación WYSIWYG.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: b2838da2-79c7-49b1-a101-15c21e80197e
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: ht
source-wordcount: '324'
ht-degree: 100%

---

# Configuración de la autenticación de sitios para la creación de contenido {#site-authentication}

Descubra cómo AEM Live admite la autenticación basada en tókenes y cómo configurar AEM para utilizar la autenticación con la creación WYSIWYG.

## Información general {#overview}

AEM Live admite la autenticación basada en tókenes. La autenticación de sitios suele aplicarse tanto a los sitios de vista previa como a los de publicación, pero también se puede configurar para proteger únicamente cualquiera de los dos sitios de forma individual.

>[!NOTE]
>
>Si decide activar la autenticación de sitios, también debe configurarla en los entornos de creación de AEM

## Requisitos  {#requirements}

Para configurar la autenticación de sitios para su uso con la creación de contenido, primero debe completar las siguientes tareas:

* Este documento da por sentado que ya ha creado un sitio para su proyecto basado en la [Guía de introducción para desarrolladores para la creación WYSIWYG con Edge Delivery Services.](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)
* Tiene que haber [habilitado la función sin repositorio para su proyecto.](/help/edge/wysiwyg-authoring/repoless.md)

## Configuración de la autenticación del sitio {#configure-authentication}

Consulte el documento [Configuración de la autenticación del sitio](https://www.aem.live/docs/authentication-setup-site) para obtener detalles sobre cómo configurar la autenticación del sitio.

Tome nota de la siguiente información cuando configure la autenticación:

* ID de la cuenta técnica
* Token de autenticación del sitio

Estos elementos son necesarios para completar la configuración de la autenticación del sitio para el entorno de creación de AEM.

## Configuración del entorno de creación {#authoring-environment}

Una vez configurada la autenticación del sitio, puede activarla en el entorno de creación de AEM.

1. Inicie sesión en la instancia de autor de AEM y vaya a **Herramientas** -> **Cloud Services** -> **Configuración de Edge Delivery Services**, seleccione la configuración que se creó automáticamente para su sitio y pulse o haga clic en **Propiedades** en la barra de herramientas.
1. En la ventana **Configuración de Edge Delivery Services**, seleccione la pestaña **Autenticación** y proporcione el **token de autenticación del sitio** que copió anteriormente.

   ![Configuración de Edge Delivery Services](/help/edge/wysiwyg-authoring/assets/site-authentication/configure-aem-author.png)

1. Compruebe que el **ID de cuenta técnica** coincida con el que copió anteriormente.

   * Este campo está predefinido como de solo lectura.
   * La cuenta técnica es la misma para todos los sitios en un solo entorno de creación de AEM.

1. Haga clic o pulse en **Guardar y cerrar**.
