---
title: Superposiciones para Adobe Experience Manager como Cloud Service
description: AEM como Cloud Service utiliza el principio de superposiciones para permitirle ampliar y personalizar las consolas y otras funciones
translation-type: tm+mt
source-git-commit: 58440cb565039becd5b08333994b70f2ea77cc99
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---


# Overlays in AEM as a Cloud Service {#overlays-in-aem}

Adobe Experience Manager como Cloud Service utiliza el principio de superposiciones para permitirle ampliar y personalizar las consolas y otras funciones (por ejemplo, la creación de páginas).

<!--
Adobe Experience Manager as a Cloud Service uses the principle of overlays to allow you to extend and customize the [consoles](/help/sites-developing/customizing-consoles-touch.md) and other functionality (for example, [page authoring](/help/sites-developing/customizing-page-authoring-touch.md)).
-->

Overlay es un término que se puede utilizar en muchos contextos. En este contexto (la ampliación de AEM como Cloud Service), una superposición significa tomar la funcionalidad predefinida e imponer sus propias definiciones sobre ella (para personalizar la funcionalidad estándar).

En una instancia estándar, la funcionalidad predefinida se mantiene en `/libs` y se recomienda definir la superposición (personalizaciones) en la `/apps` rama. AEM utiliza una ruta de búsqueda para encontrar un recurso, buscando primero la rama y luego la `/apps` rama `/libs` (la ruta de [búsqueda se puede configurar](#configuring-the-search-paths)). Este mecanismo significa que la superposición (y las personalizaciones definidas allí) tendrán prioridad.

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

* No ***debe *realizar cambios en la`/libs`rama **. Es posible que se pierdan los cambios que realice, ya que esta rama puede cambiar cada vez que:

   * actualizar en su instancia
   * aplicar una revisión
   * instalar un paquete de funciones

* Concentran los cambios en un solo lugar; facilitando el seguimiento, la migración, la copia de seguridad y/o la depuración de los cambios según sea necesario.

## Configuración de las rutas de búsqueda {#configuring-the-search-paths}

Para las superposiciones, el recurso enviado es un acumulado de los recursos y las propiedades recuperados, según las rutas de búsqueda que se puedan definir:

* El recurso **Resolver Ruta** de búsqueda según se define en la configuración [de](/help/implementing/deploying/configuring-osgi.md) OSGi para la Fábrica **de resolución de recursos de Sling de** Apache.

   * El orden descendente de las rutas de búsqueda indica sus prioridades respectivas.
   * En una instalación estándar, los valores predeterminados principales son `/apps`, `/libs` por lo que el contenido de `/apps` tiene una prioridad mayor que el de `/libs` (es decir, *lo superpone* ).

* Dos usuarios de servicios necesitan acceso JCR:READ a la ubicación donde se almacenan las secuencias de comandos. Estos usuarios son: components-search-service (utilizado por los com.day.cq.wcm.coreto componentes access/cache) y sling-scripting (utilizado por org.apache.sling.servlets.resolver para encontrar servlets).
* La siguiente configuración también debe configurarse según dónde coloque los scripts (en este ejemplo en /etc, /libs o /apps).

   ```
   PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
   resource.resolver.searchpath=["/etc","/apps","/libs"]
   resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
   ```

* Finalmente, debe configurarse también el Resolver Servlet (en este ejemplo para agregar también /etc)

   ```
   PID = org.apache.sling.servlets.resolver.SlingServletResolver
   servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
   ```

<!--
## Example of Usage {#example-of-usage}

Some examples are covered when:

* [Customizing the Consoles](/help/sites-developing/customizing-consoles-touch.md)
* [Customizing Page Authoring](/help/sites-developing/customizing-page-authoring-touch.md)
-->