---
title: Pruebas de IU
description: La prueba de IU personalizada es una función opcional que le permite crear y ejecutar automáticamente pruebas de IU para sus aplicaciones personalizadas
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
source-git-commit: a7555507f4fb0fb231e27d7c7a6413b4ec6b94e6
workflow-type: tm+mt
source-wordcount: '1401'
ht-degree: 1%

---


# Pruebas de IU {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="Pruebas de IU"
>abstract="La prueba de IU personalizada es una función opcional que le permite crear y ejecutar automáticamente pruebas de IU para sus aplicaciones. Las pruebas de interfaz de usuario son pruebas basadas en Selenium empaquetadas en una imagen Docker para permitir una amplia variedad de idiomas y marcos (como Java y Maven, Node y WebDriver.io, o cualquier otro marco y tecnología creados en Selenium)."

La prueba de IU personalizada es una función opcional que le permite crear y ejecutar automáticamente pruebas de IU para sus aplicaciones.

>[!NOTE]
> Las canalizaciones de fase y producción creadas antes del 10 de febrero de 2021 deben actualizarse para utilizar las pruebas de IU tal como se describe en esta página.
> Consulte [Canalizaciones CI-CD en Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) para obtener información sobre la configuración de la canalización.

## Información general {#custom-ui-testing}

AEM ofrece un conjunto integrado de [Puertas de calidad de Cloud Manager](/help/implementing/cloud-manager/custom-code-quality-rules.md) para garantizar actualizaciones sin problemas en las aplicaciones personalizadas. En concreto, las puertas de prueba de TI ya se han creado y automatizado pruebas personalizadas mediante API AEM.

Las pruebas de interfaz de usuario son pruebas basadas en Selenium empaquetadas en una imagen Docker para permitir una amplia variedad de idiomas y marcos (como Java y Maven, Node y WebDriver.io, o cualquier otro marco y tecnología creados en Selenium). Además, un proyecto de pruebas de interfaz de usuario se puede generar fácilmente mediante el uso de [el tipo de archivo del proyecto de AEM.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)

Las pruebas de interfaz de usuario se ejecutan como parte de una puerta de calidad específica para cada canalización de Cloud Manager con un [dedicated **Pruebas de IU personalizadas** paso a paso.](/help/implementing/cloud-manager/deploy-code.md) Cualquier prueba de la interfaz de usuario, incluidas la regresión y las nuevas funcionalidades, permite detectar y notificar errores.

A diferencia de las pruebas funcionales personalizadas, que son pruebas HTTP escritas en Java, las pruebas de interfaz de usuario pueden ser una imagen de Docker con pruebas escritas en cualquier idioma, siempre y cuando sigan las convenciones definidas en la sección [Creación de pruebas de IU.](#building-ui-tests)

>[!TIP]
>
>Adobe recomienda seguir la estructura y el idioma (JavaScript y WDIO) proporcionados en la variable [AEM tipo de archivo del proyecto.](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)

### Inclusión del cliente {#customer-opt-in}

Para que Cloud Manager pueda crear y ejecutar sus pruebas de interfaz de usuario, debe incluirse en esta función añadiendo un archivo al repositorio.

* El nombre del archivo debe ser `testing.properties`.
* El contenido del archivo debe ser `ui-tests.version=1`.
* El archivo debe estar en el submódulo maven para pruebas de interfaz de usuario junto al `pom.xml` archivo del submódulo Pruebas de interfaz de usuario .
* El archivo debe estar en la raíz del `tar.gz` archivo.

Las pruebas de interfaz de usuario se crean y las ejecuciones se omiten si este archivo no está presente.

Para incluir un `testing.properties` en el artefacto de compilación, agregue un `include` en la `assembly-ui-test-docker-context.xml` archivo.

```xml
[...]
<includes>
    <include>Dockerfile</include>
    <include>wait-for-grid.sh</include>
    <include>testing.properties</include> <!- opt-in test module in Cloud Manager -->
</includes>
[...]
```

>[!NOTE]
>
>Si el proyecto no incluye esta línea, deberá editar este archivo para optar por la prueba de IU. Si el archivo tiene una línea que aconseja no editarlo, desestime ese consejo.

>[!NOTE]
>
>Las canalizaciones de producción creadas antes del 10 de febrero de 2021 deberán actualizarse para utilizar las pruebas de IU tal como se describe en esta sección. Esto significa que el usuario debe editar la canalización de producción y hacer clic en **Guardar** desde la interfaz de usuario aunque no se hayan realizado cambios.
>Consulte [Configuración de la canalización de CI-CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager) para obtener más información sobre la configuración de la canalización.

## Creación de pruebas de interfaz de usuario {#building-ui-tests}

Un proyecto de Maven genera un contexto de compilación de Docker. Este contexto de compilación de Docker describe cómo crear una imagen de Docker que contenga las pruebas de interfaz de usuario, que los usuarios de Cloud Manager generarán una imagen de Docker que contenga las pruebas de IU reales.

En esta sección se describen los pasos necesarios para agregar un proyecto de pruebas de interfaz de usuario al repositorio.

>[!TIP]
>
>La variable [Tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype) puede generar un proyecto de pruebas de IU porque no tiene requisitos especiales para el lenguaje de programación.

### Generación de un contexto de compilación de docker {#generate-docker-build-context}

Para generar un contexto de compilación de Docker, necesita un módulo Maven que:

* Produce un archivo que contiene un `Dockerfile` y todos los demás archivos necesarios para crear la imagen Docker con sus pruebas.
* Etiqueta el archivo con la variable `ui-test-docker-context` clasificador.

La forma más sencilla de hacerlo es configurar la variable [Complemento Ensamblado de Maven](http://maven.apache.org/plugins/maven-assembly-plugin/) para crear el archivo de contexto de compilación de Docker y asignarle el clasificador adecuado.

Puede crear pruebas de interfaz de usuario con diferentes tecnologías y marcos, pero en esta sección se da por hecho que el diseño del proyecto es similar al siguiente.

```text
├── Dockerfile
├── assembly-ui-test-docker-context.xml
├── pom.xml
├── test-module
│   ├── package.json
│   ├── index.js
│   └── wdio.conf.js
└── wait-for-grid.sh
```

La variable `pom.xml` se encarga de la compilación de Maven. Añada una ejecución al complemento Maven Assembly similar a la siguiente.

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-assembly-plugin</artifactId>
    <configuration>
        <descriptors>
            <descriptor>${project.basedir}/assembly-ui-test-docker-context.xml</descriptor>
        </descriptors>
        <tarLongFileMode>gnu</tarLongFileMode>
    </configuration>
    <executions>
        <execution>
            <id>make-assembly</id>
            <phase>package</phase>
            <goals>
                <goal>single</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

Esta ejecución ordena al complemento Maven Assembly que cree un archivo basado en las instrucciones contenidas en `assembly-ui-test-docker-context.xml`, se denomina **descriptor de ensamblado** en la jerga del complemento. El descriptor de ensamblado enumera todos los archivos que deben formar parte del archivo.

```xml
<assembly>
    <id>ui-test-docker-context</id>
    <includeBaseDirectory>false</includeBaseDirectory>
    <formats>
        <format>tar.gz</format>
    </formats>
    <fileSets>
        <fileSet>
            <directory>${basedir}</directory>
            <includes>
                <include>Dockerfile</include>
                <include>wait-for-grid.sh</include>
            </includes>
        </fileSet>
        <fileSet>
            <directory>${basedir}/test-module</directory>
            <excludes>
                <exclude>node/**</exclude>
                <exclude>node_modules/**</exclude>
                <exclude>reports/**</exclude>
            </excludes>
        </fileSet>
    </fileSets>
</assembly>
```

El descriptor de ensamblado indica al complemento que cree un archivo de tipo `.tar.gz` y asigna la variable `ui-test-docker-context` clasificador para él. Además, enumera los archivos que deben incluirse en el archivo, incluyendo los siguientes.

* A `Dockerfile`, obligatorio para crear la imagen Docker
* La variable `wait-for-grid.sh` secuencia de comandos, cuyos propósitos se describen a continuación
* Las pruebas de interfaz de usuario reales, implementadas por un proyecto Node.js en la variable `test-module` carpeta

El descriptor de ensamblado también excluye algunos archivos que podrían generarse al ejecutar las pruebas de IU localmente. Esto garantiza un archivo más pequeño y compilaciones más rápidas.

El archivo que contiene el contexto de compilación de Docker se recoge automáticamente en Cloud Manager, que creará la imagen de Docker que contiene las pruebas durante sus canalizaciones de implementación. Al final, Cloud Manager ejecutará la imagen de Docker para ejecutar las pruebas de interfaz de usuario con la aplicación.

La compilación debe producir cero o un archivo. Si no genera archivos, el paso de prueba pasa de forma predeterminada. Si la compilación produce más de un archivo, qué archivo se selecciona no es determinista.

## Escritura de pruebas de interfaz de usuario {#writing-ui-tests}

En esta sección se describen las convenciones que debe seguir la imagen de Docker que contiene las pruebas de IU. La imagen Docker se crea a partir del contexto de compilación de Docker descrito en la sección anterior.

### Variables de entorno {#environment-variables}

Las siguientes variables de entorno se pasarán a la imagen de Docker en tiempo de ejecución.

| Variable | Ejemplos | Descripción |
|---|---|---|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | La URL del servidor de Selenium |
| `SELENIUM_BROWSER` | `chrome`, `firefox` | Implementación del explorador utilizada por el servidor de Selenium |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | Dirección URL de la instancia de autor de AEM |
| `AEM_AUTHOR_USERNAME` | `admin` | El nombre de usuario para iniciar sesión en la instancia de autor de AEM |
| `AEM_AUTHOR_PASSWORD` | `admin` | La contraseña para iniciar sesión en la instancia de autor de AEM |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | La URL de la instancia de publicación de AEM |
| `AEM_PUBLISH_USERNAME` | `admin` | El nombre de usuario para iniciar sesión en la instancia de publicación de AEM |
| `AEM_PUBLISH_PASSWORD` | `admin` | La contraseña para iniciar sesión en la instancia de publicación de AEM |
| `REPORTS_PATH` | `/usr/src/app/reports` | La ruta en la que se debe guardar el informe XML de los resultados de la prueba |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | La URL donde debe cargarse el archivo a para que sea accesible para Selenium |

### Esperando a que Selenium esté listo {#waiting-for-selenium}

Antes de que comiencen las pruebas, es responsabilidad de la imagen Docker asegurarse de que el servidor Selenium esté funcionando. Esperar el servicio de Selenium es un proceso de dos pasos.

1. Lea la URL del servicio de Selenium desde el `SELENIUM_BASE_URL` variable de entorno.
1. Encuesta a intervalos regulares al [extremo de estado](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready) expuesto por la API de Selenium.

Una vez que el extremo de estado de Selenium responde con una respuesta positiva, las pruebas pueden comenzar.

### Generar informes de prueba {#generate-test-reports}

La imagen Docker debe generar informes de prueba en formato XML JUnit y guardarlos en la ruta especificada por la variable de entorno `REPORTS_PATH`. El formato JUnit XML es un formato ampliamente utilizado para informar sobre los resultados de las pruebas. Si la imagen Docker utiliza Java y Maven, tanto la variable [Complemento Maven Surefire](https://maven.apache.org/surefire/maven-surefire-plugin/) y [Complemento Maven FailedSafe](https://maven.apache.org/surefire/maven-failsafe-plugin/).

Si la imagen Docker está implementada con otros lenguajes de programación o ejecutores de prueba, compruebe la documentación de las herramientas seleccionadas para generar informes XML de JUnit.

### Cargar archivos {#upload-files}

Las pruebas a veces deben cargar archivos en la aplicación que se está probando. Para que la implementación de Selenium sea flexible con respecto a sus pruebas, no es posible cargar directamente un recurso a Selenium. En su lugar, la carga de un archivo requiere los siguientes pasos.

1. Cargue el archivo en la dirección URL especificada por el `UPLOAD_URL` variable de entorno.
   * La carga debe realizarse en una solicitud de POST con un formulario de varias partes.
   * El formulario de varias partes debe tener un único campo de archivo.
   * Esto equivale a `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`.
   * Consulte la documentación y las bibliotecas del lenguaje de programación utilizado en la imagen Docker para saber cómo realizar una solicitud HTTP de este tipo.
1. Si la carga se realiza correctamente, la solicitud devuelve un valor `200 OK` respuesta del tipo `text/plain`.
   * El contenido de la respuesta es un controlador de archivo opaco.
   * Puede utilizar este identificador en lugar de una ruta de archivo en una `<input>` para probar las cargas de archivos en la aplicación.
