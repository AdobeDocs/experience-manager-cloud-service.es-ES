---
title: Iniciar flujo de trabajo en el editor de comunicaciones interactivas
description: Iniciar flujo de trabajo en el Editor de comunicaciones interactivas en AEM Forms permite a los autores aplicar flujos de trabajo predefinidos a una comunicación interactiva.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
badgeSaas: label="AEM Forms" type="Positive" tooltip="(Se aplica a AEM Forms)."
source-git-commit: 322183c28719db5b8657d9532ef234e1d18821cd
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 1%

---


# Iniciar flujo de trabajo en el editor de comunicaciones interactivas

## Información general

La función Flujo de trabajo de creación de comunicaciones interactivas permite a los autores aplicar flujos de trabajo predefinidos a una comunicación interactiva. Los flujos de trabajo ayudan a automatizar el proceso de revisión y aprobación mediante el enrutamiento de la CI a través de una secuencia de tareas asignadas a distintos usuarios.

Mediante flujos de trabajo, el autor puede garantizar que el contenido de CI se revise, valide y apruebe antes de finalizarse o publicarse.

## Aplicar un flujo de trabajo a una comunicación interactiva

Puede aplicar un flujo de trabajo a una comunicación interactiva (CI) de dos formas:

+++ Desde el panel Forms y documentos

![Buscar documento CI](/help/forms/interactive-communication/assets/workflow-in-ic.png)

Siga estos pasos para iniciar y aplicar un flujo de trabajo:

1. Vaya a **AEM Forms > Forms y documentos**.

1. Seleccione la comunicación interactiva (CI) que desee procesar.

1. En la barra de herramientas, haga clic en **Iniciar flujo de trabajo**.

1. En el cuadro de diálogo de flujo de trabajo, elija el **modelo de flujo de trabajo** necesario.

![Buscar documento CI](/help/forms/interactive-communication/assets/select-workflow.png)

1. Actualizar detalles del flujo de trabajo (como título, descripción o persona asignada).

1. Haga clic en **continuar** para iniciar el flujo de trabajo.

La CI ahora está asociada al flujo de trabajo seleccionado y se moverá a través de los pasos definidos del flujo de trabajo.
+++

+++ Desde el editor de comunicaciones interactivas

![Buscar documento CI](/help/forms/interactive-communication/assets/workflow.png)

Siga estos pasos para aplicar un flujo de trabajo desde la CI:

1. Vaya a **AEM Forms > Forms y documento**.

1. Abra la **comunicación interactiva** necesaria en el editor.

1. En la barra de herramientas superior, seleccione **Flujo de trabajo**.

1. Elija el **modelo de flujo de trabajo** necesario.

![Buscar documento CI](/help/forms/interactive-communication/assets/select-workflow.png)

1. Proporcione los detalles necesarios y haga clic en **continuar**.

El flujo de trabajo se aplica y la CI pasa por las fases de flujo de trabajo configuradas para su revisión o procesamiento.
+++

## Capacidades clave

* Automatiza los procesos de revisión y aprobación
* Garantiza la calidad y el cumplimiento del contenido
* Mejora la colaboración entre autores y editores
* Rastrea el progreso del flujo de trabajo y la finalización de tareas

Al aplicar flujos de trabajo, los autores pueden automatizar los procesos de revisión, asignar tareas a editores o revisores y garantizar que el CI se revise correctamente antes de completarse. Este enfoque estructurado mejora la eficiencia, la colaboración y la gobernanza en la administración de contenido de CI.
