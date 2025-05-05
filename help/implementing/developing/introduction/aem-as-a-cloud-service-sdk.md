---
title: SDK de AEM as a Cloud Service
description: Descripción general del kit de desarrollo de software de AEM as a Cloud Service.
exl-id: 06f3d5ee-440e-4cc5-877a-5038f9bd44c6
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 82f5078740b2cf6ac481d83df40bbbc4fb3c1a77
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 1%

---

# SDK de AEM as a Cloud Service {#aem-as-a-cloud-service-sdk}

AEM as a Cloud Service SDK se compone de los siguientes artefactos:

* **Jar de inicio rápido**: tiempo de ejecución de AEM utilizado para el desarrollo local.
* **Jar de API de Java™**: la dependencia Java™ Jar/Maven que expone todas las API de Java™ permitidas que se pueden usar para desarrollar con AEM as a Cloud Service. Anteriormente conocido como el Uberjar.
* **Jar Javadoc**: los documentos Java para el Jar de la API Java™.
* **Herramientas de Dispatcher**: conjunto de herramientas utilizadas para desarrollar Dispatcher localmente. Separe los artefactos para UNIX® y ventanas.

Además, algunos clientes que se implementaron anteriormente con AEM 6.5 o versiones anteriores utilizan los artefactos siguientes. Si la compilación local no funciona con el Jar de inicio rápido y sospecha que se debe a la eliminación de interfaces del as a Cloud Service implementado por AEM, póngase en contacto con el servicio de atención al cliente. Pueden determinar si necesita acceso. Requiere cambios en el servidor.

* **6.5 Jar de API de Java™ obsoleta**: un conjunto adicional de interfaces que se han eliminado desde AEM 6.5.
* **6.5 Javadoc Jar obsoleto**: los documentos Java para el conjunto adicional de interfaces.

>[!NOTE]
> 
> Hay diferencias entre AEM as a Cloud Service y SDK en una serie de áreas diferentes. Para situaciones en las que se necesitan cambios rápidos e iterativos, Adobe ha introducido entornos de desarrollo rápido. Eche un vistazo a [Entornos de desarrollo rápido](/help/implementing/developing/introduction/rapid-development-environments.md) para obtener más información.

## Creación para SDK {#building-for-the-sdk}

AEM as a Cloud Service SDK se utiliza para generar e implementar código personalizado. Consulte la [documentación del tipo de archivo del proyecto AEM](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/developing/archetype/using). En un nivel superior, se realizan los siguientes pasos:

* **Código de compilación**: el código Source se ha compilado, lo que genera los paquetes de contenido resultantes.
* **Artefactos de compilación**: los artefactos se crean durante este proceso.
* **Analizar paquetes**: los paquetes se analizan con el complemento Maven Analyzer, que busca problemas en el proyecto Maven, como la falta de dependencias.
* **Implementar artefactos**: los artefactos se implementan en el servidor local.

Cloud Manager ejecuta los mismos pasos al implementar en entornos de nube. La realización de compilaciones localmente permite el desarrollo y las pruebas locales. Los desarrolladores pueden identificar de forma eficaz los problemas estructurales o de código antes de comprometerse con el control de código fuente. Este proceso ayuda a evitar los retrasos causados por la activación de implementaciones de Cloud Manager, que pueden tardar más.

>[!NOTE]
>
>AEM as a Cloud Service SDK debe generarse con una distribución y versión de Java compatibles con [entorno de compilación de Cloud Manager](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md). Los clientes de AEM as a Cloud Service pueden descargar el JDK de Oracle desde [Software Distribution portal](https://experience.adobe.com/#/downloads/content/software-distribution/es-es/aemcloud.html). Tienen compatibilidad ampliada con Java 11 hasta septiembre de 2026 debido a los términos de licencia y compatibilidad de Adobe para la tecnología Java de Oracle en proyectos de Adobe Experience Manager.

## Acceso a AEM as a Cloud Service SDK {#accessing-the-aem-as-a-cloud-service-sdk}

* Puede consultar el icono de AEM Admin Console **Acerca de Adobe Experience Manager** para saber la versión de AEM que está ejecutando en producción.
* QuickStart Jar y Dispatcher Tools se pueden descargar como archivo zip desde [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-es/aemcloud.html). El acceso a los listados de SDK está limitado a las personas que tienen entornos en AEM Managed Services o AEM as a Cloud Service.
* Java™ API Jar y Javadoc Jar se pueden descargar a través de la herramienta Maven, ya sea con la línea de comandos o con su IDE preferido.
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
>La entrada de versión para SDK debe coincidir con la versión de AEM as a Cloud Service. Para ver la versión que está utilizando, inicie sesión en AEM. En la esquina superior derecha de la pantalla, ve al signo de interrogación y haz clic en **[!UICONTROL Acerca de Adobe Experience Manager]**.


## Actualizar un proyecto local con una nueva versión de SDK {#refreshing-a-local-project-with-a-new-skd-version}

¿Cuándo se recomienda actualizar el proyecto local con un nuevo SDK?

Adobe *recomienda* actualizarlo después de una versión de mantenimiento mensual.

Es *opcional* actualizarlo después de cualquier versión de mantenimiento diaria. Se informa a los clientes de cuando su instancia de producción se ha actualizado correctamente a una nueva versión de AEM. En las versiones de mantenimiento diarias, no se espera que la nueva SDK haya cambiado significativamente, si es que lo ha hecho. Sin embargo, Adobe recomienda actualizar ocasionalmente el entorno de desarrollo local de AEM con la última versión de SDK y, a continuación, volver a compilar y probar la aplicación personalizada. La versión de mantenimiento mensual suele incluir cambios más impactantes, por lo que los desarrolladores deben actualizarlos, reconstruirlos y probarlos inmediatamente.

**Para actualizar un proyecto local con una nueva versión de SDK:**

1. Asegúrese de que todo el contenido útil está comprometido con el control de código fuente. O bien, se almacenan en un paquete de contenido mutable para su importación posterior.
1. El contenido de la prueba de desarrollo local debe almacenarse por separado para que no se implemente como parte de la compilación de la canalización de Cloud Manager. La razón es que solo se utiliza para el desarrollo local.
1. Detenga el inicio rápido que se está ejecutando.
1. Mueva la carpeta `crx-quickstart` a una carpeta diferente para mantenerla a salvo.
1. Tenga en cuenta la nueva versión de AEM, que se indica en Cloud Manager (se utiliza para identificar la nueva versión de QuickStart Jar que se descargará más adelante).
1. Descargue QuickStart Jar cuya versión coincida con la versión de Production AEM desde el Portal de distribución de software.
1. Cree una carpeta completamente nueva y coloque el nuevo Jar de inicio rápido dentro.
1. Inicie el nuevo Inicio rápido con los modos de ejecución deseados (cambiando el nombre de los archivos o pasando los modos de ejecución a través de `-r`).
Asegúrese de que no quede nada del inicio rápido antiguo en la carpeta.
1. Genere la aplicación de AEM.
1. Implemente la aplicación de AEM en el AEM local mediante el Administrador de paquetes.
1. Instale cualquier paquete de contenido mutable necesario para las pruebas del entorno local mediante el Administrador de paquetes.
1. Continúe el desarrollo e implemente los cambios según sea necesario.

Si hay contenido que debería instalarse con cada nueva versión de inicio rápido de AEM, inclúyalo en un paquete de contenido y en el control de código fuente del proyecto. A continuación, instálelo cada vez.

Adobe recomienda actualizar SDK con frecuencia, por ejemplo, cada dos semanas. Además, deseche el estado local completo diariamente para que no dependa accidentalmente de datos con estado en la aplicación.

Si utiliza CryptoSupport para servicios en la nube, la configuración de correo SMTP o la API de CryptoSupport, las propiedades cifradas se protegen con una clave. Encontrará más detalles en la [documentación de la API de CryptoSupport](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/crypto/CryptoSupport.html). Esta clave se genera automáticamente al primer inicio de un entorno de AEM. Aunque la configuración en la nube se encarga de reutilizar automáticamente la clave criptográfica específica del entorno, es necesario insertar la clave criptográfica en el entorno de desarrollo local.

De forma predeterminada, AEM está configurado para almacenar los datos clave dentro de la carpeta de datos de una carpeta, pero para facilitar su reutilización en desarrollo, el proceso de AEM se puede inicializar al iniciar por primera vez con &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. Este proceso genera los datos de cifrado en &quot;`/etc/key`&quot;.

**Para reutilizar paquetes de contenido que contengan los valores cifrados:**

* Cuando inicie inicialmente el archivo quickstart.jar local, asegúrese de agregar el siguiente parámetro: &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. Adobe recomienda, de forma opcional, que siempre lo añada.
* La primera vez que inició una instancia, cree un paquete que contenga un filtro para la raíz &quot;`/etc/key`&quot;. Este paquete contiene el secreto que se debe reutilizar en todos los entornos para los que desea reutilizarlos.
* Exporte cualquier contenido mutable que contenga secretos. O bien, busque los valores cifrados mediante `/crx/de` para poder agregarlos al paquete que se reutiliza en todas las instalaciones.
* Siempre que cree una nueva instancia (para reemplazarla por una nueva versión o como varios entornos de desarrollo deben compartir las credenciales para la prueba), instale el paquete producido en los pasos 2 y 3. Al hacerlo, puede reutilizar el contenido sin necesidad de volver a configurarlo manualmente. La razón es porque ahora la clave criptográfica está sincronizada.

