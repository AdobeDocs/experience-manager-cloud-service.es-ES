---
title: Recuperación de información de acceso al repositorio de Git
description: Descubra cómo el desarrollador front-end utiliza Cloud Manager para acceder a la información del repositorio de Git.
exl-id: 3ef1cf86-6da4-4c09-9cfc-acafc8f6dd5c
solution: Experience Manager Sites
feature: Developing
role: Admin, Developer
recommendations: noDisplay, noCatalog
source-git-commit: 8c4b34a77ef85869048fae254728c58cf0d99b66
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 100%

---


# Recuperación de información de acceso al repositorio de Git {#retrieve-access}

{{traditional-aem}}

Descubra cómo el desarrollador front-end utiliza Cloud Manager para acceder a la información del repositorio de Git.

## Lo que hemos visto hasta ahora {#story-so-far}

Si usted es desarrollador front-end y responsable solo de la personalización del tema del sitio, no necesita saber cómo se configuró AEM y puede ir a la sección [Objetivo](#objective) de este documento.

Si también desempeña la función de administrador de Cloud Manager o AEM, además de desarrollador de front-end, en el documento anterior del recorrido de creación rápida de sitios de AEM, [Conceder acceso al desarrollador de front-end](grant-access.md), ha aprendido cómo incorporar al desarrollador de front-end para que tenga acceso al repositorio de Git. Y ahora debería ser capaz de:

* Cómo añadir un desarrollador front-end como usuario.
* Cómo conceder las funciones necesarias al desarrollador front-end.

Este artículo da el siguiente paso y muestra cómo el desarrollador front-end utiliza el acceso de Cloud Manager para recuperar credenciales de acceso al repositorio de Git de AEM.

Ahora que hay un sitio creado basado en una plantilla y una canalización configurada, y el desarrollador front-end está incorporado y tiene toda la información que necesita, este artículo se aleja de la perspectiva de los administradores y se centra en la función de desarrollador front-end.

## Objetivo {#objective}

En este documento se explica cómo usted, como desarrollador front-end, puede acceder a Cloud Manager y recuperar las credenciales de acceso al repositorio de Git de AEM. Después de leer esto, debería haber logrado lo siguiente:

* Comprender a alto nivel qué es Cloud Manager.
* Haber recuperado sus credenciales para acceder al Git de AEM y confirmar sus personalizaciones.

## Función responsable {#responsible-role}

Esta parte del recorrido se aplica al desarrollador front-end.

## Requisitos  {#requirements}

La herramienta de Creación rápida de sitios permite a los desarrolladores front-end trabajar de forma independiente sin tener conocimientos de AEM o de cómo se configura. Sin embargo, el administrador de Cloud Manager debe incluir al desarrollador front-end en el equipo del proyecto y el administrador de AEM debe proporcionarle la información necesaria. Asegúrese de tener la siguiente información antes de continuar.

* Desde el administrador de AEM:
   * Archivos de origen del tema para personalizar
   * Ruta a una página de ejemplo para usar como base de referencia
   * Credenciales del usuario proxy para probar las personalizaciones respecto al contenido de AEM en directo
   * Requisitos del diseño front-end
* Desde el administrador de Cloud Manager:
   * Un correo electrónico de bienvenida de Cloud Manager que le informa de su acceso
   * El nombre del programa o la URL a él dentro de Cloud Manager

Si le falta alguno de estos elementos, póngase en contacto con el administrador de AEM o de Cloud Manager.

Se da por hecho que el desarrollador front-end tiene una amplia experiencia con flujos de trabajo de desarrollo front-end, así como herramientas comunes instaladas que incluyen:

* git
* npm
* webpack
* Un editor de su preferencia

## Conocimiento de Cloud Manager {#understanding-cloud-manager}

Cloud Manager permite que las organizaciones autogestionen AEM en la nube. Incluye un marco de trabajo de integración y entrega continuas (CI/CD) que permite a los equipo de TI y a los asociados de la implementación acelerar la entrega de las personalizaciones o actualizaciones sin poner en riesgo el rendimiento o la seguridad.

Para el desarrollador front-end, es la puerta de enlace a lo siguiente:

* Acceder a la información del repositorio de Git de AEM para poder confirmar las personalizaciones del front-end.
* Iniciar la canalización de la implementación para implementar las personalizaciones.

El administrador de Cloud Manager lo habrá incorporado como usuario de Cloud Manager. Debería haber recibido un correo electrónico de bienvenida similar al siguiente.

![Correo electrónico de bienvenida](assets/welcome-email.png)

Si no ha recibido este correo electrónico, póngase en contacto con el administrador de Cloud Manager.

## Acceder a Cloud Manager {#access-cloud-manager}

1. Inicie sesión en Adobe Experience Cloud en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) o haga clic en el vínculo que aparece en el correo electrónico de bienvenida.

1. Cloud Manager enumera los distintos programas disponibles. Haga clic en el que necesite acceder según le indique el administrador de Cloud Manager. Si este es su primer proyecto front-end para AEMaaCS, es probable que solo haya un programa disponible.

   ![Selección de un programa en Cloud Manager](assets/cloud-manager-select-program.png)

Ahora verá una descripción general del programa. Su página tendrá un aspecto diferente, pero será similar al de este ejemplo.

![Información general de Cloud Manager](assets/cloud-manager-overview.png)

## Recuperación de información de acceso al repositorio  {#repo-access}

1. En la sección **Canalizaciones** de la página Cloud Manager, haga clic en el botón **Acceder a información de repositorio**.

   ![Canalizaciones](assets/pipelines-repo-info.png)

1. Se abre el cuadro de diálogo **Información del repositorio**.

   ![Información del repositorio](assets/repo-info.png)

1. Haga clic en el botón **Generar contraseña** para crear una contraseña para usted.

1. Guarde la contraseña generada en un administrador de contraseñas seguro. La contraseña no se volverá a mostrar nunca más.

1. Copie también los campos **Nombre de usuario** y la **Línea de comandos de Git**. Utilizará esta información más adelante para acceder al repositorio.

1. Seleccione **Cerrar**.

## Siguientes pasos {#what-is-next}

Ahora que ha completado esta parte del Recorrido de creación rápida de sitios de AEM, debe hacer lo siguiente:

* Comprender a alto nivel qué es Cloud Manager.
* Haber recuperado sus credenciales para acceder al Git de AEM y confirmar sus personalizaciones.

Partiendo de estos conocimientos, continúe con el recorrido de creación rápida de sitios de AEM revisando el documento [Personalización del tema del sitio](customize-theme.md), con el que aprenderá cómo se crea el tema del sitio, cómo personalizarlo y cómo probarlo con contenido de AEM en directo.

## Recursos adicionales {#additional-resources}

Aunque se recomienda pasar a la siguiente parte del recorrido de creación rápida de sitios de AEM revisando el documento [Personalización del tema del sitio](customize-theme.md), a continuación se presentan algunos recursos adicionales y opcionales que profundizan en algunos conceptos mencionados en este documento, pero que no son necesarios para continuar con el recorrido.

* [Documentación de Cloud Manager de Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=es): explore la documentación de Cloud Manager para obtener información detallada sobre sus funciones.
