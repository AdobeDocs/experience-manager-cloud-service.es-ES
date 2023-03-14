---
title: SDK de AEM as a Cloud Service
description: AEM Descripción general del Kit de desarrollo de software as a Cloud Service de la
exl-id: 06f3d5ee-440e-4cc5-877a-5038f9bd44c6
source-git-commit: c08e442e58a4ff36e89a213aa7b297b538ae3bab
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 2%

---

# SDK de AEM as a Cloud Service {#aem-as-a-cloud-service-sdk}

AEM El SDK as a Cloud Service consta de los siguientes artefactos:

* **Jar de inicio rápido** AEM - Tiempo de ejecución de la utilizado para el desarrollo local
* **Java API Jar** AEM : La dependencia de Java Jar/Maven que expone todas las API de Java permitidas que se pueden utilizar para desarrollar con las que se puede usar como Cloud Service de. Anteriormente conocido como el Uberjar
* **Javadoc Jar** - Los javadocs para el jar de la API de Java
* **Herramientas de Dispatcher** : conjunto de herramientas utilizadas para desarrollar con Dispatcher localmente. Artefactos independientes para Unix y Windows

AEM Además, algunos clientes que se implementaron anteriormente con la versión 6.5 o versiones anteriores de utilizarán los artefactos que se indican a continuación. AEM Si la compilación local no funciona con el JAR de inicio rápido y sospecha que se debe a interfaces que se han eliminado de los as a Cloud Service implementados de la implementación, póngase en contacto con Asistencia al cliente para determinar si necesita acceso. Esto requerirá cambios en el servidor.

* **6.5 Jar de API de Java en desuso** AEM - un conjunto adicional de interfaces que se han eliminado desde la versión 6.5 de la aplicación de la versión de la aplicación de
* **6.5 Javadoc Jar obsoleto** - el Javadocs para el conjunto adicional de interfaces

## Creación para el SDK {#building-for-the-sdk}

AEM El SDK as a Cloud Service de se utiliza para crear e implementar código personalizado. Para obtener más información, consulte la [AEM Documentación del tipo de archivo del proyecto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=es). En un nivel superior, se realizan los siguientes pasos:

* **Compilar código**. Como se esperaba, el código fuente se compila y genera los paquetes de contenido resultantes
* **Generar artefactos**. Los artefactos se crean durante este proceso
* **Analizar paquetes**. Los paquetes se analizan mediante el complemento Maven Analyzer, que busca problemas en el proyecto Maven como dependencias que faltan
* **Implementar artefactos**. Los artefactos se implementan en el servidor local.

Cloud Manager ejecuta los mismos pasos al implementar en entornos de nube. La realización de compilaciones localmente permite el desarrollo y las pruebas locales para que los desarrolladores puedan descubrir de forma eficaz los problemas estructurales o de código antes de comprometerse con el control de código fuente y activar las implementaciones de Cloud Manager, lo que puede tardar más.

## AEM Acceso al SDK as a Cloud Service de {#accessing-the-aem-as-a-cloud-service-sdk}

* AEM Puede consultar el Admin Console de la **Acerca de Adobe Experience Manager** AEM para averiguar la versión de la aplicación que se está ejecutando en producción.
* Las herramientas quickstart de jar y Dispatcher se pueden descargar como archivo zip desde [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-es/aemcloud.html). AEM Tenga en cuenta que el acceso a los listados de SDK está limitado a aquellos con entornos Managed Services AEM o as a Cloud Service de.
* Java API Jar y Javadoc Jar se pueden descargar a través de herramientas de Maven, ya sea con la línea de comandos o con su IDE preferido.
* Los POM del proyecto de Maven deben hacer referencia al siguiente paquete JAR de API. También se debe hacer referencia a esta dependencia en cualquier pom de subpaquete.

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
>AEM La entrada de versión para el SDK debe coincidir con la versión de as a Cloud Service de la. AEM Para ver la versión que está utilizando, inicie sesión en la página de inicio de sesión de, vaya al signo de interrogación en la esquina superior derecha de la pantalla y seleccione **[!UICONTROL Acerca de Adobe Experience Manager]**


## Actualizar un proyecto local con una nueva versión del SDK {#refreshing-a-local-project-with-a-new-skd-version}

¿Cuándo se recomienda actualizar el proyecto local con un nuevo SDK?

Lo es *recomendado* para actualizarlo al menos después de una versión de mantenimiento mensual.

Lo es *opcional* para actualizarlo después de cualquier versión de mantenimiento diaria. AEM Se informará a los clientes cuando su instancia de producción se haya actualizado correctamente a una nueva versión de la. En las versiones de mantenimiento diarias, no se espera que el nuevo SDK haya cambiado significativamente, si es que lo ha hecho. AEM Aun así, se recomienda actualizar ocasionalmente el entorno de desarrollador de la aplicación local con el SDK más reciente y, a continuación, volver a compilar y probar la aplicación personalizada. La versión de mantenimiento mensual generalmente incluye cambios más impactantes y, por lo tanto, los desarrolladores deben actualizar, reconstruir y probar inmediatamente.

A continuación se muestra el procedimiento recomendado para actualizar un entorno local:

1. Asegúrese de que cualquier contenido útil esté confirmado en el proyecto en el control de código fuente o disponible en un paquete de contenido mutable para su posterior importación
1. El contenido de la prueba de desarrollo local debe almacenarse por separado para que no se implemente como parte de la generación de canalización de Cloud Manager. Esto se debe a que solo necesita utilizarse para el desarrollo local
1. Detener el inicio rápido en ejecución
1. Mover el `crx-quickstart` Carpeta de a una carpeta diferente para un mantenimiento seguro
1. AEM Tenga en cuenta la nueva versión de la aplicación, que se indica en Cloud Manager (se utilizará para identificar la nueva versión de QuickStart Jar que se descargará más adelante)
1. AEM Descargue el JAR de QuickStart cuya versión coincida con la versión de la interfaz de usuario de producción desde el Portal de distribución de software
1. Cree una carpeta completamente nueva y coloque el nuevo Jar de inicio rápido en ella
1. Inicie el nuevo QuickStart con los modos de ejecución deseados (ya sea cambiando el nombre del archivo o pasando los modos de ejecución a través de `-r`).
   * Asegúrese de que no quede nada del inicio rápido antiguo en la carpeta.
1. AEM Creación de la aplicación de
1. AEM AEM Implemente la aplicación de en el entorno local mediante PackageManager
1. Instale cualquier paquete de contenido mutable necesario para las pruebas del entorno local mediante PackageManager
1. Continúe el desarrollo e implemente los cambios según sea necesario

AEM Si hay contenido que debe instalarse con cada nueva versión de inicio rápido de la aplicación, inclúyalo en un paquete de contenido y en el control de código fuente del proyecto. A continuación, instálelo cada vez.

Se recomienda actualizar el SDK con frecuencia (por ejemplo, cada dos semanas) y eliminar el estado local completo diariamente para no depender accidentalmente de los datos con estado en la aplicación.

En caso de que dependa de CryptoSupport ([AEM mediante la configuración de las credenciales de Cloud Services o el servicio de correo SMTP en la aplicación o utilizando la API de CryptoSupport en la aplicación.](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/crypto/CryptoSupport.html)AEM ), las propiedades cifradas se cifran con una clave que se genera automáticamente al primer inicio de un entorno de. Aunque la configuración de la nube se encarga de reutilizar automáticamente la clave criptográfica específica del entorno, es necesario insertar la clave criptográfica en el entorno de desarrollo local.

AEM AEM De forma predeterminada, la configuración está configurada para almacenar los datos clave dentro de la carpeta de datos de una carpeta, pero para facilitar la reutilización en el desarrollo, el proceso se puede inicializar al iniciar por primera vez con &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. Se generarán los datos de cifrado en &quot;`/etc/key`&quot;.

Para poder reutilizar paquetes de contenido que contengan los valores cifrados, debe seguir estos pasos:

* Cuando inicie quickstart.jar local por primera vez, asegúrese de añadir el siguiente parámetro: &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. Se recomienda, pero es opcional, agregarlo siempre.
* La primera vez que inició una instancia, cree un paquete que contenga un filtro para la raíz &quot;`/etc/key`&quot;. Esto mantendrá el secreto para reutilizarlo en todos los entornos para los que desee reutilizarlo
* Exporte cualquier contenido mutable que contenga secretos o busque los valores cifrados mediante `/crx/de` para añadirlo al paquete que se reutilizará en todas las instalaciones
* Siempre que cree una nueva instancia (para reemplazarla por una nueva versión o como varios entornos de desarrollo deben compartir las credenciales para realizar pruebas), instale el paquete producido en los pasos 2 y 3 para poder reutilizar el contenido sin necesidad de volver a configurarlo manualmente. Esto se debe a que ahora la clave criptográfica está sincronizada.
