---
title: Configurar invalidación push
description: Obtenga información acerca de cómo configurar la invalidación push para crear su propia CDN de producción.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: bb225fcb931c6e9014ab18e6efbb0620262bcd76
workflow-type: tm+mt
source-wordcount: '160'
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

Vea también [Introducción a los Edge Delivery Services en Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md#ed-todo-list).
