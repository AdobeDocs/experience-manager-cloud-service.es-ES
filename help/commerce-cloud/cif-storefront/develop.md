---
title: Desarrollo de AEM Commerce para AEM as a Cloud Service
description: Obtenga información sobre cómo generar un proyecto de AEM habilitado para el comercio mediante el arquetipo de proyecto de AEM. Obtenga información sobre cómo crear e implementar el proyecto en un entorno de desarrollo local con AEM as a Cloud Service SDK.
topics: Commerce, Development
feature: Commerce Integration Framework
version: Experience Manager as a Cloud Service
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
exl-id: 6f28a52b-52f8-4b30-95cd-0f9cb521de62
role: Admin
index: false
source-git-commit: 856442039fcd25ec675a6258d182f7a35f590c3c
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 29%

---


# Desarrollo de AEM Commerce para AEM as a Cloud Service {#develop}

El desarrollo de proyectos de AEM Commerce, basados en Commerce integration framework (CIF) para AEM as a Cloud Service, sigue las mismas reglas y prácticas recomendadas que otros proyectos de AEM en AEM as a Cloud Service. Revise primero lo siguiente:

* [Estructura del proyecto AEM](/help/implementing/developing/introduction/aem-project-content-package-structure.md)
* [SDK de AEM as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
* [Directrices de desarrollo de AEM as a Cloud Service](/help/implementing/developing/introduction/development-guidelines.md)

## Desarrollo local con AEM as a Cloud Service SDK {#local}

>[!VIDEO](https://video.tv.adobe.com/v/347035/?quality=12&learn=on&captions=spa)

Se recomienda contar con un entorno de desarrollo local para trabajar con proyectos CIF. El complemento de CIF proporcionado para AEM as a Cloud Service también está disponible para el desarrollo local. Se puede descargar desde el [Portal de distribución de software.](/help/implementing/developing/tools/package-manager.md#software-distribution)

El complemento CIF se proporciona como un archivo de funciones Sling. El archivo zip disponible en el portal de distribución de software incluye dos archivos de archivo de funciones Sling, uno para el Autor de AEM y otro para las instancias de AEM Publish.

>[!TIP]
>
>**Nuevo en AEM as a Cloud Service?**
>&#x200B;>Consulte [una guía más detallada para configurar un entorno de desarrollo local con AEM as a Cloud Service SDK.](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=es)

### Software requerido {#required-software}

Lo siguiente debe instalarse de manera local:

* [SDK de AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=es#download-the-aem-as-a-cloud-service-sdk)
* [Java™ 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
* [Apache Maven](https://maven.apache.org/) (3.3.9 o posterior)
* [Node.js v10+](https://nodejs.org/en)
* [npm 6+](https://www.npmjs.com/)
* [Git](https://git-scm.com/)

### Acceso al complemento de CIF {#accessing-add-on}

El complemento de CIF se puede descargar como archivo zip desde el [Portal de distribución de software.](/help/implementing/developing/tools/package-manager.md) El archivo zip contiene el complemento de CIF como **archivo de funciones Sling**, no es un paquete de AEM. Se puede acceder a los anuncios de SDK con una licencia de AEM as a Cloud Service.

>[!TIP]
>
>Asegúrese de utilizar siempre la última versión del complemento CIF.

### Configuración local {#local-setup}

Para el desarrollo de complementos locales de CIF mediante el uso de AEM as a Cloud Service SDK, realice los siguientes pasos:

1. Obtenga la última versión de AEM as a Cloud Service SDK.
1. Desempaquete el archivo .jar de AEM para poder crear la carpeta `crx-quickstart`. Ejecute el siguiente comando:

   ```bash
   java -jar <jar name> -unpack
   ```

1. Crear una carpeta `crx-quickstart/install`.
1. Copie el archivo de funciones Sling correcto del complemento CIF en la carpeta `crx-quickstart/install` .

   * El archivo zip del complemento de CIF contiene dos archivos del archivo de funciones Sling `.far`.
   * Asegúrese de utilizar el correcto para Autor de AEM o AEM Publish, según cómo vaya a ejecutar el SDK de AEM as a Cloud Service local.

1. Cree una variable de entorno del sistema operativo local llamada `COMMERCE_ENDPOINT` que contenga el extremo de Adobe Commerce GraphQL.

   * AEM utiliza esta variable para conectarse a su sistema de comercio. El complemento de CIF incluye un proxy inverso local para que el extremo de Commerce GraphQL esté disponible localmente. Este proxy lo utilizan las herramientas de creación de CIF (consola de producto y selectores) y los componentes de cliente de CIF que realizan llamadas directas de GraphQL.

   * Esta variable también debe configurarse para el entorno de AEM as a Cloud Service. Para obtener más información sobre las variables, consulte [Configuración de OSGi para AEM as a Cloud Service.](/help/implementing/deploying/configuring-osgi.md#local-development)

   * Ejemplo en macOS:

     ```bash
     export COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
     ```

   * Ejemplo en Windows:

     ```bash
     set COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
     ```

1. (Opcional) Para habilitar las funciones de catálogo organizadas, debe crear un token de integración para la instancia de Adobe Commerce. Siga los pasos en [Introducción](/help/commerce-cloud/cif-storefront/getting-started.md#staging) para crear el token.

   * Establezca un secreto OSGi con el nombre `COMMERCE_AUTH_HEADER` en el siguiente valor:

     ```xml
     Authorization: Bearer <Access Token>
     ```

   * Para obtener más información sobre secretos, consulte [Configuración de OSGi para AEM as a Cloud Service.](/help/implementing/deploying/configuring-osgi.md#local-development)

1. Inicie AEM as a Cloud Service SDK.

>[!NOTE]
>
>Asegúrese de iniciar AEM as a Cloud Service SDK en la misma ventana de terminal en la que se configuró la variable de entorno en el paso 5. Si la inicia en una ventana de terminal independiente o hace doble clic en el archivo .jar, asegúrese de que la variable de entorno esté visible.

Verifique la configuración a través de la consola OSGi: `http://localhost:4502/system/console/osgi-installer`. La lista debe incluir los paquetes relacionados con el complemento de CIF, el paquete de contenido y las configuraciones OSGi tal como se definen en el archivo del modelo de funciones.

## Configuración del proyecto {#project}

Existen dos maneras de crear un Bootstrap para su proyecto de CIF para AEM as a Cloud Service.

### Uso del tipo de archivo del proyecto AEM {#project-archetype}

El [tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype) es la herramienta principal para Bootstrap en un proyecto preconfigurado para comenzar con CIF. Los componentes principales de CIF y todas las configuraciones requeridas pueden incluirse en un proyecto generado con una opción adicional.

>[!TIP]
>
>Use siempre la versión más reciente de [AEM Project Archetype](https://github.com/adobe/aem-project-archetype/releases) para poder generar el proyecto.

Consulte las [instrucciones de uso](https://github.com/adobe/aem-project-archetype#usage) del tipo de archivo del proyecto AEM para saber cómo generar un proyecto AEM. Para incluir CIF en el proyecto, use la opción `includeCommerce`.

Por ejemplo:

```bash
mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate \
 -D archetypeGroupId=com.adobe.aem \
 -D archetypeArtifactId=aem-project-archetype \
 -D archetypeVersion=35 \
 -D appTitle="My Site" \
 -D appId="mysite" \
 -D groupId="com.mysite" \
 -D includeCommerce=y
```

Los componentes principales de CIF se pueden utilizar en cualquier proyecto incluido el paquete `all` proporcionado o utilizando individualmente el paquete de contenido de CIF y los paquetes OSGi relacionados. Para agregar manualmente componentes principales de CIF a un proyecto, utilice las siguientes dependencias:

```java
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-apps</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-config</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-core</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>graphql-client</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>magento-graphql</artifactId>
    <version>x.y.z</version>
</dependency>
```

### Tienda de referencia Venia en AEM {#venia-reference}

Una segunda opción para el inicio de un proyecto CIF es clonar y utilizar la [Tienda de referencia de Venia de AEM](https://github.com/adobe/aem-cif-guides-venia). AEM Venia Reference Store es una aplicación de escaparate de referencia que muestra el uso de los componentes principales del CIF de AEM. Está diseñada como un conjunto de ejemplos de prácticas recomendadas y un punto de partida potencial para desarrollar su propia funcionalidad.

Para empezar con la Tienda de referencia de Venia, clone el repositorio Git y el inicio personalizando el proyecto según sus necesidades.

>[!NOTE]
>
>El proyecto Tienda de referencia de Venia contiene dos perfiles de compilación para AEM as a Cloud Service y AEM 6.5. Compruebe [readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) del proyecto para ver cómo se utilizan.

## Recursos adicionales {#additional-resources}

* [Tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype)
* [Tienda de referencia de Venia de AEM](https://github.com/adobe/aem-cif-guides-venia)
* [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-ES/aemcloud.html)
