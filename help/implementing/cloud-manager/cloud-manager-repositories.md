---
title: Repositorios de Cloud Manager
description: Repositorios de Cloud Manager
exl-id: Cloud Manager Repositories
source-git-commit: cebc603aab9c558239588f574f52568d05081b34
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# Repositorios de Cloud Manager {#cloud-manager-repos}

Los repositorios creados y disponibles en Cloud Manager se pueden ver y administrar a través de la página Repositorios .

>[!NOTE]
>Hay un límite de 300 repositorios en todos los programas de una empresa determinada o [Identity Management System del Adobe](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/ims.html)).

## Adición y administración de repositorios {#add-manage-repos}

Siga los pasos a continuación para ver y administrar repositorios en Cloud Manager:

1. En la página **Program Overview** , haga clic en la pestaña **Repositorios** y vaya a la página **Repositorios**.

1. Haga clic en **Agregar repositorio** para iniciar el asistente.

   >[!NOTE]
   >Un usuario con la función de administrador de implementación o propietario empresarial debe iniciar sesión para poder agregar un repositorio.

   ![](assets/repos/create-repo2.png)


1. Introduzca el nombre y la descripción como se solicita y haga clic en **Save**.

   ![](assets/repos/repo-1.png)

1. Seleccione **Guardar**. El repositorio recién creado se mostrará en la tabla, como se muestra a continuación.

   >[!NOTE]
   >Hay un único repositorio *primary* o una rama para cualquier canalización dada. Con [Compatibilidad con submódulos Git](#git-submodule-support), sin embargo, muchas ramas secundarias se pueden incluir en el momento de la compilación.

   ![](assets/repos/create-repo3.png)

   >[!NOTE]
   >Los repositorios creados en Cloud Manager también estarán disponibles para su selección durante los pasos de adición o edición de canalización. Consulte [Configurar la canalización de CI-CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en) para obtener más información.

1. Puede seleccionar el repositorio y hacer clic en las opciones de menú desde el extremo derecho de la tabla a **Copiar URL del repositorio**, **Ver y actualizar** o **Eliminar** su repositorio, como se muestra en la figura siguiente.

   ![](assets/repos/create-repo3.png)


## Compatibilidad con el submódulo Git {#git-submodule-support}

Los submódulos Git se pueden usar para combinar el contenido de varias ramas en repositorios Git en el momento de la compilación. Cuando se ejecuta el proceso de compilación de Cloud Manager, después de clonar el repositorio configurado para la canalización y de desproteger la rama configurada, si la rama contiene un archivo `.gitmodules` en el directorio raíz, se ejecuta el comando.

```
$ git submodule update --init
```

Esto comprobará cada submódulo en el directorio apropiado. Esta técnica es una alternativa potencial a https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/working-with-multiple-source-git-repositories.html para organizaciones que se sienten cómodas con el uso de submódulos Git y no desean administrar un proceso de combinación externo.

Por ejemplo, supongamos que hay tres repositorios, cada uno de los cuales contiene una sola rama denominada main . En el repositorio &quot;principal&quot;, es decir, el configurado en las canalizaciones, la rama principal tiene un archivo pom.xml que declara los proyectos contenidos en los otros dos repositorios:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
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

Luego agregaría submódulos para los otros dos repositorios:

```
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

Esto da como resultado un archivo `.gitmodules` que tiene este aspecto:

```
[submodule "project-a"]
    path = project-a
    url = https://git.cloudmanager.adobe.com/ProgramName/projectA/
    branch = main
[submodule "project-b"]
    path = project-b
    url = https://git.cloudmanager.adobe.com/ProgramName/projectB/
    branch = main
```

Puede encontrar más información sobre los submódulos Git en el [Manual de referencia de Git](https://git-scm.com/book/en/v2/Git-Tools-Submodules).

Cuando utilice submódulos Git, tenga en cuenta lo siguiente:

* La URL de Git debe estar exactamente en la sintaxis descrita anteriormente. Por motivos de seguridad, no incruste credenciales en estas direcciones URL.
* Solo se admiten submódulos en la raíz de la rama.
* Las referencias de los submódulos Git se almacenan en confirmaciones de Git específicas. Como resultado, cuando se realizan cambios en el repositorio de submódulos, es necesario actualizar la confirmación a la que se hace referencia, por ejemplo, utilizando `git submodule update --remote` .

