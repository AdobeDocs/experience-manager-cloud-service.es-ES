---
title: Convenciones de nomenclatura
description: Los nodos del repositorio están sujetos a las convenciones de nomenclatura del Repositorio de contenidos de Java
exl-id: 3c5c39dd-b209-488b-a93e-e840786fe224
source-git-commit: a446efacb91f1a620d227b9413761dd857089c96
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 15%

---

# Convenciones de nomenclatura{#naming-conventions}

Los nodos del repositorio están sujetos a las convenciones de nomenclatura del Repositorio de contenidos de Java. Sin embargo, AEM impone otras convenciones para el nombre de los nodos de página.

## Convenciones de nomenclatura para las páginas {#naming-conventions-for-pages}

Estas convenciones de nomenclatura se implementan en varios niveles:

* JcrUtil: la implementación AEM de las [utilidades JCR](#jcr-utilities).
* PageManager: el [Administrador de páginas](#page-manager) proporciona métodos para las operaciones a nivel de página.
* Dentro de la interfaz de usuario de AEM {#ui-behavior}

### Utilidades JCR {#jcr-utilities}

[](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/jcr/JcrUtil.html) JcrUtiliza la implementación AEM de las utilidades JCR. De particular interés para validar nombres son las asignaciones de caracteres que controla y las siguientes validaciones:

* `isValidName`
   * Comprueba si el nombre no está vacío y contiene solo caracteres válidos.
   * Se puede utilizar para comprobar si un nombre propuesto es válido.
* `createValidName`
   * Esto crea una etiqueta válida a partir de una cadena arbitraria.
   * Se puede utilizar para crear un nombre a partir de un título.

### Administrador de páginas {#page-manager}

[](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/PageManager.html) PageManager proporciona métodos para operaciones a nivel de página, basados en  [JCRUtil](#jcr-utilities).

### Comportamiento de la interfaz de usuario de AEM {#ui-behavior}

Al administrar contenido, la interfaz de usuario de AEM:

* Valida el nombre según las restricciones impuestas por PageManager cuando:
   * se proporciona un título de página para su conversión en el nombre del nodo
   * se proporciona un nombre de nodo explícito
