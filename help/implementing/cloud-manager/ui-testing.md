---
title: Pruebas de IU
description: La prueba de IU personalizada es una característica opcional que le permite crear y ejecutar automáticamente pruebas de IU para sus aplicaciones personalizadas
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 498a58c89910f41e6b86c5429629ec9282028987
workflow-type: tm+mt
source-wordcount: '2601'
ht-degree: 56%

---


# Pruebas de IU {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="Pruebas de IU"
>abstract="La prueba de IU personalizada es una característica opcional que le permite crear y ejecutar automáticamente pruebas de IU para sus aplicaciones. Las pruebas de interfaz de usuario son pruebas basadas en Selenium empaquetadas en una imagen Docker para permitir una amplia variedad de idiomas y marcos de trabajo. Como Java y Maven, Node y WebDriver.io, o cualquier otro marco de trabajo y tecnología creados en Selenium."

La prueba de IU personalizada es una característica opcional que le permite crear y ejecutar automáticamente pruebas de IU para sus aplicaciones.

## Información general {#custom-ui-testing}

AEM ofrece un conjunto integrado de [Puertas de calidad de Cloud Manager](/help/implementing/cloud-manager/custom-code-quality-rules.md) para garantizar actualizaciones sin problemas en las aplicaciones personalizadas. En concreto, las puertas de pruebas de TI ya admiten la creación y automatización de pruebas personalizadas mediante las API de AEM.

Las pruebas de IU se empaquetan en una imagen Docker para permitir una amplia variedad de lenguajes y marcos de trabajo (como Cypress, Selenium, Java y Maven, y JavaScript). Además, se puede generar fácilmente un proyecto de pruebas de interfaz de usuario utilizando [el arquetipo del proyecto de AEM](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/developing/archetype/overview).

El Adobe fomenta el uso de Cypress, ya que ofrece recarga en tiempo real y espera automática, lo que ayuda a ahorrar tiempo y mejora la productividad durante las pruebas. Cypress también proporciona una sintaxis sencilla e intuitiva, lo que facilita el aprendizaje y el uso, incluso para usuarios que son nuevos en las pruebas.

Las pruebas de interfaz de usuario se ejecutan como una puerta de calidad en el paso [**Pruebas de IU personalizadas**](/help/implementing/cloud-manager/deploy-code.md), necesario en [canalizaciones de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md), opcional en [canalizaciones que no sean de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md). Cualquier prueba de la IU, incluidas la regresión y las nuevas funcionalidades, permite detectar y notificar errores.

A diferencia de las pruebas funcionales personalizadas, que son pruebas HTTP escritas en Java, las pruebas de interfaz de usuario pueden ser una imagen Docker. Las pruebas se pueden escribir en cualquier idioma, siempre y cuando sigan las convenciones definidas en la sección [Pruebas de generación de interfaz de usuario](#building-ui-tests).

>[!TIP]
>
>Adobe recomienda utilizar Cypress para las pruebas de IU, siguiendo el código proporcionado en el [Repositorio de ejemplos de prueba de AEM](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-cypress).
> 
>Adobe también proporciona ejemplos del módulo de prueba de la IU basados en JavaScript con WebdriverIO (consulte el [Tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)) y Java con WebDriver (consulte el [Repositorio de ejemplos de prueba de AEM](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver)).

## Introducción a las pruebas de IU {#get-started-ui-tests}

En esta sección se describen los pasos necesarios para configurar las pruebas de IU para la ejecución en Cloud Manager.

1. Decida el marco de trabajo de prueba que desee utilizar.

   * Para Cypress (predeterminado), usa el código de muestra del [repositorio de muestras de prueba de AEM](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-cypress) o usa el código de muestra que se genera automáticamente en la carpeta `ui.tests` de tu repositorio de Cloud Manager.

   * Para Playwright, usa el código de muestra del [repositorio de muestras de prueba de AEM](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-playwright).

   * Para Webdriver.IO, use el código de ejemplo del [repositorio de muestras de prueba de AEM](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-wdio).

   * Para Selenium WebDriver, use el código de ejemplo del [repositorio de muestras de prueba de AEM](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver).

   * Para otros lenguajes de programación, consulte la sección [Generación de pruebas de IU](#building-ui-tests) en este documento para configurar el proyecto de prueba.

1. Asegúrese de que las pruebas de IU estén activadas según la sección [Inclusión del cliente](#customer-opt-in) de este documento.

1. Desarrolle sus casos de prueba y [ejecute las pruebas localmente](#run-ui-tests-locally).

1. Confirme su código en el repositorio de Cloud Manager y ejecute una canalización de Cloud Manager.

## Generar pruebas de interfaz de usuario {#building-ui-tests}

Un proyecto de Maven genera un contexto de generación de Docker. Este contexto de generación de Docker describe cómo crear una imagen de Docker que contenga las pruebas de IU, que Cloud Manager usa para generar una imagen de Docker que contenga las pruebas de IU reales.

En esta sección se describen los pasos necesarios para agregar un proyecto de pruebas de interfaz de usuario al repositorio.

>[!TIP]
>
>El [Arquetipo de proyecto de AEM](https://github.com/adobe/aem-project-archetype) puede generar un proyecto de pruebas de IU que cumpla con la siguiente descripción, si no tiene requisitos especiales para el lenguaje de programación.

### Generar un contexto de generación de Docker {#generate-docker-build-context}

Para generar un contexto de generación de Docker, necesita un módulo de Maven que:

* Produzca un archivo que contenga un `Dockerfile` y todos los demás archivos necesarios para generar la imagen Docker con sus pruebas.
* Etiqueta el archivo con el clasificador `ui-test-docker-context`.

La forma más sencilla es configurar el [Complemento de Maven Assembly](https://maven.apache.org/plugins/maven-assembly-plugin/) para crear el archivo de contexto de generación de Docker y asignarle el clasificador adecuado.

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

El descriptor de ensamblado indica al complemento que cree un archivo de tipo `.tar.gz` y asigna el clasificador `ui-test-docker-context` para él. Además, enumera los archivos que deben incluirse en el archivo, incluidos los siguientes:

* Un `Dockerfile`, obligatorio para crear la imagen Docker
* El script `wait-for-grid.sh`, cuyos propósitos se describen a continuación
* Las pruebas de interfaz de usuario reales, implementadas por un proyecto Node.js en la carpeta `test-module` 

El descriptor de ensamblado también excluye algunos archivos que podrían generarse al ejecutar las pruebas de IU localmente. Esto garantiza un archivo más pequeño y generaciones más rápidas.

Cloud Manager recoge automáticamente el archivo de contexto de compilación de Docker y crea la imagen de prueba durante las canalizaciones de implementación. Finalmente, Cloud Manager ejecuta la imagen Docker para ejecutar las pruebas de interfaz de usuario contra la aplicación.

La generación debe producir ningún o un archivo. Si no genera ningún archivo, el paso de prueba se aprobará de forma predeterminada. Si la generación produce más de un archivo, qué archivo se seleccione no es determinista.

### Inclusión del cliente {#customer-opt-in}

Para que Cloud Manager pueda generar y ejecutar sus pruebas de IU, debe incluirse en esta funcionalidad al agregar un archivo al repositorio.

* El nombre del archivo debe ser `testing.properties`.
* El contenido del archivo debe ser `ui-tests.version=1`.
* El archivo debe estar en el módulo secundario de Maven para pruebas de IU junto al archivo `pom.xml` del módulo secundario de pruebas de IU.
* El archivo debe estar en la raíz del archivo de generación `tar.gz`.

La generación de pruebas de interfaz de usuario y las ejecuciones se omite si este archivo no está presente.

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
>Si el proyecto no incluye esta línea, edite el archivo para optar por la prueba de IU.
>
>El archivo puede contener una línea que aconseje no editarlo. El motivo es que se está introduciendo en el proyecto antes de que se introdujera la prueba de IU de inclusión y los clientes no tenían la intención de editar el archivo. Puede ignorar con seguridad el aviso.

Si está utilizando las muestras proporcionadas por Adobe:

* Para la carpeta basada en JavaScript `ui.tests` generada a partir del [Arquetipo de proyecto de AEM](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests), puede ejecutar el siguiente comando y añadir la configuración necesaria.

  ```shell
  echo "ui-tests.version=1" > testing.properties
  
  if ! grep -q "testing.properties" "assembly-ui-test-docker-context.xml"; then
    awk -v line='                <include>testing.properties</include>' '/<include>wait-for-grid.sh<\/include>/ { printf "%s\n%s\n", $0, line; next }; 1' assembly-ui-test-docker-context.xml > assembly-ui-test-docker-context.xml.new && mv assembly-ui-test-docker-context.xml.new assembly-ui-test-docker-context.xml
  fi
  ```

* Los ejemplos de prueba de Cypress y Java Selenium proporcionados por Adobe ya tienen el indicador de inclusión establecido.

## Escribir pruebas de interfaz de usuario {#writing-ui-tests}

En esta sección se describen las convenciones que debe seguir la imagen de Docker que contiene las pruebas de IU. La imagen Docker se crea a partir del contexto de generación de Docker descrito en la sección anterior.

### Variables de entorno {#environment-variables}

Las siguientes variables de entorno se pasan a la imagen de Docker en tiempo de ejecución, en función del marco de trabajo.

>[!NOTE]
>
> Estos valores se establecen automáticamente durante la ejecución de la canalización; no es necesario establecerlos manualmente como variables de canalización.

| Variable | Ejemplos | Descripción | Marco trabajo de prueba |
|----------------------------|----------------------------------|----------------------------------------------------------------------------------------------------|---------------------|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | URL del servidor de Selenium | Solo Selenium |
| `SELENIUM_BROWSER` | `chrome` | Implementación del explorador utilizada por el servidor de Selenium | Solo Selenium |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | URL de la instancia de autor de AEM | Todos |
| `AEM_AUTHOR_USERNAME` | `admin` | Nombre de usuario para iniciar sesión en la instancia de autor de AEM | Todos |
| `AEM_AUTHOR_PASSWORD` | `admin` | Contraseña para iniciar sesión en la instancia de autor de AEM | Todos |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | URL de la instancia de publicación de AEM | Todo * |
| `AEM_PUBLISH_USERNAME` | `admin` | Nombre de usuario para iniciar sesión en la instancia de publicación de AEM | Todo * |
| `AEM_PUBLISH_PASSWORD` | `admin` | Contraseña para iniciar sesión en la instancia de publicación de AEM | Todo * |
| `REPORTS_PATH` | `/usr/src/app/reports` | Ruta donde se debe guardar el informe XML de los resultados de la prueba | Todos |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | URL donde se debe cargar el archivo para que sea accesible para el marco de prueba | Todos |
| `PROXY_HOST` | `proxy-host` | Nombre de host del proxy HTTP interno que se utilizará en el marco de prueba | Todos excepto Selenium |
| `PROXY_HTTPS_PORT` | `8071` | Puerto de escucha del servidor proxy para conexiones HTTPS (puede estar vacío) | Todos excepto Selenium |
| `PROXY_HTTP_PORT` | `8070` | Puerto de escucha del servidor proxy para conexiones HTTP (puede estar vacío) | Todos excepto Selenium |
| `PROXY_CA_PATH` | `/path/to/root_ca.pem` | Ruta al certificado de CA que utilizará el marco de pruebas | Todos excepto Selenium |
| `PROXY_OBSERVABILITY_PORT` | `8081` | Puerto HTTP `healthcheck` del servidor proxy | Todos excepto Selenium |
| `PROXY_RETRY_ATTEMPTS` | `12` | Número sugerido de reintentos mientras se espera la preparación del servidor proxy | Todos excepto Selenium |
| `PROXY_RETRY_DELAY` | `5` | Retraso sugerido entre reintentos mientras se espera la preparación del servidor proxy | Todos excepto Selenium |

`* these values will be empty if there is no publish instance`

Las muestras de prueba de Adobe proporcionan funciones de ayuda para acceder a los parámetros de configuración:

Cypress: utilizar la función estándar `Cypress.env('VARIABLE_NAME')`
<!-- BOTH URLs are 404 JavaScript: See the [`lib/config.js`](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests.wdio/test-module/lib/config.js) module
* Java: See the [`Config`](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/Config.java) class -->

### Generar informes de prueba {#generate-test-reports}

La imagen Docker debe generar informes de prueba en formato XML JUnit y guardarlos en la ruta especificada por la variable de entorno `REPORTS_PATH`. El formato JUnit XML es un formato ampliamente utilizado para la creación de informes sobre los resultados de las pruebas. Si la imagen Docker utiliza Java y Maven, los módulos de prueba estándar como el [complemento de Maven Surefire](https://maven.apache.org/surefire/maven-surefire-plugin/) y el [complemento de Maven Failesafe](https://maven.apache.org/surefire/maven-failsafe-plugin/) pueden generar estos informes de forma predeterminada.

Si la imagen Docker está implementada con otros lenguajes de programación o ejecutores de prueba, compruebe la documentación de las herramientas seleccionadas para generar informes XML de JUnit.

>[!NOTE]
>
>El resultado del paso de prueba de la IU solo se evalúa en función de los informes de prueba. Asegúrese de generar el informe correspondiente para la ejecución de la prueba.
>
>Utilice aserciones en lugar de registrar un error en STDERR o devolver un código de salida distinto de cero; para que la canalización de implementación pueda continuar normalmente.
>
>Si se utilizó un proxy HTTP durante la ejecución de pruebas, los resultados incluyen un archivo `request.log`.

### Requisitos previos {#prerequisites}

* Las pruebas en Cloud Manager se ejecutan con un usuario administrador técnico.

>[!NOTE]
>
>Para ejecutar las pruebas funcionales desde el equipo local, cree un usuario con permisos de tipo administrador para lograr el mismo comportamiento.

* La infraestructura contenerizada que se contempla para las pruebas funcionales está limitada por los siguientes límites:

| Tipo | Valor | Descripción |
|----------------------|-------|-----------------------------------------------------------------------|
| CPU | 2.0 | Cantidad de tiempo de CPU reservado por ejecución de prueba. |
| Memoria | 1Gi | Cantidad de memoria asignada a la prueba. El valor está en gibibytes. |
| Tiempo de espera | 30m | Cuánto tiempo dura la prueba. |
| Duración recomendada | 15m | Adobe recomienda mantener las pruebas por debajo de este límite de tiempo. |

>[!NOTE]
>
> Si necesita más recursos, cree un caso de servicio de atención al cliente y describa su caso de uso; Adobe revisa su solicitud y proporciona la asistencia adecuada.

## Detalles específicos de Selenium

>[!NOTE]
>
>Esta sección solo se aplica cuando Selenium es la infraestructura de prueba elegida.

### Esperando a que Selenium esté listo {#waiting-for-selenium}

Antes de que comiencen las pruebas, es responsabilidad de la imagen Docker asegurarse de que el servidor Selenium funcione. Esperar por el servicio de Selenium es un proceso de dos pasos.

1. Lea la URL del servicio de Selenium desde la `SELENIUM_BASE_URL` variable de entorno.
1. Encuesta a intervalos regulares al [extremo de estado](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready) expuesto por la API de Selenium.

Una vez que el extremo de estado de Selenium dé una respuesta positiva, las pruebas podrán comenzar.

Las muestras de prueba de IU de Adobe utilizan `wait-for-grid.sh`. Se ejecuta al inicio de Docker y ejecuta pruebas solo después de que la cuadrícula esté lista.


### Captura de pantallas y vídeos {#capture-screenshots}

La imagen del Docker puede generar resultados de prueba adicionales (por ejemplo, capturas de pantalla o vídeos) y guardarlos en la ruta especificada por la variable de entorno `REPORTS_PATH`. Cualquier archivo que se encuentre debajo de `REPORTS_PATH` se incluirá en el archivo de resultados de la prueba.

Las muestras de prueba proporcionadas por Adobe de forma predeterminada crean capturas de pantalla para cualquier prueba fallida.

Puede utilizar las funciones de ayuda para crear capturas de pantalla a través de las pruebas.

<!-- BOTH URLS ARE 404
* JavaScript: [takeScreenshot command](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/commons.js)
* Java: [Commands](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/Commands.java) -->

Si se crea un archivo de resultados de prueba durante la ejecución de una prueba de IU, puede descargarlo desde Cloud Manager si hace clic en el botón `Download Details` en el paso [**Pruebas de IU personalizadas**](/help/implementing/cloud-manager/deploy-code.md).

### Cargar archivos {#upload-files}

Las pruebas a veces deben cargar archivos en la aplicación que se está probando. Para que la implementación de Selenium sea flexible con respecto a sus pruebas, no es posible cargar un recurso directamente en Selenium. En su lugar, la carga de un archivo requiere los siguientes pasos.

1. Cargue el archivo en la dirección URL especificada por la `UPLOAD_URL` variable de entorno.
   * La carga debe realizarse en una solicitud de POST con un formulario de varias partes.
   * El formulario de varias partes debe tener un único campo de archivo.
   * Equivalente a `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`.
   * Consulte la documentación y las bibliotecas del lenguaje de programación utilizado en la imagen Docker para saber cómo realizar una solicitud HTTP de este tipo.

   <!-- BOTH URLS ARE 404
   * The Adobe test samples provide helper functions for uploading files:
     * JavaScript: See the [getFileHandleForUpload](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/wdio.commands.js) command.
     * Java: See the [FileHandler](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/FileHandler.java) class. -->

1. Si la carga se realiza correctamente, la solicitud devolverá una `200 OK` respuesta del tipo `text/plain`.
   * El contenido de la respuesta es un controlador de archivo opaco.
   * Puede utilizar este identificador en lugar de una ruta de archivo en un elemento `<input>` para probar la carga de archivos en la aplicación.

## Detalles específicos de Cypress

>[!NOTE]
>
>Esta sección solo se aplica cuando Cypress es la infraestructura de prueba elegida.

### Configuración del proxy HTTP

El punto de entrada del contenedor Docker debe comprobar el valor de la variable de entorno `PROXY_HOST`.

Si este valor está vacío, no se requieren pasos adicionales y las pruebas deben ejecutarse sin utilizar un proxy HTTP.

Si no está vacío, el script de punto de entrada debe hacer lo siguiente:

1. Configure una conexión proxy HTTP para ejecutar pruebas de interfaz de usuario exportando la variable de entorno `HTTP_PROXY` creada con los siguientes valores:
   * Host de proxy proporcionado por la variable `PROXY_HOST`
   * Puerto del proxy proporcionado por la variable `PROXY_HTTPS_PORT` o `PROXY_HTTP_PORT` (se utiliza la variable con un valor que no está vacío)
2. Establezca el certificado de CA que se utiliza al conectarse al proxy HTTP. Su ubicación la proporciona la variable `PROXY_CA_PATH`.
   * Exportar `NODE_EXTRA_CA_CERTS` variable de entorno.
3. Espere hasta que el proxy HTTP esté listo.
   * Para comprobar la preparación, se pueden utilizar las variables de entorno `PROXY_HOST`, `PROXY_OBSERVABILITY_PORT`, `PROXY_RETRY_ATTEMPTS` y `PROXY_RETRY_DELAY`.
   * Puede comprobarlo usando una solicitud cURL, asegurándose de instalar cURL en su `Dockerfile`.

Se puede encontrar una implementación de ejemplo en el punto de entrada del módulo de prueba de muestra de Cypress en [GitHub](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-cypress/test-module/run.sh).

## Detalles específicos del dramaturgo

>[!NOTE]
>
> Esta sección solo se aplica cuando `Playwright` es la infraestructura de prueba elegida.

### Configuración del proxy HTTP

>[!NOTE]
>
> En los ejemplos presentados, Adobe supone que Chrome se está utilizando como explorador de proyectos.

De forma similar a Cypress, las pruebas deben utilizar el proxy HTTP si se proporciona una variable de entorno `PROXY_HOST` que no esté vacía.

En tal caso, es necesario realizar las siguientes ediciones.

#### Dockerfile

Instale cURL y `libnss3-tools`, que proporciona `certutil.`

```dockerfile
RUN apt -y update \
    && apt -y --no-install-recommends install curl libnss3-tools \
    && rm -rf /var/lib/apt/lists/*
```

#### Script Entrypoint

Incluya un script bash que, en caso de que se proporcione la variable de entorno `PROXY_HOST`, haga lo siguiente:

1. Exportar variables relacionadas con proxy como `HTTP_PROXY` y `NODE_EXTRA_CA_CERTS`
2. Use `certutil` para instalar el certificado de CA proxy para Chromium™.
3. Espere hasta que el proxy HTTP esté listo (o salga si hay algún error).

Ejemplo de implementación:

```bash
# setup proxy environment variables and CA certificate
if [ -n "${PROXY_HOST:-}" ]; then
  if [ -n "${PROXY_HTTPS_PORT:-}" ]; then
    export HTTP_PROXY="https://${PROXY_HOST}:${PROXY_HTTPS_PORT}"
  elif [ -n "${PROXY_HTTP_PORT:-}" ]; then
    export HTTP_PROXY="http://${PROXY_HOST}:${PROXY_HTTP_PORT}"
  fi
  if [ -n "${PROXY_CA_PATH:-}" ]; then
    echo "installing certificate"
    mkdir -p $HOME/.pki/nssdb
    certutil -d sql:$HOME/.pki/nssdb -A -t "CT,c,c" -n "EaaS Client Proxy Root" -i $PROXY_CA_PATH
    export NODE_EXTRA_CA_CERTS=${PROXY_CA_PATH}
  fi
  if [ -n "${PROXY_OBSERVABILITY_PORT:-}" ] && [ -n "${HTTP_PROXY:-}" ]; then
    echo "waiting for proxy"
    curl --silent  --retry ${PROXY_RETRY_ATTEMPTS:-3} --retry-connrefused --retry-delay ${PROXY_RETRY_DELAY:-10} \
      --proxy ${HTTP_PROXY} --proxy-cacert ${PROXY_CA_PATH:-""} \
      ${PROXY_HOST}:${PROXY_OBSERVABILITY_PORT}
    if [ $? -ne 0 ]; then
      echo "proxy is not ready"
      exit 1
    fi
  fi
fi
```

#### Configuración del dramaturgo

Modifique la configuración del dramaturgo (por ejemplo, en `playwright.config.js`) para utilizar un proxy en caso de que se establezca la variable de entorno `HTTP_PROXY`.

Ejemplo de implementación:

```javascript
const proxyServer = process.env.HTTP_PROXY || ''
```

```javascript
// enable proxy if set
if (proxyServer !== '') {
 cfg.use.proxy = {
  server: proxyServer,
 }
}
```

>[!NOTE]
>
> Se puede encontrar una implementación de ejemplo en el módulo de prueba de muestra del dramaturgo en [GitHub](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-playwright).


## Ejecución de pruebas de IU locales {#run-ui-tests-locally}

Antes de activar las pruebas de IU en una canalización de Cloud Manager, Adobe recomienda ejecutar las pruebas de IU localmente en [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md). O bien, ejecútelo con una instancia real de AEM as a Cloud Service.

### Ejemplo de prueba de Cypress {#cypress-sample}

1. Abra un elemento shell y vaya a la carpeta `ui.tests/test-module` de su repositorio

1. Instalar Cypress y otros requisitos previos

   ```shell
   npm install
   ```

1. Establecer las variables de entorno necesarias para la ejecución de pruebas

   ```shell
   export AEM_AUTHOR_URL=https://author-<program-id>-<environment-id>.adobeaemcloud.com
   export AEM_AUTHOR_USERNAME=<user>
   export AEM_AUTHOR_PASSWORD=<password>
   export AEM_PUBLISH_URL=https://publish-<program-id>-<environment-id>.adobeaemcloud.com
   export AEM_PUBLISH_USERNAME=<user>
   export AEM_PUBLISH_PASSWORD=<password>
   export REPORTS_PATH=target/
   ```

1. Ejecute las pruebas con uno de los siguientes comandos

   ```shell
   npm test              # Using default Cypress browser
   npm run test-chrome   # Using Google Chrome browser
   npm run test-firefox  # Using Firefox browser
   ```

>[!NOTE]
>
>Los archivos de registro se almacenan en la carpeta `target/` del repositorio.
>
>Para obtener más información, consulte [Repositorio de muestras de pruebas de AEM](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-cypress/test-module/README.md).

### Muestra de prueba de WebdriverIO de JavaScript {#javascript-sample}

1. Abra un shell y vaya a la carpeta `ui.tests` en el repositorio.

1. Ejecute el siguiente comando para iniciar las pruebas con Maven.

   ```shell
   mvn verify -Pui-tests-local-execution \
    -DAEM_AUTHOR_URL=https://author-<program-id>-<environment-id>.adobeaemcloud.com \
    -DAEM_AUTHOR_USERNAME=<user> \
    -DAEM_AUTHOR_PASSWORD=<password> \
    -DAEM_PUBLISH_URL=https://publish-<program-id>-<environment-id>.adobeaemcloud.com \
    -DAEM_PUBLISH_USERNAME=<user> \
    -DAEM_PUBLISH_PASSWORD=<password>
   ```

>[!NOTE]
>
>* Este comando inicia una instancia independiente de Selenium y ejecuta las pruebas correspondientes.
>* Los archivos de registro se almacenan en la carpeta `target/reports` de su repositorio
>* Debe asegurarse de que tiene la última versión de Chrome, ya que la prueba descarga la última versión de ChromeDriver automáticamente para realizar pruebas.
>
>Para obtener más información, consulte [Repositorio de muestras de pruebas de AEM](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-wdio).

### Muestra de prueba de Playwright {#playwright-sample}

1. Abra un elemento shell y vaya a la carpeta `ui.tests` de su repositorio

1. Ejecute el siguiente comando para crear una imagen de docker con Maven

   ```shell
   mvn clean package -Pui-tests-docker-build
   ```

1. Ejecute el siguiente comando para iniciar las pruebas con Maven

   ```shell
   mvn verify -Pui-tests-docker-execution \
    -DAEM_AUTHOR_URL=https://author-<program-id>-<environment-id>.adobeaemcloud.com \
    -DAEM_AUTHOR_USERNAME=<user> \
    -DAEM_AUTHOR_PASSWORD=<password> \
    -DAEM_PUBLISH_URL=https://publish-<program-id>-<environment-id>.adobeaemcloud.com \
    -DAEM_PUBLISH_USERNAME=<user> \
    -DAEM_PUBLISH_PASSWORD=<password>
   ```

>[!NOTE]
>
>Los archivos de registro se almacenan en la carpeta `target/` del repositorio.
>
>Para obtener más información, consulte [Repositorio de muestras de pruebas de AEM](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-playwright).


### Ejemplo de prueba de Java Selenium WebDriver {#java-sample}

1. Abra un elemento shell y vaya a la carpeta `ui.tests/test-module` de su repositorio

1. Ejecute el siguiente comando para iniciar las pruebas con Maven

   ```shell
   # Start selenium docker image
   # we mount /tmp/shared as a shared volume that will be used between selenium and the test module for uploads
   docker run -d -p 4444:4444 -v /tmp/shared:/tmp/shared selenium/standalone-chromium:latest
   
   # Run the tests using the previously started Selenium instance
   mvn verify -Pui-tests-local-execution -DSELENIUM_BASE_URL=http://<server>:4444
   ```

>[!NOTE]
>
>Los archivos de registro se almacenan en la carpeta `target/reports` del repositorio.
>
>Para obtener más información, consulte [Repositorio de muestras de pruebas de AEM](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/README.md).
