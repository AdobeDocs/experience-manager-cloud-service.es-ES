---
title: “Canal de prelanzamiento de [!DNL Adobe Experience Manager] as a Cloud Service”
description: “Canal de prelanzamiento de [!DNL Adobe Experience Manager] as a Cloud Service”
exl-id: cfc91699-0087-40fa-a76c-0e5e1e03a5bd
source-git-commit: c2f0b9c904374b5e59ce2b2f268fdd73dfdbfd21
workflow-type: ht
source-wordcount: '805'
ht-degree: 100%

---

# Canal de prelanzamiento de [!DNL Adobe Experience Manager] as a Cloud Service {#prerelease-channel}


## Introducción {#introduction}

[!DNL Adobe Experience Manager] as a Cloud Service ofrece nuevas funciones en una cadencia mensual, según la programación de la [hoja de ruta de publicaciones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es#aem-as-cloud-service). Para familiarizarse con las funciones programadas para entrar en funcionamiento el mes siguiente, los clientes pueden suscribirse al canal de prelanzamiento, al que se puede acceder configurando adecuadamente en entornos de desarrollo de programas estándar o en cualquier entorno de programa de zona protegida. Los clientes pueden obtener una vista previa de los cambios realizados en la consola de Sites, así como crear código para cualquier API de versión preliminar nueva.

La lista de funciones de prelanzamiento de un mes determinado se publica dentro de las [notas de la versión mensuales](/help/release-notes/release-notes-cloud/release-notes-current.md).

>[!VIDEO](/help/release-notes/assets/prerelease-overview.mp4)

## Activación de la versión preliminar {#enable-prerelease}

Las funciones de la versión preliminar se pueden experimentar de diferentes maneras:

* Entornos en la nube (entornos de desarrollo de programa estándar o cualquier tipo de entorno de programa de zona protegida)
* SDK local

### Entornos de la nube {#cloud-environments}

Para actualizar un entorno de Cloud para utilizar el prelanzamiento, agregue una nueva [variable de entorno](../implementing/cloud-manager/environment-variables.md) usando la interfaz de usuario de configuración de entorno en Cloud Manager:

1. Vaya al **Programa** > **Entorno** > **Configuración del entorno** que desea actualizar.
1. Agregar una nueva [variable de entorno](../implementing/cloud-manager/environment-variables.md):

   | Nombre | Value | Servicio aplicado | Tipo |
   |------|-------|-----------------|------|
   | `AEM_RELEASE_CHANNEL` | `prerelease` | Todos | Variable |

1. Guarde los cambios y el entorno se actualizará con las características de la versión preliminar activadas.

   ![Nueva variable de entorno](assets/env-configuration-prerelease.png)


**Alternativamente** puede utilizar la API y la CLI de Cloud Manager para actualizar las variables de entorno:

* Al usar el [punto de conexión de las variables de entorno de la API de Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/patchEnvironmentVariables), establezca la variable de entorno **AEM_RELEASE_CHANNEL** al valor **versión preliminar**.

   ```
   PATCH /program/{programId}/environment/{environmentId}/variables
   [
           {
                   "name" : "AEM_RELEASE_CHANNEL",
                   "value" : "prerelease",
                   "type" : "string"
           }
   ]
   ```

* También se puede utilizar la CLI de Cloud Manager, según las instrucciones indicadas en [https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid)

   ```aio cloudmanager:environment:set-variables <ENVIRONMENT_ID> --programId=<PROGRAM_ID> --variable AEM_RELEASE_CHANNEL “prerelease”```


La variable se puede eliminar o volver a establecerse en un valor diferente si desea que el entorno se restaure al comportamiento del canal normal (que no es de prelanzamiento).

### SDK local {#local-sdk}

Puede ver nuevas funciones en la consola de Sites en el Quickstart de SDK local y programar las nuevas API en la versión preliminar haciendo que su proyecto de Maven haga referencia a la versión preliminar `API Jar` situada en Maven Central. También puede ver estas características de la versión preliminar en el equipo local iniciando el SDK de Quickstart normal en modo de versión preliminar:

* Descargue el SDK desde el portal de distribución de software e instálelo tal como se describe en [Acceso al SDK de AEM as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).
* Al iniciar el Quickstart de SDK, incluya el argumento `-r prerelease`.
* El valor es *fijo*, por lo tanto, solo se puede seleccionar en el primer inicio. Vuelva a instalar el SDK para cambiar la opción de la línea de comandos.

Dado que puede haber varias versiones de mantenimiento de AEM entre las versiones de funciones mensuales, puede descargar estos nuevos SDK y hacer referencia a las nuevas versiones de JAR de API de SDK en proyectos en Maven. Las versiones de mantenimiento no añadirán funciones de versión preliminar adicionales, pero podrían incluir otros cambios más pequeños, como correcciones de errores, correcciones de seguridad y mejoras de rendimiento.
Los JavaDocs se publican en Maven Central.

Para compilar con el SDK de prelanzamiento:

1. Modifique el pom.xml de su proyecto de Maven para hacer referencia a un JAR de API de SDK de prelanzamiento distinto, que se publica en Maven central. Contiene cualquier nueva API de Java para las funciones de prelanzamiento y depende del JAR de la API del SDK. Utiliza la misma versión.

   Por ejemplo, a continuación se muestra un fragmento de la sección de administración de dependencias del POM principal que hace referencia al JAR de API normal:

   ```
   <dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>com.adobe.aem</groupId>
            <artifactId>aem-sdk-api</artifactId>
            <version>${aem.sdk.api}</version>
            <scope>provided</scope>
        </dependency>
   ```

   Y luego el uso en un módulo:

   ```
    <dependencies>
     <dependency>
         <groupId>com.adobe.aem</groupId>
         <artifactId>aem-sdk-api</artifactId>
     </dependency>
   ```

   Para cambiar al SDK de prelanzamiento, simplemente cambie la dependencia de `com.adobe.aem:aem-sdk-api` a `com.adobe.aem:aem-prerelease-sdk-api` como se indica a continuación:

   ```
   <dependencyManagement>
    <dependencies>
      <dependency>
            <groupId>com.adobe.aem</groupId>
            <artifactId>aem-prerelease-sdk-api</artifactId>
            <version>${aem.sdk.api}</version>
            <scope>provided</scope>
      </dependency>
   <dependencies>
      <dependency>
         <groupId>com.adobe.aem</groupId>
         <artifactId>aem-prerelease-sdk-api</artifactId>
      </dependency>
   ```

   Como de costumbre, los proyectos individuales pueden utilizar la dependencia.

1. Implementación en el servidor local
1. Si está seguro de que funciona como se espera localmente, confirme el código a una rama de desarrollo y utilice una canalización de no producción de Cloud Manager para implementar en un entorno que se suscriba al canal de prelanzamiento

>[!CAUTION]
> 
> El artifactId `aem-prerelease-sdk-api` nunca debe utilizarse al implementar en Ensayo o Producción. Utilice siempre aem-sdk-api al implementar mediante la canalización de producción. Del mismo modo, el código que hace referencia a las API de versión preliminar no debe implementarse mediante la canalización de producción.

El [plugin maven de AEM CS SDK build Analyzer v1.0 y superior](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=es#developing) detectará si la API de prelanzamiento se utiliza en un proyecto inspeccionando las dependencias. Si el analizador lo encuentra, utilizará la API del SDK de prelanzamiento para analizar el proyecto.

## Consideraciones {#considerations}

Hay algunas cosas que hay que tener en cuenta cuando se trata del canal de prelanzamiento:

* Es posible que algunas funciones que se implementarán en la versión del próximo mes no se incluyan en el canal de prelanzamiento.
* Las funciones de la versión preliminar se someten a rigurosas garantías de calidad y se pretende que sean características completas en lugar de calidad beta. Si nota algún problema, informe de él, tal como lo haría si sospechara que hay errores en las características de una versión de AEM normal.
* Para determinar si un entorno está configurado para el canal de prelanzamiento, vaya a la página **Acerca de** de la consola de AEM y compruebe si el número de versión de AEM incluye un sufijo de *versión preliminar* como ```Adobe Experience Manager 2021.4.5226.20210427T070726Z-210429-PRERELEASE```.

![acerca de](/help/release-notes/assets/about.png)
