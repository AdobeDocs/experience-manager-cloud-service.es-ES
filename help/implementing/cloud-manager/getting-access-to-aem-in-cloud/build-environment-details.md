---
title: Entorno de compilación de Cloud Manager
description: Obtenga información sobre el entorno de compilación de Cloud Manager y cómo crea y prueba su código.
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 7b9b9f3b957b27812c4a7e8f2dbcf96d8786b73e
workflow-type: tm+mt
source-wordcount: '1277'
ht-degree: 37%

---


# Entorno de compilación {#build-environment}

Obtenga información sobre el entorno de compilación de Cloud Manager y cómo crea y prueba su código.

## Generar detalles del entorno {#build-environment-details}

Cloud Manager crea y prueba su código mediante un entorno de compilación especializado.

* El entorno de compilación está basado en Linux, derivado de Ubuntu 22.04.
* Apache Maven 3.9.4 está instalado.
   * Adobe recomienda [actualizar los repositorios de Maven para que utilicen HTTPS en lugar de HTTP](#https-maven).
* Las versiones de Java instaladas son Oracle JDK 11.0.22, Oracle JDK 17.0.10 y Oracle JDK 21.0.4.
* **IMPORTANTE:** De forma predeterminada, la variable de entorno `JAVA_HOME` está configurada en `/usr/lib/jvm/jdk1.8.0_401`, que contiene el JDK de Oracle 8u401. AEM ***Este valor predeterminado debe anularse para que los proyectos de nube de utilicen JDK 21 (preferido), 17 o 11***. Consulte la sección [Configuración de la versión del JDK de Maven](#alternate-maven-jdk-version) para obtener más información.
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
>Aunque Cloud Manager no define una versión específica de `jacoco-maven-plugin`, la versión utilizada debe ser al menos `0.7.5.201505241946`.

## Repositorios de Maven HTTPS {#https-maven}

Cloud Manager [versión 2023.10.0](/help/implementing/cloud-manager/release-notes/2023/2023-10-0.md) inició una actualización móvil del entorno de compilación (que finalizó con la versión 2023.12.0), que incluía una actualización a Maven 3.8.8. Un cambio significativo introducido en Maven 3.8.1 ha sido una mejora de la seguridad destinada a mitigar posibles vulnerabilidades. En concreto, Maven ahora deshabilita de forma predeterminada todas las duplicaciones de `http://*` inseguras, tal como se describe en las [Notas de la versión de Maven](http://maven.apache.org/docs/3.8.1/release-notes.html#cve-2021-26291).

Como resultado de esta mejora de seguridad, algunas personas pueden tener problemas durante el paso de compilación, especialmente al descargar artefactos de repositorios Maven que utilizan conexiones HTTP no seguras.

Para garantizar una experiencia sin problemas con la versión actualizada, Adobe recomienda actualizar los repositorios de Maven para que utilicen HTTPS en lugar de HTTP. Este ajuste se ha llevado a cabo para adaptarse a la adopción creciente de la industria de protocolos de comunicación seguros y ayuda a mantener un proceso de compilación seguro y fiable.

### Utilizar una versión de Java específica {#using-java-support}

El proceso de generación de Cloud Manager utiliza el JDK de Oracle 8 para generar proyectos de forma predeterminada, pero los clientes de AEM Cloud Service deben establecer la versión del JDK de ejecución de Maven en 21 (preferido), 17 u 11.

#### Establezca la versión de Maven JDK {#alternate-maven-jdk-version}

El Adobe recomienda establecer la versión del JDK de ejecución de Maven en `21` o `17` en un archivo de `.cloudmanager/java-version`.

Para ello, cree un archivo con el nombre `.cloudmanager/java-version` en la rama del repositorio Git utilizada por la canalización. Edite el archivo de modo que contenga solamente el texto `21` o `17`. Aunque Cloud Manager también acepta un valor de `8`, esta versión ya no es compatible con los proyectos de AEM Cloud Service. Se ignora cualquier otro valor. Cuando se especifica `21` o `17`, se utiliza Java 21 de Oracle o Java 17 de Oracle y la variable de entorno `JAVA_HOME` se establece en `/usr/lib/jvm/jdk-21` o `/usr/lib/jvm/jdk-17`.

#### Requisitos previos para migrar a la creación con Java 21 o Java 17 {#prereq-for-building}

>[!NOTE]
>
>*Al migrar la aplicación a una nueva versión de compilación de Java y de tiempo de ejecución, realice pruebas exhaustivas en los entornos de desarrollo y ensayo antes de implementarla en producción.
>Cabe destacar que las siguientes funciones aún no se han validado formalmente con el tiempo de ejecución de Java 21: [Forms](/help/forms/home.md), [Flujos de trabajo](/help/sites-cloud/authoring/workflows/overview.md), [Bandeja de entrada](/help/sites-cloud/authoring/inbox.md) y [Proyectos](/help/sites-cloud/authoring/projects/overview.md). Si su aplicación depende de estas características, realice pruebas exhaustivas para comprobar la funcionalidad.*

##### Acerca de algunas funciones de traducción {#translation-features}

Es posible que las siguientes funciones no funcionen correctamente al crear con Java 21 o Java 17, y Adobe espera resolverlas a principios de 2025:

* `XLIFF` (formato de archivo de intercambio de localización XML) produce un error al utilizar la traducción humana.
* `I18n` (internacionalización) no administra correctamente las configuraciones regionales de idioma hebreo (`he`), indonesio (`in`) y yiddish (`yi`) debido a los cambios en el constructor de configuración regional en las versiones más recientes de Java.

#### Requisitos de tiempo de ejecución {#runtime-requirements}

El tiempo de ejecución de Java 21 se utiliza para compilaciones en Java 21, Java 17 y Java 11 a partir de febrero de 2025. Para garantizar la compatibilidad, son necesarios los siguientes ajustes.

Las actualizaciones de biblioteca se pueden aplicar en cualquier momento, ya que siguen siendo compatibles con versiones de Java anteriores.

* **Versión mínima de `org.objectweb.asm`:**
Actualice el uso de `org.objectweb.asm` a la versión 9.5 o superior para garantizar la compatibilidad con los tiempos de ejecución de JVM más recientes.

* **Versión mínima de `org.apache.groovy`:**
Actualice el uso de `org.apache.groovy` a la versión 4.0.22 o superior para garantizar la compatibilidad con los tiempos de ejecución de JVM más recientes.

  Este paquete se puede incluir indirectamente añadiendo dependencias de terceros como la consola de AEM Groovy.

* **Editar un parámetro de tiempo de ejecución:**
AEM Cuando se ejecuta la localmente con Java 21, los scripts de inicio (`crx-quickstart/bin/start` o `crx-quickstart/bin/start.bat`) fallan debido al parámetro `MaxPermSize`. Como solución, quite `-XX:MaxPermSize=256M` del script o defina la variable de entorno `CQ_JVM_OPTS`, estableciéndola en `-Xmx1024m -Djava.awt.headless=true`.

  Adobe planea resolver este problema en una versión futura.

>[!NOTE]
>
>Cuando `.cloudmanager/java-version` se establece en `21` o `17`, se implementa el tiempo de ejecución de Java 21. En febrero o marzo de 2025, el tiempo de ejecución de Java 21 está planificado para su implementación en todos los clientes, incluso si se utiliza Java 11 para generar el código.

#### Requisitos de tiempo de compilación

Se requieren los siguientes ajustes para permitir la creación del proyecto con Java 21 y Java 17. Se pueden actualizar en cualquier momento, ya que son compatibles con versiones anteriores de Java.

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
