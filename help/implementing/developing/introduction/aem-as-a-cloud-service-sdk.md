---
title: SDK de AEM as a Cloud Service
description: Descripción general del kit de desarrollo de software de AEM as a Cloud Service
exl-id: 06f3d5ee-440e-4cc5-877a-5038f9bd44c6
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1213'
ht-degree: 1%

---

# SDK de AEM as a Cloud Service {#aem-as-a-cloud-service-sdk}

El SDK de AEM as a Cloud Service está compuesto por los siguientes artefactos:

* AEM **Jar de inicio rápido**: tiempo de ejecución de la utilizado para el desarrollo local
* **Jar de API de Java™**: la dependencia Java™ Jar/Maven que expone todas las API de Java™ permitidas que se pueden usar para desarrollar con AEM as a Cloud Service. Anteriormente conocido como el Uberjar
* **Javadoc Jar**: el javadocs para el Jar de la API de Java™
* **Herramientas de Dispatcher**: conjunto de herramientas utilizadas para desarrollar Dispatcher localmente. Separar artefactos para UNIX® y ventanas

AEM Además, algunos clientes que se implementaron anteriormente con la versión 6.5 o versiones anteriores de utilizan los artefactos que se muestran a continuación. AEM Si la compilación local no funciona con el JAR de inicio rápido y sospecha que se debe a la eliminación de interfaces del as a Cloud Service implementado, póngase en contacto con el servicio de atención al cliente. Pueden determinar si necesita acceso. Requiere cambios en el servidor.

* AEM **6.5 Jar de API de Java™ obsoleta**: un conjunto adicional de interfaces que se han eliminado desde la versión 6.5 de la aplicación de la versión de la aplicación de la versión de la aplicación de la versión de la versión
* **6.5 Javadoc Jar obsoleto**: el Javadoc para el conjunto adicional de interfaces

## Creación para el SDK {#building-for-the-sdk}

El SDK de AEM as a Cloud Service se utiliza para generar e implementar código personalizado. AEM Consulte la [documentación del tipo de archivo del proyecto de](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=es). En un nivel superior, se realizan los siguientes pasos:

* **Código de compilación**. Como se esperaba, el código fuente se compila y genera los paquetes de contenido resultantes
* **artefactos de compilación**. Los artefactos se crean durante este proceso
* **Analizar paquetes**. Los paquetes se analizan mediante el complemento Maven Analyzer, que busca problemas en el proyecto Maven como dependencias que faltan
* **Implementar artefactos**. Los artefactos se implementan en el servidor local.

Cloud Manager ejecuta los mismos pasos al implementar en entornos de nube. La realización de compilaciones localmente permite el desarrollo y las pruebas locales. Los desarrolladores pueden descubrir de forma eficaz los problemas estructurales o de código antes de comprometerse con el control de código fuente y activar las implementaciones de Cloud Manager, lo que puede tardar más.

>[!NOTE]
>
>El SDK de AEM as a Cloud Service debe crearse con una distribución y versión de Java compatibles con [entorno de compilación de Cloud Manager](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md). Es posible que los clientes de AEM as a Cloud Service descarguen el JDK de Oracle desde el [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-es/aemcloud.html) y tengan compatibilidad con Java 11 ampliada hasta septiembre de 2026 debido a los términos de licencia y compatibilidad de Adobe para la tecnología Java de Oracle cuando se utilice en proyectos de Adobe Experience Manager.

## Acceso al SDK de AEM as a Cloud Service {#accessing-the-aem-as-a-cloud-service-sdk}

* AEM Puede consultar el icono **Acerca de Adobe Experience Manager AEM** del Admin Console de la para saber la versión de la aplicación que está ejecutando en producción.
* Las herramientas quickstart de jar y Dispatcher se pueden descargar como archivo zip desde [Software Distribution portal](https://experience.adobe.com/#/downloads/content/software-distribution/es-es/aemcloud.html). AEM El acceso a los listados de SDK está limitado a las personas que tienen entornos en Managed Services o AEM as a Cloud Service de la manera más sencilla y eficaz.
* Java™ API Jar y Javadoc Jar se pueden descargar a través de herramientas de Maven, ya sea con la línea de comandos o con su IDE preferido.
* Los POM del proyecto de Maven deben hacer referencia al siguiente paquete JAR de API. También se debe hacer referencia a la dependencia de cualquier pom de subpaquete.

```
<dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>aem-sdk-api</artifactId>
  <version>2019.11.3006.20191108T223635Z-191201</version>
  <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>La entrada de versión para el SDK debe coincidir con la versión de AEM as a Cloud Service. AEM Para ver la versión que está utilizando, inicie sesión en el sitio de la aplicación de. En la esquina superior derecha de la pantalla, ve al signo de interrogación y selecciona **[!UICONTROL Acerca de Adobe Experience Manager]**.


## Actualizar un proyecto local con una nueva versión del SDK {#refreshing-a-local-project-with-a-new-skd-version}

¿Cuándo se recomienda actualizar el proyecto local con un nuevo SDK?

el Adobe *recomienda* actualizarlo después de una versión de mantenimiento mensual.

Es *opcional* actualizarlo después de cualquier versión de mantenimiento diaria. AEM Se informa a los clientes de cuando su instancia de producción se ha actualizado correctamente a una nueva versión de. En las versiones de mantenimiento diarias, no se espera que el nuevo SDK haya cambiado significativamente, si es que lo ha hecho. AEM Aun así, se recomienda actualizar ocasionalmente el entorno de desarrollador de la aplicación local con el SDK más reciente y, a continuación, volver a compilar y probar la aplicación personalizada. La versión de mantenimiento mensual suele incluir cambios más impactantes, por lo que los desarrolladores deben actualizarlos, reconstruirlos y probarlos inmediatamente.

A continuación se muestra el procedimiento recomendado para actualizar un entorno local:

1. Asegúrese de que cualquier contenido útil esté confirmado en el proyecto en el control de código fuente o disponible en un paquete de contenido mutable para su posterior importación.
1. El contenido de la prueba de desarrollo local debe almacenarse por separado para que no se implemente como parte de la compilación de la canalización de Cloud Manager. La razón es que solo se utiliza para el desarrollo local.
1. Detenga el inicio rápido que se está ejecutando.
1. Mueva la carpeta `crx-quickstart` a una carpeta diferente para mantenerla a salvo.
1. AEM Tenga en cuenta la nueva versión de la aplicación, que se indica en Cloud Manager (se utiliza para identificar la nueva versión de QuickStart Jar que se descargará más adelante).
1. AEM Descargue el JAR de QuickStart cuya versión coincida con la versión del de producción desde el Portal de distribución de software.
1. Cree una carpeta completamente nueva y coloque el nuevo Jar de inicio rápido dentro.
1. Inicie el nuevo Inicio rápido con los modos de ejecución deseados (cambiando el nombre de los archivos o pasando los modos de ejecución a través de `-r`).
   * Asegúrese de que no quede nada del inicio rápido antiguo en la carpeta.
1. AEM Cree la aplicación de la.
1. AEM AEM Implemente la aplicación de en el entorno local mediante el Administrador de paquetes.
1. Instale cualquier paquete de contenido mutable necesario para las pruebas del entorno local mediante el Administrador de paquetes.
1. Continúe el desarrollo e implemente los cambios según sea necesario.

AEM Si hay contenido que debe instalarse con cada nueva versión de inicio rápido de la aplicación, inclúyalo en un paquete de contenido y en el control de código fuente del proyecto. A continuación, instálelo cada vez.

Se recomienda actualizar el SDK con frecuencia (por ejemplo, cada dos semanas) y eliminar el estado local completo diariamente para no depender accidentalmente de los datos con estado en la aplicación.

AEM Si depende de CryptoSupport ([mediante la configuración de las credenciales de Cloud Services o del servicio de correo SMTP en el servicio de correo electrónico o mediante el uso de la API de CryptoSupport en su aplicación](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/crypto/CryptoSupport.html)), las propiedades cifradas se cifran con una clave. AEM Esta clave se genera automáticamente en el primer inicio de un entorno de. Aunque la configuración en la nube se encarga de reutilizar automáticamente la clave criptográfica específica del entorno, es necesario insertar la clave criptográfica en el entorno de desarrollo local.

AEM AEM De manera predeterminada, la configuración de los datos de clave está configurada para almacenar los datos clave dentro de la carpeta de datos de una carpeta, pero para facilitar su reutilización en el desarrollo, el proceso de se puede inicializar al iniciar por primera vez con &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. Este proceso genera los datos de cifrado en &quot;`/etc/key`&quot;.

Para poder reutilizar paquetes de contenido que contengan los valores cifrados, siga estos pasos:

* Cuando inicie inicialmente el archivo quickstart.jar local, asegúrese de agregar el siguiente parámetro: &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. Se recomienda, pero es opcional, agregarlo siempre.
* La primera vez que inició una instancia, cree un paquete que contenga un filtro para la raíz &quot;`/etc/key`&quot;. Este paquete contiene el secreto que se debe reutilizar en todos los entornos para los que desea reutilizarlos.
* Exporte cualquier contenido mutable que contenga secretos o busque los valores cifrados mediante `/crx/de` para poder agregarlo al paquete que se reutiliza en las instalaciones.
* Siempre que cree una nueva instancia (para reemplazarla por una nueva versión o como varios entornos de desarrollo deben compartir las credenciales para la prueba), instale el paquete producido en los pasos 2 y 3. Al hacerlo, puede reutilizar el contenido sin necesidad de volver a configurarlo manualmente. La razón es porque ahora la clave criptográfica está sincronizada.
