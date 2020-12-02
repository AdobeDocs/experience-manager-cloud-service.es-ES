---
title: Convenciones de nomenclatura
description: Los nodos del repositorio están sujetos a las convenciones de nomenclatura del Repositorio de contenidos de Java
translation-type: tm+mt
source-git-commit: fee73b5f5ba69422494efe554ac5aa62c046ad86
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 14%

---


# Asignar nombres a las convenciones{#naming-conventions}

Los nodos del repositorio están sujetos a las convenciones de nomenclatura del Repositorio de contenidos de Java. Sin embargo, AEM impone otras convenciones para el nombre de los nodos de página.

## Convenciones de nombres para páginas {#naming-conventions-for-pages}

Estas convenciones de nombres se implementan en varios niveles:

* JcrUtil: la implementación AEM de las [utilidades JCR](#jcr-utilities).
* PageManager: el [Administrador de páginas](#page-manager) proporciona métodos para las operaciones de nivel de página.
* Dentro de la IU AEM {#ui-behavior}

### Utilidades JCR {#jcr-utilities}

[](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/commons/jcr/JcrUtil.html) JcrUtiliza la implementación AEM de las utilidades JCR. De particular interés para validar nombres son las asignaciones de caracteres que controla y las siguientes validaciones:

* `isValidName`
   * Comprueba si el nombre no está vacío y solo contiene caracteres válidos.
   * Se puede utilizar para comprobar si un nombre propuesto es válido.
* `createValidName`
   * Esto crea una etiqueta válida a partir de una cadena arbitraria.
   * Se puede utilizar para crear un nombre a partir de un título.

### Administrador de páginas {#page-manager}

[](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) PageManager proporciona métodos para las operaciones de nivel de página, según  [JCRUtil](#jcr-utilities).

### Comportamiento de la interfaz de usuario de AEM {#ui-behavior}

Al administrar el contenido, la interfaz de usuario AEM:

* Valida el nombre según las restricciones impuestas por PageManager cuando:
   * se proporciona un título de página para la conversión en el nombre del nodo
   * se proporciona un nombre de nodo explícito
