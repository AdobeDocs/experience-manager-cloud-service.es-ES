---
title: Configuración de un entorno de desarrollo local para Adobe Experience Manager Forms as a Cloud Service
description: Configuración de un entorno de desarrollo local para Adobe Experience Manager Forms as a Cloud Service
exl-id: 12877a77-094f-492a-af58-cffafecf79ae
source-git-commit: c7b4907a2d4dbecf03ac5b51376fb534096f5212
workflow-type: tm+mt
source-wordcount: '2704'
ht-degree: 2%

---

# Configuración de un entorno de desarrollo local y un proyecto de desarrollo inicial {#overview}

Al configurar y configurar un [!DNL  Adobe Experience Manager Forms] como [!DNL  Cloud Service] , configure entornos de desarrollo, ensayo y producción en la nube. Además, también puede configurar un entorno de desarrollo local.

Puede utilizar el entorno de desarrollo local para realizar las siguientes acciones sin iniciar sesión en el entorno de desarrollo de la nube:

* [Creación de formularios](creating-adaptive-form.md) y recursos relacionados (temas, plantillas, acciones de envío personalizadas, etc.)
* [Conversión de formularios adaptables en formularios PDF](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html?lang=es)
* Generar aplicaciones para generar [Comunicaciones del cliente](aem-forms-cloud-service-communications-introduction.md) bajo demanda o en modo por lotes.

Después de que un formulario adaptable o recursos relacionados estén listos en la instancia de desarrollo local o una aplicación para generar [Comunicaciones del cliente] está listo, puede exportar la aplicación Formulario adaptable o Comunicaciones del cliente desde el entorno de desarrollo local a un entorno de Cloud Service para realizar más pruebas o desplazarse a entornos de producción.

También puede desarrollar y probar código personalizado como componentes personalizados y servicio de relleno previo en el entorno de desarrollo local. Cuando el código personalizado esté listo y probado, puede utilizar el repositorio Git del entorno de desarrollo de Cloud Service para implementar el código personalizado.

Para configurar un nuevo entorno de desarrollo local y utilizarlo para desarrollar actividades, realice las siguientes acciones en el orden indicado:

* [Configuración de herramientas de desarrollo](#setup-development-tools-for-AEM-projects)

* [Configuración de instancias locales de creación y publicación](#set-up-local-experience-manager-environment-for-development)

* [Agregar archivos de Forms a instancias de desarrollo local y configurar usuarios](#add-forms-archive-configure-users)

* [Configuración del entorno de desarrollo local para microservicios](#docker-microservices)

* [Configuración de un proyecto de desarrollo](#forms-cloud-service-local-development-environment)

* [Configuración de las herramientas locales de Dispatcher](#setup-local-dispatcher-tools)

<!--
You can use the local development environment to create and test Adaptive Forms without connecting to the Cloud Service. [!DNL AEM Forms] provides an SDK to help test all the cloud-ready functionalities on the local development environment. When your forms and related assets are ready and tested on the local development environment, you can import these forms and related assets to an [!DNL AEM Forms] as a Cloud Service instance for publishing. 

You can also develop and test custom code like custom components and prefill service on the local development environment. When the custom code is tested and ready, you can use the Git repository of your [!DNL AEM Forms] as a Cloud Service development environment to deploy the custom code. 

>[!NOTE]
>
> Pre-pilot release does not support using an [!DNL AEM Forms] as a Cloud Service development instance to create forms. You can create forms, related assets, and custom code only on a local development environment.-->

<!--
You configure two types of development environments:

* **[!DNL AEM Forms] as a Cloud Service development environment:** Use the [[!DNL AEM Forms] as a Cloud Service](setup-forms-cloud-service.md) environment to store, manage, and publish Adaptive Forms and related assets. Do not use an [!DNL AEM Forms] as a Cloud Service environment to create Adaptive Forms and related assets <!--, form-centric workflows, a form data model, or to generate a Document of Record. -->

<!--
* **Local development environment:** You can use the local development environment to create and test Adaptive Forms without connecting to the service. Adobe provides a SDK for the local development to help test all the cloud-ready functionalities. 
Use a local development environment:
    
    * To create forms and related assets (themes, templates, custom Submit Actions, and more) and convert PDF forms to Adaptive Forms. After an Adaptive Form or related assets are ready on the local development instance, you can export the Adaptive Form and related assets from the local development environment to an [!DNL AEM Forms] as a Cloud Service development environment for publishing.  
    
    * To update configuration settings and develop and test custom code like custom components and prefill service. When the custom code is tested and ready, you can use the Git repository of your [!DNL AEM Forms] as a Cloud Service development environment to deploy the custom code.  

You can use the local development environment to create and test Adaptive Forms without connecting to the service. Adobe provides a SDK for the local development to help test all the cloud-ready functionalities. When your forms and related assets are ready and tested on the local development environment, you can import these forms and related assets to an [!DNL AEM Forms] as a Cloud Service instance for publishing. 

You can use the [development tools](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/dev-tools.html) to write custom code, customize or create new Adaptive Forms components, create a custom prefill service, or modify default configurations of an [!DNL AEM Forms] as a Cloud Service instance. 

-->

## Requisitos previos

Se necesita el siguiente software para configurar un entorno de desarrollo local. Descargue estos elementos antes de comenzar a configurar el entorno de desarrollo local:

| Software | Descripción | Vínculos de descarga |
|---|---|---|
| SDK de Adobe Experience Manager as a Cloud Service | SDK incluye [!DNL Adobe Experience Manager] Herramientas de QuickStart y Dispatcher | Descargue el SDK más reciente de [Distribución de software](#software-distribution) |  |
| Archivo de funciones de Adobe Experience Manager Forms (complemento de AEM Forms) | Herramientas para crear, aplicar estilo y optimizar Forms adaptable y otras funciones de Adobe Experience Manager Forms | Descargar desde [Distribución de software](#software-distribution) |
| (Opcional) Contenido de referencia de Adobe Experience Manager Forms | Herramientas para crear, aplicar estilo y optimizar Forms adaptable y otras funciones de Adobe Experience Manager Forms | Descargar desde [Distribución de software](#software-distribution) |
| (Opcional) Adobe Experience Manager Forms Designer | Herramientas para crear, aplicar estilo y optimizar Forms adaptable y otras funciones de Adobe Experience Manager Forms | Descargar desde [Distribución de software](#software-distribution) |

### Descargue la última versión de software de Distribución de software {#software-distribution}

Para descargar la última versión del SDK de Adobe Experience Manager as a Cloud Service, el archivo de funciones de Experience Manager Forms (complemento de AEM Forms), los recursos de referencia de formularios o Forms Designer desde [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-ES/aemcloud.html):

1. Iniciar sesión en <https://experience.adobe.com/#/downloads> con su Adobe ID

   >[!NOTE]
   >
   > La organización de Adobe debe estar aprovisionada para AEM as a Cloud Service para descargar el SDK as a Cloud Service de AEM.

1. Vaya a la **[!UICONTROL AEM as a Cloud Service]** pestaña .
1. Ordene por fecha publicada en orden descendente.
1. Haga clic en el SDK de Adobe Experience Manager as a Cloud Service más reciente, el archivo de funciones de Experience Manager Forms (complemento de AEM Forms), los recursos de referencia de formularios o Forms Designer.
1. Revisar y aceptar el EULA. Toque . **[!UICONTROL Descargar]** botón.

## Configuración de herramientas de desarrollo para AEM Proyectos {#setup-development-tools-for-AEM-projects}

El proyecto de Adobe Experience Manager Forms es una base de código personalizado. Contiene código, configuraciones y contenido que se implementa mediante Cloud Manager en [!DNL Adobe Experience Manager] as a Cloud Service. La variable [Tipo de archivo Maven del proyecto AEM](https://github.com/adobe/aem-project-archetype) proporciona la estructura de base para el proyecto.

Configure las siguientes herramientas de desarrollo para usar con su [!DNL Adobe Experience Manager] proyecto de desarrollo:

* [Java™](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#local-development-environment-set-up)
* [Git](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#install-git)
* [Node.js (npm)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#node-js)
* [Maven](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#install-maven)

Para obtener instrucciones detalladas sobre la configuración de las herramientas de desarrollo mencionadas anteriormente, consulte [Configuración de herramientas de desarrollo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html).

## Configuración del entorno de Experience Manager local para el desarrollo

El SDK de Cloud Service proporciona un archivo de inicio rápido. Ejecuta una versión local de Experience Manager. Puede ejecutar las instancias Autor o Publicar localmente.

Aunque QuickStart proporciona una experiencia de desarrollo local, no todas las funciones están disponibles en [!DNL Adobe Experience Manager] as a Cloud Service. Por lo tanto, pruebe siempre las características y el código con [!DNL Adobe Experience Manager] Entorno de desarrollo as a Cloud Service antes de mover las funciones a fase o producción.

Para instalar y configurar el entorno de Experience Manager local, realice los siguientes pasos:

* [Descargar y extraer](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) el [!DNL Adobe Experience Manager] SDK as a Cloud Service
* [Configuración de una instancia de autor](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=en#set-up-local-aem-author-service)
* [Configuración de una instancia de publicación](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=en#set-up-local-aem-publish-service)

## Agregue el archivo Forms a las instancias locales de Autor y Publicación y configure usuarios específicos de Forms {#add-forms-archive-configure-users}

Realice los siguientes pasos en el orden indicado para agregar el archivo de Forms a instancias de Experience Manager y configurar usuarios específicos de formularios:

### Instale el último archivo de funciones de complementos de Forms {#add-forms-archive}

El archivo de funciones as a Cloud Service de Adobe Experience Manager Forms proporciona herramientas para crear, diseñar y optimizar Forms adaptable en el entorno de desarrollo local. Instale el paquete para crear un formulario adaptable y utilice otras funciones de [!DNL AEM Forms]. Para instalar el paquete:

1. Descargue y extraiga la última [!DNL AEM Forms] archive para su sistema operativo desde [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

1. Vaya al directorio crx-quickstart/install. Si la carpeta no existe, créela.

1. Detenga la instancia de AEM, coloque la variable [!DNL AEM Forms] archivo de funciones de complementos, `aem-forms-addon-<version>.far`, en la carpeta de instalación y reinicie la instancia.

### Configuración de usuarios y permisos {#configure-users-and-permissions}

Cree usuarios como Desarrollador de formularios y Profesional de formularios y [agregar estos usuarios a grupos de formularios predefinidos](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?lang=en#accessing) para proporcionarles los permisos necesarios. La tabla siguiente muestra todos los tipos de usuarios y grupos predefinidos para cada tipo de usuarios de formularios:

| Tipo de usuario | Grupo AEM |
|---|---|
| Profesional del formulario / | [!DNL forms-users] (Usuarios de AEM Forms), [!DNL template-authors], [!DNL workflow-users], [!DNL workflow-editors]y [!DNL fdm-authors] |
| Desarrollador de formularios | [!DNL forms-users] (Usuarios de AEM Forms), [!DNL template-authors], [!DNL workflow-users], [!DNL workflow-editors]y [!DNL fdm-authors] |
| Diseñador de experiencia de cliente o experiencia de usuario | [!DNL forms-users], [!DNL template-authors] |
| Administrador de AEM | [!DNL aem-administrators], [!DNL fd-administrators] |
| Usuario final | Cuando un usuario debe iniciar sesión para ver y enviar un formulario adaptable, agregue estos usuarios a [!DNL forms-users] grupo. </br> Cuando no se requiera autenticación de usuario para acceder a Forms adaptable, no asigne ningún grupo a esos usuarios. |

<!--  

## Set up a local AEM instance for development

Perform the following steps in the listed order to set up and configure your local development environment:

1. **Set up an AEM author instance:** You require an author instance to create Adaptive Forms. Download and extract the latest AEM SDK archive. Run the quick start file in author run mode to set up an author instance. For detailed instructions, see [default local instance](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html).  

1. **Install the latest [!DNL AEM Forms] add-on feature archive:** [!DNL AEM Forms] add-on feature archive provides tools to create, style, and optimize Adaptive Forms on the local development environment. Install the package to create an Adaptive Form and use various other features of [!DNL AEM Forms]. To install the package:

    1. Download and extract the latest [!DNL AEM Forms] archive for your operating system from [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

    1. Navigate to the crx-quickstart/install directory. If the folder does not exist, create it.

    1. Stop your Cloud ready AEM instance, place the [!DNL AEM Forms] add-on feature archive, `aem-forms-addon-<version>.far`,  in the install folder, and restart the instance.

1. **Configure users and permissions:** Create users like Form Developer and Form Practitioner a nd add these users to pre-defined forms group to provide them required permissions. The table below lists all types of users and pre-defined groups for each type of forms users:
  
    | User Type | AEM Group |
    |---|---|
    | Form Practitioner  | forms-users (AEM Forms Users), template-authors  |
    | Form Developer | forms-users (AEM Forms Users), template-authors |
    | End-User| everyone* |

    `*` When a user should log in to access or submit Adaptive Forms, add such users to the everyone group.  -->

<!--    
### Set up an AEM project for the development tasks related to local AEM 6.5.5 Forms instance

Use this project to update configurations, create overlays, develop custom Adaptive Form components, and custom code using the local development environment. To set up the project:

1. **Install and configure Maven and set up an AEM project based on Apache Maven:** Apache Maven is an open-source tool for managing software projects. It helps automate builds and provides quality project information. It is the recommended build management tool for AEM projects. For detailed instructions to set up an AEM project based on Apache Maven, see [How to Build AEM Projects using Apache Maven](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/ht-projects-maven.html).

1. Configure the project to use [uber-jar](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=en#install-aem-forms-jee-installer) version 6.5.5 or later and [[!DNL AEM Forms] Client SDK](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/) version 6.0.160 or later.  

1. **Set Up an Integrated Development Environment:**  Set up an IDE of your choice for development, see [Set Up an Integrated Development Environment](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) for detailed instructions.
 -->

## Configuración del entorno de desarrollo local para el documento de registro (DoR){#docker-microservices}

AEM Forms as a Cloud Services proporciona un entorno SDK basado en docker que facilita el desarrollo del documento de registro y el uso de otros microservicios. Le libera de la configuración manual de binarios y adaptaciones específicos de la plataforma. Para configurar el entorno:

1. Instalar y configurar el acoplador:

   * Instalación (para Microsoft® Windows) [Docker Desktop](https://www.docker.com/products/docker-desktop). Configura `Docker Engine` y `docker-compose` en su máquina.

   * Instalación de (Apple macOS) [Docker Desktop para Mac](https://hub.docker.com/editions/community/docker-ce-desktop-mac). Incluye Docker Engine, Docker CLI client, Docker Compose, Docker Content Trust, Kubernetes y Credential Helper.

   * Instalación (para Linux®) [Motor de acoplamiento](https://docs.docker.com/engine/install/#server) y [Composición de Docker](https://docs.docker.com/compose/install/) en su máquina.
   >[!NOTE]
   >
   > * Para Apple macOS, carpetas de lista de permitidos que contienen instancias locales de AEM Author.
   >
   > * Docker Desktop para Windows admite dos backends, Hyper-V
      > (heredado) y WSL2 (moderno). El uso compartido de archivos se realiza automáticamente
      > gestionado por Docker cuando se utiliza WSL2 (moderno). Tiene que
      > configure explícitamente el uso compartido de archivos mientras utiliza Hyper-V (heredado).


1. Cree una carpeta, por ejemplo aem-sdk, en paralelo a las instancias de autor y publicación. Por ejemplo, C:\aem-sdk.

1. Extraiga el `aem-forms-addon-<version>.zip\aem-forms-addon-native-<version>.zip` archivo.

   ![formularios aem extraídos agregar en nativos](assets/microservice-docker.png)

1. Cree una variable de entorno AEM_HOME y elija la instalación local de AEM Author. Por ejemplo, C:\aem\author\.

1. Abra sdk.bat o sdk.sh para editarlo. Establezca AEM_HOME para que apunte a la instalación local de AEM Author. Por ejemplo, C:\aem\author\.

1. Abra el símbolo del sistema y vaya a la `aem-forms-addon-native-<version>` carpeta.

1. Asegúrese de que la instancia local de AEM Author esté funcionando. Ejecute el siguiente comando para iniciar el SDK:

   * (en Microsoft® Windows) `sdk.bat start`
   * (en Linux® o Apple macOS) `AEM_HOME=[local AEM Author installation] ./sdk.sh start`

   >[!NOTE]
   >
   > Si ha definido la variable de entorno en el archivo sdk.sh , especificarla en la línea de comandos es opcional. La opción para definir la variable de entorno en la línea de comandos se proporciona para ejecutar el comando sin actualizar la secuencia de comandos shell.

   ![start-sdk-command](assets/start-sdk.png)

Ahora puede utilizar el entorno de desarrollo local para procesar el documento de registro. Para realizar pruebas, cargue un archivo XDP en su entorno y prográmelo. Por ejemplo, <http://localhost:4502/libs/xfaforms/profiles/default.print.pdf?template=crx:///content/dam/formsanddocuments/cheque-request.xdp> convierte el archivo XDP al documento PDF.

## Configuración de un proyecto de desarrollo para Forms basado en el arquetipo de Experience Manager {#forms-cloud-service-local-development-environment}

Utilice este proyecto para crear Forms adaptable, implementar actualizaciones de configuración, superposiciones, crear componentes de formulario adaptable personalizados, probar y código personalizado en local [!DNL Experience Manager Forms] SDK. Después de realizar la prueba localmente, puede implementar el proyecto en  [!DNL Experience Manager Forms] Entornos de producción y no producción as a Cloud Service. Al implementar el proyecto, también se implementan los siguientes recursos de AEM Forms:

| Temas | Plantillas | Modelos de datos de formulario |
---------|----------|---------
| Lienzo 3.0 | Básico | Microsoft® Dynamics 365 |
| Tranquilo | Vacío | Salesforce |
| Urbane |  |  |
| Ultramarino |  |  |
| Beryl |  |  |

>[!NOTE]
>
> Configure AEM tipo de archivo versión 30 o posterior para obtener y utilizar los modelos de datos de formulario Microsoft® Dynamics 365 y Salesforce con AEM Forms as a Cloud Service.
> Configure AEM tipo de archivo versión 32 o posterior para obtener y utilizar temas de Tranquil, Urbane y Ultramarine con AEM Forms as a Cloud Service.

Para configurar el proyecto:

1. **Clonar repositorio Git de Cloud Manager en la instancia de desarrollo local:**  El repositorio Git de Cloud Manager contiene un proyecto de AEM predeterminado. Se basa en [Tipo de archivo AEM](https://github.com/adobe/aem-project-archetype/). Clona el repositorio Git de Cloud Manager mediante la administración de cuentas Git de autoservicio de la interfaz de usuario de Cloud Manager para llevar el proyecto a su entorno de desarrollo local. Para obtener más información sobre el acceso al repositorio, consulte [Acceso a repositorios](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/accessing-repos.html).

<!-- 1. 
After the repository is cloned, [integrate your Git repo with Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html)

**Make cloned AEM project compatible with [!DNL AEM Forms] as a Cloud Service:** Remove uber-jar and other non-cloud dependencies from the pom.xml files of the project. You can refer the pom.xml files of the [sample AEM project](assets/FaaCSample.zip) for the list of required dependencies and update your AEM project accordingly. You can also refer [AEM Project Structure](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html) to learn changes required to make an AEM project compatible with AEM as a Cloud Service.  -->

1. **Cree un [!DNL Experience Manager Forms] como [Cloud Service] proyecto:** Cree un [!DNL Experience Manager Forms] como [Cloud Service] proyecto basado en [AEM Tipo de archivo 32](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-32) o posterior. El arquetipo ayuda a los desarrolladores a empezar a desarrollarse fácilmente para [!DNL AEM Forms] as a Cloud Service. También incluye algunos temas de muestra y plantillas para ayudarle a empezar rápidamente.

   Abra el símbolo del sistema y ejecute el siguiente comando para crear un [!DNL Experience Manager Forms] proyecto as a Cloud Service.

   ```shell
   mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype-DarchetypeVersion=32 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeFormsenrollment="y" -DincludeFormscommunications="y" -DincludeExamples="y"
   ```

   Cambie el `appTitle`, `appId`y `groupId` en el comando anterior para reflejar su entorno.

   * Utilice la variable `includeFormsenrollment=y` para incluir configuraciones, temas, plantillas, componentes principales y dependencias específicos de Forms necesarios para crear Forms adaptable. Si utiliza Forms Portal, establezca la variable `includeExamples=y` . Agrega al proyecto los componentes principales de Forms Portal.

   * Utilice la variable `includeFormscommunications=y` incluye los componentes principales de Forms y las dependencias necesarias para incluir la funcionalidad de comunicaciones del cliente.

1. Implemente el proyecto en el entorno de desarrollo local. Puede utilizar el siguiente comando para implementar en el entorno de desarrollo local

   `mvn -PautoInstallPackage clean install`

   Para obtener la lista completa de comandos, consulte [Creación e instalación](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en#building-and-installing)

1. [Implemente el código en su [!DNL AEM Forms] Entorno as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#customer-releases).

## Configuración de las herramientas locales de Dispatcher {#setup-local-dispatcher-tools}

Dispatcher es un módulo de servidor web HTTP Apache que proporciona una capa de seguridad y rendimiento entre el nivel de CDN y AEM Publish. Dispatcher es una parte integral de la arquitectura del Experience Manager general y debe formar parte del entorno de desarrollo local.

Realice los siguientes pasos para configurar el Dispatcher local y luego agregarle reglas específicas de Forms:

### Configuración de Dispatcher local {#setup-local-dispatcher}

La variable [!DNL Experience Manager] El SDK as a Cloud Service incluye la versión de herramientas de Dispatcher recomendada, que facilita la configuración, validación y simulación de Dispatcher localmente. Las herramientas de Dispatcher están basadas en Docker y proporcionan herramientas de línea de comandos para transformar archivos de configuración de Apache HTTP Web Server y Dispatcher en un formato compatible e implementarlos en Dispatcher que se ejecuta en el contenedor de Docker.

El almacenamiento en caché en Dispatcher permite [!DNL AEM Forms] para rellenar previamente Forms adaptable en un cliente. Mejora la velocidad de procesamiento de los formularios rellenados previamente.

Para obtener instrucciones detalladas sobre la configuración de Dispatcher, consulte [Configuración de las herramientas locales de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#local-development-environment-set-up)

### Agregar reglas específicas de Forms a Dispatcher {#forms-specific-rules-to-dispatcher}

Realice los siguientes pasos para configurar la caché de Dispatcher para Experience Manager Forms as a Cloud Service:

1. Abra el proyecto AEM y vaya a `\src\conf.dispatcher.d\available_farms`
1. Cree una copia del `default.farm` archivo. Por ejemplo, `forms.farm`.
1. Abra la `forms.farm` para editar y reemplazar el siguiente código:

   ```json
   #/ignoreUrlParams {
   #/0001 { /glob "*" /type "deny" }
   #/0002 { /glob "q" /type "allow" }
   #}
   ```

   con

   ```json
   /ignoreUrlParams {
   /0001 { /glob "*" /type "deny" }
   /0002 { /glob "dataRef" /type "allow" }
   }
   ```

1. Guarde y cierre el archivo.
1. Vaya a `conf.d/enabled_farms` y cree un vínculo simbólico al `forms.farm` archivo.
1. Compile e implemente el proyecto en su [!DNL AEM Forms] Entorno as a Cloud Service.

### Consideraciones sobre el almacenamiento en caché {#considerations-about-caching}

* El almacenamiento en caché de Dispatcher permite [!DNL AEM Forms] para rellenar previamente Forms adaptable en un cliente. Mejora la velocidad de procesamiento de los formularios rellenados previamente.
* El almacenamiento en caché de las funciones de contenido seguro está deshabilitado de forma predeterminada. Para habilitar la función, puede realizar las instrucciones que se proporcionan en la [Almacenamiento en caché de contenido seguro](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=en) article
* Dispatcher puede no invalidar algunos Forms adaptables y los Forms adaptables relacionados. Para resolver estos problemas, consulte [[!DNL AEM Forms] Almacenamiento en caché](troubleshooting-caching-performance.md) en la sección resolución de problemas.
* Almacenamiento en caché de Forms adaptable localizado:
   * Usar formato de URL `http://host:port/content/forms/af/<afName>.<locale>.html` para solicitar una versión localizada de un formulario adaptable en lugar de `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * La opción Configuración regional del explorador está desactivada de forma predeterminada. Para cambiar la configuración regional del navegador,
* Cuando se usa el formato de URL `http://host:port/content/forms/af/<adaptivefName>.html`y Utilizar configuración regional del explorador en el administrador de configuración está desactivado, se proporciona la versión no localizada del formulario adaptable. El idioma no localizado es el idioma utilizado al desarrollar el formulario adaptable. No se tiene en cuenta la configuración regional configurada para el explorador (configuración regional del explorador) y se proporciona una versión no localizada del formulario adaptable.
* Cuando se usa el formato de URL `http://host:port/content/forms/af/<adaptivefName>.html`, y Utilizar configuración regional del explorador en el administrador de configuración está habilitado, se proporciona una versión localizada del formulario adaptable, si está disponible. El idioma del formulario adaptable localizado se basa en la configuración regional configurada para el explorador (configuración regional del explorador). Puede llevar a [almacenamiento en caché solo de la primera instancia de un formulario adaptable]. Para evitar que el problema se produzca en la instancia, consulte [solo se almacena en caché la primera instancia de un formulario adaptable](troubleshooting-caching-performance.md) en la sección resolución de problemas.

El entorno de desarrollo local está listo.

## Actualice el entorno de desarrollo local {#upgrade-your-local-development-environment}

La actualización del SDK a una nueva versión requiere la sustitución de todo el entorno de desarrollo local, lo que provoca la pérdida de todo el código, la configuración y el contenido en los repositorios locales. Asegúrese de que cualquier código, configuración o contenido que no se deba destruir se comprometa de forma segura con Git o se exporta desde las instancias de Experience Manager locales como paquetes CRX.

### Cómo evitar la pérdida de contenido al actualizar el SDK {#avoid-content-loss-when-upgrading--SDK}

La actualización del SDK crea de forma eficaz una nueva instancia de Autor y Publicación, que incluye un nuevo repositorio ([Configurar AEM proyecto](#forms-cloud-service-local-development-environment)), lo que significa que se pierden los cambios realizados en un repositorio de SDK anterior. Para conocer estrategias viables que permitan mantener el contenido entre actualizaciones de SDK, consulte [Cómo evitar la pérdida de contenido al actualizar el SDK de AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=en#optional-local-aem-runtime-set-up-tasks)

<!--When you update any  Forms-specifc configuration, create overlays, develop custom Adaptive Form components, or develop and test any custom code in AEM project for the development tasks related to local development instance, use the AEM project cloned from the Cloud Manager Git repository to [deploy the custom code and other changes to your [!DNL AEM Forms] as a Cloud Service's production or non-production environment](https://video.tv.adobe.com/v/30191?quality=9).

## Upgrade your local development environment {#update-local-setup}

Update the local AEM setup (AEM SDK) to latest version at least monthly on, or shortly after, the last Thursday of each month, which is the release cadence for AEM as a Cloud Service "feature releases". You can download local AEM SDK from [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

Updating the AEM SDK to a new version requires replacing the entire local development environment, resulting in a loss of all code, configuration and content in the local AEM repositories. Ensure that any code, config or content that should not be destroyed is safely committed to Git, or exported from the local AEM instance as AEM Packages.

### How to avoid content loss when upgrading the AEM SDK {#avoid-content-loss-when-upgrading--AEM-SDK}

Upgrading the AEM SDK is effectively creating a brand new AEM runtime ([Set up a local AEM instance](setup-forms-cloud-service.md)), including a new repository ([Set up AEM project](#forms-cloud-service-local-development-environment)), meaning any changes made to a prior AEM SDK's repository are lost. The following are viable strategies for aiding in persisting content between AEM SDK upgrades, and can be used discretely or in concert:

1. Create a content package dedicated to containing the sample content to aid in development and maintain it in Git. Any content that should be persisted through AEM SDK upgrades would be persisted into this package and re-deployed after upgrading the AEM SDK.
1. Use [oak-upgrade](https://jackrabbit.apache.org/oak/docs/migration.html) with the `includepaths` directive, to copy content from the prior AEM SDK repository to the new AEM SDK repository.
1. Back up any content using AEM Package Manager and content packages on the prior AEM SDK and re-install them on the new AEM SDK.

Remember, using the above approaches to maintain code between AEM SDK upgrades, indicates a development anti-pattern. Non-disposable code should originate in your Development IDE and flow into AEM SDK via deployments.

For information about troubleshooting, stopping local AEM environment, run modes, and deployment, see [Set up local AEM Runtime](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#local-development-environment-set-up).-->

### Realizar una copia de seguridad e importar contenido específico de Forms a un nuevo entorno de SDK {#backup-and-import-Forms-specific-content-to-new-SDK-environment}

Para realizar una copia de seguridad y mover recursos del SDK existente a un nuevo entorno de SDK:

* Cree una copia de seguridad del contenido existente.

* Configure un nuevo entorno de SDK.

* Importe la copia de seguridad en su nuevo entorno de SDK.

### Crear una copia de seguridad del contenido existente {#create-backup-of-your-existing-content}

Haga una copia de seguridad de su Forms adaptable, plantillas, modelo de datos de formulario, tema, configuraciones y código personalizado. Puede realizar la siguiente acción para crear una copia de seguridad:

1. [Descargar](import-export-forms-templates.md#manage-forms-and-related-assets) Forms adaptable, temas y PDF forms.
1. Exportar plantillas de formulario adaptable.

1. Descargar modelos de datos de formulario

1. Exporte plantillas editables, configuraciones de nube y modelos de flujo de trabajo. Para exportar todos los elementos mencionados anteriormente desde el SDK existente, cree un [CRX-Package](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=es) con los filtros siguientes:

   * /conf/ReferenceEditableTemplates
   * /conf/global/settings/cloudconfigs
   * /conf/global/settings/wcm
   * /var/workflow/models
   * /conf/global/settings/workflow
1. Exporte configuraciones de correo electrónico, envíe y rellene previamente código de acciones desde su entorno de desarrollo local. Para exportar esta configuración y configuración, cree una copia de las siguientes carpetas y archivos en el entorno de desarrollo local:

   * `[Archetype Project in Cloud Service Git]/core/src/main/java/com/<program name>/core/service`
   * `[Archetype Project in Cloud Service Git] /core/src/main/java/com/<program name>/core/servlets/FileAttachmentServlet.java`
   * `[Archetype Project in Cloud Service Git]/ui.apps/src/main/content/jcr_root/apps/<program name>/config`

### Importe la copia de seguridad en su nuevo entorno de SDK {#import-the-backup-to-your-new-SDK-environment}

Importe Forms adaptable, plantillas, modelo de datos de formulario, tema, configuraciones y código personalizado a su nuevo entorno. Puede realizar la siguiente acción para importar la copia de seguridad:

1. [Importar](import-export-forms-templates.md#manage-forms-and-related-assets) Forms adaptable, temas y PDF forms a nuevos entornos de SDK.
1. Importar plantillas de formulario adaptable al nuevo entorno del SDK.

1. Cargar modelos de datos de formulario al nuevo entorno del SDK.

1. Importe plantillas editables, configuraciones de nube y modelos de flujo de trabajo. Para importar todos los elementos mencionados anteriormente en su nuevo entorno de SDK, importe el CRX-Package que contenga estos elementos en su nuevo entorno de SDK.

1. Importe configuraciones de correo electrónico, envíe y rellene previamente código de acciones desde su entorno de desarrollo local. Para importar estos ajustes y configuraciones, coloque los siguientes archivos del antiguo proyecto de tipo de archivo en el nuevo proyecto de tipo de archivo:

   * `[Archetype Project in Cloud Service Git]/core/src/main/java/com/<program name>/core/service`
   * `[Archetype Project in Cloud Service Git] /core/src/main/java/com/<program name>/core/servlets/FileAttachmentServlet.java`
   * `[Archetype Project in Cloud Service Git]/ui.apps/src/main/content/jcr_root/apps/<program name>/config`

El nuevo entorno ahora tiene formularios y recursos relacionados del entorno antiguo.
