---
title: Convenciones de nomenclatura
description: Los nodos del repositorio están sujetos a las convenciones de nomenclatura del repositorio de contenido de Java
exl-id: 3c5c39dd-b209-488b-a93e-e840786fe224
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 1%

---

# Convenciones de nomenclatura{#naming-conventions}

Los nodos del repositorio están sujetos a las convenciones de nomenclatura del repositorio de contenido Java. Sin embargo, AEM impone más convenciones para el nombre de los nodos de página.

## Convenciones de nomenclatura para páginas {#naming-conventions-for-pages}

Estas convenciones de nomenclatura se implementan en varios niveles:

* JcrUtil: la implementación de AEM de [las utilidades JCR](#jcr-utilities).
* PageManager: [Page Manager](#page-manager) proporciona métodos para operaciones a nivel de página.
* Dentro de la IU de AEM {#ui-behavior}

### Utilidades JCR {#jcr-utilities}

[JcrUtil](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/jcr/JcrUtil.html) es la implementación de AEM de las utilidades JCR. De especial interés para validar nombres son las asignaciones de caracteres que controla y las siguientes validaciones:

* `isValidName`
   * Comprueba si el nombre no está vacío y contiene solo caracteres válidos.
   * Se puede utilizar para comprobar si un nombre propuesto es válido.
* `createValidName`
   * Esto crea una etiqueta válida a partir de una cadena arbitraria.
   * Se puede utilizar para crear un nombre a partir de un título.

### Administrador de páginas {#page-manager}

[PageManager](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/PageManager.html) proporciona métodos para operaciones a nivel de página, basados en [JCRUtil](#jcr-utilities).

### Comportamiento de IU de AEM {#ui-behavior}

Al administrar el contenido, la interfaz de usuario de AEM:

* Valida el nombre según las restricciones impuestas por PageManager cuando:
   * se proporciona un título de página para la conversión en el nombre del nodo
   * se proporciona un nombre de nodo explícito
