---
title: Cambios importantes en AEM Sites en AEM Cloud Service
description: 'Cambios importantes en AEM Sites en AEM Cloud Service '
translation-type: tm+mt
source-git-commit: e381807d7c199113689304e9481dfe2022ee5f93
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 16%

---


# Cambios importantes en AEM Sites as a Cloud Service {#notable-changes}

Los AEM Sites como Cloud Service proporcionan funciones de gestión de experiencias como parte de AEM nativo de la nube como plataforma de Cloud Service. Además de las ventajas principales de AEM como Cloud Service, como la escalabilidad nativa de la nube, el tiempo de actividad y el estar siempre actualizado, los AEM Sites como Cloud Service también proporcionan una serie de cambios y adiciones específicos de sitios.

>[!NOTE]
>Este documento destaca los cambios notables que se han producido en los AEM Sites. Para ver los cambios generales en AEM como Cloud Service y otros módulos, consulte:
>
>* [Introducción a Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md)
>* Una [descripción general de AEM como Cloud Service: novedades y diferencias](/help/overview/what-is-new-and-different.md)
>* La [arquitectura](/help/core-concepts/architecture.md) de Adobe Experience Manager as a Cloud Service
>* [Cambios notables en AEM como Cloud Service (Notas de la versión)](/help/release-notes/aem-cloud-changes.md)
>* [Cambios importantes en AEM Assets as a Cloud Service](/help/assets/assets-cloud-changes.md)
>* [Presentación de AEM Assets como Cloud Service](/help/assets/overview.md)
>* [Tutoriales de Adobe Experience Manager as a Cloud Service](https://docs.adobe.com/content/help/es-ES/experience-manager-learn/cloud-service/overview.html)


Los cambios y adiciones en AEM Sites como Cloud Service son los siguientes:

* [Operaciones de página asincrónicas](#asynchronous-page-operations)
* [Nuevo sitio de referencia y tutorial](#new-reference-site-and-tutorial)

## Operaciones de página asincrónicas {#asynchronous-page-operations}

En el servicio AEM Cloud, las operaciones que tradicionalmente han bloqueado la interfaz de usuario se han desglosado en tareas más pequeñas que se ejecutan en segundo plano.

* Mover páginas
* Páginas de despliegue

El iniciador de estas acciones puede comprobar su estado en una nueva interfaz de usuario en `/mnt/overlay/dam/gui/content/asyncjobs.html`.

>[!NOTE]
>
>El usuario del sistema no necesita realizar ningún cambio para utilizar esta nueva función. Se observa aquí simplemente como un cambio de comportamiento con respecto a versiones anteriores in situ de AEM.

## Nuevo sitio de referencia y tutorial {#new-reference-site-and-tutorial}

[WKND](https://wknd.site/), un nuevo sitio de referencia de AEM, se ha actualizado y publicado para reflejar las prácticas recomendadas para crear un sitio web con AEM, así como el conjunto completo de funciones, componentes y modelos de implementación disponibles en AEM. El nuevo sitio de referencia y el tutorial [que lo](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) acompaña abarcan temas fundamentales como la configuración del proyecto, los componentes principales, las plantillas editables, las bibliotecas de clientes y el desarrollo de componentes con sitios de Adobe Experience Manager.

Anteriormente, We.Retail se instalaba de forma predeterminada con AEM (excepto cuando se iniciaba en modo de producción).  Ahora, un sitio de referencia no se instalará de forma predeterminada a partir de ahora.  En su lugar, se proporciona la repo [git](https://github.com/adobe/aem-guides-wknd/) y el tutorial [que la](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) acompaña con el código de sitio de referencia WKND actualizado.

## Capacidades no disponibles en tiempo de ejecución {#capabilities-not-available-at-runtime}

AEM como Cloud Service siempre está activado y siempre actualizado. Para lograrlo, es necesario separar el repositorio de AEM en contenido inmutable y mutable, y prohibir el acceso a contenido inmutable durante la ejecución. Para obtener más información sobre el contenido mutable vs. inmutable, consulte [Áreas mutables vs. inmutables del repositorio](/help/implementing/developing/introduction/aem-project-content-package-structure.md#mutable-vs-immutable).

Como resultado de que el contenido inmutable no es accesible en tiempo de ejecución, las siguientes operaciones de AEM Sites no están disponibles en tiempo de ejecución:

* Traducción del diccionario i18n
* Modo de desarrollador en el Editor de páginas de AEM Sites

Estas funciones se pueden utilizar a través de instancias de desarrollador locales independientes de AEM como Cloud Service para actualizar contenido y código en AEM como repositorio GIT Cloud Service, pero no en instancias de tiempo de ejecución alojadas.
