---
title: Variables de canalización en Cloud Manager
description: Descubra cómo puede utilizar variables de canalización en Cloud Manager para administrar variables de configuración específicas para su compilación.
exl-id: cfcef2e2-0590-457d-a0f9-6092a6d9e0e8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: fb180685152a00d520530d21a44337381febba7f
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 14%

---

# Variables de canalización en Cloud Manager {#configuring-pipeline-variables}

El proceso de compilación puede depender de variables de configuración específicas que no deben almacenarse en el repositorio de Git. O bien, es posible que tenga que ajustarlas entre ejecuciones de canalización en la misma rama. Cloud Manager permite administrar estas configuraciones como variables de canalización.

## Acerca de las variables de canalización {#pipeline-variables}

Con Cloud Manager puede configurar variables de canalización de varias formas diferentes.

* [Uso de la interfaz de usuario de Cloud Manager](#ui)
* [Uso de la CLI de Cloud Manager](#cli)
* [Usando la API de Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Variables/operation/getPipelineVariables)

Las variables pueden almacenarse como texto sin formato o cifrarse en reposo. En cualquier caso, las variables están disponibles en el entorno de compilación como una variable de entorno a la que se puede hacer referencia desde dentro del archivo `pom.xml` u otros scripts de compilación.

## Adición de una variable de canalización a través de Cloud Manager {#ui}

Las variables de canalización se pueden configurar y administrar a través de la interfaz de usuario de Cloud Manager. Ayudan a optimizar la administración de la canalización, especialmente cuando se requieren distintas configuraciones en diferentes pasos.

Debe tener permisos para editar la canalización y agregar, editar y eliminar variables de canalización.

Si se está ejecutando una canalización, la administración de variables está bloqueada.

**Para agregar una variable de canalización mediante Cloud Manager:**

1. Cuando [administre sus canalizaciones](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md), haga clic en ![Puntos suspensivos - Icono de más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) de la canalización para la cual desea crear variables de canalización.

1. En el menú desplegable, haga clic en **Ver/Editar variables**.

   ![Ver/Editar variables de canalización](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. En el cuadro de diálogo **Configuración de variables**, escriba los detalles en la primera fila de la tabla.

   | Campo | Descripción |
   | --- | --- |
   | Nombre | Un nombre único de la variable de configuración. Identifica la variable específica que se utiliza en la canalización. Debe cumplir las siguientes convenciones de nomenclatura:<ul><li>Las variables solo pueden contener caracteres alfanuméricos y el guion bajo (`_`).</li><li>Los nombres deben estar en mayúsculas.</li><li>Hay un límite de 200 variables por canalización.</li><li>Cada nombre debe tener 100 caracteres o menos.</li><li>Cada `string` debe tener menos de 2048 caracteres.</li><li>Cada valor de la variable de tipo `secretString` debe tener 500 caracteres o menos.</li></ul> |
   | Valor | El valor que contiene la variable. |
   | Paso aplicado | Obligatorio. El paso en la canalización al que se aplica la variable:<ul><li>**Compilación**: la variable se aplica durante el proceso de compilación.</li><li>**Prueba funcional**: la variable se usa durante el paso de prueba funcional.</li><li>**Pruebas de IU** - La variable se usa durante la fase de pruebas de IU.</li><li>**Implementar**: La variable se usa durante el paso de implementación. Por ejemplo, utilice esta variable para canalizaciones de Edge Delivery Services.</li></ul> |
   | Tipo | Seleccione si la variable es texto sin formato o cifrada como secreto. |

   ![Agregar variable](/help/implementing/cloud-manager/assets/pipeline-variables-add-variable.png)

1. Haga clic en **Agregar**.

   Añada variables adicionales según sea necesario.

1. Haga clic en **Guardar**.

## Editar una variable de canalización {#edit-ui}

1. Al [administrar sus canalizaciones](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md), haga clic en ![Puntos suspensivos - Icono de más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) de la canalización para la cual desea editar las variables de canalización.

1. En el menú desplegable, haga clic en **Ver/Editar variables**.

   ![Ver/Editar variables de canalización](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. En el cuadro de diálogo **Configuración de variables**, haga clic en ![Puntos suspensivos - Icono de más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) de la variable que desea cambiar.

1. En el menú desplegable, haga clic en **Editar**.

   ![Editar variable](/help/implementing/cloud-manager/assets/pipeline-variables-edit.png)

1. Actualice el valor de la variable según sea necesario.

   Solo se puede cambiar el valor de la variable.

1. Realice una de las siguientes acciones:

   * Haga clic en ![Aplicar - Icono de marca de verificación](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg) para aplicar el cambio.
   * Haga clic en ![Deshacer icono](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Undo_18_N.svg) para revertir el cambio.

1. Haga clic en **Guardar**.


## Eliminar una variable de canalización {#delete-ui}

1. Al [administrar sus canalizaciones](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md), haga clic en ![Puntos suspensivos - Icono de más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) de la canalización para la cual desea eliminar variables de canalización.

1. En el menú desplegable, haga clic en **Ver/Editar variables**.

   ![Ver/Editar variables de canalización](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. En el cuadro de diálogo **Configuración de variables**, haga clic en ![Puntos suspensivos - Icono de más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) de la variable que desea quitar y, a continuación, haga clic en **Eliminar**.

## Establecer variables de canalización mediante la CLI de Cloud Manager {#cli}

Este comando de la CLI (interfaz de línea de comandos) establece una variable.

```shell
$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test
```

Este comando enumera las variables.

```shell
$ aio cloudmanager:list-pipeline-variables PIPELINEID
```

Cuando se utiliza en un archivo de Maven `pom.xml`, suele ser útil vincular estas variables a las propiedades de Maven mediante una sintaxis similar al siguiente ejemplo:

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
