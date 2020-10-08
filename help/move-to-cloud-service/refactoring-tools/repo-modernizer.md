---
title: Modernizador de repositorio
description: Modernizador de repositorio
translation-type: tm+mt
source-git-commit: 5da0d4cc8c6d8781dd7cce8bbbde207568a6d10b
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 4%

---


# Modernizador de repositorio {#repo-modernizer}

Repository Modernizer es una utilidad desarrollada para reestructurar los paquetes de proyectos existentes separando el contenido y el código en paquetes discretos para ser compatibles con la estructura de proyectos definida para Adobe Experience Manager como Cloud Service.

## Introducción {#introduction}

Adobe Experience Manager como Cloud Service aporta muchas nuevas funciones y posibilidades a sus proyectos AEM. Sin embargo, es necesario realizar algunos cambios en los proyectos de Adobe Experience Manager Maven para que sean compatibles con AEM Cloud Service. En un nivel superior, AEM requiere una separación de **contenido** y **código** en subpaquetes discretos para respetar la división entre contenido mutable e inmutable. Consulte [AEM Estructura](https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) del proyecto para obtener más detalles sobre la nueva estructura del proyecto AEM para Cloud Service.

El Modernizador de repositorio crea una estructura de proyecto AEM Cloud Service compatible creando la siguiente estructura de implementación:

* `ui.apps` se implementa en `/apps` y contiene todo el código

* `ui.content` se implementa en áreas de tiempo de ejecución (p. ej. `/content`, `/conf`, `/home`, o cualquier cosa que no `/apps`) y contiene todo el contenido y la configuración.

* `all` es un paquete de contenedor que contiene los subpaquetes `ui.apps` y `ui.content`.

>[!NOTE]
>La estructura del proyecto se basa en *Archetype 24* para paquetes y sus `pom.xml/filter.xml files`. Consulte [Archetype 24](https://github.com/adobe/aem-project-archetype) para obtener más información.

## Uso del modernizador de repositorio {#using-repo-modernizer}

* Mediante CLI de E/S de Adobe: Se recomienda utilizar el Modernizador de repositorio mediante `aio-cli-plugin-aem-cloud-service-migration` (AEM como un complemento de refactorización de código de Cloud Service para la CLI de E/S de Adobe).

   Consulte Recurso **[Git: aio-cli-plugin-aem-cloud-service-Migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** para aprender a instalar y utilizar el complemento.

* Como utilidad independiente: El Modernizador de repositorio también se puede ejecutar como una utilidad independiente.

   Consulte Recurso **[Git: Modernizador](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)** de repositorio para aprender a utilizar esta herramienta.

   >[!NOTE]
   >
   >El Modernizador de repositorio se desarrolla mediante NodeJS. Se recomienda tener instalado NodeJS 10.0 o posterior.
