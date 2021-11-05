---
title: Edición de una canalización que no es de producción
description: Edición de una canalización que no es de producción
index: true
source-git-commit: 7dc9f9a189927f3522445fac36a1606521f410b2
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# Edición de una canalización que no es de producción {#edit-non-prod-pipeline}

Puede editar las configuraciones de canalización desde el **Tarjeta de canalización** from **Información general del programa** página.

>[!IMPORTANT]
>No se puede editar una canalización que se esté ejecutando.

Siga los pasos a continuación para editar la canalización configurada que no sea de producción:

1. Vaya a **Canalizaciones** de la **Información general del programa** página.

1. Seleccione la canalización que no es de producción y haga clic en **...**. Haga clic en **Editar**, como se muestra en la figura siguiente.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit1.png)

1. La variable **Editar canalización de producción** se abre.

   1. La variable **Configuración** le permite actualizar el **Nombre de canalización**, **Déclencheur de implementación** y **Comportamiento de errores de métricas importantes**.

      >[!NOTE]
      >Consulte [Adición y administración de repositorios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para aprender a añadir y administrar repositorios en Cloud Manager.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit2.png)


   1. La variable **Código fuente** le permite actualizar el **Repositorio** y **Rama de Git**.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit3.png)

1. Haga clic en **Actualizar** una vez que haya terminado de editar la canalización que no es de producción.

## Acciones adicionales de canalización que no son de producción {#additional-nonprod-actions}

### Ejecución de una canalización que no sea de producción {#run-nonprod}

Puede ejecutar la canalización de producción desde la tarjeta Canalizaciones:

1. Vaya a **Canalizaciones** de la **Información general del programa** página.

1. Haga clic en **...** de la variable **Canalizaciones** y haga clic en **Ejecutar**, como se muestra en la figura siguiente.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-run1.png)

### Eliminación de una canalización que no es de producción {#delete-nonprod}

Puede eliminar la canalización de producción de la tarjeta Canalizaciones:

1. Vaya a **Canalizaciones** de la **Información general del programa** página.

1. Haga clic en **...** de la variable **Canalizaciones** y haga clic en **Eliminar**, como se muestra en la figura siguiente.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-delete.png)
