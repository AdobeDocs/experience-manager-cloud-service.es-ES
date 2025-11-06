---
title: Uso de varios repositorios
description: Obtenga información sobre cómo administrar varios repositorios de Git al trabajar con Cloud Manager.
exl-id: 1b9cca36-c2d7-4f9e-9733-3f1f4f8b2c7a
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 31%

---

# Uso de varios repositorios {#working-with-multiple-source-git-repos}

Obtenga información sobre cómo administrar varios repositorios de Git al trabajar con Cloud Manager.

## Sincronización de repositorios Git privados {#syncing-customer-managed-git-repositories}

En lugar de trabajar directamente con el repositorio Git de Cloud Manager, [los clientes pueden trabajar con su propio repositorio Git privado](integrating-with-git.md) o con varios repositorios Git propios. En estos casos, configure un proceso de sincronización automatizado para garantizar que el repositorio de Git en Cloud Manager siempre se mantenga actualizado.

Dependiendo de dónde esté alojado el repositorio de Git del cliente, se podría utilizar una acción de GitHub o una solución de integración continua como Jenkins para configurar la automatización. Con la automatización configurada, cada inserción en un repositorio Git propiedad del cliente se puede reenviar automáticamente al repositorio Git de Cloud Manager.

Aunque esta automatización para un único repositorio de Git propiedad del cliente es sencilla, la configuración para varios repositorios requiere una configuración inicial. El contenido de varios repositorios de Git debe asignarse a distintos directorios dentro del repositorio de Git de Cloud Manager único. El repositorio Git de Cloud Manager debe aprovisionarse con un Maven raíz `pom.xml`, que enumere los diferentes subproyectos en la sección de módulos.

El siguiente es un archivo de muestra `pom.xml` para dos repositorios Git propiedad del cliente.

* El segundo proyecto se coloca en el directorio llamado `project-a`.
* El segundo proyecto se colocará en el directorio llamado `project-b`.

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

Un `pom.xml` raíz como este se inserta en una rama del repositorio de Git de Cloud Manager. A continuación, los dos proyectos deben configurarse para que reenvíen los cambios automáticamente al repositorio de Git de Cloud Manager.

Una posible solución sería la siguiente:

1. Almacene en déclencheur una acción de GitHub insertándola en una rama del proyecto A.
1. La acción extrae el proyecto A y el repositorio Git de Cloud Manager. A continuación, copia todo el contenido del proyecto A en el directorio `project-a` del repositorio Git de Cloud Manager.
1. A continuación, la acción confirma e inserta el cambio.

Por ejemplo, un cambio en la rama principal del proyecto A se inserta automáticamente en la rama principal del repositorio de Git de Cloud Manager. Podría haber una asignación entre ramas, como si una inserción en una rama llamada `dev` del proyecto A se inserta una rama denominada `development` en el repositorio Git de Cloud Manager. Se requieren pasos similares para el proyecto B.

Según la estrategia de ramificación y los flujos de trabajo, la sincronización se puede configurar para diferentes ramas. Si el repositorio de Git utilizado no proporciona un concepto similar a las acciones de GitHub, también es posible una integración a través de Jenkins (o similar). En este caso, un enlace web déclencheur un trabajo de Jenkins, que hace el trabajo.

Siga estos pasos para poder agregar un tercer origen o repositorio nuevo.

1. Agregue una acción de GitHub al nuevo repositorio, que inserta cambios de ese repositorio en el repositorio de Git de Cloud Manager.
1. Realice esa acción al menos una vez para asegurarse de que el código del proyecto esté en el repositorio de Git de Cloud Manager.
1. En el repositorio Git de Cloud Manager, agregue una referencia al nuevo directorio en el Maven raíz `pom.xml`.



## Muestra de acción de GitHub {#sample-github-action}

A continuación se muestra un ejemplo de acción de GitHub activada por una inserción en la rama principal. A continuación, inserte en un subdirectorio del repositorio de Git de Cloud Manager. Las acciones de GitHub deben tener dos secretos, `MAIN_USER` y `MAIN_PASSWORD`, para poder conectarse y enviar al repositorio de Git de Cloud Manager.

```java
name: SYNC
env:
  # Username/email used to commit to Cloud Manager's Git repository
  USER_NAME: <NAME>
  USER_EMAIL: <EMAIL>
  # Directory within the Cloud Manager Git repository
  PROJECT_DIR: project-a
  # Cloud Manager's Git repository
  MAIN_REPOSITORY: https://$MAIN_USER:$MAIN_PASSWORD@git.cloudmanager.adobe.com/<PATH>
  # The branch in Cloud Manager's Git repository to push to
  MAIN_BRANCH : <BRANCH_NAME>
 
# Only run on a push to this branch
on:
  push:
     branches: [ main ]
 
jobs:
  build:
    runs-on: ubuntu-latest
 
    steps:
      # Checkout this project into a sub folder
      - uses: actions/checkout@v2
        with:
          path: sub
      # Cleanup sub project
      - name: Clean project
        run: |
          git -C sub log --format="%an : %s" -n 1 > commit.txt
          rm -rf sub/.git
          rm -rf sub/.github
      # Set global git configuration
      - name: Set git config
        run: |
          git config --global credential.helper cache
          git config --global user.email ${USER_EMAIL}
          git config --global user.name ${USER_NAME}
      # Checkout the main project
      - name: Checkout main project
        run:
          git clone -b ${MAIN_BRANCH} ${MAIN_REPOSITORY} ${MAIN_BRANCH} 
      # Move sub project
      - name: Move project to main project
        run: |
          rm -rf ${MAIN_BRANCH}/${PROJECT_DIR} 
          mv sub ${MAIN_BRANCH}/${PROJECT_DIR}
      - name: Commit Changes
        run: |
          git -C ${MAIN_BRANCH} add -f ${PROJECT_DIR}
          git -C ${MAIN_BRANCH} commit -F ../commit.txt
          git -C ${MAIN_BRANCH} push
```

El uso de una acción de GitHub es flexible. Se puede realizar cualquier asignación entre ramas de los repositorios de Git y cualquier asignación de los proyectos de Git independientes al diseño de directorio del proyecto principal.

>[!NOTE]
>
>El script de ejemplo utiliza `git add` para actualizar el repositorio. La secuencia de comandos supone que se incluyen las eliminaciones. Según la configuración predeterminada de Git, debe reemplazarse por `git add --all`.

## Muestra de trabajo de Jenkins {#sample-jenkins-job}

El siguiente es un script de ejemplo que se puede utilizar en un trabajo de Jenkins o similar y que tiene el siguiente flujo:

1. Se activa mediante un cambio en un repositorio Git.
1. El trabajo de Jenkins comprueba el estado más reciente de ese proyecto o rama.
1. A continuación, el trabajo activa ese script.
1. A su vez, esta extrae el repositorio de Git de Cloud Manager y confirma el código del proyecto en un subdirectorio.

Se debe proporcionar al trabajo de Jenkins dos secretos, `MAIN_USER` y `MAIN_PASSWORD`, para poder conectarse e insertarse en el repositorio Git de Cloud Manager.

```java
# Username/email used to commit to Cloud Manager's Git repository
export USER_NAME=<NAME>
export USER_EMAIL=<EMAIL>
# Directory within the Cloud Manager Git repository
export PROJECT_DIR=project-a
# Cloud Manager's Git repository
export MAIN_REPOSITORY=https://$MAIN_USER:$MAIN_PASSWORD@git.cloudmanager.adobe.com/<PATH>
# The branch in Cloud Manager's Git repository to push to
export MAIN_BRANCH=<BRANCH_NAME>
 
# clean up and init
rm -rf target
mkdir target
 
# mv project to sub folder
mkdir target/sub
for f in .* *
do
    if [ "$f" != "." -a "$f" != ".." -a "$f" != "target" ]
    then
        mv "$f" target/sub
    fi
done
cd target
 
# capture log and remove git info
cd sub
git log --format="%an : %s" -n 1 > ../commit.txt
rm -rf .git
rm -rf .github
cd ..
 
# checkout main repository
git clone -b $MAIN_BRANCH $MAIN_REPOSITORY main
cd main
 
# configure main repository
git config credential.helper cache
git config user.email $USER_EMAIL
git config user.name $USER_NAME
 
# update project in main
rm -rf $PROJECT_DIR
mv ../sub $PROJECT_DIR
 
# commit changes to main
git add -f $PROJECT_DIR
git commit -F ../commit.txt
git push
```

El uso de un trabajo de Jenkins es flexible. Se puede realizar cualquier asignación entre ramas de los repositorios de Git y cualquier asignación de los proyectos de Git independientes al diseño de directorio del proyecto principal.

>[!NOTE]
>
>El script de ejemplo utiliza `git add` para actualizar el repositorio. La secuencia de comandos supone que se incluyen las eliminaciones. Según la configuración predeterminada de Git, debe reemplazarse por `git add --all`.
