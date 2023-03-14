---
title: Superposiciones para Adobe Experience Manager as a Cloud Service
description: AEM El as a Cloud Service utiliza el principio de superposiciones para permitirle ampliar y personalizar las consolas y otras funcionalidades
exl-id: 24bdb1a9-6d77-43c7-a75e-28e6e0fd7608
source-git-commit: ac760e782f80ee82a9b0604ef64721405fc44ee4
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 2%

---

# Superposiciones en AEM as a Cloud Service {#overlays-in-aem}

Adobe Experience Manager as a Cloud Service utiliza el principio de las superposiciones para permitirle ampliar y personalizar las consolas y otras funcionalidades (por ejemplo, la creación de páginas).

Superposición es un término que se puede utilizar en muchos contextos. AEM En este contexto (ampliar la as a Cloud Service), una superposición significa tomar la funcionalidad predefinida e imponer sus propias definiciones sobre ella (para personalizar la funcionalidad estándar).

En una instancia estándar, la funcionalidad predefinida se encuentra en `/libs` y se recomienda definir la superposición (personalizaciones) en `/apps` rama (con un [ruta de búsqueda](#search-paths) para resolver los recursos).

* La IU táctil utiliza [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)Superposiciones relacionadas con:

   * Método

      * Reconstruya el adecuado `/libs` estructura bajo `/apps`.

         Esto no requiere una copia 1:1, ya que la [Fusión de recursos de Sling](/help/implementing/developing/introduction/sling-resource-merger.md) se utiliza para hacer referencia a las definiciones originales que son necesarias. La fusión de recursos de Sling proporciona servicios para acceder y combinar recursos mediante mecanismos de diferencia.

      * Realice cualquier cambio en `/apps`.
   * Ventajas

      * Más robustas a los cambios en `/libs`.
      * Redefina solo lo que realmente se necesita.


>[!CAUTION]
>
>El [Fusión de recursos de Sling](/help/implementing/developing/introduction/sling-resource-merger.md) y los métodos relacionados solo se pueden utilizar con [Granite](https://www.adobe.io/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html). Esto significa que la creación de una superposición con una estructura de esqueleto solo es adecuada para la IU táctil estándar.

Las superposiciones son el método recomendado para muchos cambios, como configurar las consolas o crear la categoría de selección en el explorador de recursos del panel lateral (utilizado al crear páginas). Se requieren como sigue:

* Usted ***no debe* realice cambios en la `/libs` ramificación **Cualquier cambio que realice puede perderse, ya que esta rama puede cambiar cada vez que se apliquen actualizaciones a su instancia.

* Concentran los cambios en una ubicación, lo que facilita el seguimiento, la migración, la realización de copias de seguridad o la depuración de los cambios según sea necesario.

## Rutas de búsqueda {#search-paths}

AEM utiliza una ruta de búsqueda para encontrar un recurso. La búsqueda (predeterminada) se realiza primero en el `/apps` y luego la `/libs` Rama. Este mecanismo significa que la superposición en `/apps` (y las personalizaciones definidas allí) tendrán prioridad.

En el caso de las superposiciones, el recurso enviado es un agregado de los recursos y las propiedades recuperados, según las rutas de búsqueda definidas en la configuración OSGi.
