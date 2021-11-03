---
title: Edición de una canalización de producción
description: Edición de una canalización de producción
index: false
source-git-commit: b9d28088ad18a389108ebfb81aa750c63e637922
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# Edición de una canalización de producción {#edit-prod-pipeline}

Puede editar las configuraciones de canalización desde el **Información general del programa** página.

Siga los pasos a continuación para editar la canalización configurada:

1. Vaya a **Canalizaciones** de la **Información general del programa** página.

1. Haga clic en **...** de la variable **Canalizaciones** y haga clic en **Editar**, como se muestra en la figura siguiente.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit1.png)

1. La variable **Editar canalización de producción** se abre.

   1. La variable **Configuración** le permite actualizar el **Nombre de canalización**, **Déclencheur de implementación** y **Comportamiento de error de métricas importantes**.

      >[!NOTE]
      >Consulte [Adición y administración de repositorios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para aprender a añadir y administrar repositorios en Cloud Manager.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit2.png)


   1. La variable **Fuente** proporciona una opción para marcar o desmarcar **Pausar antes de implementar en producción** y **Programado** opciones de **Opciones de implementación de producción**.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-editnotier.png)

   1. La variable **Auditoría de experiencias** permite actualizar o agregar páginas nuevas.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit4.png)

1. Haga clic en **Actualizar** una vez que haya terminado de editar la canalización.

## Acciones adicionales de canalización de producción {#additional-prod-actions}

### Ejecución de una canalización de producción {#run-prod}

Puede ejecutar la canalización de producción desde la tarjeta Canalizaciones:

1. Vaya a **Canalizaciones** de la **Información general del programa** página.

1. Haga clic en **...** de la variable **Canalizaciones** y haga clic en **Ejecutar**, como se muestra en la figura siguiente.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-run.png)

### Eliminación de una canalización de producción {#delete-prod}

Puede eliminar la canalización de producción de la tarjeta Canalizaciones:

1. Vaya a **Canalizaciones** de la **Información general del programa** página.

1. Haga clic en **...** de la variable **Canalizaciones** y haga clic en **Eliminar**, como se muestra en la figura siguiente.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-delete.png)

   >[!NOTE]
   >Un usuario con la función de administrador de implementación ahora puede eliminar la canalización de producción con un método de autoservicio a través del **Eliminar** de la tarjeta Canalización.