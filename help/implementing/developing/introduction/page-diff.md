---
title: Desarrollo y diferencia de página
description: Comprender cómo funciona la función Diferencias de página y cómo puede afectar a un desarrollador
exl-id: 03c08616-2203-4b90-bed6-4836266e2507
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 11%

---

# Desarrollo y diferencia de página {#developing-and-page-diff}

## Descripción general de características {#feature-overview}

La creación de contenido es un proceso iterativo. La creación con eficiencia de contenido requiere poder ver qué ha cambiado de una iteración a otra. Visualizar una versión de la página y luego otra es un proceso poco eficaz y propenso a errores. Un autor quiere poder comparar la página actual con una versión anterior en paralelo con las diferencias resaltadas.

La diferencia de página permite al usuario comparar la página actual con los lanzamientos, versiones anteriores, etc. Para obtener más información sobre esta función de usuario, consulte [Diferencias de página](/help/sites-cloud/authoring/features/page-diff.md).

## Detalles de la operación {#operation-details}

Al comparar versiones de una página, la versión anterior que el usuario desea comparar se vuelve a crear AEM en segundo plano para facilitar la comparación de diferencias. Esto es necesario para poder renderizar el contenido [para la comparación en paralelo](/help/sites-cloud/authoring/features/page-diff.md).

Esta operación de recreación la realiza AEM internamente y es transparente para el usuario y no requiere ninguna intervención. Sin embargo, un administrador que viera el repositorio por ejemplo en CRX DE Lite vería estas versiones recreadas dentro de la estructura de contenido.

Cuando se compara el contenido, todo el árbol hasta la página para comparar se vuelve a crear en la siguiente ubicación:

`/tmp/versionhistory/`

Una tarea de limpieza se ejecuta automáticamente para limpiar este contenido temporal.

## Restricciones     {#limitations}

La diferencia se produce en el lado del cliente mediante la comparación DOM, lo que simplifica el proceso de comparación de diferencias. Sin embargo, el desarrollador debe tener en cuenta varias limitaciones.

* Esta función utiliza clases CSS que no tienen espacios de nombres en el producto AEM. Si se incluyen en la página otras clases CSS personalizadas o clases CSS de terceros con los mismos nombres, la visualización de la diferencia puede verse afectada.

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* Dado que la comparación de diferencias es del lado del cliente y se ejecuta al cargar la página, cualquier ajuste al DOM después de que se haya ejecutado el servicio de comparación de diferencias del lado del cliente no se contabilizará. Esto puede afectar

   * Componentes que utilizan AJAX para incluir contenido
   * Aplicaciones de una sola página
   * Componentes basados en JavaScript que manipulan el DOM tras la interacción del usuario.
