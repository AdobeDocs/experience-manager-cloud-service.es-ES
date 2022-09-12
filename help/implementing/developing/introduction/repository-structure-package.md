---
title: Paquete de estructura del repositorio de proyectos de AEM
description: Los proyectos de Adobe Experience Manager as a Cloud Service Maven requieren una definición de subpaquete de estructura de repositorio cuyo único propósito es definir las raíces del repositorio JCR en el que se implementan los subpaquetes de código del proyecto.
exl-id: dec08410-d109-493d-bf9d-90e5556d18f0
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 9%

---

# Paquete de estructura del repositorio de proyectos de AEM

Los proyectos Maven para Adobe Experience Manager as a Cloud Service requieren una definición de subpaquete de estructura de repositorio cuyo único propósito es definir las raíces del repositorio JCR en las que se implementan los subpaquetes de código del proyecto. Esto garantiza que la instalación de paquetes en el Experience Manager as a Cloud Service se ordene automáticamente mediante dependencias de recursos JCR. Las dependencias que faltan pueden dar lugar a escenarios en los que las subestructuras se instalarían antes que sus estructuras principales y, por lo tanto, se eliminarían de forma inesperada, lo que rompe la implementación.

Si el paquete de código se implementa en una ubicación **no cubierta** por el paquete de código, cualquier recurso antecesor (recursos JCR más cercanos a la raíz JCR) debe enumerarse en el paquete de estructura del repositorio para establecer estas dependencias.

![Paquete de estructura del repositorio](./assets/repository-structure-packages.png)

El paquete de estructura del repositorio define el estado común esperado de `/apps` que el validador de paquetes utiliza para determinar las áreas &quot;seguras frente a posibles conflictos&quot;, ya que son raíces estándar.

Las rutas más típicas para incluir en el paquete de estructura del repositorio son:

+ `/apps` que es un nodo proporcionado por el sistema
+ `/apps/cq/...`, `/apps/dam/...`, `/apps/wcm/...`y `/apps/sling/...` que proporcionan superposiciones comunes para `/libs`.
+ `/apps/settings` que es la ruta raíz de configuración compartida según el contexto

Tenga en cuenta que este subpaquete **no tiene** cualquier contenido y está compuesto únicamente por un `pom.xml` definición de las raíces del filtro.

## Creación del paquete de estructura del repositorio

Para crear un paquete de estructura de repositorios para su proyecto Maven, cree un nuevo subproyecto vacío de Maven, con lo siguiente `pom.xml`, actualizando los metadatos del proyecto para que se ajusten al proyecto principal de Maven.

Actualice el `<filters>` para incluir todas las rutas del repositorio JCR, los paquetes de código se implementan en .

Asegúrese de agregar este nuevo subproyecto Maven a los proyectos principales `<modules>` lista.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/maven-v4_0_0.xsd">
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

Para utilizar el paquete de estructura del repositorio, haga referencia a él a través de todos los paquetes de código (los subpaquetes que se implementan en `/apps`) Proyectos Maven a través del paquete de contenido FileVault Complementos Maven `<repositoryStructurePackage>` configuración.

En el `ui.apps/pom.xml`y cualquier otro paquete de código `pom.xml`s, agregue una referencia a la configuración del paquete de estructura de repositorios del proyecto (#repository-structure-package) al complemento Maven del paquete FileVault.

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

## Caso de uso de paquete de varios códigos

Un caso de uso menos común y más complejo es el soporte para la implementación de varios paquetes de código que se instalan en las mismas áreas del repositorio JCR.

Por ejemplo:

+ El paquete de código A se implementa en `/apps/a`
+ El paquete de código B se implementa en `/apps/a/b`

Si no se establece una dependencia de nivel de paquete a partir del paquete de código B en el paquete de código A, el paquete de código B puede implementarse primero en `/apps/a`, seguido del paquete de código B, que se implementa en `/apps/a`, lo que resulta en la eliminación de los `/apps/a/b`.

En este caso:

+ El paquete de código A debe definir una `<repositoryStructurePackage>` en el paquete de estructura del repositorio del proyecto (que debería tener un filtro para `/apps`).
+ El paquete de código B debe definir una `<repositoryStructurePackage>` en el paquete de código A, porque el paquete de código B se implementa en el espacio compartido por el paquete de código A.

## Errores y depuración

Si los paquetes de estructura del repositorio no están correctamente configurados, en la compilación de Maven se notificará un error:

```
1 error(s) detected during dependency analysis.
Filter root's ancestor '/apps/some/path' is not covered by any of the specified dependencies.
```

Esto indica que el paquete de código de interrupción no tiene un `<repositoryStructurePackage>` que `/apps/some/path` en su lista de filtros.

## Recursos adicionales

+ [Complemento Maven del paquete de contenido de FileVault](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
