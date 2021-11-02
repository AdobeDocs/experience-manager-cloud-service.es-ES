---
title: Canalizaciones CI-CD
description: Canalizaciones CI-CD
index: false
source-git-commit: 1887cc7374ece840b2dcca4482924b14c4793567
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---


# Canalizaciones de CI-CD de Cloud Manager {#intro-cicd}

## Introducción {#introduction}

Una canalización de CD/CI en Cloud Manager se puede activar mediante algún tipo de evento, como una solicitud de extracción de un repositorio de código fuente, es decir, un cambio de código o algún tipo de programación regular para coincidir con una cadencia de versión.

>[!NOTE]
>Para configurar la canalización, debe:
>* definir el déclencheur que iniciará la canalización
>* definir los parámetros que controlan la implementación de producción
>* configurar los parámetros de prueba de rendimiento


En Cloud Manager, hay dos tipos de Canalización:

* [Canalización de producción](#prod-pipeline)
* [Canalización que no es de producción](#non-prod-pipeline)

## Canalización de producción {#prod-pipeline}

Las canalizaciones de producción son una canalización creada a propósito que incluye una serie de pasos organizados para llevar el código fuente hasta la producción. Los pasos incluyen la creación, empaquetado, prueba, validación e implementación en todo el entorno de ensayo primero. Huelga decir que una canalización de producción solo se puede añadir una vez que se crea un conjunto de entornos de producción y de fase.

Consulte Configuración de canalización de producción para obtener más información.


## Canalización que no es de producción {#non-prod-pipeline}

Una canalización que no es de producción tiene como objetivo ejecutar análisis de calidad de código o implementar código fuente en un entorno de desarrollo.

Consulte las canalizaciones de no producción y solo calidad de código para obtener más información.
