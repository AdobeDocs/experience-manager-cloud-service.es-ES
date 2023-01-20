---
title: Entorno de compilación
description: Obtenga información sobre el entorno de compilación de Cloud Manager y cómo crea y prueba su código.
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
source-git-commit: 3348662e3da4dad75b851d7af7251d456321a3ec
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 98%

---


# Entorno de compilación {#build-environment}

Obtenga información sobre el entorno de compilación de Cloud Manager y cómo crea y prueba su código.

## Generar detalles del entorno {#build-environment-details}

Cloud Manager crea y prueba su código mediante un entorno de compilación especializado.

* El entorno de compilación está basado en Linux, derivado de Ubuntu 18.04.
* Apache Maven 3.6.0 está instalado.
* Las versiones de Java instaladas son Oracle JDK 8u202 y Oracle JDK 11.0.2.
* De forma predeterminada, la variable de entorno `JAVA_HOME` está configurada en `/usr/lib/jvm/jdk1.8.0_202`, que contiene Oracle JDK 8u202. Consulte [Versión JDK de ejecución de Maven alternativa](#alternate-maven-jdk-version) para obtener más información.
* Hay algunos paquetes de sistema adicionales instalados que son necesarios.

   * `bzip2`
   * `unzip`
   * `libpng`
   * `imagemagick`
   * `graphicsmagick`

* Se pueden instalar otros paquetes en el momento de la compilación, tal como se describe en la sección [Instalación de paquetes de sistema adicionales.](#installing-additional-system-packages)
* Cada compilación se realiza en un entorno prístino; el contenedor de compilación no mantiene ningún estado entre ejecuciones.
* Maven siempre se ejecuta con los tres comandos siguientes.

* `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
* `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
* `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent package`
* Maven se configura a nivel de sistema con un archivo `settings.xml`, que incluye automáticamente el repositorio de artefactos de Adobe público usando un perfil denominado `adobe-public`. (Consulte [Repositorio Maven público de Adobe](https://repo1.maven.org/) para obtener más información).

>[!NOTE]
>
>Aunque Cloud Manager no define una versión específica de `jacoco-maven-plugin`, la versión utilizada debe ser al menos `0.7.5.201505241946`.

### Uso de una versión de Java específica {#using-java-support}

De forma predeterminada, los proyectos se crean mediante el proceso de compilación de Cloud Manager con el JDK de Oracle 8. Los clientes que deseen utilizar un JDK alternativo tienen dos opciones.

* [Utilizar Maven Toolchain.](#maven-toolchains)
* [Seleccione una versión JDK alternativa para todo el proceso de ejecución de Maven.](#alternate-maven-jdk-version)

#### Maven Toolchains {#maven-toolchains}

La variable [Complemento Maven Toolchains](https://maven.apache.org/plugins/maven-toolchains-plugin/) permite a los proyectos seleccionar un JDK específico (o toolchain) para utilizarlo en el contexto de complementos Maven con conocimiento de herramientas. Esto se hace en el archivo `pom.xml` del proyecto especificando un valor de proveedor y de versión.

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-toolchains-plugin</artifactId>
    <version>1.1</version>
    <executions>
        <execution>
            <goals>
                <goal>toolchain</goal>
            </goals>
        </execution>
    </executions>
    <configuration>
        <toolchains>
            <jdk>
                <version>11</version>
                <vendor>oracle</vendor>
            </jdk>
        </toolchains>
    </configuration>
</plugin>
```

Esto hará que todos los complementos Maven con conocimiento de herramientas utilicen el JDK de Oracle, versión 11.

Al utilizar este método, el propio Maven sigue ejecutándose utilizando el JDK predeterminado (Oracle 8) y la variable de entorno `JAVA_HOME` no cambia. Por lo tanto, la comprobación o aplicación de la versión de Java a través de complementos como el plug-in Apache Maven Enforcer no funciona y estos plug-ins no deben usarse.

Las combinaciones de proveedor/versión disponibles actualmente son:

| Proveedor | Versión |
|---|---|
| `oracle` | `8` |
| `oracle` | `11` |
| `sun` | `8` |
| `sun` | `11` |

Esta tabla se refiere a los números de versión del producto. Los números de compilación de Java o las rutas de instalación pueden reflejar convenciones de versiones de Java antiguas, como 1.8 para Java 8.

>[!NOTE]
>
>A partir de abril de 2022, el JDK de Oracle será el JDK predeterminado para el desarrollo y funcionamiento de aplicaciones de AEM. El proceso de creación de Cloud Manager cambiará automáticamente al uso de JDK de Oracle, incluso si se selecciona explícitamente una opción alternativa en Maven Toolchain. Consulte las notas de la versión de abril una vez publicadas para obtener más información.

#### Versión JDK de ejecución de Maven alternativa {#alternate-maven-jdk-version}

También es posible seleccionar Java 8 o Java 11 como JDK para toda la ejecución de Maven. A diferencia de las opciones de Toolchain, esto cambia el JDK utilizado para todos los plug-ins a menos que también se establezca la configuración de Toolchain en cuyo caso la configuración de Toolchain se sigue aplicando a los plug-ins de Maven que tienen en cuenta las cadenas de herramientas. Como resultado, comprobar y aplicar la versión de Java utilizando el [complemento Apache Maven Enforcer](https://maven.apache.org/enforcer/maven-enforcer-plugin/) funcionará.

Para ello, cree un archivo con el nombre `.cloudmanager/java-version` en la rama del repositorio de Git utilizada por la canalización. Este archivo puede tener el contenido 11 u 8. Se ignora cualquier otro valor. Si se especifica 11, se utiliza Oracle 11 y la variable de entorno `JAVA_HOME` se configura como `/usr/lib/jvm/jdk-11.0.2`. Si se especifica 8, se utiliza Oracle 8 y la variable de entorno `JAVA_HOME` se configura como `/usr/lib/jvm/jdk1.8.0_202`.

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

Cloud Manager permite que estas variables se configuren mediante la API de Cloud Manager o la CLI de Cloud Manager por canalización. Las variables pueden almacenarse como texto sin formato o cifrarse en reposo. En cualquier caso, las variables están disponibles dentro del entorno de compilación como una variable de entorno a la que se puede hacer referencia desde dentro del archivo `pom.xml` u otras secuencias de comandos de compilación.

Este comando de CLI configura una variable.

```shell
$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test
```

Este comando enumera las variables.

```shell
$ aio cloudmanager:list-pipeline-variables PIPELINEID
```

Los nombres de las variables deben cumplir las siguientes convenciones.

* Las variables solo pueden contener caracteres alfanuméricos y el guion bajo (`_`).
* Los nombres deben estar en mayúsculas.
* Hay un límite de 200 variables por canalización.
* Cada nombre debe tener menos de 100 caracteres.
* Cada `string` debe tener menos de 2048 caracteres.
* Cada valor de la variable de tipo `secretString` debe tener menos de 500 caracteres.

Cuando se utiliza dentro de un archivo `pom.xml` de Maven, normalmente resulta útil asignar estas variables a las propiedades de Maven mediante una sintaxis similar a esta.

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                <property>
                    <name>env.CM_BUILD</name>
                </property>
            </activation>
            <properties>
                <my.custom.property>${env.MY_CUSTOM_VARIABLE}</my.custom.property> 
            </properties>
        </profile>
```

## Instalación de paquetes de sistema adicionales {#installing-additional-system-packages}

Algunas compilaciones requieren que se instalen paquetes de sistema adicionales para funcionar completamente. Por ejemplo, una compilación puede invocar un script Python o Ruby y deberá tener instalado un intérprete de idioma adecuado. Esto se puede hacer llamando a la función [`exec-maven-plugin`](https://www.mojohaus.org/exec-maven-plugin/) en su `pom.xml` para invocar APT. Esta ejecución debe envolverse generalmente en un perfil Maven específico de Cloud Manager. En este ejemplo se instala Python.

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
>Para obtener más información sobre el entorno de compilación front-end, consulte el documento [Desarrollo de sitios con la canalización front-end.](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)
