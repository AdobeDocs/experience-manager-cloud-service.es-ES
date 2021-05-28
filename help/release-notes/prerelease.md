---
title: '[!DNL Adobe Experience Manager] como Cloud Service Canal de prelanzamiento'
description: '[!DNL Adobe Experience Manager] como Cloud Service Canal de prelanzamiento'
source-git-commit: 4ee9a5744cdcec00dd497a00b0d8dbf288a5adcb
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---


# [!DNL Adobe Experience Manager] como Cloud Service Canal de prelanzamiento  {#prerelease-channel}


## Introducción {#introduction}

[!DNL Adobe Experience Manager] as a Cloud Service ofrece nuevas funciones en una cadencia mensual, según la programación de versiones de  [Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=en#aem-as-cloud-service). Para familiarizarse con las funciones programadas para entrar en funcionamiento el mes siguiente, los clientes pueden suscribirse al canal de prelanzamiento, al que se puede acceder configurando adecuadamente en entornos de desarrollo de programas estándar o en cualquier entorno de programa de simulación de pruebas. Los clientes pueden obtener una vista previa de los cambios realizados en la consola Sitios, así como crear código para cualquier API de versión preliminar nueva.

La lista de características de la versión preliminar de un mes determinado se publica en las [notas de la versión mensuales](/help/release-notes/release-notes-cloud/release-notes-current.md).

>[!VÍDEO](/help/release-notes/assets/prerelease-overview.mp4)

## Cómo habilitar la versión preliminar {#enable-prerelease}

Las funciones de la versión preliminar se pueden experimentar de diferentes maneras:

* Entornos en la nube (entornos de desarrollo de programa estándar o cualquier tipo de entorno de programa de entorno limitado)
* SDK local

### Entornos de nube {#cloud-environments}

Para ver las nuevas funciones de la consola Sitios en los entornos de desarrollo de la nube, así como el resultado de cualquier personalización de proyecto:

* Utilizando el [extremo de las variables de entorno de la API de Cloud Manager](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Variables/patchEnvironmentVariables), establezca la variable de entorno **AEM_RELEASE_CHANNEL** en el valor **prelanzamiento**.

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

También se puede utilizar la CLI de Cloud Manager, según las instrucciones en [https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid)
```aio cloudmanager:environment:set-variables <ENVIRONMENT_ID> --programId=<PROGRAM_ID> --variable AEM_RELEASE_CHANNEL “prerelease”```


La variable se puede eliminar o volver a establecer en un valor diferente si desea que el entorno se restaure al comportamiento del canal normal (que no es de prelanzamiento)

### SDK local {#local-sdk}

Puede ver nuevas funciones en la consola Sitios en el SDK local de Quickstart y código para las nuevas API en la versión preliminar. Para ello, haga que su proyecto maven haga referencia a la versión preliminar `API Jar` ubicada en Maven Central. También puede ver estas características de la versión preliminar en el equipo local iniciando el SDK de inicio rápido normal en modo de versión preliminar:

* Descargue el SDK desde el portal de distribución de software e instálelo tal como se describe en [Acceso al AEM como SDK de Cloud Service](/help/implementing/developing/aem-as-a-cloud-service-sdk.md#accessing-the-aem-as-a-cloud-service-sdk.)
* Al iniciar el inicio rápido del SDK, incluya el argumento `-r prerelease`.
* El valor es *fijo*, por lo que solo se puede seleccionar en el primer inicio. Vuelva a instalar el SDK para cambiar la opción de la línea de comandos.

Dado que puede haber varias versiones de mantenimiento de AEM entre las versiones de funciones mensuales, puede descargar estos nuevos SDK y hacer referencia a las nuevas versiones de Jar de API de SDK en proyectos de Maven. Las versiones de mantenimiento no agregarán funciones de revisión previa adicionales, pero podrían incluir otros cambios más pequeños, como correcciones de errores, correcciones de seguridad y mejoras de rendimiento.
Los javadocs se publican en Maven Central.

Para compilar con el SDK de prelanzamiento:

1. modifique el pom.xml de su proyecto maven para hacer referencia a un jar de api de sdk de prelanzamiento distinto, que se publica en Maven central. Contiene cualquier nueva api de Java para las funciones de prelanzamiento y depende del jar de la api del sdk. Utiliza la misma versión.

   Por ejemplo, a continuación se muestra un fragmento de la sección de administración de dependencias del pom principal que hace referencia al Jar de API normal:

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

1. Implementar en el servidor local
1. Si está seguro de que funciona como se espera localmente, confirme el código a una rama de desarrollo y utilice una canalización de no producción de Cloud Manager para implementar en un entorno que se suscriba al canal de prelanzamiento

>[!CAUTION]
El `aem-prerelease-sdk-api` artifactId nunca debe utilizarse al implementar en fase o producción. Utilice siempre la api de aem-sdk al implementar mediante la canalización de producción. Del mismo modo, el código que hace referencia a las API de versión preliminar no debe implementarse mediante la canalización de producción.

El [AEM analizador de compilaciones del SDK CS para maven plugin v1.0 y superior](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing) detectará si la api de prelanzamiento se utiliza en un proyecto inspeccionando las dependencias. Si el analizador lo encuentra, utilizará la api del sdk de prelanzamiento para analizar el proyecto.

## Consideraciones {#considerations}

Hay algunas cosas que hay que tener en cuenta cuando se trata del canal de prelanzamiento:

* Es posible que algunas funciones que se implementarán en la versión del próximo mes no se incluyan en el canal de prelanzamiento.
* Las funciones de la versión preliminar se someten a rigurosas garantías de calidad y se pretende que sean características completas en lugar de calidad beta. Si nota algún problema, informe de él, tal como lo haría si sospechara que hay errores en las características de una versión AEM normal.
* Para determinar si un entorno está configurado para el canal de prelanzamiento, vaya a la página **Acerca de** de la Consola de AEM y compruebe si el número de versión de AEM incluye un sufijo *de prelanzamiento* como ```Adobe Experience Manager 2021.4.5226.20210427T070726Z-210429-PRERELEASE```.

![about](/help/release-notes/assets/about.png)
