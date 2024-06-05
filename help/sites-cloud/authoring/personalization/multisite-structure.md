---
title: Estructurar la administración de diversos sitios para el contenido segmentado
description: Un diagrama muestra cómo se estructura la compatibilidad con varios sitios para el contenido de destino
exl-id: c6b05c2a-0897-4514-8937-e23bfcf757d5
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 39%

---

# Estructurar la administración de diversos sitios para el contenido segmentado {#how-multisite-management-for-targeted-content-is-structured}

El diagrama siguiente muestra cómo se estructura la compatibilidad con varios sitios para el contenido de destino.

Las áreas aparecen debajo de **/content/campaigns/&lt;brand>** y, de forma predeterminada, cada marca tiene un área principal, que se crea automáticamente. Cada área tiene su propio conjunto de actividades, experiencias y ofertas.

![Estructura de varios sitios](/help/sites-cloud/authoring/assets/multisite-structure.png)

Para buscar contenido de destino, las páginas o sitios pueden asignarse a un área. AEM Si no hay ningún área configurada, vuelve a la zona principal para esta marca específica.

En el diagrama siguiente se muestra un ejemplo de cómo funciona la lógica para tres sitios, llamados site1, site2 y site3.

![Estructura de varios sitios entre sitios](/help/sites-cloud/authoring/assets/multisite-structure-2.png)

* site1 busca myarea1 para brand1 y otherarea2 para brand2 en función de la asignación de áreas.
* site2 busca myarea1 para brand1 y área principal para brand2, ya que solo se define la asignación de área para brand1.
* site3 busca el área principal para brand1 y brand2, ya que no se ha definido ninguna otra asignación de área para este sitio.
