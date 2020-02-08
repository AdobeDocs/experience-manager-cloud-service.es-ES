---
title: Migrar al servicio de nube desde Adobe Experience Manager 6.x
description: Migrar al servicio de nube desde Adobe Experience Manager 6.x
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Pasar a Recursos Adobe Experience Manager como un servicio de nube {#move-to-assets-cloud-service}

<!-- About the need to move from previous AEM deployment to a cloud service deployment. And how does Adobe help do it OOTB?
-->

## Acerca de la herramienta de migración {#migration-tool}

<!-- 
Link back to information about the tool in the Experience Manager as a Cloud Service docs if the tool works the same for Sites and Assets. Document the Assets-specific information here.

* What is the migration tool called? Is there a branding term for it?
* How much do we want to elaborate about the Pattern Detector rules? Is there a branding term for it?
* Before migrating using the tool, is any prepping required?
* See CQ-4271901

-->

La herramienta de migración le ayuda a lograr lo siguiente:

* Convierta los modelos de flujo de trabajo existentes en perfiles de procesamiento que funcionen con el servicio de cómputo de recursos.
* Elimine los pasos no admitidos de los modelos de flujo de trabajo.
* Desactive los iniciadores de flujo de trabajo.
* Combine las configuraciones, después de la confirmación/validación del usuario, en el código fuente existente.

La herramienta de migración crea perfiles de procesamiento en un módulo Maven que los usuarios pueden utilizar de las dos formas siguientes:

* Fusiona en uno de sus proyectos existentes.
* Agregue el módulo como nuevo submódulo.

La herramienta de migración proporciona un informe de los cambios realizados e información sobre los mismos.

<!--  

What is the output of the tool, besides migrated content.

Give details about reports and logs of the tool. 

* How to access the report, including required permissions.
* How to read/interpret the report.
* Location of logs. How to read the logs.
* What common errors to look for. Troubleshooting for these errors.

-->

## Migrar contenido a una nueva implementación {#content-migration-across-deployments}
