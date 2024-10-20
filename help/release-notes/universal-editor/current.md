---
title: Notas de la versión de Universal Editor 2024.08.13
description: Estas son las notas de la versión de la versión 2024.08.13 del Editor universal.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: c66621eb336b8e6eb5ceb1056c089c190fcd1c34
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---


# Notas de la versión de Universal Editor 2024.08.13 {#release-notes}

Estas son las notas de la versión del editor universal del 13 de agosto de 2024.

>[!TIP]
>
>Para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service, consulte [esta página.](/help/release-notes/release-notes-cloud/release-notes-current.md)

## Novedades de la aplicación {#what-is-new}

* **Tipos de datos personalizados**: adapte el editor a sus necesidades de datos únicas con la capacidad de [crear campos personalizados dentro del panel de propiedades.](https://developer.adobe.com/uix/docs/services/aem-universal-editor/api/item-types-renderers/)
   * Tanto si va a desarrollar un selector de productos personalizado para casos de uso comerciales como si va a rellenar una lista desplegable con valores de sus backends, esta función le proporciona el control que necesita sobre los datos que los autores utilizan para componer contenido.
* **Arrastrar y soltar contenedores**: disfruta de una mayor flexibilidad en la composición del diseño con la capacidad de [mover componentes entre diferentes contenedores mediante arrastrar y soltar](/help/sites-cloud/authoring/universal-editor/authoring.md#reordering-components) dentro del [panel Árbol de contenido.](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode)
* **Integración de GitHub optimizada**: se ha introducido el almacenamiento en caché para las respuestas de GitHub, lo que acelera considerablemente la recuperación de etiquetas y `universal-editor-cors-library`, lo que da como resultado una experiencia de usuario más rápida y fluida.
* **Validación de token de IMS configurable**: Para aumentar la flexibilidad en la administración de tokens, la validación de tokens de [IMS ahora es opcional.](/help/implementing/universal-editor/local-dev.md#setting-up-service)
   * Esta opción de configuración le permite deshabilitar la validación según sea necesario y simplificar las configuraciones de la puerta de enlace en la nube.
* **Integración de Splunk**: el registro de Splunk se ha integrado en el [servicio de editor universal para el desarrollo local](/help/implementing/universal-editor/local-dev.md#setting-up-service), lo que mejora la supervisión y el diagnóstico.
   * Esta integración garantiza un seguimiento eficiente del registro, operaciones más fluidas y una solución de problemas más rápida.

## Correcciones de errores {#bug-fixes}

* **Comentarios mejorados sobre la publicación**: Si la publicación falla porque no tiene permisos suficientes, los comentarios recibidos por el usuario durante la publicación se han mejorado para mostrar una advertencia clara en lugar de indicar simplemente un error.
* **Administración de URL mejorada**: se solucionaron los problemas con la codificación/descodificación de URL incorrecta que causaban errores de publicación.
* **Administración de datos precisa**: Se ha solucionado un problema por el que los números flotantes se almacenaban incorrectamente como números enteros, lo que garantiza una administración de datos precisa en todo el contenido.
* **Seguridad y estabilidad**: se han corregido las vulnerabilidades de seguridad en las imágenes Docker y se ha implementado la cobertura de prueba para componentes críticos como el Selector de componentes y las Rutas de exploración, lo que conduce a una experiencia de editor más segura, estable y confiable.
