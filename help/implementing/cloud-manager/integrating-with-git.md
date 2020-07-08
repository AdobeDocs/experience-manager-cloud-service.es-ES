---
title: Integración con Git
description: 'Integración con Git: Cloud Service'
translation-type: tm+mt
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 2%

---


# Integrar Git con Adobe Cloud Manager {#git-integration}

Adobe Cloud Manager se suministra con un único repositorio de Git que se utiliza para implementar código mediante las canalizaciones CI/CD de Cloud Manager. Los clientes pueden utilizar el repositorio de Git del Administrador de nube de forma predeterminada. Los clientes también tienen la opción de integrar un repositorio Git local o gestionado por el **cliente** con Cloud Manager.

## Información general sobre la integración de Git {#git-integration-overview}

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

Esta serie de vídeos explora varios casos de uso cuando se trata de integrar un repositorio Git administrado por el cliente con Cloud Manager, incluidos:

* [Sincronización inicial](#initial-sync)
* [Estrategia básica de ramas](#branching-strategy)
* [Desarrollo de ramas de funciones](#feature-development)
* [Implementación de producción](#production-deployment)
* [Sincronización de etiquetas de versión](#sync-tags)

La serie de vídeos asume un conocimiento básico de la gestión de la entrada y el control de fuentes. Consulte los recursos [adicionales a continuación](#additional-resources) para obtener más detalles sobre Git.

>[!NOTE]
>
>Los pasos y las convenciones de nombres que se describen en esta serie de vídeos representan algunas prácticas recomendadas para trabajar con un repositorio Git gestionado por el cliente y con Cloud Manager. Se espera que los convenios y flujos de trabajo descritos se adapten a los distintos equipos de desarrollo.

## Sincronización inicial {#initial-sync}

Primeros pasos para sincronizar un repositorio Git administrado por el cliente con el repositorio Git de Cloud Manager.

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## Estrategia básica de ramas {#branching-strategy}

Siga el siguiente vídeo para conocer las estrategias básicas de ramificación.

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## Desarrollo de ramas de funciones {#feature-development}

Utilice una rama de funciones para aislar los cambios de código en un repositorio Git gestionado por el cliente y sincronizar con el repositorio Git de Cloud Manager para utilizar una canalización que no sea de producción para la calidad del código y las pruebas de validación.

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## Implementación de producción {#production-deployment}

Prepare el código para una versión de producción en un repositorio de Git gestionado por el cliente y sincronícelo con el repositorio de Git de Cloud Manager para implementarlo en entornos de producción y ensayo.

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## Sincronización de etiquetas de versión {#sync-tags}

Sincronice las etiquetas de lanzamiento de un repositorio de Git de Cloud Manager con un repositorio de Git gestionado por el cliente para proporcionar visibilidad sobre qué código se ha implementado en los entornos de ensayo y producción.

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## Recursos adicionales {#additional-resources}

* [Recursos de GitHub](https://try.github.io)
* [Tutoriales de Atlassian Git](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Hoja de Chrome de Git](https://education.github.com/git-cheat-sheet-education.pdf)