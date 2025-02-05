---
title: Tareas del desarrollador y del administrador de implementación
description: Una vez que el administrador del sistema haya configurado los recursos de la nube necesarios, aprenda cómo los desarrolladores y los administradores de implementación pueden acceder a Git para desarrollar aplicaciones y utilizar canalizaciones para implementarlas.
feature: Onboarding
role: Admin, User, Developer
exl-id: f57a856b-0932-4e8f-be59-a19fe692e2ab
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1397'
ht-degree: 94%

---


# Tareas del desarrollador y del administrador de implementación {#developer-deployment-manager}

En esta parte opcional del [recorrido de incorporación](overview.md), aprenderá cómo los desarrolladores y los administradores de implementación pueden acceder a Git para desarrollar aplicaciones y utilizar canalizaciones para implementarlas.

## La historia hasta ahora {#story-so-far}

¡Ha recorrido un largo camino en su recorrido de incorporación! ¡Enhorabuena! El administrador del sistema ha completado el recorrido AEM de incorporación al configurar los recursos de nube necesarios y conceder acceso en el documento [Asignar perfiles de producto](assign-profiles-aem.md).

En este punto, los desarrolladores y los administradores de implementación pueden empezar a crear sus propias aplicaciones, mientras que los usuarios de AEM pueden empezar a crear contenido. En este sentido, la incorporación es completa y es el momento de usar su nuevo sistema AEM as a Cloud Service, que ilustrará este documento.

## Audiencia {#audience}

Por lo tanto, el presente documento se redacta desde la perspectiva del **desarrollador** y el **administrador de implementación**.

El administrador del sistema también puede realizar estas mismas tareas, pero generalmente estos roles los tienen distintos usuarios.

## Objetivo {#objective}

Este documento es un complemento del proceso de incorporación para mostrar las tareas básicas de un desarrollador y un administrador de implementación una vez que el administrador del sistema ha incorporado todos los usuarios y ha creado los recursos de nube necesarios.

Después de leer este documento, debería poder hacer lo siguiente:

* Como desarrollador, saber acceder y administrar sus repositorios de Git de Cloud Manager.
* Como administrador de implementación, poder configurar canalizaciones e implementar su código en Cloud Manager.

## Desarrolladores y administradores de implementación {#roles}

Una vez que el administrador del sistema ha completado las principales tareas de incorporación de la creación de usuarios y la configuración de los recursos de la nube, los usuarios que suelen estar ansiosos por acceder al sistema son los desarrolladores y los administradores de implementación. Esto se debe a que son los usuarios responsables de crear sus aplicaciones personalizadas sobre AEM as a Cloud Service.

* **Desarrolladores**: Estos usuarios acceden a los repositorios de Git de Cloud Manager, donde administrarán el código de sus aplicaciones personalizadas de AEM.
* **Administradores de implementación**: Estos usuarios utilizan Cloud Manager para crear y ejecutar canalizaciones que implementen el código de los repositorios de Git en los entornos de AEM en ejecución.

Según sus necesidades organizativas, los mismos usuarios pueden tener ambos roles.

## Requisitos previos {#prerequisites}

Antes de comenzar las tareas descritas en este documento como desarrollador o administrador de implementación, asegúrese de que el administrador del sistema haya completado todos los pasos de este recorrido de incorporación. Esto significa lo siguiente:

* El administrador del sistema ha asignado desarrolladores y administradores de implementación a sus respectivos perfiles de producto.
* Los desarrolladores deben asignarse adicionalmente a los perfiles de producto de **usuarios de AEM** o de **administradores de AEM** para utilizar AEM también.
* Se han configurado los recursos de Cloud.

## Acceder a Git {#accessing-git}

Puede acceder a sus repositorios de Git y administrarlos mediante la administración de cuentas de Git de autoservicio desde Cloud Manager.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a la tarjeta **Canalizaciones** de la página **Información general del programa** y busque el botón **Acceder a la info del repositorio** para acceder y administrar su repositorio de Git.

   ![Botón Acceder a la info del repositorio en la tarjeta Entornos](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

1. Haga clic en el botón **Ver información de repositorios** para abrir un cuadro de diálogo para ver lo siguiente:

   * La dirección URL del repositorio de Git de Cloud Manager.
   * El nombre de usuario de Git.
   * La contraseña de Git, cuyo valor se muestra cuando se hace clic en el botón **Generar contraseña**.

   ![Información de repositorio](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

Con estas credenciales, el usuario puede clonar una copia local del repositorio y realizar cambios en ese repositorio local, y cuando esté listo, puede volver a enviar cualquier cambio de código al repositorio de código remoto en Cloud Manager.

## Configuración de canalización {#setup-pipeline}

Una vez que los desarrolladores han agregado su código personalizado a sus repositorios de Git, el administrador de implementación puede crear y ejecutar canalizaciones para implementar ese código en sus entornos de AEM.

Siga estos pasos para crear la primera canalización de implementación que no sea de producción.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Acceda a la tarjeta **Canalizaciones** de la pantalla de inicio de Cloud Manager. Haga clic en **+Agregar** y seleccione **Añadir canalización que no es de producción**.

   ![Agregar canalización que no sea de producción](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. En la pestaña **Configuración** del cuadro de diálogo **Agregar canalización que no sea de producción**, seleccione el tipo de canalización que no es de producción que desee agregar. Para este ejemplo, seleccione **Canalización de implementación**.

   ![Cuadro de diálogo Agregar canalización que no sea de producción](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. Proporcione un **Nombre de canalización que no sea de producción** para identificar la canalización junto con la siguiente información adicional.

1. Para el **activador de la implementación** seleccione **Manual** de modo que la canalización se ejecute únicamente cuando la inicie.

1. Haga clic en **Continuar**.

1. En la pestaña **Código fuente** del cuadro de diálogo **Agregar canalización que no sea de producción**, debe seleccionar qué tipo de código debe procesar la canalización. Para este ejemplo, seleccione **Código de pila completa**.

1. En el **Código fuente**, debe definir las siguientes opciones.

   * **Entornos de implementación aptos**: Debe elegir el entorno al que debe implementarse la canalización.
   * **Repositorio**: esta opción define desde qué repositorio de Git la canalización debe recuperar el código.
   * **Rama de Git**: esta opción define desde qué rama de la canalización seleccionada debe recuperar el código.
      * Introduzca los primeros caracteres del nombre de la rama y la función de autocompletar de este campo encontrará las ramas coincidentes que le ayudarán a seleccionar.

   ![Canalización de pila completa](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. Haga clic en **Guardar**.

Ahora ha creado su primera canalización. Los usuarios con el rol de administrador de implementación ahora pueden iniciar la canalización desde la interfaz de usuario de Cloud Manager.

## Implementación de {#deploy}

Ahora que los desarrolladores han agregado su código personalizado a los repositorios de Git y ha creado una canalización para implementar ese código, es hora de ejecutar la canalización para mover ese código de Git a su entorno.

![Tarjeta de canalización en Cloud Manager](/help/implementing/cloud-manager/assets/configure-pipeline/pipelines-card.png)

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Navegue hasta la tarjeta **Canalizaciones** de la página **Información general del programa**, haga clic en el botón de los tres puntos situado junto a la canalización que ha creado en la sección anterior y seleccione **Ejecutar** del menú.

1. La ejecución de la canalización comienza y se indica con la columna **Estado**.

Para ver los detalles de la ejecución, vuelva a hacer clic en el botón de los tres puntos y seleccione **Ver detalles**.

¡Enhorabuena! Ya ha implementado código desde el repositorio de Git en un entorno que no es de producción.

## Siguientes pasos {#whats-next}

Ahora que ha leído este documento, debería saber lo siguiente:

* Como desarrollador, saber acceder y administrar sus repositorios de Git de Cloud Manager.
* Como administrador de implementación, poder configurar canalizaciones e implementar su código en Cloud Manager.

Se ha puesto en marcha como desarrollador o administrador de implementación, no solo con conocimientos prácticos de Cloud Manager, sino también con entornos de trabajo, repositorios y canalizaciones. Pero hay más que aprender sobre las poderosas herramientas de CI/CD de AEM as a Cloud Service. Consulte la sección [Recursos adicionales](#additional-resources) para obtener más información.

AEM Si le interesa cómo acceden y utilizan los autores de contenido de as a Cloud Service, continúe con la parte final del recorrido AEM de incorporación, [Tareas del usuario](aem-users.md), que se encuentra en la parte superior de la página de inicio de la aplicación, que se encuentra en la parte superior de la página de inicio de la aplicación, que se encuentra en la parte superior de la página de inicio de la aplicación, y que se encuentra en la parte superior de la página de inicio de la página de inicio de la aplicación .

>[!TIP]
>
>Ahora que se ha incorporado, puede [aprender a agregar fácilmente el complemento de demostraciones de referencia de AEM](/help/journey-sites/demos-add-on/overview.md) a un entorno de zona protegida con una configuración mínima de AEM, y puede probar las potentes características de AEM con ricos ejemplos basados en las mejores prácticas.

## Recursos adicionales {#additional-resources}

Los siguientes son recursos opcionales adicionales si desea ir más allá del contenido del recorrido de incorporación.

* [Acceder a repositorios](/help/implementing/cloud-manager/managing-code/accessing-repos.md): Obtenga información sobre cómo acceder y administrar su repositorio de Git mediante la administración de cuentas de Git de autoservicio desde Cloud Manager.
* [Uso de Git con Cloud Manager](/help/implementing/cloud-manager/managing-code/integrating-with-git.md): Aprenda a utilizar los repositorios de Git de Cloud Manager y a integrar su propio repositorio de Git administrado por los clientes con Cloud Manager.
* [Configuración del entorno de desarrollo local](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=es): Este tutorial le guiará a través de la configuración de un entorno de desarrollo local para Adobe Experience Manager (AEM) mediante el SDK de AEM as a Cloud Service.
* [Introducción a AEM Sites: Tutorial de WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=es): Este tutorial de varias partes está diseñado para desarrolladores que utilicen Adobe Experience Manager (AEM) por primera vez. Este tutorial recorre la implementación de un sitio de AEM para una marca ficticia: WKND. El tutorial abarca temas fundamentales como la configuración del proyecto, los componentes principales, las plantillas editables, las bibliotecas del lado del cliente y el desarrollo de componentes con Adobe Experience Manager Sites.
* [Introducción a SPA en AEM con React](/help/implementing/developing/hybrid/getting-started-react.md): este artículo presenta una aplicación de SPA de muestra, explica cómo se crea y le permite ponerse en marcha con sus propios SPA rápidamente mediante el marco de trabajo React.
* [Introducción a SPA en AEM con Angular](/help/implementing/developing/hybrid/getting-started-angular.md): este artículo presenta una aplicación de SPA de ejemplo, explica cómo se crea y le permite ponerse en marcha con su propia SPA rápidamente mediante el marco de trabajo Angular.
* [Recorrido para desarrolladores de contenido sin encabezado](/help/journey-headless/developer/overview.md): empiece aquí para iniciar un curso guiado para desarrollar aplicaciones sin encabezamiento con AEM.
