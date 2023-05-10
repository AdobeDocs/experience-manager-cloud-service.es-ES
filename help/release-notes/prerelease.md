---
title: Canal de la versión preliminar de Adobe Experience Manager as a Cloud Service
description: Aprenda a utilizar el canal de la versión preliminar para obtener una vista previa de las próximas funciones de AEM as a Cloud Service.
exl-id: cfc91699-0087-40fa-a76c-0e5e1e03a5bd
source-git-commit: a66814c0f7f8dbdf794ff1867c7a4d7fdc2956cf
workflow-type: ht
source-wordcount: '1311'
ht-degree: 100%

---


# Canal de la versión preliminar de Adobe Experience Manager as a Cloud Service {#prerelease-channel}

Aprenda a utilizar el canal de la versión preliminar para obtener una vista previa de las próximas funciones de AEM as a Cloud Service.

## Introducción {#introduction}

Adobe Experience Manager as a Cloud Service ofrece nuevas funciones con regularidad, según la [Hoja de ruta de versiones de Experience Manager.](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es#aem-as-cloud-service)

Para familiarizarse con las funciones programadas para entrar en funcionamiento en la siguiente versión de funciones, puede suscribirse al canal de la versión preliminar, al que puede acceder configurando sus entornos de desarrollo o de zona protegida. Puede previsualizar los cambios accesibles a través de la IU de AEM, así como crear código con cualquier API de versión preliminar nueva.

La lista de funciones de la versión preliminar de una determinada versión se publica en las [notas de la versión.](/help/release-notes/release-notes-cloud/release-notes-current.md)

## Versiones de AEM as a Cloud Service {#releases}

AEM as a Cloud Service tiene dos tipos de versiones.

* Las **versiones de funciones** agregan funcionalidades y características a AEM as a Cloud Service, previa activación.
* Las **versiones de mantenimiento** añaden actualizaciones de seguridad, mejoras de rendimiento y correcciones de errores, y se aplican de forma regular y frecuente.

Este modelo garantiza lanzamientos continuos sin interrupción del servicio.

El canal de la versión preliminar le permite previsualizar las funciones programadas para la próxima versión a fin de evaluar la funcionalidad futura y planificar su posible implementación en sus proyectos. Le permite planificar con antelación la próxima versión de funciones.

Por ejemplo, si es mayo y está suscrito al canal de la versión preliminar, puede evaluar las funciones de la próxima versión de junio.

![Gráfico de cadencia de la versión preliminar](assets/prerelease-cadence.png)

La versión preliminar le proporciona una ventana móvil de un mes sobre las próximas funciones de AEMaaCS, lo que le da tiempo de evaluar el impacto de cualquier nueva función en sus proyectos y personalizaciones, así como de planificar el despliegue de dichas funciones, pruebas y formación del usuario.

Para aprovechar al máximo el canal de la versión preliminar se requieren cuatro pasos.

1. [Marcado de calendarios](#mark-calendars)
1. [Revisión de las notas de la versión](#release-notes)
1. [Acceso y prueba de las nuevas funciones](#new-features)
1. [Formación de los usuarios](#train-users)

## Marcado de calendarios {#mark-calendars}

Las versiones de funciones se programan con mucha antelación y las fechas de activación de las mismas se publican en [Adobe Experience League.](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es#aem-as-cloud-service)

Tenga en cuenta las fechas de lanzamiento para planificar el tiempo necesario para revisar y probar las próximas funciones.

## Revisión de las notas de la versión {#release-notes}

Una vez que tenga las fechas de lanzamiento marcadas en el calendario, asegúrese de comprobar el sitio web de [Adobe Experience League](/help/release-notes/release-notes-cloud/release-notes-current.md) el día correspondiente para obtener las últimas notas de la versión.

Cada versión va acompañada de notas de la versión que documentan no solo las novedades, sino también las funciones disponibles para la evaluación de la versión preliminar. Infórmese con antelación y planifique cómo aprovechar las últimas funciones de AEMaaCS.

También puede [ver los problemas conocidos](/help/release-notes/maintenance/latest.md) que se publican junto con cada versión para conocer cualquier problema técnico que pueda presentar un desafío para su evaluación o posible adopción de cualquier función nueva.

## Habilitación del canal de la versión preliminar para acceder y probar nuevas funciones {#new-features}

El canal de la versión preliminar se puede habilitar en cualquier entorno de desarrollo o zona protegida. La versión preliminar no se puede habilitar en entornos de ensayo o producción.

Las funciones de la versión preliminar se pueden experimentar de diferentes maneras:

* [Entornos de la nube](#cloud-environments)
* [SDK local](#local-sdk)

### Entornos de la nube {#cloud-environments}

Para actualizar un entorno de nube a fin de utilizar la versión preliminar, debe agregar una nueva variable de entorno. Puede hacerlo mediante la IU de Cloud Manager o mediante CLI.

#### Adición de variable de entorno mediante la IU {#add-with-ui}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Vaya al programa en el que desea habilitar la versión preliminar.

1. Seleccione el entorno en el que desea habilitar la versión preliminar y acceda a su configuración mediante **Programa** > **Entorno** > **Configuración del entorno**.

1. Agregue una nueva [variable de entorno:](../implementing/cloud-manager/environment-variables.md)

   | Nombre | Value | Servicio aplicado | Tipo |
   |------|-------|-----------------|------|
   | `AEM_RELEASE_CHANNEL` | `prerelease` | Todos | Variable |

1. Guarde los cambios y el entorno se actualizará con las características de la versión preliminar activadas.

   ![Nueva variable de entorno](assets/env-configuration-prerelease.png)

#### Adición de variable de entorno mediante CLI {#add-with-cli}

También puede utilizar la API y la CLI de Cloud Manager para actualizar las variables de entorno.

* Mediante el [punto final de variables de entorno de API de Cloud Manager,](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/patchEnvironmentVariables) establezca la `AEM_RELEASE_CHANNEL`variable de entorno en el valor `prerelease`.

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

* [La CLI de Cloud Manager](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) también se puede utilizar en

   ```shell
   aio cloudmanager:environment:set-variables <ENVIRONMENT_ID> --programId=<PROGRAM_ID> --variable AEM_RELEASE_CHANNEL “prerelease
   ```

La variable se puede eliminar o volver a establecerse en un valor diferente si desea que el entorno se restaure al comportamiento del canal normal (que no es de prelanzamiento).

### El SDK local {#local-sdk}

Puede ver nuevas funciones en la consola de Sites en el SDK de Quickstart local y programar las nuevas API en la versión preliminar configurando su proyecto de Maven para que haga referencia a la versión preliminar `API Jar` situada en Maven Central. También puede ver estas características de la versión preliminar en el entorno de desarrollo local iniciando el SDK de Quickstart normal en modo de la versión preliminar.

#### Inicio del SDK de Quickstart en modo de versión preliminar {#prerelease-mode}

1. Descargue el SDK desde el portal de distribución de software e instálelo tal como se describe en [Acceso al SDK de AEM as a Cloud Service.](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
1. Al iniciar Quickstart de SDK, incluya el argumento `-r prerelease`.

El valor es fijo, por lo tanto, solo se puede seleccionar en el primer inicio. Vuelva a instalar el SDK para cambiar la opción de la línea de comandos.

Dado que puede haber varias versiones de mantenimiento de AEM entre las versiones de funciones mensuales, puede descargar estos nuevos SDK y hacer referencia a las nuevas versiones de JAR de API de SDK en proyectos en Maven. Las versiones de mantenimiento no añadirán funciones de versión preliminar adicionales, pero podrían incluir otros cambios más pequeños, como correcciones de errores, correcciones de seguridad y mejoras de rendimiento.
Los JavaDocs se publican en Maven Central.

#### Compilación con el SDK de la versión preliminar {#build-sdk}

1. Modifique el `pom.xml` de su proyecto de Maven para hacer referencia a un JAR de API de SDK de la versión preliminar distinta, que se publica en Maven central. Contiene cualquier nueva API de Java para las funciones de la versión preliminar y depende del JAR de la API del SDK. Utiliza la misma versión.

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

1. Implementación en el servidor local.

1. Si está seguro de que funciona como se espera localmente, confirme el código a una rama de desarrollo y utilice una canalización de no producción de Cloud Manager para implementar en un entorno que se suscriba al canal de la versión preliminar.

>[!CAUTION]
> 
> El artifactId `aem-prerelease-sdk-api` nunca debe utilizarse al implementar en ensayo o producción. Utilice siempre `aem-sdk-api` al implementar mediante la canalización de producción. Del mismo modo, el código que hace referencia a las API de la versión preliminar no debe implementarse mediante la canalización de producción.

El [complemento Maven de AEM CS SDK Analyzer versión 1.0 y superior](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=es#developing) detectará si la API de la versión preliminar se utiliza en un proyecto inspeccionando las dependencias. Si el analizador lo encuentra, utilizará la API del SDK de la versión preliminar para analizar el proyecto.

## Formación de los usuarios {#train-users}

Una vez que haya probado las nuevas funciones en el canal de la versión preliminar y haya decidido aprovecharlas en sus proyectos, debe formar a los usuarios.

Adobe Experience League ofrece muchos recursos para aprender AEMaaCS.

* [La documentación de AEMaaCS](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=es)
* [Tutoriales](https://experienceleague.adobe.com/docs/experience-manager-learn/aem-tutorials/overview.html?lang=es)
* [Vídeo de información general de la versión mensual](/help/release-notes/release-notes-cloud/release-notes-current.md#release-video) en las notas de la versión

## Consideraciones {#considerations}

Hay algunos elementos que se deben tener en cuenta al utilizar el canal de la versión preliminar.

* El canal de la versión preliminar no contiene necesariamente todas las nuevas funciones que se implementarán en la siguiente versión.
* Las funciones de la versión preliminar se someten a rigurosas garantías de calidad y se pretende que sean características completas en lugar de calidad beta. Si nota algún problema, informe de él, tal como lo haría si sospechara que hay errores en las características de una versión de AEM normal.
* Para determinar si un entorno está configurado para el canal de la versión preliminar, vaya a la página **Acerca de** de la consola de AEM y compruebe si el número de versión de AEM incluye un sufijo de *la versión preliminar* como ```Adobe Experience Manager 2021.4.5226.20210427T070726Z-210429-PRERELEASE```.

![Acerca de](/help/release-notes/assets/about.png)
