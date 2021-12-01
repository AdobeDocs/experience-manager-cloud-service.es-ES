---
title: 'Pruebas funcionales: Cloud Services'
description: 'Pruebas funcionales: Cloud Services'
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: 778fa187df675eada645c73911e6f02e8a112753
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 3%

---

# Pruebas funcionales {#functional-testing}


>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="Pruebas funcionales"
>abstract="Las pruebas funcionales se clasifican en tres tipos: Pruebas funcionales del producto, pruebas funcionales personalizadas y pruebas de IU personalizadas"

Las pruebas funcionales se clasifican en tres tipos:


* Prueba funcional del producto
* Pruebas funcionales personalizadas
* Pruebas de IU personalizadas

## Prueba funcional del producto {#product-functional-testing}

Las pruebas funcionales del producto son un conjunto de pruebas de integración HTTP (TI) estables en torno a la funcionalidad principal de AEM (por ejemplo, creación y replicación) que impiden que los cambios del cliente en su código de aplicación se implementen si rompe esta funcionalidad principal.

Las pruebas funcionales de producto se ejecutan automáticamente cada vez que un cliente implementa un nuevo código en Cloud Manager y no se puede omitir.

Consulte [Pruebas funcionales del producto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) para pruebas de ejemplo.

## Pruebas funcionales personalizadas {#custom-functional-testing}

El paso Prueba funcional personalizada de la canalización siempre está presente y no se puede omitir.

La compilación debe producir cero o un JAR de prueba. Si produce JAR de prueba cero, el paso de prueba pasa de forma predeterminada. Si la compilación produce más de un JAR de prueba, el JAR seleccionado no es determinista.

>[!NOTE]
>El botón **Descargar registro** permite acceder a un archivo ZIP que contiene el formulario detallado de la ejecución de la prueba. Estos registros no incluyen los registros del proceso de tiempo de ejecución de AEM real; se puede acceder a ellos mediante la funcionalidad regular Descargar o Registros de cola . Consulte [Acceso y administración de registros](/help/implementing/cloud-manager/manage-logs.md) para obtener más información.


## Escritura de pruebas funcionales {#writing-functional-tests}

Las pruebas funcionales escritas por el cliente deben empaquetarse como un archivo JAR independiente producido por la misma compilación de Maven que los artefactos que se implementarán en AEM. Generalmente sería un módulo Maven separado. El archivo JAR resultante debe contener todas las dependencias requeridas y generalmente se crearía usando el complemento maven-assembly-plugin usando el descriptor jar-with-dependencias.

Además, el JAR debe tener el encabezado de manifiesto Cloud-Manager-TestType establecido en integration-test. En el futuro, se espera que se admitan valores de encabezado adicionales. Un ejemplo de configuración para maven-assembly-plugin es:

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

Las clases de prueba deben ser pruebas JUnit normales. La infraestructura de prueba está diseñada y configurada para ser compatible con las convenciones utilizadas por la biblioteca de prueba aem-testing-client. Se recomienda encarecidamente a los desarrolladores que utilicen esta biblioteca y sigan sus prácticas recomendadas. Consulte [Vínculo de Git](https://github.com/adobe/aem-testing-clients) para obtener más información.

## Ejecución de pruebas locales {#local-test-execution}

Como las clases de prueba son pruebas JUnit, se pueden ejecutar desde IDE de Java convencionales como Eclipse, IntelliJ, NetBeans, etc.

Sin embargo, al ejecutar estas pruebas, será necesario establecer una variedad de propiedades del sistema que esperan los clientes de prueba de aem (y los clientes de prueba de Sling subyacentes).

Las propiedades del sistema son las siguientes:

* `sling.it.instances - should be set to 2`
* `sling.it.instance.url.1 - should be set to the author URL, for example, http://localhost:4502`
* `sling.it.instance.runmode.1 - should be set to author`
* `sling.it.instance.adminUser.1 - should be set to the author admin user, e.g. admin`
* `sling.it.instance.adminPassword.1 - should be set to the author admin password`
* `sling.it.instance.url.2 - should be set to the author URL, for example, http://localhost:4503`
* `sling.it.instance.runmode.2 - should be set to publish`
* `sling.it.instance.adminUser.2 - should be set to the publish admin user, for example, admin`
* `sling.it.instance.adminPassword.2 - should be set to the publish admin password`
