---
title: Configuración de la invalidación push para un sitio de Edge Delivery
description: Descubra cómo configurar la invalidación push para un sitio de Edge Delivery a fin de garantizar actualizaciones de contenido y un control de almacenamiento en caché eficientes.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 7cded93c-325c-4a4b-8644-e6a2379d5179
source-git-commit: bb149cd43158bfd1ceb43b04cc536c8c8291f968
workflow-type: ht
source-wordcount: '173'
ht-degree: 100%

---

# Configuración de invalidación push

La invalidación push garantiza que las actualizaciones de contenido realizadas por los autores se eliminen automáticamente de la red de distribución de contenido (CDN) administrada cuando se publican. Al hacerlo, se garantiza que solo se proporcione el contenido más reciente.

El sistema borra el contenido en función de URL y etiquetas o claves de caché específicas, lo que garantiza que se purguen las versiones obsoletas.

Para habilitar la invalidación push, se deben añadir propiedades específicas al archivo de configuración del proyecto. Por ejemplo, un libro de Microsoft Excel denominado `.helix/config.xlsx` en SharePoint o un nombre de hoja de Google `.helix/config` en Google Drive.

Las siguientes propiedades de configuración definen el nombre del host de producción y el tipo de administración de CDN:

| key | valor | comentario |
| --- | --- | --- |
| `cdn.prod.host` | `<Production Host>` | Nombre de host del sitio de producción. Por ejemplo, `www.example.com`. |
| `cdn.prod.type` | Administrado |   |

Una vez que se realicen cambios en la hoja de configuración, los usuarios deben obtener una vista previa y activarla mediante la [herramienta de barra de tareas](https://www.aem.live/docs/sidekick) para aplicar las actualizaciones.

Ver también [Acerca de la lista de tareas pendientes de Edge Delivery en Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md#ed-todo-list).
