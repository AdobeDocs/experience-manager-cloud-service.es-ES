---
title: Visualización de registros de un conjunto de migraciones en la herramienta de transferencia de contenido (heredada)
description: Visualización de registros de un conjunto de migraciones en la herramienta de transferencia de contenido
hide: true
hidefromtoc: true
source-git-commit: 1fb4d0f2a3b3f9a27f5ab1228ec2d419149e0764
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 64%

---

# Visualización de registros de un conjunto de migraciones (heredado) {#view-logs-content-transfer-tool}

Una vez completado cada paso (extracción e ingesta), compruebe los registros y busque errores.  Cualquier error debe solucionarse inmediatamente, ya sea abordando los problemas notificados o poniéndose en contacto con el servicio de asistencia al Adobe.

## Pasos para ver registros {#viewing-logs}

La visualización de registros de un conjunto de migraciones existente en la página *Información general* .
Complete los siguientes pasos:

1. Vaya a la página *Información general*, seleccione el conjunto de migración que desee eliminar y haga clic en **Visualización de registros** en la barra de acciones.

   ![image](/help/journey-migration/content-transfer-tool/assets/view-log1.png)

1. Aparece el cuadro de diálogo **Registros** . Haga clic en **Extracción de registros** para ver los registros en una nueva pestaña.

   ![image](/help/journey-migration/content-transfer-tool/assets/view-log2.png)
O

   también puede crear Visualización de registros para el conjunto de migraciones desde la pantalla *Información general* . Seleccione el conjunto de migración y haga clic en el estado en el campo **EXTRACCIÓN** . En este caso, haga clic en **FINALIZADO** para ver los registros de vista en una nueva pestaña.

   ![image](/help/journey-migration/content-transfer-tool/assets/view-log3.png)

1. Para rastrear los registros sin utilizar la interfaz de usuario, puede SSH en el entorno AEM de origen y seguir el `crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`.
