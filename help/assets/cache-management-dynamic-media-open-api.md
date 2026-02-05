---
title: Administración de caché en Dynamic Media con API abiertas
description: Administración de caché en Dynamic Media con API abiertas
role: User
source-git-commit: 89f21f96a741acbd6458c3777227548fbc89e525
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 1%

---

# Administración de caché en Dynamic Media con API abiertas {#cache-management-dynamic-media-open-apis}

La administración eficaz de la caché es esencial para ofrecer recursos digitales de alto rendimiento, escalables y actualizados. En Dynamic Media con API abiertas, la administración de caché define cómo se almacena, actualiza y entrega el contenido en las distintas capas de la canalización de envíos. Las respuestas de entrega de recursos se almacenan en caché en varias capas para garantizar un rendimiento óptimo y una entrega de contenido rápida.

El almacenamiento en caché prolongado en Dynamic Media con API abiertas consiste en [almacenamiento en caché de nivel CDN](#cdn-layer-caching) y [control de caché externo (BYOCDN y almacenamiento en caché de explorador)](#byocdn-browser-caching).

## Almacenamiento en caché de capa CDN {#cdn-layer-caching}

Las respuestas de entrega de recursos se almacenan en caché en [Adobe Managed CDN](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn#aem-managed-cdn) durante un período prolongado para maximizar el rendimiento y minimizar la carga en el origen. Adobe administra completamente este almacenamiento en caché para garantizar una experiencia de alta calidad coherente para los usuarios finales. La duración de la caché está optimizada intencionadamente para el rendimiento y los usuarios no pueden personalizarla para mantener la fiabilidad y la eficacia en la entrega de contenido a todos los clientes.

Todas las direcciones URL de envío se almacenan en caché en el perímetro (Fastly) durante un periodo de tiempo prolongado para garantizar un rendimiento óptimo. Los objetos de envío en caché incluyen representaciones estáticas, vídeos, binarios de imagen originales e imágenes transformadas dinámicamente, como recursos cambiados de tamaño o con formato modificado generados mediante parámetros de URL. <!--The CDN is designed to serve these assets directly from the cache without revalidating them, unless an explicit purge is performed.-->

## Control de caché externo (BYOCDN y almacenamiento en caché del explorador) {#byocdn-browser-caching}

Las respuestas de entrega de recursos incluyen un encabezado `Cache-Control` con un valor predeterminado `max-age` de **10 minutos** para las capas de almacenamiento en caché descendentes. Esto se aplica a las configuraciones personalizadas de *Traiga su propia CDN (BYOCDN)*, *exploradores de usuarios finales* y cualquier *proxy de almacenamiento en caché intermedio*, lo que garantiza un control de caché coherente en toda la ruta de envío.

### Personalizar encabezados de control de caché {#customizing-cache-control-headers}

El aumento del tiempo de caché para los valores activos más allá de la configuración predeterminada aumenta la probabilidad de ofrecer contenido obsoleto, lo que puede retrasar la visibilidad de las actualizaciones de contenido en la experiencia del usuario final. Si necesita modificar el comportamiento del control de caché para un caso de uso específico, puede configurar reglas de CDN personalizadas para ajustar los encabezados de respuesta. Esto le permite configurar diferentes duraciones de la caché según sus necesidades. Consulte [Reglas de CDN personalizadas de AEM para encabezados de respuesta](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic).

```
responseTransformations:
    rules:
      - name: cache-asset-delivery
        when:
          allOf:
            - reqProperty: path
              like: '/adobe/assets/urn:aaid:aem:*'
            - reqProperty: tier
              equals: delivery
        actions:
          - type: set
            respHeader: Cache-Control
            value: max-age=300
```

Para obtener ayuda adicional o hacer preguntas sobre la administración de caché, comuníquese con [Soporte técnico de Adobe](https://helpx.adobe.com/in/contact.html).

## Invalidación de caché activa {#active-cache-invalidation}

Cada vez que se actualiza, elimina o modifica un recurso (cualquier cambio en los metadatos), Dynamic Media con API abiertas invalida automáticamente todas las URL de entrega asociadas en la CDN administrada por Adobe. Esto se aplica a las direcciones URL que utilizan ID o alias de vanidad, junto con cualquier dirección URL que incluya parámetros de transformación, como anchura, formato o calidad. Esta invalidación impulsada por eventos garantiza que los usuarios siempre reciban la versión más actual de los recursos sin intervención manual.

### Depuración manual de caché {#manual-cache-purging}

Cuando es necesario purgar manualmente el contenido almacenado en caché, puede hacerlo usando las capacidades de invalidación de la caché de AEM. Para obtener instrucciones detalladas sobre cómo purgar direcciones URL de caché específicas, consulte [Invalidación de caché de CDN de AEM](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-cache-purge#single-purge).

## Preguntas frecuentes{#faq-cache-management}

+++**¿Cómo afecta la administración de caché a las integraciones existentes?**

Las direcciones URL de los recursos permanecen sin cambios y el encabezado de control de caché enviado a los exploradores (y otros intermediarios de flujo descendente) desde Adobe Managed CDN sigue siendo de 10 minutos con un [`stale-while-revalidate directive`](https://web.dev/articles/stale-while-revalidate#whats_it_mean), lo que garantiza que los sistemas de flujo descendente sigan aprovechando sus cachés de forma óptima.

+++

+++**¿En qué déclencheur se purga la memoria caché?**

Las déclencheur de depuración de caché se almacenan automáticamente cuando se actualiza, modifica, archiva o elimina un recurso.

<!--The cache purge triggers automatically in the following circumstances:
 
 - when an asset is updated, modified, or archived.
 - when an asset reaches `ready_for_delivery` state after approval.-->

+++

<!--
+++ **How long does it take for the cache to refresh after updating an asset?**

Any time the asset changes, the cache refreshes usually in *less than 60 seconds*.

+++

<!--
+++ **What happens if the cache purge system fails?**
The following mechanisms can be followed:
 
 - **Automatic retries:** 3 retry attempts with exponential backoff
 - **Monitoring:** Sev-2 alert fires if staleness exceeds 10 minutes
 - **Natural expiry:** Even without purge, cache expires after 10 hours maximum
 - **Manual override:** Engineers can manually purge via CLI tool

+++
-->

+++ **¿Qué tipos de recursos son compatibles con el almacenamiento en caché de larga duración?**

El almacenamiento en caché prolongado con invalidación de caché activa impulsada por evento es aplicable a todos los tipos de recursos de Dynamic Media con API abiertas, independientemente del tipo o formato de recurso.

+++

+++ **¿Puedo excluirme del almacenamiento en caché de larga duración para mi repositorio?**

Puede ponerse en contacto con el [Soporte de Adobe](https://helpx.adobe.com/in/contact.html) para explicarle los motivos y Adobe se pondrá en contacto con usted para hablar sobre el tema.

+++


>[!MORELIKETHIS]
>
>- [Integrar el Selector de recursos con varias aplicaciones](/help/assets/integrate-asset-selector.md)
>- [URL de vanidad](/help/assets/vanity-urls.md)
