---
title: 'Paquete de estructura del repositorio de proyectos de AEM  '
description: Adobe Experience Manager como Cloud Service de proyectos Maven requiere una definición de subpaquete de estructura de repositorio cuyo único propósito es definir las raíces del repositorio JCR en las que se implementan los subpaquetes de código del proyecto.
translation-type: tm+mt
source-git-commit: a6820eab30f2b318d62d2504cb17c12081a320a3
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 9%

---


# Paquete de estructura del repositorio de proyectos de AEM

Los proyectos Maven para Adobe Experience Manager como Cloud Service requieren una definición de subpaquete de estructura de repositorio cuyo único propósito es definir las raíces del repositorio JCR en las que se implementan los subpaquetes de código del proyecto. Esto garantiza que la instalación de paquetes en Experience Manager como Cloud Service se ordene automáticamente por las dependencias de recursos de JCR. La falta de dependencias puede dar lugar a situaciones en las que las subestructuras se instalarían por encima de sus estructuras principales y, por lo tanto, se eliminarían inesperadamente, con lo que se rompería la implementación.

Si el paquete de código se implementa en una ubicación **no cubierta** por el paquete de código, cualquier recurso antecesor (recursos JCR más cercanos a la raíz JCR) debe enumerarse en el paquete de estructura del repositorio para establecer estas dependencias.

![Paquete de estructura de repositorio](./assets/repository-structure-packages.png)

El paquete de estructura del repositorio define el estado común esperado de `/apps` que utiliza el validador de paquetes para determinar las áreas &quot;seguras de posibles conflictos&quot; ya que son raíces estándar.

Las rutas más típicas que se incluirán en el paquete de estructura del repositorio son:

+ `/apps` que es un nodo proporcionado por el sistema
+ `/apps/cq/...`,  `/apps/dam/...`,  `/apps/wcm/...`y  `/apps/sling/...` que proporcionan superposiciones comunes para  `/libs`.
+ `/apps/settings` que es la ruta raíz de configuración compartida según el contexto

Tenga en cuenta que este subpaquete **no tiene** contenido y está compuesto únicamente por `pom.xml` que define las raíces del filtro.

## Creación del paquete de estructura del repositorio

Para crear un paquete de estructura de repositorio para el proyecto Maven, cree un nuevo subproyecto vacío Maven, con el siguiente `pom.xml`, actualizando los metadatos del proyecto para que se ajusten al proyecto principal Maven.

Actualice el `<filters>` para incluir todas las rutas del repositorio JCR que originan sus paquetes de código implementados en.

Asegúrese de agregar este nuevo subproyecto Maven a la lista `<modules>` de proyectos principales.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <!-- ====================================================================== -->
    <!-- P A R E N T  P R O J E C T  D E S C R I P T I O N                      -->
    <!-- ====================================================================== -->
    <parent>
        <groupId>com.my-company</groupId>
        <artifactId>my-app</artifactId>
        <version>x.x.x</version>
        <relativePath>../pom.xml</relativePath>
    </parent>

    <!-- ====================================================================== -->
    <!-- P R O J E C T  D E S C R I P T I O N                                   -->
    <!-- ====================================================================== -->
    <artifactId>ui.apps.structure</artifactId>
    <packaging>content-package</packaging>
    <name>UI Apps Structure - Repository Structure Package for /apps</name>

    <description>
        Empty package that defines the structure of the Adobe Experience Manager repository the code packages in this project deploy into.
        Any roots in the code packages of this project should have their parent enumerated in the filters list below.
    </description>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.jackrabbit</groupId>
                <artifactId>filevault-package-maven-plugin</artifactId>
                <extensions>true</extensions>
                <properties>
                    <!-- Set Cloud Manager Target to none, else this package will be deployed and remove all defined filter roots -->
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
                <configuration>
                    <properties>
                        <!-- Set Cloud Manager Target to none, else this package will be deployed and remove all defined filter roots -->
                        <cloudManagerTarget>none</cloudManagerTarget>
                    </properties>
                    <filters>

                        <!-- /apps root -->
                        <filter><root>/apps</root></filter>

                        <!--
                        Examples of complex roots


                        Overlays of /libs typically require defining the overlayed structure, at each level here.

                        For example, adding a new section to the main AEM Tools navigation, necessitates the following rules:

                        <filter><root>/apps/cq</root></filter>
                        <filter><root>/apps/cq/core</root></filter>
                        <filter><root>/apps/cq/core/content</root></filter>
                        <filter><root>/apps/cq/core/content/nav/</root></filter>
                        <filter><root>/apps/cq/core/content/nav/tools</root></filter>


                        Any /apps level Context-aware configurations need to enumerated here. 
                        
                        For example, providing email templates under `/apps/settings/notification-templates/com.day.cq.replication` necessitates the following rules:

                        <filter><root>/apps/settings</root></filter>
                        <filter><root>/apps/settings/notification-templates</root></filter>
                        <filter><root>/apps/settings/notification-templates/com.day.cq.replication</root></filter>
                        -->

                    </filters>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

## Referencia al paquete de estructura del repositorio

Para utilizar el paquete de estructura del repositorio, haga referencia a él a través de todos los paquetes de código (los subpaquetes que se implementan en `/apps`) proyectos de Maven a través de la configuración `<repositoryStructurePackage>` del paquete de contenido de FileVault.

En `ui.apps/pom.xml` y cualquier otro paquete de código `pom.xml`s, agregue una referencia a la configuración del paquete de estructura de repositorio del proyecto (#repository-structure-package) al complemento Maven del paquete FileVault.

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        ...
        <repositoryStructurePackages>
          <repositoryStructurePackage>
              <groupId>${project.groupId}</groupId>
              <artifactId>ui.apps.structure</artifactId>
              <version>${project.version}</version>
          </repositoryStructurePackage>
        </repositoryStructurePackages>
      </configuration>
    </plugin>
    ...
</build>
<dependencies>
    <!-- Add the dependency for the repository structure package so it resolves -->
    <dependency>
        <groupId>${project.groupId}</groupId>
        <artifactId>ui.apps.structure</artifactId>
        <version>${project.version}</version>
        <type>zip</type>
    </dependency>
    ...
</dependencies>
```

## Caso de uso de paquetes de varios códigos

Un caso de uso menos común y más complejo es el soporte para la implementación de varios paquetes de código que se instalan en las mismas áreas del repositorio JCR.

Por ejemplo:

+ El paquete de código A se implementa en `/apps/a`
+ El paquete de código B se implementa en `/apps/a/b`

Si no se establece una dependencia de nivel de paquete a partir del paquete de código B en el paquete de código A, el paquete de código B puede implementarse primero en `/apps/a`, seguido del paquete de código B, que se implementa en `/apps/a`, lo que resulta en la eliminación del `/apps/a/b` previamente instalado.

En este caso:

+ El paquete de código A debe definir un `<repositoryStructurePackage>` en el paquete de estructura de repositorio del proyecto (que debe tener un filtro para `/apps`).
+ El paquete de código B debe definir un `<repositoryStructurePackage>` en el paquete de código A, porque el paquete de código B se implementa en el espacio compartido por el paquete de código A.

## Errores y depuración

Si los paquetes de estructura de repositorio no están correctamente configurados, en la compilación de Maven se mostrará un error:

```
1 error(s) detected during dependency analysis.
Filter root's ancestor '/apps/some/path' is not covered by any of the specified dependencies.
```

Esto indica que el paquete de código de interrupción no tiene una `<repositoryStructurePackage>` que lista `/apps/some/path` en su lista de filtro.

## Recursos adicionales

+ [Complemento Maven del paquete de contenido de FileVault](http://jackrabbit.apache.org/filevault-package-maven-plugin/)
