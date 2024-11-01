---
title: Entorno de compilación
description: Obtenga información sobre el entorno de compilación de Cloud Manager y cómo crea y prueba su código.
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 41a67b0747ed665291631de4faa7fb7bb50aa9b9
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 77%

---


# Entorno de compilación {#build-environment}

Obtenga información sobre el entorno de compilación de Cloud Manager y cómo crea y prueba su código.

## Generar detalles del entorno {#build-environment-details}

Cloud Manager crea y prueba su código mediante un entorno de compilación especializado.

* El entorno de compilación está basado en Linux, derivado de Ubuntu 22.04.
* Apache Maven 3.9.4 está instalado.
   * Adobe recomienda [actualizar los repositorios de Maven para que utilicen HTTPS en lugar de HTTP](#https-maven).
* Las versiones de Java instaladas son Oracle JDK 11.0.22 y Oracle JDK 8u401.
* **IMPORTANT**: De forma predeterminada, la variable de entorno `JAVA_HOME` está configurada en `/usr/lib/jvm/jdk1.8.0_401`, que contiene el JDK de Oracle 8u401. AEM *_Este valor predeterminado debe anularse para que los proyectos de nube de utilicen JDK 11_*. Consulte la sección [Configuración de la versión del JDK de Maven](#alternate-maven-jdk-version) para obtener más información.
* Hay algunos paquetes de sistema adicionales instalados que son necesarios.
   * `bzip2`
   * `unzip`
   * `libpng`
   * `imagemagick`
   * `graphicsmagick`
* Se pueden instalar otros paquetes en el momento de la compilación, tal como se describe en la sección [Instalación de paquetes de sistema adicionales](#installing-additional-system-packages).
* Cada compilación se realiza en un entorno prístino; el contenedor de compilación no mantiene ningún estado entre ejecuciones.
* Maven siempre se ejecuta con los tres comandos siguientes.
   * `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
   * `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
   * `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent package`
* Maven se configura a nivel de sistema con un archivo `settings.xml`, que incluye automáticamente el repositorio de artefactos de Adobe público usando un perfil denominado `adobe-public`. (Consulte [Repositorio Maven público de Adobe](https://repo1.maven.org/) para obtener más información).

>[!NOTE]
>
>Aunque Cloud Manager no define una versión específica de `jacoco-maven-plugin`, la versión utilizada debe ser al menos `0.7.5.201505241946`.

## Repositorios de Maven HTTPS {#https-maven}

Cloud Manager [versión 2023.10.0](/help/implementing/cloud-manager/release-notes/2023/2023-10-0.md) inició una actualización móvil del entorno de compilación (que finalizó con la versión 2023.12.0), que incluía una actualización a Maven 3.8.8. Un cambio significativo introducido en Maven 3.8.1 ha sido una mejora de la seguridad destinada a mitigar posibles vulnerabilidades. En concreto, Maven ahora deshabilita de forma predeterminada todas las duplicaciones de `http://*` inseguras, tal como se describe en las [Notas de la versión de Maven](http://maven.apache.org/docs/3.8.1/release-notes.html#cve-2021-26291).

Como resultado de esta mejora de seguridad, algunas personas pueden tener problemas durante el paso de compilación, especialmente al descargar artefactos de repositorios Maven que utilizan conexiones HTTP no seguras.

Para garantizar una experiencia sin problemas con la versión actualizada, Adobe recomienda actualizar los repositorios de Maven para que utilicen HTTPS en lugar de HTTP. Este ajuste se ha llevado a cabo para adaptarse a la adopción creciente de la industria de protocolos de comunicación seguros y ayuda a mantener un proceso de compilación seguro y fiable.

### Uso de una versión de Java específica {#using-java-support}

De forma predeterminada, los proyectos se crean mediante el proceso de compilación de Cloud Manager con el JDK de Oracle 8, pero se aconseja a los clientes de AEM Cloud Service que establezcan la versión del JDK utilizado para ejecutar Maven en `11`.

#### Configuración de la versión del JDK de Maven {#alternate-maven-jdk-version}

Se recomienda establecer la versión del JDK para toda la ejecución de Maven en `11` en un archivo `.cloudmanager/java-version`.

Para ello, cree un archivo con el nombre `.cloudmanager/java-version` en la rama del repositorio de Git utilizada por la canalización. Edite el archivo de modo que contenga únicamente el texto `11`. Aunque Cloud Manager también acepta un valor de `8`, esta versión ya no es compatible con los proyectos de AEM Cloud Service. Se ignora cualquier otro valor. Cuando se especifica `11`, se usa el Oracle 11 y la variable de entorno `JAVA_HOME` se establece en `/usr/lib/jvm/jdk-11.0.22`.

## Variables de entorno {#environment-variables}

### Variables de entorno estándar {#standard-environ-variables}

Es posible que necesite variar el proceso de compilación en función de la información sobre el programa o la canalización.

Por ejemplo, si la minificación de JavaScript en tiempo de compilación se realiza a través de una herramienta como gulp, puede haber un deseo de usar un nivel de minificación diferente al crear para un entorno de desarrollo en lugar de construir para ensayo y producción.

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

### Variables de canalización {#pipeline-variables}

El proceso de compilación puede depender de variables de configuración específicas que no deberían colocarse en el repositorio de Git o puede que necesite variarlas entre ejecuciones de canalización que usen la misma rama.

Consulte también [Configurar variables de canalización](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) para obtener más información

## Instalación de paquetes de sistema adicionales {#installing-additional-system-packages}

Algunas compilaciones requieren que se instalen paquetes de sistema adicionales para funcionar completamente. Por ejemplo, una compilación puede invocar un script de Python o Ruby y debe tener instalado un intérprete de idioma adecuado. Esto se puede hacer llamando a la función [`exec-maven-plugin`](https://www.mojohaus.org/exec-maven-plugin/) en su `pom.xml` para invocar APT. Esta ejecución debe envolverse generalmente en un perfil Maven específico de Cloud Manager. En este ejemplo se instala Python.

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
