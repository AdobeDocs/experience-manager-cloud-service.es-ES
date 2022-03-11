---
title: Superposiciones de Adobe Experience Manager as a Cloud Service
description: AEM as a Cloud Service utiliza el principio de las superposiciones para permitirle ampliar y personalizar las consolas y otras funciones
exl-id: 24bdb1a9-6d77-43c7-a75e-28e6e0fd7608
source-git-commit: ac760e782f80ee82a9b0604ef64721405fc44ee4
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 2%

---

# Superposiciones en AEM as a Cloud Service {#overlays-in-aem}

Adobe Experience Manager as a Cloud Service utiliza el principio de las superposiciones para permitirle ampliar y personalizar las consolas y otras funciones (por ejemplo, la creación de páginas).

La superposición es un término que se puede utilizar en muchos contextos. En este contexto (ampliación AEM as a Cloud Service), una superposición implica tomar la funcionalidad predefinida e imponer sus propias definiciones sobre ella (para personalizar la funcionalidad estándar).

En una instancia estándar, la funcionalidad predefinida se mantiene en `/libs` y se recomienda definir la superposición (personalizaciones) en la variable `/apps` rama (usando una [ruta de búsqueda](#search-paths) para resolver los recursos).

* La IU táctil utiliza [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)Superposiciones relacionadas:

   * Método

      * Reconstruya el `/libs` estructura `/apps`.

         Esto no requiere una copia 1:1, ya que la variable [Fusión de recursos de Sling](/help/implementing/developing/introduction/sling-resource-merger.md) se utiliza para hacer referencia cruzada a las definiciones originales que son necesarias. La fusión de recursos de Sling proporciona servicios para acceder y fusionar recursos mediante mecanismos de diferenciación (diferenciación).

      * Realice cualquier cambio en `/apps`.
   * Ventajas

      * Más robusto en `/libs`.
      * Solo redefina lo que realmente se requiere.


>[!CAUTION]
>
>La variable [Fusión de recursos de Sling](/help/implementing/developing/introduction/sling-resource-merger.md) y los métodos relacionados solo se pueden usar con [Granite](https://www.adobe.io/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html). Esto significa que la creación de una superposición con una estructura de esqueletos solo es adecuada para la IU estándar con capacidad táctil.

Las superposiciones son el método recomendado para muchos cambios, como configurar las consolas o crear la categoría de selección en el navegador de recursos del panel lateral (se utiliza al crear páginas). Son necesarias como:

* You ***no debe* realice cambios en `/libs` Rama **Cualquier cambio que realice puede perderse, ya que esta rama puede variar cada vez que se apliquen actualizaciones a la instancia.

* Concentran los cambios en un solo lugar; facilitando el seguimiento, la migración, la copia de seguridad o la depuración de los cambios según sea necesario.

## Rutas de búsqueda {#search-paths}

AEM utiliza una ruta de búsqueda para encontrar un recurso, buscando (de forma predeterminada) primero la variable `/apps` y luego la `/libs` rama. Este mecanismo significa que la superposición de `/apps` (y las personalizaciones definidas allí) tendrán prioridad.

Para las superposiciones, el recurso enviado es un agregado de los recursos y propiedades recuperados, según las rutas de búsqueda definidas en la configuración OSGi.
