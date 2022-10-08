---
title: Pruebas funcionales
description: Obtenga información sobre los tres tipos diferentes de pruebas funcionales incorporadas en el proceso de implementación as a Cloud Service AEM para garantizar la calidad y fiabilidad de su código.
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 0%

---


# Pruebas funcionales {#functional-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="Pruebas funcionales"
>abstract="Obtenga información sobre los tres tipos diferentes de pruebas funcionales incorporadas en el proceso de implementación as a Cloud Service AEM para garantizar la calidad y fiabilidad de su código."

Obtenga información sobre los tres tipos diferentes de pruebas funcionales integradas en la [AEM proceso de implementación as a Cloud Service](/help/implementing/cloud-manager/deploy-code.md) para garantizar la calidad y fiabilidad de su código.

## Información general {#overview}

Hay tres tipos diferentes de pruebas funcionales en AEM as a Cloud Service.

* [Prueba funcional del producto](#product-functional-testing)
* [Pruebas funcionales personalizadas](#custom-functional-testing)
* [Pruebas de IU personalizadas](#custom-ui-testing)

Para todas las pruebas funcionales, los resultados detallados de las pruebas pueden descargarse como un `.zip` usando la variable **Descargar registro de compilación** en la pantalla de información general de la compilación como parte del [proceso de implementación.](/help/implementing/cloud-manager/deploy-code.md)

Estos registros no incluyen los registros del proceso de tiempo de ejecución de AEM real. Para acceder a esos registros, consulte el documento [Acceso y administración de registros](/help/implementing/cloud-manager/manage-logs.md) para obtener más información.

Tanto las pruebas funcionales del producto como las pruebas funcionales personalizadas de ejemplo se basan en la variable [AEM clientes de prueba.](https://github.com/adobe/aem-testing-clients)

## Prueba funcional del producto {#product-functional-testing}

Las pruebas funcionales del producto son un conjunto de pruebas de integración HTTP (TI) estables de funcionalidad central en AEM como las tareas de creación y replicación. Estas pruebas se mantienen por Adobe y su objetivo es evitar que se implementen cambios en el código de aplicación personalizado si rompe la funcionalidad principal.

Las pruebas funcionales del producto se ejecutan automáticamente cada vez que implementa un nuevo código en Cloud Manager y no se pueden omitir.

Las pruebas funcionales del producto se mantienen como un proyecto de código abierto. Consulte [pruebas funcionales del producto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) en GitHub para obtener más información.

## Pruebas funcionales personalizadas {#custom-functional-testing}

Aunque la prueba funcional del producto está definida por el Adobe, puede escribir sus propias pruebas de calidad para su propia aplicación. Esto se ejecutará como prueba funcional personalizada como parte de la canalización de producción para garantizar la calidad de la aplicación.

Las pruebas funcionales personalizadas se ejecutan tanto para implementaciones de código personalizado como para actualizaciones de push, lo que hace especialmente importante escribir buenas pruebas funcionales que eviten que los cambios en el código de AEM rompan el código de la aplicación. El paso de prueba funcional personalizada siempre está presente y no se puede omitir.

### Escritura de pruebas funcionales personalizadas {#writing-functional-tests}

Las mismas herramientas que utiliza Adobe para escribir pruebas funcionales de productos se pueden usar para escribir las pruebas funcionales personalizadas. Utilice la variable [pruebas funcionales del producto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) en GitHub como ejemplo de cómo escribir las pruebas.

El código para la prueba funcional personalizada es el código Java ubicado en la variable `it.tests` carpeta del proyecto. Debe producir un único JAR con todas las pruebas funcionales. Si la compilación produce más de una prueba JAR, que JAR está seleccionado no es determinista. Si produce JAR de prueba cero, el paso de prueba pasa de forma predeterminada. [Consulte el tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/it.tests) para pruebas de ejemplo.

Las pruebas se ejecutan en una infraestructura de pruebas mantenida por Adobe que incluye al menos dos instancias de autor, dos instancias de publicación y una configuración de Dispatcher. Esto significa que las pruebas funcionales personalizadas se ejecutan con toda la pila de AEM.

Las pruebas funcionales personalizadas deben empaquetarse como un archivo JAR independiente producido por la misma compilación de Maven que los artefactos que se van a implementar en AEM. Generalmente sería un módulo Maven separado. El archivo JAR resultante debe contener todas las dependencias requeridas y se crearía generalmente utilizando la variable `maven-assembly-plugin` usando la variable `jar-with-dependencies` descriptor.

Además, el JAR debe tener el `Cloud-Manager-TestType` encabezado de manifiesto definido como `integration-test`.

A continuación se muestra un ejemplo de configuración para la variable `maven-assembly-plugin`.

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

Dentro de este archivo JAR, los nombres de clase de las pruebas reales que se van a ejecutar deben finalizar en `IT`.

Por ejemplo, una clase denominada `com.myco.tests.aem.it.ExampleIT` se ejecuta, pero una clase denominada `com.myco.tests.aem.it.ExampleTest` no.

Además, para excluir el código de prueba de la comprobación de cobertura del análisis de código, el código de prueba debe estar debajo de un paquete denominado `it` (el filtro de exclusión de cobertura es `**/it/**/*.java`).

Las clases de prueba deben ser pruebas JUnit normales. La infraestructura de prueba está diseñada y configurada para ser compatible con las convenciones utilizadas por el `aem-testing-clients` biblioteca de prueba. Se recomienda encarecidamente a los desarrolladores que utilicen esta biblioteca y sigan sus prácticas recomendadas.

Consulte la [`aem-testing-clients` Repositorio de GitHub](https://github.com/adobe/aem-testing-clients) para obtener más información.

>[!TIP]
>
>[Ver este vídeo](https://www.youtube.com/watch?v=yJX6r3xRLHU) acerca de cómo puede usar pruebas funcionales personalizadas para mejorar su confianza en sus canalizaciones de CI/CD.

## Pruebas de IU personalizadas {#custom-ui-testing}

La prueba de IU personalizada es una función opcional que le permite crear y ejecutar automáticamente pruebas de IU para sus aplicaciones. Las pruebas de interfaz de usuario son pruebas basadas en Selenium empaquetadas en una imagen Docker para permitir una amplia variedad de idiomas y marcos (como Java y Maven, Node y WebDriver.io, o cualquier otro marco y tecnología creados en Selenium).

Consulte el documento [Pruebas de IU personalizadas](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing) para obtener más información.

## Ejecución de pruebas locales {#local-test-execution}

Como las clases de prueba son pruebas JUnit, se pueden ejecutar desde IDE de Java convencionales como Eclipse, IntelliJ, NetBeans, etc. Dado que tanto las pruebas funcionales de producto como las pruebas funcionales personalizadas se basan en la misma tecnología, ambas se pueden ejecutar localmente copiando las pruebas de producto en las pruebas personalizadas.

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
