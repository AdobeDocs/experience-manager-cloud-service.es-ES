---
title: Dividir canalizaciones solo de fase y solo de producción
description: Descubra cómo puede dividir las implementaciones de fase y producción mediante canalizaciones dedicadas.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
badge: label="Beta" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#staging-production-only-pipelines"
hide: false
hidefromtoc: false
index: true
exl-id: 7d76a87c-122c-4c4d-8071-957bef4c9cf1
source-git-commit: f61183c43d9380900b92fe040098e2eb3155979c
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 48%

---

# Dividir canalizaciones solo de fase y de producción {#stage-prod-only}

Puede dividir las implementaciones de ensayo y producción mediante canalizaciones dedicadas.

## Información general {#overview}

Los entornos de ensayo y producción están perfectamente asociados. De forma predeterminada, estas implementaciones están vinculadas a una sola canalización. Es una canalización de implementación que se implementa en los entornos de ensayo y producción de ese programa. Aunque este acoplamiento suele ser adecuado, hay ciertos casos de uso en los que existen desventajas:

* Si desea implementar en solo ensayo, debe rechazar el paso **Promocionar para producción** en la canalización. Sin embargo, la ejecución se marca como cancelada.
* Si desea implementar el código más reciente de un entorno de ensayo en el de producción, debe volver a implementar toda la canalización, incluida la implementación de fase, aunque ahí no se haya cambiado ningún código.
* Los entornos no se pueden actualizar durante las implementaciones. Si se detiene para probar en el entorno de ensayo durante varios días antes de pasar a producción, el entorno de producción permanece bloqueado y no se puede actualizar. Esto hace que las tareas no dependientes, como la actualización de las [variables de entorno](/help/implementing/cloud-manager/environment-variables.md), sean imposibles.

Las canalizaciones de solo fase y producción ofrecen soluciones para estos casos de uso al proporcionar opciones de implementación dedicadas.

* Las **canalizaciones de implementación de solo fase** se implementan solo en un entorno de fase, quedando la ejecución finalizada una vez realizadas la implementación y las pruebas. Una canalización de solo fase se comporta de forma idéntica a la canalización de producción de pila completa asociada estándar, pero sin los pasos de implementación de producción (aprobación, programación, implementación).
* **Canalizaciones de implementación solo de producto:** se implementa solamente en producción al seleccionar la ejecución de fase exitosa más reciente. A continuación, implemente sus artefactos en producción. Las canalizaciones solo de producción reutilizan artefactos de implementación de fase, omitiendo la fase de compilación.

Las canalizaciones solo de fase y de solo producción no se ejecutan mientras una canalización de producción de pila completa está en curso y viceversa. Si tanto la canalización de solo fase como la de producción de pila completa tienen configurado el activador **Cambios en Git** y apuntan a la misma rama y repositorio, solo se inicia automáticamente la canalización de solo fase. Las canalizaciones de solo producción no inician **`On Git Changes`** porque no están vinculadas directamente a un repositorio.

Las canalizaciones solo de producción se activan manualmente, ya que no están vinculadas directamente a un repositorio para **Cambios en Git**.

Estas canalizaciones dedicadas ofrecen más flexibilidad, pero tenga en cuenta los siguientes detalles de funcionamiento y recomendaciones.

>[!NOTE]
>
>Las canalizaciones solo de producción siempre utilizan artefactos de la canalización solo de fase. Este proceso sigue siendo válido incluso si la canalización de producción acoplada estándar ha implementado algo más para ensayo mientras tanto.
>
>* Este tipo de escenario podría provocar reversiones de código no deseadas.
>* Adobe recomienda dejar de usar la canalización de producción asociada estándar una vez que comience a utilizar las canalizaciones de solo producción y de solo fase.
>* Si todavía decide ejecutar tanto las canalizaciones asociadas estándar como las canalizaciones de solo fase/producción, tenga en cuenta la reutilización de artefactos para evitar reversiones del código.

## Creación de canalizaciones {#pipeline-creation}

Las canalizaciones de solo producción y fase se crean de forma similar a las [canalizaciones de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) asociadas estándar y las [canalizaciones que no sean de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md). Consulte estos documentos para obtener más información.

1. En la ventana **Canalizaciones**, haga clic en **Agregar canalización**.

   * Seleccione **Agregar canalización que no sea de producción** para [crear una canalización solo de etapa](#stage-only).
   * Seleccione **Agregar canalización de solo producción** para [crear una canalización de solo producción](#prod-only).

![Creación de una canalización de solo producción/solo fase](/help/implementing/cloud-manager/configuring-pipelines/assets/prod-stage-pipeline.png)

>[!NOTE]
>
>Algunas opciones pueden aparecer atenuadas si ya existen las canalizaciones correspondientes.
>
>* **Agregar una canalización de solo producción** no estará disponible si una canalización de solo fase no existe aún.
>* **Agregar canalización de producción** no está disponible si ya existe una canalización asociada estándar.
>* Solo se permite una canalización de solo producción y una de solo fase por programa.

### Creación de una canalización solo de fase {#stage-only}

1. En el cuadro de diálogo **Agregar canalización que no sea de producción**, en la ficha **Configuración**, seleccione el campo **Canalización de implementación** para su canalización.
1. En el campo Nombre de la canalización que no es de producción, introduzca un nombre de texto libre.
1. Seleccione las opciones de implementación que desee y haga clic en **Continuar**.

   ![Ficha Configuración en el cuadro de diálogo Agregar canalización que no sea de producción](/help/implementing/cloud-manager/configuring-pipelines/assets/add-non-prod-pipeline-1.png)

1. En la ficha **Código Source**, seleccione **Código de pila completa**. Esta opción crea e implementa toda la aplicación de AEM (back-end, configuración de nivel web/Dispatcher y cualquier módulo front-end del repositorio).

1. En la lista desplegable **Entornos de implementación aptos**, seleccione el entorno de **fase** como entorno de implementación para su canalización. Al seleccionar fase, se crea una canalización dedicada al entorno de ensayo (la promoción de la producción se produce mediante una canalización independiente).

1. Seleccione su **repositorio** y **rama Git** en las listas desplegables respectivas y luego haga clic en **Continuar**.

   ![Ficha Código Source en el cuadro de diálogo Agregar canalización que no sea de producción](/help/implementing/cloud-manager/configuring-pipelines/assets/add-non-prod-pipeline-2.png)

1. En la ficha **Auditoría de experiencias**, la dirección URL del sitio especificada es la dirección URL publicada que Cloud Manager audita para la calidad de la página.

1. En el campo **Ruta de página**, especifique qué páginas desea auditar y luego haga clic en **![Agregar icono](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg) Agregar página**.

   La auditoría de experiencias analiza cada ruta que agrega para obtener rendimiento, accesibilidad, aplicaciones web progresivas, prácticas recomendadas, SEO y otras comprobaciones de calidad. Puede agregar varias rutas y eliminar cualquiera si hace clic en ![Icono de tamaño cruzado 400](https://spectrum.adobe.com/static/icons/ui_18/CrossSize400.svg).

   ![Pestaña Auditoría de experiencias en el cuadro de diálogo Agregar canalización que no sea de producción](/help/implementing/cloud-manager/configuring-pipelines/assets/add-non-prod-pipeline-3.png)

1. Haga clic en **Guardar**.


### Creación de una canalización solo de producción {#prod-only}

1. En el cuadro de diálogo **Agregar canalización solo de producción**, en el campo de texto **Nombre de canalización**, escriba el nombre de texto libre de la canalización.
1. En el campo **Nombre de canalización**, escriba el nombre que desee.
1. En **Opciones de implementación de producción**, seleccione **Pausar antes de implementar en Producción**.

   Esta opción inserta una puerta de aprobación manual justo antes del paso de producción. La canalización se detiene y espera a que un aprobador (como un administrador de implementación o un propietario del negocio) apruebe o cancele la implementación de producción.

   Se utiliza para el control de cambios o comprobaciones de última hora.

1. Haga clic en **Guardar** para crear la canalización de solo producción con estas opciones.

   ![Creación de una canalización de solo producción](/help/implementing/cloud-manager/configuring-pipelines/assets/add-production-only-pipeline.png)

## Ejecutar canalizaciones solo de fase y de solo producción {#running}

Puede iniciar las nuevas canalizaciones [como cualquier otra canalización](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines). También puede almacenar en déclencheur una canalización solo de producción directamente desde los detalles de ejecución de una canalización solo de fase.

<!-- * Stage-only and prod-only pipelines offer a new [emergency mode](#emergency-mode) to skip testing.
Prod-only pipeline run can be triggered directly from the execution details of a [stage-only pipeline](#stage-only-run).


### Emergency Mode {#emergency-mode}

When starting production-only and staging-online pipelines, you are prompted to confirm the start and how it starts.

* **Normal Mode** is a standard run and includes stage testing steps.
* **Emergency Mode** skips stage testing steps.

![Emergency Mode](/help/assets/configure-pipelines/emergency-mode.png) -->

### Ejecutar canalizaciones solo de fase {#stage-only-run}

En los detalles de ejecución, aparece un botón **Promocionar compilación** después de los pasos de prueba. Haga clic en él para almacenar en déclencheur una canalización de solo producción que implemente los artefactos de fase de esta ejecución en producción. El botón solo se muestra en la última ejecución solo de fase correcta.

![Ejecución de canalización de solo fase](/help/implementing/cloud-manager/configuring-pipelines/assets/stage-only-pipelines-run.png)

Al hacer clic en **Promocionar compilación**, se abre un cuadro de diálogo para que confirme la ejecución de la canalización de solo producción relacionada. Haga clic en **Ejecutar** para iniciarlo.

![Promocionar compilación - Ejecutar cuadro de diálogo de canalización](/help/implementing/cloud-manager/configuring-pipelines/assets/promote-build-run.png)

Si no existe ninguno, un cuadro de diálogo de configuración le pedirá que cree uno.

![Promocionar compilación: no hay ningún cuadro de diálogo de canalización válido](/help/implementing/cloud-manager/configuring-pipelines/assets/promote-build-no-valid-pipeline.png)


### Ejecutar canalizaciones solo de producción {#prod-only-run}

Para una canalización de **solo producción**, Cloud Manager muestra los artefactos de origen que se implementan en producción. Compruebe el paso **Preparación de artefactos** para la ejecución de origen y, a continuación, ábralo para ver los detalles y registros.


![Detalles del artefacto](/help/implementing/cloud-manager/configuring-pipelines/assets/prod-only-pipelines-run.png)
