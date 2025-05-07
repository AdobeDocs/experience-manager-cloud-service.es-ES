---
title: Entorno de compilación de Cloud Manager
description: Obtenga información sobre el entorno de compilación de Cloud Manager y cómo crea y prueba su código.
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f102cdbab6b38ffabc370691e507754227b91f4e
workflow-type: tm+mt
source-wordcount: '1595'
ht-degree: 28%

---


# Entorno de compilación {#build-environment}

Obtenga información sobre el entorno de compilación de Cloud Manager y cómo crea y prueba su código.

>[!TIP]
>
>Este documento cubre el entorno de compilación de Cloud Manager para desarrollar su proyecto de AEM as a Cloud Service. Para obtener más información acerca de las plataformas cliente compatibles con AEM as a Cloud Service para la creación de contenido, consulte el documento [Plataformas de cliente compatibles.](/help/overview/supported-platforms.md)

## Generar detalles del entorno {#build-environment-details}

Cloud Manager crea y prueba su código mediante un entorno de compilación especializado.

* El entorno de compilación está basado en Linux, derivado de Ubuntu 22.04.
* Apache Maven 3.9.4 está instalado.
   * Adobe recomienda [actualizar los repositorios de Maven para que utilicen HTTPS en lugar de HTTP](#https-maven).
<!-- OLD Removed 1/16/25 * The Java versions installed are Oracle JDK 11.0.22 and Oracle JDK 8u401. -->
* Las versiones de Java instaladas son Oracle JDK 11.0.22, Oracle JDK 17.0.10 y Oracle JDK 21.0.4.

<!-- OLD Removed 1/16/25 * **IMPORTANT:** By default, the JAVA_HOME environment variable is set to `/usr/lib/jvm/jdk1.8.0_401`, which contains Oracle JDK 8u401. This default should be overridden for AEM Cloud Projects to use JDK 11. See the Setting the Maven JDK Version section for more details. -->
* **IMPORTANTE:** De forma predeterminada, la variable de entorno `JAVA_HOME` está configurada en `/usr/lib/jvm/jdk1.8.0_401`, que contiene Oracle JDK 8u401. ***Este valor predeterminado debe anularse para que los proyectos de AEM Cloud utilicen JDK 21 (preferido), 17 o 11***. Consulte la sección [Configuración de la versión del JDK de Maven](#alternate-maven-jdk-version) para obtener más información.
* Hay algunos paquetes de sistema adicionales instalados que son necesarios.
   * `bzip2`
   * `unzip`
   * `libpng`
   * `imagemagick`
   * `graphicsmagick`
* Se pueden instalar otros paquetes en el momento de la compilación, tal como se describe en la sección [Instalación de paquetes de sistema adicionales](#installing-additional-system-packages).
* Cada compilación se ejecuta en un entorno limpio, y el contenedor de compilación no mantiene ningún estado entre ejecuciones.
* Maven siempre se ejecuta con los tres comandos siguientes.
   * `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
   * `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
   * `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent package`
* Maven se configura a nivel de sistema con un archivo `settings.xml`, que incluye automáticamente el repositorio de artefactos de Adobe público usando un perfil denominado `adobe-public`. (Consulte [Repositorio Maven público de Adobe](https://repo1.maven.org/) para obtener más información).

>[!NOTE]
>
>Cloud Manager no especifica una versión específica de `jacoco-maven-plugin`, pero la versión requerida depende de la versión Java del proyecto. Para Java 8, la versión del complemento debe ser al menos `0.7.5.201505241946`, mientras que las versiones más recientes de Java pueden requerir una versión más reciente.

## Repositorios de Maven HTTPS {#https-maven}

Cloud Manager [versión 2023.10.0](/help/implementing/cloud-manager/release-notes/2023/2023-10-0.md) inició una actualización móvil del entorno de compilación (que finalizó con la versión 2023.12.0), que incluía una actualización a Maven 3.8.8. Un cambio significativo introducido en Maven 3.8.1 ha sido una mejora de la seguridad destinada a mitigar posibles vulnerabilidades. En concreto, Maven ahora deshabilita de forma predeterminada todas las duplicaciones de `http://*` inseguras, tal como se describe en las [Notas de la versión de Maven](http://maven.apache.org/docs/3.8.1/release-notes.html#cve-2021-26291).

Como resultado de esta mejora de seguridad, algunas personas pueden tener problemas durante el paso de compilación, especialmente al descargar artefactos de repositorios Maven que utilizan conexiones HTTP no seguras.

Para garantizar una experiencia sin problemas con la versión actualizada, Adobe recomienda actualizar los repositorios de Maven para que utilicen HTTPS en lugar de HTTP. Este ajuste se ha llevado a cabo para adaptarse a la adopción creciente de la industria de protocolos de comunicación seguros y ayuda a mantener un proceso de compilación seguro y fiable.

<!-- OLD below Removed 1/16/25

### Use a specific Java version

The Cloud Manager build process uses the Oracle 8 JDK to build projects by default, but AEM Cloud Service customers should set the Maven execution JDK version to 11. -->

<!-- OLD below Removed 1/16/25

#### Set the Maven JDK version

Adobe recommends that you set the JDK version for the entire Maven execution to `11` in a `.cloudmanager/java-version file`.

To do so, create a file named `.cloudmanager/java-version` in the git repository branch used by the pipeline. Edit the file so that it contains only the text, `11`. While Cloud Manager also accepts a value of `8`, this version is no longer supported for AEM Cloud Service projects. Any other value is ignored. When `11` is specified, Oracle 11 is used and the `JAVA_HOME` environment variable is set to `/usr/lib/jvm/jdk-11.0.22`. -->

### Utilizar una versión de Java específica {#using-java-support}

El proceso de generación de Cloud Manager utiliza el JDK de Oracle 8 para generar proyectos de forma predeterminada, pero los clientes de AEM Cloud Service deben establecer la versión del JDK de ejecución de Maven en 21 (preferido), 17 u 11.

#### Establezca la versión de Maven JDK {#alternate-maven-jdk-version}

Para establecer el JDK de ejecución de Maven, cree un archivo con el nombre `.cloudmanager/java-version` en la rama del repositorio Git utilizada por la canalización. Edite el archivo de modo que contenga solamente el texto `21` o `17`. Aunque Cloud Manager también acepta un valor de `8`, esta versión ya no es compatible con proyectos de AEM Cloud Service. Se ignora cualquier otro valor. Cuando se especifica `21` o `17`, se utiliza Oracle Java 21 o Oracle Java 17.


#### Requisitos previos para migrar a la creación con Java 21 o Java 17 {#prereq-for-building}

Para compilar con Java 21 o Java 17, Cloud Manager ahora utiliza SonarQube 9.9, que es compatible con estas versiones de Java. Este cambio se introdujo en la versión 2025.1.0 de Cloud Manager. No se requiere ninguna acción del cliente para actualizar SonarQube. Para obtener más información y comprender el cambio, consulte las [Notas de la versión para Cloud Manager 2025.1.0](/help/implementing/cloud-manager/release-notes/2025/2025-1-0.md).

Al migrar la aplicación a una nueva versión de compilación de Java y de tiempo de ejecución, realice pruebas exhaustivas en los entornos de desarrollo y ensayo antes de su implementación en producción.

Adobe recomienda la siguiente estrategia de implementación:

1. Ejecute su SDK local con Java 21, que puede descargar de https://experience.adobe.com/#/downloads, e implemente su aplicación en él y valide su funcionalidad. Compruebe en los registros que no hay errores, lo que indica problemas con la carga de clases o el tejido de código de bytes.
1. Configure una rama en el repositorio de Cloud Manager para utilizar Java 21 como la versión de Java en tiempo de compilación, configure una canalización de DEV para utilizar esta rama y ejecute la canalización. Ejecute las pruebas de validación.
1. Si tiene buen aspecto, configure la canalización de fase/producción para utilizar Java 21 como la versión de Java en tiempo de compilación y ejecute la canalización.

##### Acerca de algunas funciones de traducción {#translation-features}

Es posible que las siguientes funciones no funcionen correctamente cuando se implementan en el tiempo de ejecución de Java 21 y Adobe espera resolverlas a principios de 2025:

* `XLIFF` (formato de archivo de intercambio de localización XML) produce un error al utilizar la traducción humana.
* `I18n` (internacionalización) no administra correctamente las configuraciones regionales de idioma hebreo (`he`), indonesio (`in`) y yiddish (`yi`) debido a los cambios en el constructor de configuración regional en las versiones más recientes de Java.

#### Requisitos de tiempo de ejecución {#runtime-requirements}

El tiempo de ejecución de Java 21 se utiliza para compilaciones con Java 21 y Java 17, y se aplicará gradualmente a las compilaciones de Java 11 también (consulte la Nota a continuación). Un entorno debe estar en la versión de AEM 17098 o más reciente para recibir la actualización de Java 21. Para garantizar la compatibilidad, se requieren los siguientes ajustes.

Las actualizaciones de biblioteca se pueden aplicar en cualquier momento, ya que siguen siendo compatibles con versiones de Java anteriores.

* **Versión mínima de ASM:**
Actualice el uso del paquete Java`org.objectweb.asm`, a menudo agrupado en artefactos de `org.ow2.asm.*`, a la versión 9.5 o superior para garantizar la compatibilidad con los tiempos de ejecución de JVM más recientes.

* **Versión mínima de Groovy:**
Actualice el uso de los paquetes Java `org.apache.groovy` o `org.codehaus.groovy` a la versión 4.0.22 o superior para garantizar la compatibilidad con los tiempos de ejecución de JVM más recientes.

  Este paquete se puede incluir indirectamente añadiendo dependencias de terceros como la consola de AEM Groovy.

* **Versión mínima de Aries SPIFly:**
Actualice el uso del paquete Java `org.apache.aries.spifly.dynamic.bundle` a la versión 1.3.6 o posterior para garantizar la compatibilidad con los tiempos de ejecución de JVM más recientes.

AEM Cloud Service SDK admite Java 21 y le permite comprobar la compatibilidad del proyecto con Java 21 antes de ejecutar una canalización de Cloud Manager.

* **Editar un parámetro de tiempo de ejecución:**
Al ejecutar AEM localmente con Java 21, los scripts de inicio (`crx-quickstart/bin/start` o `crx-quickstart/bin/start.bat`) fallan debido al parámetro `MaxPermSize`. Como solución, quite `-XX:MaxPermSize=256M` del script o defina la variable de entorno `CQ_JVM_OPTS`, estableciéndola en `-Xmx1024m -Djava.awt.headless=true`.

  Este problema se resuelve en la versión 19149 y posteriores de SDK de AEM Cloud Service.

>[!IMPORTANT]
>
>Cuando `.cloudmanager/java-version` se establece en `21` o `17`, se implementa el tiempo de ejecución de Java 21. El tiempo de ejecución de Java 21 está programado para su despliegue gradual en todos los entornos (no solo en aquellos cuyo código se haya creado con Java 11) a partir del martes, 4 de febrero de 2025. Los despliegues comienzan con entornos limitados y de desarrollo, seguidos de todos los entornos de producción en abril de 2025. Los clientes que deseen adoptar el tiempo de ejecución de Java 21 *antes* pueden comunicarse con Adobe en [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com).


#### Requisitos de tiempo de compilación {#build-time-reqs}

Se requieren los siguientes ajustes para permitir la creación del proyecto con Java 21 y Java 17. Pueden actualizarse incluso antes de ejecutar Java 21 y Java 17, ya que son compatibles con versiones de Java más antiguas.

Se recomienda a los clientes de AEM Cloud Service que creen sus proyectos con Java 21 lo antes posible para aprovechar las nuevas funciones de idioma.

* **Versión mínima de `bnd-maven-plugin`:**
Actualice el uso de `bnd-maven-plugin` a la versión 6.4.0 para garantizar la compatibilidad con los tiempos de ejecución de JVM más recientes.

  Las versiones 7 o posteriores no son compatibles con Java 11 o versiones posteriores, por lo que no se recomienda actualizar a esa versión.

* **Versión mínima de `aemanalyser-maven-plugin`:**
Actualice el uso de `aemanalyser-maven-plugin` a la versión 1.6.6 o superior para garantizar la compatibilidad con los tiempos de ejecución de JVM más recientes.

* **Versión mínima de `maven-bundle-plugin`:**
Actualice el uso de `maven-bundle-plugin` a la versión 5.1.5 o superior para garantizar la compatibilidad con los tiempos de ejecución de JVM más recientes.

  Las versiones 6 o posteriores no son compatibles con Java 11 o versiones posteriores, por lo que no se recomienda actualizar a esa versión.

* **Actualizar dependencias en `maven-scr-plugin`:**
`maven-scr-plugin` no es compatible directamente con Java 21 o Java 17. Sin embargo, los archivos descriptor se pueden generar actualizando la versión de dependencia de ASM en la configuración del complemento, como se muestra en el siguiente ejemplo:

```XML
<project>
  ...
  <build>
    ...
    <plugins>
      ...
      <plugin>
        <groupId>org.apache.felix</groupId>
        <artifactId>maven-scr-plugin</artifactId>
        <version>1.26.4</version>
        <executions>
          <execution>
            <id>generate-scr-scrdescriptor</id>
            <goals>
              <goal>scr</goal>
            </goals>
          </execution>
        </executions>
        <dependencies>
          <dependency>
            <groupId>org.ow2.asm</groupId>
            <artifactId>asm-analysis</artifactId>
            <version>9.7.1</version>
            <scope>compile</scope>
          </dependency>
        </dependencies>
      </plugin>
      ...
    </plugins>
    ...
  </build>
  ...
</project>
```

## Variables de entorno: estándar {#environment-variables}

Es posible que necesite variar el proceso de compilación en función de la información sobre el programa o la canalización.

Por ejemplo, si la minificación de JavaScript se produce en el momento de la compilación con una herramienta como gulp, se pueden preferir diferentes niveles de minificación para varios entornos. Una compilación de desarrollo podría utilizar un nivel de minificación más ligero en comparación con el ensayo y la producción.

Para admitir esto, Cloud Manager agrega estas variables de entorno estándar al contenedor de compilación para cada ejecución.

| Nombre de la variable | Definición |
|---|---|
| `CM_BUILD` | Siempre se configura como `true` |
| `BRANCH` | La rama configurada para la ejecución |
| `CM_PIPELINE_ID` | El identificador numérico de la canalización |
| `CM_PIPELINE_NAME` | El nombre de la canalización |
| `CM_PROGRAM_ID` | Identificador numérico del programa |
| `CM_PROGRAM_NAME` | El nombre del programa |
| `ARTIFACTS_VERSION` | Para una fase o canalización de producción, la versión sintética generada por Cloud Manager |
| `CM_AEM_PRODUCT_VERSION` | La versión |

## Variables de entorno: canalización {#pipeline-variables}

El proceso de compilación puede requerir variables de configuración específicas que no deben almacenarse en el repositorio de Git. Además, es posible que tenga que ajustar estas variables entre ejecuciones de canalización que utilicen la misma rama.

Consulte también [Configurar variables de canalización](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) para obtener más información.

## Instalación de paquetes de sistema adicionales {#installing-additional-system-packages}

Algunas compilaciones requieren paquetes de sistema adicionales para funcionar completamente. Por ejemplo, una compilación puede invocar un script de Python o Ruby y debe tener instalado un intérprete de idioma adecuado. Este proceso de instalación se puede administrar llamando a [`exec-maven-plugin`](https://www.mojohaus.org/exec-maven-plugin/) en su `pom.xml` para invocar APT. Esta ejecución debe envolverse generalmente en un perfil Maven específico de Cloud Manager. En este ejemplo se instala Python.

```xml
        <profile>
            <id>install-python</id>
            <activation>
                <property>
                        <name>env.CM_BUILD</name>
                </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <groupId>org.codehaus.mojo</groupId>
                        <artifactId>exec-maven-plugin</artifactId>
                        <version>1.6.0</version>
                        <executions>
                            <execution>
                                <id>apt-get-update</id>
                                <phase>validate</phase>
                                <goals>
                                    <goal>exec</goal>
                                </goals>
                                <configuration>
                                    <executable>apt-get</executable>
                                    <arguments>
                                        <argument>update</argument>
                                    </arguments>
                                </configuration>
                            </execution>
                            <execution>
                                <id>install-python</id>
                                <phase>validate</phase>
                                <goals>
                                    <goal>exec</goal>
                                </goals>
                                <configuration>
                                    <executable>apt-get</executable>
                                    <arguments>
                                        <argument>install</argument>
                                        <argument>-y</argument>
                                        <argument>--no-install-recommends</argument>
                                        <argument>python</argument>
                                    </arguments>
                                </configuration>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

Esta misma técnica se puede utilizar para instalar paquetes específicos para idiomas, por ejemplo, utilizando `gem` para RubyGems o `pip` para paquetes de Python.

>[!NOTE]
>
>La instalación de un paquete del sistema de esta manera no lo instala en el entorno de tiempo de ejecución utilizado para ejecutar Adobe Experience Manager. Si necesita instalar un paquete del sistema en el entorno de AEM, póngase en contacto con su representante de Adobe.

>[!TIP]
>
>Para obtener más información acerca del entorno de creación front-end, consulte el documento [Desarrollo de sitios con la canalización front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md).
