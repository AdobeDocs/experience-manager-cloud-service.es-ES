---
title: Cambios notables en los sitios de AEM en el servicio de nube de AEM
description: 'Cambios notables en los sitios de AEM en el servicio de nube de AEM '
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Cambios notables en los sitios de AEM como servicio de nube {#notable-changes}

AEM Sites como servicio de nube ofrece funciones de gestión de experiencias como parte de AEM nativo de la nube como plataforma de servicio de nube. Además de las ventajas principales de AEM como servicio de nube, como la escalabilidad nativa de la nube, el tiempo de actividad y el estar siempre actualizado, AEM Sites como servicio de nube también ofrece una serie de cambios y adiciones específicos de sitios.

>[!NOTE]
>Este documento resalta los cambios más notables en los sitios de AEM. Para ver los cambios generales de AEM en la nube, consulte:
>
>* [Cambios notables en Adobe Experience Manager (AEM) como servicio de nube](/help/release-notes/aem-cloud-changes.md)


Los cambios y las adiciones en AEM Sites como servicio de nube son los siguientes:

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

[WKND](https://wknd.site/), un nuevo sitio de referencia de AEM, se ha actualizado y publicado para reflejar las prácticas recomendadas para crear un sitio web con AEM, así como el conjunto completo de funciones, componentes y modelos de implementación disponibles en AEM. El nuevo sitio de referencia y el tutorial [que lo](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) acompaña abarcan temas fundamentales como la configuración de proyectos, componentes principales, plantillas editables, bibliotecas de clientes y desarrollo de componentes con sitios de Adobe Experience Manager.

Anteriormente, We.Retail se instalaba de forma predeterminada con AEM (excepto cuando se iniciaba en modo de producción).  Ahora, un sitio de referencia no se instalará de forma predeterminada a partir de ahora.  En su lugar, se proporciona la repo [git](https://github.com/adobe/aem-guides-wknd/) y el tutorial [que la](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) acompaña con el código de sitio de referencia WKND actualizado.

## Capacidades no disponibles en tiempo de ejecución {#capabilities-not-available-at-runtime}

AEM como servicio de nube siempre está activado y siempre actualizado. Para lograrlo, es necesario separar el repositorio de AEM en contenido inmutable y mutable, y prohibir el acceso a contenido inmutable durante la ejecución. Para obtener más información sobre el contenido mutable vs. inmutable, consulte [Áreas mutables vs. inmutables del repositorio](/help/implementing/developing/introduction/aem-project-content-package-structure.md#mutable-vs-immutable).

Debido a que el contenido inmutable no es accesible durante la ejecución, las siguientes operaciones de AEM Sites no están disponibles en tiempo de ejecución:

* Traducción del diccionario i18n
* Modo de desarrollador en el Editor de páginas de AEM Sites

Estas funciones se pueden utilizar a través de instancias de desarrollador locales independientes de AEM como servicio de nube para actualizar contenido y código en AEM como repositorio de GIT de servicio de nube, pero no en instancias de tiempo de ejecución alojadas.
