---
title: Superposiciones para Adobe Experience Manager as a Cloud Service
description: AEM as a Cloud Service utiliza el principio de las superposiciones para permitirle ampliar y personalizar las consolas y otras funcionalidades
exl-id: 24bdb1a9-6d77-43c7-a75e-28e6e0fd7608
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 2%

---

# Superposiciones en AEM as a Cloud Service {#overlays-in-aem}

Adobe Experience Manager as a Cloud Service utiliza el principio de las superposiciones para permitirle ampliar y personalizar las consolas y otras funcionalidades (por ejemplo, la creación de páginas).

Superposición es un término que se puede utilizar en muchos contextos. En este contexto, al ampliar AEM as a Cloud Service, una superposición significa tomar la funcionalidad predefinida e imponer sus propias definiciones sobre ella para personalizar la funcionalidad estándar.

En una instancia estándar, la funcionalidad predefinida se mantiene en `/libs` y se recomienda definir la superposición (personalizaciones) en la rama `/apps` (mediante una [ruta de búsqueda](#search-paths) para resolver los recursos).

* La interfaz de usuario táctil usa superposiciones relacionadas con [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html):

   * Método

      * Reconstruir la estructura `/libs` adecuada en `/apps`.

        Esta reestructuración no requiere una copia de 1:1 porque [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) se usa para hacer referencia a las definiciones originales que se requieren. La fusión de recursos de Sling proporciona servicios para acceder y combinar recursos con mecanismos de diferencia.

      * En `/apps`, realice cambios.

   * Ventajas

      * Más seguro para los cambios en `/libs`.
      * Redefina solo lo que sea necesario.

>[!CAUTION]
>
>La [Fusión de recursos de Sling](/help/implementing/developing/introduction/sling-resource-merger.md) y los métodos relacionados solo se pueden usar con [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html). Esta regla significa que la creación de una superposición con una estructura de esqueleto solo es adecuada para la interfaz de usuario táctil estándar.

Las superposiciones son el método recomendado para muchos cambios. Por ejemplo, configurar las consolas o crear la categoría de selección en el explorador de recursos del panel lateral (utilizado al crear páginas). Se requieren como sigue:

* **En la rama `/libs`, *no* realice cambios**
Cualquier cambio que realice puede perderse, ya que esta rama puede cambiar cada vez que se apliquen actualizaciones a su instancia.

* Concentran los cambios en una ubicación, lo que facilita el seguimiento, la migración, la copia de seguridad o la depuración de los cambios según sea necesario.

## Rutas de búsqueda {#search-paths}

AEM usa una ruta de búsqueda para encontrar un recurso, buscando primero (de forma predeterminada) la rama `/apps` y, a continuación, la rama `/libs`. Este mecanismo significa que la superposición en `/apps` (y las personalizaciones definidas) tiene prioridad.

En el caso de las superposiciones, el recurso enviado es un agregado de los recursos y las propiedades recuperados, según las rutas de búsqueda definidas en la configuración OSGi.
