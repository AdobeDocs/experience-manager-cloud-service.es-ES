---
title: 'Pruebas de IU: Cloud Services'
description: 'Pruebas de IU: Cloud Services'
translation-type: tm+mt
source-git-commit: ea0c9675ca03b1d247c7e5fd13e03072fb4a13ae
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 0%

---


# Prueba de UI {#ui-testing}

Las pruebas de interfaz de usuario son pruebas basadas en selenio empaquetadas en una imagen de Docker para permitir una amplia variedad de idiomas y marcos (como Java y Maven, Node y WebDriver.io, o cualquier otro marco de trabajo y tecnología creados en Selenium). La imagen del Docker se puede crear con herramientas estándar, pero debe respetar ciertas convenciones durante su ejecución. Al ejecutar la imagen del Docker, se aprovisiona automáticamente un servidor Selenium. Las convenciones de tiempo de ejecución que se describen a continuación permiten que el código de prueba acceda tanto al servidor de Selenium como a las instancias de AEM que se están probando.

>[!NOTE]
> Las canalizaciones de fase y producción creadas antes del 10 de febrero de 2012 deben actualizarse para utilizar las pruebas de interfaz de usuario tal como se describe en esta página.
> Consulte [Configuración de la canalización CI-CD](/help/implementing/cloud-manager/configure-pipeline.md) para obtener información sobre la configuración de la canalización.

## Generando pruebas de IU {#building-ui-tests}

Las pruebas de interfaz de usuario se crean a partir de un contexto de compilación de Docker generado por un proyecto de Maven. Cloud Manager utiliza el contexto de compilación de Docker para generar una imagen de Docker que contiene las pruebas de IU reales. En resumen, un proyecto de Maven genera un contexto de compilación de Docker y el contexto de compilación de Docker describe cómo crear una imagen de Docker que contenga las pruebas de IU.

En esta sección se explican los pasos necesarios para agregar un proyecto de pruebas de interfaz de usuario al repositorio. Si tiene prisa o no tiene requisitos especiales para el lenguaje de programación, el [AEM Arquetipo de proyecto](https://github.com/adobe/aem-project-archetype) puede generar un proyecto de pruebas de interfaz de usuario.

### Generar un contexto de compilación de Docker {#generate-docker-build-context}

Para generar un contexto de compilación de Docker, necesita un módulo Maven que:

- Produce un archivo que contiene un `Dockerfile` y todos los demás archivos necesarios para crear la imagen del Docker con las pruebas.
- Etiqueta el archivo con el clasificador `ui-test-docker-context`.

La manera más sencilla de lograr esto es configurar el [Complemento de ensamblaje de maven](http://maven.apache.org/plugins/maven-assembly-plugin/) para crear el archivo de contexto de compilación de Docker y asignarle el clasificador adecuado.

Puede crear pruebas de interfaz de usuario con diferentes tecnologías y marcos, pero en esta sección se asume que el proyecto está diseñado de manera similar a la siguiente.

```
├── Dockerfile
├── assembly-ui-test-docker-context.xml
├── pom.xml
├── test-module
│   ├── package.json
│   ├── index.js
│   └── wdio.conf.js
└── wait-for-grid.sh
```

El archivo `pom.xml` se encarga de la compilación de Maven. Añada una ejecución en el complemento Maven Assembly similar a la siguiente.

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

Esta ejecución ordena al complemento de ensamblaje de Maven que cree un archivo basado en las instrucciones contenidas en `assembly-ui-test-docker-context.xml`, llamado &quot;descriptor de ensamblado&quot; en la jerga del complemento. El descriptor de ensamblado lista todos los archivos que deben formar parte del archivo.

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

El descriptor de ensamblado indica al complemento que cree un archivo de tipo `.tar.gz` y le asigna el clasificador `ui-test-docker-context`. Además, lista los archivos que deben incluirse en el archivo:

- Un `Dockerfile`, obligatorio para generar la imagen del Docker.
- La secuencia de comandos `wait-for-grid.sh`, cuyos propósitos se describen a continuación.
- Las pruebas de IU reales, implementadas por un proyecto Node.js en la carpeta `test-module`.

El descriptor de ensamblado también excluye algunos archivos que se pueden generar al ejecutar las pruebas de interfaz de usuario localmente. Esto garantiza un archiving más pequeño y compilaciones más rápidas.

El Cloud Manager recoge automáticamente el archivo que contiene el contexto de compilación del Docker, que generará la imagen del Docker que contiene las pruebas durante las canalizaciones de implementación. Con el tiempo, Cloud Manager ejecutará la imagen de Docker para ejecutar las pruebas de interfaz de usuario con la aplicación.

## Escritura de pruebas de IU {#writing-ui-tests}

En esta sección se describen las convenciones que debe seguir la imagen del Docker que contiene las pruebas de IU. La imagen del Docker se ha creado a partir del contexto de compilación del Docker descrito en la sección anterior.

### Variables de entorno {#environment-variables}

Las siguientes variables de entorno se pasarán a la imagen del Docker en tiempo de ejecución.

| Variable | Ejemplos | Descripción |
|---|---|---|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | La dirección URL del servidor Selenium |
| `SELENIUM_BROWSER` | `chrome`, `firefox` | La implementación del explorador que utiliza el servidor de selenio |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | Dirección URL de la instancia de creación de AEM |
| `AEM_AUTHOR_USERNAME` | `admin` | El nombre de usuario para iniciar sesión en la instancia de creación de AEM |
| `AEM_AUTHOR_PASSWORD` | `admin` | La contraseña para iniciar sesión en la instancia de creación de AEM |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | Dirección URL de la instancia de publicación AEM |
| `AEM_PUBLISH_USERNAME` | `admin` | El nombre de usuario para iniciar sesión en la instancia de publicación de AEM |
| `AEM_PUBLISH_PASSWORD` | `admin` | La contraseña para iniciar sesión en la instancia de publicación de AEM |
| `REPORTS_PATH` | `/usr/src/app/reports` | Ruta en la que se debe guardar el informe XML de los resultados de la prueba |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | La dirección URL en la que se debe cargar el archivo para que sea accesible para Selenium |

### Esperando que Selenium esté listo {#waiting-for-selenium}

Antes del inicio de pruebas, es responsabilidad de la imagen del Docker asegurarse de que el servidor Selenium esté activo y en funcionamiento. Esperar al servicio Selenium es un proceso de dos pasos:

1. Lea la dirección URL del servicio Selenium desde la variable de entorno `SELENIUM_BASE_URL`.
2. Encuesta a intervalos regulares al extremo de estado [](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready) expuesto por la API de Selenium.

Una vez que el extremo de estado de Selenium responde con una respuesta positiva, las pruebas finalmente pueden inicio.

### Generar los informes de prueba {#generate-test-reports}

La imagen del Docker debe generar informes de prueba en formato XML JUnit y guardarlos en la ruta especificada por la variable de entorno `REPORTS_PATH`. El formato JUnit XML es un formato muy extendido para el sistema de informes de los resultados de las pruebas. Si la imagen del Docker utiliza Java y Maven, tanto el [Complemento Maven Surefire](https://maven.apache.org/surefire/maven-surefire-plugin/) como el [Complemento Maven Failsafe](https://maven.apache.org/surefire/maven-failsafe-plugin/). Si la imagen del Docker está implementada con otros lenguajes de programación o ejecutores de pruebas, consulte la documentación de las herramientas elegidas para saber cómo generar informes XML de JUnit.

### Carga de archivos (#upload-files)

En ocasiones, las pruebas deben cargar archivos en la aplicación que se está probando. Para mantener flexible la implementación de Selenium en relación con sus pruebas, no es posible cargar directamente un recurso a Selenium. En su lugar, la carga de un archivo pasa por algunos pasos intermedios:

1. Cargue el archivo en la dirección URL especificada por la variable de entorno `UPLOAD_URL`. La carga debe realizarse en una solicitud de POST con un formulario de varias partes. El formulario de varias partes debe tener un solo campo de archivo. Es equivalente a `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`. Consulte la documentación y las bibliotecas del lenguaje de programación utilizado en la imagen del Docker para saber cómo realizar una solicitud HTTP de este tipo.
2. Si la carga se realiza correctamente, la solicitud devuelve una respuesta `200 OK` de tipo `text/plain`. El contenido de la respuesta es un controlador de archivo opaco. Puede utilizar este identificador en lugar de una ruta de archivo en un elemento `<input>` para probar las cargas de archivos en la aplicación.
