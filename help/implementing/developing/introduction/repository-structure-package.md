---
title: Paquete de estructura del repositorio de proyectos de AEM
description: Los proyectos de Adobe Experience Manager as a Cloud Service Maven requieren una definición de subpaquete de estructura de repositorio cuyo único propósito sea definir las raíces del repositorio JCR en las que se implementan los subpaquetes de código del proyecto.
exl-id: dec08410-d109-493d-bf9d-90e5556d18f0
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 9%

---

# Paquete de estructura del repositorio de proyectos de AEM

Los proyectos de Maven para Adobe Experience Manager as a Cloud Service requieren una definición de subpaquete de estructura de repositorio cuyo único propósito es definir las raíces del repositorio JCR en las que se implementan los subpaquetes de código del proyecto. Esto garantiza que las dependencias de recursos JCR ordenen automáticamente la instalación de paquetes en Experience Manager as a Cloud Service. Las dependencias que faltan pueden dar lugar a escenarios en los que las subestructuras se instalarían antes que sus estructuras principales y, por lo tanto, se eliminarían inesperadamente, lo que rompería la implementación.

Si el paquete de código se implementa en una ubicación **no cubierta** por el paquete de código, cualquier recurso antecesor (recursos JCR más cercanos a la raíz JCR) debe enumerarse en el paquete de estructura del repositorio para establecer estas dependencias.

![Paquete de estructura de repositorio](./assets/repository-structure-packages.png)

El paquete de estructura del repositorio define el estado esperado y común de `/apps` que el validador de paquetes utiliza para determinar las áreas &quot;seguras frente a posibles conflictos&quot;, ya que son raíces estándar.

Las rutas más típicas que se incluyen en el paquete de estructura del repositorio son:

+ `/apps` que es un nodo proporcionado por el sistema
+ `/apps/cq/...`, `/apps/dam/...`, `/apps/wcm/...`, y `/apps/sling/...` que proporcionan superposiciones comunes para `/libs`.
+ `/apps/settings` que es la ruta raíz de la configuración compartida según el contexto

Tenga en cuenta que este subpaquete **no tiene** cualquier contenido y está compuesto únicamente por un `pom.xml` definición de las raíces del filtro.

## Creación del paquete de estructura del repositorio

Para crear un paquete de estructura de repositorio para su proyecto de Maven, cree un nuevo subproyecto de Maven vacío, con lo siguiente `pom.xml`, actualizando los metadatos del proyecto para adaptarlos al proyecto Maven principal.

Actualice el `<filters>` para incluir todas las raíces de ruta del repositorio JCR en las que se implementan los paquetes de código.

Asegúrese de agregar este nuevo subproyecto de Maven a los proyectos principales `<modules>` lista.

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
                    <!-- Set Cloud Manager Target to none, else this package is deployed and remove all defined filter roots -->
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
                <configuration>
                    <properties>
                        <!-- Set Cloud Manager Target to none, else this package is deployed and remove all defined filter roots -->
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

Para utilizar el paquete de estructura del repositorio, haga referencia a él a través del paquete de todos los códigos (los subpaquetes que se implementan en `/apps`) Proyectos Maven a través del paquete de contenido FileVault Complementos Maven `<repositoryStructurePackage>` configuración.

En el `ui.apps/pom.xml`y cualquier otro paquete de código `pom.xml`Como, agregue una referencia a la configuración del paquete de estructura del repositorio (#repository-structure-package) del proyecto al complemento Maven del paquete FileVault.

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

## Caso de uso de paquete de código múltiple

Un caso de uso menos común y más complejo es admitir la implementación de varios paquetes de código que se instalan en las mismas áreas del repositorio JCR.

Por ejemplo:

+ Paquete de código A implementado en `/apps/a`
+ El paquete de código B se implementa en `/apps/a/b`

Si no se establece una dependencia de nivel de paquete a partir del paquete de código B en el paquete de código A, el paquete de código B puede implementarse primero en `/apps/a`, seguido del paquete de código B, que se implementa en `/apps/a`, lo que provoca la eliminación del instalado anteriormente `/apps/a/b`.

En este caso:

+ El paquete de código A debe definir un `<repositoryStructurePackage>` en el paquete de estructura del repositorio del proyecto (que debería tener un filtro para `/apps`).
+ El paquete de código B debe definir un `<repositoryStructurePackage>` en el paquete de código A, ya que el paquete de código B se implementa en el espacio compartido por el paquete de código A.

## Errores y depuración

Si los paquetes de estructura del repositorio no están correctamente configurados, se informa de un error en la compilación de Maven:

```
1 error(s) detected during dependency analysis.
Filter root's ancestor '/apps/some/path' is not covered by any of the specified dependencies.
```

Esto indica que el paquete de código de ruptura no tiene un `<repositoryStructurePackage>` que enumera `/apps/some/path` en su lista de filtros.

## Recursos adicionales

+ [Complemento Maven del paquete de contenido de FileVault](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
