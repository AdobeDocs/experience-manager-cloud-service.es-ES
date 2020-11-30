---
title: Cambios importantes en AEM Sites en AEM Cloud Service
description: 'Cambios importantes en AEM Sites en AEM Cloud Service '
translation-type: tm+mt
source-git-commit: e381807d7c199113689304e9481dfe2022ee5f93
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 21%

---


# Cambios importantes en AEM Sites as a Cloud Service {#notable-changes}

AEM Sites como Cloud Service ofrece funciones de administración de experiencia como parte de la AEM nativa de la nube como plataforma Cloud Service. Además de los beneficios principales de AEM como Cloud Service, como escalabilidad nativa de la nube, tiempo activo y estar siempre actualizado, AEM Sites como Cloud Service también proporciona una serie de cambios y adiciones específicos del sitio.

>[!NOTE]
>Este documento destaca los cambios notables que se han producido en AEM Sites. Para ver los cambios generales a AEM como Cloud Service y otros módulos, consulte:
>
>* [Introducción a Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md)
>* Una [descripción general de AEM as a Cloud Service: novedades y diferencias](/help/overview/what-is-new-and-different.md)
>* La [arquitectura](/help/core-concepts/architecture.md) de Adobe Experience Manager as a Cloud Service
>* [Cambios importantes en AEM as a Cloud Service (Notas de la versión)](/help/release-notes/aem-cloud-changes.md)
>* [Cambios importantes en AEM Assets as a Cloud Service](/help/assets/assets-cloud-changes.md)
>* [Introducción a AEM Assets como Cloud Service](/help/assets/overview.md)
>* [Tutoriales de Adobe Experience Manager as a Cloud Service](https://docs.adobe.com/content/help/es-ES/experience-manager-learn/cloud-service/overview.html)


Los cambios y adiciones en AEM Sites como Cloud Service son los siguientes:

* [Operaciones de página asincrónicas](#asynchronous-page-operations)
* [Nuevo sitio de referencia y tutorial](#new-reference-site-and-tutorial)

## Operaciones de página asincrónicas {#asynchronous-page-operations}

En AEM servicio de nube, las operaciones que tradicionalmente han bloqueado la interfaz de usuario se han desglosado en tareas más pequeñas que se ejecutan en segundo plano.

* Mover páginas
* Páginas de despliegue

El iniciador de estas acciones puede comprobar su estado en una nueva interfaz de usuario en `/mnt/overlay/dam/gui/content/asyncjobs.html`.

>[!NOTE]
>
>El usuario del sistema no necesita realizar ningún cambio para utilizar esta nueva función. Se observa aquí simplemente como un cambio en el comportamiento con respecto a versiones anteriores in situ de AEM.

## Nuevo sitio de referencia y tutorial {#new-reference-site-and-tutorial}

[WKND](https://wknd.site/), un nuevo sitio de referencia de AEM, se ha actualizado y publicado para reflejar las prácticas recomendadas para crear un sitio web con AEM, así como el conjunto completo de funciones, componentes y modelos de implementación disponibles en AEM. El nuevo sitio de referencia y el tutorial [que lo](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) acompaña abarcan temas fundamentales como la configuración del proyecto, los componentes principales, las plantillas editables, las bibliotecas de clientes y el desarrollo de componentes con Adobe Experience Manager Sites.

Anteriormente, We.Retail se instalaba de forma predeterminada con AEM (excepto cuando se iniciaba en modo de producción).  Ahora, un sitio de referencia no se instalará de forma predeterminada a partir de ahora.  En su lugar, se proporciona la repo [git](https://github.com/adobe/aem-guides-wknd/) y el tutorial [que la](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) acompaña con el código de sitio de referencia WKND actualizado.

## Capacidades no disponibles en tiempo de ejecución {#capabilities-not-available-at-runtime}

AEM como Cloud Service siempre está activado y siempre actualizado. Para lograrlo, es necesario separar el repositorio de AEM en contenido inmutable y mutable, y prohibir el acceso a contenido inmutable en tiempo de ejecución. Para obtener más información sobre el contenido mutable vs. inmutable, consulte [Áreas mutables vs. inmutables del repositorio](/help/implementing/developing/introduction/aem-project-content-package-structure.md#mutable-vs-immutable).

Como resultado de que el contenido inmutable no es accesible en tiempo de ejecución, las siguientes operaciones de AEM Sites no están disponibles en tiempo de ejecución:

* Traducción del diccionario i18n
* Modo de desarrollador en el Editor de páginas de AEM Sites

Estas funciones se pueden utilizar a través de instancias de desarrollador locales independientes de AEM como Cloud Service para actualizar contenido y código en el AEM como repositorio GIT Cloud Service, pero no en instancias de tiempo de ejecución alojadas.
