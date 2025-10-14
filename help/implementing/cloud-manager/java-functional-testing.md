---
title: Java &trade; Pruebas funcionales
description: Aprenda a escribir pruebas funcionales de Java &trade; para AEM as a Cloud Service
exl-id: e014b8ad-ac9f-446c-bee8-adf05a6b4d70
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 498a58c89910f41e6b86c5429629ec9282028987
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 78%

---

# Prueba funcional de Java™

Obtenga información sobre cómo escribir pruebas funcionales de Java™ para AEM as a Cloud Service

## Introducción a las pruebas funcionales {#getting-started-functional-tests}

Al crear un nuevo repositorio de código en Cloud Manager, se crea una carpeta `it.tests` automáticamente con casos de prueba de ejemplo.

>[!NOTE]
>
>Si el repositorio se creó antes de que Cloud Manager creara automáticamente carpetas `it.tests`, también puede generar la última versión utilizando el [Arquetipo de proyecto de AEM](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/it.tests).

Una vez que tenga el contenido de la carpeta `it.tests`, puede utilizarlo como base para sus propias pruebas y, a continuación:

1. [Desarrolle sus casos de prueba](#writing-functional-tests).
1. [Ejecute las pruebas localmente](#local-test-execution).
1. Confirme su código en el repositorio de Cloud Manager y ejecute una canalización de Cloud Manager.

## Escribir pruebas funcionales personalizadas {#writing-functional-tests}

Las mismas herramientas que utiliza Adobe para escribir pruebas funcionales de productos se pueden usar para escribir las pruebas funcionales personalizadas. Utilice las [pruebas funcionales del producto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) en GitHub como ejemplo de cómo escribir las pruebas.

El código para la prueba funcional personalizada es el código Java™ ubicado en la carpeta `it.tests` del proyecto. Debe producir un único JAR con todas las pruebas funcionales. Si la generación produce más de un JAR de prueba, el JAR seleccionado no es determinista. Si no produce ningún JAR de prueba, el paso de prueba se aprueba de forma predeterminada. Consulte [Arquetipo de proyecto de AEM](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/it.tests) para ver pruebas de ejemplo.

Las pruebas se ejecutan en una infraestructura de pruebas mantenida por Adobe que incluye al menos dos instancias de autor, dos instancias de publicación y una configuración de Dispatcher. Esta configuración significa que las pruebas funcionales personalizadas se ejecutan con toda la pila de AEM.

### Estructura de pruebas funcionales {#functional-tests-structure}

Las pruebas funcionales personalizadas deben empaquetarse como un archivo JAR independiente producido por la misma generación de Maven que los artefactos que se van a implementar en AEM. Generalmente, esta versión sería un módulo de Maven separado. El archivo JAR resultante debe contener todas las dependencias requeridas y se crearía generalmente con el `maven-assembly-plugin` `jar-with-dependencies` descriptor.

Además, el JAR debe tener el `Cloud-Manager-TestType` encabezado de manifiesto definido como `integration-test`.

El siguiente es un ejemplo de configuración para el `maven-assembly-plugin`.

```XML
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
</build>
```

Dentro de este archivo JAR, los nombres de clase de las pruebas reales que se van a ejecutar deben terminar en `IT`.

Por ejemplo, una clase denominada `com.myco.tests.aem.it.ExampleIT` se ejecutaría, pero una clase denominada `com.myco.tests.aem.it.ExampleTest` no.

Además, para excluir el código de prueba de la comprobación de cobertura del análisis de código, el código de prueba debe estar debajo de un paquete denominado `it` (el filtro de exclusión de cobertura es `**/it/**/*.java`).

Las clases de prueba deben ser JUnit normales. La infraestructura de la prueba está diseñada y configurada para ser compatible con las convenciones utilizadas por la biblioteca de prueba `aem-testing-clients`. Se recomienda a los desarrolladores que utilicen esta biblioteca y sigan sus prácticas recomendadas.

Consulte el [`aem-testing-clients`repositorio de GitHub](https://github.com/adobe/aem-testing-clients) para obtener más información.

>[!TIP]
>
>[Vea este vídeo](https://www.youtube.com/watch?v=yJX6r3xRLHU) sobre cómo puede usar las pruebas funcionales personalizadas para mejorar su confianza en sus canalizaciones de CI/CD.

### Requisitos previos {#prerequisites}

1. Las pruebas en Cloud Manager se ejecutan con un usuario administrador técnico.

>[!NOTE]
>
>Para ejecutar las pruebas funcionales desde el equipo local, cree un usuario con permisos de tipo administrador para lograr el mismo comportamiento.

1. La infraestructura contenerizada que se contempla para las pruebas funcionales está limitada por los siguientes límites:


| Tipo | Valor | Descripción |
|----------------------|-------|--------------------------------------------------------------------|
| CPU | 0,5 | Cantidad de tiempo de CPU reservado por ejecución de prueba |
| Memoria | 0,5Gi | Cantidad de memoria asignada a la prueba, valor en gibibytes. |
| Tiempo de espera | 30 m | Límite de tiempo tras el cual se detiene la prueba. |
| Duración recomendada | 15 m | Adobe recomienda escribir las pruebas para que no tarden más de este tiempo. |

>[!NOTE]
>
> Si necesita más recursos, cree un caso de uso con el Servicio de atención al cliente y descríbalo. El equipo de Adobe revisará su solicitud y proporcionará la asistencia adecuada.

#### Dependencias

* aem-cloud-testing-customers:

Los próximos cambios en la infraestructura en contenedores para ejecutar pruebas funcionales requieren actualizar la biblioteca [aem-cloud-testing-customers](https://github.com/adobe/aem-testing-clients) en sus pruebas funcionales personalizadas a la versión **1.2.1** o superior. Asegúrese de que la dependencia del archivo `it.tests/pom.xml` se actualice en consecuencia.

```
<dependency>
   <groupId>com.adobe.cq</groupId>
   <artifactId>aem-cloud-testing-clients</artifactId>
   <version>1.2.1</version>
</dependency>
```

>[!NOTE]
>
>Este cambio debe realizarse antes del 6 de abril de 2024.
>&#x200B;>No actualizar la biblioteca de dependencias puede provocar errores de canalización en el paso &quot;Pruebas funcionales personalizadas&quot;.

### Ejecución de pruebas locales {#local-test-execution}

Antes de activar pruebas funcionales en una canalización de Cloud Manager, se recomienda ejecutar las pruebas funcionales localmente mediante [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) o una instancia de AEM as a Cloud Service.

#### Ejecutar en un IDE {#running-in-an-ide}

Como las clases de prueba son pruebas JUnit, se pueden ejecutar desde IDE de Java ™ convencionales como Eclipse, IntelliJ y NetBeans. Dado que tanto las pruebas funcionales de producto como las personalizadas se basan en la misma tecnología, ambas se pueden ejecutar localmente al copiar las pruebas de producto en las pruebas personalizadas.

Sin embargo, al ejecutar estas pruebas, será necesario establecer una serie de propiedades del sistema que espera el `aem-testing-clients` (y la biblioteca de clientes de prueba de Sling subyacente).

Las propiedades del sistema son las siguientes:

| Propiedad | Descripción | Ejemplos |
|-------------------------------------|------------------------------------------------------------------|-------------------------|
| `sling.it.instances` | El número de instancias que coinciden con el servicio en la nube debe establecerse en `2`. | `2` |
| `sling.it.instance.url.1` | Se establece en URL del autor. | `http://localhost:4502` |
| `sling.it.instance.runmode.1` | Modo de ejecución de la primera instancia. Establecido en `author`. | `author` |
| `sling.it.instance.adminUser.1` | Se establece en usuario administrador de autor. | `admin` |
| `sling.it.instance.adminPassword.1` | Establezca como contraseña de administrador de autor. |                         |
| `sling.it.instance.url.2` | se establece en publicar URL. | `http://localhost:4503` |
| `sling.it.instance.runmode.2` | Modo de ejecución de la segunda instancia. Establecido en `publish`. | `publish` |
| `sling.it.instance.adminUser.2` | Configúrelo en usuario administrador de publicación. | `admin` |
| `sling.it.instance.adminPassword.2` | Configúrelo en Contraseña de administrador de publicación. |                         |



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

