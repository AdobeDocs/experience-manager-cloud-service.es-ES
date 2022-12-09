---
title: Canal de prelanzamiento de Adobe Experience Manager as a Cloud Service
description: Aprenda a utilizar el canal de prelanzamiento para obtener una vista previa de las próximas funciones AEM as a Cloud Service.
exl-id: cfc91699-0087-40fa-a76c-0e5e1e03a5bd
source-git-commit: 5b38e7d0ad97cdf8b7d0d5da79cf3d6721fa618a
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 25%

---


# Canal de prelanzamiento de Adobe Experience Manager as a Cloud Service {#prerelease-channel}

Aprenda a utilizar el canal de prelanzamiento para obtener una vista previa de las próximas funciones AEM as a Cloud Service.

## Introducción {#introduction}

Adobe Experience Manager as a Cloud Service ofrece nuevas funciones en una cadencia mensual, según la [Experience Manager publica la hoja de ruta.](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es#aem-as-cloud-service)

Para familiarizarse con las funciones programadas para entrar en funcionamiento el mes siguiente, puede suscribirse al canal de prelanzamiento, al que se puede acceder configurando los entornos de desarrollo o cualquier entorno de entorno limitado. Puede obtener una vista previa de los cambios accesibles a través de la interfaz de usuario de AEM, así como crear código con cualquier API de versión preliminar nueva.

La lista de funciones de prelanzamiento de un mes determinado se publica dentro de la [notas de la versión mensuales.](/help/release-notes/release-notes-cloud/release-notes-current.md)

## Versiones as a Cloud Service de AEM {#releases}

AEM as a Cloud Service tiene dos tipos de versiones.

* **Versiones mensuales** agregar funciones y características a AEM as a Cloud Service
* **Actualizaciones críticas** agregue actualizaciones de seguridad, mejoras de rendimiento y correcciones de errores, y se aplican diariamente.

Este patrón garantiza lanzamientos continuos sin interrupción del servicio.

El canal de prelanzamiento le permite obtener una vista previa de las funciones programadas para la próxima versión mensual para evaluar la funcionalidad futura y planificar su posible implementación para sus propios proyectos. Le permite planificar con antelación la próxima versión mensual.

Por ejemplo, si es mayo y está suscrito al canal de prelanzamiento, puede evaluar las funciones en la próxima versión de junio.

![Gráfico de cadencia previa al lanzamiento](assets/prerelease-cadence.png)

La versión previa le proporciona una ventana móvil de un mes sobre las próximas funciones de AEMaaCS, lo que le da tiempo de evaluar el impacto de cualquier función nueva en sus proyectos y personalizaciones, así como de planificar el despliegue de dichas funciones, pruebas y formación del usuario.

Para aprovechar al máximo el canal de prelanzamiento se requieren cuatro pasos.

1. [Marcar sus calendarios](#mark-calendars)
1. [Revise las notas de la versión](#release-notes)
1. [Acceder e probar las nuevas funciones](#new-features)
1. [Capacitar a los usuarios](#train-users)

## Marcar los calendarios {#mark-calendars}

Las versiones mensuales están programadas con mucha antelación y las fechas de lanzamiento se publican en [Adobe Experience League.](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html#aem-as-cloud-service)

Tenga en cuenta las fechas de lanzamiento para poder planificar el tiempo necesario para revisar y probar las próximas funciones.

## Consulte las notas de la versión {#release-notes}

Una vez que tenga las fechas de lanzamiento marcadas en el calendario, asegúrese de comprobar la variable [Adobe Experience League](/help/release-notes/release-notes-cloud/release-notes-current.md) sitio web el día de la versión para obtener las últimas notas de la versión.

Cada versión va acompañada de notas de la versión que documentan no solo las novedades de esa versión, sino también las funciones disponibles para la evaluación previa al lanzamiento. Aprenda con antelación y planifique aprovechar las últimas funciones de AEMaaCS.

También puede [comprobar los problemas conocidos](/help/release-notes/known-issues.md) que se publican junto con cada versión para que también pueda conocer cualquier problema técnico que pueda presentar un desafío para su evaluación o posible adopción de cualquier función nueva.

## Habilitar el canal de prelanzamiento para acceder y probar nuevas funciones {#new-features}

El canal de prelanzamiento se puede habilitar en cualquier entorno de desarrollo o simulación de pruebas. El prelanzamiento no se puede habilitar en entornos de ensayo o producción.

Las funciones de la versión preliminar se pueden experimentar de diferentes maneras:

* [Entornos en la nube](#cloud-environments)
* [SDK local](#local-sdk)

### Entornos de la nube {#cloud-environments}

Para actualizar un entorno de nube para utilizar el prelanzamiento, debe agregar una nueva variable de entorno. Puede hacerlo mediante la interfaz de usuario de Cloud Manager o mediante CLI.

#### Agregar variable de entorno mediante la interfaz de usuario {#add-with-ui}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Vaya al programa en el que desea habilitar la versión preliminar.

1. Seleccione el entorno en el que desea habilitar la versión preliminar y acceder a su configuración mediante **Programa** > **Entorno** > **Configuración del entorno**.

1. Agregar una nueva [variable de entorno:](../implementing/cloud-manager/environment-variables.md)

   | Nombre | Value | Servicio aplicado | Tipo |
   |------|-------|-----------------|------|
   | `AEM_RELEASE_CHANNEL` | `prerelease` | Todos | Variable |

1. Guarde los cambios y el entorno se actualizará con las características de la versión preliminar activadas.

   ![Nueva variable de entorno](assets/env-configuration-prerelease.png)

#### Agregar variable de entorno usando la CLI {#add-with-cli}

También puede utilizar la API y la CLI de Cloud Manager para actualizar las variables de entorno.

* Uso [Punto final de las variables de entorno de la API de Cloud Manager,](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/patchEnvironmentVariables) configure la variable `AEM_RELEASE_CHANNEL` variable de entorno al valor `prerelease`.

   ```text
   PATCH /program/{programId}/environment/{environmentId}/variables
   [
           {
                   "name" : "AEM_RELEASE_CHANNEL",
                   "value" : "prerelease",
                   "type" : "string"
           }
   ]
   ```

* [CLI de Cloud Manager](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) también se puede utilizar

   ```shell
   aio cloudmanager:environment:set-variables <ENVIRONMENT_ID> --programId=<PROGRAM_ID> --variable AEM_RELEASE_CHANNEL “prerelease
   ```

La variable se puede eliminar o volver a establecerse en un valor diferente si desea que el entorno se restaure al comportamiento del canal normal (que no es de prelanzamiento).

### SDK local {#local-sdk}

Puede ver nuevas funciones en la consola Sitios en el SDK local de inicio rápido y código con las nuevas API en la versión preliminar configurando el proyecto de Maven para que haga referencia a la versión previa `API Jar` situado en Maven Central. También puede ver estas funciones de la versión preliminar en su entorno de desarrollo local iniciando el SDK de inicio rápido normal en modo de versión preliminar.

#### Iniciar el SDK de inicio rápido en modo prelanzamiento {#prerelease-mode}

1. Descargue el SDK desde el portal de distribución de software e instálelo tal como se describe en [Acceso al SDK de AEM as a Cloud Service.](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
1. Al iniciar el Quickstart de SDK, incluya el argumento `-r prerelease`.

El valor es fijo, por lo tanto, solo se puede seleccionar en el primer inicio. Vuelva a instalar el SDK para cambiar la opción de la línea de comandos.

Dado que puede haber varias versiones de mantenimiento de AEM entre las versiones de funciones mensuales, puede descargar estos nuevos SDK y hacer referencia a las nuevas versiones de JAR de API de SDK en proyectos en Maven. Las versiones de mantenimiento no añadirán funciones de versión preliminar adicionales, pero podrían incluir otros cambios más pequeños, como correcciones de errores, correcciones de seguridad y mejoras de rendimiento.
Los JavaDocs se publican en Maven Central.

#### Generar con el SDK de prelanzamiento {#build-sdk}

1. Modifique el proyecto de maven `pom.xml` para hacer referencia a un jar de la API del SDK de la versión preliminar distinto, que se publica en Maven Central. Contiene cualquier nueva API de Java para las funciones de la versión preliminar y depende del jar de la API de SDK. Utiliza la misma versión.

   Por ejemplo, a continuación se muestra un fragmento de la sección de administración de dependencias del pom principal que hace referencia al jar de API normal:

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

1. Implementación en el servidor local.

1. Si está seguro de que funciona como se espera localmente, confirme el código a una rama de desarrollo y utilice una canalización de no producción de Cloud Manager para implementar en un entorno que se suscriba al canal de prelanzamiento.

>[!CAUTION]
> 
> La variable `aem-prerelease-sdk-api` artifactId nunca debe usarse al implementar en fase o producción. Utilice siempre la variable `aem-sdk-api` al implementar mediante la canalización de producción. Del mismo modo, el código que hace referencia a las API de prelanzamiento no debe implementarse mediante la canalización de producción.

La variable [AEM CS SDK build Analyzer maven plugin v1.0 y superior](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html#developing) detectará si la API de prelanzamiento se utiliza en un proyecto inspeccionando las dependencias. Si el analizador lo encuentra, utilizará la API del SDK de versión previa para analizar el proyecto.

## Capacitar a los usuarios {#train-users}

Una vez que haya probado las nuevas funciones en el canal de prelanzamiento y haya decidido aprovecharlas en sus proyectos, debe formar a los usuarios.

Adobe Experience League ofrece muchos recursos para aprender AEMaaCS.

* [La documentación de AEMaaCS](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=es)
* [Tutoriales](https://experienceleague.adobe.com/docs/experience-manager-learn/aem-tutorials/overview.html)
* [Vídeo de información general de la versión mensual](/help/release-notes/release-notes-cloud/release-notes-current.md#release-video) en las notas de la versión

## Consideraciones {#considerations}

Hay algunos elementos que se deben tener en cuenta al utilizar el canal de prelanzamiento.

* El canal de prelanzamiento no contiene necesariamente todas las nuevas funciones que se implementarán en la siguiente versión.
* Las funciones de la versión preliminar se someten a rigurosas garantías de calidad y se pretende que sean características completas en lugar de calidad beta. Si nota algún problema, informe de él, tal como lo haría si sospechara que hay errores en las características de una versión de AEM normal.
* Para determinar si un entorno está configurado para el canal de prelanzamiento, vaya a la consola de AEM **Acerca de** y compruebe si el número de versión AEM incluye un *versión preliminar* sufijo como ```Adobe Experience Manager 2021.4.5226.20210427T070726Z-210429-PRERELEASE```.

![Acerca de](/help/release-notes/assets/about.png)
