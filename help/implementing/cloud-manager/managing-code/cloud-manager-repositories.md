---
title: Repositorios de Cloud Manager
description: Obtenga información sobre cómo crear, ver y eliminar repositorios de Git en Cloud Manager.
exl-id: 6e1cf636-78f5-4270-9a21-38b4d5e5a0b0
source-git-commit: cc6565121a76f70b958aa9050485e0553371f3a3
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 100%

---


# Repositorios de Cloud Manager {#cloud-manager-repos}

Obtenga información sobre cómo crear, ver y eliminar repositorios de Git en Cloud Manager.

>[!NOTE]
>
>Hay un límite de 300 repositorios en todos los programas de cualquier empresa u organización de IMS.

## Adición y administración de repositorios {#add-manage-repos}

Siga estos pasos para ver y administrar repositorios en Cloud Manager.

1. En la página **Información general del programa** página, haga clic en **Repositorios** y vaya a la página **Repositorios**.

1. Haga clic en **Agregar repositorio** para iniciar el asistente.

   ![Botón Agregar repositorio](/help/implementing/cloud-manager/assets/repos/create-repo2.png)

1. Introduzca el nombre y la descripción como se solicita y haga clic en **Guardar**.

   ![Cuadro de diálogo Agregar repositorio](/help/implementing/cloud-manager/assets/repos/repo-1.png)

Cuando se cierre el asistente, el nuevo repositorio se mostrará en la tabla.

Puede seleccionar el repositorio en la tabla, hacer clic en el botón de puntos suspensivos y seleccionar **Copiar URL del repositorio**, **Ver y actualizar** o **Eliminar**.

![Opciones del repositorio](/help/implementing/cloud-manager/assets/repos/create-repo3.png)

Los repositorios creados en Cloud Manager también estarán disponibles para su selección al añadir o editar canalizaciones. Consulte el documento [Canalizaciones CI-CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) para obtener más información.

Hay un único repositorio principal o una rama para una canalización determinada. Con [compatibilidad con el submódulo git](#git-submodule-support), se pueden incluir muchas ramas secundarias en el momento de la compilación.

>[!NOTE]
>
>Un usuario debe tener la función **Administrador de implementación** o **Propietario empresarial** para poder añadir un repositorio.

## Eliminación de un repositorio {#delete-repo}

Al eliminar un repositorio:

* Se impide que el nombre del repositorio eliminado se pueda utilizar para nuevos repositorios que se puedan crear en el futuro.
   * El mensaje de error `Repository name should be unique within organization.` aparecerá en estos casos.
* Se hace que el repositorio eliminado no esté disponible en Cloud Manager y no esté disponible para vincularlo a una canalización.

Siga estos pasos para eliminar un repositorio en Cloud Manager.

1. En la página **Información general del programa** página, haga clic en **Repositorios** y vaya a la página **Repositorios**.

1. Seleccione el repositorio y haga clic en el botón de tres puntos y seleccione **Eliminar** para eliminar el repositorio.

   ![Eliminar repositorio](/help/implementing/cloud-manager/assets/repos/delete-repo.png)

## Compatibilidad con el submódulo Git {#git-submodule-support}

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

Cuando utilice submódulos Git, tenga en cuenta las siguientes limitaciones.

* La dirección URL de Git debe estar exactamente en la sintaxis descrita en la sección anterior.
* Solo se admiten submódulos en la raíz de la rama.
* Por motivos de seguridad, no incruste credenciales en las direcciones URL de Git.
* A menos que sea necesario, se recomienda encarecidamente utilizar submódulos superficiales.
   * Para ello, ejecute `git config -f .gitmodules submodule.<submodule path>.shallow true` para cada submódulo.
* Las referencias del submódulo Git se almacenan en confirmaciones de Git específicas. Como resultado, cuando se realizan cambios en el repositorio de submódulos, es necesario actualizar la confirmación a la que se hace referencia.
   * Por ejemplo, utilizando `git submodule update --remote`
