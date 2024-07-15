---
title: Información general sobre el transformador de contenido
description: Obtenga información sobre cómo detectar y corregir problemas relacionados con el contenido notificados por la BPA mediante el transformador de contenido.
exl-id: aa3397ff-3dd6-4c67-9064-cb9b19bf1c73
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 3%

---

# Información general {#overview-ct}

El transformador de contenido (CT) es una herramienta desarrollada por Adobe AEM que se puede usar para detectar y corregir automáticamente los problemas relacionados con el contenido notificados por el [Analizador de prácticas recomendadas (BPA)](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) antes de migrar el contenido de su implementación actual (On-Premise o Managed Services) a AEM as a Cloud Service.

El transformador de contenido puede ayudar a resolver los problemas que se encuentran en las siguientes [categorías de patrones de BPA](https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html?lang=es) (que se muestran en la tabla siguiente), ya que permite a los usuarios realizar acciones masivas como mover o eliminar. Esto puede reducir significativamente el tiempo y la complejidad asociada con un proyecto de migración.

## Categorías de patrones cubiertas por el transformador de contenido y soluciones sugeridas {#pattern-categories-and-benefits}

| Código de patrón | Tipo/subtipo de sospecha | Posible corrección antes de migrar contenido a AEM as a Cloud Service |
|--------------|--------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| ACV | missing.jcrcontent <br> missing.original.rendition <br> metadata.descendientes. | Mueva estos recursos a una ubicación diferente o elimínelos para asegurarse de que no se migran a AEM as a Cloud Service. |
| CAV | content.area.violation | Mueva las rutas temporalmente a `/etc/packages/content-transformation/paths` para asegurarse de que no se migran a AEM as a Cloud Service. |
| DOPI | deprecated.ordered.index | Elimine los índices obsoletos. |
| OAUI | non.migrated.oauth.users | Elimine estos usuarios para asegurarse de que no se migran a AEM as a Cloud Service. |
| PCX | page.complex.medium <br> page.complex.high | Elimine las páginas o elementos secundarios o muévalos a una ubicación diferente para asegurarse de que no se migran a AEM as a Cloud Service. |
| REP | forward.replication <br> reverse.replication <br> standard.replication.agent.modify <br> custom.replication.agent.discovery | Elimine los agentes de replicación creados. <br> O <br> Quitar las propiedades modificadas o agregadas. |
| URS | clientlibs.location <br> file.location <br> node.location <br> workflow.location | Desplácese a la ubicación correcta para evitar problemas durante la migración. |
| URS | node.size | Mueva los nodos temporalmente a `/etc/packages/content-transformation/paths` para asegurarse de que no se migran a AEM as a Cloud Service. |

## Ventajas proporcionadas por el transformador de contenido {#benefits}

El transformador de contenido ofrece las siguientes ventajas:

* Seguridad contra fallos: el transformador de contenido crea un paquete cada vez que realiza alguna modificación en el repositorio para solucionar problemas. Si es necesario, puede volver al estado anterior instalando el paquete.
* Fácil de usar: el transformador de contenido se ha integrado con la herramienta de transferencia de contenido y viene con una interfaz de usuario sencilla e intuitiva.
* Ahorra tiempo: cuando tiene un número elevado de problemas de contenido que se incluyen en una categoría de patrón, puede resolverlos todos con varios clics mediante el transformador de contenido.
