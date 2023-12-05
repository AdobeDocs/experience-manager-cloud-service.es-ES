---
title: Configuración del proyecto
description: Descubra cómo se crean los proyectos AEM con Maven y los estándares que debe observar al crear su propio proyecto.
exl-id: 76af0171-8ed5-4fc7-b5d5-7da5a1a06fa8
source-git-commit: abe5f8a4b19473c3dddfb79674fb5f5ab7e52fbf
workflow-type: tm+mt
source-wordcount: '1399'
ht-degree: 96%

---

# Configuración del proyecto {#project-setup}

Descubra cómo se crean los proyectos AEM con Maven y los estándares que debe observar al crear su propio proyecto.

## Detalles de configuración del proyecto {#project-setup-details}

Para crear e implementar correctamente con Cloud Manager, los proyectos de AEM deben cumplir las siguientes directrices:

* Los proyectos deben crearse con [Apache Maven.](https://maven.apache.org)
* Debe haber un archivo `pom.xml` en la raíz del repositorio de Git. El archivo `pom.xml` puede hacer referencia a tantos submódulos (que a su vez pueden tener otros submódulos) como sea necesario.
* Puede agregar referencias a repositorios de artefactos de Maven adicionales en sus archivos `pom.xml`.
   * El acceso a [repositorios de artefactos protegidos por contraseña](#password-protected-maven-repositories) se admite cuando se configura. Sin embargo, no se admite el acceso a repositorios de artefactos protegidos por la red.
* Los paquetes de contenido que se pueden implementar se descubren al analizar los archivos `.zip` del paquete de contenido, que se encuentran en un directorio denominado `target`.
   * Cualquier número de módulos secundarios puede producir paquetes de contenido.
* Los artefactos de Dispatcher que se pueden implementar se detectan al analizar archivos `.zip` (también incluidos en el directorio denominado `target`), que tienen directorios llamados `conf` y `conf.d`.
* Si hay más de un paquete de contenido, no se garantiza la ordenación de las implementaciones de paquetes.
   * Si se necesita un orden específico, se pueden utilizar dependencias del paquete de contenido para definir el orden.
* Los paquetes pueden [omitirse](#skipping-content-packages) durante la implementación.

## Activar perfiles de Maven en Cloud Manager {#activating-maven-profiles-in-cloud-manager}

En algunos casos limitados, es posible que tenga que variar ligeramente el proceso de generación al ejecutarse dentro de Cloud Manager, en lugar de hacerlo en las estaciones de trabajo de los desarrolladores. Para estos casos, los [Perfiles de Maven](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) se pueden utilizar para definir cómo la generación debe ser diferente en diferentes entornos, incluido Cloud Manager.

La activación de un perfil de Maven dentro del entorno de generación de Cloud Manager debe realizarse al buscar la `CM_BUILD` [variable de entorno](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md). Del mismo modo, un perfil que se pretenda usar solo fuera del entorno de generación de Cloud Manager debe realizarse al buscar la ausencia de esta variable.

Por ejemplo, debe hacerlo si desea enviar un mensaje simple solo cuando la generación se ejecuta dentro de Cloud Manager.

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
>Para probar este perfil en una estación de trabajo de desarrolladores, puede activarlo en la línea de comandos (con `-PcmBuild`) o en su entorno de desarrollo integrado (IDE).

Y también debe hacerlo si desea enviar un mensaje simple solo cuando la generación se ejecuta fuera de Cloud Manager.

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

## Compatibilidad con repositorios de Maven protegidos por contraseña {#password-protected-maven-repositories}

>[!NOTE]
>
>Los artefactos de un repositorio Maven protegido por contraseña deben utilizarse con precaución porque el código implementado mediante este mecanismo actualmente no se ejecuta a través de [reglas de calidad de código](/help/implementing/cloud-manager/custom-code-quality-rules.md) implementado en las puertas de calidad de Cloud Manager. Por lo tanto, solo debe utilizarse en casos excepcionales y para código no vinculado a AEM. También se recomienda implementar las fuentes Java, así como todo el código fuente del proyecto junto con el binario.

Para utilizar un repositorio de Maven protegido por contraseña en Cloud Manager, haga lo siguiente:

1. Especifique la contraseña (y, opcionalmente, el nombre de usuario) como un secreto en la [variable de canalización](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md).
1. A continuación, haga referencia a ese secreto dentro de un archivo llamado `.cloudmanager/maven/settings.xml` en el repositorio de Git, que sigue al esquema [Archivo de configuración de Maven](https://maven.apache.org/settings.html).

Cuando se inicia el proceso de generación de Cloud Manager:

* El elemento `<servers>` de este archivo se combina con el archivo predeterminado `settings.xml` proporcionado por Cloud Manager.
   * ID de servidor que empiezan por `adobe` y `cloud-manager` se consideran reservados. No los utilice en servidores personalizados.
   * Los Id. de servidor que no coinciden con uno de estos prefijos o con el Id. predeterminado `central` nunca se reflejarán en Cloud Manager.
* Con este archivo en su lugar, se hará referencia al Id. del servidor desde un `<repository>` y/o un elemento `<pluginRepository>` dentro del archivo `pom.xml`.
* Generalmente, estos `<repository>` y/o elementos `<pluginRepository>` están dentro de un [perfil específico de Cloud Manager](#activating-maven-profiles-in-cloud-manager), aunque no es estrictamente necesario.

Por ejemplo, supongamos que el repositorio se encuentra en `https://repository.myco.com/maven2`, el nombre de usuario que debe usar Cloud Manager es `cloudmanager`y la contraseña es `secretword`. Debería seguir los siguientes pasos.

1. Establecer la contraseña como un secreto en la canalización.

   ```text
   $ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword`
   ```

1. Hacer referencia a esto desde el archivo `.cloudmanager/maven/settings.xml`.

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <settings xmlns="https://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="https://maven.apache.org/SETTINGS/1.0.0 https://maven.apache.org/xsd/settings-1.0.0.xsd">
       <servers>
           <server>
               <id>myco-repository</id>
               <username>cloudmanager</username>
              <password>${env.CUSTOM_MYCO_REPOSITORY_PASSWORD}</password>
           </server>
       </servers>
   </settings>
   ```

1. Finalmente, hacer referencia al Id. del servidor dentro del archivo `pom.xml`:

   ```xml
   <profiles>
       <profile>
           <id>cmBuild</id>
           <activation>
                   <property>
                       <name>env.CM_BUILD</name>
                   </property>
           </activation>
           <repositories>
                <repository>
                    <id>myco-repository</id>
                    <name>MyCo Releases</name>
                    <url>https://repository.myco.com/maven2</url>
                    <snapshots>
                        <enabled>false</enabled>
                    </snapshots>
                    <releases>
                        <enabled>true</enabled>
                    </releases>
                </repository>
            </repositories>
            <pluginRepositories>
                <pluginRepository>
                    <id>myco-repository</id>
                    <name>MyCo Releases</name>
                    <url>https://repository.myco.com/maven2</url>
                    <snapshots>
                        <enabled>false</enabled>
                    </snapshots>
                    <releases>
                        <enabled>true</enabled>
                    </releases>
                </pluginRepository>
            </pluginRepositories>
       </profile>
   </profiles>
   ```

### Implementar fuentes {#deploying-sources}

Se recomienda implementar las fuentes Java junto con el binario en un repositorio de Maven.

Para ello, configure el complemento maven-source-plugin en su proyecto.

```xml
         <plugin>
             <groupId>org.apache.maven.plugins</groupId>
             <artifactId>maven-source-plugin</artifactId>
             <executions>
                 <execution>
                     <id>attach-sources</id>
                     <goals>
                         <goal>jar-no-fork</goal>
                     </goals>
                 </execution>
             </executions>
         </plugin>
```

### Implementar fuentes de proyecto {#deploying-project-sources}

Se recomienda implementar todo el origen del proyecto junto con el binario en un repositorio de Maven. Esto permite reconstruir el artefacto exacto.

Para ello, configure el complemento maven-assembly-plugin en su proyecto.

```xml
         <plugin>
             <groupId>org.apache.maven.plugins</groupId>
             <artifactId>maven-assembly-plugin</artifactId>
             <executions>
                 <execution>
                     <id>project-assembly</id>
                     <phase>package</phase>
                     <goals>
                         <goal>single</goal>
                     </goals>
                     <configuration>
                         <descriptorRefs>
                             <descriptorRef>project</descriptorRef>
                         </descriptorRefs>
                     </configuration>
                 </execution>
             </executions>
         </plugin>
```

## Omitir paquetes de contenido {#skipping-content-packages}

En Cloud Manager, las generaciones pueden producir cualquier cantidad de paquetes de contenido. Por varios motivos, puede ser recomendable producir un paquete de contenido, pero no implementarlo. Por ejemplo, al crear paquetes de contenido que solo se utilizan para pruebas o que se van a volver a empaquetar mediante otro paso en el proceso de generación. Es decir, un subpaquete de otro paquete.

Para dar cabida a estos escenarios, Cloud Manager busca una propiedad denominada `cloudManagerTarget` en las propiedades de los paquetes de contenido creados. Si esta propiedad se establece en `none`, el paquete se omite y no se implementa.

El mecanismo para establecer esta propiedad depende de la forma en que la generación produce el paquete de contenido. Por ejemplo, con `filevault-maven-plugin` puede configurar el complemento de esta manera.

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

`content-package-maven-plugin` tiene una configuración similar.

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

## Reutilización de artefactos de generación {#build-artifact-reuse}

En muchos casos, el mismo código se implementa en varios entornos de AEM. Cuando sea posible, Cloud Manager evitará la regeneración del código base cuando detecte que se utiliza el mismo compromiso de Git en varias ejecuciones de canalización full-stack.

Cuando se inicia una ejecución, se extrae el compromiso de HEAD actual para la canalización de ramas. El hash de compromiso se puede ver en la interfaz de usuario y a través de la API. Cuando el paso de generación se completa correctamente, los artefactos resultantes se almacenan en base a ese hash de compromiso y se pueden reutilizar en ejecuciones de canalización posteriores.

Los paquetes se reutilizan en todas las canalizaciones si están en el mismo programa. Al buscar paquetes que puedan reutilizarse, AEM ignora las ramas y vuelve a utilizar artefactos a través de las ramas.

Cuando se produce una reutilización, los pasos de generación y calidad del código se sustituyen eficazmente por los resultados de la ejecución original. El archivo de registro para el paso de generación enumerará los artefactos y la información de ejecución que se utilizó para crearlos originalmente.

El siguiente es un ejemplo de este resultado de registro.

```shell
The following build artifacts were reused from the prior execution 4 of pipeline 1 which used commit f6ac5e6943ba8bce8804086241ba28bd94909aef:
build/aem-guides-wknd.all-2021.1216.1101633.0000884042.zip (content-package)
build/aem-guides-wknd.dispatcher.cloud-2021.1216.1101633.0000884042.zip (dispatcher-configuration)
```

El registro del paso de calidad del código contiene información similar.

### Ejemplos {#example-reuse}

#### Ejemplo 1 {#example-1}

Imagine que su programa tiene dos canalizaciones de desarrollo:

* Canalización 1 en rama `foo`
* Canalización 2 en rama `bar`

Ambas ramas están en el mismo Id. de compromiso.

1. Al ejecutar la Canalización 1 primero, se crearán los paquetes normalmente.
1. A continuación, al ejecutar la Canalización 2, se reutilizarán los paquetes creados por la Canalización 1.

#### Ejemplo 2 {#example-2}

Imagine que el programa tiene dos ramas:

* Rama `foo`
* Rama `bar`

Ambas ramas tienen el mismo Id. de compromiso.

1. Se genera y ejecuta una canalización de desarrollo `foo`.
1. Posteriormente, se genera y ejecuta una canalización de producción `bar`.

En este caso, el artefacto de `foo` se reutiliza para la canalización de producción, ya que se identificó el mismo hash de compromiso.

### Exclusión {#opting-out}

Si lo desea, el comportamiento de reutilización se puede deshabilitar para canalizaciones específicas si configura la variable de canalización `CM_DISABLE_BUILD_REUSE` a `true`. Si se establece esta variable, el hash de compromiso se extrae y los artefactos resultantes se almacenan para su uso posterior, pero los artefactos almacenados anteriormente no se reutilizan. Para comprender este comportamiento, imagine el siguiente escenario.

1. Se crea una nueva canalización.
1. La canalización se ejecuta (ejecución #1) y el compromiso de HEAD actual es `becdddb`. La ejecución se realiza correctamente y se almacenan los artefactos resultantes.
1. La variable `CM_DISABLE_BUILD_REUSE` está configurada.
1. La canalización se vuelve a ejecutar sin cambiar el código. Aunque hay artefactos almacenados asociados con `becdddb`, no se vuelven a utilizar debido a la variable `CM_DISABLE_BUILD_REUSE`.
1. El código se cambia y se ejecuta la canalización. El compromiso de HEAD es ahora `f6ac5e6`. La ejecución se realiza correctamente y se almacenan los artefactos resultantes.
1. La variable `CM_DISABLE_BUILD_REUSE` se elimina.
1. La canalización se vuelve a ejecutar sin cambiar el código. Como hay artefactos almacenados asociados con `f6ac5e6`, esos artefactos se reutilizan.

### Advertencias {#caveats}

* Los artefactos de generación no se reutilizan en programas diferentes, independientemente de si el hash de compromiso es idéntico.
* Los artefactos de generación se reutilizan dentro del mismo programa incluso si la rama o canalización son diferentes.
* [El tratamiento de las versiones de Maven](/help/implementing/cloud-manager/managing-code/project-version-handling.md) reemplaza a la versión del proyecto solo en las canalizaciones de producción. Por lo tanto, si se utiliza el mismo compromiso tanto en la ejecución de una implementación de desarrollo como en la ejecución de una canalización de producción, y la canalización de implementación de desarrollo se ejecuta primero, las versiones se implementan en fase y producción sin sufrir cambios. Sin embargo, se seguirá creando una etiqueta en este caso.
* Si la recuperación de los artefactos almacenados no se realiza correctamente, el paso de generación se ejecuta como si no se hubieran almacenado artefactos.
* Las variables de canalización distintas de `CM_DISABLE_BUILD_REUSE` no se tienen en cuenta cuando Cloud Manager decide reutilizar los artefactos de generación creados anteriormente.
