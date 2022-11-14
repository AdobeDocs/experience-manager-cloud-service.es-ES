---
title: Usar varios repositorios
description: Obtenga información sobre cómo administrar varios repositorios de Git al trabajar con Cloud Manager.
exl-id: 1b9cca36-c2d7-4f9e-9733-3f1f4f8b2c7a
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: ht
source-wordcount: '757'
ht-degree: 100%

---

# Usar varios repositorios {#working-with-multiple-source-git-repos}

Obtenga información sobre cómo administrar varios repositorios de Git al trabajar con Cloud Manager.

## Sincronización de repositorios de Git administrados por el cliente {#syncing-customer-managed-git-repositories}

En lugar de trabajar directamente con el repositorio de Git de Cloud Manager, [los clientes pueden trabajar con su propio repositorio de Git](integrating-with-git.md) o varios repositorios de Git propios. En estos casos, se debe configurar un proceso de sincronización automatizado para garantizar que el repositorio de Git de Cloud Manager siempre se mantenga actualizado.

Dependiendo de dónde esté alojado el repositorio de Git del cliente, se podría utilizar una acción de GitHub o una solución de integración continua como Jenkins para configurar la automatización. Con la automatización configurada, cada inserción en un repositorio de Git propiedad del cliente se puede reenviar automáticamente al repositorio de Git de Cloud Manager.

Aunque esta automatización para un único repositorio de Git propiedad del cliente es sencilla, la configuración de este repositorio para varios repositorios requiere una configuración inicial. El contenido de varios repositorios de Git debe asignarse a distintos directorios dentro del repositorio de Git de Cloud Manager único.  El repositorio de Git de Cloud Manager debe aprovisionarse con una raíz de Maven `pom.xml`, que enumere los diferentes proyectos secundarios en la sección de módulos.

El siguiente es un ejemplo `pom.xml` para dos repositorios de Git propiedad del cliente.

* El primer proyecto se colocará en el directorio llamado `project-a`.
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

Tal raíz `pom.xml` se inserta en una rama del repositorio de Git de Cloud Manager. A continuación, es necesario configurar ambos proyectos para que reenvíen automáticamente los cambios al repositorio de Git de Cloud Manager.

Una posible solución sería la siguiente:

1. Una acción de GitHub se puede activar si se inserta una rama en el proyecto A.
1. La acción retirará el proyecto A y el repositorio de Git de Cloud Manager y copiará todo el contenido del proyecto A en el directorio `project-a` en el repositorio de Git de Cloud Manager.
1. Entonces la acción se comprometerá a insertar el cambio.

Por ejemplo, un cambio en la rama principal del proyecto A se inserta automáticamente en la rama principal del repositorio de Git de Cloud Manager. Por supuesto, podría haber una asignación entre ramas, como una inserción a una rama llamada `dev` en el proyecto A se inserta una rama denominada `development` en el repositorio de Git de Cloud Manager. Se requieren pasos similares para el proyecto B.

Según la estrategia de ramificación y los flujos de trabajo, la sincronización se puede configurar para diferentes ramas. Si el repositorio de Git utilizado no proporciona un concepto similar a las acciones de GitHub, también es posible una integración a través de Jenkins (o similar). En este caso, un enlace web activa un trabajo Jenkins que hace el trabajo.

Siga estos pasos para agregar un tercer origen o repositorio nuevo.

1. Agregue una acción de GitHub nueva al repositorio nuevo que inserte cambios de ese repositorio en el repositorio de Git de Cloud Manager.
1. Realice esa acción al menos una vez para asegurarse de que el código del proyecto está en el repositorio de Git de Cloud Manager.
1. Agregue una referencia al nuevo directorio en la raíz de Maven `pom.xml` en el repositorio de Git de Cloud Manager.

## Ejemplo de acción de GitHub {#sample-github-action}

Esta es una acción de ejemplo de GitHub activada por una inserción a la rama principal y luego insertada en un subdirectorio del repositorio de Git de Cloud Manager. Las acciones de GitHub deben tener dos secretos, `MAIN_USER` y `MAIN_PASSWORD`, para poder conectarse e insertarse en el repositorio de Git de Cloud Manager.

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
          git clone -b ${MAIN_BRANCH} ${MAIN_REPOSITORY}.git main 
      # Move sub project
      - name: Move project to main project
        run: |
          rm -rf main/${PROJECT_DIR} 
          mv sub main/${PROJECT_DIR}
      - name: Commit Changes
        run: |
          git -C main add -f ${PROJECT_DIR}
          git -C main commit -F ../commit.txt
          git -C main push
```

El uso de una acción de GitHub es muy flexible. Se puede realizar cualquier asignación entre ramas de los repositorios de Git, así como cualquier asignación de los proyectos de Git independientes al diseño de directorio del proyecto principal.

>[!NOTE]
>
>El script de ejemplo utiliza `git add` para actualizar el repositorio. Esto supone que se incluyen las eliminaciones. Según la configuración predeterminada de Git, es posible que deba reemplazarse por `git add --all`.

## Ejemplo de trabajo de Jenkins {#sample-jenkins-job}

Este es un script de ejemplo que se puede utilizar en un trabajo de Jenkins o similar y que tiene el siguiente flujo:

1. Se activa mediante un cambio en un repositorio de Git.
1. El trabajo de Jenkins comprueba el estado más reciente de ese proyecto o rama.
1. A continuación, el trabajo activa ese script.
1. A su vez, este script extrae el repositorio de Git de Cloud Manager y confirma el código del proyecto en un subdirectorio.

El trabajo de Jenkins debe tener dos secretos, `MAIN_USER` y `MAIN_PASSWORD`, para poder conectarse e insertarse en el repositorio de Git de Cloud Manager.

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

Usar un trabajo de Jenkins es algo muy flexible. Se puede realizar cualquier asignación entre ramas de los repositorios de Git, así como cualquier asignación de los proyectos de Git independientes al diseño de directorio del proyecto principal.

>[!NOTE]
>
>El script de ejemplo utiliza `git add` para actualizar el repositorio. Esto supone que se incluyen las eliminaciones. Según la configuración predeterminada de Git, es posible que deba reemplazarse por `git add --all`.
