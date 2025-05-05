---
title: Introducción a Forms adaptable.
description: Aprenda a crear formularios adaptables con capacidad de respuesta móvil con nuestro tutorial paso a paso. Estos formularios se adaptan perfectamente a todos los dispositivos, lo que garantiza una experiencia sin problemas.
keywords: Formularios adaptables, formularios adaptables, formularios HTML5
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
hide: true
hidefromtoc: true
exl-id: b59cb56c-9629-48e4-b5c9-a861013a1360
source-git-commit: af58a784f24f212962ad73f11015fb788493d8b5
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 6%

---

# Creación de un formulario adaptable (componentes principales): tutorial

En este día y esta edad, los usuarios esperan una experiencia adaptada a dispositivos móviles en todas sus interacciones y los formularios no son una excepción. Los formularios adaptables pueden ayudarle a crear formularios que no solo sean compatibles con dispositivos móviles, sino que también mejoren la participación del usuario y reduzcan el tiempo necesario para completarlos.

Este tutorial proporciona una guía paso a paso para crear un formulario adaptable. Se desglosa en un caso de uso y varias guías, cada una de las cuales le enseñará a agregar una nueva característica al formulario adaptable.

Al final del tutorial, debe ser capaz de:

* Crear un formulario adaptable y su modelo de datos
* Aplicar estilo a un formulario adaptable
* Generar reglas empresariales con el editor de reglas de formularios adaptables
* Rellenar previamente campos de formulario adaptables
* Agregar firmas electrónicas al formulario
* Protect su formulario desde bots mediante Google reCAPTCHA
* Localice el formulario adaptable para diferentes idiomas
* Configurar el formulario para que produzca datos estructurados
* Configure el formulario para enviar datos a un extremo REST
* Publish su formulario adaptable


## ¿Por qué crear formularios basados en componentes principales?

AEM Forms proporciona Componentes básicos y Componentes principales para crear experiencias de formularios. Los componentes principales son el método moderno y recomendado para crear cualquier nueva experiencia de formularios. ¿Por qué utilizar los componentes principales? Estos componentes son ligeros, de código abierto (disponibles en github), ofrecen una buena puntuación de Google Lighthouse y web vitales, cumplen con la accesibilidad y aportan todas las funciones familiares de AEM Sites (como el control de versiones y la localización). Además, estos componentes son más fáciles de diseñar y se puede personalizar fácilmente su aspecto según las directrices de marca de su organización. No tienen dependencias de terceros, cualquier desarrollador con conocimientos de JavaScript y CSS puede personalizar fácilmente estos componentes.

![¿Por qué crear componentes principales basados en Forms adaptable? AEM AEM Estos componentes son ligeros, fáciles de diseñar, ofrecen una puntuación alta en cuanto a faro, admiten estándares de accesibilidad, se pueden personalizar fácilmente, son de código abierto, están disponibles en github, no dependen de bibliotecas de terceros y casi no tienen una curva de aprendizaje para desarrolladores y autores de. Además, los componentes principales de AEM Forms AEM tienen todas las características de los componentes principales de WCM.](/help/forms/assets/cc-core-components-benefits.png){width="50%"}

## Caso de uso: calificación previa optimizada de préstamos para el hogar con Forms adaptable

En este tutorial, creará un formulario adaptable para un banco grande. El caso de uso es:

Los posibles compradores de viviendas visitan el sitio web o la sucursal del banco para explorar las opciones de préstamo de viviendas. El proceso de solicitud tradicional es largo y abrumador, y a menudo requiere documentación por adelantado. Esto disuade a algunos compradores de iniciar el proceso, dificultando tanto la generación de clientes potenciales del banco como la capacidad del comprador para buscar con confianza la casa de sus sueños.

Se le encarga que desarrolle un formulario interactivo de precalificación de préstamo hipotecario. Este formulario reuniría información básica, precalificaría al prestatario en función de sus insumos, ofreciendo cantidades estimadas de préstamos, posibles necesidades de pago inicial y tasas de interés basadas en diferentes tipos de préstamos. Los usuarios precalificados podrían iniciar una solicitud de préstamo completa directamente desde el formulario de precalificación.

El formulario se crearía con formularios adaptables. Esto permite una experiencia personalizada mientras se recopilan los datos financieros necesarios para una precalificación precisa del préstamo hipotecario.

Al finalizar el tutorial, el formulario tendría el siguiente aspecto y funcionaría de la siguiente manera:

![Agregar un formulario de trabajo aquí](/help/forms/assets/cc-tutorial-final-form.png)

## Configurar el entorno de desarrollo

Puede crear y probar el formulario adaptable directamente en el equipo local, antes de implementarlo en un entorno de Cloud Service. El Adobe AEM de proporciona un SDK para la aplicación de para el desarrollo local que le permite

* Cree, personalice y pruebe formularios localmente.
* Diseñar temáticas de formularios y crear configuraciones localmente.
* Implemente fácilmente los recursos finalizados en la nube.

AEM El desarrollo local con el SDK de la le ahorra tiempo y simplifica el proceso de desarrollo


**¿Listo para comenzar?**

1. AEM [Configurar herramientas de desarrollo para proyectos de](/help/forms/setup-local-development-environment.md#set-up-development-tools-for-aem-projects): Descargue e instale la última versión de [Java 11™](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=es#local-development-environment-set-up), [Git](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=es#install-git), [Node.js (npm)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=es#node-js) y [Maven](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=es#install-maven). Instale también un editor de texto sin formato. Los ejemplos de este tutorial se basan en Visual Studio Code.

1. AEM AEM [Instalar el SDK de la](/help/forms/setup-local-development-environment.md#set-up-local-experience-manager-environment-for-development): Descargue e instale la versión más reciente del SDK de la. AEM Esto proporciona las herramientas esenciales para el desarrollo de la. AEM Tenga en cuenta la versión del SDK de.

   ![Distribución de software](/help/forms/assets/software-distribution.png)

   AEM ![instalar SDK de la](/help/forms/assets/start-aem-sdk.png)

1. [Agregar el complemento de AEM Forms](/help/forms/setup-local-development-environment.md#add-forms-archive-to-local-author-and-publish-instances-and-configure-forms-specific-users): descargue e instale el complemento de AEM Forms AEM que coincida con la versión de su SDK de desde el portal de [Distribución de software](https://experience.adobe.com/#/downloads).
   ![install-aem-forms-add-on](/help/forms/assets/install-aem-forms-add-on.png)

   +++Instalar el complemento de AEM Forms:

   Para instalar el complemento de AEM Forms:

   1. AEM Detenga el SDK de.
   1. Agregue el archivo de complemento de AEM Forms (.far) a la carpeta `AEM SDK/crx-quickstart/install`,
   1. AEM Reinicie el SDK de.

   +++

1. [Configurar permisos de usuario](/help/forms/setup-local-development-environment.md#configure-users-and-permissions): cree usuarios con permisos de desarrollo, creación y otros permisos y agréguelos a grupos de formularios predefinidos.


1. [Agregar plantillas de Forms AEM AEM AEM adaptables](/help/forms/setup-local-development-environment.md#set-up-a-development-project-for-forms-based-on-experience-manager-archetype): Use los tipos de archivo 48 o posteriores de la para crear un nuevo proyecto de e implementarlo en el SDK de la aplicación. El proyecto agrega plantillas de Forms AEM adaptables al SDK de la.

   ![Plantillas de formulario adaptable](/help/forms/assets/adaptive-forms-templates.png)

   +++Agregue plantillas de Forms AEM adaptables al SDK de la:

   1. AEM Ejecute el siguiente comando para crear un proyecto de.

      ```
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate -D archetypeGroupId=com.adobe.aem -D archetypeArtifactId=aem-project-archetype -D archetypeVersion="48" -D appTitle=securbank -D appId=securbank -D groupId=com.securbank -D includeFormsenrollment="y" -D aemVersion="cloud"
      ```

      AEM ![Proyecto-Arquetioe-](/help/forms/assets/aem-archetype-project.png)

   1. Implemente el proyecto en su entorno de desarrollo local. Puede utilizar el siguiente comando para implementarlo en su entorno de desarrollo local

      ```
      cd securbank
      
      mvn -PautoInstallPackage clean install
      ```

   AEM Después de implementar el proyecto de, puede ver plantillas de Forms adaptables en su entorno.

   +++


Para obtener instrucciones detalladas y una guía paso a paso sobre la configuración de su entorno de desarrollo local de AEM Forms, consulte el artículo [configurar el entorno de desarrollo local para AEM Forms](/help/forms/setup-local-development-environment.md).



## Siguiente paso

Después de configurar el entorno de desarrollo, estará listo para crear un formulario adaptable. En el artículo siguiente, aprenderá a lo siguiente

* Cree un formulario adaptable a partir de la plantilla en blanco
* Campos de diseño para mostrar y aceptar fácilmente la información.
* Previsualice el formulario.

<!-- 

### Step 2: Create Form Data Model

A form data model lets you connect an adaptive form to disparate data sources. For example, AEM user profile, RESTful web services, SOAP-based web services, OData services, and relational databases. You can use the form data model with an adaptive form to retrieve, update, delete, and add data to connected data sources.

Goals of article:

* Create the form data model using Rest endpoint.
* Add data model objects so you can form the data model.
* Configure read and write services for the form data model.
* Test form data model and configured services with test data.

### Step 4: Apply rules to adaptive form fields

AEM Forms provide an editor to write rules on adaptive form objects. These rules define actions to trigger on form objects based on preset conditions, user inputs, and user actions on the form. It helps ensure accuracy and speeds up the form-filling experience.

Goals:

* Create and apply rules to adaptive form fields.
* Use rules to trigger form data model services to update the data to database.

### Step 5: Style your adaptive form

Adaptive forms provide OOTB themes and allows you to customize an existing theme to make a brand specific theme. 


A theme contains styling details for components and panels, and you can reuse a theme in different forms. Styles include properties such as background colors, state colors, transparency, alignment, and size. When you apply the theme to your form, the specified style reflects on corresponding components of your form.

Goals:

* Apply an out of the box theme to an adaptive form.
* Create your brand specific theme.


### Step 6: Publish your adaptive form

You can publish adaptive forms as a stand-alone form (single page application), include in AEM Sites page, or include in a non-AEM Sites page.

Goals:

* Publish the adaptive form as an AEM Page.
* Embed the adaptive form in an AEM Sites Page.
* Embed the adaptive form in an external webpage (a non-AEM webpage hosted outside AEM).

-->
