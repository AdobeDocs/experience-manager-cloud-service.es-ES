---
title: AEM como SDK de servicio de nube
description: 'Para completar '
translation-type: tm+mt
source-git-commit: a7dc007230632bf8343004794b2bc4c5baaf4e05

---


# AEM como SDK de servicio de nube {#aem-as-a-cloud-service-sdk}

El SDK de AEM como servicio de nube está compuesto por los siguientes artefactos:

* **Jar** de inicio rápido: tiempo de ejecución de AEM utilizado para el desarrollo local
* **Java API Jar** : la dependencia Java Jar/Maven que expone todas las API de Java permitidas que se pueden usar para desarrollarse con AEM como servicio de nube. Anteriormente denominado Uberjar
* **Javadoc Jar** - Los javadocs para Java API Jar
* **Herramientas** de despachante: conjunto de herramientas utilizadas para desarrollar con Dispatcher localmente. Objetos independientes para unix y ventanas

Además, algunos clientes que se implementaron previamente con AEM 6.5 o versiones anteriores utilizarán los artefactos siguientes. Si la compilación local no funciona con el tarro de inicio rápido y sospecha que se debe a interfaces que se han eliminado de AEM implementadas como servicio de nube, póngase en contacto con el servicio de asistencia al cliente para determinar si necesita acceso. Esto requerirá cambios en el servidor.

* **6.5 Java API Jar** , un conjunto adicional de interfaces que se han eliminado desde AEM 6.5
* **6.5 Javadoc Jar** desaprobado: los javadocs para el conjunto adicional de interfaces

## Acceso a AEM como SDK de servicio de nube {#accessing-the-aem-as-a-cloud-service-sdk}

* Puede consultar el icono **Acerca de Adobe Experience Manager** de AEM Admin Console para conocer la versión de AEM que está ejecutando en producción.
* El archivo jar y Dispatcher Tools de inicio rápido se pueden descargar como archivo zip desde el portal [de distribución de](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html)software. Tenga en cuenta que el acceso a los listados de SDK está limitado a los que tienen AEM Managed Services o AEM como entornos de servicio de nube.
* El Jar de la API de Java y Javadoc Jar se pueden descargar mediante herramientas muevas, ya sea con la línea de comandos o con su IDE preferido.
* Las páginas de proyecto principales deben hacer referencia al siguiente paquete de Jar de API. Esta dependencia también se debe hacer referencia a ella en cualquier página de subpaquete.

```
<dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>aem-sdk-api</artifactId>
  <version>2019.11.3006.20191108T223635Z-191201</version> 
  <scope>provided</scope>
</dependency>
```

> [!NOTE] La entrada de versión del SDK debe coincidir con la versión de AEM como un servicio de nube. Para ver qué versión utiliza, inicie sesión en AEM y, a continuación, vaya al signo de interrogación en la esquina superior derecha de la pantalla y seleccione **[!UICONTROL Acerca de Adobe Experience Manager]**

* La coordenada remota del repositorio principal en el que se aloja el paquete debe incluirse en el archivo pom.

```
<repository>
    <id>adobe-aem-releases</id>
    <name>Adobe AEM Repository</name>
    <url>https://downloads.experiencecloud.adobe.com/content/maven/public</url>
    <releases>
        <enabled>true</enabled>
        <updatePolicy>never</updatePolicy>
    </releases>
    <snapshots>
        <enabled>false</enabled>
    </snapshots>
</repository>
```

## Actualización de un proyecto local con una nueva versión del SDK {#refreshing-a-local-prokect-with-a-new-skd-version}

¿Cuándo se recomienda actualizar el proyecto local con un nuevo SDK?

Se *recomienda* actualizarla al menos después de una versión de mantenimiento mensual.

Es *opcional* actualizarla después de cualquier revisión de mantenimiento diaria. Se informará a los clientes cuando su instancia de producción se haya actualizado correctamente a una nueva versión de AEM. Para las versiones de mantenimiento diarias, no se espera que el nuevo SDK haya cambiado significativamente, si es que ha cambiado. Sin embargo, se recomienda actualizar ocasionalmente el entorno de desarrollador de AEM local con el SDK más reciente y, a continuación, volver a compilar y probar la aplicación personalizada. La versión de mantenimiento mensual generalmente incluye cambios más impactantes y, por lo tanto, los desarrolladores deben actualizar, reconstruir y probar inmediatamente.

A continuación se muestra el procedimiento recomendado para actualizar un entorno local:

1. Asegúrese de que cualquier contenido útil esté comprometido con el proyecto en el control de código fuente o disponible en un paquete de contenido mutable para su posterior importación
1. El contenido de la prueba de desarrollo local debe almacenarse por separado para que no se implemente como parte de la compilación del flujo de Cloud Manager. Esto se debe a que sólo se debe usar para el desarrollo local
1. Detener el inicio rápido que se está ejecutando
1. Mover la `crx-quickstart` carpeta a otra carpeta para protegerla
1. Tenga en cuenta la nueva versión de AEM, que se indica en Cloud Manager (esto se utilizará para identificar la nueva versión de Jar de QuickStart para seguir descargándola)
1. Descargue el JAR de inicio rápido cuya versión coincida con la versión de AEM de producción desde el portal de distribución de software
1. Cree una nueva carpeta y coloque la nueva barra de inicio rápido dentro
1. Inicie el nuevo inicio rápido con los modos de ejecución deseados (ya sea cambiando el nombre del archivo o pasando los modos de ejecución a través de `-r`).
   * Asegúrese de que no quede nada del inicio rápido anterior en la carpeta.
1. Cree su aplicación de AEM
1. Implementar la aplicación de AEM en AEM local mediante PackageManager
1. Instale los paquetes de contenido mutable necesarios para las pruebas del entorno local mediante PackageManager
1. Continúe con el desarrollo e implemente los cambios según sea necesario

Si hay contenido que debe instalarse con cada nueva versión de inicio rápido de AEM, inclúyalo en un paquete de contenido y en el control de código fuente del proyecto. A continuación, instálela cada vez.

La recomendación es actualizar el SDK con frecuencia (por ejemplo, cada dos semanas) y disponer de un estado local completo todos los días para no depender accidentalmente de los datos de estado de la aplicación.

En caso de que dependa de CryptoSupport ([ya sea configurando las credenciales de Cloudservices o el servicio de correo SMTP en AEM o utilizando la API de CryptoSupport en la aplicación](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/crypto/CryptoSupport.html)), las propiedades cifradas se cifrarán con una clave que se genere automáticamente en el primer inicio de un entorno AEM. Aunque la configuración de nube se encarga de reutilizar automáticamente la CryptoKey específica del entorno, es necesario inyectar la criptoclave en el entorno de desarrollo local.

De forma predeterminada, AEM está configurado para almacenar los datos clave en la carpeta de datos de una carpeta, pero para facilitar su reutilización en el desarrollo, el proceso de AEM se puede inicializar al iniciar por primera vez con &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. Esto generará los datos de cifrado en &quot;`/etc/key`&quot;.

Para poder reutilizar paquetes de contenido que contengan los valores cifrados, debe seguir estos pasos:

* Cuando inicialmente inicie el archivo local quickstart.jar, asegúrese de agregar el parámetro siguiente: &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. Se recomienda, pero es opcional, agregarla siempre.
* La primera vez que inició una instancia, cree un paquete que contenga un filtro para la raíz &quot;`/etc/key`&quot;. Esto mantendrá el secreto para que se vuelva a utilizar en todos los entornos para los que desea que se reutilicen
* Exporte cualquier contenido mutable que contenga secretos o busque los valores cifrados mediante `/crx/de` para agregarlo al paquete que se reutilizará en las instalaciones
* Siempre que gire una instancia nueva (ya sea para reemplazarla con una nueva versión o cuando varios entornos de desarrollo deban compartir las credenciales para la prueba), instale el paquete producido en los pasos 2 y 3 para poder reutilizar el contenido sin necesidad de volver a configurarlo manualmente. Esto se debe a que ahora la criptoclave está sincronizada.