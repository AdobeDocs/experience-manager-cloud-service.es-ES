---
title: Notas de la versión 2025.07.09 del editor universal
description: Estas son las notas de la versión 2025.07.09 del editor universal.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 199ee7e11f6706773bd426c3d27236d6ea791a6c
workflow-type: ht
source-wordcount: '368'
ht-degree: 100%

---


# Notas de la versión 2025.07.09 del editor universal {#release-notes}

Estas son las notas de la versión del 9 de julio de 2025 del editor universal.

>[!TIP]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Novedades {#what-is-new}

* [Al hacer clic en el botón de la barra de herramientas **Añadir** en los contenedores,](/help/sites-cloud/authoring/universal-editor/authoring.md#adding-components) si solo se permite un tipo de componente, se inserta inmediatamente sin que sea necesario seleccionarlo en el menú desplegable.
* [La opción de la barra de herramientas del encabezado de autenticación](/help/sites-cloud/authoring/universal-editor/navigation.md#autentication-settings) se ha colocado detrás de una opción de función, ya que no resulta útil en la mayoría de los casos.
* [Dado que no se permite anidar contenedores para múltiples campos en el panel de propiedades,](/help/implementing/universal-editor/field-types.md#fields) la rutina de renderizado ahora filtra los contenedores anidados de la lista de campos para evitar anidamientos no válidos.

## Funciones de adopción anticipada {#early-adopter}

Si le interesa probar estas nuevas funciones y compartir sus comentarios, envíe un correo electrónico a su Adobe Customer Success Manager desde la dirección de correo electrónico asociada a su Adobe ID.

### Nuevo RTE {#new-rte}

El nuevo RTE de ProseMirror, que cuenta con un selector de páginas en el cuadro de diálogo de vínculos, ya está disponible en el panel derecho.

### Deshacer/Rehacer {#undo-redo}

Deshacer y rehacer ya está disponible para los autores de contenido del editor universal.

* Esto incluye las ediciones realizadas en el contexto y las realizadas a través del panel Propiedades, así como la adición (o duplicación), el movimiento y la eliminación de bloques.
* Deshacer y rehacer está limitado a la sesión actual del explorador.

## Otras mejoras {#other-improvements}

* Se ha solucionado un problema por el que no era posible eliminar referencias de recursos individuales al editar mediante el carril de propiedades.
* Se ha solucionado un problema por el que el panel Propiedades se cargaba indefinidamente porque las referencias de los recursos se convertían automáticamente en matrices, lo que provocaba un estado de carga infinita.
   * Los valores de referencia de los recursos ahora se almacenan tal cual, sin conversión automática a matrices.
* Se ha solucionado un problema por el que el panel Propiedades no mostraba campos cuando se definía un modelo, pero no contenía ningún contenido.
   * Esto provocaba un estado de carga infinita para el panel Propiedades para respuestas de detalles vacías, como los fragmentos de contenido vacíos.
* La configuración de ESLint se ha rediseñado para garantizar la compatibilidad con la versión 9, incluidas las reglas actualizadas y la compatibilidad con los complementos.

## Componentes obsoletos {#deprecations}

* El componente `text-input` ya está oficialmente obsoleto.
   * En `model-definition.json`, utilice el componente de texto para crear entradas de texto para el panel Propiedades.
