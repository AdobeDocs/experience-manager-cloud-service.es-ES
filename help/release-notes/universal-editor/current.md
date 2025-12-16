---
title: Notas de la versión 2025.12.12 del editor universal
description: Estas son las notas de la versión 2025.12.11 del editor universal.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: b7b89587a81d0cadc81d4b2a486c022557c4a9fb
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 21%

---


# Notas de la versión 2025.12.12 del editor universal {#release-notes}

Estas son las notas de la versión del editor universal del 12 de diciembre de 2025.

>[!TIP]
>
>Si desea probar las **próximas** funciones del editor universal antes de su lanzamiento, consulte las [notas de la versión del editor universal.](/help/release-notes/universal-editor/preview.md)

>[!TIP]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Novedades {#what-is-new}

* Se ha agregado compatibilidad a las tablas existentes en el [editor de texto enriquecido.](/help/sites-cloud/authoring/universal-editor/authoring.md#formatting-options)
* La tecla de tabulación se ha habilitado para anidar listas en el [editor de texto enriquecido.](/help/sites-cloud/authoring/universal-editor/authoring.md#formatting-options)
* La característica de inicio de sesión para desarrolladores ahora se puede deshabilitar mediante la [metaetiqueta `aem-dev-login`.](/help/implementing/universal-editor/customizing.md#meta-tags)
* Ahora, al hacer clic con el botón secundario en la sección de superposición, se muestra un [menú de opciones contextuales.](/help/sites-cloud/authoring/universal-editor/authoring.md#context-options)
* [La sangría de ámbito](/help/implementing/universal-editor/configure-rte.md#indentation) ahora se admite en el [editor de texto enriquecido.](/help/sites-cloud/authoring/universal-editor/authoring.md#formatting-options)

## Funciones de adopción anticipada {#early-adopter}

Si le interesa probar las próximas funciones enumeradas a continuación y compartir sus comentarios, envíe un correo electrónico a Customer Success Manager de Adobe desde la dirección de correo electrónico asociada a su Adobe ID.

* Se ha implementado una copia superficial para los fragmentos de contenido.

## Otras mejoras {#other-improvements}

* El carril de propiedades ahora se sincroniza cuando varios campos cambian en contexto.
* El selector de Fragmentos de contenido ahora se abre como se espera en las instancias de AEM 6.5.
* La tecla escape ahora cierra los cuadros de diálogo en el editor de texto enriquecido.
* La acción **Quitar componente** ahora solo está disponible cuando se selecciona un componente.
* El editor de fragmentos de contenido correcto (antiguo o nuevo) ahora se abre en función de la instancia utilizada (si el nombre de host es el patrón de AEM as a Cloud Service, utilice el nuevo editor; de lo contrario, utilice el editor heredado).
* La validación del filtro se agrega a la acción duplicada.
* Los títulos largos ahora se truncan en el carril de propiedades.
* Las matrices de administradores de varios sitios con más de 10 valores ahora se administran correctamente.
* Los errores de conflicto al crear varios componentes con el mismo nombre ahora se gestionan correctamente.
* Se ha añadido la administración de matrices de administradores de varios sitios con valores >10.
