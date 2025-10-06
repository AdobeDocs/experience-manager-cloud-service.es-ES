---
title: Cambios importantes en AEM Sites en AEM Cloud Service
description: Descubra cómo crear contenido y administrar AEM Sites as a Cloud Service, así como los cambios importantes en AEM Sites en AEM Cloud Service.
exl-id: 60b1aec4-75a0-459f-bf77-8d8c1af757ce
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 3761019b42ddc4b3a6cc904afe91b47eb3d99ac6
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 97%

---


# Cambios importantes en AEM Sites as a Cloud Service {#notable-changes}

AEM Sites as a Cloud Service proporciona funciones de administración de experiencias como parte de la plataforma nativa de la nube de AEM as a Cloud Service. Además de las ventajas principales de AEM as a Cloud Service, como la escalabilidad nativa de la nube, el tiempo de actividad y estar siempre actualizado, AEM Sites as a Cloud Service también proporciona varios cambios y adiciones específicos de sitios.

>[!NOTE]
>Este documento destaca los cambios más importantes que se han producido en AEM Sites. Para ver los cambios generales en AEM as a Cloud Service y otros módulos, consulte:
>
>* [Introducción a Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md)
>* Una [descripción general de AEM as a Cloud Service: novedades y diferencias](/help/overview/what-is-new-and-different.md)
>* La [arquitectura](/help/overview/architecture.md) de Adobe Experience Manager as a Cloud Service
>* [Cambios importantes en AEM as a Cloud Service (Notas de la versión)](/help/release-notes/aem-cloud-changes.md)
>* [Cambios importantes en AEM Assets as a Cloud Service](/help/assets/assets-cloud-changes.md)
>* [Presentación de AEM Assets as a Cloud Service](/help/assets/overview.md)
>* [Tutoriales de Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html?lang=es)

Los cambios y adiciones en AEM Sites as a Cloud Service son los siguientes:

* [Operaciones asincrónicas de página](#asynchronous-page-operations)
* [Nuevo sitio de referencia y tutorial](#new-reference-site-and-tutorial)

## Operaciones asincrónicas de página {#asynchronous-page-operations}

En AEM Cloud Service, las operaciones que tradicionalmente bloquean la interfaz de usuario se han desglosado en tareas más pequeñas que se ejecutan en segundo plano.

* Mover páginas
* Desplegar páginas

<!--
The initiator of such actions can check their status in a new UI at `/mnt/overlay/dam/gui/content/asyncjobs.html`.
-->

Puede ver el estado de los trabajos asincrónicos desde el [tablero Operaciones en segundo plano](/help/operations/asynchronous-jobs.md).

>[!NOTE]
>
>El usuario del sistema no necesita hacer ningún cambio para utilizar esta nueva función. Se observa aquí simplemente como un cambio en el comportamiento con respecto a versiones locales anteriores de AEM.

## Nuevo sitio de referencia y tutorial {#new-reference-site-and-tutorial}

[WKND](https://wknd.site/), un nuevo sitio de referencia de AEM, se ha actualizado y publicado para reflejar las prácticas recomendadas para generar un sitio web con AEM, así como el conjunto completo de funcionalidades, componentes y modelos de implementación disponibles en AEM. El nuevo sitio de referencia y el [tutorial complementario](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=es) cubren temas fundamentales como la configuración del proyecto, los componentes principales, las plantillas editables, las bibliotecas de cliente y el desarrollo de componentes con Adobe Experience Manager Sites.

Anteriormente, We.Retail se instalaba de forma predeterminada con AEM (excepto cuando se iniciaba en el modo de producción). En AEM as a Cloud Service, un sitio de referencia no está instalado de forma predeterminada. En su lugar, se proporcionan el [repositorio de Git](https://github.com/adobe/aem-guides-wknd/) y el [tutorial complementario](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=es) con el código de sitio de referencia WKND actualizado.

## Funciones no disponibles durante la ejecución {#capabilities-not-available-at-runtime}

AEM as a Cloud Service siempre está activado y actualizado. Para lograrlo, es necesario separar el repositorio de AEM en contenido inmutable y mutable, y prohibir el acceso a contenido inmutable durante la ejecución. Para obtener más información sobre el contenido mutable e inmutable, consulte [Áreas mutables e inmutables del repositorio](/help/implementing/developing/introduction/aem-project-content-package-structure.md#mutable-vs-immutable).

Como el contenido inmutable no es accesible durante la ejecución, las siguientes operaciones de AEM Sites no están disponibles durante la ejecución:

* Traducción con diccionarios i18n
* Modo de desarrollador en el editor de páginas de AEM Sites

Estas funcionalidades se pueden utilizar a través de instancias de desarrollador locales independientes de AEM as a Cloud Service para actualizar contenido y código en el repositorio de Git de AEM as a Cloud Service, pero no en instancias de tiempo de ejecución alojadas.
