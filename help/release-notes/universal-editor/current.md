---
title: Notas de la versión 2026.02.19 del editor universal
description: Estas son las notas de la versión 2026.02.19 del editor universal.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 39137052e9fa409f7f5494be53fa7693aaa60b17
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 28%

---


# Notas de la versión 2026.02.19 del editor universal {#release-notes}

Estas son las notas de la versión del editor universal del 19 de febrero de 2026.

>[!TIP]
>
>Si desea probar las **próximas** funciones del editor universal antes de su lanzamiento, consulte las [notas de la versión del editor universal.](/help/release-notes/universal-editor/preview.md)

>[!TIP]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Novedades {#what-is-new}

* Se han realizado mejoras en el RTE.
   * [Ahora se admite la ocultación de elementos de la barra de herramientas en el contexto RTE](/help/implementing/universal-editor/configure-rte.md#common-action-options).
   * [Ahora se admite ajustar texto dentro de tablas con párrafos](/help/implementing/universal-editor/configure-rte.md#table-actions).
   * [Etiquetas HTML no admitidas](/help/implementing/universal-editor/configure-rte.md#unsupported-html) ahora RTE puede conservarlas.
   * La lógica RTE ahora se proporciona desde un archivo independiente.
   * Ahora se pueden crear [tablas](/help/sites-cloud/authoring/universal-editor/authoring.md#formatting-options) que también se pueden editar con RTE.
* Si no se establece ninguna etiqueta, ahora se utiliza el título del componente de la definición del componente.
* `setEditorMode` ya está disponible a través de extensiones.

## Funciones de adopción anticipada {#early-adopter}

Si le interesa probar las próximas funciones enumeradas a continuación y compartir sus comentarios, envíe un correo electrónico a Customer Success Manager de Adobe desde la dirección de correo electrónico asociada a su Adobe ID.

* Se ha implementado una copia superficial para los fragmentos de contenido.

## Otras mejoras {#other-improvements}

* Los extremos RTE ahora se proporcionan para el editor in situ.
* La edición de campos anidados ya no provoca la sobrescritura de entradas del mismo nivel de esas estructuras.
* Los campos RTE obligatorios ya no se pueden guardar como vacíos.
* El formato in situ ya no se aplica de forma incorrecta al añadir vínculos después del formato.
