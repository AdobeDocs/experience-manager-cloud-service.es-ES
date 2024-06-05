---
title: Desarrollo y diferencia de página
description: Comprenda cómo funciona la función Diferencias de página y cómo puede afectar a un desarrollador
exl-id: 03c08616-2203-4b90-bed6-4836266e2507
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 12%

---

# Desarrollo y diferencia de página {#developing-and-page-diff}

## Descripción general de funciones {#feature-overview}

La creación de contenido es un proceso iterativo. La creación con eficiencia de contenido requiere poder ver qué ha cambiado de una iteración a otra. Visualizar la versión de la página y luego otra es un proceso poco eficaz y propenso a errores. Un autor desea poder comparar la página actual con una versión anterior en paralelo con las diferencias resaltadas.

La diferencia de página permite al usuario comparar la página actual con lanzamientos, versiones anteriores, etc. Para obtener más información sobre esta función de usuario, consulte [Diferencias de página](/help/sites-cloud/authoring/sites-console/page-diff.md).

## Detalles de operación {#operation-details}

AEM Al comparar versiones de una página, la versión anterior que el usuario desea comparar se vuelve a crear en segundo plano para facilitar la comparación de diferencias. La comparación de versiones de una página se realiza de nuevo en segundo plano para facilitar la comparación de diferencias. Esta versión anterior es necesaria para procesar el contenido [para una comparación en paralelo](/help/sites-cloud/authoring/sites-console/page-diff.md).

AEM Esta operación de recreación se realiza por parte de los usuarios de forma interna, es transparente para el usuario y no requiere intervención alguna. Sin embargo, un administrador que visualice el repositorio, por ejemplo, en CRXDE Lite, verá estas versiones recreadas dentro de la estructura de contenido.

Cuando se compara contenido, todo el árbol hasta la página para comparar se vuelve a crear en la siguiente ubicación:

`/tmp/versionhistory/`

Se ejecuta automáticamente una tarea de limpieza para limpiar este contenido temporal.

## Restricciones {#limitations}

La diferencia se produce en el lado del cliente mediante la comparación DOM, lo que simplifica el proceso de diferencia. Sin embargo, el desarrollador debe tener en cuenta varias limitaciones.

* AEM Esta función utiliza clases CSS a las que no se les asigna un espacio de nombres para el producto de. Si se incluyen en la página otras clases CSS personalizadas o clases CSS de terceros con los mismos nombres, la visualización de la diferencia puede verse afectada.

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* Dado que la comparación de diferencias es del lado del cliente y se ejecuta al cargar la página, no se contabilizan los ajustes en el DOM después de ejecutar el servicio de comparación de diferencias del lado del cliente. Este proceso puede afectar a lo siguiente:

   * AJAX Componentes que utilizan la para incluir contenido
   * Aplicaciones de una sola página
   * Componentes basados en JavaScript que manipulan el DOM tras la interacción del usuario.
