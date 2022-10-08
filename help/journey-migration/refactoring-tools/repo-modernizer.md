---
title: Modernizador de repositorio
description: Modernizador de repositorio
exl-id: cd9d212e-e720-4209-8b5a-659883cc1d95
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 12%

---

# Modernizador de repositorio {#repo-modernizer}

Modernizador de repositorio es una utilidad desarrollada para reestructurar paquetes de proyectos existentes separando contenido y código en paquetes discretos para que sean compatibles con la estructura de proyectos definida para Adobe Experience Manager as a Cloud Service.

## Introducción {#introduction}

Adobe Experience Manager as a Cloud Service ofrece muchas nuevas funciones y posibilidades en sus proyectos AEM. Con todo, se requieren algunos cambios en los proyectos de Adobe Experience Manager Maven para que sean compatibles con AEM Cloud Service. En un nivel superior, AEM requiere una separación de **contenido** y **code** en subpaquetes discretos para respetar la división entre contenido mutable e inmutable. Consulte [AEM estructura del proyecto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=es) para obtener más información sobre la nueva estructura del proyecto AEM para Cloud Service.

El Modernizador de repositorio crea una estructura de proyecto de AEM Cloud Service compatible creando la siguiente estructura de implementación:

* `ui.apps` implementación de paquetes a `/apps` y contiene todo el código

* `ui.content` implementaciones de paquetes en áreas de tiempo de ejecución (por ejemplo, `/content`, `/conf`, `/home`, o cualquier cosa que no sea `/apps`) y contiene todo el contenido y la configuración.

* `all` es un paquete de contenedor que contiene los subpaquetes `ui.apps` y `ui.content`.

>[!NOTE]
>La estructura del proyecto se basa en *Tipo de archivo 24* para paquetes y sus `pom.xml/filter.xml files`. Consulte [Tipo de archivo 24](https://github.com/adobe/aem-project-archetype) para obtener más información.

## Uso del Modernizador de repositorio {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/333057/?quality=12&learn=on)

* A través de la CLI de Adobe I/O : Se recomienda utilizar el Modernizador de repositorio mediante `aio-cli-plugin-aem-cloud-service-migration` (AEM complemento de refactorización de código as a Cloud Service para la CLI de Adobe I/O).

   Consulte **[Recurso de Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** para aprender a instalar y utilizar el complemento.

* Como utilidad independiente: El Modernizador de repositorio también se puede ejecutar como una utilidad independiente.

   Consulte **[Recurso de Git: Modernizador de repositorio](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)** para aprender a utilizar esta herramienta.

   >[!NOTE]
   >
   >El Modernizador de repositorio se desarrolla mediante NodeJS. Se recomienda tener instalado NodeJS 10.0+.
