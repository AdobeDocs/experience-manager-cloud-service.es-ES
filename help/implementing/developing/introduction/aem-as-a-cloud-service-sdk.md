---
title: SDK de AEM as a Cloud Service
description: Información general sobre el Kit de desarrollo de software as a Cloud Service de AEM
exl-id: 06f3d5ee-440e-4cc5-877a-5038f9bd44c6
source-git-commit: c08e442e58a4ff36e89a213aa7b297b538ae3bab
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 1%

---

# El SDK as a Cloud Service AEM {#aem-as-a-cloud-service-sdk}

El SDK as a Cloud Service AEM consta de los siguientes artefactos:

* **Jar de inicio rápido** - El tiempo de ejecución de AEM utilizado para el desarrollo local
* **Java API Jar** - La dependencia Java Jar/Maven que expone todas las API de Java permitidas que se pueden usar para desarrollar con AEM como Cloud Service. Anteriormente denominado Uberjar
* **Javadoc Jar** - Los javadocs para el Jar de API de Java
* **Herramientas de Dispatcher** - El conjunto de herramientas utilizadas para desarrollar con Dispatcher localmente. Dispositivos separados para unix y windows

Además, algunos clientes que se hayan implementado anteriormente con AEM 6.5 o versiones anteriores utilizarán los artefactos siguientes. Si la compilación local no funciona con el jar de inicio rápido y cree que se debe a interfaces que se han eliminado de AEM implementadas as a Cloud Service, póngase en contacto con el Servicio de atención al cliente para determinar si necesita acceso. Esto requerirá cambios en el servidor.

* **6.5 Jar de API Java obsoleto** - un conjunto adicional de interfaces que se han eliminado desde AEM 6.5
* **Javadoc Jar obsoleto 6.5** - los Javadocs para el conjunto adicional de interfaces

## Creación para el SDK {#building-for-the-sdk}

El SDK as a Cloud Service AEM se utiliza para crear e implementar código personalizado. Para obtener más información, consulte [Documentación del tipo de archivo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en). En un nivel superior, se realizan los siguientes pasos:

* **Compilar código**. Como se espera, el código fuente se compila, generando los paquetes de contenido resultantes
* **Creación de artefactos**. Los artefactos se crean durante este proceso
* **Analizar paquetes**. Los paquetes se analizan mediante el complemento Maven analyzer , que busca problemas en el proyecto Maven, como dependencias que faltan
* **Implementar artefactos**. Los artefactos se implementan en el servidor local.

Cloud Manager ejecuta los mismos pasos al implementar en entornos de Cloud. La realización de compilaciones localmente permite el desarrollo local y las pruebas para que los desarrolladores puedan descubrir de forma eficaz los problemas estructurales o de código antes de comprometerse con el control de código fuente y activar las implementaciones de Cloud Manager, que pueden tardar más.

## Acceso al SDK as a Cloud Service AEM {#accessing-the-aem-as-a-cloud-service-sdk}

* Puede comprobar el Admin Console de AEM **Acerca de Adobe Experience Manager** para conocer la versión de AEM que está ejecutando en producción.
* El jar de inicio rápido y las herramientas de Dispatcher se pueden descargar como archivo zip desde el [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-es/aemcloud.html). Tenga en cuenta que el acceso a las listas de SDK está limitado a aquellos que tengan AEM Managed Services o AEM entornos as a Cloud Service.
* El Jar de la API Java y Javadoc Jar se pueden descargar a través de herramientas maven, ya sea con la línea de comandos o con su IDE preferido.
* Las páginas del proyecto maven deben hacer referencia al siguiente paquete Jar de API. También se debe hacer referencia a esta dependencia en cualquier poms de subpaquete.

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
>La entrada de versión del SDK debe coincidir con la versión de AEM as a Cloud Service. Para ver qué versión utiliza, inicie sesión en AEM, vaya al signo de interrogación en la esquina superior derecha de la pantalla y seleccione **[!UICONTROL Acerca de Adobe Experience Manager]**


## Actualización de un proyecto local con una nueva versión del SDK {#refreshing-a-local-project-with-a-new-skd-version}

¿Cuándo se recomienda actualizar el proyecto local con un nuevo SDK?

Es *recomendado* para actualizarlo al menos después de una versión de mantenimiento mensual.

Es *opcional* para actualizarlo después de cualquier versión de mantenimiento diaria. Se informará a los clientes cuando su instancia de producción se haya actualizado correctamente a una nueva versión de AEM. En las revisiones de mantenimiento diarias, no se espera que el nuevo SDK haya cambiado significativamente, si es que lo ha hecho. Sin embargo, se recomienda actualizar ocasionalmente el entorno de desarrollador de AEM local con el SDK más reciente y, a continuación, reconstruir y probar la aplicación personalizada. La versión de mantenimiento mensual normalmente incluirá cambios más impactantes y, por lo tanto, los desarrolladores deben actualizar, reconstruir y probar inmediatamente.

A continuación se muestra el procedimiento recomendado para actualizar un entorno local:

1. Asegúrese de que cualquier contenido útil esté comprometido con el proyecto en el control de código fuente o esté disponible en un paquete de contenido mutable para su importación posterior
1. El contenido de la prueba de desarrollo local debe almacenarse por separado para que no se implemente como parte de la compilación de canalización de Cloud Manager. Esto se debe a que solo necesita utilizarse para el desarrollo local
1. Detener el inicio rápido que se está ejecutando
1. Mover el `crx-quickstart` carpeta a una carpeta diferente para un mantenimiento seguro
1. Tenga en cuenta la nueva versión de AEM, que se indica en Cloud Manager (se utilizará para identificar la nueva versión de Jar de inicio rápido para descargar más adelante)
1. Descargue el JAR de inicio rápido cuya versión coincida con la versión de AEM de producción del portal de distribución de software
1. Cree una nueva carpeta y coloque el nuevo Jar de inicio rápido dentro de
1. Inicie el nuevo QuickStart con los modos de ejecución deseados (cambiar el nombre del archivo o pasar los modos de ejecución mediante `-r`).
   * Asegúrese de que no quede nada del antiguo inicio rápido en la carpeta.
1. Cree su aplicación AEM
1. Implemente la aplicación AEM en la AEM local mediante PackageManager
1. Instale los paquetes de contenido mutable necesarios para las pruebas de entorno local mediante PackageManager
1. Continúe con el desarrollo e implemente los cambios según sea necesario

Si hay contenido que debe instalarse con cada nueva versión AEM inicio rápido, inclúyalo en un paquete de contenido y en el control de código fuente del proyecto. A continuación, instálelo cada vez.

La recomendación es actualizar el SDK con frecuencia (por ejemplo, cada dos semanas) y disponer diariamente el estado local completo para que no dependa accidentalmente de los datos de estado de la aplicación.

En caso de que dependa de CryptoSupport ([bien configurando las credenciales de Cloudservices o el servicio de correo SMTP en AEM o utilizando la API CryptoSupport en la aplicación](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/crypto/CryptoSupport.html)), las propiedades cifradas se cifrarán con una clave que se genere automáticamente al primer inicio de un entorno de AEM. Aunque cloudsetup se encarga de reutilizar automáticamente la CryptoKey específica del entorno, es necesario introducir la criptoclave en el entorno de desarrollo local.

De forma predeterminada, AEM está configurado para almacenar los datos clave dentro de la carpeta de datos de una carpeta, pero para facilitar la reutilización en el desarrollo, el proceso de AEM se puede inicializar en el primer inicio con &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. Esto generará los datos de cifrado en &quot;`/etc/key`&quot;.

Para poder reutilizar paquetes de contenido que contengan los valores cifrados, debe seguir estos pasos:

* Cuando inicie el archivo local quickstart.jar, asegúrese de agregar el siguiente parámetro: &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. Se recomienda, pero opcional, añadirlo siempre.
* La primera vez que inició una instancia, cree un paquete que contenga un filtro para la raíz &quot;`/etc/key`&quot;. Esto mantendrá el secreto para que se reutilice en todos los entornos para los que desea que se reutilicen
* Exporte cualquier contenido mutable que contenga secretos o busque los valores cifrados mediante `/crx/de` para añadirlo al paquete que se reutilizará en todas las instalaciones
* Siempre que gire una instancia nueva (para reemplazarla con una versión nueva o ya que varios entornos de desarrollo deben compartir las credenciales para la prueba), instale el paquete producido en los pasos 2 y 3 para poder reutilizar el contenido sin necesidad de reconfigurar manualmente. Esto se debe a que ahora la criptoclave está sincronizada.
