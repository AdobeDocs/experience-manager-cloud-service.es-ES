---
title: Notas de la versión 2025.08.22 del Editor universal
description: Estas son las notas de la versión 2025.08.22 del editor universal.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: cd717eac1e4eb6eda3b2a60fc28ad63d92e858ec
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 71%

---


# Notas de la versión 2025.08.22 del Editor universal {#release-notes}

Estas son las notas de la versión del editor universal del 22 de agosto de 2025.

>[!TIP]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Novedades {#what-is-new}

* Nuevas funciones para [usuarios que adoptaron por primera vez RTE](#new-rte)
   * El título del vínculo ahora está disponible en el cuadro de diálogo del vínculo.
   * El desenlace ya está disponible.
   * Los elementos de la lista ahora admiten vínculos y formato en línea.
   * El área de desplazamiento era fija.

## Funciones de adopción anticipada {#early-adopter}

Si le interesa probar estas nuevas funciones y compartir sus comentarios, envíe un correo electrónico a su Adobe Customer Success Manager desde la dirección de correo electrónico asociada a su Adobe ID.

### Nuevo RTE {#new-rte}

El nuevo RTE de ProseMirror, que cuenta con un selector de páginas en el cuadro de diálogo de vínculos, ya está disponible en el panel derecho.

### Deshacer/Rehacer {#undo-redo}

Deshacer y rehacer ya está disponible para los autores de contenido del editor universal.

* Esto incluye las ediciones realizadas en el contexto y las realizadas a través del panel Propiedades, así como la adición (o duplicación), el movimiento y la eliminación de bloques.
* Deshacer y rehacer está limitado a la sesión actual del explorador.

## Otras mejoras {#other-improvements}

* [La característica de deshacer y rehacer que adoptó por primera vez](#undo-redo) ya no déclencheur una recarga de página cuando se agrega un componente mediante una operación de deshacer o rehacer.

## Componentes obsoletos {#deprecations}

* Los componentes `text-input` y `text-area` quedaron oficialmente obsoletos con la [versión 2025.07.09.](/help/release-notes/universal-editor/2025/2025-07-09.md)
   * En `model-definition.json`, utilice el componente de texto para crear entradas de texto para el panel Propiedades.
