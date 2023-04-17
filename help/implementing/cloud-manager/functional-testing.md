---
title: Pruebas funcionales
description: Obtenga información sobre los tres tipos diferentes de pruebas funcionales integradas en el proceso de implementación de AEM as a Cloud Service para garantizar la calidad y fiabilidad de su código.
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: cd0b40ffa54eac0d7488b23329c4d2666c992da7
workflow-type: tm+mt
source-wordcount: '1124'
ht-degree: 100%

---


# Pruebas funcionales {#functional-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="Pruebas funcionales"
>abstract="Obtenga información sobre los tres tipos diferentes de pruebas funcionales integradas en el proceso de implementación de AEM as a Cloud Service para garantizar la calidad y fiabilidad de su código."

Obtenga información sobre los tres tipos diferentes de pruebas funcionales integradas en el [proceso de implementación de AEM as a Cloud Service](/help/implementing/cloud-manager/deploy-code.md) para garantizar la calidad y fiabilidad de su código.

## Información general {#overview}

Hay tres tipos diferentes de pruebas funcionales en AEM as a Cloud Service.

* [Prueba funcional del producto](#product-functional-testing)
* [Prueba funcional personalizada](#custom-functional-testing)
* [Prueba de IU personalizada](#custom-ui-testing)

Para todas las pruebas funcionales, los resultados detallados de las pruebas pueden descargarse como un `.zip` archivo mediante el botón **Descargar registro de generación** en la pantalla de información general de la generación como parte del [proceso de implementación.](/help/implementing/cloud-manager/deploy-code.md)

Estos registros no incluyen los registros del proceso del tiempo de ejecución de AEM real. Para acceder a esos registros, consulte el documento [Acceder y administrar registros](/help/implementing/cloud-manager/manage-logs.md) para obtener más información.

Tanto las pruebas funcionales del producto como las pruebas funcionales personalizadas de ejemplo se basan en la los [clientes de prueba de AEM.](https://github.com/adobe/aem-testing-clients)

### Prueba funcional del producto {#product-functional-testing}

Las pruebas funcionales del producto son un conjunto de pruebas de integración (TI) HTTP estables de funcionalidad central en AEM como las tareas de creación y replicación. Estas pruebas las mantiene Adobe y su objetivo es evitar que se implementen cambios en el código de aplicación personalizado si rompen la funcionalidad principal.

* [Canalizaciones de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md): pruebas funcionales del producto que se ejecutan automáticamente cada vez que implementa un código nuevo en Cloud Manager y no se pueden omitir.
* [Canalizaciones que no son de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md): las pruebas funcionales de producto se pueden seleccionar de forma opcional para que se ejecuten, siempre que ejecute la canalización que no sea de producción.

Las pruebas funcionales del producto se mantienen como un proyecto de código abierto. Consulte [pruebas funcionales del producto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) en GitHub para obtener más información.

### Prueba funcional personalizada {#custom-functional-testing}

Aunque la prueba funcional del producto está definida por Adobe, puede escribir sus propias pruebas de calidad para su propia aplicación. Esto se ejecutará como prueba funcional personalizada como parte de la [canalización de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) o una [canalización que no sea de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) para garantizar la calidad de la aplicación.

Las pruebas funcionales personalizadas se ejecutan tanto para implementaciones de código personalizado como para actualizaciones push, lo que hace especialmente importante escribir buenas pruebas funcionales que eviten que los cambios en el código de AEM rompan el código de la aplicación. El paso de prueba funcional personalizada siempre está presente y no se puede omitir.

### Prueba de IU personalizada {#custom-ui-testing}

La prueba de IU personalizada es una característica opcional que le permite crear y ejecutar automáticamente pruebas de IU para sus aplicaciones. Las pruebas de interfaz de usuario son pruebas basadas en Selenium empaquetadas en una imagen Docker para permitir una amplia variedad de lenguajes y marcos de trabajo como Java y Maven, Node y WebDriver.io, o cualquier otro marco de trabajo y tecnología creados en Selenium.

Consulte el documento [Pruebas de IU personalizadas](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing) para obtener más información.

## Introducción a las pruebas funcionales {#getting-started-functional-tests}

Al crear un nuevo repositorio de código en Cloud Manager, se crea una carpeta `it.tests` automáticamente con casos de prueba de ejemplo.

>[!NOTE]
>
>Si el repositorio se creó antes de que Cloud Manager creara automáticamente carpetas `it.tests`, usted también puede generar la última versión utilizando el [Arquetipo de proyecto de AEM.](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/it.tests)

Una vez que tenga el contenido de la carpeta `it.tests`, puede utilizarlo como base para sus propias pruebas y, a continuación:

1. [Desarrolle sus casos de prueba.](#writing-functional-tests)
1. [Ejecute las pruebas localmente.](#local-test-execution)
1. Confirme su código en el repositorio de Cloud Manager y ejecute una canalización de Cloud Manager.

## Escribir pruebas funcionales personalizadas {#writing-functional-tests}

Las mismas herramientas que utiliza Adobe para escribir pruebas funcionales de productos se pueden usar para escribir las pruebas funcionales personalizadas. Utilice las [pruebas funcionales del producto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) en GitHub como ejemplo de cómo escribir las pruebas.

El código para la prueba funcional personalizada es el código Java ubicado en la carpeta `it.tests` del proyecto. Debe producir un único JAR con todas las pruebas funcionales. Si la generación produce más de un JAR de prueba, el JAR seleccionado no es determinista. Si no produce ningún JAR de prueba, el paso de prueba se aprueba de forma predeterminada. [Consulte el arquetipo del proyecto AEM](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/it.tests) para pruebas de ejemplo.

Las pruebas se ejecutan en una infraestructura de pruebas mantenida por Adobe que incluye al menos dos instancias de autor, dos instancias de publicación y una configuración de Dispatcher. Esto significa que las pruebas funcionales personalizadas se ejecutan con toda la pila de AEM.

### Estructura de pruebas funcionales {#functional-tests-structure}

Las pruebas funcionales personalizadas deben empaquetarse como un archivo JAR independiente producido por la misma generación de Maven que los artefactos que se van a implementar en AEM. Generalmente sería un módulo de Maven separado. El archivo JAR resultante debe contener todas las dependencias requeridas y se crearía generalmente con el `maven-assembly-plugin` `jar-with-dependencies` descriptor.

Además, el JAR debe tener el `Cloud-Manager-TestType` encabezado de manifiesto definido como `integration-test`.

El siguiente es un ejemplo de configuración para el `maven-assembly-plugin`.

```java
<build>
    <plugins>
        <!-- Create self-contained jar with dependencies -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-assembly-plugin</artifactId>
            <version>3.1.0</version>
            <configuration>
                <descriptorRefs>
                    <descriptorRef>jar-with-dependencies</descriptorRef>
                </descriptorRefs>
                <archive>
                    <manifestEntries>
                        <Cloud-Manager-TestType>integration-test</Cloud-Manager-TestType>
                    </manifestEntries>
                </archive>
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
    </plugins>
```

Dentro de este archivo JAR, los nombres de clase de las pruebas reales que se van a ejecutar deben terminar en `IT`.

Por ejemplo, una clase denominada `com.myco.tests.aem.it.ExampleIT` se ejecutaría, pero una clase denominada `com.myco.tests.aem.it.ExampleTest` no.

Además, para excluir el código de prueba de la comprobación de cobertura del análisis de código, el código de prueba debe estar debajo de un paquete denominado `it` (el filtro de exclusión de cobertura es `**/it/**/*.java`).

Las clases de prueba deben ser pruebas JUnit normales. La infraestructura de prueba está diseñada y configurada para ser compatible con las convenciones utilizadas por la `aem-testing-clients` biblioteca de prueba. Se recomienda encarecidamente a los desarrolladores que utilicen esta biblioteca y sigan sus prácticas recomendadas.

Consulte el [`aem-testing-clients` Repositorio de GitHub](https://github.com/adobe/aem-testing-clients) para obtener más información.

>[!TIP]
>
>[Vea este vídeo](https://www.youtube.com/watch?v=yJX6r3xRLHU) sobre cómo puede usar pruebas funcionales personalizadas para mejorar su confianza en sus canalizaciones de CI/CD.

### Ejecución de pruebas locales {#local-test-execution}

Antes de activar pruebas funcionales en una canalización de Cloud Manager, se recomienda ejecutar las pruebas funcionales localmente mediante [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) o una instancia de AEM as a Cloud Service.

#### Requisitos previos {#prerequisites}

Las pruebas en Cloud Manager se ejecutarán con un usuario administrador técnico.

Para ejecutar las pruebas funcionales desde el equipo local, cree un usuario con permisos de tipo administrador para lograr el mismo comportamiento.

#### Ejecutar en un IDE {#running-in-an-ide}

Como las clases de prueba son pruebas JUnit, se pueden ejecutar desde IDE de Java convencionales como Eclipse, IntelliJ y NetBeans. Dado que tanto las pruebas funcionales de producto como las pruebas funcionales personalizadas se basan en la misma tecnología, ambas se pueden ejecutar localmente al copiar las pruebas de producto en las pruebas personalizadas.

Sin embargo, al ejecutar estas pruebas, será necesario establecer una serie de propiedades del sistema que espera el `aem-testing-clients` (y la biblioteca de clientes de prueba de Sling subyacente).

Las propiedades del sistema son las siguientes:

* `sling.it.instances - should be set to 2`
* `sling.it.instance.url.1 - should be set to the author URL, for example, http://localhost:4502`
* `sling.it.instance.runmode.1 - should be set to author`
* `sling.it.instance.adminUser.1 - should be set to the author admin user, for example, admin`
* `sling.it.instance.adminPassword.1 - should be set to the author admin password`
* `sling.it.instance.url.2 - should be set to the publish URL, for example, http://localhost:4503`
* `sling.it.instance.runmode.2 - should be set to publish`
* `sling.it.instance.adminUser.2 - should be set to the publish admin user, for example, admin`
* `sling.it.instance.adminPassword.2 - should be set to the publish admin password`

#### Ejecución de todas las pruebas con Maven {#using-maven}

1. Abra un shell y vaya a la carpeta `it.tests` en el repositorio.

1. Ejecute el siguiente comando proporcionando los parámetros necesarios para iniciar las pruebas con Maven.

```shell
mvn verify -Plocal \
    -Dit.author.url=https://author-<program-id>-<environment-id>.adobeaemcloud.com \
    -Dit.author.user=<user> \
    -Dit.author.password=<password> \
    -Dit.publish.url=https://publish-<program-id>-<environment-id>.adobeaemcloud.com \
    -Dit.publish.user=<user> \
    -Dit.publish.password=<password>
```
