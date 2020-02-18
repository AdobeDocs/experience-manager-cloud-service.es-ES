---
title: 'Comprender los resultados de la prueba: servicios de nube'
description: 'Comprender los resultados de la prueba: servicios de nube'
translation-type: tm+mt
source-git-commit: e1504c73e443d449f8fc9d5fbad433ea1a298843

---


# Comprender los resultados de la prueba {#understand-test-results}

Las ejecuciones de canalizaciones de Cloud Manager para servicios de nube admitirán la ejecución de pruebas que se ejecuten en el entorno de ensayo. Esto contrasta con las pruebas que se ejecutan durante el paso Generar y Prueba de unidades que se ejecutan sin conexión, sin acceso a ningún entorno AEM en ejecución.
Existen dos tipos de pruebas ejecutadas en este contexto:
* Pruebas escritas por el cliente
* Pruebas escritas por Adobe

Ambos tipos de pruebas se ejecutan en una infraestructura de contenedores diseñada para ejecutar estos tipos de pruebas.


## Prueba de calidad del código {#code-quality-testing}

Como parte de la canalización, se analiza el código fuente para asegurarse de que las implementaciones cumplen determinados criterios de calidad. Actualmente, esto se implementa mediante una combinación de SonarQube y un examen a nivel de paquete de contenido con OakPAL. Existen más de 100 reglas que combinan reglas genéricas de Java y reglas específicas de AEM. La siguiente tabla resume la clasificación para los criterios de prueba:

| Nombre | Definición | Categoría | Umbral de error |
|--- |--- |--- |--- |
| Clasificación de seguridad | A = 0 Vulnerabilidad <br/>B = al menos 1 vulnerabilidad<br/> menor C = al menos 1 vulnerabilidad grave <br/>D = al menos 1 vulnerabilidad crítica <br/>E = al menos 1 vulnerabilidad de bloqueador | Crítico | &lt; B |
| Clasificación de confiabilidad | A = 0 Error <br/>B = al menos 1 Error menor <br/>C = al menos 1 Error mayor <br/>D = al menos 1 Error crítico E = al menos 1 Error de bloqueo | Importante | &lt; C |
| Clasificación de mantenimiento | El costo de corrección sobresaliente de los olores de código es: <br/><ul><li>&lt;=5% del tiempo que ya ha pasado a la aplicación, la clasificación es A </li><li>entre el 6 y el 10 % la calificación es B </li><li>entre el 11 y el 20 % la calificación es una C </li><li>entre el 21 y el 50 % la calificación es una D</li><li>cualquier cosa superior al 50% es una E</li></ul> | Importante | &lt; A |
| Cobertura | Combinación de cobertura de la línea de prueba unitaria y cobertura de condición mediante esta fórmula: <br/>`Coverage = (CT + CF + LC)/(2*B + EL)` donde <br/>: CT = condiciones que se han evaluado en &#39;true&#39; al menos una vez mientras se ejecutan las pruebas unitarias <br/>CF = condiciones que se han evaluado en &#39;false&#39; al menos una vez mientras se ejecutan las pruebas unitarias <br/>LC = líneas cubiertas = líneas_to_cover - líneasdescubiertas <br/><br/> B = número total de condiciones <br/>EL = número total de líneas ejecutables (lines_to_cover) | Importante | &lt; 50% |
| Pruebas unitarias omitidas | Número de pruebas unitarias omitidas. | Información | > 1 |
| Problemas abiertos | Tipos de problemas generales: Vulnerabilidades, errores y huecos de código | Información | > 1 |
| Líneas duplicadas | Número de líneas involucradas en bloques duplicados. <br/>Para que un bloque de código se considere como duplicado: <br/><ul><li>**Proyectos que no son de Java:**</li><li>Debe haber al menos 100 tokens sucesivos y duplicados.</li><li>Estos tokens deben propagarse al menos en: </li><li>30 líneas de código para COBOL </li><li>20 líneas de código para ABAP </li><li>10 líneas de código para otros idiomas</li><li>**Proyectos de Java:**</li><li> Debe haber al menos 10 declaraciones sucesivas y duplicadas, independientemente del número de tokens y líneas.</li></ul> <br/>Las diferencias en sangría y en literales de cadena se omiten al detectar duplicaciones. | Información | > 1% |


>[!NOTE]
>
>Consulte Definiciones [de métricas](https://docs.sonarqube.org/display/SONAR/Metric+Definitions) para obtener definiciones más detalladas.

Puede descargar la lista de reglas aquí [code-quality-rules.xlsx](/help/implementing/cloud-manager/assets/CodeQuality-Rules-new-one.xlsx)

>[!NOTE]
>
>Para obtener más información sobre las reglas de calidad de código personalizadas ejecutadas por [!UICONTROL Cloud Manager], consulte Reglas [de calidad de código](/help/implementing/cloud-manager/custom-code-quality-rules.md)personalizado.

### Tratar con falsos positivos {#dealing-with-false-positives}

El proceso de análisis de calidad no es perfecto y a veces identifica incorrectamente problemas que no son realmente problemáticos. Esto se denomina &quot;falso positivo&quot;.

En estos casos, el código fuente se puede anotar con la anotación estándar de Java `@SuppressWarnings` que especifica el ID de la regla como el atributo de anotación. Por ejemplo, un problema común es que la regla SonarQube para detectar contraseñas codificadas puede ser agresiva sobre cómo se identifica una contraseña codificada.

Para ver un ejemplo específico, este código sería bastante común en un proyecto de AEM que tiene código para conectarse a algún servicio externo:

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

SonarQube generará una vulnerabilidad de bloqueador. Después de revisar el código, se identifica que no se trata de una vulnerabilidad y se puede anotar con la identificación de regla adecuada.

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

Sin embargo, por otro lado, si el código era en realidad esto:

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

A continuación, la solución correcta es quitar la contraseña codificada.

>[!NOTE]
>
>Si bien es recomendable que la anotación sea lo más específica posible, es decir, que solo haga una anotación de la sentencia o bloque específico que causa el problema, es posible realizar anotaciones a nivel de clase. `@SuppressWarnings`

## Escritura de pruebas funcionales {#writing-functional-tests}

Las pruebas funcionales escritas por el cliente deben empaquetarse como un archivo JAR independiente producido por la misma compilación Maven que los artefactos que se implementarán en AEM. Generalmente sería un módulo Maven independiente. El archivo JAR resultante debe contener todas las dependencias requeridas y generalmente se crearía usando el complemento maven-assembly-plugin usando el descriptor jar-con-dependencias.

Además, JAR debe tener el encabezado de manifiesto Cloud-Manager-TestType establecido en integration-test. En el futuro, se espera que se admitan valores de encabezado adicionales. Una configuración de ejemplo para maven-assembly-plugin es:

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

## Prueba funcional personalizada {#custom-functional-test}

El paso de prueba funcional personalizada de la canalización siempre está presente y no se puede omitir.

Sin embargo, si la compilación no produce JAR de prueba, la prueba pasa de forma predeterminada. Este paso se realiza inmediatamente después de la implementación de la etapa.

>[!NOTE]
>El botón **Descargar registro** permite acceder a un archivo ZIP que contiene los registros del formulario detallado de ejecución de la prueba. Estos registros no incluyen los registros del proceso de tiempo de ejecución real de AEM; se puede acceder a ellos mediante la funcionalidad de registro de descargas o de cola habitual. Consulte [Acceso y administración de registros](/help/implementing/cloud-manager/manage-logs.md) para obtener más detalles.

## Ejecución de pruebas locales {#local-test-execution}

Como las clases de prueba son pruebas JUnit, se pueden ejecutar desde IDE de Java convencionales como Eclipse, IntelliJ, NetBeans, etc.

Sin embargo, al ejecutar estas pruebas necesariamente, será necesario establecer una variedad de propiedades del sistema que esperan los clientes de prueba de aem (y los clientes de prueba de Sling subyacentes).

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