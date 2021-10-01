---
title: Canalizaciones CI-CD
description: Canalizaciones CI-CD
index: false
source-git-commit: e51b995aebb053f38cb99879be70e23447f543c0
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---


# Canalizaciones de CI-CD de Cloud Manager {#intro-cicd}

En Cloud Manager, hay dos tipos de Canalización:

* **Canalización de producción**
* **Canalización que no es de producción**

## Canalización de producción {#prod-pipeline}

Las canalizaciones de producción son una canalización creada a propósito que incluye una serie de pasos organizados para llevar el código fuente hasta la producción. Los pasos incluyen la creación, empaquetado, prueba, validación e implementación en todo el entorno de ensayo primero. Huelga decir que una canalización de producción solo se puede añadir una vez que se crea un conjunto de entornos de producción y de fase.

>[!NOTE]
>Consulte Configuración de canalización de producción para obtener más información.


## Canalización que no es de producción {#non-prod-pipeline}

Una canalización que no es de producción tiene como objetivo ejecutar análisis de calidad de código o implementar código fuente en un entorno de desarrollo.

>[!NOTE]
>Consulte las canalizaciones de no producción y solo calidad de código para obtener más información.

La implementación y la calidad del código compatibles en la canalización de producción y no producción en Cloud Manager se clasifican en dos tipos diferentes:

* Front-End
* Pila completa

La siguiente tabla resume las canalizaciones:


>[!NOTE]
>Una canalización de CD/CI en Cloud Manager se activa mediante un evento, como una solicitud de extracción de un repositorio de código fuente, es decir, un cambio de código, o una programación regular para coincidir con una cadencia de lanzamiento.
>
>Para configurar la canalización, debe:
>* definir el déclencheur que iniciará la canalización
>* definir los parámetros que controlan la implementación de producción
>* configurar los parámetros de prueba de rendimiento