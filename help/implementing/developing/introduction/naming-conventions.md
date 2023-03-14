---
title: Convenciones de nomenclatura
description: Los nodos del repositorio están sujetos a las convenciones de nomenclatura del Repositorio de contenidos de Java
exl-id: 3c5c39dd-b209-488b-a93e-e840786fe224
source-git-commit: c08e442e58a4ff36e89a213aa7b297b538ae3bab
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 17%

---

# Convenciones de nomenclatura{#naming-conventions}

Los nodos del repositorio están sujetos a las convenciones de nomenclatura del Repositorio de contenidos de Java. AEM Sin embargo, impone otras convenciones para el nombre de los nodos de la página.

## Convenciones de nomenclatura para páginas {#naming-conventions-for-pages}

Estas convenciones de nomenclatura se implementan en varios niveles:

* AEM JcrUtil: la implementación de la aplicación de la aplicación de la aplicación de la [Utilidades JCR](#jcr-utilities).
* PageManager: el [Administrador de páginas](#page-manager) proporciona métodos para operaciones a nivel de página.
* AEM Dentro de la IU de {#ui-behavior}

### Utilidades JCR {#jcr-utilities}

[JcrUtil](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/jcr/JcrUtil.html) AEM es la implementación de la implementación de la implementación de JCR. De especial interés para validar nombres son las asignaciones de caracteres que controla y las siguientes validaciones:

* `isValidName`
   * Comprueba si el nombre no está vacío y contiene solo caracteres válidos.
   * Se puede utilizar para comprobar si un nombre propuesto es válido.
* `createValidName`
   * Esto crea una etiqueta válida a partir de una cadena arbitraria.
   * Se puede utilizar para crear un nombre a partir de un título.

### Administrador de páginas {#page-manager}

[PageManager](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/PageManager.html) proporciona métodos para operaciones a nivel de página, basados en [JCRUtil](#jcr-utilities).

### AEM Comportamiento de interfaz de usuario {#ui-behavior}

AEM Al administrar el contenido, la interfaz de usuario de:

* Valida el nombre según las restricciones impuestas por PageManager cuando:
   * se proporciona un título de página para la conversión en el nombre del nodo
   * se proporciona un nombre de nodo explícito
