---
title: Notas de la versión 2025.06.19 del editor universal
description: Estas son las notas de la versión 2025.06.19 del editor universal.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 5ffae9e548ca952975b3ea805808e227102ec99f
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 26%

---


# Notas de la versión 2025.06.19 del editor universal {#release-notes}

Estas son las notas de la versión del editor universal del 19 de junio de 2025.

>[!TIP]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Novedades {#what-is-new}

* **Compatibilidad con varios campos en el carril Propiedades** -
  [Ahora se puede usar el componente contenedor](/help/implementing/universal-editor/field-types.md#container) para crear propiedades de varios campos.
* **Compatibilidad con propiedades anidadas**: el campo [`name`](/help/implementing/universal-editor/field-types.md#nesting) ahora admite rutas para habilitar el anidamiento de propiedades.
* **Panel derecho redimensionable**: ahora se puede cambiar el tamaño del panel lateral para tener en cuenta el contenido más largo que se muestra en el panel lateral.

## Funciones de adopción anticipada {#early-adopter}

Para tener la oportunidad de probar algunas de las próximas funciones, forme parte del programa de adopción anticipada de Adobe.

### **Deshacer/Rehacer** {#undo-redo}

Deshacer y rehacer ya está disponible para los autores de contenido del Editor universal.

* Esto incluye las ediciones realizadas en el contexto y las realizadas a través del panel Propiedades, así como la adición (o duplicación), el movimiento y la eliminación de bloques.
* Deshacer y rehacer está limitado a la sesión actual del explorador.

Si le interesa probar esta nueva función y compartir sus comentarios, envíe un correo electrónico a su Adobe Customer Success Manager desde la dirección de correo electrónico asociada a su ID de Adobe.

## Otras mejoras {#other-improvements}

* Se corrigieron errores de colisión de claves de recursos al mover bloques entre contenedores.
* Se ha corregido un problema que hacía que fallara la duplicación del último bloque de un contenedor.
* La lista desplegable Agregar acción ahora solo enumera los componentes que tienen un complemento adecuado definido en el archivo `component-definition.json`.
* La fecha de modificación utilizada por el cuadro de diálogo de publicación se corrigió en el que, en algunas circunstancias, las páginas no se reconocieron como modificadas y no se volvieron a publicar.
* Se ha corregido el comportamiento de herencia de MSM en el que al editar un contenedor se cancelaba la herencia para nodos secundarios.
* `fetchUrl` se corrigió y se restauraron los bloques en movimiento de un contenedor a otro.
