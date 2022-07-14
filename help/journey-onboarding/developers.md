---
title: Tareas del desarrollador y del administrador de implementación
description: Una vez que el administrador del sistema haya configurado los recursos de nube necesarios, conozca cómo los desarrolladores y los administradores de implementación pueden acceder a Git para desarrollar aplicaciones y utilizar canalizaciones para implementarlas.
feature: Onboarding
role: Admin, User, Developer
exl-id: f57a856b-0932-4e8f-be59-a19fe692e2ab
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '1400'
ht-degree: 2%

---


# Tareas del desarrollador y del administrador de implementación {#developer-deployment-manager}

En esta parte opcional del [recorrido de incorporación,](overview.md) aprenderá cómo los desarrolladores y los administradores de implementación pueden acceder a git para desarrollar aplicaciones y utilizar canalizaciones para implementarlas.

## La historia hasta ahora {#story-so-far}

¡Ha recorrido un largo camino en su recorrido de incorporación! Felicitaciones! El administrador del sistema ha completado el recorrido de incorporación configurando los recursos de nube necesarios y otorgando acceso en el documento [Asignación AEM Perfiles De Producto.](assign-profiles-aem.md)

En este punto, los desarrolladores y los administradores de implementación pueden empezar a crear sus propias aplicaciones, mientras que los usuarios de AEM pueden empezar a crear contenido. En este sentido, su incorporación está completa y ahora es el momento de usar su nuevo sistema as a Cloud Service AEM, que este documento ilustrará.

## Audiencia {#audience}

Por lo tanto, el presente documento se redacta desde la perspectiva de la **desarrollador** y **administrador de implementación**.

El administrador del sistema también puede realizar estas mismas tareas, pero generalmente estas funciones las tienen distintos usuarios.

## Objetivo {#objective}

Este documento es un suplemento del recorrido de integración para mostrar las tareas básicas de un desarrollador y un administrador de implementación una vez que el administrador del sistema ha incorporado todos los usuarios y ha creado los recursos de nube necesarios.

Después de leer este documento, debería poder hacer lo siguiente:

* Como desarrollador, debe comprender cómo acceder y administrar sus repositorios Git de Cloud Manager.
* Como administrador de implementación, puede configurar canalizaciones e implementar su código en Cloud Manager.

## Desarrolladores y gestores de implementación {#roles}

Una vez que el administrador del sistema ha completado las principales tareas de integración de la creación de usuarios y la configuración de los recursos de la nube, los usuarios que suelen estar más ansiosos de acceder al sistema son los desarrolladores y los administradores de implementación. Esto se debe a que son los usuarios responsables de crear sus aplicaciones personalizadas sobre AEM as a Cloud Service.

* **Desarrolladores** : estos usuarios acceden a los repositorios de Git de Cloud Manager, donde administrarán el código de sus aplicaciones personalizadas AEM.
* **Administradores de implementación** : Estos usuarios utilizan Cloud Manager para crear y ejecutar canalizaciones que implementen el código de los repositorios de Git en los entornos de AEM en ejecución.

Según sus necesidades organizativas, los mismos usuarios pueden tener ambas funciones.

## Requisitos previos {#prerequisites}

Antes de comenzar las tareas descritas en este documento como desarrollador o administrador de implementación, asegúrese de que el administrador del sistema haya completado todos los pasos de este recorrido de integración. Esto significa que:

* El administrador del sistema ha asignado desarrolladores y administradores de implementación a sus respectivos perfiles de producto.
* Los desarrolladores deben asignarse adicionalmente a **AEM usuarios** o **Administradores de AEM** perfiles de producto para utilizar también AEM.
* Se han configurado los recursos de Cloud.

## Acceso a Git {#accessing-git}

Puede acceder a sus repositorios Git y administrarlos mediante la administración de cuentas Git de autoservicio desde Cloud Manager.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y el programa adecuados.

1. Vaya a **Canalizaciones** tarjeta de su **Información general del programa** y busque **Acceder a información de repositorios** para acceder y administrar su Repositorio de Git.

   ![Botón Acceder a Información de Repositorio en la tarjeta Entornos](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

1. Haga clic en el **Ver información de repositorios** para abrir un cuadro de diálogo para ver:

   * Dirección URL del repositorio de Git de Cloud Manager.
   * El nombre de usuario de Git.
   * La contraseña de Git, cuyo valor se muestra cuando se usa la variable **Generar contraseña** se hace clic en el botón .

   ![Información del repositorio](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

Con estas credenciales, el usuario puede clonar una copia local del repositorio y realizar cambios en ese repositorio local, y cuando esté listo, puede volver a enviar cualquier cambio de código al repositorio de código remoto en Cloud Manager.

## Configuración de canalización {#setup-pipeline}

Una vez que los desarrolladores han agregado su código personalizado a sus repositorios Git, el administrador de implementación puede crear y ejecutar canalizaciones para implementar ese código en sus entornos AEM.

Siga estos pasos para crear la primera canalización de implementación que no sea de producción.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y el programa adecuados.

1. Acceda a la **Canalizaciones** de la pantalla de inicio de Cloud Manager. Haga clic en **+Añadir** y seleccione **Agregar canalización que no sea de producción**.

   ![Añadir canalización que no sea de producción](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. En el **Configuración** de la pestaña **Agregar canalización que no sea de producción** , seleccione el tipo de canalización que no es de producción que desee añadir. Para este ejemplo, seleccione **Canalización de implementación**.

   ![Cuadro de diálogo Agregar canalización que no sea de producción](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. Proporcione un **Nombre de canalización que no es de producción** para identificar la canalización junto con la siguiente información adicional.

1. Para la variable **Déclencheur de implementación** select **Manual** de modo que la canalización se ejecute únicamente cuando la inicie.

1. Haga clic en **Continuar**.

1. En el **Código fuente** de la pestaña **Agregar canalización que no sea de producción** , debe seleccionar qué tipo de código debe procesar la canalización. Para este ejemplo, seleccione **Código de pila completa**.

1. En el **Código fuente** , debe definir las siguientes opciones.

   * **Entornos de implementación aptos** : debe elegir el entorno al que debe implementarse la canalización.
   * **Repositorio** - Esta opción define desde qué repositorio de Git la canalización debe recuperar el código.
   * **Rama de Git** - Esta opción define desde qué rama de la canalización seleccionada debe recuperar el código.
      * Introduzca los primeros caracteres del nombre de la rama y la función de autocompletar de este campo encontrará las ramas coincidentes que le ayudarán a seleccionar.

   ![Canalización de pila completa](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. Haga clic en **Guardar**.

Ahora ha creado su primera canalización. Los usuarios con la función de administrador de implementación ahora pueden iniciar la canalización desde la interfaz de usuario de Cloud Manager.

## Implementación de {#deploy}

Ahora que los desarrolladores han agregado su código personalizado a los repositorios de Git y ha creado una canalización para implementar ese código, es hora de ejecutar la canalización para mover ese código de Git a su entorno.

![Tarjeta de canalización en Cloud Manager](/help/implementing/cloud-manager/assets/configure-pipeline/pipelines-card.png)

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y el programa adecuados.

1. Vaya a la **Canalizaciones** de la **Información general del programa** , haga clic en el botón elipsis situado junto a la canalización que ha creado en la sección anterior y seleccione **Ejecutar** del menú .

1. La ejecución de la canalización comienza y se indica con la variable **Estado** para abrir el Navegador.

Para ver los detalles de la ejecución, vuelva a hacer clic en el botón de puntos suspensivos y seleccione **Ver detalles**.

Felicitaciones! Ya ha implementado código desde el repositorio de Git en un entorno que no sea de producción.

## Siguientes pasos {#whats-next}

Ahora que ha leído este documento, debe:

* Como desarrollador, debe comprender cómo acceder y administrar sus repositorios Git de Cloud Manager.
* Como administrador de implementación, puede configurar canalizaciones e implementar su código en Cloud Manager.

Se ha puesto en marcha como desarrollador o administrador de implementación, no solo con conocimientos prácticos de Cloud Manager, sino también con entornos de trabajo, repositorios y canalizaciones. Pero hay más que aprender sobre las poderosas herramientas de CI/CD de AEM as a Cloud Service. Consulte la [Recursos adicionales](#additional-resources) para obtener más información.

Si le interesa cómo acceden y usan los autores de contenido AEM as a Cloud Service, continúe con la parte final del recorrido de incorporación, [AEM Tareas De Usuario.](aem-users.md)

>[!TIP]
>
>Ahora que está integrado, puede [obtenga información sobre cómo agregar fácilmente el complemento de demostraciones de referencia de AEM](/help/journey-sites/demos-add-on/overview.md) a un entorno de entorno limitado con una configuración de AEM mínima y poder probar las potentes funciones de AEM con ejemplos enriquecidos basados en las prácticas recomendadas.

## Recursos adicionales {#additional-resources}

* [Acceso a repositorios](/help/implementing/cloud-manager/managing-code/accessing-repos.md) : Obtenga información sobre cómo acceder y administrar su repositorio de Git mediante la administración de cuentas de Git de autoservicio desde Cloud Manager.
* [Uso de Git con Cloud Manager](/help/implementing/cloud-manager/managing-code/integrating-with-git.md) : Aprenda a utilizar los repositorios Git de Cloud Manager y a integrar su propio repositorio Git administrado por los clientes con Cloud Manager.
* [Configuración del entorno de desarrollo local](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=es) : Este tutorial le guía a través de la configuración de un entorno de desarrollo local para Adobe Experience Manager (AEM) mediante el SDK as a Cloud Service de AEM.
* [Introducción a AEM Sites: Tutorial de WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=es) : este tutorial de varias partes está diseñado para desarrolladores que utilicen Adobe Experience Manager (AEM) por primera vez. Este tutorial recorre la implementación de un sitio AEM para una marca ficticia de estilo de vida WKND. El tutorial trata temas fundamentales como la configuración del proyecto, los componentes principales, las plantillas editables, las bibliotecas del lado del cliente y el desarrollo de componentes con Adobe Experience Manager Sites.
* [Introducción a SPA en AEM con React](/help/implementing/developing/hybrid/getting-started-react.md) - Este artículo presenta una aplicación de SPA de muestra, explica cómo se crea y le permite ponerse en marcha con sus propios SPA rápidamente usando el marco React.
* [Introducción a SPA en AEM Uso de Angular](/help/implementing/developing/hybrid/getting-started-angular.md) - Este artículo presenta una aplicación de SPA de ejemplo, explica cómo se crea y le permite ponerse en marcha con su propia SPA rápidamente utilizando el marco de Angular.
* [Recorrido para desarrolladores sin objetivos](/help/journey-headless/developer/overview.md) - Empiece aquí para un curso guiado para desarrollar aplicaciones sin cabeza con AEM.
