---
title: SDK de AEM as a Cloud Service
description: AEM Descripción general del Kit de desarrollo de software as a Cloud Service de la
exl-id: 06f3d5ee-440e-4cc5-877a-5038f9bd44c6
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 2%

---

# SDK de AEM as a Cloud Service {#aem-as-a-cloud-service-sdk}

AEM El SDK as a Cloud Service se compone de los siguientes artefactos:

* **Jar de inicio rápido** AEM - Tiempo de ejecución de la utilizado para el desarrollo local
* **Java™ API Jar** AEM : La dependencia Java™ Jar/Maven que expone todas las API de Java™ permitidas que se pueden utilizar para desarrollar frente a las as a Cloud Service de la. Anteriormente conocido como el Uberjar
* **Javadoc Jar** - Los javadocs para el jar de la API de Java™
* **Herramientas de Dispatcher** : conjunto de herramientas utilizadas para desarrollar con Dispatcher localmente. Separar artefactos para UNIX® y ventanas

AEM Además, algunos clientes que se implementaron anteriormente con la versión 6.5 o versiones anteriores de utilizan los artefactos que se muestran a continuación. AEM Si la compilación local no funciona con el JAR de inicio rápido y sospecha que se debe a la eliminación de interfaces del as a Cloud Service implementado, póngase en contacto con el servicio de atención al cliente. Pueden determinar si necesita acceso. Requiere cambios en el servidor.

* **6.5 Jar de API de Java™ obsoleta** AEM - un conjunto adicional de interfaces que se han eliminado desde la versión 6.5 de la aplicación de la versión de.
* **6.5 Javadoc Jar obsoleto** - el Javadocs para el conjunto adicional de interfaces

## Creación para el SDK {#building-for-the-sdk}

AEM El SDK as a Cloud Service de se utiliza para crear e implementar código personalizado. Consulte la [AEM Documentación del tipo de archivo del proyecto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=es). En un nivel superior, se realizan los siguientes pasos:

* **Compilar código**. Como se esperaba, el código fuente se compila y genera los paquetes de contenido resultantes
* **Generar artefactos**. Los artefactos se crean durante este proceso
* **Analizar paquetes**. Los paquetes se analizan mediante el complemento Maven Analyzer, que busca problemas en el proyecto Maven como dependencias que faltan
* **Implementar artefactos**. Los artefactos se implementan en el servidor local.

Cloud Manager ejecuta los mismos pasos al implementar en entornos de nube. La realización de compilaciones localmente permite el desarrollo y las pruebas locales. Los desarrolladores pueden descubrir de forma eficaz los problemas estructurales o de código antes de comprometerse con el control de código fuente y activar las implementaciones de Cloud Manager, lo que puede tardar más.

>[!NOTE]
>
>AEM El SDK as a Cloud Service debe crearse con una distribución y versión de Java admitidas por [Entorno de compilación de Cloud Manager](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md). AEM Los clientes as a Cloud Service pueden descargar el JDK de Oracle desde el [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-es/aemcloud.html) y tienen compatibilidad extendida con Java 11 hasta septiembre de 2026 debido a los términos de licencia y compatibilidad de Adobe para la tecnología Java de Oracle cuando se utiliza en proyectos de Adobe Experience Manager.

## AEM Acceso al SDK as a Cloud Service de {#accessing-the-aem-as-a-cloud-service-sdk}

* AEM Puede consultar el Admin Console de la **Acerca de Adobe Experience Manager** AEM para averiguar la versión de la aplicación que se está ejecutando en producción.
* Las herramientas quickstart de jar y Dispatcher se pueden descargar como archivo zip desde [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-es/aemcloud.html). AEM El acceso a los listados del SDK está limitado a las personas que tienen entornos en la Managed Services AEM as a Cloud Service o en la.
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
>AEM La entrada de versión para el SDK debe coincidir con la versión de as a Cloud Service de la. AEM Para ver la versión que está utilizando, inicie sesión en el sitio de la aplicación de. En la esquina superior derecha de la pantalla, vaya al signo de interrogación y seleccione **[!UICONTROL Acerca de Adobe Experience Manager]**.


## Actualizar un proyecto local con una nueva versión del SDK {#refreshing-a-local-project-with-a-new-skd-version}

¿Cuándo se recomienda actualizar el proyecto local con un nuevo SDK?

Adobe *recomienda* actualizarlo después de una versión de mantenimiento mensual.

Lo es *opcional* para actualizarlo después de cualquier versión de mantenimiento diaria. AEM Se informa a los clientes de cuando su instancia de producción se ha actualizado correctamente a una nueva versión de. En las versiones de mantenimiento diarias, no se espera que el nuevo SDK haya cambiado significativamente, si es que lo ha hecho. AEM Aun así, se recomienda actualizar ocasionalmente el entorno de desarrollador de la aplicación local con el SDK más reciente y, a continuación, volver a compilar y probar la aplicación personalizada. La versión de mantenimiento mensual suele incluir cambios más impactantes, por lo que los desarrolladores deben actualizarlos, reconstruirlos y probarlos inmediatamente.

A continuación se muestra el procedimiento recomendado para actualizar un entorno local:

1. Asegúrese de que cualquier contenido útil esté confirmado en el proyecto en el control de código fuente o disponible en un paquete de contenido mutable para su posterior importación.
1. El contenido de la prueba de desarrollo local debe almacenarse por separado para que no se implemente como parte de la generación de canalización de Cloud Manager. La razón es que solo se utiliza para el desarrollo local.
1. Detenga el inicio rápido que se está ejecutando.
1. Mover el `crx-quickstart` Carpeta de a una carpeta diferente para un mantenimiento seguro.
1. AEM Tenga en cuenta la nueva versión de la aplicación, que se indica en Cloud Manager (se utiliza para identificar la nueva versión de QuickStart Jar que se descargará más adelante).
1. AEM Descargue el JAR de QuickStart cuya versión coincida con la versión del de producción desde el Portal de distribución de software.
1. Cree una carpeta completamente nueva y coloque el nuevo Jar de inicio rápido dentro.
1. Inicie el nuevo QuickStart con los modos de ejecución deseados (ya sea cambiando el nombre de los archivos o pasando los modos de ejecución mediante `-r`).
   * Asegúrese de que no quede nada del inicio rápido antiguo en la carpeta.
1. AEM Cree la aplicación de la.
1. AEM AEM Implemente la aplicación de en el entorno local mediante el Administrador de paquetes.
1. Instale cualquier paquete de contenido mutable necesario para las pruebas del entorno local mediante el Administrador de paquetes.
1. Continúe el desarrollo e implemente los cambios según sea necesario.

AEM Si hay contenido que debe instalarse con cada nueva versión de inicio rápido de la aplicación, inclúyalo en un paquete de contenido y en el control de código fuente del proyecto. A continuación, instálelo cada vez.

Se recomienda actualizar el SDK con frecuencia (por ejemplo, cada dos semanas) y eliminar el estado local completo diariamente para no depender accidentalmente de los datos con estado en la aplicación.

Si depende de CryptoSupport ([AEM mediante la configuración de las credenciales de los servicios en la nube o el servicio de correo SMTP en la aplicación o utilizando la API de CryptoSupport en la aplicación](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/crypto/CryptoSupport.html)), las propiedades cifradas se cifran con una clave. AEM Esta clave se genera automáticamente en el primer inicio de un entorno de. Aunque la configuración en la nube se encarga de reutilizar automáticamente la clave criptográfica específica del entorno, es necesario insertar la clave criptográfica en el entorno de desarrollo local.

AEM AEM De forma predeterminada, la configuración de la almacena los datos clave dentro de la carpeta de datos de una carpeta, pero para facilitar su reutilización durante el desarrollo, el proceso de creación se puede inicializar al iniciar por primera vez con &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. Este proceso genera los datos de cifrado en &quot;`/etc/key`&quot;.

Para poder reutilizar paquetes de contenido que contengan los valores cifrados, siga estos pasos:

* Cuando inicie quickstart.jar local por primera vez, asegúrese de añadir el siguiente parámetro: &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. Se recomienda, pero es opcional, agregarlo siempre.
* La primera vez que inicie una instancia, cree un paquete que contenga un filtro para la raíz &quot;`/etc/key`&quot;. Este paquete contiene el secreto que se debe reutilizar en todos los entornos para los que desea reutilizarlos.
* Exporte cualquier contenido mutable que contenga secretos o busque los valores cifrados mediante `/crx/de` para poder agregarlo al paquete que se reutiliza en todas las instalaciones.
* Siempre que cree una nueva instancia (para reemplazarla por una nueva versión o como varios entornos de desarrollo deben compartir las credenciales para la prueba), instale el paquete producido en los pasos 2 y 3. Al hacerlo, puede reutilizar el contenido sin necesidad de volver a configurarlo manualmente. La razón es porque ahora la clave criptográfica está sincronizada.
