---
title: Notas de la versión 2025.02.17 del editor universal
description: Estas son las notas de la versión 2025.02.17 del editor universal.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: af04ad7e3f89247580c48c276cb371d78ac56a49
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 22%

---


# Notas de la versión 2025.02.17 del editor universal {#release-notes}

Estas son las notas de la versión del editor universal del 17 de febrero de 2025.

>[!TIP]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Novedades {#what-is-new}

* **Publicar para vista previa**: al publicar (o cancelar la publicación) del contenido mediante el Editor universal, puede elegir si desea publicar en el entorno de vista previa además del entorno de publicación
   * Esto permite revisar el contenido antes de publicarlo.
* **El modelo y el filtro se pueden definir en la definición del componente**. Ahora puede definir qué modelo y filtro utiliza un componente en la definición del componente.
   * Esta información se puede mantener de forma centralizada en la definición y no necesita especificarse en la instrumentación.
   * Esto le permite mover componentes entre contenedores.
* **Los elementos secundarios de los contenedores se consideran implícitamente componentes**. Si un elemento con un `data-aue-resource` se coloca como elemento secundario directo en un contenedor, se considera un componente y se puede mover sin tener que especificar `data-aue-behavior="component"`.

## Otras mejoras {#other-improvements}

* **Selector de recursos de AEM 6.5**: el selector de recursos de 6.5 ahora se abre correctamente al ejecutar el Editor universal con AEM 6.5.

