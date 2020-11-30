---
title: Superposiciones para Adobe Experience Manager como Cloud Service
description: AEM como Cloud Service utiliza el principio de superposiciones para permitirle ampliar y personalizar las consolas y otras funciones
translation-type: tm+mt
source-git-commit: 8028682f19ba6ba7db6b60a2e5e5f5843f7ac11f
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 2%

---


# Superposiciones en AEM as a Cloud Service {#overlays-in-aem}

Adobe Experience Manager como Cloud Service utiliza el principio de superposiciones para permitirle ampliar y personalizar las consolas y otras funciones (por ejemplo, la creación de páginas).

<!--
Adobe Experience Manager as a Cloud Service uses the principle of overlays to allow you to extend and customize the [consoles](/help/sites-developing/customizing-consoles-touch.md) and other functionality (for example, [page authoring](/help/sites-developing/customizing-page-authoring-touch.md)).
-->

Overlay es un término que se puede utilizar en muchos contextos. En este contexto (extendiendo AEM como Cloud Service), una superposición significa tomar la funcionalidad predefinida e imponer sus propias definiciones sobre ella (para personalizar la funcionalidad estándar).

En una instancia estándar, la funcionalidad predefinida se mantiene en `/libs` y se recomienda definir la superposición (personalizaciones) en la `/apps` rama (mediante una ruta [de](#search-paths) búsqueda para resolver los recursos).

* La IU táctil utiliza superposiciones relacionadas con [granito](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html):

   * Método

      * Reconstruya la `/libs` estructura adecuada en `/apps`.

         Esto no requiere una copia 1:1, ya que la fusión [de recursos de](/help/implementing/developing/introduction/sling-resource-merger.md) Sling se utiliza para hacer referencia cruzada a las definiciones originales que son necesarias. La fusión de recursos Sling proporciona servicios para acceder a los recursos y combinarlos mediante mecanismos de diferenciación (diferenciación).

      * Realice los cambios en `/apps`.
   * Ventajas

      * Más robusto para los cambios en `/libs`.
      * Solo redefinir lo que realmente se requiere.


<!-- Still links to reference material in 6.5 -->

>[!CAUTION]
>
>La fusión [de recursos de](/help/implementing/developing/introduction/sling-resource-merger.md) Sling y los métodos relacionados solo pueden utilizarse con [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). Esto significa que la creación de una superposición con una estructura de esqueleto solo es adecuada para la IU estándar con capacidad táctil.

Las superposiciones son el método recomendado para realizar muchos cambios, como la configuración de las consolas o la creación de la categoría de selección en el navegador de recursos del panel lateral (utilizado al crear páginas). Se requieren como:

<!--
Overlays are the recommended method for many changes, such as [configuring your consoles](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) or [creating your selection category to the asset browser in the side panel](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) (used when authoring pages). They are required as:
-->

* No ***debe* realizar cambios en la `/libs` rama **. Es posible que se pierdan los cambios que realice, ya que esta rama puede sufrir cambios cada vez que se apliquen actualizaciones a la instancia.

* Concentran los cambios en un solo lugar; facilitando el seguimiento, la migración, la copia de seguridad y/o la depuración de los cambios según sea necesario.

## Rutas de búsqueda {#search-paths}

AEM utiliza una ruta de búsqueda para encontrar un recurso, buscando (de forma predeterminada) primero la rama y luego la `/apps` rama `/libs` . Este mecanismo significa que la superposición en `/apps` (y las personalizaciones definidas en ella) tendrán prioridad.

Para las superposiciones, el recurso enviado es un acumulado de los recursos y las propiedades recuperados, según las rutas de búsqueda definidas en la configuración OSGi.

<!--
## Example of Usage {#example-of-usage}

Some examples are covered when:

* [Customizing the Consoles](/help/sites-developing/customizing-consoles-touch.md)
* [Customizing Page Authoring](/help/sites-developing/customizing-page-authoring-touch.md)
-->