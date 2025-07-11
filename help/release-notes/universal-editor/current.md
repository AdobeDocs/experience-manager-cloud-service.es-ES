---
title: Notas de la versión 2025.07.09 del editor universal
description: Estas son las notas de la versión 2025.07.09 del editor universal.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 199ee7e11f6706773bd426c3d27236d6ea791a6c
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 25%

---


# Notas de la versión 2025.07.09 del editor universal {#release-notes}

Estas son las notas de la versión del editor universal del 9 de julio de 2025.

>[!TIP]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Novedades {#what-is-new}

* [Al hacer clic en el botón de barra de herramientas **Agregar** en los contenedores,](/help/sites-cloud/authoring/universal-editor/authoring.md#adding-components) si solo se permite un tipo de componente, se inserta inmediatamente sin que sea necesario seleccionar en el menú desplegable.
* [La opción de la barra de herramientas del encabezado de autenticación](/help/sites-cloud/authoring/universal-editor/navigation.md#autentication-settings) se ha colocado detrás de una opción de característica, ya que no resulta útil en la mayoría de los casos.
* [Dado que no se permite anidar contenedores para varios campos en el panel de propiedades,](/help/implementing/universal-editor/field-types.md#fields) la rutina de procesamiento ahora filtra los contenedores anidados de la lista de campos para evitar el anidamiento no válido.

## Funciones de adopción anticipada {#early-adopter}

Si le interesa probar estas próximas funciones y compartir sus comentarios, envíe un correo electrónico a Customer Success Manager de Adobe desde la dirección de correo electrónico asociada a su Adobe ID.

### Nuevo RTE {#new-rte}

El nuevo RTE de ProseMirror, con un selector de páginas en el cuadro de diálogo de vínculos, ya está disponible en el panel derecho.

### Deshacer/Rehacer {#undo-redo}

Deshacer y rehacer ya está disponible para los autores de contenido del editor universal.

* Esto incluye las ediciones realizadas en el contexto y las realizadas a través del panel Propiedades, así como la adición (o duplicación), el movimiento y la eliminación de bloques.
* Deshacer y rehacer está limitado a la sesión actual del explorador.

## Otras mejoras {#other-improvements}

* Se ha corregido un problema en el cual la eliminación de una sola referencia de recurso no era posible al editar mediante el carril de propiedades.
* Se ha corregido un problema en el cual el panel Propiedades se cargaba indefinidamente porque las referencias de recursos se convertían automáticamente en matrices, lo que provocaba un estado de carga infinito.
   * Los valores de referencia de recursos ahora se almacenan tal cual, sin conversión automática a matrices.
* Se corrigió un problema en el cual el panel Propiedades no mostraba campos cuando se definía un modelo, pero no contenía contenido.
   * Esto provocaba un estado de carga infinito para el panel Propiedades para respuestas de detalle vacías, como fragmentos de contenido vacíos.
* La configuración de ESLint se ha refactorizado para garantizar la compatibilidad con la versión 9, incluidas las reglas actualizadas y la compatibilidad con complementos.

## Degradaciones {#deprecations}

* El componente `text-input` ya está oficialmente obsoleto.
   * En `model-definition.json`, utilice el componente Texto para crear entradas de texto para el panel Propiedades.
