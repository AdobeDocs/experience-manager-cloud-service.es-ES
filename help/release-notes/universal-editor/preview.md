---
title: Notas de la versión de Universal Editor Preview
description: Estas son las notas de la versión de la vista previa del editor universal.
feature: Release Information
role: Admin
exl-id: e8d031aa-4676-4e45-977b-e5dffcc404c4
source-git-commit: 374c8045043f67f06d4ae68aef499bb594f1c08c
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Notas de la versión de Universal Editor Preview {#preview}

Estas son las notas de la versión de la **versión de vista previa** del editor universal. Estas características están disponibles actualmente en el **entorno de vista previa** del editor universal. Estas funciones están programadas para su lanzamiento general el 19 de febrero de 2026.

Estas notas de la versión de **preview** se proporcionan para que sepa qué cambios se avecinan en el editor universal y pueda probarlos al [cambiar a la versión de vista previa.](/help/sites-cloud/authoring/universal-editor/navigation.md#user-properties)

>[!TIP]
>
>Para las **notas de la versión actuales** del editor universal, consulte el documento [Notas de la versión del editor universal.](/help/release-notes/universal-editor/current.md)

>[!NOTE]
>
>El contenido de la versión real y la fecha de lanzamiento están sujetos a cambios.

## Próximas nuevas funciones {#what-is-new}

* Se han realizado mejoras en el RTE.
   * Ahora se admite la ocultación de elementos de barra de herramientas en el RTE en contexto.
   * Ahora se admite el ajuste de texto dentro de tablas con párrafos.
   * Las etiquetas RTE no admitidas ahora se conservan.
   * La lógica RTE ahora se proporciona desde un archivo independiente.
   * Ahora se pueden crear y editar tablas con el RTE.
* Si no se establece ninguna etiqueta, ahora se utiliza el título del componente de la definición del componente.
* `setEditorMode` ya está disponible a través de extensiones.

## Próximas mejoras {#other-improvements}

* Se ha corregido la funcionalidad de copiar y pegar entre páginas.
* `universal-editor-extensibility` se ha cambiado a `universal-editor`.
* Se ha reducido el número de solicitudes al extremo de extensiones.
* Los desmontajes de RemoteApp se han reducido de tres a uno.
* Los extremos RTE ahora se proporcionan para el editor in situ.
* La edición de campos anidados ya no provoca la sobrescritura de entradas del mismo nivel de esas estructuras.
* Los campos RTE obligatorios ya no se pueden guardar como vacíos.
* El formato in situ ya no se aplica de forma incorrecta al añadir vínculos después del formato.
