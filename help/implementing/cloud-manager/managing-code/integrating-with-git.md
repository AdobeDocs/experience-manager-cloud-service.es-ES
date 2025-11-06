---
title: Uso de Git con Cloud Manager
description: Obtenga información sobre cómo utilizar los repositorios de Git de Cloud Manager y cómo integrar su propio repositorio de Git administrado por los clientes con Cloud Manager.
exl-id: 57e71b8a-4546-4d7f-825c-a1637d08e608
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 100%

---

# Uso de Git con Cloud Manager {#git-integration}

Adobe Cloud Manager incluye un único repositorio de Git que se utiliza para implementar código mediante las canalizaciones de CI/CD de Cloud Manager.

Puede utilizar el repositorio de Git de Cloud Manager de forma predeterminada, pero también tiene la opción de integrar un repositorio de Git administrado por el cliente con Cloud Manager.

## Información general sobre la integración de Git {#git-integration-overview}

Esta serie de vídeos explora varios casos prácticos al integrar un repositorio de Git administrado por el cliente con Cloud Manager, incluidos los siguientes:

* [Sincronización inicial](#initial-sync)
* [Estrategia básica de ramas](#branching-strategy)
* [Desarrollo de ramas de características](#feature-development)
* [Implementación de producción](#production-deployment)
* [Sincronización de etiquetas de versión](#sync-tags)

Los vídeos asumen un conocimiento básico de la administración de Git y el control de fuentes. Consulte los [siguientes recursos adicionales](#additional-resources) para obtener más información sobre Git.

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

Los pasos y las convenciones de nomenclatura descritos en estos vídeos representan algunas prácticas recomendadas para trabajar con un repositorio de Git administrado por el cliente en Cloud Manager. Se espera que las convenciones y flujos de trabajo representados se adapten a los casos de uso individuales.

## Sincronización inicial {#initial-sync}

En este vídeo, aprenderá los primeros pasos para sincronizar un repositorio Git administrado por el cliente con el repositorio Git de Cloud Manager.

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## Estrategia básica de ramas {#branching-strategy}

En este vídeo, aprenderá estrategias básicas de ramificación.

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## Desarrollo de ramas de funciones {#feature-development}

Utilice una rama de funciones para aislar los cambios de código en un repositorio de Git administrado por el cliente y sincronizar con el repositorio de Git de Cloud Manager para utilizar una canalización que no sea de producción para las pruebas de calidad y validación del código.

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## Implementación de producción {#production-deployment}

Prepare el código para una versión de producción en un repositorio de Git administrado por el cliente y sincronícelo con el repositorio de Git de Cloud Manager para poder implementarlo en entornos de ensayo y producción.

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## Sincronización de etiquetas de versión {#sync-tags}

Sincronice las etiquetas de versión de un repositorio de Git de Cloud Manager en un repositorio de Git administrado por el cliente para dar visibilidad al código que se ha implementado en los entornos de ensayo y producción.

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## Recursos adicionales {#additional-resources}

* [Recursos de GitHub](https://docs.github.com/es/get-started/getting-started-with-git/set-up-git)
* [Tutoriales de Atlassian Git](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Hoja de Git Cheat](https://education.github.com/git-cheat-sheet-education.pdf)
