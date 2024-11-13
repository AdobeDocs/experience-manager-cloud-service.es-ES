---
title: Configurar invalidación push
description: Obtenga información acerca de cómo configurar la invalidación push para crear su propia CDN de producción.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 7cded93c-325c-4a4b-8644-e6a2379d5179
source-git-commit: 0ac6856e8f3e664fcc7e3c08faac4c4f5c16af18
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 2%

---

# Configuración de invalidación push

La invalidación push garantiza que las actualizaciones de contenido realizadas por los autores se eliminen automáticamente de la red de distribución de contenido (CDN) administrada cuando se publican. Al hacerlo, se garantiza que solo se proporcione el contenido más reciente.

El sistema borra el contenido en función de direcciones URL específicas y etiquetas o claves de caché, lo que garantiza que se purguen las versiones obsoletas.

Para habilitar la invalidación push, se deben agregar propiedades específicas al archivo de configuración del proyecto. Por ejemplo, un libro de Microsoft Excel denominado `.helix/config.xlsx` en SharePoint o un nombre de hoja de Google `.helix/config` en Google Drive.

Las siguientes propiedades de configuración definen el nombre del host de producción y el tipo de administración de CDN:

| key | valor | comentario |
| --- | --- | --- |
| `cdn.prod.host` | `<Production Host>` | Nombre de host del sitio de producción. Por ejemplo, `www.example.com`. |
| `cdn.prod.type` | administrado |   |

Una vez que se realicen cambios en la hoja de configuración, los usuarios deben obtener una vista previa y activarla mediante la [herramienta de Sidekick](/help/edge/docs/sidekick.md) para aplicar las actualizaciones.

Ver también [Acerca de la lista de tareas pendientes de Edge Delivery en Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md#ed-todo-list).
