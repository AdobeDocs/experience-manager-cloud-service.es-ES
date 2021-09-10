---
title: Uso de repositorios Git de varias fuentes
description: 'Uso de repositorios Git de varias fuentes: Cloud Services'
exl-id: 1b9cca36-c2d7-4f9e-9733-3f1f4f8b2c7a
source-git-commit: 21669a29fbfd1072b637f407f5220825c4d1edbb
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 0%

---

# Uso de repositorios Git de varias fuentes {#working-with-multiple-source-git-repos}


## Sincronización de repositorios Git administrados por el cliente {#syncing-customer-managed-git-repositories}

En lugar de trabajar directamente con el repositorio Git de Cloud Manager, los clientes pueden trabajar con su propio repositorio Git o con varios repositorios Git propios. En estos casos, se debe configurar un proceso de sincronización automatizada para garantizar que el repositorio Git de Cloud Manager siempre se mantenga actualizado. Dependiendo de dónde esté alojado el repositorio Git del cliente, se podría utilizar una acción de GitHub o una solución de integración continua como Jenkins para configurar la automatización. Con la automatización implementada, cada inserción en un repositorio Git propiedad del cliente se puede reenviar automáticamente al repositorio Git de Cloud Manager.

Aunque esta automatización para un único repositorio Git propiedad del cliente es directa, la configuración de varios repositorios requiere una configuración inicial. El contenido de los distintos repositorios Git debe asignarse a distintos directorios dentro del repositorio Git de Cloud Manager.  El repositorio Git de Cloud Manager debe aprovisionarse con un pom raíz de Maven, que enumera los diferentes subproyectos en la sección de módulos

A continuación se muestra un ejemplo de pom para dos repositorios Git de propiedad del cliente: el primer proyecto se colocará en el directorio llamado `project-a`, el segundo proyecto se colocará en el directorio llamado `project-b`.

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

Este tipo de pom raíz se inserta en una rama del repositorio Git de Cloud Manager. A continuación, es necesario configurar los dos proyectos para que reenvíen automáticamente los cambios al repositorio Git de Cloud Manager.

Por ejemplo, una acción de GitHub se puede activar presionando a una rama del proyecto A. La acción retirará el proyecto A y el repositorio Git de Cloud Manager y copiará todo el contenido del proyecto A al directorio `project-a` del repositorio Git de Cloud Manager y, a continuación, aprobará e impulsará el cambio. Por ejemplo, un cambio en la rama principal del proyecto A se inserta automáticamente en la rama principal del repositorio Git de Cloud Manager. Por supuesto, podría haber una asignación entre ramas como una inserción en una rama denominada &quot;dev&quot; en el proyecto A se inserta en una rama denominada &quot;development&quot; en el repositorio Git de Cloud Manager. Se requieren pasos similares para el proyecto B.

Según la estrategia de ramificación y los flujos de trabajo, la sincronización se puede configurar para diferentes ramas. Si el repositorio Git utilizado no proporciona un concepto similar a las acciones de GitHub, también es posible una integración a través de Jenkins (o similar). En este caso, un enlace web déclencheur un trabajo de Jenkins que hace el trabajo.

Siga los pasos a continuación para agregar un nuevo (tercer) origen o repositorio:

1. Agregue una nueva acción de GitHub al nuevo repositorio que inserta cambios de ese repositorio al repositorio Git de Cloud Manager.
1. Realice esa acción al menos una vez para asegurarse de que el código de proyecto está en el repositorio Git de Cloud Manager.
1. Agregue una referencia al nuevo directorio en el pom raíz Maven del repositorio Git de Cloud Manager.


## Ejemplo de acción de GitHub {#sample-github-action}

Esta es una acción de GitHub de muestra desencadenada por una notificación push a la rama principal y luego insertada en un subdirectorio del repositorio Git de Cloud Manager. Las acciones de GitHub deben tener dos secretos, `MAIN_USER` y `MAIN_PASSWORD`, para poder conectarse y enviarse al repositorio Git de Cloud Manager.

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
          git clone -b ${MAIN_BRANCH} https://${{ secrets.PAT }}@github.com/${MAIN_REPOSITORY}.git main 
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

Como se muestra arriba, el uso de una acción de GitHub es muy flexible. Se puede realizar cualquier asignación entre ramas de los repositorios Git, así como cualquier asignación de los proyectos Git independientes en el diseño de directorio del proyecto principal.

>[!NOTE]
>La secuencia de comandos anterior utiliza `git add` para actualizar el repositorio que supone que se incluyen las eliminaciones: según la configuración predeterminada de Git, esto debe reemplazarse por `git add --all`.

## Ejemplo de trabajo de Jenkins {#sample-jenkins-job}

Este es un script de ejemplo que puede utilizarse en un trabajo de Jenkins o similar. Se activa mediante un cambio en un repositorio Git. El trabajo de Jenkins comprueba el estado más reciente de ese proyecto o rama y luego déclencheur este script.

A su vez, esta secuencia de comandos extrae el repositorio Git de Cloud Manager y confirma el código del proyecto en un subdirectorio.

El trabajo de Jenkins debe proporcionarse con dos secretos, `MAIN_USER` y `MAIN_PASSWORD`, para poder conectarse y enviarse al repositorio Git de Cloud Manager.

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

Como se ha mostrado anteriormente, el uso de un trabajo de Jenkins es muy flexible. Se puede realizar cualquier asignación entre ramas de los repositorios Git, así como cualquier asignación de los proyectos Git independientes en el diseño de directorio del proyecto principal.

>[!NOTE]
>La secuencia de comandos anterior utiliza `git add` para actualizar el repositorio que supone que se incluyen las eliminaciones: según la configuración predeterminada de Git, esto debe reemplazarse por `git add --all`.
