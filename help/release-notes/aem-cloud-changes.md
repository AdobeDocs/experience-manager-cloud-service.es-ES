---
title: Cambios importantes en Adobe Experience Manager (AEM) as a Cloud Service
description: Cambios importantes en Adobe Experience Manager (AEM) as a Cloud Service
exl-id: fe11d779-66cd-45aa-aa6b-c819b88d2405
source-git-commit: d3208a9a0785909e9b62d4033437a8ff44f7ba3e
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 84%

---

# Cambios importantes en Adobe Experience Manager (AEM) as a Cloud Service {#notable-changes-aem-cloud}

AEM Cloud Service ofrece muchas funciones y posibilidades nuevas para la gestión de sus proyectos de AEM. Sin embargo, existen varias diferencias entre AEM Sites local o como Adobe Managed Service en comparación con AEM Cloud Service. Este documento destaca las diferencias fundamentales.

>[!CONTEXTUALHELP]
>id="aem_cloud_notable_changes"
>title="Cambios importantes en AEM as a Cloud Service"
>abstract="En esta pestaña, puede ver contenido que le ayudará a comprender las diferencias entre AEM local o en Adobe Managed Services, en comparación con AEM as a Cloud Service."
>additional-url="https://video.tv.adobe.com/v/330543" text="Evolución de AEM as a Cloud Service"


>[!NOTE]
>En este documento se destacan los cambios más importantes que se han producido en AEM en su conjunto. Para obtener más información y ver los cambios específicos de la solución, consulte:
>
>* [Introducción a Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md)
>* [Novedades y diferencias](/help/overview/what-is-new-and-different.md) entre Adobe Experience Manager as a Cloud Service y las versiones anteriores
>* La [arquitectura](/help/overview/architecture.md) de Adobe Experience Manager as a Cloud Service
>* [Cambios importantes en AEM Sites as a Cloud Service](/help/sites-cloud/sites-cloud-changes.md)
>* [Cambios importantes en AEM Assets as a Cloud Service](/help/assets/assets-cloud-changes.md)


Las principales diferencias se encuentran en las siguientes áreas:

* [/apps y /libs son inmutables en tiempo de ejecución](#apps-libs-immutable)

* [Los paquetes y configuraciones de OSGi deben tratarse como código](#osgi)

* [No se permiten los cambios en el repositorio de publicación](#changes-to-publish-repo)

* [No se permiten los modos de ejecución personalizados](#custom-runmodes)

* [Eliminación de agentes de replicación y cambios relacionados](#replication-agents)

* [Eliminación de la IU clásica](#classic-ui)

* [Entrega en el lado de publicación ](#publish-side-delivery)

* [Administración y entrega de recursos](#asset-handling)

## /apps y /libs son inmutables en tiempo de ejecución {#apps-libs-immutable}

Cualquier contenido y carpetas secundarias de `/apps` y `/libs` son de solo lectura. Cualquier función o código personalizados que deba realizar cambios allí no podrá hacerlo. Se muestra un error que indica que dicho contenido es de solo lectura y que la operación de escritura no se pudo completar. Esto afecta a varias áreas de AEM:

* No se permite ningún cambio en `/libs`.
   * Esta regla no es nueva, pero no se aplicaba en versiones anteriores locales de AEM.
* Superposiciones en áreas `/libs` que pueden superponerse siguen estando permitidas en `/apps`.
   * Estas superposiciones deben proceder de Git a través de la canalización CI/CD.
* La información de diseño de plantilla estática almacenada en `/apps` no se puede editar mediante la interfaz de usuario.
   * En su lugar, se recomienda utilizar plantillas editables.
   * Si las plantillas estáticas siguen siendo necesarias, la información de configuración debe proceder de Git a través de la canalización CI/CD.
* El modelo MSM y las configuraciones de implementación MSM personalizadas deben instalarse desde Git a través de la canalización CI/CD.
* Los cambios en la traducción y localización deben proceder de Git a través de la canalización CI/CD.

## Los paquetes y configuraciones de OSGi deben tratarse como código {#osgi}

Los cambios en los paquetes y configuraciones de OSGi deben introducirse a través de la canalización CI/CD.

* Los paquetes OSGi nuevos o actualizados deben introducirse a través de Git a través de la canalización CI/CD.
* Los cambios en las configuraciones de OSGi solo pueden proceder de Git a través de la canalización CI/CD.

La consola web, utilizada en versiones anteriores de AEM para cambiar paquetes y configuraciones de OSGi, no está disponible en AEM Cloud Service.

## No se permiten los cambios en el repositorio de publicación {#changes-to-publish-repo}

Además de los cambios en la carpeta `/home` en el nivel de publicación, no se permiten cambios directos en el repositorio de publicación en AEM Cloud Service. En versiones anteriores de AEM locales o AEM en AMS, los cambios de código se podían realizar directamente en el repositorio de publicación. Algunas limitaciones se pueden mitigar de las siguientes maneras:

* Para la configuración de contenido o basada en contenido: realice los cambios en la instancia de creación y publíquelos.
* Para el código y la configuración: realice los cambios en el repositorio de GIT y ejecute la canalización CI/CD para implementarlos.

## No se permiten los modos de ejecución personalizados {#custom-runmodes}

Se proporcionan los siguientes modos de ejecución predeterminados para AEM Cloud Service:

* `author`
* `publish`
* `prod`
* `author.prod`
* `publish.prod`
* `stage`
* `author.stage`
* `publish.stage`
* `dev`
* `author.dev`
* `publish.dev`

Los modos de ejecución adicionales o personalizados no son compatibles en AEM Cloud Service.

## Eliminación de agentes de replicación y cambios relacionados {#replication-agents}

En AEM Cloud Service, el contenido se publica mediante [Sling Content Distribution](https://sling.apache.org/documentation/bundles/content-distribution.html). Los agentes de replicación utilizados en versiones anteriores de AEM ya no se utilizan ni se proporcionan, lo que podría afectar a las siguientes áreas de los proyectos de AEM existentes:

* Flujos de trabajo personalizados que llevan contenido a los agentes de replicación de los servidores de vista previa, por ejemplo.
* Personalización a agentes de replicación para transformar contenido.
* Uso de la replicación inversa para devolver el contenido de la publicación al creador.

Además, tenga en cuenta que los botones de pausa y desactivación se han eliminado de la consola de administración del agente de replicación.

## Eliminación de la IU clásica {#classic-ui}

La IU clásica ya no está disponible en AEM Cloud Service.

## Entrega en el lado de publicación {#publish-side-delivery}

La aceleración HTTP, incluida la CDN y la administración de tráfico para los servicios de creación y publicación, se proporcionan de forma predeterminada en AEM Cloud Service.

Para la transición de proyectos desde AMS o una instalación local, Adobe recomienda aprovechar la CDN integrada, ya que las funciones del AEM Cloud Service están optimizadas para la CDN proporcionada.

## Administración y entrega de recursos {#asset-handling}

La carga, el procesamiento y la descarga de recursos están optimizados en [!DNL Experience Manager Assets] como [!DNL Cloud Service]. [!DNL Assets] ahora es más eficiente, permite un mayor escalado, y cargar y descargar a una velocidad mucho más rápida. Además, afecta al código personalizado existente y a algunas operaciones. Para ver una lista de cambios y para la paridad con [!DNL Experience Manager] 6.5, consulte [cambios en [!DNL Assets]](/help/assets/assets-cloud-changes.md).
