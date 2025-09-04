---
title: Notas de la versión 2025.09.04 del Editor universal
description: Estas son las notas de la versión 2025.09.04 del editor universal.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 0c380e0faca1db0966d22d056dd1f824a731a7bc
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 71%

---


# Notas de la versión 2025.09.04 del Editor universal {#release-notes}

Estas son las notas de la versión del editor universal del 4 de septiembre de 2025.

>[!TIP]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Novedades {#what-is-new}

* Copiar y pegar está disponible para [usuarios que lo adoptaron por primera vez](#copy-paste)

### Deshacer/Rehacer {#undo-redo}

Deshacer y rehacer ya está disponible para los autores de contenido del editor universal.

* Esto incluye las ediciones realizadas en el contexto y las realizadas a través del panel Propiedades, así como la adición (o duplicación), el movimiento y la eliminación de bloques.
* Deshacer y rehacer está limitado a la sesión actual del explorador.

## Funciones de adopción anticipada {#early-adopter}

Si le interesa probar estas nuevas funciones y compartir sus comentarios, envíe un correo electrónico a su Adobe Customer Success Manager desde la dirección de correo electrónico asociada a su Adobe ID.

### Nuevo RTE {#new-rte}

El nuevo RTE de ProseMirror, que cuenta con un selector de páginas en el cuadro de diálogo de vínculos, ya está disponible en el panel derecho.

### Copiar/Pegar {#copy-paste}

Los autores de contenido ya pueden copiar y pegar componentes dentro de la misma página.

## Otras mejoras {#other-improvements}

* El estilo de la barra de herramientas del editor se ha actualizado para alinearse mejor con el próximo RTE nuevo.
* Se han restaurado los filtros del cuadro de diálogo del selector de recursos.

## Componentes obsoletos {#deprecations}

* Los componentes `text-input` y `text-area` quedaron oficialmente obsoletos con la [versión 2025.07.09.](/help/release-notes/universal-editor/2025/2025-07-09.md)
   * En `model-definition.json`, utilice el componente de texto para crear entradas de texto para el panel Propiedades.
