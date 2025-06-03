---
title: Modernizador de repositorio
description: Aprenda a reestructurar los paquetes de proyectos existentes y a hacerlos compatibles con la estructura de proyectos definida para Adobe Experience Manager as a Cloud Service.
exl-id: cd9d212e-e720-4209-8b5a-659883cc1d95
feature: Migration
role: Admin
source-git-commit: 6920651420da9b427510518b7add0637479adef5
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 8%

---

# Modernizador de repositorio {#repo-modernizer}

Repository Modernizer es una utilidad desarrollada para reestructurar los paquetes de proyectos existentes separando contenido y código en paquetes discretos para que sean compatibles con la estructura de proyectos definida para Adobe Experience Manager as a Cloud Service.

## Introducción {#introduction}

Adobe Experience Manager as a Cloud Service ofrece muchas nuevas funciones y posibilidades para sus proyectos de AEM. Con todo, se requieren algunos cambios en los proyectos de Adobe Experience Manager Maven para que sean compatibles con AEM Cloud Service. En un nivel superior, AEM requiere una separación de **content** y **code** en subpaquetes discretos para respetar la división entre contenido mutable e inmutable. Consulte [Estructura del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=es) para obtener más información sobre la nueva estructura del proyecto AEM para Cloud Service.

El Modernizador de repositorio crea una estructura de proyecto de AEM Cloud Service compatible mediante la creación de la siguiente estructura de implementación:

* El paquete `ui.apps` se implementa en `/apps` y contiene todo el código

* El paquete `ui.content` se implementa en áreas en tiempo de ejecución modificables (por ejemplo, `/content`, `/conf`, `/home` o cualquier elemento que no sea `/apps`) y contiene todo el contenido y la configuración.

* El paquete `all` es un paquete contenedor que contiene los subpaquetes `ui.apps` y `ui.content`.

>[!NOTE]
>
>La estructura del proyecto se basa en *tipo de archivo 24* para los paquetes y sus `pom.xml/filter.xml files`. Consulte [Tipo de archivo 24](https://github.com/adobe/aem-project-archetype) para obtener más información.

## Uso del Modernizador de repositorio {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/3412958/?quality=12&learn=on&captions=spa)

* A través de Adobe I/O CLI : Adobe recomienda utilizar el Modernizador de repositorio mediante `aio-cli-plugin-aem-cloud-service-migration` (complemento de refactorización de código AEM as a Cloud Service para Adobe I/O CLI).

  Consulte **[Recurso de Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** para obtener información sobre cómo instalar y utilizar el complemento.

* Como utilidad independiente : El Modernizador de repositorios también se puede ejecutar como utilidad independiente.

  Consulte **[Recurso Git: Modernizador de repositorio](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)** para que pueda aprender a usar esta herramienta.

  >[!NOTE]
  >
  >El Modernizador de repositorio se desarrolla mediante NodeJS. Se recomienda tener instalado NodeJS 10.0+.
