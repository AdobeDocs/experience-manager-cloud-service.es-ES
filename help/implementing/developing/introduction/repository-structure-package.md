---
title: 'Desarrollar un paquete de estructura de repositorio   '
description: Adobe Experience Manager como proyecto de Cloud Service Maven requiere una definición de subpaquete de estructura de repositorio cuyo único propósito es definir las raíces del repositorio JCR en las que se implementan los subpaquetes de código del proyecto.
translation-type: tm+mt
source-git-commit: 46d556fdf28267a08e5021f613fbbea75872ef21

---


# Desarrollar un paquete de estructura de repositorio

Los proyectos Maven para Adobe Experience Manager como servicio de nube requieren una definición de subpaquete de estructura de repositorio cuyo único propósito es definir las raíces del repositorio JCR en las que se implementan los subpaquetes de código del proyecto. Esto garantiza la instalación de paquetes en Experience Manager, ya que las dependencias de recursos de JCR solicitan automáticamente un servicio de nube. La falta de dependencias puede dar lugar a situaciones en las que las subestructuras se instalarían por encima de sus estructuras principales y, por lo tanto, se eliminarían inesperadamente, con lo que se rompería la implementación.

Si el paquete de código se implementa en una ubicación **no cubierta** por el paquete de código, cualquier recurso antecesor (recursos JCR más cercanos a la raíz JCR) debe enumerarse en el paquete de estructura del repositorio para establecer estas dependencias.

![Paquete de estructura de repositorio](./assets/repository-structure-packages.png)

El paquete de estructura del repositorio define el estado común esperado del `/apps` que el validador de paquetes utiliza para determinar las áreas &quot;seguras de posibles conflictos&quot; ya que son raíces estándar.

Las rutas más típicas que se incluirán en el paquete de estructura del repositorio son:

+ `/apps` que es un nodo proporcionado por el sistema
+ `/apps/cq/...`, `/apps/dam/...`, `/apps/wcm/...`y `/apps/sling/...` que proporcionan superposiciones comunes para `/libs`.
+ `/apps/settings` que es la ruta raíz de configuración compartida según el contexto

Tenga en cuenta que este subpaquete **no tiene** contenido y está compuesto únicamente por una `pom.xml` definición de las raíces del filtro.

## Creación del paquete de estructura del repositorio

Para crear un paquete de estructura de repositorio para el proyecto Maven, cree un nuevo subproyecto vacío Maven, con lo siguiente `pom.xml`, actualizando los metadatos del proyecto para que se ajusten al proyecto principal Maven.

Actualice el `<filters>` para incluir todas las rutas de repositorio de JCR que originan sus paquetes de código implementados en.

Asegúrese de agregar este nuevo subproyecto Maven a la lista de proyectos principales `<modules>` .

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
    <artifactId>my-app.repository-structure</artifactId>
    <packaging>content-package</packaging>
    <name>My App - Adobe Experience Manager Repository Structure Package</name>

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
                <configuration>
                    <properties>
                        <!-- Set Cloud Manager Target to none, else this package will be deployed and remove all defined filter roots -->
                        <cloudManagerTarget>none</cloudManagerTarget>
                    </properties>
                    <filters>

                        <!-- /apps root -->
                        <filter><root>/apps</root></filter>

                        <!-- Common overlay roots -->
                        <filter><root>/apps/sling</root></filter>
                        <filter><root>/apps/cq</root></filter>
                        <filter><root>/apps/dam</root></filter>
                        <filter><root>/apps/wcm</root></filter>

                        <!-- Immutable context-aware configurations -->
                        <filter><root>/apps/settings</root></filter>

                    </filters>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

## Referencia al paquete de estructura del repositorio

Para utilizar el paquete de estructura del repositorio, haga referencia a él a través de todos los paquetes de código (los subpaquetes que se implementan en `/apps`) los proyectos de Maven a través de la configuración de los complementos de Maven del paquete de contenido de FileVault `<repositoryStructurePackage>` .

En el `ui.apps/pom.xml`, y en cualquier otro paquete `pom.xml`de código, agregue una referencia a la configuración del paquete de estructura de repositorio del proyecto (#repositorio-estructura-paquete) al complemento Maven del paquete FileVault.

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
              <artifactId>my-app.repository-structure</artifactId>
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
        <artifactId>my-app.repository-structure</artifactId>
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

Si no se establece una dependencia de nivel de paquete a partir del paquete de código B en el paquete de código A, el paquete de código B puede implementarse primero en `/apps/a`, seguido del paquete de código B, que se implementa en `/apps/a`, lo que resulta en la eliminación del paquete de código previamente instalado `/apps/a/b`.

En este caso:

+ El paquete de código A debe definir un `<repositoryStructurePackage>` en el paquete de estructura de repositorio del proyecto (para el que debería haber un filtro `/apps`).
+ El paquete de código B debe definir un `<repositoryStructurePackage>` en el paquete de código A, porque el paquete de código B se implementa en el espacio compartido por el paquete de código A.

## Errores y depuración

Si los paquetes de estructura de repositorio no están correctamente configurados, en la compilación de Maven se mostrará un error:

```
1 error(s) detected during dependency analysis.
Filter root's ancestor '/apps/some/path' is not covered by any of the specified dependencies.
```

Esto indica que el paquete de código de salto no tiene un `<repositoryStructurePackage>` que figure `/apps/some/path` en su lista de filtros.

## Recursos adicionales

+ [Complemento Maven del paquete de contenido de FileVault](http://jackrabbit.apache.org/filevault-package-maven-plugin/)
