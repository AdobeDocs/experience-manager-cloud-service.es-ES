---
title: Pruebas de IU
description: La prueba de IU personalizada es una característica opcional que le permite crear y ejecutar automáticamente pruebas de IU para sus aplicaciones personalizadas
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
source-git-commit: 31e84b7383cd9774b0eaf8ee0f2fe39bcd77fa15
workflow-type: tm+mt
source-wordcount: '1407'
ht-degree: 95%

---


# Pruebas de IU {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="Pruebas de IU"
>abstract="La prueba de IU personalizada es una característica opcional que le permite crear y ejecutar automáticamente pruebas de IU para sus aplicaciones. Las pruebas de interfaz de usuario son pruebas basadas en Selenium empaquetadas en una imagen Docker para permitir una amplia variedad de lenguajes y marcos de trabajo (como Java y Maven, Node y WebDriver.io, o cualquier otro marco de trabajo y tecnología creados en Selenium)."

La prueba de IU personalizada es una característica opcional que le permite crear y ejecutar automáticamente pruebas de IU para sus aplicaciones.

## Información general {#custom-ui-testing}

AEM ofrece un conjunto integrado de [Puertas de calidad de Cloud Manager](/help/implementing/cloud-manager/custom-code-quality-rules.md) para garantizar actualizaciones sin problemas en las aplicaciones personalizadas. En concreto, las puertas de prueba de TI ya crearon y automatizaron pruebas personalizadas mediante las API de AEM.

Las pruebas de interfaz de usuario son pruebas basadas en Selenium empaquetadas en una imagen Docker para permitir una amplia variedad de lenguajes y marcos de trabajo (como Java y Maven, Node y WebDriver.io, o cualquier otro marco de trabajo y tecnología creados en Selenium). Además, se puede generar fácilmente un proyecto de pruebas de interfaz de usuario mediante el uso de [el arquetipo del proyecto AEM.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es)

Las pruebas de interfaz de usuario se ejecutan como parte de una puerta de calidad específica para cada canalización de Cloud Manager con un paso [dedicado de **Pruebas de IU personalizadas**.](/help/implementing/cloud-manager/deploy-code.md) Cualquier prueba de la interfaz de usuario, incluidas la regresión y las nuevas funcionalidades, permite detectar y notificar errores.

A diferencia de las pruebas funcionales personalizadas, que son pruebas HTTP escritas en Java, las pruebas de interfaz de usuario pueden ser una imagen de Docker con pruebas escritas en cualquier lenguaje, siempre y cuando sigan las convenciones definidas en la sección [Generar pruebas de IU.](#building-ui-tests)

>[!TIP]
>
>Adobe recomienda seguir la estructura y los lenguajes (JavaScript y WDIO) proporcionados en el [arquetipo del proyecto AEM.](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)

### Inclusión del cliente {#customer-opt-in}

Para que Cloud Manager pueda crear y ejecutar sus pruebas de interfaz de usuario, debe incluirse en esta característica al agregar un archivo al repositorio.

* El nombre del archivo debe ser `testing.properties`.
* El contenido del archivo debe ser `ui-tests.version=1`.
* El archivo debe estar en el módulo secundario de Maven para pruebas de interfaz de usuario junto al `pom.xml` archivo del módulo secundario Pruebas de interfaz de usuario.
* El archivo debe estar en la raíz del archivo de generación `tar.gz`.

La generación de pruebas de interfaz de usuario y las ejecuciones se omitirán si este archivo no está presente.

Para incluir un archivo `testing.properties` en el artefacto de generación, agregue un enunciado `include` en el `assembly-ui-test-docker-context.xml` archivo.

```xml
[...]
<includes>
    <include>Dockerfile</include>
    <include>wait-for-grid.sh</include>
    <include>testing.properties</include> <!-- opt-in test module in Cloud Manager -->
</includes>
[...]
```

>[!NOTE]
>
>Si el proyecto no incluye esta línea, deberá editar el archivo para optar por la prueba de IU.
>
>El archivo puede contener una línea que aconseje no editarlo. Esto se debe a que se introdujo en el proyecto antes de que se introdujera la prueba de IU de inclusión y a que los clientes no tenían la intención de editar el archivo. Se puede ignorar con seguridad.

## Generar pruebas de interfaz de usuario {#building-ui-tests}

Un proyecto de Maven genera un contexto de generación de Docker. Este contexto de generación de Docker describe cómo crear una imagen de Docker que contenga las pruebas de interfaz de usuario, que Cloud Manager usará para generar una imagen de Docker que contenga las pruebas de IU reales.

En esta sección se describen los pasos necesarios para agregar un proyecto de pruebas de interfaz de usuario al repositorio.

>[!TIP]
>
>El [arquetipo del proyecto AEM](https://github.com/adobe/aem-project-archetype) puede generar un proyecto de pruebas de IU porque no tiene requisitos especiales para el lenguaje de programación.

### Generar un contexto de generación de Docker {#generate-docker-build-context}

Para generar un contexto de generación de Docker, necesita un módulo de Maven que:

* Produzca un archivo que contenga un `Dockerfile` y todos los demás archivos necesarios para generar la imagen Docker con sus pruebas.
* Etiqueta el archivo con el clasificador `ui-test-docker-context`.

La forma más sencilla de hacerlo es configurar el [Complemento de Maven Assembly](https://maven.apache.org/plugins/maven-assembly-plugin/) para crear el archivo de contexto de generación de Docker y asignarle el clasificador adecuado.

Puede crear pruebas de interfaz de usuario con diferentes tecnologías y marcos de trabajo, pero en esta sección se da por hecho que el diseño del proyecto es similar al siguiente.

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

El archivo `pom.xml` se encarga de la generación de Maven. Agregue una ejecución al complemento de Maven Assembly similar a la siguiente.

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

Esta ejecución ordena al complemento de Maven Assembly que cree un archivo basado en las instrucciones contenidas en `assembly-ui-test-docker-context.xml`, se denomina **descriptor de ensamblado** en la jerga del complemento. El descriptor de ensamblado enumera todos los archivos que deben formar parte del archivo.

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

El descriptor de ensamblado indica al complemento que cree un archivo de tipo `.tar.gz` y asigna el clasificador `ui-test-docker-context` para él. Además, enumera los archivos que deben incluirse en el archivo, incluidos los siguientes.

* Un `Dockerfile`, obligatorio para crear la imagen Docker
* El script `wait-for-grid.sh`, cuyos propósitos se describen a continuación
* Las pruebas de interfaz de usuario reales, implementadas por un proyecto Node.js en la carpeta `test-module` 

El descriptor de ensamblado también excluye algunos archivos que podrían generarse al ejecutar las pruebas de IU localmente. Esto garantiza un archivo más pequeño y generaciones más rápidas.

El archivo que contiene el contexto de generación de Docker se recoge automáticamente en Cloud Manager, que creará la imagen de Docker que contiene las pruebas durante sus canalizaciones de implementación. Al final, Cloud Manager ejecutará la imagen de Docker para ejecutar las pruebas de interfaz de usuario contra la aplicación.

La generación debe producir ningún o un archivo. Si no genera ningún archivo, el paso de prueba se aprobará de forma predeterminada. Si la generación produce más de un archivo, qué archivo se seleccione no es determinista.

## Escribir pruebas de interfaz de usuario {#writing-ui-tests}

En esta sección se describen las convenciones que debe seguir la imagen de Docker que contiene las pruebas de IU. La imagen Docker se crea a partir del contexto de generación de Docker descrito en la sección anterior.

### Variables de entorno {#environment-variables}

Las siguientes variables de entorno se pasarán a la imagen de Docker en tiempo de ejecución.

| Variable | Ejemplos | Descripción |
|---|---|---|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | La URL del servidor de Selenium |
| `SELENIUM_BROWSER` | `chrome` | La implementación del explorador que utiliza el servidor de Selenium |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | La dirección URL de la instancia de autor de AEM |
| `AEM_AUTHOR_USERNAME` | `admin` | El nombre de usuario para iniciar sesión en la instancia de autor de AEM |
| `AEM_AUTHOR_PASSWORD` | `admin` | La contraseña para iniciar sesión en la instancia de autor de AEM |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | La URL de la instancia de publicación de AEM |
| `AEM_PUBLISH_USERNAME` | `admin` | El nombre de usuario para iniciar sesión en la instancia de publicación de AEM |
| `AEM_PUBLISH_PASSWORD` | `admin` | La contraseña para iniciar sesión en la instancia de publicación de AEM |
| `REPORTS_PATH` | `/usr/src/app/reports` | La ruta en la que se debe guardar el informe XML de los resultados de la prueba |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | La URL donde debe cargarse el archivo para que sea accesible para Selenium |

### Esperando a que Selenium esté listo {#waiting-for-selenium}

Antes de que comiencen las pruebas, es responsabilidad de la imagen Docker asegurarse de que el servidor Selenium funcione. Esperar por el servicio de Selenium es un proceso de dos pasos.

1. Lea la URL del servicio de Selenium desde la `SELENIUM_BASE_URL` variable de entorno.
1. Encuesta a intervalos regulares al [extremo de estado](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready) expuesto por la API de Selenium.

Una vez que el extremo de estado de Selenium dé una respuesta positiva, las pruebas podrán comenzar.

### Generar informes de prueba {#generate-test-reports}

La imagen Docker debe generar informes de prueba en formato XML JUnit y guardarlos en la ruta especificada por la variable de entorno `REPORTS_PATH`. El formato JUnit XML es un formato ampliamente utilizado para informar sobre los resultados de las pruebas. Si la imagen Docker utiliza Java y Maven, los módulos de prueba estándar como el [complemento de Maven Surefire](https://maven.apache.org/surefire/maven-surefire-plugin/) y el [complemento de Maven Failesafe](https://maven.apache.org/surefire/maven-failsafe-plugin/) pueden generar estos informes de forma predeterminada.

Si la imagen Docker está implementada con otros lenguajes de programación o ejecutores de prueba, compruebe la documentación de las herramientas seleccionadas para generar informes XML de JUnit.

### Captación de capturas de pantalla y vídeos {#capture-screenshots}

La imagen del Docker puede generar resultados de prueba adicionales (por ejemplo, capturas de pantalla, vídeos) y guardarlos en la ruta especificada por la variable de entorno `REPORTS_PATH`. Cualquier archivo que se encuentre debajo de la variable `REPORTS_PATH` se incluyen en el archivo de resultados de la prueba.

Si se ha creado un archivo de resultados de prueba durante una ejecución de prueba de interfaz de usuario, el archivo de registro de prueba contiene al final una referencia a la ubicación del archivo de resultados de la prueba.

```
[...]

===============================================================
The detailed test results can be downloaded from the URL below.
Note: the link will expire after 60 days

    https://results-host/test-results.zip

===============================================================
```

### Cargar archivos {#upload-files}

Las pruebas a veces deben cargar archivos en la aplicación que se está probando. Para que la implementación de Selenium sea flexible con respecto a sus pruebas, no es posible cargar directamente un recurso a Selenium. En su lugar, la carga de un archivo requiere los siguientes pasos.

1. Cargue el archivo en la dirección URL especificada por la `UPLOAD_URL` variable de entorno.
   * La carga debe realizarse en una solicitud de POST con un formulario de varias partes.
   * El formulario de varias partes debe tener un único campo de archivo.
   * Esto equivale a `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`.
   * Consulte la documentación y las bibliotecas del lenguaje de programación utilizado en la imagen Docker para saber cómo realizar una solicitud HTTP de este tipo.
1. Si la carga se realiza correctamente, la solicitud devolverá una `200 OK` respuesta del tipo `text/plain`.
   * El contenido de la respuesta es un controlador de archivo opaco.
   * Puede utilizar este identificador en lugar de una ruta de archivo en un elemento `<input>` para probar la carga de archivos en la aplicación.
