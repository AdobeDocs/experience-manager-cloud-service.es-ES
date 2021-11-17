---
title: 'Pruebas funcionales: Cloud Services'
description: 'Pruebas funcionales: Cloud Services'
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: 2bb72c591d736dd1fe709abfacf77b02fa195e4c
workflow-type: tm+mt
source-wordcount: '946'
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

## Pruebas de IU personalizadas {#custom-ui-testing}

AEM proporciona a sus clientes un conjunto integrado de puertas de calidad de Cloud Manager para garantizar actualizaciones sin problemas de sus aplicaciones. En particular, las puertas de prueba de TI ya permiten a los clientes crear y automatizar sus propias pruebas que usan API de AEM.

La función de prueba de IU personalizada es una [característica opcional](#customer-opt-in) que permite a nuestros clientes crear y ejecutar automáticamente pruebas de interfaz de usuario para sus aplicaciones. Las pruebas de interfaz de usuario son pruebas basadas en Selenium empaquetadas en una imagen Docker para permitir una amplia variedad de idiomas y marcos (como Java y Maven, Node y WebDriver.io, o cualquier otro marco y tecnología creados en Selenium). Puede obtener más información sobre cómo crear IU y escribir pruebas de IU desde aquí. Además, un proyecto de pruebas de interfaz de usuario se puede generar fácilmente mediante el tipo de archivo del proyecto AEM.

Los clientes pueden crear (a través de GIT) pruebas personalizadas y conjuntos de pruebas para la interfaz de usuario. La prueba de la interfaz de usuario se ejecutará como parte de una puerta de calidad específica para cada canalización de Cloud Manager con su información específica de comentarios y pasos. Cualquier prueba de la interfaz de usuario, incluidas la regresión y las nuevas funcionalidades, permitirá detectar errores y crear informes de ellos en el contexto del cliente.

Las pruebas de la interfaz de usuario del cliente se ejecutan automáticamente en la canalización de producción, en el paso &quot;Pruebas de la interfaz de usuario personalizada&quot;.

A diferencia de las pruebas funcionales personalizadas que son pruebas HTTP escritas en java, las pruebas de interfaz de usuario pueden ser una imagen de docker con pruebas escritas en cualquier idioma, siempre y cuando sigan las convenciones definidas en [Creación de pruebas de interfaz de usuario](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/ui-testing.html?lang=en#building-ui-tests).

>[!NOTE]
>Se recomienda seguir la estructura y el idioma *(js y wdio)* convenientemente provisto en el [Tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests) como punto de partida.

### Inclusión del cliente {#customer-opt-in}

Para crear y ejecutar sus pruebas de interfaz de usuario, los clientes deben &quot;incluirse&quot; añadiendo un archivo a su repositorio de código, en el submódulo maven para pruebas de interfaz de usuario (junto al archivo pom.xml del submódulo de pruebas de interfaz de usuario) y asegurarse de que este archivo esté en la raíz del `tar.gz` archivo.

*Nombre de archivo*: `testing.properties`

*Contenido*: `ui-tests.version=1`

Si no está en la compilación `tar.gz` , la compilación de las pruebas de interfaz de usuario y las ejecuciones se omitirán.

Para agregar `testing.properties` en el artefacto creado, añada un `include` declaración en `assembly-ui-test-docker-context.xml` (en el submódulo Pruebas de interfaz de usuario ):

    &quot;
    [...]
    &lt;includes>
    &lt;include>Archivo de documento&lt;/include>
    &lt;include>wait-for-grid.sh&lt;/include>
    &lt;include>testing.properties&lt;/include> &lt;!>- módulo de prueba de inclusión en Cloud Manager —>
    &lt;/includes>
    [...]
    &quot;

>[!NOTE]
>Las canalizaciones de producción creadas antes del 10 de febrero de 2021 deberán actualizarse para utilizar las pruebas de IU tal como se describe en esta sección. Esto significa que el usuario debe editar la canalización de producción y hacer clic en **Guardar** desde la interfaz de usuario aunque no se hayan realizado cambios.
>Consulte [Configuración de la canalización de CI-CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager) para obtener más información sobre la configuración de la canalización.

### Escritura de pruebas funcionales {#writing-functional-tests}

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

### Ejecución de pruebas locales {#local-test-execution}

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
