---
title: 'Proyecto de aplicación de AEM: Cloud Service'
description: 'Proyecto de aplicación de AEM: Cloud Service'
translation-type: tm+mt
source-git-commit: e3370b7a7f543ae93b25ead8c174796fd27067f2
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 10%

---


# Creación de un proyecto de aplicación de AEM {#aem-application-project}

## Uso del asistente para crear un proyecto de aplicación de AEM {#using-wizard-to-create-an-aem-application-project}

Para ayudar a que los nuevos clientes se inicien, Cloud Manager ahora puede crear un proyecto mínimo de AEM como punto de partida. Este proceso se basa en el arquetipo [**del proyecto de **](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)AEM.


Siga los pasos a continuación para crear un proyecto de aplicación de AEM en Cloud Manager:

1. Una vez que inicie sesión en Cloud Manager y se complete la configuración básica del programa, se mostrará una tarjeta de llamada a la acción especial en la pantalla **Información general**, si el repositorio está vacío.

   ![](assets/create-wizard1.png)

1. Haga clic en **Crear** para desplazarse hasta la pantalla **Crear una rama y un proyecto**.

   ![](assets/create-wizard2.png)

1. El mosaico Creación de **proyectos en curso** se muestra en la pantalla Información general *de* Programa.

   ![](assets/create-wizard3.png)

1. Una vez que la creación del programa ha finalizado, el mosaico **Agregar entorno** aparece en la página *Información general del programa*.
   ![](assets/create-wizard4.png)

   Consulte [Administración de Entornos](/help/implementing/cloud-manager/manage-environments.md) para obtener información sobre cómo agregar o administrar entornos.

## Configuración del proyecto {#setting-up-your-project}

### Modificación de los detalles de configuración del proyecto {#modifying-project-setup-details}

Para poder compilar e implementar correctamente con Cloud Manager, los proyectos de AEM existentes deben cumplir algunas reglas básicas:

* Los proyectos deben crearse con Apache Maven.
* Debe haber un *archivo pom.xml* en la raíz del repositorio Git. Este archivo *pom.xml* puede referirse a tantos submódulos (que a su vez pueden tener otros submódulos, etc.) según sea necesario.

* Puede agregar referencias a repositorios de artefactos Maven adicionales en los archivos *pom.xml* . Sin embargo, no se admite el acceso a repositorios de artefactos protegidos por contraseña o de red.
* Los paquetes de contenido implementable se descubren mediante la búsqueda de archivos *zip* del paquete de contenido que se encuentran en un directorio denominado *destinatario*. Cualquier número de submódulos puede producir paquetes de contenido.

* Los artefactos de Dispatcher implementables se descubren mediante la búsqueda de archivos *zip* (nuevamente, contenidos en un directorio llamado *destinatario*) que tienen directorios llamados *conf* y *conf.d*.

* Si hay más de un paquete de contenido, no se garantiza el orden de las implementaciones de paquetes. Si se necesita un orden específico, se pueden usar dependencias de paquetes de contenido para definir el orden. Es posible que los paquetes se [omitan](#skipping-content-packages) de la implementación.


## Detalles del Entorno de compilación {#build-environment-details}

Cloud Manager crea y prueba el código mediante un entorno de compilación especializado. Este entorno tiene los atributos siguientes:

* El entorno de compilación está basado en Linux, derivado de Ubuntu 18.04.
* Se ha instalado Apache Maven 3.6.0.
* La versión de Java instaló Oracle JDK 8u202 y 11.0.2.
* Hay algunos paquetes de sistema adicionales instalados que son necesarios:

   * bzip2
   * descomprimir
   * libpng
   * imagemagick
   * graphicsmagick

* Se pueden instalar otros paquetes en el momento de la compilación, como se describe [a continuación](#installing-additional-system-packages).
* Cada obra se construye sobre un entorno prístino; el contenedor de compilación no mantiene ningún estado entre las ejecuciones.
* Maven siempre se ejecuta con el comando: *mvn —batch-mode clean org.jacoco:jacoco-maven-plugin:prepare-agent package*
* Maven se configura a nivel del sistema con un archivo settings.xml que incluye automáticamente el repositorio público de Adobe **Artiact** . (Para obtener más información, consulte el Repositorio [público de](https://repo.adobe.com/) Adobe Maven).

### Uso de Java 11 {#using-java-11}

Cloud Manager ahora admite la creación de proyectos de clientes con Java 8 y Java 11. De forma predeterminada, los proyectos se crean con Java 8. Los clientes que deseen utilizar Java 11 en sus proyectos pueden hacerlo usando el complemento [Apache Maven Toolchain](https://maven.apache.org/plugins/maven-toolchains-plugin/).

Para ello, en el archivo pom.xml, agregue una `<plugin>` entrada con este aspecto:

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
```

>[!NOTE]
>* Los proveedores admitidos son `oracle` y `sun`.
>* Las versiones admitidas son `1.8`, `1.11`y `11`.


## Variables de Entorno {#environment-variables}

### Variables de Entorno estándar {#standard-environ-variables}

En algunos casos, los clientes consideran necesario variar el proceso de compilación en función de la información sobre el programa o la canalización.

Por ejemplo, si se está realizando la minimización de JavaScript en tiempo de compilación, a través de una herramienta como gulp, puede haber un deseo de usar un nivel de minificación diferente cuando se construye para un entorno de desarrollo en lugar de construir para etapa y producción.

Para admitir esto, Cloud Manager agrega estas variables de entorno estándar al contenedor de compilación para cada ejecución.

| **Nombre de variable** | **Definición** |
|---|---|
| CM_BUILD | Siempre configurado como &quot;true&quot; |
| RAMA | La rama configurada para la ejecución |
| CM_PIPELINE_ID | El identificador de canalización numérica |
| CM_PIPELINE_NAME | El nombre de la canalización |
| CM_PROGRAMA_ID | El identificador de programa numérico |
| CM_PROGRAMA_NAME | El nombre del programa |
| ARTIFACTS_VERSION | Para una fase o canalización de producción, la versión sintética generada por Cloud Manager |
| CM_AEM_PRODUCT_VERSION | El nombre de la versión |


### Variables de Entorno personalizadas {#custom-environ-variables}

En algunos casos, el proceso de creación de un cliente puede depender de variables de configuración específicas que no sería adecuado colocar en el repositorio git. Cloud Manager permite que un representante de Adobe configure estas variables cliente por cliente. Estas variables se almacenan en una ubicación de almacenamiento segura y solo son visibles en el contenedor de compilación para el cliente específico. Los clientes que deseen utilizar esta función deben ponerse en contacto con su representante de Adobe para configurar sus variables.

Una vez configuradas, estas variables estarán disponibles como variables de entorno. Para utilizarlas como propiedades de Maven, puede hacer referencia a ellas dentro del archivo pom.xml, potencialmente dentro de un perfil como se describe anteriormente:

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                  <property>
                        <name>env.CM_BUILD</name>
                  </property>
            </activation>
            <properties>
                  <my.custom.property>${env.MY_CUSTOM_PROPERTY}</my.custom.property>  
            </properties>
        </profile>
```

>[!NOTE]
>
>Los nombres de las variables de Entorno sólo pueden contener caracteres alfanuméricos y de subrayado (_). Por convención, los nombres deben estar en mayúsculas.

## Activación de Perfiles Maven en Cloud Manager {#activating-maven-profiles-in-cloud-manager}

En algunos casos limitados, es posible que deba variar ligeramente el proceso de compilación al ejecutarse dentro de Cloud Manager, en lugar de hacerlo en estaciones de trabajo para desarrolladores. En estos casos, los Perfiles [](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) Maven se pueden usar para definir cómo la compilación debe ser diferente en diferentes entornos, incluido Cloud Manager.

La Activación de un Perfil Maven dentro del entorno de compilación de Cloud Manager debe realizarse buscando la variable de entorno CM_BUILD descrita anteriormente. Por el contrario, un perfil que se pretenda usar solamente fuera del entorno de compilación de Cloud Manager debería realizarse buscando la ausencia de esta variable.

Por ejemplo, si desea enviar un mensaje sencillo solo cuando la compilación se ejecute dentro de Cloud Manager, puede hacer lo siguiente:

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                  <property>
                        <name>env.CM_BUILD</name>
                  </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <artifactId>maven-antrun-plugin</artifactId>
                        <version>1.8</version>
                        <executions>
                            <execution>
                                <phase>initialize</phase>
                                <configuration>
                                    <target>
                                        <echo>I'm running inside Cloud Manager!</echo>
                                    </target>
                                </configuration>
                                <goals>
                                    <goal>run</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

>[!NOTE]
>
>Para probar este perfil en una estación de trabajo para desarrolladores, puede habilitarlo en la línea de comandos (con `-PcmBuild`) o en el Entorno de desarrollo integrado (IDE).

Y si desea enviar un mensaje sencillo solo cuando la compilación se ejecute fuera de Cloud Manager, puede hacer lo siguiente:

```xml
        <profile>
            <id>notCMBuild</id>
            <activation>
                  <property>
                        <name>!env.CM_BUILD</name>
                  </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <artifactId>maven-antrun-plugin</artifactId>
                        <version>1.8</version>
                        <executions>
                            <execution>
                                <phase>initialize</phase>
                                <configuration>
                                    <target>
                                        <echo>I'm running outside Cloud Manager!</echo>
                                    </target>
                                </configuration>
                                <goals>
                                    <goal>run</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```


## Instalación de paquetes de sistema adicionales {#installing-additional-system-packages}

Algunas compilaciones requieren que se instalen paquetes de sistema adicionales para funcionar completamente. Por ejemplo, una compilación puede invocar una secuencia de comandos Python o ruby y, como resultado, debe tener instalado un intérprete de idioma adecuado. Esto se puede hacer llamando al [exec-maven-plugin](https://www.mojohaus.org/exec-maven-plugin/) para invocar APT. Esta ejecución generalmente debe envolverse en un perfil Maven específico del Administrador de la nube. Por ejemplo, para instalar python:

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

Esta misma técnica se puede utilizar para instalar paquetes específicos de idioma, es decir, `gem` para RubyGems o `pip` para paquetes Python.

>[!NOTE]
>
>La instalación de un paquete de sistema de esta manera **no** lo instala en el entorno de tiempo de ejecución utilizado para ejecutar Adobe Experience Manager. Si necesita un paquete de sistema instalado en el entorno de AEM, póngase en contacto con su representante de Adobe.

## Omisión de paquetes de contenido {#skipping-content-packages}

En Cloud Manager, las compilaciones pueden producir cualquier número de paquetes de contenido.
Por diversos motivos, puede que sea conveniente crear un paquete de contenido pero no implementarlo. Esto puede resultar útil, por ejemplo, cuando se generan paquetes de contenido que solo se utilizan para pruebas o que se van a volver a empaquetar con otro paso en el proceso de compilación, es decir, como un subpaquete de otro paquete.

Para dar cabida a estos escenarios, Cloud Manager buscará una propiedad denominada ***cloudManagerTarget*** en las propiedades de los paquetes de contenido creados. Si esta propiedad se establece en “ninguno”, el paquete se omitirá y no se implementará. El mecanismo para establecer esta propiedad depende de la forma en que la compilación produce el paquete de contenido. Por ejemplo, con el complemento filevault-maven-plugin puede configurar el complemento de esta manera:

```xml
        <plugin>
            <groupId>org.apache.jackrabbit</groupId>
            <artifactId>filevault-package-maven-plugin</artifactId>
            <extensions>true</extensions>
            <configuration>
                <properties>
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
        <!-- other configuration -->
            </configuration>
        </plugin>
```

Con el content-package-maven-plugin es similar:

```xml
        <plugin>
            <groupId>com.day.jcr.vault</groupId>
            <artifactId>content-package-maven-plugin</artifactId>
            <extensions>true</extensions>
            <configuration>
                <properties>
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
        <!-- other configuration -->
            </configuration>
        </plugin>
```
