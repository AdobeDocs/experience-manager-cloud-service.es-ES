---
title: Desarrollo de AEM Commerce para AEM as a Cloud Service
description: AEM AEM Obtenga información sobre cómo generar un proyecto de habilitado para el comercio mediante el arquetipo de proyecto de. Obtenga información sobre cómo crear e implementar el proyecto en un entorno de desarrollo local mediante el SDK para AEM as a Cloud Service.
topics: Commerce, Development
feature: Commerce Integration Framework
version: Cloud Service
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
exl-id: 6f28a52b-52f8-4b30-95cd-0f9cb521de62
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 41%

---

# Desarrollo de AEM Commerce para AEM as a Cloud Service {#develop}

AEM El desarrollo de proyectos de Commerce basados en Commerce integration framework CIF () para AEM as a Cloud Service AEM sigue las mismas reglas y prácticas recomendadas que otros proyectos de en AEM as a Cloud Service. Revise primero lo siguiente:

- [Estructura del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=es)
- [SDK de AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=es)
- [Directrices de desarrollo de AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html)

## Desarrollo local con el SDK de AEM as a Cloud Service {#local}

>[!VIDEO](https://video.tv.adobe.com/v/39476/?quality=12&learn=on)

Se recomienda contar con un entorno de desarrollo local para trabajar con proyectos CIF. CIF El complemento de proporcionado para AEM as a Cloud Service también está disponible para el desarrollo local. Se puede descargar desde el [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-es/aemcloud.html).

El complemento CIF se proporciona como un archivo de funciones Sling. El archivo zip disponible en el portal de distribución de software incluye dos archivos de archivo de funciones Sling, uno para el Autor de AEM y otro para las instancias de AEM Publish.

**¿Es novato en el uso de AEM as a Cloud Service?** Consulte [una guía más detallada para configurar un entorno de desarrollo local con el SDK para AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=es).

### Software requerido

Lo siguiente debe instalarse de manera local:

- [SDK de AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#download-the-aem-as-a-cloud-service-sdk)
- [Java™ 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 o posterior)
- [Node.js v10+](https://nodejs.org/en)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### Acceso al complemento CIF.

El complemento CIF se puede descargar como archivo zip desde el [portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-ES/aemcloud.html). CIF AEM El archivo zip contiene el complemento de como **archivo de funciones Sling**, no es un paquete de la. Se puede acceder a los listados de SDK con una licencia de AEM as a Cloud Service.

>[!TIP]
>
>Asegúrese de utilizar siempre la última versión del complemento CIF.

### Configuración local

Para el desarrollo del complemento CIF local mediante el uso del SDK de AEM as a Cloud Service, realice los siguientes pasos:

1. Obtenga la última versión de SDK de AEM as a Cloud Service
1. AEM Desempaquete el archivo .jar de la para poder crear la carpeta `crx-quickstart`. Ejecute:

   ```bash
   java -jar <jar name> -unpack
   ```

1. Cree una carpeta `crx-quickstart/install` .
1. Copie el archivo de funciones Sling correcto del complemento CIF en la carpeta `crx-quickstart/install` .

   El archivo zip del complemento CIF contiene dos `.far` archivos del archivo de funciones Sling. Asegúrese de utilizar el correcto para Autor de AEM o AEM Publish, según cómo vaya a ejecutar el SDK de AEM as a Cloud Service local.

1. Cree una variable de entorno del sistema operativo local llamada `COMMERCE_ENDPOINT` que contenga el extremo de Adobe Commerce GraphQL.

   Ejemplo de macOS X:

   ```bash
   export COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
   ```

   Ejemplo con Windows:

   ```bash
   set COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
   ```

   AEM Esta variable la utiliza el usuario para conectarse a su sistema de comercio de. CIF Además, el complemento de incluye un proxy inverso local para que el extremo de Commerce GraphQL esté disponible localmente. CIF CIF Este proxy lo utilizan las herramientas de creación de (consola de productos y selectores) y los componentes del lado del cliente que realizan llamadas directas de GraphQL, en el caso de los componentes del lado del cliente de la aplicación.

   Esta variable también debe configurarse para el entorno de AEM as a Cloud Service. Para obtener más información sobre las variables, consulte [Configuración de OSGi para AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html#local-development).

1. (Opcional) Para habilitar las funciones de catálogo organizadas, debe crear un token de integración para la instancia de Adobe Commerce. Siga los pasos en [Introducción](./getting-started.md#staging) para crear el token.

   Establezca un secreto OSGi con el nombre `COMMERCE_AUTH_HEADER` en el siguiente valor:

   ```xml
   Authorization: Bearer <Access Token>
   ```

   Para obtener más información sobre secretos, consulte [Configuración de OSGi para AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html#local-development).

1. Inicie el SDK de AEM as a Cloud Service

>[!NOTE]
>
>Asegúrese de iniciar el SDK de AEM as a Cloud Service en la misma ventana de terminal en la que se configuró la variable de entorno en el paso 5. Si la inicia en una ventana de terminal independiente o hace doble clic en el archivo .jar, asegúrese de que la variable de entorno esté visible.

Verifique la configuración mediante la consola OSGI: `http://localhost:4502/system/console/osgi-installer`. La lista debe incluir los paquetes relacionados con el complemento CIF, el paquete de contenido y las configuraciones OSGI tal como se definen en el archivo del modelo de funciones.

## Configuración del proyecto {#project}

Existen dos formas de dirigir el Bootstrap CIF de su proyecto de para AEM as a Cloud Service.

### Uso del tipo de archivo del proyecto AEM

AEM El [Tipo de archivo del proyecto de](https://github.com/adobe/aem-project-archetype) es la principal herramienta de Bootstrap CIF de un proyecto preconfigurado para empezar a usar la herramienta de creación de proyectos de tipo de archivo de tipo de archivo. Los componentes principales de CIF y todas las configuraciones requeridas pueden incluirse en un proyecto generado con una opción adicional.

>[!TIP]
>
>AEM Utilice siempre la última versión del [Arquetipo de proyecto de la serie ](https://github.com/adobe/aem-project-archetype/releases) para que pueda generar el proyecto.

Consulte las [instrucciones de uso](https://github.com/adobe/aem-project-archetype#usage) del tipo de archivo del proyecto AEM para saber cómo generar un proyecto AEM. CIF Para incluir a los usuarios en el proyecto, utilice la opción `includeCommerce`.

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

CIF CIF Los componentes principales se pueden usar en cualquier proyecto incluyendo el paquete `all` proporcionado o utilizando individualmente el paquete de contenido de la aplicación y los paquetes OSGI relacionados. CIF Para añadir manualmente componentes principales de la a un proyecto, utilice las dependencias siguientes:

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

### Tienda de referencia Venia en AEM

Una segunda opción para el inicio de un proyecto CIF es clonar y utilizar la [Tienda de referencia de Venia de AEM](https://github.com/adobe/aem-cif-guides-venia). La Tienda de referencia de Venia de AEM es una aplicación de tienda de referencia que muestra el uso de los componentes principales del CIF de AEM. Está diseñada como un conjunto de ejemplos de prácticas recomendadas y un punto de partida potencial para desarrollar su propia funcionalidad.

Para empezar con la Tienda de referencia de Venia, clone el repositorio Git y el inicio personalizando el proyecto según sus necesidades.

>[!NOTE]
>
>El proyecto Tienda de referencia de Venia contiene dos perfiles de compilación para AEM as a Cloud Service AEM y 6.5. Compruebe [readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) del proyecto para ver cómo se utilizan.

## Recursos adicionales

- [Tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype)
- [Tienda de referencia de Venia de AEM](https://github.com/adobe/aem-cif-guides-venia)
- [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-ES/aemcloud.html)
