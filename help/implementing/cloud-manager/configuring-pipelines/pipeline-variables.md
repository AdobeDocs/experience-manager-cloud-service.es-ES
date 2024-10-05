---
title: Configuración de variables de canalización
description: Descubra cómo puede utilizar variables de canalización en Cloud Manager para administrar variables de configuración específicas para su compilación.
exl-id: cfcef2e2-0590-457d-a0f9-6092a6d9e0e8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 500e1b78fb9688601848fc17f312fc23be83bcb0
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 20%

---

# Configuración de variables de canalización {#configuring-pipeline-variables}

El proceso de compilación puede depender de variables de configuración específicas que no deberían colocarse en el repositorio de Git o puede que necesite variarlas entre ejecuciones de canalización que usen la misma rama. Cloud Manager le permite administrar estos datos como variables de canalización.

## Variables de canalización {#pipeline-variables}

Con Cloud Manager puede configurar variables de canalización de varias formas diferentes.

* [Mediante la IU de Cloud Manager](#ui)
* [Uso de la CLI de Cloud Manager](#cli)
* [Usando la API de Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Variables/operation/getPipelineVariables)

Las variables pueden almacenarse como texto sin formato o cifrarse en reposo. En cualquier caso, las variables están disponibles dentro del entorno de compilación como una variable de entorno a la que se puede hacer referencia desde dentro del archivo `pom.xml` u otras secuencias de comandos de compilación.

### Convenciones de nomenclatura de variables de canalización {#naming-conventions}

Los nombres de las variables deben cumplir las siguientes convenciones.

* Las variables solo pueden contener caracteres alfanuméricos y el guion bajo (`_`).
* Los nombres deben estar en mayúsculas.
* Hay un límite de 200 variables por canalización.
* Cada nombre debe tener 100 caracteres o menos.
* Cada `string` debe tener menos de 2048 caracteres.
* Cada valor de la variable de tipo `secretString` debe tener 500 caracteres o menos.

## Mediante la IU de Cloud Manager {#ui}

Las variables de canalización se pueden configurar y administrar a través de la interfaz de usuario de Cloud Manager. Debe tener permisos para editar la canalización a fin de agregar, editar y eliminar variables de canalización.

Si se está ejecutando una canalización, la administración de variables está bloqueada.

### Agregar variables de canalización {#add-ui}

1. Al [administrar sus canalizaciones,](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) pulse o haga clic en el botón de los tres puntos de la canalización para la que desea crear variables de canalización y seleccione **Ver/editar variables** del menú contextual.

   ![Ver/editar variables de canalización](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. Se abre la ventana **Configuración de variables**. Escriba los detalles de la variable en la primera fila de la tabla y toque o haga clic en **Agregar**.

   * **Nombre de configuración** es un identificador único para su variable, que debe encabezar [convenciones de nomenclatura de variables de canalización](#naming-conventions).
   * **Valor** es el valor que contiene la variable.
   * **Paso aplicado** es el paso en la canalización al que se aplica la variable. Es obligatorio.
      * **Compilación**
      * **Pruebas funcionales**
      * **Pruebas de IU**
   * **Type** define si la variable es texto sin formato o está cifrada como un secreto.

   ![Agregar variable](/help/implementing/cloud-manager/assets/pipeline-variables-add-variable.png)

1. El se añade a la tabla. Agregue variables adicionales según sea necesario y, a continuación, toque o haga clic en **Guardar** para guardar las variables que agregó a la canalización.

### Edición de variables de canalización {#edit-ui}

1. Al [administrar sus canalizaciones,](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) pulse o haga clic en el botón de los tres puntos de la canalización para la que desea crear variables de canalización y seleccione **Ver/editar variables** del menú contextual.

   ![Ver/editar variables de canalización](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. Se abre la ventana **Configuración de variables**. Pulse o haga clic en el botón de los tres puntos de la variable que desee editar y seleccione **Editar**.

   ![Editar variable](/help/implementing/cloud-manager/assets/pipeline-variables-edit.png)

1. Actualice el valor de la variable según sea necesario y toque o haga clic en **Aplicar** (la marca de verificación al final de la fila) para aplicar el cambio o en **Descartar** (la flecha hacia atrás) para revertir el cambio.

   * Solo se puede editar el valor de la variable.

   ![Editando una variable](/help/implementing/cloud-manager/assets/pipeline-variables-edit-save.png)

1. Toque o haga clic en **Guardar** para guardar los cambios que hizo en las variables en la canalización.

Si desea eliminar una variable, seleccione **Eliminar** en lugar de **Editar** del menú de los tres puntos de la variable de canalización en la ventana **Configuración de variables**.

## Uso de la CLI de Cloud Manager {#cli}

Este comando de CLI configura una variable.

```shell
$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test
```

Este comando enumera las variables.

```shell
$ aio cloudmanager:list-pipeline-variables PIPELINEID
```

Cuando se utiliza dentro de un archivo `pom.xml` de Maven, normalmente resulta útil asignar estas variables a las propiedades de Maven mediante una sintaxis similar a esta.

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                <property>
                    <name>env.CM_BUILD</name>
                </property>
            </activation>
            <properties>
                <my.custom.property>${env.MY_CUSTOM_VARIABLE}</my.custom.property> 
            </properties>
        </profile>
```
