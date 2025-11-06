---
title: Paquete de estructura del repositorio de proyectos de AEM
description: Los proyectos de Maven en Adobe Experience Manager as a Cloud Service requieren una definición de subpaquete de estructura de repositorio cuyo único propósito sea definir las raíces del repositorio JCR en las que se implementan los subpaquetes de código del proyecto.
exl-id: dec08410-d109-493d-bf9d-90e5556d18f0
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 2%

---

# Paquete de estructura del repositorio de proyectos de AEM

Los proyectos de Maven para Adobe Experience Manager as a Cloud Service requieren una definición de subpaquete de estructura de repositorio cuyo único propósito es definir las raíces del repositorio JCR en las que se implementan los subpaquetes de código del proyecto. Este método garantiza que las dependencias de recursos JCR ordenen automáticamente la instalación de paquetes en Experience Manager as a Cloud Service. Las dependencias que faltan pueden dar lugar a escenarios en los que las subestructuras se instalarían antes que sus estructuras principales y, por lo tanto, se eliminarían inesperadamente, lo que rompería la implementación.

Si el paquete de código se implementa en una ubicación **no cubierta** por el paquete de código, cualquier recurso antecesor (recursos JCR más cercanos a la raíz JCR) debe enumerarse en el paquete de estructura del repositorio. Este proceso es necesario para establecer estas dependencias.

![Paquete de estructura de repositorio](./assets/repository-structure-packages.png)

El paquete de estructura del repositorio define el estado común esperado de `/apps` que el validador del paquete utiliza para determinar las áreas &quot;seguras frente a posibles conflictos&quot;, ya que son raíces estándar.

Las rutas más típicas que se incluyen en el paquete de estructura del repositorio son:

+ `/apps`, que es un nodo proporcionado por el sistema
+ `/apps/cq/...`, `/apps/dam/...`, `/apps/wcm/...` y `/apps/sling/...`, que proporcionan superposiciones comunes para `/libs`.
+ `/apps/settings` que es la ruta de acceso raíz de la configuración compartida según el contexto

Este subpaquete **no tiene** contenido y se compone únicamente de `pom.xml` que define las raíces del filtro.

## Creación del paquete de estructura del repositorio

Para crear un paquete de estructura de repositorio para su proyecto de Maven, cree un subproyecto de Maven vacío, con los siguientes `pom.xml`, actualizando los metadatos del proyecto para que se ajusten a su proyecto de Maven principal.

Actualice `<filters>` para incluir todas las raíces de ruta del repositorio JCR en las que se implementan los paquetes de código.

Asegúrese de agregar este nuevo subproyecto Maven a la lista de proyectos principales `<modules>`.

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


                        Overlays of /libs typically require defining the overlay structure, at each level here.

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

Para utilizar el paquete de estructura del repositorio, haga referencia a él a través del paquete de código completo (los subpaquetes que se implementan en `/apps`) y a los proyectos Maven a través de la configuración de los complementos Maven del paquete de contenido FileVault `<repositoryStructurePackage>`.

En `ui.apps/pom.xml`, y en cualquier otro paquete de código `pom.xml`s, agregue una referencia a la configuración del paquete de estructura de repositorio (#repository-structure-package) del proyecto al complemento Maven del paquete FileVault.

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

+ El paquete de código A se implementa en `/apps/a`
+ El paquete de código B se implementa en `/apps/a/b`

Si no se establece una dependencia de nivel de paquete a partir del paquete de código B en el paquete de código A, el paquete de código B puede implementarse primero en `/apps/a`. Si va seguido del paquete de código A, que se implementa en `/apps/a`, el resultado es la eliminación del `/apps/a/b` instalado anteriormente.

En este caso:

+ El paquete de código A debe definir un `<repositoryStructurePackage>` en el paquete de estructura del repositorio del proyecto (que debe tener un filtro para `/apps`).
+ El paquete de código B debe definir un `<repositoryStructurePackage>` en el paquete de código A, ya que el paquete de código B se implementa en el espacio compartido por el paquete de código A.

## Errores y depuración

Si los paquetes de estructura del repositorio no están correctamente configurados, se informa de un error en la compilación de Maven:

```
1 error(s) detected during dependency analysis.
Filter root's ancestor '/apps/some/path' is not covered by any of the specified dependencies.
```

Este error indica que el paquete de código de ruptura no tiene un `<repositoryStructurePackage>` que enumere `/apps/some/path` en su lista de filtros.

## Recursos adicionales

+ [Complemento Maven del paquete de contenido FileVault](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
