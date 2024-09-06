---
title: Canalizaciones de solo fase y de producción
description: Descubra cómo puede dividir las implementaciones de fase y producción mediante canalizaciones dedicadas.
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 88%

---


# Canalizaciones de solo fase y de producción {#stage-prod-only}

Descubra cómo puede dividir las implementaciones de fase y producción mediante canalizaciones dedicadas.

>[!NOTE]
>
>Esta funcionalidad solo está disponible para [el programa de clientes pioneros](/help/implementing/cloud-manager/release-notes/current.md#early-adoption).

## Información general {#overview}

Los entornos de ensayo y producción están perfectamente asociados. De forma predeterminada, estas implementaciones están vinculadas a una sola canalización. Es una canalización de implementación que se implementa en los entornos de ensayo y producción de ese programa. Aunque este acoplamiento suele ser adecuado, hay ciertos casos de uso en los que existen desventajas:

* Si desea implementar en solo ensayo, únicamente puede hacerlo rechazando el paso **Promocionar para producción** en la canalización. Sin embargo, la ejecución se marcará como cancelada.
* Si desea implementar el código más reciente de un entorno de ensayo en el de producción, debe volver a implementar toda la canalización, incluida la implementación de fase, aunque ahí no se haya cambiado ningún código.
* Dado que los entornos no se pueden actualizar durante las implementaciones, si desea pausar y realizar pruebas en el entorno de fase durante varios días antes de la promoción a producción, el entorno de producción no se puede actualizar. Esto hace que las tareas no dependientes, como la actualización de las [variables de entorno](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#environment-variables), sean imposibles.

Las canalizaciones de solo fase y producción ofrecen soluciones para estos casos de uso al proporcionar opciones de implementación dedicadas.

* Las **canalizaciones de implementación de solo fase** se implementan solo en un entorno de fase, quedando la ejecución finalizada una vez realizadas la implementación y las pruebas.
   * Una canalización de solo fase se comporta de forma idéntica a la canalización de producción de pila completa asociada estándar, pero sin los pasos de implementación de producción (aprobación, programación, implementación).
* Las **canalizaciones de implementación de solo producción** se implementan únicamente en un entorno de producción con la opción de seleccionar una ejecución finalizada y validada correctamente en el escenario e implementar sus artefactos en la producción.
   * Las canalizaciones de solo producción reutilizarán los artefactos de las implementaciones de fase, lo que omitirá la fase de generación.

Ni las canalizaciones de solo fase ni las de solo producción se ejecutarán mientras se esté ejecutando una canalización de producción de pila completa y viceversa. Si tanto la canalización de solo fase como la de producción de pila completa tienen configurado el activador **Cambios en Git** y apuntan a la misma rama y repositorio, solo se inicia automáticamente la canalización de solo fase. No se han iniciado las canalizaciones de solo producción **Cambios en Git**, ya que no están directamente vinculadas a un repositorio.

Estas canalizaciones dedicadas ofrecen más flexibilidad, pero tenga en cuenta los siguientes detalles de funcionamiento y recomendaciones.

## Limitaciones {#limitations}

Las canalizaciones de solo producción siempre utilizarán los artefactos de la canalización de solo fase, independientemente de lo que se haya podido implementar en el escenario a través de la canalización de producción asociada estándar mientras tanto.

* Esto podría provocar reversiones de código no deseadas.
* Adobe recomienda dejar de usar la canalización de producción asociada estándar una vez que comience a utilizar las canalizaciones de solo producción y de solo fase.
* Si todavía decide ejecutar tanto las canalizaciones asociadas estándar como las canalizaciones de solo fase/producción, tenga en cuenta la reutilización de artefactos para evitar reversiones del código.

## Problemas conocidos {#known-issues}

Tenga en cuenta también los siguientes problemas conocidos antes de comenzar a probar esta función.

* AEM Una vez que utilice canalizaciones solo de producción, es posible que no se beneficie de las últimas actualizaciones de la
   * AEM En algunos casos, el proceso de actualización de la puede revertir el código al código que se implementó por última vez mediante la canalización de pila completa.
* No podrá solicitar una [restauración de entorno](/help/operations/restore.md#offsite-backup) si usa canalizaciones solo de producción o de ensayo.

## Creación de canalizaciones {#pipeline-creation}

Las canalizaciones de solo producción y fase se crean de forma similar a las [canalizaciones de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) asociadas estándar y las [canalizaciones que no sean de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md). Consulte estos documentos para obtener más información.

1. En la ventana **Canalizaciones**, haga clic en **Agregar canalización**.

   * Seleccione **Agregar canalización que no sea de producción** para crear una canalización de solo fase.
   * Seleccione **Añadir una canalización de solo producción** para crear una canalización de solo producción.

   ![Creación de una canalización de solo producción/solo fase](assets/prod-stage-pipelines.png)

>[!NOTE]
>
>Algunas opciones pueden aparecer atenuadas si ya existen las canalizaciones correspondientes.
>
>* **Agregar una canalización de solo producción** no estará disponible si una canalización de solo fase no existe aún.
>* **Agregar canalización de producción** no está disponible si ya existe una canalización asociada estándar.
>* Solo se permite una canalización de solo producción y una de solo fase por programa.

### Canalizaciones de solo fase {#stage-only}

1. Una vez seleccionada la opción **Agregar canalización que no sea de producción** se abre el cuadro de diálogo **Agregar canalización que no sea de producción**.
1. Para crear una canalización de solo fase, seleccione el entorno de fase en el campo **Entornos de implementación aptos** para la canalización. Complete los campos restantes y haga clic en **Continuar**.

   ![Creación de una canalización de solo fase](assets/stage-only.png)

1. En la pestaña **Pruebas de ensayos**, puede definir luego las pruebas que deben realizarse en el entorno de ensayo. Toque o haga clic en **Guardar** para guardar la canalización nueva.

### Canalizaciones de solo producción {#prod-only}

1. Al seleccionar la opción **Agregar canalización solo de producción**, se abre el cuadro de diálogo **Agregar canalización solo de producción**.
1. Proporcione un **nombre para la canalización**. Las opciones y funcionalidades restantes del cuadro de diálogo funcionan igual que las del cuadro de diálogo de creación de canalización asociada estándar. Haga clic en **Guardar** para guardar la canalización.

## Ejecución de canalizaciones de solo producción y de solo fase {#running}

Las canalizaciones de solo producción y de solo fase se ejecutan del mismo modo que [se ejecutan todas las demás canalizaciones](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines). Consulte la documentación para obtener más detalles.

Además, la ejecución de una canalización de solo producción se puede activar directamente desde los detalles de ejecución de una canalización de solo fase.

### Canalizaciones de solo fase {#stage-only-run}

Una canalización de solo fase se ejecuta casi del mismo modo que las canalizaciones asociadas estándar. Sin embargo, al final de la ejecución, después de los pasos de pruebas, el botón **Promocionar versión** permite iniciar una ejecución de canalización de solo producción que utilice los artefactos implementados en el escenario por esta ejecución y los implemente en la producción.

![Ejecución de canalización de solo fase](assets/stage-only-pipeline-run.png)

El botón **Promocionar versión** solo aparece si se encuentra en la última ejecución correcta de canalización de solo fase. Al hacer clic en esta opción, se le pedirá que confirme la ejecución de la canalización de solo producción o que cree una canalización de solo producción si aún no existe ninguna.

### Canalizaciones de solo producción {#prod-only-run}

Para las canalizaciones de solo producción es importante identificar los artefactos de origen que se van a implementar en la producción. Estos detalles se encuentran en el paso **Preparación de artefactos**. Puede navegar a esas ejecuciones para obtener más detalles y registros.

![Detalles del artefacto](assets/prod-only-pipeline-run.png)
