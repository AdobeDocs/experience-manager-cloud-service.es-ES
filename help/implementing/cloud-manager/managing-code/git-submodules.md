---
title: Compatibilidad con los submódulos de Git
description: Obtenga información sobre cómo usar los submódulos de Git para combinar el contenido de varias ramas en los distintos repositorios de Git en el momento de la compilación.
exl-id: fa5b0f49-4b87-4f39-ad50-7e62094d85f4
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 93%

---

# Compatibilidad con los submódulos de Git para repositorios de Adobe {#git-submodule-support}

Los submódulos Git se pueden usar para combinar el contenido de varias ramas en repositorios de Git en el momento de la compilación.

Cuando se ejecuta el proceso de creación de Cloud Manager, después de clonar el repositorio configurado para la canalización y de retirar la rama configurada, si la rama contiene un archivo `.gitmodules` en el directorio raíz, se ejecuta el comando.

El siguiente comando extraerá cada submódulo en el directorio correspondiente.

```
$ git submodule update --init
```

Esta técnica es una alternativa potencial a la solución descrita en el documento [Uso de repositorios de Git de varias fuentes](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md) para organizaciones que se sientan cómodas con el uso de submódulos Git y no desean administrar un proceso de combinación externo.

Por ejemplo, supongamos que hay tres repositorios, cada uno de los cuales contiene una sola rama denominada `main`. En el repositorio principal, es decir, el configurado en las canalizaciones, la rama `main` tiene un archivo `pom.xml` que declara los proyectos contenidos en los otros dos repositorios.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
   
    <groupId>customer.group.id</groupId>
    <artifactId>customer-reactor</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>pom</packaging>
   
    <modules>
        <module>project-a</module>
        <module>project-b</module>
    </modules>
   
</project>
```

Luego agregaría submódulos para los otros dos repositorios.

```shell
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

Esto da como resultado un archivo `.gitmodules` similar al siguiente.

```text
[submodule "project-a"]
    path = project-a
    url = https://git.cloudmanager.adobe.com/ProgramName/projectA/
    branch = main
[submodule "project-b"]
    path = project-b
    url = https://git.cloudmanager.adobe.com/ProgramName/projectB/
    branch = main
```

Puede encontrar más información sobre los submódulos Git en el [Manual de referencia de Git.](https://git-scm.com/book/en/v2/Git-Tools-Submodules)

### Limitaciones y recomendaciones {#limitations-recommendations}

Cuando utilice submódulos Git con repositorios administrados por Adobe, tenga en cuenta las siguientes limitaciones.

* La dirección URL de Git debe estar exactamente en la sintaxis descrita en la sección anterior.
* Solo se admiten submódulos en la raíz de la rama.
* Por motivos de seguridad, no incruste credenciales en las direcciones URL de Git.
* A menos que sea necesario, se recomienda encarecidamente utilizar submódulos superficiales.
   * Para ello, ejecute `git config -f .gitmodules submodule.<submodule path>.shallow true` para cada submódulo.
* Las referencias del submódulo Git se almacenan en confirmaciones de Git específicas. Como resultado, cuando se realizan cambios en el repositorio de submódulos, se debe actualizar la confirmación a la que se hace referencia.
   * Por ejemplo, utilizando `git submodule update --remote`

## Compatibilidad con los submódulos de Git para repositorios privados {#private-repositories}

La compatibilidad con los submódulos de Git al utilizar [repositorios privados](private-repositories.md) es prácticamente la misma que cuando se usan repositorios de Adobe.

Sin embargo, después de configurar su archivo `pom.xml` y ejecutar los comandos `git submodule`, debe añadir un archivo `.gitmodules` al directorio raíz del repositorio de agregación para que Cloud Manager detecte la configuración del submódulo.

![Archivo .gitmodules](assets/gitmodules.png)

![Agregador](assets/aggregator.png)

### Limitaciones y recomendaciones {#limitations-recommendations-private-repos}

Cuando utilice submódulos de Git con repositorios privados, tenga en cuenta las siguientes limitaciones.

* Las direcciones URL de Git para los submódulos pueden estar en formato HTTPS o SSH, pero deben vincularse a un repositorio de github.com
   * Añadir un submódulo de repositorio de Adobe a un repositorio de agregación de GitHub, o viceversa, no funcionará.
* Los submódulos de GitHub deben ser accesibles para la aplicación de Adobe GitHub.
* [Las limitaciones de uso de submódulos de Git con repositorios administrados por Adobe](#limitations-recommendations) también se aplican.
