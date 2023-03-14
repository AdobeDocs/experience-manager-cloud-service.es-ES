---
title: Desarrollo de AEM Commerce para AEM as a Cloud Service
description: AEM AEM Obtenga información sobre cómo generar un proyecto de habilitado para el comercio mediante el arquetipo de proyecto de. AEM Obtenga información sobre cómo crear e implementar el proyecto en un entorno de desarrollo local mediante el SDK as a Cloud Service de la aplicación de código de tiempo de ejecución (SDK) de.
topics: Commerce, Development
feature: Commerce Integration Framework
version: Cloud Service
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
exl-id: 6f28a52b-52f8-4b30-95cd-0f9cb521de62
source-git-commit: d054f960f13b7308dbf42556ef60a971e880197e
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 65%

---

# Desarrollo de AEM Commerce para AEM as a Cloud Service {#develop}

El desarrollo de proyectos de AEM Commerce basados en Commerce Integration Framework (CIF) para AEM as a Cloud Service sigue las mismas reglas y recomendaciones como otros Proyectos AEM también en AEM as a Cloud Service. Primero revise estos:

- [Estructura del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=es)
- [SDK de AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=es)
- [Directrices de desarrollo de AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=es)

## Desarrollo local con SDK de AEM as a Cloud Service {#local}

>[!VIDEO](https://video.tv.adobe.com/v/39476/?quality=12&learn=on)

Se recomienda contar con un entorno de desarrollo local para trabajar con proyectos CIF. AEM El complemento CIF previsto para el as a Cloud Service también está disponible para el desarrollo local. Se puede descargar desde el [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-es/aemcloud.html).

El complemento CIF se proporciona como un archivo de funciones Sling. El archivo zip disponible en el portal de distribución de software incluye dos archivos de archivo de funciones Sling, uno para el Autor de AEM y otro para las instancias de AEM Publish.

**¿Es novato en el uso de AEM as a Cloud Service?** Desproteger [AEM una guía más detallada para configurar un entorno de desarrollo local con el SDK as a Cloud Service de la](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=es).

### Software requerido

Lo siguiente debe instalarse de manera local:

- [SDK de AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#download-the-aem-as-a-cloud-service-sdk)
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 o posterior)
- [Node.js v10+](https://nodejs.org/en/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### Acceso al complemento CIF.

El complemento CIF se puede descargar como archivo zip desde el [portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-ES/aemcloud.html). El archivo zip contiene el complemento CIF como **Archivo de funciones Sling** AEM No, no es un paquete de. Tenga en cuenta que el acceso a los listados de SDK está limitado a aquellos con una licencia de AEM as a Cloud Service.

>[!TIP]
>
>Asegúrese de utilizar siempre la última versión del complemento CIF.

### Configuración local

Para el desarrollo del complemento CIF local mediante el uso del SDK de AEM as a Cloud Service, realice los siguientes pasos:

1. Obtenga la última versión de SDK de AEM as a Cloud Service
1. Desempaquete el archivo .jar de AEM para crear la carpeta `crx-quickstart` , ejecute:

   ```bash
   java -jar <jar name> -unpack
   ```

1. Cree una carpeta `crx-quickstart/install` .
1. Copie el archivo de funciones Sling correcto del complemento CIF en la carpeta `crx-quickstart/install` .

   El archivo zip del complemento CIF contiene dos `.far` archivos del archivo de funciones Sling. Asegúrese de utilizar el correcto para Autor de AEM o AEM Publish, según cómo vaya a ejecutar el SDK de AEM as a Cloud Service local.

1. Cree una variable de entorno del sistema operativo local con el nombre `COMMERCE_ENDPOINT` que contiene el punto final de Adobe Commerce GraphQL.

   Ejemplo con Mac OSX:

   ```bash
   export COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
   ```

   Ejemplo con Windows:

   ```bash
   set COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
   ```

   AEM Esta variable la utiliza el usuario para conectarse a su sistema de comercio de. Además, el complemento CIF incluye un proxy inverso local para que el extremo de Commerce GraphQL esté disponible localmente. Las herramientas de creación del CIF (consola de productos y selectores) y los componentes del lado del cliente del CIF que realizan llamadas directas a GraphQL lo utilizan.

   Esta variable también debe configurarse para el entorno AEM as a Cloud Service. Para obtener más información sobre las variables, consulte [AEM Configuración de OSGi para la as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html#local-development).

1. (Opcional) Para habilitar las funciones de catálogo organizadas, debe crear un token de integración para la instancia de Adobe Commerce. Siga los pasos que se indican en [Primeros pasos](./getting-started.md#staging) para crear el token.

   Establecer un secreto OSGi con el nombre `COMMERCE_AUTH_HEADER` al siguiente valor:

   ```xml
   Authorization: Bearer <Access Token>
   ```

   Para obtener más información sobre secretos, consulte [AEM Configuración de OSGi para la as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html#local-development).

1. Inicie el SDK de AEM as a Cloud Service

>[!NOTE]
>
>AEM Asegúrese de iniciar el SDK as a Cloud Service en la misma ventana de terminal en la que se configuró la variable de entorno en el paso 5. Si la inicia en una ventana de terminal independiente o hace doble clic en el archivo .jar, asegúrese de que la variable de entorno esté visible.

Verifique la configuración mediante la consola OSGI: `http://localhost:4502/system/console/osgi-installer`. La lista debe incluir los paquetes relacionados con el complemento CIF, el paquete de contenido y las configuraciones OSGI tal como se definen en el archivo del modelo de funciones.

## Configuración del proyecto {#project}

Existen dos maneras de arrancar su proyecto CIF para AEM as a Cloud Service.

### Uso del tipo de archivo del proyecto AEM

El [tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype) es la principal herramienta para arrancar un proyecto preconfigurado para comenzar con CIF. Los componentes principales de CIF y todas las configuraciones requeridas pueden incluirse en un proyecto generado con una opción adicional.

>[!TIP]
>
>Utilice siempre la versión más reciente de [AEM Tipo de archivo del proyecto](https://github.com/adobe/aem-project-archetype/releases) para generar el proyecto.

Consulte las [instrucciones de uso](https://github.com/adobe/aem-project-archetype#usage) del tipo de archivo del proyecto AEM para saber cómo generar un proyecto AEM. Para incluir CIF en el proyecto, utilice la opción `includeCommerce` .

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

Los componentes principales del CIF pueden utilizarse en cualquier proyecto incluyendo el `all` o individualmente mediante el paquete de contenido del CIF y los paquetes OSGI relacionados. Para añadir los componentes principales de CIF manualmente a un proyecto, utilice las siguientes dependencias:

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

Para comenzar con la Tienda de referencia de Venia, simplemente clone el repositorio Git y el inicio personalizando el proyecto según sus necesidades.

>[!NOTE]
>
>El proyecto de Tienda de referencia de Venia contiene dos perfiles de compilación para AEM as a Cloud Service y AEM 6.5. Compruebe el archivo [readme.md del proyecto](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) para ver cómo se utilizan.

## Recursos adicionales

- [Tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype)
- [Tienda de referencia de Venia de AEM](https://github.com/adobe/aem-cif-guides-venia)
- [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-ES/aemcloud.html)
