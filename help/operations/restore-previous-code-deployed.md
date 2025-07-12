---
title: Restaurar el código de Source anterior implementado
description: Aprenda a restaurar un entorno a su última compilación correcta &ndash; no se requiere la ejecución de la canalización.
feature: Operations
role: Admin
badge: label="Alpha" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket"
exl-id: 8f804f55-a66d-47ad-a48d-61b861cef4f7
source-git-commit: 19e23785f2c4fbfa5a244864fe16500c1e7e128b
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 3%

---

# Restaurar el código fuente anterior implementado en AEM as a Cloud Service {#restore-previous-code-deployed}

>[!NOTE]
>
>La función descrita en este artículo solo está disponible a través del programa pionero alpha. Para suscribirse al alfa, vea [Reversión en un solo clic para implementaciones de canalización](/help/implementing/cloud-manager/release-notes/current.md##one-click-rollback).

Use **Restaurar código anterior implementado** para revertir un entorno instantáneamente a su última compilación correcta; no se requiere la ejecución de la canalización.

Simplemente abre el menú ![Icono de más o el icono de menú de puntos suspensivos](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) del entorno seleccionado y elige **Restaurar** > **Código anterior implementado** para revertir el código fuente implementado más recientemente en segundos.

>[!TIP]
>
>Puede ver la versión del código fuente activo en uso en la vista de detalles del entorno, en la ficha **General**. Ver [Ver detalles de un entorno](/help/implementing/cloud-manager/manage-environments.md#viewing-environment).
>
>![Versión de código Source en uso](/help/operations/assets/environments-view-details-sourcecodeversion.png)

La característica **Restaurar código anterior implementado** solo está disponible cuando la condición **every** que se muestra a continuación es verdadera:

* Usted tiene permisos de **Environment Restore Create**. Para obtener más información sobre la administración de permisos, consulte [Permisos personalizados](/help/implementing/cloud-manager/custom-permissions.md).
* Su organización está inscrita en el programa de adopción anticipada y el indicador de funcionalidad está activado.
* El programa se ejecuta en AEM as a Cloud Service.
* El entorno elegido es `Development` (límite temporal de Alpha).
* La última canalización para ese entorno se ejecutó correctamente hace **menos de 10 días**.
* El estado del entorno es *En ejecución* y no hay ninguna canalización en curso.
* La versión de código fuente de destino que desea restaurar se implementó **en un plazo de 30 días**.

Si alguna comprobación falla, Cloud Manager abre el siguiente cuadro de diálogo que enumera una o más condiciones incumplidas y deshabilita **Confirm**, lo que impide la restauración.

![Restaurar el código anterior implementado en el cuadro de diálogo](/help/operations/assets/restore-previous-code-deployment-not-allowed.png).

Si solo desea restaurar los datos que se perdieron, dañaron o eliminaron accidentalmente a su estado original, puede usar [Restaurar contenido en AEM as a Cloud Service](/help/operations/restore.md). Este proceso de restauración solo afecta al contenido, no modifica el código fuente ni la versión de AEM.

**Para restaurar el código anterior implementado:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Haga clic en el programa para el que desea iniciar una restauración.

1. Enumere todos los entornos para el programa mediante uno de los procedimientos siguientes:

   * En el menú del lado izquierdo, debajo de **Servicios**, haga clic en ![Icono de datos](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Entornos**.

     ![Pestaña Entornos](assets/environments-1.png)

   * En el menú del lado izquierdo, debajo de **Programa**, haga clic en **Información general** y, a continuación, en la tarjeta **Entornos**, haga clic en ![Icono de flujo de trabajo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) **Mostrar todo**.

     ![Mostrar todas las opciones](assets/environments-2.png)

     >[!NOTE]
     >
     >La tarjeta **Entornos** solo enumera tres entornos. Haga clic en **Mostrar todo** en la tarjeta para ver *todos* los entornos del programa.

1. En la tabla Entornos, a la derecha de un entorno cuyo código fuente desee restaurar, haga clic en ![icono Más o icono de menú de puntos suspensivos](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) y, a continuación, haga clic en **Restaurar** > **Código anterior implementado**.

   ![Restaurar el código anterior implementado desde el menú de puntos suspensivos](/help/operations/assets/restore-previous-code-deployed-menu.png)

1. En el cuadro de diálogo **Restaurar código anterior implementado**, revise la versión implementada actualmente y la versión que desea restaurar y, a continuación, haga clic en **Confirmar**.

   ![Restaurar código anterior implementado en el cuadro de diálogo](/help/operations/assets/restore-previous-code-deployed-dialogbox.png)

1. Cloud Manager revierte el entorno a la versión anterior, mantiene el contenido y la configuración intactos y marca el entorno **Restaurando** en la página Entornos hasta que se complete la implementación.

   ![Restaurando activación](/help/operations/assets/restore-previous-code-deployed-restoring.png)
