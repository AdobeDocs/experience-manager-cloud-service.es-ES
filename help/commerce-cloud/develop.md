---
title: Desarrollar AEM comercio para AEM como Cloud Service
description: Desarrollar AEM comercio para AEM como Cloud Service
translation-type: tm+mt
source-git-commit: e30086c546d9efcc1da07ac5862c012a0db02c09
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 9%

---


# Desarrollar AEM comercio para AEM como Cloud Service {#develop}

Desarrollar proyectos comerciales AEM basados en el marco de integración comercial (CIF) para AEM como Cloud Service sigue las mismas reglas y mejores prácticas como otros proyectos AEM en AEM también como Cloud Service. Revise primero estos:

- [Estructura del proyecto de AEM](https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)
- [AEM as a Cloud Service SDK](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html)
- [Directrices de desarrollo de AEM as a Cloud Service](https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-service/implementing/developing/development-guidelines.html)

## Desarrollo local con AEM como SDK Cloud Service {#local}

Se recomienda contar con un entorno de desarrollo local para trabajar con proyectos de CIF. El Añado CIF previsto para AEM como entornos Cloud Service también está disponible para el desarrollo local. Se puede descargar desde el portal [de distribución de](https://experience.adobe.com/#/downloads/content/software-distribution/es-ES/aemcloud.html)software.

El Añada de CIF se proporciona como archivo de funciones Sling. El archivo zip disponible en el portal de distribución de software incluye dos archivos de archivo de funciones Sling, uno para AEM autor y otro para AEM instancias de publicación.

**¿Es nuevo en AEM como Cloud Service?** Consulte la [siguiente guía para configurar un entorno de desarrollo local con el AEM como SDK](https://docs.adobe.com/content/help/es-ES/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html)Cloud Service.

### Software requerido

Lo siguiente debe instalarse localmente:

- [AEM as a Cloud Service SDK](https://docs.adobe.com/content/help/en/*experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#download-the-aem-as-a-cloud-service-sdk)
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 o posterior)
- [Node.js v10+](https://nodejs.org/en/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### Acceso al complemento CIF

The CIF add-on can be downloaded as a zip file from the [Software Distribution portal](https://experience.adobe.com/#/downloads/content/software-distribution/es-ES/aemcloud.html). El archivo zip contiene el complemento CIF como archivo de funciones Sling, no es un paquete AEM. Tenga en cuenta que el acceso a los listados de SDK está limitado a aquellos con AEM como licencia de Cloud Service.

>[!TIP]
>
>Asegúrese de utilizar siempre la última versión de Añada de CIF.

### Configuración local

Para el desarrollo de Añadas de CIF local mediante el uso de la AEM como un SDK de Cloud Service, siga los pasos siguientes:

1. Obtenga la AEM más reciente como SDK de Cloud Service
2. Desempaquete el archivo .jar de AEM para crear la `crx-quickstart` carpeta, ejecute:

   ```bash
   java -jar <jar name> -unpack
   ```

3. Create a `crx-quickstart/install` folder
4. Copie el archivo de características de Sling correcto del complemento CIF en la `crx-quickstart/install` carpeta.

   El archivo zip del complemento CIF contiene dos `.far` archivos de archivo de funciones Sling. Asegúrese de utilizar el correcto para AEM Author o AEM Publish, según cómo vaya a ejecutar la AEM local como un SDK de Cloud Service.

5. Cree una variable de entorno del sistema operativo local con el nombre `COMMERCE_ENDPOINT` de mantener el extremo GraphQL de Magento.

   Ejemplo de Mac OSX:

   ```bash
   export COMMERCE_ENDPOINT=https://demo.magentosite.cloud/graphql
   ```

   Ejemplo de Windows:

   ```bash
   set COMMERCE_ENDPOINT=https://demo.magentosite.cloud/graphql
   ```

   Esta variable también debe configurarse para el AEM como entorno Cloud Service.

6. Inicio del AEM como un SDK de Cloud Service

Verifique la configuración mediante la consola OSGI:`http://localhost:4502/system/console/osgi-installer`. La lista debe incluir los paquetes relacionados con el complemento CIF, el paquete de contenido y las configuraciones OSGI tal como se definen en el archivo del modelo de funciones.

## Configuración del proyecto {#project}

Existen dos maneras de arrancar su proyecto CIF para AEM como Cloud Service.

### Usar AEM arquetipo de proyecto

El [AEM Arquetipo](https://github.com/adobe/aem-project-archetype) de Proyecto es la principal herramienta para arrancar un proyecto preconfigurado para comenzar con CIF. Los componentes principales de CIF y todas las configuraciones requeridas pueden incluirse en un proyecto generado con una opción adicional.

>[!TIP]
>
>Utilice [AEM arquetipo de proyecto 24 o posterior](https://github.com/adobe/aem-project-archetype/releases) para generar el proyecto.

Consulte AEM instrucciones [de](https://github.com/adobe/aem-project-archetype#usage) uso de Arquetipos de proyecto sobre cómo generar un proyecto AEM. Para incluir CIF en el proyecto, utilice la `includeCommerce` opción .

Por ejemplo:

```bash
mvn -B archetype:generate \
 -D archetypeGroupId=com.adobe.granite.archetypes \
 -D archetypeArtifactId=aem-project-archetype \
 -D archetypeVersion=24 \
 -D aemVersion=cloud \
 -D appTitle="My Site" \
 -D appId="mysite" \
 -D groupId="com.mysite" \
 -D frontendModule=general \
 -D includeExamples=n \
 -D includeCommerce=y
```

Los componentes principales de CIF pueden utilizarse en cualquier proyecto incluyendo el paquete proporcionado `all` o utilizando individualmente el paquete de contenido de CIF y los paquetes de OSGI relacionados. Para agregar componentes principales de CIF manualmente a un proyecto, utilice las siguientes dependencias:

```java
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-apps</artifactId>
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

### Utilizar AEM tienda de referencia de Venia

Una segunda opción para el inicio de un proyecto de CIF es clonar y utilizar la [AEM tienda](https://github.com/adobe/aem-cif-guides-venia)de referencia de Venia. El almacén de referencia de Venia AEM es una aplicación de referencia de referencia de tienda que muestra el uso de componentes principales de CIF para AEM. Está diseñado como un conjunto de ejemplos de mejores prácticas, así como como como un punto de partida potencial para desarrollar su propia funcionalidad.

Para comenzar con Venia Reference Store, simplemente clona el repositorio Git y el inicio personalizando el proyecto según sus necesidades.

>[!NOTE]
>
>El proyecto de Venia Reference Store contiene dos perfiles de compilación para AEM como Cloud Service y AEM 6.5. Compruebe el archivo readme.md [del](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) proyecto para ver cómo se utilizan.

## Recursos adicionales

- [Tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype)
- [Tienda de referencia de AEM Venecia](https://github.com/adobe/aem-cif-guides-venia)
- [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-ES/aemcloud.html)
