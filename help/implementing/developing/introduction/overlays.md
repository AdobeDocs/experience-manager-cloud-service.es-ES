---
title: Superposiciones para Adobe Experience Manager as a Cloud Service
description: AEM El as a Cloud Service utiliza el principio de superposiciones para permitirle ampliar y personalizar las consolas y otras funcionalidades
exl-id: 24bdb1a9-6d77-43c7-a75e-28e6e0fd7608
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 2%

---

# Superposiciones en AEM as a Cloud Service {#overlays-in-aem}

Adobe Experience Manager as a Cloud Service utiliza el principio de las superposiciones para permitirle ampliar y personalizar las consolas y otras funcionalidades (por ejemplo, la creación de páginas).

Superposición es un término que se puede utilizar en muchos contextos. AEM En este contexto, al ampliar el espacio de trabajo de manera as a Cloud Service, una superposición significa tomar la funcionalidad predefinida e imponer sus propias definiciones sobre ella para personalizar la funcionalidad estándar.

En una instancia estándar, la funcionalidad predefinida se encuentra en `/libs` y se recomienda definir la superposición (personalizaciones) en `/apps` rama (con un [ruta de búsqueda](#search-paths) para resolver los recursos).

* La interfaz de usuario táctil utiliza [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)Superposiciones relacionadas con:

   * Método

      * Reconstruya el adecuado `/libs` estructura bajo `/apps`.

        Esta reestructuración no requiere una copia 1:1 porque la variable [Fusión de recursos de Sling](/help/implementing/developing/introduction/sling-resource-merger.md) se utiliza para hacer referencia a las definiciones originales que son necesarias. La fusión de recursos de Sling proporciona servicios para acceder y combinar recursos con mecanismos de diferencia.

      * En `/apps`, realice cambios.

   * Ventajas

      * Más robustas a los cambios en `/libs`.
      * Redefina solo lo que sea necesario.

>[!CAUTION]
>
>El [Fusión de recursos de Sling](/help/implementing/developing/introduction/sling-resource-merger.md) y los métodos relacionados solo se pueden utilizar con [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html). Esta regla significa que la creación de una superposición con una estructura de esqueleto solo es adecuada para la interfaz de usuario táctil estándar.

Las superposiciones son el método recomendado para muchos cambios. Por ejemplo, configurar las consolas o crear la categoría de selección en el explorador de recursos del panel lateral (utilizado al crear páginas). Se requieren como sigue:

* **En el `/libs` rama, *no* realice cambios**
Cualquier cambio que realice puede perderse, ya que esta rama puede cambiar cada vez que se apliquen actualizaciones a su instancia.

* Concentran los cambios en una ubicación, lo que facilita el seguimiento, la migración, la copia de seguridad o la depuración de los cambios según sea necesario.

## Rutas de búsqueda {#search-paths}

AEM utiliza una ruta de búsqueda para encontrar un recurso. La búsqueda es la primera opción (de forma predeterminada): `/apps` y luego la `/libs` Rama. Este mecanismo significa que la superposición en `/apps` (y las personalizaciones definidas allí) tiene prioridad.

En el caso de las superposiciones, el recurso enviado es un agregado de los recursos y las propiedades recuperados, según las rutas de búsqueda definidas en la configuración OSGi.
