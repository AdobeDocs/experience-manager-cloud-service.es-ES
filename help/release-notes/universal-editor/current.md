---
title: Notas de la versión de Universal Editor 2024.06.28
description: Estas son las notas de la versión de la versión 2024.06.28 de Universal Editor.
feature: Release Information
role: Admin
source-git-commit: cc94ad2ba42707bb7541217f0225b995f64ad84f
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 1%

---


# Notas de la versión de Universal Editor 2024.06.28 {#release-notes}

Estas son las notas de la versión del editor universal del 28 de junio de 2024.

>[!TIP]
>
>Para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service, consulte [esta página.](/help/release-notes/release-notes-cloud/release-notes-current.md)

## Novedades {#what-is-new}

* **Inicio**: las páginas recientes se muestran como una lista, sin imágenes de vista previa.
* **Barra de ubicación**: se añadió la validación mejorada de URL, que aplica las URL HTTPS y admite hashes en las URL para contabilizar aplicaciones enrutadas por hash.
* **Navegación por teclado**: la selección de superposición de página se desacopló del enfoque del carril de propiedades para mejorar la navegación mediante el teclado en la página sin perder el enfoque.
* **Etiquetas de elementos**: el valor de reserva para etiquetas ahora utiliza `data-aue-prop` en lugar de `data-aue-type` para una identificación más clara en las superposiciones y el árbol de contenido.
* **Modal RTE**: A **Cancelar** se ha añadido el botón al modal del editor de texto enriquecido al abrirlo desde el panel de propiedades.
* **Servicio UE en el nodo**: Se ha vuelto a introducir la compatibilidad HTTP para el servicio de editor universal, ya que todas las conexiones HTTPS finalizan en el nivel de Dispatcher.
* **API de copia interna**: se ha añadido una API al servicio de editor universal para copiar componentes, lo que permite la futura introducción de las opciones de la barra de herramientas para copiar y duplicar contenido.

## Correcciones de errores {#bug-fixes}

* **Ruta de exploración del panel Propiedades**: se ha corregido el menú de ruta de exploración del panel de propiedades de los elementos anidados profundamente que no permanecían abiertos.
* **Selector de fragmentos de contenido**: El selector de Fragmento de contenido se mejoró para garantizar que respeta las reglas definidas en el modelo de fragmento de contenido o en el `data-aue-filter`.
* **Inserción de componentes**: Se corrigió la lista para insertar nuevos componentes que no se actualizaron con precisión después de navegar a otra página.
* **Estado de publicación**: se mejoró la gestión de los estados de publicación para funcionar de forma más coherente.
* **Correcciones diversas**: Esta versión también contiene varias correcciones menores, limpieza de deuda técnica, mejoras de seguridad y pruebas consolidadas para la estabilidad y el rendimiento generales.
