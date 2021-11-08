---
title: 'Pruebas de IU: Cloud Services'
description: 'Pruebas de IU: Cloud Services'
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
source-git-commit: 0be391cb760d81a24f2a4815aa6e1e599243c37b
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 0%

---

# Pruebas de IU {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="Pruebas de IU"
>abstract="Las pruebas de interfaz de usuario son pruebas basadas en Selenium empaquetadas en una imagen Docker para permitir una amplia variedad de idiomas y marcos (como Java y Maven, Node y WebDriver.io, o cualquier otro marco y tecnología creados en Selenium). La imagen Docker se puede crear con herramientas estándar, pero debe respetar ciertas convenciones durante su ejecución. Al ejecutar la imagen Docker, se aprovisiona automáticamente un servidor de Selenium. Las convenciones de tiempo de ejecución que se describen a continuación permiten que el código de prueba acceda tanto al servidor de Selenium como a las instancias de AEM que se están probando."

Las pruebas de interfaz de usuario son pruebas basadas en Selenium empaquetadas en una imagen Docker para permitir una amplia variedad de idiomas y marcos (como Java y Maven, Node y WebDriver.io, o cualquier otro marco y tecnología creados en Selenium). La imagen Docker se puede crear con herramientas estándar, pero debe respetar ciertas convenciones durante su ejecución. Al ejecutar la imagen Docker, se aprovisiona automáticamente un servidor de Selenium. Las convenciones de tiempo de ejecución que se describen a continuación permiten que el código de prueba acceda tanto al servidor de Selenium como a las instancias de AEM que se están probando.

>[!NOTE]
> Las canalizaciones de fase y producción creadas antes del 10 de febrero de 2021 deben actualizarse para utilizar las pruebas de IU tal como se describe en esta página.
> Consulte [Canalizaciones CI-CD en Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) para obtener información sobre la configuración de la canalización.

## Creación de pruebas de interfaz de usuario {#building-ui-tests}

Las pruebas de interfaz de usuario se crean a partir de un contexto de compilación de Docker generado por un proyecto de Maven. Cloud Manager utiliza el contexto de compilación de Docker para generar una imagen de Docker que contenga las pruebas de IU reales. En resumen, un proyecto de Maven genera un contexto de compilación de Docker y el contexto de compilación de Docker describe cómo crear una imagen de Docker que contenga las pruebas de IU.

Esta sección pasa por los pasos necesarios para agregar un proyecto de Pruebas de interfaz de usuario al repositorio. Si tiene prisa o no tiene requisitos especiales para el lenguaje de programación, [Tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype) puede generar un proyecto de pruebas de interfaz de usuario.

### Generación de un contexto de compilación de Docker {#generate-docker-build-context}

Para generar un contexto de compilación de Docker, necesita un módulo Maven que:

- Produce un archivo que contiene un `Dockerfile` y todos los demás archivos necesarios para crear la imagen Docker con sus pruebas.
- Etiqueta el archivo con la variable `ui-test-docker-context` clasificador.

La forma más sencilla de lograr esto es configurar la variable [Complemento Ensamblado de Maven](http://maven.apache.org/plugins/maven-assembly-plugin/) para crear el archivo de contexto de compilación de Docker y asignarle el clasificador adecuado.

Puede crear pruebas de interfaz de usuario con diferentes tecnologías y marcos, pero en esta sección se da por hecho que el diseño del proyecto es similar al siguiente.

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

Esta ejecución ordena al complemento Maven Assembly que cree un archivo basado en las instrucciones contenidas en `assembly-ui-test-docker-context.xml`, se denomina &quot;descriptor de ensamblado&quot; en la jerga del complemento. El descriptor de ensamblado enumera todos los archivos que deben formar parte del archivo.

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

El descriptor de ensamblado indica al complemento que cree un archivo de tipo `.tar.gz` y asigna la variable `ui-test-docker-context` clasificador para él. Además, enumera los archivos que deben incluirse en el archivo:

- A `Dockerfile`, obligatorio para crear la imagen Docker.
- La variable `wait-for-grid.sh` , cuyos propósitos se describen a continuación.
- Las pruebas de interfaz de usuario reales, implementadas por un proyecto Node.js en la variable `test-module` carpeta.

El descriptor de ensamblado también excluye algunos archivos que podrían generarse al ejecutar las pruebas de IU localmente. Esto garantiza un archivo más pequeño y compilaciones más rápidas.

El archivo que contiene el contexto de compilación de Docker lo recoge automáticamente Cloud Manager, que creará la imagen de Docker que contiene las pruebas durante sus canalizaciones de implementación. Al final, Cloud Manager ejecutará la imagen de Docker para ejecutar las pruebas de interfaz de usuario con la aplicación.

La compilación debe producir cero o un archivo. Si no genera ningún archivo, el paso de prueba pasa de forma predeterminada. Si la compilación produce más de un archivo, qué archivo se selecciona no es determinista.

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

Antes de que comiencen las pruebas, es responsabilidad de la imagen Docker asegurarse de que el servidor Selenium esté funcionando. Esperar el servicio de Selenium es un proceso de dos pasos:

1. Lea la URL del servicio de Selenium desde el `SELENIUM_BASE_URL` variable de entorno.
2. Encuesta a intervalos regulares al [extremo de estado](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready) expuesto por la API de Selenium.

Una vez que el punto final de estado de Selenium responde con una respuesta positiva, las pruebas finalmente pueden comenzar.

### Generar los informes de prueba {#generate-test-reports}

La imagen Docker debe generar informes de prueba en formato XML JUnit y guardarlos en la ruta especificada por la variable de entorno `REPORTS_PATH`. El formato XML de JUnit es un formato generalizado para informar de los resultados de las pruebas. Si la imagen Docker utiliza Java y Maven, tanto la variable [Complemento Maven Surefire](https://maven.apache.org/surefire/maven-surefire-plugin/) y [Complemento Maven FailedSafe](https://maven.apache.org/surefire/maven-failsafe-plugin/). Si la imagen Docker se implementa con otros lenguajes de programación o ejecutores de prueba, compruebe la documentación de las herramientas seleccionadas para saber cómo generar informes XML de JUnit.

### Cargar archivos (#upload-files)

Las pruebas a veces deben cargar archivos a la aplicación que se está probando. Para mantener flexible la implementación de Selenium en relación con sus pruebas, no es posible cargar directamente un recurso a Selenium. En su lugar, la carga de un archivo pasa por algunos pasos intermedios:

1. Cargue el archivo en la dirección URL especificada por el `UPLOAD_URL` variable de entorno. La carga debe realizarse en una solicitud de POST con un formulario de varias partes. El formulario de varias partes debe tener un único campo de archivo. Esto equivale a `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`. Consulte la documentación y las bibliotecas del lenguaje de programación utilizado en la imagen Docker para saber cómo realizar una solicitud HTTP de este tipo.
2. Si la carga se realiza correctamente, la solicitud devuelve un valor `200 OK` respuesta del tipo `text/plain`. El contenido de la respuesta es un controlador de archivo opaco. Puede utilizar este identificador en lugar de una ruta de archivo en una `<input>` para probar las cargas de archivos en la aplicación.
