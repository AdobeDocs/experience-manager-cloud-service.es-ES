---
title: Habilitar los componentes principales de Forms adaptables en el entorno de desarrollo as a Cloud Service y local de AEM Forms
seo-title: Step-by-Step Guide for enabling Adaptive Forms Core Components on AEM Forms as a Cloud Service and local development environment
description: Obtenga información sobre cómo habilitar los componentes principales de Forms adaptables en AEM Forms as a Cloud Service con nuestra guía paso a paso. Nuestro tutorial le guiará por el proceso, lo que facilita la activación de esta potente función para su entorno de AEM Forms.
seo-description: Learn how to enable Adaptive Forms Core Components on AEM Forms as a Cloud Service with our step-by-step guide. Our tutorial walks you through the process, making it easy to enable this powerful feature for your AEM Forms environment.
contentOwner: Khushwant Singh
docset: CloudService
role: Admin
hide: true
hidefromtoc: true
source-git-commit: 7dc36220c1f12177037aaa79d864c1ec2209a301
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 7%

---


# Habilitar los componentes principales de Forms adaptables en el entorno de desarrollo as a Cloud Service y local de AEM Forms {#enable-headless-adaptive-forms-on-aem-forms-cloud-service}

Al habilitar los componentes principales de Forms adaptable en AEM Forms as a Cloud Service, puede empezar a crear, publicar y ofrecer componentes principales basados en Forms adaptable y Forms sin encabezado mediante las instancias de Cloud Service de AEM Forms en varios canales. Se necesita un entorno habilitado para los componentes principales de Forms adaptable para utilizar Forms adaptable sin encabezado.

## Consideraciones

* Cuando crea un nuevo programa as a Cloud Service de AEM Forms, [Los componentes principales de Forms adaptable y Forms adaptable sin encabezado ya están habilitados para su entorno](#are-adaptive-forms-core-components-enabled-for-my-environment).

* Si tiene un programa as a Cloud Service de Forms anterior en el que los componentes principales estén [sin activar](#enable-components), puede [Añadir dependencias de componentes principales de Forms adaptable](#enable-headless-adaptive-forms-for-an-aem-forms-as-a-cloud-service-environment) AEM a su repositorio as a Cloud Service de la e implemente el repositorio en los entornos de su Cloud Service para habilitar Forms adaptable sin encabezado.

* Si el entorno de Cloud Service existente proporciona la opción de [crear Forms adaptable basado en componentes principales](creating-adaptive-form-core-components.md), los componentes principales de Forms adaptable y Forms adaptable sin encabezado ya están habilitados para su entorno y puede ofrecer Forms adaptable basado en componentes principales como formularios sin encabezado para canales como móvil, web, aplicaciones nativas y servicios que requieren una representación sin encabezado de Forms adaptable.


## Habilitar los componentes principales de Forms adaptables y Forms adaptable sin encabezado {#enable-headless-forms}

Realice los siguientes pasos, en el orden indicado, para habilitar los componentes principales de Forms adaptable y Forms adaptable sin encabezado para un entorno as a Cloud Service de AEM Forms


![](/help/forms/assets/enable-headless-adaptive-forms-on-aem-forms-cloud-service.png)


## 1. Clone su repositorio Git as a Cloud Service de AEM Forms {#clone-git-repository}

1. Iniciar sesión en [Cloud Manager](https://my.cloudmanager.adobe.com/) y seleccione su organización y programa.

1. Vaya a **Canalizaciones** Tarjeta de su **Resumen del programa** , haga clic en **Acceder a info del repositorio** para acceder y administrar su repositorio de Git. La página incluye la siguiente información:

   * URL del repositorio Git de Cloud Manager.
   * Credenciales del nombre de usuario de Git Repository (nombre de usuario y contraseña).

   Clic **Generar contraseña** para ver o generar la contraseña.

1. Abra el terminal o el símbolo del sistema en el equipo local y ejecute el siguiente comando:

   ```Shell
   git clone [Git Repository URL]
   ```

   Cuando se le solicite, proporcione las credenciales. El repositorio se clona en el equipo local.


## 2. Añadir dependencias de componentes principales de Forms adaptables al repositorio de Git {#add-adaptive-forms-core-components-dependencies}

1. Abra la carpeta Repositorio de Git en un editor de código de texto sin formato. Por ejemplo, VS Code.
1. Abra el archivo `[AEM Repository Folder]\pom.xml` para editarlo.
1. Reemplazar versiones de `core.forms.components.version`, `core.forms.components.af.version` y `core.wcm.components.version` componentes con versiones especificadas en [documentación de componentes principales](https://github.com/adobe/aem-core-forms-components). Si el componente no existe, agregue estos componentes.

   ```XML
   <!-- Replace the version with the latest released version at https://github.com/adobe/aem-core-forms-components/tags -->
   
   <properties>
       <core.forms.components.version>2.0.14</core.formscomponents.version>
       <core.forms.components.af.version>2.0.14</core.forms.components.af.version>  
       <core.wcm.components.version>2.21.2</core.wcmcomponents.version>
   </properties>
   ```

   ![Mencione la versión más reciente de los componentes principales de Forms](/help/forms/assets/latest-forms-component-version.png)

1. En la sección de dependencias del `[AEM Repository Folder]\pom.xml` , agregue las siguientes dependencias y guarde el archivo.

   ```XML
       <!-- WCM Core Component Examples Dependencies -->
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.apps</artifactId>
               <type>zip</type>
               <version>${core.wcm.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.content</artifactId>
               <type>zip</type>
               <version>${core.wcm.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.config</artifactId>
               <version>${core.wcm.components.version}</version>
               <type>zip</type>
           </dependency>    
           <!-- End of WCM Core Component Examples Dependencies -->
           <!-- Forms Core Component Dependencies -->
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-core</artifactId>
               <version>${core.forms.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-apps</artifactId>
               <version>${core.forms.components.version}</version>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-af-core</artifactId>
               <version>${core.forms.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-af-apps</artifactId>
               <version>${core.forms.components.version}</version>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-apps</artifactId>
               <type>zip</type>
               <version>${core.forms.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-content</artifactId>
               <type>zip</type>
               <version>${core.forms.components.version}</version>
           </dependency>
   <!-- End of AEM Forms Core Component Dependencies -->
   ```

1. Abra el archivo `[AEM Repository Folder]/all/pom.xml` para editarlo. Agregue las siguientes dependencias en la `<embeddeds>` y guarde el archivo.

   ```XML
   <!-- WCM Core Component Examples Dependencies -->
   
   <!-- inside plugin config of filevault-package-maven-plugin -->  
   <!-- embed wcm core components examples artifacts -->
   
   <embedded>
       <groupId>com.adobe.cq</groupId>
       <artifactId>core.wcm.components.examples.ui.apps</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.cq</groupId>
       <artifactId>core.wcm.components.examples.ui.content</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.cq</groupId>
       <artifactId>core.wcm.components.examples.ui.config</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <!-- embed forms core components artifacts -->
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-af-apps</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/application/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-af-core</artifactId>
       <target>/apps/${appId}-vendor-packages/application/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-examples-apps</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-examples-content</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   ```

   >[!NOTE]
   >
   >
   >  Reemplazar `${appId}` con su appId.
   >
   >  Para encontrar su `${appId}`, en el `[AEM Repository Folder]/all/pom.xml` , busque el archivo `-packages/application/install` término. El texto antes de `-packages/application/install` el término es su `${appId}`. Por ejemplo, el siguiente código, `myheadlessform` es `${appId}`.
   >
   >   
   ```
   >             <embedded>
   >                     <groupId>com.myheadlessform</groupId>
   >                     <artifactId>myheadlessform.ui.apps<artifactId>
   >                     <type>zip</type>
   >                   <target>/apps/myheadlessform-packages/application install</target>
   >             </embedded>
   >   ```

1. En el `<dependencies>` de la sección `[AEM Repository Folder]/all/pom.xml` , agregue las siguientes dependencias y guarde el archivo:

   ```XML
           <!-- Other existing dependencies -->
           <!-- wcm core components examples dependencies -->
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.apps</artifactId>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.config</artifactId>
               <type>zip</type>
               </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.content</artifactId>
               <type>zip</type>
           </dependency>
               <!-- forms core components dependencies -->
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-af-apps</artifactId>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-apps</artifactId>
               <type>zip</type>
           </dependency>
               <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-content</artifactId>
               <type>zip</type>
           </dependency>
   ```

1. Abra `[AEM Repository Folder]/ui.apps/pom.xml` para editarlo. Añada el `af-core bundle` y guarde el archivo.

   ```XML
       <dependency>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-af-core</artifactId>
       </dependency>
   ```

   >[!NOTE]
   >
   >Asegúrese de que los siguientes artefactos de componentes principales de formularios adaptables no estén incluidos en el proyecto.
   >
   > `<dependency>`
   >
   >   `<groupId>com.adobe.aem</groupId>`
   >   `<artifactId>core-forms-components-apps</artifactId>`
   >
   > `</dependency>`
   >
   > y
   >
   > `<dependency>`
   >
   >   `<groupId>com.adobe.aem</groupId>`
   >   `<artifactId>core-forms-components-core</artifactId>`
   >
   > `</dependency>`


1. Guarde y cierre el archivo.

## 3. Generar e implementar el código actualizado

Implemente el código actualizado en los entornos de desarrollo local y de Cloud Service para habilitar los componentes principales en ambos entornos:

* [AEM Cree e implemente código actualizado en un entorno de desarrollo local (SDK as a Cloud Service de la)](#core-components-on-aem-forms-local-sdk)

* [Crear e implementar código actualizado en un entorno as a Cloud Service de AEM Forms](#core-components-on-aem-forms-cs)

### Generar e implementar código actualizado en un entorno de desarrollo local {#core-components-on-aem-forms-local-sdk}

1. Abra el símbolo del sistema o el terminal.

1. Vaya al directorio raíz del proyecto del repositorio de Git.

1. Ejecute el siguiente comando para crear el paquete para su entorno:

   ```Shell
       mvn clean install
   ```



   Una vez que el paquete se haya creado correctamente, puede encontrarlo en [Carpeta de repositorio de Git]\all\target\[appid].all-[version].zip

1. Utilice el [Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=es) para implementar el [AEM Carpeta de proyecto de tipo de archivo]\all\target\[appid].all-[version]Paquete .zip en el entorno de desarrollo local.


### Crear e implementar código actualizado en un entorno as a Cloud Service de AEM Forms {#core-components-on-aem-forms-cs}

1. Abra el terminal o el símbolo del sistema.
1. Navegue hasta su `[AEM Repository Folder]` y ejecute los siguientes comandos en el orden indicado

   ```Shell
    git add pom.xml
    git add all/pom.xml
    git add ui.apps/pom.xml
    git commit -m "Added dependencies for Adaptive Forms Core Components"
    git push origin
   ```

1. Una vez que los archivos se hayan confirmado en el repositorio Git, [Ejecutar la canalización](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=es).

   Una vez que la ejecución de la canalización se haya realizado correctamente, los componentes principales de Forms adaptable se habilitan para el entorno correspondiente. Además, se añaden una plantilla de Forms adaptable (componentes principales) y una temática de Canvas 3.0 al entorno as a Cloud Service de Forms, lo que le proporciona opciones para personalizar y crear componentes principales basados en Forms adaptable.


## Preguntas frecuentes  {#faq}

### ¿Qué son los componentes principales? {#core-components}

El [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) AEM son un conjunto de componentes estandarizados de gestión de contenido web (WCM) para la administración de contenido web con el fin de acelerar el tiempo de desarrollo y reducir el coste de mantenimiento de los sitios web.

### ¿Qué se añaden todas las funciones al habilitar los componentes principales? {#core-components-capabilities}

Cuando los componentes principales de Forms adaptable están habilitados para su entorno, se agregan a este una plantilla de formulario adaptable basada en componentes principales en blanco y una temática de Canvas 3.0. Después de habilitar los componentes principales de Forms adaptable para su entorno, puede:

* [Crear componentes principales basados en Forms adaptable](/help/forms/creating-adaptive-form-core-components.md).
* [Crear componentes principales basados en plantillas de formulario adaptable](/help/forms/template-editor.md).
* [Crear temáticas personalizadas para componentes principales basadas en plantillas de formulario adaptable](/help/forms/using-themes-in-core-components.md).
* [Proporcione representaciones JSON de un formulario adaptable basado en componentes principales a canales como móvil, web, aplicaciones nativas y servicios que requieren la representación sin encabezado de un formulario](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=es).

### ¿Los componentes principales de Forms adaptable están habilitados para mi entorno? {#enable-components}

Para comprobar que los componentes principales de Forms adaptable están habilitados para su entorno:

1. [Clone su repositorio as a Cloud Service de AEM Forms](#1-clone-your-aem-forms-as-a-cloud-service-git-repository).

1. Abra el `[AEM Repository Folder]/all/pom.xml` del repositorio Git del Cloud Service de AEM Forms.

1. Busque las siguientes dependencias:

   * core-forms-components-af-core
   * core-forms-components-core
   * core-forms-components-apps
   * core-forms-components-af-apps
   * core-forms-components-example-apps
   * core-forms-components-samples-content

   ![busque el artefacto core-forms-components-af-core en all/pom.xml](/help/forms/assets/enable-headless-adaptive-forms-on-aem-forms-cloud-service-locate-core-af-artifact.png)

   Si existen dependencias, los componentes principales de Forms adaptable se habilitan para su entorno.

