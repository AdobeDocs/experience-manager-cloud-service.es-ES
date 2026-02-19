---
title: Notas de la versión de Universal Editor Preview
description: Estas son las notas de la versión de la vista previa del editor universal.
feature: Release Information
role: Admin
exl-id: e8d031aa-4676-4e45-977b-e5dffcc404c4
source-git-commit: 39137052e9fa409f7f5494be53fa7693aaa60b17
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# Notas de la versión de Universal Editor Preview {#preview}

Estas son las notas de la versión de la **versión de vista previa** del editor universal. Estas características están disponibles actualmente en el **entorno de vista previa** del editor universal. Estas funciones están programadas para su lanzamiento general el 26 de febrero de 2026.

Estas notas de la versión de **preview** se proporcionan para que sepa qué cambios se avecinan en el editor universal y pueda probarlos al [cambiar a la versión de vista previa.](/help/sites-cloud/authoring/universal-editor/navigation.md#user-properties)

>[!TIP]
>
>Para las **notas de la versión actuales** del editor universal, consulte el documento [Notas de la versión del editor universal.](/help/release-notes/universal-editor/current.md)

>[!NOTE]
>
>El contenido de la versión real y la fecha de lanzamiento están sujetos a cambios.

## Próximas mejoras {#other-improvements}

* El editor ya no establece el contenido predeterminado en `{}` antes de que llegue el contenido, lo que evita la pérdida de datos en determinadas situaciones.
* Los cambios ya no se pierden al editar en el panel izquierdo y, a continuación, seleccionar otro elemento en la ventana del editor.
* Ya no se requiere la importación manual de css al utilizar `headless-canvas`.
* Para fines de CORS, se utilizan los puntos finales correctos para stage, preview y prod.
* Se ha añadido una descripción a todos los campos de esquema.
* Ahora se admiten actualizaciones de varios campos en fragmentos de contenido para ediciones en contexto.
* La persistencia de los datos cuando el campo está enfocado se hizo más robusta.
