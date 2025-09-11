---
title: Compatibilidad con los submódulos de Git
description: Obtenga información sobre cómo usar los submódulos de Git para combinar el contenido de varias ramas en los distintos repositorios de Git en el momento de la compilación.
exl-id: fa5b0f49-4b87-4f39-ad50-7e62094d85f4
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 8a53bef8bdf592869c895cbaca1e79034e52f856
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 24%

---

# Compatibilidad con los submódulos de Git para repositorios de Adobe {#git-submodule-support}

Los submódulos Git se pueden usar para combinar el contenido de varias ramas en repositorios Git en el momento de la compilación.

Cuando se ejecuta el proceso de generación de Cloud Manager, clona el repositorio de la canalización y extrae la rama. Si existe un archivo `.gitmodules` en el directorio raíz de la rama, se ejecuta el comando correspondiente.

El siguiente comando extrae cada submódulo en el directorio apropiado.

```
$ git submodule update --init
```

Esta técnica ofrece una alternativa a la solución descrita en [Uso de varios repositorios de Git de Source](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md). Es ideal para organizaciones cómodas con los submódulos Git y que prefieren no administrar un proceso de combinación externo.

Por ejemplo, supongamos que hay tres repositorios. Cada repositorio contiene una sola rama denominada `main`. En el repositorio principal, es decir, el configurado en las canalizaciones, la rama `main` tiene un archivo `pom.xml` que declara los proyectos contenidos en los otros dos repositorios:

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

Luego debe agregar submódulos para los otros dos repositorios:

```shell
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

El resultado es un archivo `.gitmodules` similar al siguiente:

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

Consulte también el [Manual de referencia de Git](https://git-scm.com/book/en/v2/Git-Tools-Submodules) para obtener más información sobre los submódulos Git.

## Notas de uso de los repositorios de Adobe {#usage-notes-recommendations-adobe-repos}

* La dirección URL de Git debe ser exacta como la sintaxis descrita en la sección anterior.
* Solo se admiten submódulos en la raíz de la rama.
* Por motivos de seguridad, no incruste credenciales en las direcciones URL de Git.
* A menos que sea necesario, Adobe recomienda utilizar submódulos superficiales ejecutando lo siguiente:
  `git config -f .gitmodules submodule.<submodule path>.shallow true` para cada submódulo.
* Las referencias del submódulo Git se almacenan en confirmaciones de Git específicas. Como resultado, cuando se realizan cambios en el repositorio de submódulos, se debe actualizar la confirmación a la que se hace referencia.
Por ejemplo, mediante el uso de lo siguiente:

  `git submodule update --remote`

## Compatibilidad con los submódulos de Git para repositorios privados {#private-repositories}

La compatibilidad con los submódulos Git en [repositorios privados](private-repositories.md) suele ser similar a su uso con repositorios de Adobe.

Sin embargo, después de configurar el archivo `pom.xml` y ejecutar los comandos `git submodule`, debe agregar un archivo `.gitmodules` al directorio raíz del repositorio del agregador para que Cloud Manager reconozca la configuración del submódulo.

![Archivo .gitmodules](assets/gitmodules.png)

![Agregador](assets/aggregator.png)

### Notas de uso {#usage-notes-recommendations-private-repos}

* Las direcciones URL de Git del submódulo pueden estar en formato HTTPS o SSH, pero deben apuntar a un repositorio GitHub.com. No se admite agregar un submódulo de repositorio de Adobe a un repositorio de agregador de GitHub o al revés.
* La aplicación de Adobe GitHub debe poder acceder a los submódulos de GitHub.
* [Las limitaciones de uso de submódulos de Git con repositorios administrados por Adobe](#usage-notes-recommendations-adobe-repos) también se aplican.
