---
title: Modernizador de repositorio
description: Aprenda a reestructurar los paquetes de proyectos existentes y a hacerlos compatibles con la estructura de proyectos definida para Adobe Experience Manager as a Cloud Service.
exl-id: cd9d212e-e720-4209-8b5a-659883cc1d95
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 16%

---

# Modernizador de repositorio {#repo-modernizer}

Repository Modernizer es una utilidad desarrollada para reestructurar los paquetes de proyectos existentes separando contenido y código en paquetes discretos para que sean compatibles con la estructura de proyectos definida para Adobe Experience Manager as a Cloud Service.

## Introducción {#introduction}

Adobe Experience Manager as a Cloud Service ofrece muchas nuevas funciones y posibilidades para sus Proyectos AEM. Con todo, se requieren algunos cambios en los proyectos de Adobe Experience Manager Maven para que sean compatibles con AEM Cloud Service. AEM En un nivel elevado, la separación de las funciones requiere, por lo tanto, la separación de las funciones de la **content** y **código** en subpaquetes discretos para respetar la división entre contenido mutable e inmutable. Consulte [AEM Estructura del proyecto de](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=es) AEM para obtener más información sobre la nueva estructura de proyecto de la para Cloud Service.

El Modernizador de repositorio crea una estructura de proyecto de AEM Cloud Service compatible mediante la creación de la siguiente estructura de implementación:

* `ui.apps` el paquete se implementa en `/apps` y contiene todo el código

* `ui.content` El paquete de se implementa en áreas de tiempo de ejecución grabables (por ejemplo, `/content`, `/conf`, `/home`, o cualquier cosa que no `/apps`), y contiene todo el contenido y la configuración.

* `all` es un paquete de contenedor que contiene los subpaquetes `ui.apps` y `ui.content`.

>[!NOTE]
>La estructura del proyecto se basa en *Arquetipo 24* para paquetes y sus `pom.xml/filter.xml files`. Consulte [Arquetipo 24](https://github.com/adobe/aem-project-archetype) para obtener más información.

## Uso del Modernizador de repositorio {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/333057/?quality=12&learn=on)

* A través de CLI de Adobe I/O : Adobe recomienda utilizar el Modernizador de repositorio mediante `aio-cli-plugin-aem-cloud-service-migration` AEM (complemento de refactorización de código as a Cloud Service para la CLI de Adobe I/O).

  Consulte **[Recurso de Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** para que pueda aprender a instalar y utilizar el complemento.

* Como utilidad independiente : El Modernizador de repositorios también se puede ejecutar como utilidad independiente.

  Consulte **[Recurso de Git: Modernizador de repositorio](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)** para que pueda aprender a utilizar esta herramienta.

  >[!NOTE]
  >
  >El Modernizador de repositorio se desarrolla mediante NodeJS. Se recomienda tener instalado NodeJS 10.0+.
