---
title: Estructurar la administración de diversos sitios para el contenido segmentado
description: En un diagrama se muestra la estructuración de la compatibilidad con el uso de varios sitios para contenido de destino
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 86%

---


# Estructurar la administración de diversos sitios para el contenido segmentado {#how-multisite-management-for-targeted-content-is-structured}

En el siguiente diagrama se muestra la estructuración de la compatibilidad con el uso de varios sitios para contenido de destino

Las áreas aparecen debajo de **/content/campañas/&lt;marca>** y, de forma predeterminada, cada marca tiene un área maestra, que se crea automáticamente. Cada área tiene su propio conjunto de actividades, experiencias y ofertas.

![Estructura multisitio](/help/sites-cloud/authoring/assets/multisite-structure.png)

Para contenido de destino, las páginas o los sitios pueden asignarse a un área. Si no ninguna área configurada, AEM utiliza el área principal para esta marca específica.

En el diagrama siguiente se muestra un ejemplo de cómo funciona la lógica para tres sitios, llamados site1, site2 y site3.

![Estructura multisitio en los sitios](/help/sites-cloud/authoring/assets/multisite-structure-2.png)

* El sitio site1 busca myarea1 para brand1 y otherarea2 para brand2 en función de la asignación de áreas.
* El sitio site2 busca myarea1 para brand1 y el área principal para brand2, dado que solo está definida la asignación de áreas para brand1.
* El sitio site3 busca el área principal para brand1 y brand2, ya que no se ha definido ninguna otra asignación de área para este sitio.
