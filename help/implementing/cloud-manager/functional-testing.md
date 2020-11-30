---
title: 'Prueba funcional: Cloud Services'
description: 'Prueba funcional: Cloud Services'
translation-type: tm+mt
source-git-commit: 25ba5798de175b71be442d909ee5c9c37dcf10d4
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 4%

---


# Prueba funcional {#functional-testing}

Las pruebas funcionales se clasifican en dos tipos:

* Prueba funcional del producto
* Prueba funcional personalizada

## Prueba funcional del producto {#product-functional-testing}

Las pruebas funcionales del producto son un conjunto de pruebas de integración HTTP (TI) estables en torno a la funcionalidad básica en AEM (por ejemplo, creación y replicación) que impiden que se implementen los cambios de cliente en el código de la aplicación si rompe esta funcionalidad básica.

Las pruebas funcionales del producto se ejecutan automáticamente cada vez que un cliente implementa un nuevo código en Cloud Manager y no se pueden omitir.

Consulte las pruebas [funcionales](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) del producto para obtener pruebas de muestra.

## Prueba funcional personalizada {#custom-functional-testing}

El paso de prueba funcional personalizada de la canalización siempre está presente y no se puede omitir.

Sin embargo, si la compilación no produce JAR de prueba, la prueba pasa de forma predeterminada.

>[!NOTE]
>El botón **Descargar registro** permite acceder a un archivo ZIP que contiene el formulario detallado de la ejecución de la prueba. Estos registros no incluyen los registros del proceso de tiempo de ejecución de AEM real; se puede acceder a ellos mediante la funcionalidad de los registros de descargas o de colas. Consulte [Acceso y administración de registros](/help/implementing/cloud-manager/manage-logs.md) para obtener más detalles.


### Escritura de pruebas funcionales {#writing-functional-tests}

Las pruebas funcionales escritas por el cliente deben empaquetarse como un archivo JAR independiente producido por la misma compilación Maven que los artefactos que se implementarán en AEM. Generalmente sería un módulo Maven independiente. El archivo JAR resultante debe contener todas las dependencias requeridas y generalmente se crearía usando el complemento maven-assembly-plugin usando el descriptor jar-con-dependencias.

Además, JAR debe tener el encabezado de manifiesto Cloud-Manager-TestType definido en integration-test. En el futuro, se espera que se admitan valores de encabezado adicionales. Una configuración de ejemplo para maven-assembly-plugin es:

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

Dentro de este archivo JAR, los nombres de clase de las pruebas reales que se van a ejecutar deben terminar en TI.

Por ejemplo, se ejecutaría una clase denominada `com.myco.tests.aem.ExampleIT` , pero no una clase denominada `com.myco.tests.aem.ExampleTest` .

Las clases de prueba deben ser pruebas JUnit normales. La infraestructura de prueba está diseñada y configurada para ser compatible con las convenciones utilizadas por la biblioteca de pruebas aem-testing-customers. Se recomienda encarecidamente a los desarrolladores que utilicen esta biblioteca y sigan sus prácticas recomendadas. Consulte [Git Link](https://github.com/adobe/aem-testing-clients) para obtener más detalles.

### Ejecución de pruebas locales {#local-test-execution}

Como las clases de prueba son pruebas JUnit, se pueden ejecutar desde IDE de Java convencionales como Eclipse, IntelliJ, NetBeans, etc.

Sin embargo, al ejecutar estas pruebas, será necesario establecer una serie de propiedades del sistema que esperan los clientes de prueba de problemas (y los clientes de prueba de Sling subyacentes).

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

